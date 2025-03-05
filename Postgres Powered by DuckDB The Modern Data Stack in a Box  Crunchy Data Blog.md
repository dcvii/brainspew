---
title: "Postgres Powered by DuckDB: The Modern Data Stack in a Box | Crunchy Data Blog"
source: https://www.crunchydata.com/blog/postgres-powered-by-duckdb-the-modern-data-stack-in-a-box
author:
  - "[[Crunchy Data]]"
published: 2024-08-16
created: 2025-03-02
description: Marco reviews the challenges and strengths of analytical and transactional workloads and what a modern data stack that merges the two might look like.
tags:
  - clippings
  - duckdb
---
Looking for Postgres with the power of DuckDB? [Crunchy Data Warehouse](https://www.crunchydata.com/products/warehouse) is the latest Postgres-native tool with full Iceberg support and DuckDB integration.

[Postgres for analytics](https://www.crunchydata.com/products/crunchy-bridge-for-analytics) has always been a huge question mark. By using PostgreSQL's extension APIs, [integrating DuckDB](https://www.crunchydata.com/solutions/postgres-with-duckdb) as a query engine for state-of-the-art analytics performance without forking either project could Postgres be the analytics database too?

Bringing an analytical query engine into a transactional database system raises many interesting possibilities and questions. In this blog post I want to reflect on what makes these workloads and system architectures so different and what bringing them together means.

## OLAP & OLTP: Never the twain shall meet

[Database systems](https://www.crunchydata.com/blog/an-overview-of-distributed-postgresql-architectures) have always been divided into two worlds: Transactional and Analytical (traditionally referred to as OLTP) and OLAP (Online Transactional/Analytical Processing).

Both types of data stores use very similar concepts. The relational data model and SQL dominate. Writes, schema management, transactions and indexes use similar syntax and semantics. Many tools can interact with both types. Why then are they separate systems?

The answer has multiple facets. At a high level, OLTP involves doing a very large number of small queries and OLAP involves doing a small number of very large queries. They represent two extremes of the database workload spectrum. While many workloads fall somewhere in between, they can often be optimized or split until they can reasonably be handled by conventional OLTP or OLAP systems.

For many applications, the database system does the bulk of the critical computational work. Deep optimizations are essential for a database system to be useful and appealing, but optimization inherently comes with complexity. Consider that relational database systems have a vast amount of functionality and need to cater to a wide range of workloads. Building a versatile yet well-optimized database system can take a very long time.

Optimization is most effective when specializing for the characteristics of specific workloads, which practically always comes with the trade-off of being less optimized for other workloads. As it turns out, doing many small things or a few large things, when optimized to the extreme across a wide range of system functions over a long period, results in fundamentally different system architectures. The interface may be similar, but everything from the way queries and transactions are processed down to the storage architecture is going to be vastly different.

Let's have a look at what the main challenges are for each type of system.

## Challenges of transactional systems

The biggest challenge in transactional systems is the efficient handling of a high rate of small update/delete transactions, in a way that guarantees ACID properties, while also handling concurrent read queries.

Storage in transactional systems is organized around small in-memory buffers that can be modified in less than a microsecond and written to disk in under a millisecond. Rows are packed together in the buffers, with tree data structures across the buffers (indexes) used to efficiently find the rows.

An insert/update/delete command involves modifying several buffers to write the new rows and add index entries, or a larger number when modifying multiple rows at once. The changes to the buffers are also written to a write ahead log (WAL) to ensure that they can be recovered in case of a crash.

In the cloud, the buffers and WAL can be stored in elastic block storage or other network-attached storage systems that replicate small disk blocks with minimal latency. Only the WAL is synchronously flushed to disk when committing a transaction. Recently modified buffers may only exist in the memory of the database server. The disk can have many stale and sometimes even truncated buffers. It can only be correctly interpreted by the server to which it is attached or through a crash recovery process that restores changes from the WAL.

Many write operations and read queries will be running concurrently. Database systems typically try to prevent queries from seeing ongoing changes by versioning the rows during a write, such that concurrent reads can skip row versions that were added after the query started ("snapshot isolation"). This comes with additional challenges. For instance, consider that strange anomalies would occur if concurrent updates would operate on the same snapshot without considering each other’s effects. PostgreSQL resolves this through a combination of row-level locks, a chain of forward pointers from past to current row versions, and using the latest row version in the update regardless of the snapshot.

To build a high performance transactional system it is essential to minimize the overhead from synchronization across all these operations, as well as storage access, query processing, transaction management, I/O, and concurrency control.

## Challenges of analytical systems

The biggest challenge in analytical systems is to process a very large number of records in as little time as possible within the context of a single query.

Analytical queries compute statistics and trends across historical data. The number of records involved in a single query can easily be in the billions, which means it's a billion times higher than the number of records involved in a typical transactional query (1-100). If your database system needed 1 second per record, a single query might not finish in your lifetime. Hence, spending as little time as possible per record matters above all else.

One of the techniques analytical systems use to minimize per-record overhead is columnar storage, which dissects records into fixed-sized vectors of values from the same column. Analytical queries often only use a subset of the columns while involving most of the records, and columnar storage enables skipping unused columns during reads. The vectors can also be compressed effectively because columns often contain many similar values.

Database systems that use columnar storage can be architected for vectorized execution, which means they process a vector at a time rather than a record at a time. For instance, a filter might be evaluated on a vector from column A, which produces a list of indices to be retrieved from a vector from column B. Vectorized execution minimizes the overhead of switching between different expression states, and can take advantage of modern CPU instructions that process multiple values at once (SIMD).

Analytical database systems also optimize for parallel execution within a single query. Data needs to be passed around efficiently between different parts of a parallel execution pipeline.

Managing the flows of data in a parallel, vectorized executor with minimal data copying, while also using data structures that maximize performance is the most complex part of building an analytical database system. The query planner and executor are very different than in transactional systems, with higher processing time per query, but much lower processing time per row when a query spans many rows.

In modern analytical database systems, storage is organized around files in distributed storage systems like Amazon S3, because they can scale the amount of storage and retrieval bandwidth, and can be accessed directly by various applications. The latency of such systems is relatively high, but acceptable for analytical queries which typically range from hundreds of milliseconds to minutes.

The overhead of synchronization between components and concurrent queries is also less of an issue in analytical systems than in transactional systems because they are negligible compared to the time required to execute a single query.

## Can you build a unified database architecture?

It is technically possible to build a database engine that can simultaneously handle a high rate of low latency transactions and perform fast analytical queries on a *single copy of the data*, with ACID properties. Such systems are often referred to as HTAP (Hybrid Transactional/Analytical Processing). However, hybrid systems generally underperform against dedicated OLTP or OLAP systems or make other invasive trade-offs such as limited functionality, or lower durability.

It is hard to precisely identify the workloads that benefit substantially from a hybrid approach. Moreover, the incremental cost of keeping a second copy of transactional data in a format that is optimized for analytics and compression in object storage is relatively small. Hence, replicating transactional data into an analytical system with some lag has become the dominant way of doing analytics on transactional data.

The OLTP vs. OLAP disparity is likely to stay, though it is not without downsides. The capabilities, tools, ecosystem, and practices differ significantly between different parts of the data stack, which becomes a source of complexity and high maintenance cost. In addition, expensive, brittle data movement tools are needed to get data from transactional to analytical stores.

OLTP and OLAP workloads are often managed by different teams, so some differences in tooling and practices are to be expected. Still, organizations spend a huge amount of time and money on moving data and integrating different systems. Moreover, an application that is purely transactional or purely analytical is not likely to remain so for long.

Consider that analytics teams often create dashboards and popular dashboards end up having various types of materialized views, typically kept in transactional database systems. Data management also involves a lot of metadata and bookkeeping, and those are best done in a transactional way to avoid duplicate or missing data.

Application teams use transactional database systems, but often want to add value by providing their customers with insights. However, they do not want the complexity of funneling the data through several (company-wide) analytics systems.

OLTP and OLAP are fundamentally different workloads that benefit from fundamentally different techniques and storage solutions, but they don't necessarily benefit from using wholly different database systems. The fact that most database systems are focused on only one type of workload is because it is extremely hard for a database builder to be simultaneously successful in two different worlds.

The solution to this conundrum, we believe, lies in extensibility.

## Database extensibility: Bringing disparate systems together

From its inception, PostgreSQL has been designed to be extensible. It supports many forms of extensibility, with extensions able to control the behavior of query processing and data storage at many different levels. There is a flourishing ecosystem of extensions.

DuckDB is an embedded OLAP database, which is taking the analytics landscape by storm. DuckDB takes inspiration from SQLite for its deployment model, and PostgreSQL for its functionality and extensibility.

With both of these systems being extensible, and having a similar interface, they can be integrated in interesting ways. In Crunchy Bridge for Analytics, we introduced the notion of analytics tables that are backed by files in S3 and integrated DuckDB as a query engine for queries that involve analytics tables. PostgreSQL gives sufficient flexibility to use DuckDB for the full query or specific parts of the query. We used DuckDB extensions to incrementally fill any gaps that DuckDB might have compared to PostgreSQL, to ensure a wide range of PostgreSQL queries can take advantage of parallel, vectorized execution on columnar Parquet files within DuckDB.

Our goal in Crunchy Bridge for Analytics is not necessarily to enable HTAP tables. It is meant "for analytics". We do believe it is very useful to have your analytics database use the same system as your transactional databases, and that it is also very useful to be able to handle arbitrary transactional workloads in your analytics database, including handling of metadata, fast insert queues, partitioned time series tables, materialized views, etc. We also think it is useful to be able to easily move data between transactional and analytical tables without needing external tools, or do fast analytics without needing to switch to a different set of tools, data types, syntax, and ecosystem.

Effectively, extensibility can reduce the traditional OLTP-OLAP gap to a difference between tables, rather than a difference between database systems. Multiple query engines that make very different trade-offs and use different storage layers can be blended together into a single environment.

## The power single machine database systems

One of the most surprising and disruptive aspects of DuckDB is that it is taking fast analytics away from the complex world of distributed systems back into the much simpler single-machine realm. While transactional database systems like PostgreSQL can be distributed, the vast majority of database systems run on a single machine. Hence, we now have two state-of-the-art, open source OLAP & OLTP systems which we can reasonably run together on the same machine.

There is still a difference between running a single machine briefly to handle a large analytics query (common for OLAP) vs. running it all the time to handle a steady rate of transactions (common for OLTP). However, we found that using a persistent machine for analytics on modern hardware has one tremendous benefit: long-lived cached in memory and on large NVMe drives.

Retrieving a file over S3 over a single connection is generally limited to 50-80MB/sec. Multiple concurrent connections can help, but in most scenarios the aggregate throughput on a single machine only goes a few times higher. Conversely, locally-attached NVMe drives easily reach 2-3GB/sec of read throughput and are usually big enough to hold a large part of the data. Keeping our data cached lets us take advantage of DuckDB’s processing power at a limited, predictable cost.

Even with a local cache, you do want your machine to have a high bandwidth connection to S3 for querying files that are not in cache or for loading into cache within a reasonable amount of time. The best way to achieve that is to run the machine on EC2 in the same AWS region as your S3 buckets. A major benefit DuckDB-in-PostgreSQL has over plain DuckDB in that regard is that it has a well-defined network protocol and an huge ecosystem of tools that support it. Moreover, PostgreSQL can be managed for you in EC2 by Crunchy Bridge.

Of course, when we talk about single machine systems, you can still have as many of those as you need to handle various applications and workflows with high concurrency. The big advantage is that you avoid a lot of the cost and complexity of gluing together operationally complex data processing systems, and instead you have a set of versatile units that are managed for you.

## DuckDB + PostgreSQL = The Everything Database?

So, with [Crunchy Bridge for Analytics](https://www.crunchydata.com/products/crunchy-bridge-for-analytics) you can get the stellar analytics performance of DuckDB along with all the familiar transactional capabilities and versatility of PostgreSQL in one box, which is managed for you by the team at Crunchy Data.

You can do fast ad-hoc queries on [Parquet](https://www.crunchydata.com/solutions/postgres-for-parquet-and-iceberg) in S3 or create materialized views, you can schedule your ETL processes via [pg\_cron](https://www.crunchydata.com/blog/annoucing-the-scheduler-for-crunchy-bridge), you can track data operations via transactions, you can efficiently import and export Parquet/CSV/JSON, you can use any PostgreSQL-compatible tool (incl. most BI tools), and you can use all the PostgreSQL [extensions](https://docs.crunchybridge.com/extensions-and-languages?CrunchyAnonId=bocdjphhuzaylhckmljohrpwhocjvvwcxnossfkdfkusaol) and [managed database features](https://docs.crunchybridge.com/concepts?CrunchyAnonId=bocdjphhuzaylhckmljohrpwhocjvvwcxnossfkdfkusaol) offered by Crunchy Bridge. Finally, you get a predictable price with great price-performance thanks to long-lived caches.

It might just be time for a new data stack.