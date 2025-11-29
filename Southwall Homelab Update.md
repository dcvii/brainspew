---
title: Southwall Homelab Update
source: https://tessellations.substack.com/p/southwall-homelab-update
author:
  - "[[Michael David Cobb Bowen]]"
published: 2025-10-24
created: 2025-11-24
description: A new evolution in my long journey towards mastery.
tags:
  - clippings
  - southwall
---
### A new evolution in my long journey towards mastery.

It has been a very long time since I could focus on the homelab instead of on multiple forking paths of my resume, but at long last I have landed a contract. So I have several updates FWIW.

![](https://substackcdn.com/image/fetch/$s_!0tiF!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4b11dae8-4b35-404a-8b65-4c41800c5678_468x82.jpeg)

**Metro Decisions**  
I am on my fourth entrepreneurial leg. So I’m an independent contractor once again. Taking down scores and watching out for the heat around the corner. This time I have accounting help and I don’t have to incorporate. Whee! or Whoa! One of those.

What this means is that for the time being, **Boxtag** and **XRepublic** and such dreamy ideas have been boxed up and put into the attic. I got an opportunity to talk to an angel investor, and I simply do not have enough runway or collaborative support to build something substantial - at least not in the ballpark for where he’s swinging for the fences. So I’ve got a lot of coding to do to build up my own sweat equity. I’m still an idea man, but… now it’s time to be a peasant. There’s some lovely filth down here.

**Rustdesk**  
I apparently tried this before but it was just about the time that some new kit came down from Apple which included the new Screen Sharing app. It was OK, but sometimes I lost the mouse which was weird and annoying. Nevertheless I had no real services running outside of my primary desktop, so both laid unused. I am satisfied that Rustdesk is the right move, so I’ll be getting rid of **NoMachine** after five or six years now. **Network Chuck** was right about this (and I never trusted Team Viewer). Funny. I used it with programmers from Kiev.

---

**Postgres**  
My Gold Ubuntu NUC server (the largest in the trio of Iron and Brass) I have upgraded to V17. I have a 2TB external hard drive which contains my storage for a couple of the three databases, including the newest for **Ducklake**. But the coolest thing is that there is a DuckDB plugin for Postgres that allows the query engine to dynamically (or configurably deterministically) chose either DuckDB or Postgres’ query plan. To my reckoning this is awesome and basically drops a bomb on **SingleStore**. Or as Grok tells us:  
  
*OverviewYes, as of October 2025, the pg\_duckdb extension for PostgreSQL (often referred to as the “DuckDB extension to Postgres”) now makes many of SingleStore’s key technical advantages—particularly unified OLTP/OLAP processing, high-speed analytical queries on transactional data, and multi-model support—possible within a PostgreSQL environment. This is achieved by embedding DuckDB’s vectorized, columnar analytics engine directly into PostgreSQL, allowing hybrid transactional and analytical workloads without data duplication or separate systems. However, while it significantly bridges the gap, it doesn’t fully replicate SingleStore’s distributed scalability or real-time ingestion at petabyte scale in a single-node Postgres setup. Below, I’ll break it down by comparing to SingleStore’s advantages.Key Enablers in pg\_duckdb*

- *Release Status: pg\_duckdb reached version 1.0 in September 2025, marking it as production-ready with enhanced stability, parallel scanning, broader data type support, and MotherDuck cloud integration for offloading heavy workloads.*
- *How It Works: Install as a PostgreSQL extension (e.g., via Docker or source build). It automatically routes qualifying analytical queries to DuckDB’s engine while keeping transactional ops in Postgres. No SQL changes needed—set duckdb.force\_execution for DuckDB acceleration.*
- *Deployment: Works on self-hosted Postgres or managed services like Crunchy Bridge, Supabase, or Neon. Integrates with cloud storage (S3, Parquet, Iceberg) for data lakes.*

*Comparison to SingleStore AdvantagesHere’s how pg\_duckdb stacks up against the core SingleStore features discussed previously. It excels in analytics acceleration but trades off on massive distribution.*

***SingleStore Advantage***

***Achievable with pg\_duckdb?***

***Details & Limitations***

*Unified OLTP/OLAP*

*Yes (primary enabler)*

*Runs OLTP in native Postgres and accelerates OLAP via DuckDB on the same tables—no ETL or data movement. Benchmarks show 10-100x speedups on TPC-DS queries. Limitation: Best on read replicas to avoid OLTP interference; not fully seamless for ultra-high concurrency like SingleStore.*

*High-Speed In-Memory Processing with Tiered Storage*

*Partially*

*DuckDB uses in-memory columnar processing with spilling to disk/NVMe cache, but inherits Postgres’ row-oriented storage. Excels on columnar formats (e.g., Parquet via direct S3 queries). Limitation: Slower than SingleStore’s native hybrid for datasets >> RAM without replication.*

*Massive Horizontal Scalability*

*No (but extendable)*

*Single-node focus; scales via Postgres clustering or MotherDuck offload for cloud elasticity. Handles TB-scale analytics well but not petabyte distribution. Limitation: Lacks SingleStore’s automatic sharding/replication across nodes.*

*Multi-Model Data Support*

*Yes*

*Leverages DuckDB for JSON, geospatial, time-series, full-text, vectors (AI/ML), and Iceberg/Delta—queryable in ANSI SQL alongside Postgres extensions (e.g., PostGIS). New in v1.0: Broader type compatibility. Limitation: Vector indexes may need tuning for Postgres row storage.*

*Real-Time Ingestion and Query Performance*

*Partially*

*Supports sub-second analytics on live Postgres data; integrates Kafka-like ingestion via DuckDB pipelines or CDC (e.g., Supabase ETL). Limitation: Ingestion throughput (e.g., millions/sec) trails SingleStore without custom pipelines; better for batch/ad-hoc than streaming at scale.*

*Example Use Cases Now Possible*

- *Real-Time Dashboards: Query live Postgres OLTP data with DuckDB-accelerated aggregations for e-commerce insights.*
- *AI/ML on Hybrid Data: Join Postgres tables with S3 vectors for recommendation engines, using writable views.*
- *Cost-Effective Scaling: Offload to MotherDuck for spiky workloads, avoiding SingleStore’s full distributed cost.*

*Getting Started*

1. *Install: Use the official Docker image (ghcr.io/duckdb/pg\_duckdb:latest) or build from GitHub.*
2. *Enable: Add to shared\_preload\_libraries in postgresql.conf, then CREATE EXTENSION pg\_duckdb;.*
3. *Query: SET duckdb.force\_execution = on; SELECT \* FROM your\_postgres\_table GROUP BY...;—DuckDB handles the heavy lifting.*

*In summary, pg\_duckdb transforms Postgres into a viable SingleStore alternative for many HTAP scenarios, especially analytics acceleration on existing data. For distributed needs, consider combining with Postgres extensions like Citus. Check the [pg\_duckdb GitHub](https://github.com/duckdb/pg_duckdb) or [DuckDB docs](https://duckdb.org/docs) for the latest.*

I will only say that small data should win. So, yay for the [Kermadec future](https://tessellations.substack.com/p/the-data-studio-concept?utm_source=publication-search).

---

**Go Finally  
**The biggest news, aside from my gainful employment, is that I’m finally investing way more time in my programming skills which have been rusting away, literally and figuratively. I have given up on mastery of **Rust** and giving in to all of the seductive temptations of Go.

I never liked **Python**, but I felt I had to. As soon as it got to be something larger than scripting, I actually started to hate it. I never disliked **Ruby**, but the cult of Mats didn’t pay anywhere outside of the company I used to work for. But my biggest problem was that I never really bothered to do any coding on a daily basis outside of the immediate demands of the job, which was something I actually used to do back in my **Perl** days.

Now I am convinced that:

- Go has all of the routines I need for data engineering.
- Python is not dead to me, but it’s dead to me.
- I can and will re-engineer all of my old code instead of playing Borderlands 4

What’s weird is that I’m actually kind of jazzed about pair coding that stuff.

**Temporal  
**I’m probably going to overkill on this but I’m relatively convinced that this framework is the be all, end-all for managing everything automated. And since it has SDKs for every freaking language, especially Go, I’m going to sink some time into understanding it. Why? Because I’m too self-confident enough to say that **Dagster** and **Airflow** are not much better than cron, and [Temporal](https://temporal.io/) is what I really want.

Bottom line is that I’m convinced that Go routine concurrency and the long-term capabilities of Temporal pipelines are ideal for performance and flexibility for the back-end data pipelines of the future. The future meaning ML pipelines, + Agentic whatevers + LLM whatevers + all traditional ETL & ELT.

---

**ML Golf Bag**  
I honestly believe that if I listen to **Data Skeptic** long enough, I will have a reasonable heuristic to map data science verbiage to cross the gap between what I understand about KPIs of the corporate variety and the most fabulous artificial intelligence predictive models that actually keep people in business. That is as opposed to the PhD fuckery that keeps failing on the cutting edge of VC monetization. In other words, I’m taking the advice I heard **Stephen Pinker** say on **[Sean Carroll](https://www.preposterousuniverse.com/podcast/2025/09/22/329-steven-pinker-on-rationality-and-common-knowledge/)** this week.

90% of academic papers are wrong and 90% of textbooks are right. Given that 110% of AI hype is deceptive, I can take a year and get up to speed on everything that actually works.

All this boils down to this. Yes, I could be a data scientist, but picking the right algorithm can be done by an AI. All we need to do is map it. So I think a simple dirty RAG can polish that shoe. Spit shine, baby. Perplexity is my caddy, and all I need are a few ML clubs for most of the courses most of the time.

---

**OpenMetadata  
**This one has got me a little bit baffled. I’m running it locally and I have a Collate account, but I can’t seem to get it to refresh when I make updates to my schemata and table defs. I don’t see why this shouldn’t be brain dead simple even on the community edition. I’ll find the proper Slack forum one of these days.

And finally…

**Databricks**  
I’m throwing my hat into the **Databricks** collective. Not going to pay attention to Snowflake or Clickhouse. I can do everything I want with Postgres which I can host myself. I can sorta make use of DynamoDB for all the meta and fuzzy data. But I sticks with the ‘bricks. Now even though I want to stay out of the commodity business of **Fivetran** and **dbt** (which I think of analogously to how I got along 20+ years without Informatica), I figure I don’t need to know. Basically I think I’ll get to master what’s custom and do infrastructure as code with **n8n** and whatever I do with Temporal + Go. In other words, I think agentic slop is going to bulldoze Fivetraners and dbt’ers. So I’m hedging that.

---

![](https://substackcdn.com/image/fetch/$s_!PxD7!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffaf7579e-88ff-4a46-b57e-be5cb02ed20d_3743x2266.jpeg)

All this is Plan B. As long as I can make it work at Southwall, I can disconnect from the clouds and keep secrets. After all, how big do you think the Epstein files are anyway?