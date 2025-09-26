---
title: "Building a high recall vector database serving 1 billion embeddings from a single machine"
source: "https://blog.wilsonl.in/corenn/"
author:
  - "[[Wilson Lin]]"
published: 2025-08-09
created: 2025-08-21
description: "Introduction to CoreNN, an open source vector database that scales to 1 billion vectors on a single machine with high recall and throughput."
tags:
  - "clippings"
---
In this 3-part series, I deep dive into vector search and [ANN](https://en.wikipedia.org/wiki/Nearest_neighbor_search#Approximation_methods) indexing, the limitations of scaling popular algorithms like HNSW, and how I built an open source vector DB for querying across billions of vectors on commodity machines, called [**CoreNN**](https://github.com/wilsonzlin/corenn). For example, here it is searching across 1 billion Reddit comment embeddings in 15 ms from a 4.8 TB index on disk—all time is spent embedding the query and fetching results:

<video src="./reddit-demo-30s.mp4" controls=""></video>

In the [first post](https://blog.wilsonl.in/graph-vector-search/), I laid out the problem of searching vectors efficiently and how graph algorithms like [HNSW](https://arxiv.org/abs/1603.09320) intuitively solve this problem. In the [second post](https://blog.wilsonl.in/diskann/), I discussed how such algorithms, while they're good at *building* fast and accurate indices, have shortcomings when trying to use them in real-world production use cases:

- They are in-memory. 1 billion 768-dim embeddings requires 2.8 TB of RAM.
- Loading and transporting this amount of data is not easy.
- Upserts/deletes are merely post-filtered [soft-deletes](https://en.wikipedia.org/wiki/Tombstone_\(programming\)), bloating the index.
- Inserts and mutations typically require a full rewrite.

In this post, I introduce [**CoreNN**](https://github.com/wilsonzlin/corenn), which aims to solve these problems:

- Uses cheap flash storage, not expensive DRAM, costing 40x–100x less.
- Seamlessly scales from 1 to 1 billion vectors in a single index.
- Upserts and deletes perform local graph optimizations, free space, maintain speed, and don't need full rewrites.
- Supports concurrent live queries and updates without blocking.

My motivation came from a large scale web search engine side project where efficiency and simplicity as a solo developer was important. CoreNN allowed me to scale down my cluster of sharded HNSW indices totalling 3 TB RAM into a single 96 GB RAM machine, with a much simpler update and query pipeline: no sharding across machines, continuous rebuilding, chunking, storing diffs, dynamically un/loading into memory, etc.

Unlike [other lossy approaches](https://github.com/facebookresearch/faiss) that result in high recall loss, CoreNN scales to billions of vectors with memory efficiency while still outperforming HNSW in accuracy, given the same parameters. It's built on top of the DiskANN ([see last post](https://blog.wilsonl.in/diskann/)) and [FreshDiskANN](https://arxiv.org/abs/2105.09613) papers, with some novel improvements. For example, on the GIST1M dataset, it achieves a higher recall using 2.5x fewer graph traversals:

[![](https://blog.wilsonl.in/corenn/gist-80M-query-ground-truth-found.webp)](https://blog.wilsonl.in/corenn/gist-80M-query-ground-truth-found.webp)

I also set out to make CoreNN as easy and ubiquitous to use as SQLite. It's a single binary with a simple REST API. It's also an embedded database that is available for Node.js, Python, and Rust, with more language bindings to come.

I recommend reading the previous posts in this series:

1. [From Kevin Bacon to HNSW: the intuition behind semantic search and vector databases](https://blog.wilsonl.in/graph-vector-search/)
2. [From 3 TB RAM to 96 GB: superseding billion vector HNSW with 40x cheaper DiskANN](https://blog.wilsonl.in/diskann/)
3. Building a high recall vector database serving 1 billion embeddings from a single machine

## CoreNN

As explored in the [last post](https://blog.wilsonl.in/diskann/), Vamana is a significant improvement over HNSW's shortcomings that makes it possible to query and serve large scale graph indices from disk. CoreNN puts Vamana into practice by using RocksDB as the backing persistent store for the graph, vectors, and other metadata.

Vectors are inserted with a key. For flexibility, arbitrary strings are accepted, and they're mapped to integer IDs internally. These integers are never reused, avoiding the complexity of correctly handling subtle race conditions across all parts of the system when an ID changes keys whilst querying or updating the graph. It also provides a total ordering of updates, which could come in handy for replication or streaming.

RocksDB is a robust, easy-to-use, fast KV database often used as the backing store for [many production systems](https://github.com/facebook/rocksdb/blob/main/USERS.md). LMDB was evaluated, but had large on-disk bloat (around 1.5-2x the size of the raw data, compared to RocksDB's 1x) and a mmap-based API that required an upfront allocation size and bumped into system resource limits.

The index used by CoreNN goes through two stages:

- Initially, all nodes and full vectors are cached in memory and used for queries. This provides full accuracy and fast performance. This is the *in-memory* stage.
- After running into memory limits, only compressed vectors are stored in memory, which moves the graph and full vectors to disk. Queries navigate the graph by reading nodes from the disk instead of memory. This is the *on-disk* stage, and what allows CoreNN to achieve truly large scale indices.

These transitions are handled transparently by CoreNN and querying remains seamlessly available and accurate at all times, including during transitions. There's no configuration, downtime, or manual work needed to scale the database from 1 to 1 billion.

## Storage layout

DiskANN describes an optimization called *implicit re-ranking using full-precision vectors*. In the on-disk stage, the neighbors list for a node we expand during a query iteration is on disk instead of in memory. To capitalize the fact that disk reads are usually minimum 4K, we also store the original vector with the neighbors list to read the full-precision vector for "free". Our vectors in memory are quantized, so this will allow us to recalculate the distance to the candidate for a more accurate result.

This is better than fetching all the vectors and re-ranking after the search, as that means doing another round of disk reads when we're already tight on latency budget. Note that we're only reranking the already-expanded node: we don't fetch full vectors for all candidate nodes, as there are M per iteration, exploding I/O costs.

CoreNN stores each node's full vector + neighbors in a single RocksDB entry, to approximate the optimization. Keys have a 1-byte type prefix and use binary, not string, integer representation for maximum compactness. A common prefix allows efficient iteration. How the graph is built and queries traverse are unpredictable, so there's no "ideal" order to lay out nodes on disk to exploit spatial locality, and we gain nothing by omitting the full vector for more density.

In both stages, vectors and nodes are stored in the DB using the same entries, for durable persistence. Using the same DB format means transitioning between in-memory and on-disk require no mass rewrites or deletes; we simply evict from memory and instantly begin using the disk, already optimally laid out.

## Backedge deltas

When inserting a new node, Vamana inserts backedges to its new neighbors. This poses a problem when on disk: each vector will require updating M other nodes, a huge [write amplification](https://en.wikipedia.org/wiki/Write_amplification) that uses up a lot of IOPS.

The FreshDiskANN paper remedies this by using temporary in-memory indices. Inserts first go to an in-memory Vamana graph. Once this reaches a certain size, it's snapshotted to disk and inserts go to a new temporary in-memory graph. After there are a number of these snapshots, the whole system begins the `StreamingMerge` procedure, where vectors from these frozen graphs get inserted into the on disk index all at once, ideally coalescing writes.

This setup has one major drawback: all our computation optimizing those temporary graphs are discarded, and we have to expend the same amount of computation again to re-insert all those vectors into our main on-disk graph. During this time, the machine will be under heavy CPU utilization, causing a drop in QPS.

CoreNN takes a different approach. We can observe two things:

- Inserting a backedge means rewriting the node's neighbors list of M for the purpose of adding 1/M more data, causing write amplification.
- The node's neighbors list has size M as it was optimized with `RobustPrune`; adding just 1 node exceeds M and triggers the `RobustPrune` immediately.

Therefore, CoreNN stores a list of "additional neighbors" for each node, which is merged with the base neighbors when expanding. When writing, it's persisted at a different DB key, so no wasteful rewriting of existing nodes is done. RocksDB compacts small values efficiently, and the nodes touched during an insert are random on average (and therefore have few additional neighbors), which combine to reduce write amplification significantly.

CoreNN introduces `max_degree_bound`, which allows a node to reach this threshold of neighbors before optimizing down to `degree_bound`; this reduces the frequency of the O(n <sup>2</sup>) computations and rewrites of the node in the DB. This has no effect on accuracy, as we're only adding additional edges to consider, not removing any existing optimized ones; it just increases query computation times slightly.

I believe this is a better trade off as it's easier and cheaper to add another SSD and double the durability, IOPS, and space, than doubling the CPU core count or clock speed. Flash storage is flexibly shaped with almost no upper limit, but one machine can only have so many CPU cores or clock speed. Additionally, NVMe SSDs are massively parallel with separate read/write pipelines, whereas CPU time spent inserting cannot answer queries.

There is also the benefit of a near-instant transition to on-disk, as the DB inserts and optimization calculations are amortized. Using the FreshDiskANN approach, there is a sudden period of degraded SLA upon triggering the long and intensive process to re-insert all vectors from temporary indices into the on-disk index.

FreshDiskANN's approach requires rebuilding the latest unfrozen temporary index when loading up, as it hasn't been snapshotted yet. This makes recovery and repeated opening slow and expensive. CoreNN doesn't need to recompute as inserts are done directly to the main on-disk index.

## Product quantization

Quantization comes into play as we move into the on-disk stage and start reading from disk instead of memory while traversing the graph.

When we expand a node during a query iteration, all its unseen neighbors are new candidates and we calculate the distance to the query for each. Even with a reasonable degree bound of 50, if our vectors were solely on disk, that would be 50 disk reads per iteration; the latency and I/O pressure adds up quickly.

We'd prefer the latency of RAM, but the vectors alone for 1 billion entries would occupy around 1 TB of RAM. Therefore, we keep reading the full vectors and graph nodes from disk, but store quantized vectors in memory. The accuracy remains high, as the graph was built using full-precision original vectors.

Product quantization is the approach CoreNN takes, as suggested by the DiskANN paper. It's a lossy vector compression mechanism that works by:

- Dividing each vector into smaller chunks ("subspaces"). For example, a 512D vector becomes 64×8D vectors.
- Clustering (e.g. k-means) all chunks for each subspace into C clusters, usually 256.
- Representing each chunk by its cluster index. Now 64×8D vectors become 64×1D, as 256 possible values can be represented in a single u8 byte.

What was 64 subspaces × 8 dimensions × 4 bytes per f32 becomes 64 × 1 byte per u8, a compression ratio of 32. Like most other compression algorithms, PQ works well because real-world data have exploitable correlations and structures. Now, we can fit all vectors in memory.

Here's a quick interactive visualization:

After quantizing, we can represet each point's position only with the index of the line for each axis (in this case, only log(20) = 5 bits), rather than a more precise but expensive float (32 bits). Distance relationships are largely retained, but we save a lot of bits. Of course, as mentioned, in practice:

- You cluster more than one dimension at once.
- "Lines" are drawn along these clusters, not uniformly across the space.

But you get the idea.

## float16, binary quantization, Matroyshka

For ANN, using float16 or bfloat16 over float32 often has negligible accuracy impact: the important thing is to preserve distance relationships between points, and both have enough precision for most well-designed embeddings, esp. in a high dimensional space. The upside is that they double the amount of vectors that can fit in memory, as well as halving storage costs. CoreNN supports these (as well as float64) natively, which is an improvement over [hnswlib](https://github.com/nmslib/hnswlib/issues/122) as of this writing.

All computations, regardless of dtype, use optimized AVX-512 where possible. (SVE is [not yet supported](https://rust-lang.github.io/rust-project-goals/2025h1/arm-sve-sme.html) in Rust.)

Surprisingly, text embeddings tend to perform reasonably well when precision quantized, all the way down to binary quantization, where only 1 bit is used to represent each dimension (usually the sign i.e. positive or negative). A theory is that effective training naturally leads to effective "spreading" of concepts across the space, using the full dynamic range effectively, so the sign alone contains enough signal to separate differing concepts, esp. when combined with a lot of dimensions.

CoreNN supports binary quantization as another compression mode out of the box. It also supports truncation compression if you have [Matryoshka embeddings](https://huggingface.co/blog/matryoshka).

## Async vs sync

My initial approach was to use async Rust, if only because this is a database that does I/O. But it turned out that async was not the best fit:

- RocksDB itself is not async, as it's a C++ library. This means a lot of [spawn\_blocking](https://docs.rs/tokio/latest/tokio/task/fn.spawn_blocking.html) at C++ boundaries, but the RocksDB C++ code itself does a lot of computation and not just I/O. A backing store written from the ground up using async Rust would likely fare better here.
- There's a lot of computation, not just I/O, which doesn't mix easily with an async program. A lot of careful handling of compute so they don't block the async runtime, while also not oversaturating the system, is necessary.
- Async lets you do millions of lightweight tasks concurrently, which makes sense with networking and event-driven programs, but less so with disk I/O which tends to scale more reasonably closely with threads.

But I think the biggest annoyance was that async doesn't work great with tooling like profiling and debugging, which are really nice things to have that work when you have a "traditional" program. Using `perf` and [flamegraphs](https://github.com/flamegraph-rs/flamegraph) make light work of finding and squashing hotspots quickly, and is way better than 1) guessing or 2) manually adding timing statements everywhere. People suggest alternatives like [tracing](https://docs.rs/tracing/latest/tracing/) and [tokio-console](https://github.com/tokio-rs/console), but there's already an entire ready-to-go ecosystem with well-built out infrastructure, polished tools, great reading material, and standardized concepts that work well with all of these.

## Usages and getting started

One of the nice things is that you can use CoreNN in many places for many different situations, given it uses a consistent data format, is highly scalable, and can function as an embedded library or a production-scale service:

- Prototypes or research projects can drop in the dependency for the embedded library and get something working without setting up any services. Once you need to scale to production, you can simply switch out the library for the service.
- Analysts can use CoreNN to process and query billions of social media comments, semantic data, etc. and have it updated in real time, leveraging the power of AI and deep learning based semantic analysis.
- Libraries and programs can drop this into their code like SQLite and instantly add powerful semantic search capabilities.
- The full disk mode means you can quickly run queries without loading the index from disk first, for one-off queries over giant datasets, or systems without a need for high QPS (e.g. only one or a few users). Examples: desktop OSes, Jupyter Notebooks, personal apps, static data dumps.

As mentioned, CoreNN is open source: you can get started by checking out the [GitHub repo](https://github.com/wilsonzlin/CoreNN), which contains quickstarts for supported languages and more documentation. Please come and contribute to the [open source project](https://github.com/wilsonzlin/CoreNN)!