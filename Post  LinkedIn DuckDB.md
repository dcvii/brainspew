---
title: Post | LinkedIn
source: https://www.linkedin.com/posts/medriscoll_aicouncil-share-7460452137131565056-NUMB/
author:
published:
created: 2026-05-20
description:
tags:
  - brain_spew
  - duckdb
---
Postgres has had a good 30-year run – is DuckDB coming for its crown?  
  
Yesterday at his [**#AICouncil**](https://www.linkedin.com/search/results/all/?keywords=%23aicouncil&origin=HASH_TAG_FROM_FEED) keynote, DuckDB's co-creator [**Hannes Mühleisen**](https://www.linkedin.com/in/hfmuehleisen/) unveiled a shot across the bow: a new client-server protocol called Quack.  
  
This is a foundational shift, enabling DuckDB to move beyond its roots as an in-process, single-node, analytics database towards more general purpose use cases.  
  
With Quack, DuckDB supports transaction-oriented workloads: fast inserts, parallel writes, and syncing read replicas. DuckDB's Quack is 36X faster than Postgres for bulk inserts, and rivals Postgres performance for transaction throughput on smaller inserts. \[1\]  
  
More broadly, Quack provides a core primitive for building distributed systems with DuckDB, now with a native, highly optimized remote procedure call protocol to coordinate across clusters of database nodes. [**MotherDuck**](https://www.linkedin.com/company/motherduck/), who operate the leading DuckDB-powered cloud database, has undoubtably inspired and influenced Quack's architecture.  
  
Hannes has been contemplating how a better protocol would work for years: he and DuckDB co-creator [**Mark Raasveldt**](https://www.linkedin.com/in/mark-raasveldt-256b9a70/) authored a paper in 2017 titled "A Case for Client Protocol Redesign" where they mused about the inefficiencies of the then-current, and still-used approaches.  
  
Brick by brick, the [**DuckDB**](https://www.linkedin.com/company/duckdb/) team members are rewriting the foundations of databases and data infrastructure for the modern era: more ergonomic SQL (c.f. GROUP BY ALL), a simpler data lake (DuckLake), a faster SQL parser (PEG not YACC), and much, much more.  
  
As Hannes said on stage yesterday, "Maybe it's time to use a database built after 2000." Ultimately, the world of developers will be the final judge.  
  
\[1\] For a 60M row bulk insert, DuckDB's Quack finished in 5 seconds, vs Postgres' 20 seconds. For small inserts with 8 clients, DuckDB's Quack supported 5000 transactions per second, slightly faster than Postgres.

[

](https://www.linkedin.com/posts/medriscoll_aicouncil-share-7460452137131565056-NUMB/)