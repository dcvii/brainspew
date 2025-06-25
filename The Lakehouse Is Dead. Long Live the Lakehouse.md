---
title: "The Lakehouse Is Dead. Long Live the Lakehouse"
source: "https://medium.com/@tfmv/the-lakehouse-is-dead-long-live-the-lakehouse-fd12241ce840"
author:
  - "[[Thomas F McGeehan V]]"
published: 2025-06-09
created: 2025-06-13
description: "A critique of modern data architecture bloat and a call to rebuild the lakehouse with simplicity, performance, and developer sanity in mind."
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

![Split cartoon image contrasting two data architectures. Left panel labeled “Lakehouse” shows a boot sinking into a muddy swamp with a shovel and a “Metadata Swamp” warning sign. Right panel labeled “Lean Stack” shows a cheerful duck standing on grass under a rainbow, labeled “DuckDB.”](https://miro.medium.com/v2/resize:fit:640/format:webp/1*W_L5rDhvVKB7zIRmgzUkJg.png)

Split cartoon image contrasting two data architectures. Left panel labeled “Lakehouse” shows a boot sinking into a muddy swamp with a shovel and a “Metadata Swamp” warning sign. Right panel labeled “Lean Stack” shows a cheerful duck standing on grass under a rainbow, labeled “DuckDB.”

You’ve just stood up a pristine Iceberg table on S3. You’ve configured Hive metastore, wired up your catalog, scheduled your compaction jobs, and written a 300-line Airflow DAG to orchestrate it all. Your data is now governed, versioned, and warehouse-ready.

So why does everything still suck?

Your dashboards are slow. Your pipelines are brittle. Your devs are drowning in config files. And you’re starting to suspect ==this revolution looks a lot like a really fancy folder of Parquet files with a PhD in distributed systems.==

Welcome to the lakehouse. Population: you, three Kubernetes clusters, and a YAML file so long it has a table of contents.

## The Unified Theory of Everything Wrong

The lakehouse was supposed to unify the warehouse and the lake. Instead, it unified the worst parts of both.

Meet the villain — Platform Maximalism. The belief that more layers equals more enterprise-ready. That abstraction is sophistication. That if your data stack doesn’t require a dedicated platform team, you’re not doing it right.

We were promised elegance. What we got was:

- Distributed file systems pretending to be databases
- Query engines pretending to be storage layers
- Metadata catalogs pretending to be source control
- Orchestrators pretending to be operating systems
- Observability tools pretending to explain any of it

The result is a beautiful blueprint with a dozen points of failure and exactly zero people who understand the whole stack.

> “It’s not a revolution. It’s a rebrand with extra metadata.”

## The House Always Wins

Here’s the dirty secret — Iceberg, Delta, and Hudi are genuinely impressive pieces of engineering. Time travel queries? Snapshot isolation? Schema evolution? These are hard problems, elegantly solved.

But power isn’t the problem. Gravity is.

The moment you adopt a table format, everything else in your stack starts orbiting it. Your query engines become format-aware. Your pipelines become catalog-dependent. Your monitoring becomes metadata-driven. Your developers become YAML archaeologists.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*9PQ5ud15GRIIrdsvAj2TDQ.png)

Figure 1 — Eight layers of abstraction to read a file

We’ve re-centralized control in the name of flexibility. The catalog is the new single point of failure, dressed up as the solution to single points of failure.

==Most organizations using lakehouses could accomplish 90% of their goals with a well-configured Postgres and some scheduled== ==`pg_dump`== ==scripts. But that doesn't make for compelling conference talks.==

## The Orchestration Tax

Want to know the real cost of your lakehouse? Count the systems that need to stay synchronized for a single query.

1. Object storage (S3, ADLS, GCS)
2. Table format (Iceberg, Delta, Hudi)
3. Metadata catalog (Hive, Glue, Unity Catalog)
4. Query engine (Spark, Trino, Athena)
5. Orchestrator (Airflow, Prefect, Dagster)
6. Transformation layer (dbt, Dataform)
7. Serving layer (Snowflake, BigQuery, ClickHouse)
8. API gateway (because of course)

That’s eight moving parts for what used to be `SELECT * FROM table`. Each one has its own configuration, monitoring, alerting, backup strategy, and inevitable 3 AM page.

*“But wait,”* you say, *“we get ACID transactions!”*

Show me the person who can debug a failed ACID transaction that spans four AWS services and involves schema evolution conflicts during a compaction job triggered by a misconfigured retention policy.

I’ll wait.

## KISS the Lakehouse Goodbye

Here’s the uncomfortable truth — most organizations don’t need a lakehouse. They need a SQL engine that doesn’t file a support ticket when it sees a semicolon.

Complexity became the selling point instead of the warning label.

Pop quiz — Do you really need snapshot isolation and merge-on-read for your 12-person startup’s customer analytics?

Follow-up question — When was the last time you actually used time travel queries for anything other than showing them off in a demo?

## Lakehouse Lies We Tell Ourselves

```c
+----------------------------------------------------+-------------------------------------------------------------+
| The Hype                                           | The Reality                                                 |
+----------------------------------------------------+-------------------------------------------------------------+
| We need ACID transactions for analytics            | Fresh insights beat perfect consistency                     |
| Schema evolution is critical for our business      | You've tweaked schemas only twice in three years            |
| We're planning for massive scale                   | Your largest table holds just 10 million rows               |
| Time-travel queries are indispensable              | You've used them only once—to recover a dropped table       |
| Our data is too complex for simple tools           | Your CEO only asks "how much?" and "how many?"              |
```

## The Configuration Burden

Here’s what “simple” looks like in lakehouse land:

```c
# Just the basics for Iceberg + Spark + Hive
spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions
spark.sql.catalog.spark_catalog.type=hive
spark.sql.catalog.local.warehouse=s3a://my-bucket/warehouse
# Plus 47 more hive-site.xml properties...
# Plus 200 lines of Airflow DAG logic...
```

Now here’s the DuckDB version:

```c
COPY (SELECT * FROM 'my_data.parquet') TO 's3://foo-bucket/foo.parquet';
```

One of these approaches will still work in five years. Hint — it’s not the one that requires a Spark cluster.

## What’s Next — The Duck Revolution

DuckDB flipped the script. So did tools like DuckLake. So did the resurgence of SQLite for analytics workloads.

They asked a simple question — What if we optimized for understanding instead of scale?

The answer is beautiful. Local-first. Human-scale. Actually debuggable.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*SEHvNrKf8Vft4UBF0sk5Pg.png)

Figure 2 — Three layers to enlightenment

Instead of Iceberg + Hive + Spark + Airflow + dbt + Looker  
Try DuckDB + FlightSQL + whatever you’re already using.

Instead of complex schema evolution with table format versioning  
Try `ALTER TABLE` statements that actually work.

Instead of distributed query planning across multiple services  
Try SQL that runs where your data lives.

FlightSQL and Arrow give you protocol-native access without the ceremony.

```c
# Old way - Configure Spark, connect to cluster, hope everything works
spark = SparkSession.builder.appName("Analytics").enableHiveSupport().getOrCreate()
df = spark.sql("SELECT * FROM iceberg.analytics.events").toPandas()

# New way - Just query the damn data
import duckdb
df = duckdb.connect().execute("SELECT * FROM 's3://bucket/events.parquet'").df()
```

One approach lets you iterate quickly. The other lets you write blog posts about “big data engineering best practices.”

And maybe even land a conference talk about how you debugged it once. In prod.

## Edge-Native Reality

Your laptop has 32GB of RAM and an NVMe SSD. It can process most “big data” workloads faster than your distributed cluster can *schedule* them.

Tools like DuckLake bring computation to where data already lives. The future isn’t centralized; it’s composable, lean, and boring in the best possible way.

## When You Actually Need Complexity

I’m not saying lakehouses are always wrong. If you’re processing petabytes with hundreds of concurrent users and complex governance requirements, knock yourself out.

But if you’re a startup with under 100GB of data, an enterprise team with clear ownership, or anyone who values shipping features over managing infrastructure — then maybe you don’t need to solve distributed systems problems you don’t have.

## The Death and Resurrection

The lakehouse isn’t dead because it failed. It’s dead because it won, and now we see what that win cost us.

We traded simplicity for sophistication. Understanding for abstraction. Debuggability for distributed perfection.

The lake was messy but flexible. The warehouse was rigid but reliable. The lakehouse promised to fix both problems and created a third — complexity that requires a platform team to operate and a PhD to debug.

We don’t need smarter platforms. We need simpler foundations.

The future isn’t about building a house on a lake. It’s about remembering that sometimes, the best place to store data is in a file. The best place to query data is where it lives. And the best way to process data is with tools you can understand.

## Your Recovery Program

If you’re ready to leave the lakehouse behind:

1. Admit you have a problem. Your data pipeline has more moving parts than a Rube Goldberg machine.
2. Start small. Replace one complex pipeline with DuckDB + a cron job.
3. Measure what matters. Compare debuggability and time-to-insight, not just throughput.
4. Embrace boring technology. The newest table format won’t solve your organizational problems.
5. Build for understanding. If your junior engineers can’t debug it, it’s too complex.
6. Ship features, not infrastructure. Your users don’t care about your architecture.

We’ve seen the future. It’s not distributed. It’s understandable.

Full disclosure. I have not used it, but I trust the builder and this [boring pipeline framework](https://www.boringdata.io/) might be exactly the kind of sanity-preserving tool your stack needs, though there is an associated cost.

I write about AI, data systems, edge computing, and small tools that punch above their weight. I build tools and toys. [www.github.com/TFMV](http://www.github.com/TFMV)

## Responses (2)

Michael David Cobb Bowen

What are your thoughts?  

==this revolution looks a lot like a really fancy folder of Parquet files with a PhD in distributed systems.==

```c
Lol relatable. I think I said this a few weeks ago about our new platform. The followup question was "are the schema names just folder names?"

 It's actually kind of funny, I'm currently far from office. Any offices. At lunch. And two data engineersn at the next table are complaining about migrations.
```

12

```c
This hits hard! A lot of data teams out there don't keep their feet on the ground. Running shiny tech after shiny tech, overcomplicates the matters. Great read!
```

5

## More from Thomas F McGeehan V

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--fd12241ce840---------------------------------------)