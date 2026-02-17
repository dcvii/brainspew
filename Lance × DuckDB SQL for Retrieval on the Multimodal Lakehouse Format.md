---
title: "Lance × DuckDB: SQL for Retrieval on the Multimodal Lakehouse Format"
source: https://lancedb.com/blog/lance-x-duckdb-sql-retrieval-on-the-multimodal-lakehouse-format/
author:
  - "[[By [Xuanwo]]]"
published:
created: 2026-02-09
description:
tags:
  - clippings
  - LanceDB
  - duckdb
---
---

---

The challenge with building efficient, scalable retrieval systems isn’t that teams are unable to build a vector index (that part is well understood) — it’s that the end-to-end workflow from a data management perspective is fragmented: embeddings live in one place, text and metadata in another, evaluation slices in a third, and the “analysis” layer is often a separate pipeline that requires copying data into yet another format.

[Lance](https://lance.org/) is an open lakehouse format for multimodal AI, built to address these challenges. The Lance format spans three layers of the lakehouse stack: it’s a file format, a table format, *and* a catalog spec. The goal is simple: to build a complete, open-source lakehouse format for multimodal data that can serve as the durable and scalable data plane for AI and ML.

Today, we’re happy to announce the new [Lance × DuckDB extension](https://github.com/lance-format/lance-duckdb). This makes it *much* easier to use Lance as the lakehouse layer for retrieval and RAG by bringing Lance into DuckDB natively. With this extension, you can query, scan, and write Lance datasets directly from SQL. You can run vector search, full-text search, and hybrid search as SQL table functions, and then immediately join, aggregate, debug, and materialize results *without leaving DuckDB*.

💡

Here’s a TL;DR if you want a quick mental model of what we cover in this post:

- Lance is the open lakehouse format for multimodal AI (data plane).
- DuckDB is a portable SQL query engine (compute plane).
- The extension makes search and retrieval feel like regular SQL operators on top of your multimodal lakehouse datasets.

## Why this matters for Retrieval & AI teams

#### Treat Lance as the open lakehouse layer for multimodal AI

Lance’s design intentionally spans the file, table, and catalog spec layers of the lakehouse stack. This separation of concerns matters: your underlying data stays stable within the file format (compute engines may come and go) — and you can keep your multimodal datasets and embeddings where they already live (object storage), using the table and catalog layers, without rebuilding a new storage stack every time you change your compute engine.

#### Put retrieval inside the lakehouse, and inside SQL

Lance’s larger goal is to provide hybrid search plus analytics on the same dataset. DuckDB’s vision is to provide developers a familiar SQL interface for all their workflows. The Lance × DuckDB extension makes that combination practical by exposing retrieval operators as table functions in SQL, allowing direct scans of `.lance` datasets by path.

#### Make iteration loops faster: retrieve → analyze → materialize 🔁 repeat

These days, most teams building retrieval systems for RAG and agents need to:

- Add features and labels over time
- Slice and evaluate data repeatedly
- Save reproducible top-k subsets and hard negatives

DuckDB gives you the **analysis surface**. Lance gives you a durable **dataset format** to store and manage those artifacts right next to the source data.

## What you get by using the Lance × DuckDB extension

Let’s briefly list the standout features of the extension before going into a 5-minute quickstart below.

1. **Direct scanning of Lance datasets**: After installing and loading the extension, DuckDB can query a Lance dataset by pointing SQL at a `.lance` path.
2. **Retrieval operators as SQL table functions**: The extension adds SQL-friendly table functions for retrieval that operate natively on the Lance table underneath: `lance_vector_search`,`lance_fts` and `lance_hybrid_search`, for vector search, full-text search, and hybrid search, respectively. All these functions **push down work into Lance**, so you get all the benefits of fast retrieval while writing SQL.
3. **Organize your datasets with namespaces**: When you `ATTACH` a [Lance namespace](https://lance.org/format/namespace/), running `CREATE TABLE` creates datasets managed by that namespace (similar to how catalogs work in other systems). This is a nice way to keep “derived datasets” (data slices, hard negatives, reranked features) organized without having to remember path specifiers.
4. **Cloud-native access via DuckDB secrets**: Keep using DuckDB’s familiar cloud connectivity features to access object-storage URIs like `s3://...` and more. You simply configure a secret with a scoped prefix once, and then query the dataset path directly.

## 5-minute quickstart

In this section, we’ll go through examples that cover hybrid retrieval, joins, and materialized slices, all done with SQL from the comfort of your DuckDB CLI.

#### Install and load the extension

Install the extension as follows. If you’ve already installed the extension before, you can just update it.

```sql
INSTALLlanceFROMcommunity;LOADlance;-- UPDATE if you've installed a previous version.
UPDATEEXTENSIONS;
```

#### Create a small retrieval table (text + embedding) and write to Lance

Let’s create a simple Lance dataset about animals and the noises they make. This is done using SQL DDL/DML as shown below. The query generates data in SQL and writes a new Lance dataset.

```sql
COPY(SELECT*FROM(VALUES(1,'duck','quack',[0.9,0.7,0.1]::FLOAT[3]),(2,'horse','neigh',[0.3,0.1,0.5]::FLOAT[3]),(3,'dragon','roar',[0.5,0.2,0.7]::FLOAT[3]))ASt(id,title,text,vec))TO'./docs.lance'(FORMATlance,mode'overwrite');
```

You can now call hybrid search as a table function in SQL, which is pushed down and executed at the Lance table layer. A hybrid search query lets you combine a full-text search query with a vector search query via a linear combination of scores. The hybrid search results contain a `_hybrid_score` (larger is better, so we sort in descending order).

```sql
SELECTid,_hybrid_score,_distance,_scoreFROMlance_hybrid_search('./docs.lance','vec',[0.8,0.7,0.2]::FLOAT[],'text','the duck surprised the dragon',k=10,alpha=0.5,oversample_factor=4)ORDERBY_hybrid_scoreDESC;
```

You can also do joins between DuckDB tables and Lance tables. The example below joins results from a hybrid search query run on a Lance dataset and a regular DuckDB table `doc_meta`.

```sql
CREATETABLEdoc_metaASSELECT*FROM(VALUES(1,'train',0.12),(2,'train',0.34),(3,'eval',0.56))ASt(id,split,quality_score);SELECTr.id,r._hybrid_score,r._distance,r._score,m.split,m.quality_scoreFROMlance_hybrid_search('./docs.lance','vec',[0.8,0.7,0.2]::FLOAT[],'text','the duck surprised the dragon',k=50,alpha=0.5,oversample_factor=4)rJOINdoc_metamUSING(id)WHEREm.split='eval'ORDERBYr._hybrid_scoreDESCLIMIT50;
```

#### Materialize the top-k slice and write back into Lance

The extension supports both reads and writes. In the example below, we materialize the top-k results from our hybrid search query and write them to a new Lance dataset.

```sql
COPY(SELECTr.*FROMlance_hybrid_search('./docs.lance','vec',[0.8,0.7,0.2]::FLOAT[],'text','the duck surprised the dragon',k=50,alpha=0.5,oversample_factor=4)rORDERBYr._hybrid_scoreDESCLIMIT50)TO'./topk_eval_slice.lance'(FORMATlance,mode'overwrite');
```

## Cloud integration

Using the extension, you query your Lance data where it lives, whether on your local machine or on object stores in the cloud. The example below shows how to create an S3-scoped secret, and then directly query your Lance datasets on S3 in SQL.

```sql
CREATESECRET(TYPELANCE,PROVIDERcredential_chain,SCOPE's3://bucket/');SELECT*FROM's3://bucket/path/to/dataset.lance'LIMIT5;
```

The key takeaway is: configure access to cloud storage once, then treat the dataset path as a queryable input in the future.

## A note for users of the earlier Python + PyArrow workflow

If you’ve previously used DuckDB with LanceDB in Python, that integration is done via Apache Arrow, which enables zero-copy data sharing. DuckDB can also push down column selections and basic filters to reduce scanned data. **This remains a great option for Python-first exploration and notebooks**.

However, Arrow boundaries can limit the expressivity of pushdowns for more production-style access patterns. We [previously](https://lancedb.com/blog/benchmarking-random-access-in-lance/#duckdb-integration) called out that DuckDB’s Arrow integration has extremely limited filter pushdown in some cases, which can translate into large latency differences for certain access patterns. We’re happy to announce that the Lance × DuckDB extension is not constrained by that interface boundary, giving us more room to improve pushdown, parallelism, and diagnostics in the future.

## Conclusions

> One open lakehouse, with multiple compute engines for search & retrieval, accessible within a familiar SQL interface.

[Lance](https://lance.org/) is designed to be the open lakehouse format for multimodal AI: an open-source, durable, and performant data layer on object storage that supports multimodal datasets at immense scale.

[DuckDB](https://duckdb.org/) is an open-source, developer-friendly database and compute engine that provides a convenient SQL interface. With the Lance × DuckDB extension, you get first-class SQL operators for retrieval within a modern query engine, while operating on top of an open lakehouse format. You can run vector, FTS, or hybrid retrieval, immediately join to features and metadata, compute analysis and evaluation data on-the-fly, and materialize and reproduce slices of the data back into Lance, all using the SQL syntax you’re already familiar with.

If you’re building RAG systems, retrieval pipelines for agents, or working with very large multimodal AI datasets on object storage, you now have a concrete way to unify your retrieval and analytics workloads without copying data between formats.

Install the Lance × DuckDB extension, point DuckDB at a Lance dataset, and run your first retrieval query now!

## Links

Check out the following pages to learn more about this extension and reach out to us on [Lance Discord](https://discord.gg/lance) with your comments and feedback!