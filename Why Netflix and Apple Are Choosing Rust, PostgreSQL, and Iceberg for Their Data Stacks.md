---
title: "Why Netflix and Apple Are Choosing Rust, PostgreSQL, and Iceberg for Their Data Stacks"
source: "https://blog.devgenius.io/why-netflix-and-apple-are-choosing-rust-postgresql-and-iceberg-for-their-data-stacks-985242ff564e"
author:
  - "[[RisingWave Labs]]"
published: 2025-05-12
created: 2025-05-17
description: "From LinkedIn to Apple, Netflix to Tencent, today’s leading tech companies are converging on a common set of technologies to manage their ever-growing, real-time data pipelines. These choices aren’t…"
tags:
  - "clippings"
---
## [Dev Genius](https://blog.devgenius.io/?source=post_page---publication_nav-4e2c1156667e-985242ff564e---------------------------------------)

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*S0OuPFz_CHFFMbBI0wenjA.png)

𝐅𝐞𝐚𝐭𝐮𝐫𝐞𝐬 𝐂𝐡𝐚𝐧𝐠𝐞. 𝐈𝐧𝐭𝐞𝐠𝐚𝐫𝐚𝐭𝐢𝐨𝐧𝐬 𝐞𝐯𝐨𝐥𝐯𝐞. 𝐏𝐫𝐢𝐜𝐢𝐩𝐥𝐞𝐬 𝐞𝐧𝐝𝐮𝐫𝐞. (Image Created by the Author)

> *“We’ve seen a structural shift in how modern data infrastructure is built.”*

From LinkedIn to Apple, Netflix to Tencent, today’s leading tech companies are converging on a common set of technologies to manage their ever-growing, real-time data pipelines. These choices aren’t random — they reflect deeper shifts in how we build for scale, openness, and flexibility.

In this post, I’ll unpack why technologies like **Rust**, **PostgreSQL**, **S3**, and **Apache Iceberg** are quietly becoming the new foundation of the modern data stack — and how we’ve brought them together in **RisingWave**, a next-gen cloud-native streaming database.

## 🚀 Rust: Performance Meets Safety

Rust has become a favorite among systems developers — and for good reason.

- Most admired language (83%) — Stack Overflow 2024
- 42,712 daily downloads from [crates.io](http://crates.io/)
- Thriving communities: `r/rust` (322k), `r/learnrust` (31k), `r/rust_gamedev` (40k)
- Adopted by AWS, Dropbox, Cloudflare, and many database vendors

Rust’s safety guarantees and zero-cost abstractions make it ideal for high-performance, concurrent, and scalable systems like modern streaming engines.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*upjUGUjy5MzsSz_YxvZ2yw.png)

Rust: Growth, Adoption and Community Momentum. (Image created by the author)

## 🐘 PostgreSQL: SQL That Just Works (and Scales)

PostgreSQL has evolved from a reliable OLTP database into a foundational protocol for today’s data infrastructure.

- DBMS of the Year — three consecutive wins (DB-Engines 2024)
- Used by 48.7% of developers — Stack Overflow 2024
- Compatible with Spark, Flink, dbt, BI dashboards
- The core interface for new databases like TimescaleDB and RisingWave

Its rich ecosystem and long-term stability make it the default SQL layer for many modern data platforms.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*OxJ8B1rOFuZ9ZdndpsvshQ.png)

PostgreSQL: DBMS of the Year (2024) — 3rd consecutive win. (Image Created by the Author)

## ☁️ Amazon S3: The Storage Workhorse Behind Cloud Data

Amazon S3 is more than a storage service — it’s a platform.

- 350 trillion objects stored
- 100M+ requests per second
- 11 nines (99.999999999%) durability
- Adopted by MinIO, R2, DigitalOcean, IBM Cloud, and more

With its scale, simplicity, and API compatibility, S3 has become the universal storage layer for everything from analytics to AI.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*3RwDEKbEgfLLk_eXZkUSZw.png)

Amazon S3: Scale, Speed and Standard. (Image Created by the Author)

## ❄️ Apache Iceberg: The New Default for Open Data Lakes

Iceberg is redefining how we manage large-scale analytical data.

- Adopted by Netflix, Apple, AWS, Adobe, LinkedIn, Tencent, and Pinterest
- Ecosystem momentum: Databricks acquired Tabular, Snowflake launched Polaris Catalog, Dremio built a Hybrid Iceberg Catalog
- Supported by Trino, BigQuery, Flink, StarRocks, Redpanda, and more
- Enables batch-streaming unification, zero-ETL architectures, and open data governance

Iceberg isn’t just a format — it’s a modern contract for interoperable, vendor-neutral data infrastructure.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*eXe_FQFRWrldRXWeGX4atw.png)

Apache Iceberg: The Open Data Format of the future. (Image Created by the Author)

## 💡 Bringing It All Together in RisingWave

At [RisingWave](https://www.risingwave.com/), we’ve built our streaming-first database on these exact foundations:

- **Rust** for a fast and safe core engine
- **PostgreSQL protocol** to keep things familiar and interoperable
- **Amazon S3** as the default low-cost, scalable storage layer
- **Apache Iceberg** to connect streaming and historical data into a single queryable system

With RisingWave, developers can use simple SQL to ingest, process, and analyze real-time data — no lock-in, no proprietary layers, just open standards done right.

An open-source distributed SQL streaming database designed for the cloud. [https://risingwave.com/](https://risingwave.com/). [https://go.risingwave.com/slack](https://go.risingwave.com/slack)

## More from RisingWave Labs and Dev Genius

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--985242ff564e---------------------------------------)