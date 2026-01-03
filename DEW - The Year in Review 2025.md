---
title: "DEW - The Year in Review 2025"
source: "https://www.dataengineeringweekly.com/p/dew-the-year-in-review-2025?publication_id=73271&post_id=182368564&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Ananth Packkildurai]]"
published: 2025-12-22
created: 2025-12-22
description: "From Digital Plumbers to Architects of Intelligence: The 7 Paradigm Shifts That Defined 2025"
tags:
  - "clippings"
---
### From Digital Plumbers to Architects of Intelligence: The 7 Paradigm Shifts That Defined 2025

![](https://substackcdn.com/image/fetch/$s_!uS1U!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1668a0fa-db0f-455b-b17a-8b8388d4dded_2816x1536.heic)

If 2023 was the year of “Shock” and 2024 was the year of “Hype,” 2025 will be remembered as the year of **Engineering**.

For the past decade, our industry has been obsessed with the mechanics of movement. We argued about “ETL vs. ELT.” We fought “Format Wars” over table specifications. We optimized commit protocols and debated the merits of various orchestrators. We were, fundamentally, digital plumbers ensuring the water reached the tap.

But in 2025, the mandate changed. The business no longer wants “data”; it demands “intelligence.” It demands systems that reason, agents that act, and infrastructure that guarantees truth in a non-deterministic world. The “Big Data” era of managing volume formally ended, replaced by the “Context Era” of managing meaning.

We are no longer just Data Engineers. We are the architects of the cognitive layer.

Here are the seven patterns that defined Data & AI Engineering in 2025.

---

## 1\. Agent Engineering: The Inevitable Evolution of the Pipeline

The most significant shift of 2025 was the industry’s realization that “Agents” are not just fancy chatbots—they are the new compute engine. In 2024, we treated LLMs as text generators. In 2025, we started treating them as reasoning engines that execute logic we previously wrote in Python or SQL.

This birthed a new discipline: **Agent Engineering**.

We moved beyond the chaotic “vibes-based” coding of early experiments into structured, rigorous engineering. We stopped asking “Can AI write code?” and started asking “How do we architect a system where AI reliably executes complex workflows?”

## The Rise of Context Engineering

The bottleneck for intelligent systems shifted from *model capacity* to *context management*. We realized that an agent is only as smart as the context you feed it.

Anthropic defined the year with their masterclass on **[Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)**, framing it as a discipline focused on managing the “attention budget” of models. It wasn’t enough to dump documents into a prompt. Engineers at Manus demonstrated that we must curate, compress, and dynamically retrieve tokens during inference to sustain coherent behavior over long horizons in their piece on **[Context Engineering for AI Agents](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus)**.

We learned that “Context” is an information management problem. We saw teams optimizing “KV-cache hit rates” and treating context windows like precious RAM. The winning architecture wasn’t the one with the biggest model; it was the one that engineered the most relevant context.

## The USB-C of Intelligence: Model Context Protocol (MCP)

History will likely view the introduction of the **Model Context Protocol (MCP)** as the moment agents became viable enterprise software. Before MCP, connecting an LLM to a database or API was a bespoke, brittle integration task.

In 2025, MCP standardized this connection. It became the “USB-C for Agents,” allowing developers to build a connector once and have it work across any MCP-compliant model or application, as detailed in Alibaba’s **[comprehensive analysis of MCP features](https://www.alibabacloud.com/blog/a-comprehensive-analysis-and-practical-implementation-of-the-new-features-in-the-mcp-specification_602206)**. However, the rollout wasn’t without caution; TigerData engineers noted that while MCP solved interoperability, it introduced new attack vectors, arguing that **[security is its Achilles heel](https://www.tigerdata.com/blog/three-tigerdata-engineers-told-us-the-truth-about-mcp-security-is-its-achilles-heel)**.

## From Chatbots to Colleagues

The proof was in the production deployments. Uber revealed **[Genie](https://www.uber.com/blog/enhanced-agentic-rag/)**, an internal agent that didn’t just answer questions but also acted as a “near-human” subject-matter expert. LinkedIn unveiled its **[Hiring Assistant](https://www.linkedin.com/blog/engineering/ai/accelerating-llm-inference-with-speculative-decoding-lessons-from-linkedins-hiring-assistant)**, an agent that handled complex recruiting workflows using speculative decoding to accelerate inference.

These weren’t toys. They were engineered systems with rigorous orchestration, state management, and error handling. The industry formalized patterns like “Prompt Chaining,” “Routing,” and “Parallelization.” We stopped treating agents as magic boxes and started treating them as software components that required a new kind of engineering.

---

## 2\. “Evals” Are The New Unit Tests

If Agent Engineering was the engine of 2025, **Evaluation (Evals)** was the brakes—and the steering wheel.

The “Vibe Coding” era—where we judged models by looking at a few outputs and saying “looks good to me”—died a hard death. In 2025, organizations realized they could not ship non-deterministic software without rigorous, deterministic measurement.

## The “Judge-LLM” Pattern

How do you test a system that gives a different answer every time? You build a machine to grade the machine.

The industry standardized around the **Judge-LLM** framework. Booking.com offers **[practical tips for LLM evaluation](https://booking.ai/llm-evaluation-practical-tips-at-booking-com-1b038a0d6662)**, using a “stronger” model (trained on a “Golden Dataset” of human-verified answers) to grade the outputs of “weaker,” cheaper production models. Pinterest followed suit with its **[LLM-powered relevance assessment](https://medium.com/pinterest-engineering/llm-powered-relevance-assessment-for-pinterest-search-b846489e358d)**, replacing costly manual labeling with fine-tuned LLMs that achieved high agreement with human experts.

This wasn’t just about checking for “correctness.” We developed specific metrics for **Hallucination Rate**, **Instruction Following**, and **Tone Consistency**. Uber built **[Requirement Adherence systems](https://www.uber.com/en-IN/blog/requirement-adherence-boosting-data-labeling-quality-using-llms/)** that extracted rules from standard operating procedures (SOPs) and enforced them in real-time, reducing post-labeling audits by 80%.

## Evaluation-Driven Development (EDD)

“Test-Driven Development” (TDD) evolved into **Evaluation-Driven Development (EDD)**. Engineers learned that you cannot optimize what you cannot measure.

Infrastructure teams integrated these evals directly into CI/CD pipelines. Databricks shared how they “shifted left” on reliability, **[scaling database reliability](https://www.databricks.com/blog/databricks-databricks-scaling-database-reliability)** by embedding schema scorers into their build processes to catch data quality issues before they hit production.

The takeaway for every data engineer in 2025 was clear: If you don’t have an eval for it, it doesn’t exist. You aren’t “prompt engineering” until you have a metric that tells you if your changes made things better or worse.

---

## 3\. The Streaming-Lakehouse Merger: The End of Lambda Architecture

For fifteen years, we lived with the “Lambda Architecture”—maintain a fast streaming path (Kafka/Flink) and a slow batch path (Hadoop/Spark), and pray they match. In 2025, we finally merged the lanes.

The barrier between “Stream” and “Table” dissolved. We entered the era of the **Streaming Lakehouse**.

## Stream-Table Duality

The concept of “Stream-Table Duality”—long preached by Kafka’s creators—became a reality in storage. New engines like **Apache Paimon** and **Apache Fluss** emerged to bridge the gap.

Alibaba championed **[Apache Paimon](https://www.alibabacloud.com/blog/apache-paimon-real-time-lake-storage-with-iceberg-compatibility-2025_602485)** as a lake format designed specifically for real-time updates, offering the high-throughput ingestion of a stream with the query capabilities of a lakehouse table. Jack Vanlightly’s deep dive into **[Understanding Apache Fluss](https://jack-vanlightly.com/blog/2025/9/2/understanding-apache-fluss)** revealed a system that combines log tablets with KV tablets, effectively creating a database that exposes its own changelog as a first-class citizen.

We stopped debating “Stream vs. Batch” and started designing architectures that ingest data once and make it immediately available for both real-time operational lookups and historical analytical queries.

## The Zero-Copy Debate

However, this merger wasn’t without conflict. The buzzword of the year was “Zero-Copy”—the promise that you could point your data warehouse at your Kafka topic and query it without moving bytes.

But seasoned engineers pushed back. WarpStream argued **[the case for an Iceberg-native database](https://www.warpstream.com/blog/the-case-for-an-iceberg-native-database-why-spark-jobs-and-zero-copy-kafka-wont-cut-it)**, claiming that coupling your operational message bus directly to your analytical engine violates separation of concerns.

The consensus that emerged? “Zero-Copy” is great for ad-hoc exploration, but for production, **Materialization** (making a copy) is still the price of performance and isolation.

## Diskless Kafka and the Cloud-Native Log

Even Kafka itself couldn’t escape the modernization wave. The community rallied around **[KIP-1150 (Diskless Topics)](https://topicpartition.io/blog/kip-1150-diskless-topics-in-apache-kafka)**, a proposal to re-architect Kafka for the cloud era.

We realized that in a world of S3 Express and high-speed networking, storing data on local broker disks was an expensive relic. The future of streaming is “Tiered Storage by Default,” where the broker is just a caching layer on top of infinite object storage. This shift promises to slash costs and make “infinite retention” streams a standard architectural pattern.

---

## 4\. The Efficiency Counter-Revolution: Small Data and Rust

While the AI teams were burning cash on GPUs, the Data Infrastructure teams were leading a quiet counter-revolution. After years of defaulting to massive, expensive distributed clusters (Spark/Hadoop) for every problem, 2025 was the year we right-sized our compute.

We realized that “Big Data” tools are overkill for “Medium Data” problems.

## The Single-Node Renaissance

“Does this really need a 50-node cluster, or just a bigger laptop?”

That question dismantled pipelines across the industry. Tools like **DuckDB** and **Polars** graduated from “analyst favorites” to “production workhorses.” Decathlon shared a viral case study about being **[Ready to Play with Polars](https://medium.com/decathlondigital/polars-at-decathlon-ready-to-play-6abc4328d06c)**, replacing massive Spark clusters with Polars scripts for datasets under 50GB and slashing infrastructure costs to near zero.

Benchmarks from Daniel Beach confirmed this, showing that for **[650GB of Data (Delta Lake on S3)](https://dataengineeringcentral.substack.com/p/650gb-of-data-delta-lake-on-s3-polars)**, single-node engines often beat distributed clusters simply by avoiding network overhead. We stopped being ashamed of “vertical scaling” and started embracing it as a FinOps victory.

## The Rust Rewrite

When we did need performance, we turned to **Rust**.

Agoda explained **[why they bet on Rust to supercharge their Feature Store](https://medium.com/agoda-engineering/why-we-bet-on-rust-to-supercharge-feature-store-at-agoda-ed4a70d2efb7)**, achieving a 5x increase in traffic capacity.

The lesson was clear: The “Java Tax” is real. For critical, low-latency infrastructure, Rust’s safety and performance are worth the learning curve. We are entering a new era where the foundational tools of data engineering are being rebuilt, brick by brick, in Rust.

## FinOps as Architecture

Efficiency wasn’t just about code; it was about architecture. Wix documented **[how they slashed Spark costs by 60%](https://www.wix.engineering/post/how-wix-slashed-spark-costs-by-60-and-migrated-5-000-daily-workflows-from-emr-to-emr-on-eks)** not by rewriting code, but by migrating workloads from managed services (EMR) to Kubernetes (EKS).

We learned that “Serverless” often means “Wallet-less” if you aren’t careful. The smartest teams in 2025 were those who aggressively optimized their compute substrates, moving workloads to Spot instances, ARM processors, and single-node containers whenever possible.

---

## 5\. Lakehouse 2.0: The Catalog is the New Database

The “Format Wars” (Iceberg vs. Delta vs. Hudi) that dominated the early 2020s largely settled into a peace treaty in 2025. With the rise of interoperability layers, we stopped caring about data folder structure.

The battleground shifted “up the stack” to the **Catalog**. We realized that the “Lakehouse” is just a database turned inside out, and the Catalog is its operating system.

## The Catalog Wars

In 2025, the Catalog stopped being just a “list of tables” and became the active control plane for the enterprise.

New concepts like **[DuckLake](https://duckdb.org/2025/05/27/ducklake.html)** challenged the status quo, proposing that we use DuckDB itself as a catalog and metadata layer, replacing the heavy, complex Hive Metastore with a lightweight, transactional database.

Hyperscalers (AWS, Snowflake, Databricks) all converged on Managed Iceberg services. As Simon Späti noted in **[The Open Table Format Revolution](https://www.ssp.sh/blog/open-table-format-revolution/)**, the major players stopped fighting the open format and started trying to own the metadata layer that manages it. The value proposition shifted from “we store your data” to “we govern your transactions.”

---

## 6\. The “Context” Supply Chain: Unstructured Data & Knowledge Graphs

For decades, Data Engineering was about rows and columns. In 2025, we had to get good at text, images, and relationships. To support the GenAI revolution, we had to build the **Context Supply Chain**.

We aren’t just moving data anymore; we are moving *meaning*.

## Knowledge Graphs Return

The most surprising comeback of 2025 was the **Knowledge Graph**. As we struggled with LLM hallucinations, we realized that probabilistic models need deterministic facts to ground them.

Netflix details its **[Unified Data Architecture](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d)** and how it is **[Unlocking Entertainment Intelligence with Knowledge Graph](https://netflixtechblog.medium.com/unlocking-entertainment-intelligence-with-knowledge-graph-da4b22090141)** to provide a “source of truth” for its AI models.

We learned that “RAG” (Retrieval-Augmented Generation) isn’t just about vector search. It’s about “GraphRAG”—using the relationships between data points to provide richer, more accurate context to the model.

## The Embedding Pipeline

Data Engineers had to master a new type of transformation: the **Embedding**.

We moved beyond simple “Word2Vec” tutorials. Milvus released guides on **[how to choose the right embedding model for RAG](https://milvus.io/blog/how-to-choose-the-right-embedding-model-for-rag.md)**, helping teams select between LLM2Vec, BGE-M3, and others for specific domains. We built pipelines that chunked documents, generated embeddings, and stored them in vector databases, treating “semantic distance” as a first-class data type.

## Unstructured Data Management

We formally recognized **[Unstructured Data Management at Scale](https://piethein.medium.com/unstructured-data-management-at-scale-4c612f822f70)** as a core competency. Piethein Strengholt argued that it wasn’t enough to dump PDFs into an S3 bucket; we needed to parse, clean, chunk, and govern that data with the same rigor we apply to our financial tables.

The “Medallion Architecture” (Bronze/Silver/Gold) was adapted for unstructured data. We started talking about “Raw Documents” (Bronze), “Parsed & Chunked Text” (Silver), and “Curated Embeddings” (Gold).

---

## 7\. Governance 2.0: The Safety Brake for Autonomous Agents

As AI agents began taking actions—booking interviews, executing code, modifying databases—Governance stopped being a “compliance checkbox” and became a “safety brake.”

In 2024, if a dashboard was wrong, a manager made a bad decision. In 2025, if an agent is wrong, it might delete a production database or leak PII to a competitor.

## Privacy-Aware Infrastructure

Meta writes about **[discovering data flows via lineage at scale](https://engineering.fb.com/2025/01/22/security/how-meta-discovers-data-flows-via-lineage-at-scale/)**. They didn’t just write policies; they wrote code that tracked data lineage and enforced purpose limitations at the exabyte scale. Meta introduced **[Policy Zones](https://engineering.fb.com/2025/07/23/security/policy-zones-meta-purpose-limitation-batch-processing-systems/)** to ensure that data collected for one purpose (e.g., safety) couldn’t be used for another (e.g., ad targeting) without explicit permission.

This level of granularity is the future. We are moving toward systems where every piece of data carries its own “passport” of permissions, and every agent must present a “visa” to access it.

## Shadow AI and the New Perimeter

The rise of “Shadow AI”—engineers spinning up local LLMs or using unapproved APIs—forced data teams to harden the perimeter.

We saw the emergence of **Data Contracts** as a defense mechanism. Grab implemented **[real-time data quality monitoring](https://engineering.grab.com/real-time-data-quality-monitoring)** with strict contracts for its Kafka streams, ensuring that bad data was rejected before it could poison the downstream AI models.

Governance in 2025 is about **Observability**. It’s about knowing exactly which agent accessed which document, why, and what it did with it.

---

## Conclusion: The Era of the Context Engineer

Looking back at 2025, it is clear that the role of the Data Engineer has fundamentally changed.

We are no longer just building pipelines to move data from Point A to Point B. We are building the **enterprise’s Cognitive Nervous System**.

- We are **Agent Engineers**, designing the workflows that allow AI to reason and act.
- We are **Eval Architects**, building the metric systems that keep AI honest.
- We are **Context Curators**, ensuring that the “meaning” of our data is preserved and accessible.
- We are **Efficiency Experts**, maximizing the ROI of every compute cycle in a world of expensive GPUs.

> The tools will continue to change. Spark might yield to Polars; Kafka might yield to object storage. But the discipline of *engineering* —of rigor, measurement, and architecture—is stronger than ever.

---

*All rights reserved, Dewpeche Pvt Ltd, India. I have provided links for informational purposes and do not suggest endorsement. All views expressed in this newsletter are my own and do not represent current, former, or future employers’ opinions.*