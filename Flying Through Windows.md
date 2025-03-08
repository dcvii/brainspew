---
title: "Flying Through Windows"
source: "https://duckdb.org/2025/02/14/window-flying"
author:
  - "[[Richard Wesley]]"
published: 2025-02-13
created: 2025-02-15
description: "Dive into the details of recent DuckDB windowing performance improvements."
tags:
  - "clippings"
---
![Author Avatar](https://duckdb.org/images/blog/authors/richard_wesley.jpg)

*TL;DR: Dive into the details of recent DuckDB windowing performance improvements.*

## Introduction

In the previous post I went into some new windowing functionality in DuckDB available through SQL. But there are other changes that improve our use of resources (such as memory) without adding new functionality. So let's get “under the feathers” and look at these changes.

> #### Note
> 
> We previously [benchmarked ourselves on a window function-heavy workload](https://duckdb.org/2024/06/26/benchmarks-over-time.html), which showed great performance improvements over time. The optimizations presented in this blog post push the performance of DuckDB's window operator even further.

## Segment Tree Vectorization

One important improvement that was made in the summer of 2023 was converting the segment tree evaluation code to vectorized evaluation from single-value evaluation. You might wonder why it wasn't that way to begin with in a “vectorized relational database” (!), but the answer is lost in the mists of time. My best guess is either that the published algorithm was written for values or that the aggregation API had not been nailed down yet (or both).

In the old version, we used the aggregate's `update` or `combine` APIs, but with only the values and tree states for a single row. To vectorize the segment tree aggregation, we accumulate *vectors* of leaf values and tree states and flush them into each output row's state when we reach the vector capacity of 2048 rows. Some care needed to be taken to handle order-sensitive aggregates by accumulating values in the correct order. `FILTER` and `EXCLUDE` clauses also provided some entertainment, but the segment trees are now fully vectorized. The performance gains here were about a factor of four (from “Baseline” to “Fan Out”).

The chart below shows the speedups achieved by the vectorization improvements:

[![Vectorization Improvements](https://duckdb.org/images/blog/windowing/vectorization-improvements.png "Vectorization Improvements")](https://duckdb.org/images/blog/windowing/vectorization-improvements.png)

Once segment trees were vectorized, we could use the same approach when implementing `DISTINCT` aggregates with merge sort trees. It may be worth updating the custom window API to handle vectorization at some point, because although most custom window aggregates are quite slow (e.g., `quantile`, `mad` and `mode`), `count(*)` is also implemented as a custom aggregate and would likely benefit from a vectorized implementation.

## Constant Aggregation

A lot of window computations are aggregates over frames, and a common analytic task with these results is to compare a partial aggregate to the same aggregate over *the entire partition*. Computing this value repeatedly is expensive and potentially wasteful of memory (e.g, the old implementation would construct a segment tree even though only one value was needed.)

The previous performance workaround for this was to compute the aggregate in a subquery and join it in on the partition keys, but that was, well, unfriendly. Instead, we have added an optimization that checks for *partition-wide aggregates* and computes that value once per partition. This not only reduces memory and compute time for the aggregate itself, but we can often return a constant vector that shares the values across all rows in a chunk, reducing copy costs and potentially even downstream evaluation costs.

Returning a constant vector can yield surprisingly large memory and performance benefits. In the issue that drove this improvement, the user was constructing a constant 100k element list (!) and then computing the median with a list aggregation lambda. By returning a single constant list, we build and reduce that list only once instead of once per row!

## Streaming Windows

Computing window functions is usually quite expensive! The entire relation has to be materialized, broken up into partitions, and each partition needs to be sorted.

But what if there is no partitioning or ordering? This just means that the window function is computed over the entire relation, in the “natural order”, using a frame that starts with the first row and continues to the current row. Examples might be assigning row numbers or computing a running sum. This is simple enough that we can *stream* the evaluation of the function on a single thread.

First, let's step back a bit and talk about the window *operator*. During parsing and optimization of a query, all the window functions are attached to a single *logical* window operator. When it comes time to plan the query, we group the functions that have common partitions and “compatible” orderings (see Cao et al., [*Optimization of Analytic Window Functions*](https://www.vldb.org/pvldb/vol5/p1244_yucao_vldb2012.pdf) for more information) and hand each group off to a separate *physical* window operator that handles that partitioning and ordering. In order to use the “natural order” we have to group those functions that can be streamed and execute them first (or the order will have been destroyed!) and hand them off to the *streaming* physical window operator.

So which [window functions](https://duckdb.org/docs/sql/functions/window_functions.html) can we stream? It turns out there are quite a few:

- Aggregates `BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` (we just update the aggregate)
- `first_value` – it's always the same
- `percent rank` – it's always 0
- `rank` – it's always 0
- `dense_rank` – it's always 0
- `row_number` – we just count the rows
- `lead` and `lag` – we just keep a buffer

There are a few more restrictions:

- `IGNORE NULLS`, `EXCLUDE` and `ORDER BY` arguments are not allowed
- `lead` and `lag` distances are restricted to a constant within ±2048 (one vector). this is not really a big deal because the distance is usually 1.

The improvements for streaming `LEAD` were quite dramatic:

```sql
SELECT setseed(0.8675309);
CREATE OR REPLACE TABLE df AS
    SELECT 
        random() AS a,
        random() AS b,
        random() AS c,
    FROM range(10_000_000);

SELECT sum(a_1 + a_2 + b_1 + b_2)
FROM (
    SELECT
        lead(a, 1) OVER () AS a_1,
        lead(a, 2) OVER () AS a_2,
        lead(b, 1) OVER () AS b_1,
        lead(b, 2) OVER () AS b_2
    FROM df
) t;
```

The chart below shows the performance improvements.

- Baseline – Where we started
- Shift – Copying blocks of rows inside the non-streaming implementation, instead of one at a time
- Streaming – First implementation of streaming `LEAD`
- Partials – Avoid copying when the entire chunk can just be referenced

Note that the *x* axis shows the speedups compared to the baseline (1×) and the absolute runtimes (in seconds) are shown as labels.

[![Streaming Lead Performance](https://duckdb.org/images/blog/windowing/streaming-lead.png "Streaming Lead Performance")](https://duckdb.org/images/blog/windowing/streaming-lead.png)

In the future we may be able to relax the end of the frame to a constant distance from the current row that fits inside the buffer length (e.g., `BETWEEN UNBOUNDED PRECEDING AND 1 PRECEDING`) but that hasn't been investigated yet.

## Partition Major Evaluation

Window partitions are completely independent, so evaluating them separately is attractive. Our first implementation took advantage of this and evaluated each partition on a separate thread. This works well if you have more partitions than threads, and they are all roughly the same size, but if the partition sizes are skewed or if there is only one partition (a common situation), then most of the cores will be idle, reducing throughput.

[![Thread Partition Evaluation](https://duckdb.org/images/blog/windowing/parallel-partitions.png "Thread Partition Evaluation")](https://duckdb.org/images/blog/windowing/parallel-partitions.png)

To improve the CPU utilization, we changed the execution model for v1.1 to evaluate partitions in parallel. The partitions are evaluated from largest to smallest and we then distribute each partition across as many cores as we can, while synchronizing access to shared data structures. This was a lot more challenging than independent single-threaded evaluation of partitions, and we had some synchronization issues (hopefully all sorted now!) that were dealt with in the v1.1.x releases. But we now have much better core utilization, especially for unpartitioned data. As a side benefit, we were able to reduce the memory footprint because fewer partitions were in memory at a time.

[![Partition Major Evaluation](https://duckdb.org/images/blog/windowing/partition-major.png "Partition Major Evaluation")](https://duckdb.org/images/blog/windowing/partition-major.png)

One remaining issue is the coarseness of the sub-partitions. At the moment to avoid copying they use the blocks produced by the sorting code, which are often larger than we would like. Reducing the size of these chunks is future work, but hopefully we will get to it as part of some proposed changes to the sorting code.

## Out of Memory Operation

Because windowing materializes the entire relation, it was very easy to blow out the memory budget of a query. For v1.2 we have switched from materializing active partitions in memory to using a pageable collection. So now not only do we have fewer active partitions (due to partition major evaluation above), but those partitions themselves can now spool to disk. This further reduces memory pressure during evaluation of large partitions.

Windowing is so complex, however, that there are still some remaining large data structures. The [segment trees](https://www.vldb.org/pvldb/vol8/p1058-leis.pdf) and [merge sort trees](https://dl.acm.org/doi/10.1145/3514221.3526184) used for accelerating aggregation are still in memory, especially the intermediate aggregate states in the middle of the trees. Solving this completely, will require a general method of serializing aggregate states to disk, which we do not yet have. Still, most aggregates can be serialized as binary data without special handling, so in the short term we can probably cover a lot of cases with the current aggregation infrastructure, just as we do for `GROUP BY`.

Window expressions are evaluated independently, but they often share expressions. Some of those expressions can be expensive to evaluate and others need to be materialized over the entire partition. As an example of the latter, aggregate functions can reference values anywhere in the partition. This could result in computing and materializing the same values multiple times:

```sql
-- Compute the moving average and range of x over a large window
SELECT
    x,
    min(x) OVER w AS min_x,
    avg(x) OVER w AS avg_x,
    max(x) OVER w AS max_x,
FROM data
WINDOW w AS (
    PARTITION BY p
    ORDER BY s
    ROWS BETWEEN 1_000_000 PRECEDING and 1_000_000 FOLLOWING
);
```

Paging the data for `x` reduces the memory footprint, but the segment trees used to evaluate the three aggregates will contain duplicate copies of `x` – along with the with operator itself (which has to return `x`). With v1.2 we have added a mechanism for sharing evaluation of expressions like these between functions. This not only reduces memory, but in this example we will also reduce disk paging because all three functions will be accessing the same values.

There are a number of places where we are sharing expressions, including `ORDER BY` arguments, `range` expressions and “value” functions like `lead`, `lag` and `nth_value`, and we are always on the lookout for more (such as frame boundaries – or even segment trees).

## Future Work

While I have mentioned a number of things we would like to get to in the future, one that doesn't fit nicely into any of the topics so far is query rewriting. It turns out that some window functions can be evaluated using other techniques such as [self-joins](https://www.vldb.org/pvldb/vol17/p2162-baca.pdf) and some of our smarter aggregates (like `arg_max`). Generating these alternate query plans can have large performance benefits and we plan to investigate them.

## Conclusion

As you can see, windowing is a big hairy beast! There is also not a lot of published research on effective algorithms (I've linked to pretty much all of it), so we are often stuck making it up ourselves or falling back to extremely simple and slow approaches. But I hope that many of you will find something new and exciting in what we have been up to for the past 2-3 years - and I will try to be more timely in blogging about future window improvements.