---
title: "Apache Iceberg: The Hadoop of the Modern Data Stack?"
source: https://blog.det.life/apache-iceberg-the-hadoop-of-the-modern-data-stack-c83f63a4ebb9
author:
  - "[[Dani]]"
published: 2024-12-13
created: 2025-03-14
description: In the early 2010s, Apache Hadoop dominated the big data conversation. Organizations raced to adopt it, seeing it as the cornerstone for scalable, distributed storage and processing. Today, Apache…
tags:
  - hadoop
  - iceberg
---
Featured

![An elephant on an iceberg](https://miro.medium.com/v2/resize:fit:700/0*-G1xL7Lc8KtFb1X3)

In the early 2010s, [Apache Hadoop](https://hadoop.apache.org/) dominated the big data conversation. Organizations raced to adopt it, seeing it as the cornerstone for scalable, distributed storage and processing. Today, [Apache Iceberg](https://iceberg.apache.org/) is emerging as a cornerstone for data lakes and lakehouses in the modern data stack.

And yet, for those who lived through the “Big Data era,” a deeper look reveals striking parallels between Iceberg’s trajectory and the story of Hadoop.

Let’s explore these parallels and what they mean for the future of data engineering.

## Adoption Frenzy: Solving the Right Problem at the Right Time

![Hadoop google trends over the years](https://miro.medium.com/v2/resize:fit:700/0*gS1Gzd0xJ8WPpGe3)

Hey it’s an Iceberg!

Hadoop’s rise was fueled by an urgent need for distributed file storage and processing, offering a solution to the “big data deluge.” Similarly, Iceberg addresses a core problem in data lakes: managing large, constantly evolving datasets with ACID compliance and schema evolution.

However, technology adoption often operates on a pendulum — the promise of solving a significant pain point drives rapid adoption, even when operational readiness lags. Hadoop’s meteoric rise led many organizations to implement it without understanding its complexities, often resulting in underutilized clusters or over-engineered architectures. Iceberg is walking a similar path. The ability to unify batch and streaming workloads, combined with features like schema evolution, has made it an alluring choice. Yet, Iceberg’s adoption often outpaces organizations’ abilities to operationalize it effectively.

The lesson here is timeless: Adoption should be driven by alignment with organizational maturity. Jumping on the Iceberg bandwagon without a clear data strategy can lead to technical debt and unmet expectations. For example, a fintech company might adopt Iceberg for ACID guarantees in their fraud detection pipelines but grapple with compaction strategies because their streaming setup generates too many small files.

Successful Iceberg adoption requires the same care as Hadoop — focusing on skill-building, workload alignment, and incremental integration.

## The Small Files Problem Redux

One of Hadoop’s most infamous pain points was the “small files problem.” HDFS wasn’t designed to handle many small files efficiently, leading to bottlenecks and degraded performance. Organizations often resorted to nightly compaction jobs or elaborate ETL pipelines to aggregate data.

Iceberg is not immune to this issue. While it abstracts much of the storage layer, small files remain a persistent challenge. For instance, streaming data pipelines or frequent incremental writes can lead to performance degradation due to excessive metadata overhead. Tools like Apache Spark and Flink — commonly used with Iceberg — magnify this issue if not carefully tuned.

However, the issues don’t stop there; the small file problem considerably impacts object storage costs (think of the number of requests toward S3), exponential extra computing is required for compaction, and so on.

For example, consider a retail company capturing clickstream data. A poorly configured Flink job writes data into Iceberg tables with a default file size of 10 MB. Over time, these small files pile up, bloating the metadata catalog and slowing down query performance. Implementing periodic compaction jobs and tuning Flink’s file size thresholds could alleviate this problem.

As a counterexample, Estuary Flow utilizes a few tricks to [stream data into the underlying Parquet files efficiently](https://estuary.dev/memory-efficient-streaming-parquet/). It also allows users to stagger data materializations even in a streaming environment to align with compaction schedules.

File size tuning and write strategies are critical. Use tools like Apache Spark’s adaptive query execution to optimize partitioning or leverage Iceberg’s built-in compaction utilities to merge small files periodically. Ignoring these tasks can turn a promising Iceberg deployment into a performance bottleneck.

## A Complex Stack to Maintain

![machine learning AI data landscape of tools](https://miro.medium.com/v2/resize:fit:700/0*JaP5lqTvsLyA0mPt)

Source: [https://mad.firstmark.com/](https://mad.firstmark.com/)

Hadoop was never a standalone product. It required a constellation of tools — HBase for real-time reads, Hive for SQL queries, and Spark for advanced analytics. Managing this complexity demanded specialized skill sets and sophisticated orchestration.

Iceberg, despite its simplifications, is no different. Its power lies in its ecosystem: query engines (Trino, Spark, Flink), storage backends (S3, GCS, HDFS), and catalogs (Hive, Glue, Nessie, Polaris, Unity, the REST Catalog, and probably many more..). The configuration options can be overwhelming. For example, partitioning strategies can significantly impact query performance, and selecting the wrong catalog implementation might limit scalability.

This complexity highlights a broader truth: No tool is an island. The success of Iceberg depends not just on its features but on the ecosystem around it. Companies that excel with Iceberg often adopt a “platform engineering” mindset, creating internal tooling and automation to manage metadata, monitor performance, and orchestrate workloads.

## Metadata Overhead: A New Kind of Complexity

Hadoop’s NameNode bottleneck exemplified how metadata management could derail performance. With its distributed snapshot-based metadata model, Iceberg avoids this single point of failure but introduces its own challenges. As table sizes grow, so do snapshots and manifests, leading to bloated metadata stores.

A media company uses Iceberg to manage petabytes of video analytics data. Over time, their snapshot history grows unchecked, causing query planning times to increase. By implementing periodic snapshot expiration and manifest compaction, they keep their query performance consistent while controlling metadata growth.

My tip: Treat metadata as a first-class citizen. Automate snapshot pruning and compaction tasks and invest in monitoring solutions that surface metadata bottlenecks early.

## Build vs. Buy

Hadoop’s early days required organizations to build everything from scratch. Managed services like Cloudera and AWS EMR eventually simplified adoption but came with trade-offs in cost and flexibility.

Iceberg users face a similar decision. Self-hosting offers maximum control but requires expertise in scaling and tuning. Managed solutions like Snowflake’s Iceberg tables or Starburst Galaxy reduce operational overhead but can limit flexibility and lead to vendor lock-in.

The decision boils down to your organization’s core competencies. If your team already excels in DevOps, self-hosting may offer the best ROI. Conversely, smaller teams or those new to Iceberg might benefit from managed services to jumpstart adoption.

## The Community Effect: Vibrant, Yet Fragmented

![Social engagement around the Iceberg project](https://miro.medium.com/v2/resize:fit:700/0*YDQ4FVPVpnLMQhUu)

Source: [https://www.linkedin.com/posts/ydolan\_in-the-last-2-years-most-of-my-apache-iceberg-activity-7256666018935173121-ofqB/](https://www.linkedin.com/posts/ydolan_in-the-last-2-years-most-of-my-apache-iceberg-activity-7256666018935173121-ofqB/)

Hadoop thrived on open-source collaboration, but its fragmentation — Spark vs. MapReduce, Hive vs. Impala — often created confusion. Iceberg benefits from a vibrant open-source community. Yet, competing table formats like Delta Lake and Hudi mirror this fragmentation.

While competition drives innovation, it can also stall adoption. Standardization efforts — such as integrating Iceberg more deeply with query engines — will be crucial for its long-term success. The emergence of interoperability layers, akin to the “Hive Metastore” era, may define the next chapter for Iceberg.

## What’s Next for Iceberg?

Despite its parallels to Hadoop, Iceberg benefits from hindsight. The data community has learned to prioritize simplicity, scalability, and cloud-native architectures. Here are key trends to watch:

## 1\. Consolidation

Just as Spark emerged as the dominant engine in the Hadoop ecosystem, a dominant table format and catalog may appear in the Iceberg era. This consolidation will drive standardization, whether Iceberg itself or a future innovation.

Projects like [Apache XTable](https://xtable.apache.org/) are working on making interoperability super easy among table formats.

## 2\. Operational Maturity

The next wave of Iceberg tools will focus on reducing operational complexity. Managed services and orchestration frameworks are already emerging, following the footsteps of Databricks and Snowflake.

Amazon’s recently announced [S3 Tables](https://estuary.dev/s3-tables-for-apache-iceberg/) is an excellent example of this. It abstracts away the complexities of maintaining Iceberg tables and offers a built-in catalog, although this has a side effect of reduced compatibility with the rest of the ecosystem.

## 3\. Beyond Analytics

Iceberg’s support for streaming and transactional workloads positions it as more than an analytics tool. Imagine using Iceberg to power event-driven architectures or real-time machine learning pipelines — scenarios that push beyond traditional batch processing.

[Estuary Flow’s Iceberg connector](https://estuary.dev/destination/s3-iceberg/) is a good example of the table format that can be integrated into real-time streaming projects.

## Final Thoughts

![](https://miro.medium.com/v2/resize:fit:700/0*0Wm2OH8fq6J5dNVq.jpg)

Iceberg is here to stay

Apache Iceberg is undeniably transformative, much like Hadoop was a decade ago. But with great power comes great complexity. As with any tool in the modern data stack, success lies in aligning the technology with your organization’s readiness, skill set, and strategic goals.

While the parallels to Hadoop are striking, we also have the opportunity to avoid its pitfalls. By learning from the past, we can ensure that Iceberg isn’t just the Hadoop of the modern data stack — it’s the evolution we’ve been waiting for.