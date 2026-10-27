---
title: "Claude Conversation"
source: "https://claude.ai/share/b8097669-3142-4976-9f0f-3e038dc7e3dd"
author:
published: 2026-10-26
created: 2026-10-27
description: "Claude conversation with 24 messages"
tags:
  - "brainspew"
---
**You**

I have a 30 minute interview with 66Degrees tomorrow. What do you suggest I study?

---

**Claude**

For a 30-minute call, this is probably a screen with a recruiter or hiring manager rather than a deep technical panel. I’d split your evening between two things: polishing four or five stories that match the job description, and learning enough Google Cloud vocabulary that you can talk about GCP as easily as you talk about AWS.

**Know the company (10 minutes)**

- **Google-only partner.** 66degrees works only on Google Cloud, delivering AI, data and cloud services. It was formed on May 25th, 2021 when Cloudbakers merged with Qwinix. [66degrees](https://66degrees.com/?p=4247) [cbinsights](https://www.cbinsights.com/company/cloudbakers)
- **Recent award.** In April it was named 2026 Google Cloud Partner of the Year for Artificial Intelligence. [aijourn](https://aijourn.com/66degrees-named-2026-google-cloud-partner-of-the-year-for-artificial-intelligence/)
- **Agentic direction.** In March they appointed Jonathan Cremers as chief delivery officer to lead an agentic teams model. They also market a platform called Paradigm, which they say speeds cloud modernization by 50-70% using AI agents. [simplify](https://simplify.jobs/c/66-Degrees) [simplify](https://simplify.jobs/c/66-Degrees)

That agentic push is your opening. Most Data Architect candidates won’t have your hands-on Claude, MCP and Temporal work. Position yourself as someone who has done many migrations the hard way and is now automating them with agents. Ask about Paradigm by name.

**Your strongest stories, mapped to the job description**

- **Migration to BigQuery:** At Darwin Analytics you moved on-prem SAP HANA data to BigQuery two ways (Estuary and WebMethods), then on to Fabric and PowerBI. This is your only real GCP story, so lead with it.
- **Teradata:** Qantas, where you integrated Teradata and Jeppesen sources into an AWS/Vertica redesign. They list Teradata-to-BigQuery as “proven experience,” so be ready to discuss Teradata-specific translation issues (below).
- **Oracle and MySQL migrations:** HelloWorld (Oracle backend to Vertica) and Lasidco (MySQL to Vertica).
- **POC and MVP rigor:** Cymer/ASML, with 800+ benchmark scenarios comparing Redshift and MSSQL. This is exactly how a careful architect runs a POC.
- **Infrastructure as code:** Teva’s Terraform estate. Also mention the GCP Terraform work from Zoomcamp.
- **Linking business and tech leaders:** Hyperion presales, the Solver VP role, and the Boeing RFP build-off.
- **Education workshops:** You trained and certified Essbase DBAs and designed Hyperion’s worldwide training curriculum.

**GCP topics to cram (most of your time)**

*BigQuery data modeling*

- Partitioning (by time or integer range) versus clustering
- Nested and repeated fields (STRUCT and ARRAY) versus a star schema. Know when to denormalize.
- Materialized views and BI Engine
- Slot-based pricing (editions) versus on-demand pricing

Your columnar background from Vertica maps over well. Vertica projections are roughly like BigQuery clustering and partitioning, and that comparison will sound fluent.

*Migration tooling*

- **BigQuery Migration Service:** the SQL translator (batch and interactive) and its assessment tool for Teradata
- **BigQuery Data Transfer Service**
- **Database Migration Service (DMS):** moves MySQL and Postgres to Cloud SQL. For Oracle, check how DMS handles Oracle-to-PostgreSQL (Cloud SQL or AlloyDB) tonight, since the job description specifically mentions Oracle to Cloud SQL.

*Teradata-to-BigQuery problems you’d have to solve*

- Primary indexes become partitioning and clustering choices
- SET tables (duplicate-row semantics) have no direct equivalent
- BTEQ scripts and stored procedures become BigQuery scripting and procedures
- Volatile tables become temp tables
- Data type and case-sensitivity differences

*Processing and orchestration*

- When to use plain BigQuery SQL, Dataflow (Apache Beam), or Dataproc (managed Spark)
- Cloud Composer (managed Airflow) versus Cloud Workflows
- Dataform versus dbt. You know dbt, so learn how Dataform differs.

*Security and governance*

- IAM roles on BigQuery datasets
- Column-level security with policy tags
- Row-level access policies
- VPC Service Controls
- Dataplex, at a headline level

*Healthcare (listed as a plus)*

- Know in one sentence what a Healthcare API FHIR store is, and that it can stream into BigQuery. Your Teva pharma work and healthcare background give you a hook.

**Prepare for two predictable concerns**

1. **“How much hands-on GCP do you have?”** The posting accepts “or similar cloud experience.” Answer with Darwin first, then your 12+ years of AWS depth. If you’re willing to pursue the Professional Data Engineer or Professional Cloud Architect certification, say so; they list it as a plus.
2. **“How many projects?”** Pick one number for your Full360 project count and stick to it. Your resume says 29, but your notebook tally ends at “28 projects completed.”

**Questions to ask them**

- What does the typical client mix look like right now: migrations, AI builds, or both?
- How does Paradigm change what a Data Architect actually does day to day?
- What do the first 90 days of this role look like?

If it would help, I can run you through a mock Q&A tonight on the Teradata migration and BigQuery modeling questions.

Sources:

- [66degrees company profile (Simplify)](https://simplify.jobs/c/66-Degrees)
- [66degrees named 2026 Google Cloud Partner of the Year for AI (AI Journal)](https://aijourn.com/66degrees-named-2026-google-cloud-partner-of-the-year-for-artificial-intelligence/)
- [66degrees site](https://66degrees.com/?p=4247)
- [Cloudbakers/66degrees (CB Insights)](https://www.cbinsights.com/company/cloudbakers)

---

**You**

is BigQuery columnar?

---

**Claude**

Yes. BigQuery stores data in columns, using Google’s internal format called **Capacitor**. Queries run on **Dremel**, a distributed tree-structured execution engine, and storage sits on Colossus, separate from compute.

Since you know Vertica, here is how the two compare.

**Similar to Vertica**

- Queries read only the columns they reference, and data is compressed and encoded per column.
- It is built for scans, aggregations and joins over large tables, not row-at-a-time OLTP.

**Different from Vertica (worth saying in the interview)**

- **Compute and storage are fully separated and serverless.** You don’t size nodes. Compute comes as “slots,” either on-demand or reserved through editions. This is closer to Vertica Eon mode than to Enterprise mode, but with no cluster to manage.
- **No projections or traditional indexes.** Your physical-design levers are partitioning, clustering, materialized views and search indexes. Clustering is the closest thing to Vertica’s projection sort order.
- **Cost follows column choice.** On-demand pricing charges by bytes scanned, so `SELECT *` costs real money. Column pruning is a billing concern as well as a performance one, which makes it a good point to raise as an architect.
- **Nested and repeated fields (STRUCT/ARRAY) are first-class.** Because the columnar format handles nesting, Google often recommends denormalizing instead of strict star schemas. Expect a “star schema vs. nested tables” question.
- **Weak at frequent small updates.** Singleton UPDATE and DELETE statements are inefficient and subject to DML limits. Batch writes or streaming inserts with periodic MERGE are the usual patterns, much like Vertica’s trickle-load cautions.

A one-line answer for the interview: “Yes, Capacitor columnar storage on Dremel. Coming from Vertica, my physical design shifts from projections to partitioning and clustering, and I think about bytes scanned as a cost driver as well as performance.”

---

**You**

Tell me more about nested tables. What is the columnar limit? Remind me about clustering. Assume I will use wide denormalized tables.

---

**Claude**

### Nested and repeated fields

Instead of a fact table joined to child tables, you store the children inside the parent row:

- **STRUCT (RECORD)**: a group of fields embedded in a row. Use it for one-to-one data, such as a `customer` struct with `name`, `tier` and `region`.
- **ARRAY**: a repeated field. Use it for one-to-many data, such as an order’s line items.
- **ARRAY\<STRUCT>**: the main pattern. One order row holds an array of line-item structs.

```sql
CREATE TABLE sales.orders (
  order_id     STRING,
  order_ts     TIMESTAMP,
  customer     STRUCT<id STRING, name STRING, tier STRING, region STRING>,
  line_items   ARRAY<STRUCT<sku STRING, qty INT64, unit_price NUMERIC>>
)
PARTITION BY DATE(order_ts)
CLUSTER BY customer_id_flat, region_flat;  -- see clustering caveat below
```

You query the nested data with dot notation, and flatten arrays with `UNNEST`:

```sql
SELECT o.order_id, o.customer.region, li.sku, li.qty * li.unit_price AS amt
FROM sales.orders o, UNNEST(o.line_items) li
WHERE DATE(o.order_ts) = '2026-10-01';
```

**Why Google pushes this design:**

- Parent and child data are stored together, so the order-to-line-item join disappears.
- Each nested leaf field is still its own column. Selecting `line_items.sku` reads only that one column, so you keep columnar pruning even inside the nesting.

**The cost:**

- Updating one child element means rewriting the parent row.
- Dimensions that change slowly get copied into every row and go stale. In Kimball terms, you are freezing an SCD Type 1 or Type 2 snapshot into each fact row.

### Limits

- **10,000 columns** per table, query result or view, and this includes nested and repeated columns. Every leaf inside a STRUCT counts toward the 10,000.
- **Recently deleted columns** can keep counting toward that total for a while and cause false quota errors until it resets. This matters if your wide tables change schema often.
- **100 MB** maximum row size, approximate, and enforced during certain stages of query execution. A wide table with large nested arrays can hit this.
- **Nesting depth** is capped at 15 levels of STRUCT, as far as I know. Check the docs before quoting it.
- **Partitions** are capped at around 10,000 per table, also worth confirming. Separately, the daily quota on partition modifications cannot be increased, and Google’s fix is coarser partitioning, such as monthly instead of daily.

### Clustering

**How it works**

- BigQuery sorts data by the clustering columns and organizes it into blocks.
- Filters on those columns skip blocks entirely, so fewer bytes are scanned and the query costs less.

**Rules**

- **Up to four clustering columns.** If you need more selectivity, combine clustering with partitioning.
- **Order matters.** Data is sorted by the first column, then the second, and so on, just like a Vertica projection’s ORDER BY. Put your most common filter first.
- **Top-level, non-repeated columns only.** Allowed types include STRING, INT64, NUMERIC, BIGNUMERIC, DATE and DATETIME. You can’t cluster on `customer.region` inside a STRUCT, so you would promote the field to a top-level column. That’s what the `_flat` columns in my example stand for.
- **STRING columns** cluster on only the first 1,024 characters.
- **Maintenance is free.** Automatic reclustering, batch loads and table copies cost nothing. However, changing the clustering specification applies only to new data unless you rewrite the existing data.

**When to use it**

- Tables or partitions larger than about **64 MB** are the ones likely to benefit.
- Partition first only if partitions average around **10 GB or more**. Many small partitions bloat metadata and slow it down.

### Wide, denormalized design in one sentence

Partition on the date you prune by, cluster on up to four top-level filter keys in order of selectivity, nest one-to-many children as ARRAY\<STRUCT>, promote any nested field you filter on to the top level, and remember that every leaf counts toward 10,000 columns and on-demand billing is by bytes scanned, so tell users not to run `SELECT *`.

Sources:

- [BigQuery quotas and limits](https://cloud.google.com/bigquery/quotas)
- [BigQuery quotas (columns limit)](https://cloud.google.com/bigquery-transfer/quotas)
- [Introduction to clustered tables](https://developers.google.com/bigquery/docs/clustered-tables)
- [Troubleshoot quota and limit errors](https://cloud.google.com/bigquery/docs/troubleshoot-quotas)

---

**You**

If I have a customer struct and part of it is PII what's a good strategy?

---

**Claude**

A good default is to keep the struct as it is, put a **policy tag** on each PII leaf field, and add **dynamic data masking** on top. If the requirements are stricter, move the PII out of the wide table entirely.

### Option 1: Policy tags on nested leaf fields (the default)

Column-level security works on individual leaf fields inside a STRUCT, so `customer.email` can be locked down while `customer.tier` and `customer.region` stay open.

1. **Build a taxonomy** in Data Catalog / Dataplex, for example `PII > High (SSN, DOB)` and `PII > Medium (email, phone, name)`.
2. **Tag the leaf fields** in the schema with those policy tags.
3. **Grant Fine-Grained Reader** on each tag only to the groups that need the raw values.
4. **Add data masking policies** to the tags so everyone else gets a masked value instead of an error. Masking rules include SHA-256 hash, nullify, default value, last-four-characters, email mask, and year-only for dates.

Masking matters for usability. Without it, a user who lacks access gets an access-denied error on queries that touch the column, including `SELECT *`. They then have to write `SELECT * EXCEPT(...)`, which is awkward for nested fields. With masking, their queries run and just return masked values.

A **SHA-256 hash mask** is also useful for analytics: analysts can still count distinct customers and join on hashed email without ever seeing the raw value.

### Option 2: Split the PII out (when requirements are stricter)

When regulations, GDPR-style deletion or audit needs demand it, take PII out of the wide table:

- **Wide fact table:** holds `customer.customer_key` (a surrogate or token) plus non-PII attributes.
- **PII vault table:** keyed by `customer_key`, in a separate dataset or project with tight IAM and possibly CMEK encryption.
- **Authorized views:** join the two only for approved consumers.

This trades away some of the join-free benefit of denormalizing. In return:

- The PII has a single home.
- Deleting a customer is a one-row operation rather than a rewrite across every partition of the wide table.
- Access auditing is simple.

### Option 3: Encrypt inside the table

BigQuery’s AEAD functions, together with Cloud KMS-wrapped keys, let you encrypt values inside the row:

- **Deterministic encryption** keeps encrypted values joinable on equality.
- **Crypto-shredding** handles deletion: destroy a customer’s key and their data becomes unreadable, with no row rewrites. This is useful with wide denormalized tables, where rewriting rows across years of partitions is expensive.

### Supporting pieces

- **Sensitive Data Protection (formerly Cloud DLP)** finds PII you didn’t know about, often in free-text fields, and can de-identify data in the pipeline before it lands.
- **Row-level access policies** handle region-based restrictions, such as EU analysts seeing only EU rows. These are separate from column-level controls.
- **VPC Service Controls** around the project limit where data can be exfiltrated to.

### Interview line

“Keep the customer struct for analytics, tag the PII leaf fields with a policy-tag taxonomy, and apply dynamic masking with SHA-256 hashing so analysts can still join and count. For regulated data or right-to-delete, tokenize into a separate PII vault with authorized views, or use KMS-wrapped AEAD encryption so I can crypto-shred instead of rewriting partitions.”

---

**You**

I want to do RBAC, role based, not row based. How many roles push a limit for set joins and transforms? Also is there a masking type that preserves sort order?

---

**Claude**

### RBAC in BigQuery

In practice, RBAC here means mapping groups to sensitivity tiers:

- **Roles become Google Groups**, for example `analysts@`, `finance-pii@`, `support-pii@`.
- **Sensitivity becomes policy tags**, for example `PII-High` and `PII-Medium`.
- **Each tag gets data policies** that bind a group to an outcome: raw access, which needs Fine-Grained Reader, or a specific masking rule.

So you grant roles against tags, not against tables or columns. That design decision is what keeps it manageable.

### Does the number of roles hit a limit?

There is no hard ceiling on roles you’re likely to reach. The limits that matter come from structure and from how masking interacts with joins.

**Hard limits that shape the design**

- **One policy tag per column.** You cannot stack a role-specific tag for each role on the same column. All differences between roles have to be expressed as different data policies on a single tag.
- **Dataplex Attribute Store limits:**
	- 100 taxonomies per region
		- 10,000 attributes in total
		- 50 attributes per table
		- 4 levels of depth per attribute tree
- **IAM allow policies** cap the number of principals per policy, about 1,500 as far as I know. Always grant to groups, never to individual users, and you won’t come near it.

**What really sets the limit: joins on masked columns**

- Masking is applied when each user reads the data, so their joins and transforms operate on the masked values.
- **SHA256 is deterministic.** The same input always gives the same hash, so joins and GROUP BY still match across tables, provided both sides use the same masking rule.
- **RANDOM\_HASH breaks joins.** It adds a random value per query, so the masked output differs every time. Use it when you specifically want to prevent linking across queries.
- **Partial masks break joins on key columns.** LAST\_FOUR, FIRST\_FOUR and EMAIL\_MASK produce collisions, so many rows become `XXXXX@gmail.com`.
- **A user in several groups** gets only one masking rule per tag. BigQuery picks it by a fixed priority order, so check that order in the docs before relying on overlapping roles.

**Practical guidance:** keep it to about 3–5 sensitivity tiers and a handful of access outcomes. Beyond that, the problem is not quotas but that nobody can predict which join results a given person will see.

**For joins and transforms:** build them as authorized views or dbt/Dataform models that run under a service account with raw access. Join on surrogate keys, not on PII, and expose only the results. Then masking affects how values are displayed, not what joins correctly.

### Is there a masking type that preserves sort order?

Not exactly. The predefined rules are:

- SHA256
- ALWAYS\_NULL
- DEFAULT\_MASKING\_VALUE
- LAST\_FOUR\_CHARACTERS
- FIRST\_FOUR\_CHARACTERS
- EMAIL\_MASK
- DATE\_YEAR\_MASK
- RANDOM\_HASH

None of them preserves full sort order. Two preserve it coarsely:

- **DATE\_YEAR\_MASK** truncates dates to January 1 of their year, so year-level sorting still works.
- **FIRST\_FOUR\_CHARACTERS** keeps the prefix, so alphabetical order is preserved at four-character granularity.

**For anything finer, write a custom masking routine.** Data policies accept a custom routine (a UDF) instead of a predefined rule. You can make it coarsen values in an order-preserving way, for example truncating to the month, rounding amounts to bands, or bucketing ages.

**True order-preserving encryption isn’t offered,** and it’s cryptographically weak anyway: sorted ciphertext reveals the distribution of the values. The usual architect’s answer is not to sort on PII at all. Sort on a non-PII column such as the event timestamp or a surrogate key, or keep a coarsened copy as a separate column, for example `dob_year` alongside a masked `dob`.

### Interview line

“RBAC through groups bound to policy-tag data policies, a few sensitivity tiers, deterministic SHA-256 wherever joins must survive masking, and sensitive joins pushed into authorized views on surrogate keys. For sort order, I’d use a custom masking routine that coarsens values, or sort on non-PII columns, because order-preserving encryption leaks the distribution.”

Sources:

- [Dataplex Attribute Store quotas](https://cloud.google.com/dataplex/docs/attribute-store)
- [Column-level access control](https://cloud.google.com/bigquery/docs/column-level-security)
- [DataPolicy REST reference (v2)](https://cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies)
- [PredefinedExpression reference](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-bigquery-data_policies-v1/latest/Google-Cloud-Bigquery-DataPolicies-V1-DataMaskingPolicy-PredefinedExpression)

---

**You**

What's this about SET tables? Is that Teradata or BQ?

---

**Claude**

It’s **Teradata**. BigQuery has no equivalent, and that gap is why it matters in a migration.

### In Teradata

Every table is either SET or MULTISET:

- **SET tables do not allow fully duplicate rows**, meaning rows identical in every column.
	- A single-row `INSERT` of a duplicate raises an error.
		- An `INSERT ... SELECT` drops the duplicates without any error.
- **MULTISET tables allow duplicates**, like most databases.
- **The default depends on session mode.** In Teradata mode a plain `CREATE TABLE` produces a SET table; in ANSI mode it produces MULTISET. Many older Teradata warehouses are therefore full of SET tables that nobody chose on purpose.
- **Checking for duplicates costs performance**, so Teradata DBAs often add a unique primary index or a unique secondary index to make the check cheap.

### In BigQuery

- **Every table behaves like MULTISET.** Duplicates are always allowed.
- **Primary and foreign keys exist but are not enforced.** They are hints for the optimizer, for example to eliminate joins, not constraints.

### Why it breaks migrations

Old Teradata ETL often relies, without saying so, on SET tables silently removing duplicates. You might have reruns that are safe only because duplicates disappear, or overlapping extract windows. Move the same logic to BigQuery and those duplicates land in the table. Row counts grow, and aggregates are quietly overstated.

**How to handle it**

1. **Inventory first.** Query `DBC.TablesV` for SET tables. The BigQuery Migration Service assessment also reports on this.
2. **Replace the implicit deduplication with explicit logic:**
	- Use `MERGE` on the business key for incremental loads. This is the cleanest fix.
		- Or deduplicate in the transform with `QUALIFY ROW_NUMBER() OVER (PARTITION BY <key> ORDER BY <load_ts> DESC) = 1`. BigQuery supports `QUALIFY`, so this ports easily from Teradata.
		- Or use `SELECT DISTINCT` for small, true full-row duplicate cases.
3. **Add data-quality checks** to the pipeline, such as duplicate-key assertions in Dataform or dbt tests, because the database won’t enforce uniqueness for you.

**Interview line:** “Teradata SET tables silently remove duplicates and BigQuery enforces nothing, so I inventory SET tables up front and replace that implicit behavior with MERGE on business keys or QUALIFY ROW\_NUMBER() deduplication, plus uniqueness tests in Dataform or dbt.”

---

**You**

How much of Apache Beam is implemented in Dataflow?

---

**Claude**

Essentially all of it. **Dataflow is Google’s managed runner for Apache Beam**, and it was the reference implementation: Beam started as the open-sourced Dataflow SDK in 2016. In Beam’s capability matrix, Dataflow is the runner with the most complete coverage.

### What Dataflow supports from the Beam model

- **Core transforms:** ParDo, GroupByKey, CoGroupByKey, Combine, Flatten and Partition, plus side inputs and multiple outputs.
- **Windowing:** fixed, sliding, session and global windows.
- **Event-time processing:** watermarks, triggers (early, on-time and late firings) and allowed lateness. This is what separates Beam from simple batch tools.
- **Stateful processing:** per-key state and timers.
- **Splittable DoFn:** the framework for custom, scalable sources and sinks.
- **One programming model for batch and streaming:** the same pipeline code runs either way.
- **Exactly-once processing** in streaming, with an optional at-least-once mode that is cheaper and has lower latency.
- **SDKs:** Java and Python are fully supported. Go works, but its ecosystem is thinner.
- **Cross-language pipelines:** with Runner v2 (the portable runner), a Python pipeline can call Java transforms, such as the Kafka or JDBC connectors.
- **Higher-level layers:** Beam SQL, Beam YAML, the Beam DataFrames API in Python, and `RunInference` for ML models, including GPU workers.

### Where gaps show up

The gaps are rarely in the Beam model itself. They tend to be:

- **Connector maturity by SDK.** Java has the deepest set of I/O connectors. Python sometimes depends on cross-language wrappers around the Java ones.
- **Occasional newer or experimental Beam features** that reach the direct runner before Dataflow, or the reverse. Check Beam’s capability matrix for anything unusual.
- **Updating running pipelines.** Updating a streaming job in place requires compatible changes. Changing pipeline structure often means draining the job and relaunching it.

### What Dataflow adds beyond Beam

The value of the managed service is mostly operational:

- Horizontal **autoscaling** and **dynamic work rebalancing**, which reduces the impact of straggler workers.
- **Streaming Engine** and **Dataflow Shuffle**, which move state and shuffle off the worker VMs to make jobs cheaper and more stable.
- **Flex Templates** for parameterized, reusable jobs, plus Google-provided templates for common pipelines such as Pub/Sub to BigQuery and JDBC to BigQuery.
- Job monitoring through **Cloud Monitoring**.

### How it compares to Dataproc and BigQuery SQL

Choosing among these is a common interview question:

- **BigQuery SQL / Dataform:** for batch ELT where the data is already in BigQuery. It is the simplest and cheapest choice, and the right default for a wide denormalized warehouse.
- **Dataflow:** for streaming with event-time correctness (late data, windows, exactly-once), or heavy transforms before data lands, such as Pub/Sub or Kafka into BigQuery or de-identifying PII on the way in.
- **Dataproc:** when the client already has Spark or Hadoop code to lift and shift, or wants the Spark ecosystem. This is where your VerticaPy-versus-PySpark reasoning applies.

**Interview line:** “Dataflow is the reference runner for Beam and covers the full model, including windowing, triggers, state and timers, and exactly-once streaming, plus managed autoscaling, Streaming Engine and Flex Templates. I’d use it for streaming and pre-landing transforms, BigQuery SQL with Dataform for in-warehouse ELT, and Dataproc when a client has existing Spark.”

---

**You**

Which analytical functions will be missing from GBQ? How often does it need Spark or other external calculation engines? What's the best integration?

---

**Claude**

### Analytic gaps in BigQuery

There are fewer than you might expect, and several recent additions closed the big ones.

**Already covered, despite what older material says**

- Window functions, `QUALIFY`, ROLLUP, CUBE and GROUPING SETS, PIVOT and UNPIVOT, recursive CTEs, and `LAST_VALUE ... IGNORE NULLS`.
- **`MATCH_RECOGNIZE`** for pattern matching over row sequences, released in late 2025. Google presents it as familiar to anyone who has used Teradata’s nPath, which removes a classic Teradata migration blocker.
- **Managed Python UDFs**, generally available since June 2026. They run on BigQuery-managed serverless resources and can import NumPy, SciPy, pandas and scikit-learn directly from a SELECT. This covers much of the “we need a custom calculation” problem.

**Still missing or awkward**, with workarounds:

- **No true aggregate median or percentile.** `PERCENTILE_CONT` works only as a window function. For aggregates you use `APPROX_QUANTILES` or the window form with DISTINCT. There’s also no native MODE.
- **Time-series features like Vertica’s.** There is no `TIMESERIES` clause, no interpolated event-series joins, and no ASOF JOIN as far as I know. Gap filling and bucketing exist in some form, but as-of joins become window tricks or range joins.
- **RANGE window frames take numbers, not intervals.** You convert timestamps with `UNIX_SECONDS()`.
- **Teradata-specific features** such as NORMALIZE, EXPAND ON, the legacy CSUM and MSUM functions, and some PERIOD semantics need rewrites. The migration translator handles many of them.
- **Oracle MODEL clause and CONNECT BY.** CONNECT BY becomes a recursive CTE. MODEL becomes procedural scripting.
- **No multidimensional cube engine.** Essbase-style outlines, member formulas and allocations become SQL or a semantic layer. This is your strongest area of expertise, so it’s worth raising.
- **Iterative and algorithmic work:** graph algorithms like PageRank, optimization solvers, heavy Monte Carlo, and matrix work. BigQuery scripting loops can do it, but slowly and expensively.

### How often you actually need Spark or another external engine

For a typical warehouse migration with wide denormalized tables, **rarely**. Most analytics, ELT and classical machine learning (BigQuery ML) stay inside BigQuery. The Python UDFs have reduced this further.

**When an external engine is justified**

1. **Existing Spark code or a team that knows Spark.** Rewriting working code is often wasteful.
2. **Iterative or algorithmic workloads:** graphs, simulations, large custom ML training.
3. **Heavy processing before data lands:** large raw files, deeply nested JSON, unstructured data, especially in streaming.
4. **Lakehouse requirements:** multiple engines sharing Iceberg tables.

### Best integrations, in order of preference

1. **Native SQL + BigQuery ML + Python UDFs.** No data movement, one billing model, and one governance model, so your policy tags and masking still apply.
2. **BigQuery DataFrames (bigframes).** A pandas-style API that generates SQL and pushes it down to BigQuery. **This is the BigQuery equivalent of VerticaPy and its vDataFrame**, so you can explain it in your own terms.
3. **Remote functions** (on Cloud Run) when the calculation needs an external service or API.
4. **Serverless Spark** (formerly Dataproc Serverless) or **Spark stored procedures** called from BigQuery. Spark reads through the BigQuery Storage Read API, which is fast columnar access with column-level security enforced. For a multi-engine lakehouse, use **BigLake Iceberg tables** as shared storage instead of copying data between engines.
5. **Dataflow** for streaming and event-time work, as discussed earlier.

**Interview line:** “Most of the classic gaps are closed: MATCH\_RECOGNIZE replaces nPath, and Python UDFs cover custom math. My default is to push compute into BigQuery with bigframes, which is essentially VerticaPy for BigQuery. I bring in serverless Spark over the Storage API or BigLake Iceberg only for existing Spark code, iterative algorithms, or lakehouse sharing, so governance stays in one place.”

Sources:

- [Managed Python UDFs GA (Google Cloud blog)](https://cloud.google.com/blog/products/data-analytics/python-udf-in-bigquery-now-generally-available?hl=en)
- [Introducing MATCH\_RECOGNIZE in BigQuery (Google Cloud blog)](https://cloud.google.com/blog/ja/products/data-analytics/introducing-match_recognize-in-bigquery?hl=ja)

---

**You**

I'm thinking that dumping subsets of data into separate narrower 'analytical tables' computed by DuckDB will outperform Pandas, Python and Polars. How clumsy might that be?

---

**Claude**

Your instinct is mostly right about the engine. The awkward parts are moving the data out and losing governance, not DuckDB itself.

### Performance

- **DuckDB versus pandas:** DuckDB usually wins by a wide margin on joins, aggregations and window functions. It’s vectorized, multithreaded and spills to disk, while pandas is single-threaded and limited to memory.
- **DuckDB versus Polars:** roughly even. Results depend on the workload, and either can win a given benchmark. Choose based on whether your team prefers working in SQL or in a dataframe API.
- **Plain Python loops:** no comparison; DuckDB is far faster.

So DuckDB is a reasonable engine for working on extracted subsets.

### Where it gets awkward

1. **Narrow tables gain less in BigQuery than you’d expect.** BigQuery is already columnar, so a query that selects 12 columns from a 3,000-column table reads only those 12. A narrow copy pays off only when it also **pre-aggregates, pre-filters or pre-joins** the data. You can build that inside BigQuery with `CREATE TABLE AS SELECT`, materialized views or Dataform models, with no export at all.
2. **Exporting bypasses your governance.** Once data lands in Parquet files or a DuckDB database, policy tags, masking, row-level policies and audit logs no longer apply. After everything we discussed about PII, this is the issue an interviewer would raise. If you do export, export from masked or authorized views, and treat the extracts as governed assets with their own storage access controls and retention.
3. **Keeping extracts current becomes your job.** Someone has to own refreshes, schedules, incremental logic and checks that each extract still matches its source. Copies tend to multiply without anyone tracking them.
4. **Getting the data out.** You have two options:
	- `EXPORT DATA` to Parquet in Cloud Storage, which DuckDB reads directly.
		- The community DuckDB BigQuery extension, which reads through the Storage Read API. It’s convenient, but Storage API reads are billed and the extension isn’t Google-supported.
5. **Single-node limits.** DuckDB is excellent up to a few hundred GB on a large VM. Beyond that, you’re back to BigQuery or Spark.

### Where it’s worth doing

- **Repeated, interactive iteration on a stable subset**, such as notebooks, feature exploration or model development. With BigQuery on-demand pricing, every query is billed and has a second or two of startup latency, while local DuckDB costs nothing per query and returns in milliseconds.
- **Cost control** for teams that run the same exploratory queries many times.
- **Embedded or edge analytics**, or shipping a self-contained data product to a client.
- **Dev and test environments** that mirror production logic cheaply.

### A sound pattern

1. BigQuery does the heavy lifting and the governance.
2. Dataform or dbt builds narrow, **pre-aggregated, already-masked** marts inside BigQuery.
3. Marts that need fast local iteration are exported to Parquet or Iceberg in Cloud Storage. Exporting to BigLake Iceberg tables lets BigQuery and DuckDB share the same files instead of keeping copies.
4. DuckDB, or MotherDuck for shared use, handles the interactive work.

**For the interview:** 66degrees sells Google Cloud. Present DuckDB as an addition for developer productivity and cost control, not as a way around BigQuery. For example: “I keep compute and governance in BigQuery and push everything I can down with bigframes. For tight iteration loops on governed, pre-aggregated marts, I’ll use DuckDB over Iceberg in Cloud Storage. It’s cheaper per iteration, and the data stays on the same files instead of being copied.”

---

**You**

Remind me of what Dataform is again.

---

**Claude**

Dataform is **Google’s SQL transformation framework built into BigQuery**, essentially Google’s version of dbt. Google acquired it in 2020 and now runs it as a managed service inside the BigQuery console.

### What it does

- **SQLX files:** each file is a SQL `SELECT` plus a config block that declares what it produces, such as a table, a view, an incremental table or an assertion.
- **`${ref("table_name")}`** declares dependencies between models. Dataform uses these to build the dependency graph and run models in the right order, the same way dbt’s `{{ ref() }}` does.
- **Incremental tables** process only new or changed rows, typically by generating a MERGE.
- **Assertions** are data-quality checks, such as uniqueness, non-null and custom conditions. In Teradata migrations, this is where you replace the deduplication that SET tables used to do.
- **Git integration:** repositories, workspaces for development, and pull-request workflows.
- **Scheduling:** release configurations compile a branch, and workflow configurations run it on a schedule. For more complex orchestration, you trigger it from Cloud Composer (Airflow) or Workflows.
- **JavaScript** is used for templating and generating SQL dynamically, where dbt uses Jinja.

### Cost

Dataform itself is free. You pay only for the BigQuery compute its SQL uses.

### Dataform versus dbt

|  | Dataform | dbt |
| --- | --- | --- |
| Warehouses | BigQuery only | Many |
| Templating | JavaScript | Jinja |
| Hosting | Managed in the BigQuery console, no extra cost | dbt Core (self-run) or dbt Cloud (paid) |
| Ecosystem | Smaller | Large: packages, community, semantic layer |
| Governance fit | Native IAM, part of the GCP setup | Requires separate setup |

**When to use each:** choose Dataform for a client that is committed to BigQuery and wants the simplest native option. Choose dbt for a client that uses several warehouses, already has dbt models, or wants its broader ecosystem.

**Interview line:** “Dataform is BigQuery’s native version of dbt. It uses SQLX models with ref-based dependency graphs, incremental tables, assertions and Git workflows, and it costs only the BigQuery compute it runs. I’ve used dbt, and the concepts carry over almost directly; mainly you swap Jinja for JavaScript templating.”

---

**You**

How would I create a region redundant system for GBQ in a 'pilot light' fashion?

---

**Claude**

Pilot light fits BigQuery well. In a pilot light design, data is kept continuously in sync in the second region, while compute and the surrounding pipelines stay minimal or turned off until you fail over. BigQuery offers two ways to do this, at different price points.

### Option A: Cross-region replication (the cheaper pilot light)

**How it works**

- Turn on **cross-region dataset replication** for each dataset you need to protect. The secondary region holds a read-only replica.
- On failover, **you promote the dataset**, one dataset at a time. It’s a soft failover and works with any capacity model.

**Keeping the secondary small**

- In the secondary region, define a reservation with **zero baseline slots and autoscaling**, or just plan to use on-demand pricing there.
- The result: you pay only for replicated storage and replication traffic until something goes wrong.

**Tradeoffs**

- Recovery is slower and manual, because you promote datasets one by one.
- RPO depends on standard replication lag.

### Option B: Managed disaster recovery (the better pilot light, on Enterprise Plus)

**How it works**

- Create a **failover reservation**: an Enterprise Plus reservation in the primary region with a `secondary_location` set.
- **Attach datasets to it.** You can attach up to 1,000.
- Standby compute in the paired region is included in the reservation. However, those slots aren’t usable until you fail over, and stale reads in the secondary need capacity you buy separately.
- Google’s documentation shows exactly the pilot-light shape: `slot_capacity = 0` with an `autoscale_max_slots` ceiling.

**Recovery characteristics**

- **Turbo replication** shrinks the window for data loss, and RPO is defined per dataset.
- **Five-minute RTO** once you start a failover.
- **Two failover types:**
	- *Soft failover* waits until everything committed in the primary has replicated. Use it for planned events and drills.
		- *Hard failover* promotes the secondary immediately. Use it when the primary region is actually down.

**Constraints to mention in the interview**

- Once a dataset is attached, **only Enterprise Plus reservations can write to it**. Reads can use any capacity model.
- Load and extract jobs can’t use the free shared slot pool. You need a PIPELINE reservation assignment.
- Replicated storage is billed at the same list price as primary storage, plus turbo replication charges.

### The rest of the platform

BigQuery replication covers only the datasets. A real pilot light also has to restart everything that runs around them:

- **Infrastructure as code for region two.** Write Terraform for the secondary reservation, IAM, service accounts, Composer, Dataflow and networking. Run `plan` regularly and `apply` only during failover. Keep Composer off in the secondary, because an idle Composer environment costs money.
- **Landing zone:** use dual-region or multi-region **Cloud Storage** buckets so raw files and Parquet exports survive the outage too.
- **Pipelines:** store Dataflow Flex Templates and container images in a multi-region Artifact Registry. Point Dataform release and workflow configurations at the secondary location.
- **Governance:** policy tag taxonomies and data policies belong to a location. Confirm that the secondary has matching taxonomies, so PII masking still works after failover. Otherwise the DR region becomes a governance hole.
- **Clients:** BigQuery jobs specify a location. Make apps and BI tools switch region through a config flag or connection setting, not hard-coded values.
- **Runbook and drills:** run a scheduled soft failover each quarter, and measure the real RTO and RPO against the client’s targets.

### DR is not backup

Replication copies mistakes and corruption to the secondary too, such as a bad `DELETE` or a broken pipeline run. Pair it with:

- **Time travel**, up to 7 days.
- **Table snapshots** or clones for longer retention, ideally in a separate project.

### Interview line

“For pilot light, I replicate datasets cross-region and keep compute at zero baseline in the secondary. On Enterprise Plus I’d use managed DR with a failover reservation: zero baseline slots, an autoscale ceiling, turbo replication, and roughly a five-minute RTO. Around it I keep Terraform ready to stand up Composer and Dataflow, dual-region Cloud Storage, and matching policy-tag taxonomies so masking survives failover. I run quarterly soft-failover drills, and use snapshots and time travel for logical corruption, since replication copies mistakes too.”

Sources:

- [Managed disaster recovery (BigQuery docs)](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery?authuser=1)
- [Migrate to managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/disaster-recovery-migration)
- [BigQuery gets managed disaster recovery (Google Cloud blog)](https://cloud.google.com/blog/products/data-analytics/bigquery-gets-managed-disaster-recovery)

---

**You**

Create a Claude Doc from your last answer.

---
---
title: "Claude Conversation"
source: "https://claude.ai/share/b8097669-3142-4976-9f0f-3e038dc7e3dd"
author:
published: 2026-10-26
created: 2026-10-27
description: "Claude conversation with 24 messages"
tags:
  - "brainspew"
---
**You**

I have a 30 minute interview with 66Degrees tomorrow. What do you suggest I study?

---

**Claude**

For a 30-minute call, this is probably a screen with a recruiter or hiring manager rather than a deep technical panel. I’d split your evening between two things: polishing four or five stories that match the job description, and learning enough Google Cloud vocabulary that you can talk about GCP as easily as you talk about AWS.

**Know the company (10 minutes)**

- **Google-only partner.** 66degrees works only on Google Cloud, delivering AI, data and cloud services. It was formed on May 25th, 2021 when Cloudbakers merged with Qwinix. [66degrees](https://66degrees.com/?p=4247) [cbinsights](https://www.cbinsights.com/company/cloudbakers)
- **Recent award.** In April it was named 2026 Google Cloud Partner of the Year for Artificial Intelligence. [aijourn](https://aijourn.com/66degrees-named-2026-google-cloud-partner-of-the-year-for-artificial-intelligence/)
- **Agentic direction.** In March they appointed Jonathan Cremers as chief delivery officer to lead an agentic teams model. They also market a platform called Paradigm, which they say speeds cloud modernization by 50-70% using AI agents. [simplify](https://simplify.jobs/c/66-Degrees) [simplify](https://simplify.jobs/c/66-Degrees)

That agentic push is your opening. Most Data Architect candidates won’t have your hands-on Claude, MCP and Temporal work. Position yourself as someone who has done many migrations the hard way and is now automating them with agents. Ask about Paradigm by name.

**Your strongest stories, mapped to the job description**

- **Migration to BigQuery:** At Darwin Analytics you moved on-prem SAP HANA data to BigQuery two ways (Estuary and WebMethods), then on to Fabric and PowerBI. This is your only real GCP story, so lead with it.
- **Teradata:** Qantas, where you integrated Teradata and Jeppesen sources into an AWS/Vertica redesign. They list Teradata-to-BigQuery as “proven experience,” so be ready to discuss Teradata-specific translation issues (below).
- **Oracle and MySQL migrations:** HelloWorld (Oracle backend to Vertica) and Lasidco (MySQL to Vertica).
- **POC and MVP rigor:** Cymer/ASML, with 800+ benchmark scenarios comparing Redshift and MSSQL. This is exactly how a careful architect runs a POC.
- **Infrastructure as code:** Teva’s Terraform estate. Also mention the GCP Terraform work from Zoomcamp.
- **Linking business and tech leaders:** Hyperion presales, the Solver VP role, and the Boeing RFP build-off.
- **Education workshops:** You trained and certified Essbase DBAs and designed Hyperion’s worldwide training curriculum.

**GCP topics to cram (most of your time)**

*BigQuery data modeling*

- Partitioning (by time or integer range) versus clustering
- Nested and repeated fields (STRUCT and ARRAY) versus a star schema. Know when to denormalize.
- Materialized views and BI Engine
- Slot-based pricing (editions) versus on-demand pricing

Your columnar background from Vertica maps over well. Vertica projections are roughly like BigQuery clustering and partitioning, and that comparison will sound fluent.

*Migration tooling*

- **BigQuery Migration Service:** the SQL translator (batch and interactive) and its assessment tool for Teradata
- **BigQuery Data Transfer Service**
- **Database Migration Service (DMS):** moves MySQL and Postgres to Cloud SQL. For Oracle, check how DMS handles Oracle-to-PostgreSQL (Cloud SQL or AlloyDB) tonight, since the job description specifically mentions Oracle to Cloud SQL.

*Teradata-to-BigQuery problems you’d have to solve*

- Primary indexes become partitioning and clustering choices
- SET tables (duplicate-row semantics) have no direct equivalent
- BTEQ scripts and stored procedures become BigQuery scripting and procedures
- Volatile tables become temp tables
- Data type and case-sensitivity differences

*Processing and orchestration*

- When to use plain BigQuery SQL, Dataflow (Apache Beam), or Dataproc (managed Spark)
- Cloud Composer (managed Airflow) versus Cloud Workflows
- Dataform versus dbt. You know dbt, so learn how Dataform differs.

*Security and governance*

- IAM roles on BigQuery datasets
- Column-level security with policy tags
- Row-level access policies
- VPC Service Controls
- Dataplex, at a headline level

*Healthcare (listed as a plus)*

- Know in one sentence what a Healthcare API FHIR store is, and that it can stream into BigQuery. Your Teva pharma work and healthcare background give you a hook.

**Prepare for two predictable concerns**

1. **“How much hands-on GCP do you have?”** The posting accepts “or similar cloud experience.” Answer with Darwin first, then your 12+ years of AWS depth. If you’re willing to pursue the Professional Data Engineer or Professional Cloud Architect certification, say so; they list it as a plus.
2. **“How many projects?”** Pick one number for your Full360 project count and stick to it. Your resume says 29, but your notebook tally ends at “28 projects completed.”

**Questions to ask them**

- What does the typical client mix look like right now: migrations, AI builds, or both?
- How does Paradigm change what a Data Architect actually does day to day?
- What do the first 90 days of this role look like?

If it would help, I can run you through a mock Q&A tonight on the Teradata migration and BigQuery modeling questions.

Sources:

- [66degrees company profile (Simplify)](https://simplify.jobs/c/66-Degrees)
- [66degrees named 2026 Google Cloud Partner of the Year for AI (AI Journal)](https://aijourn.com/66degrees-named-2026-google-cloud-partner-of-the-year-for-artificial-intelligence/)
- [66degrees site](https://66degrees.com/?p=4247)
- [Cloudbakers/66degrees (CB Insights)](https://www.cbinsights.com/company/cloudbakers)

---

**You**

is BigQuery columnar?

---

**Claude**

Yes. BigQuery stores data in columns, using Google’s internal format called **Capacitor**. Queries run on **Dremel**, a distributed tree-structured execution engine, and storage sits on Colossus, separate from compute.

Since you know Vertica, here is how the two compare.

**Similar to Vertica**

- Queries read only the columns they reference, and data is compressed and encoded per column.
- It is built for scans, aggregations and joins over large tables, not row-at-a-time OLTP.

**Different from Vertica (worth saying in the interview)**

- **Compute and storage are fully separated and serverless.** You don’t size nodes. Compute comes as “slots,” either on-demand or reserved through editions. This is closer to Vertica Eon mode than to Enterprise mode, but with no cluster to manage.
- **No projections or traditional indexes.** Your physical-design levers are partitioning, clustering, materialized views and search indexes. Clustering is the closest thing to Vertica’s projection sort order.
- **Cost follows column choice.** On-demand pricing charges by bytes scanned, so `SELECT *` costs real money. Column pruning is a billing concern as well as a performance one, which makes it a good point to raise as an architect.
- **Nested and repeated fields (STRUCT/ARRAY) are first-class.** Because the columnar format handles nesting, Google often recommends denormalizing instead of strict star schemas. Expect a “star schema vs. nested tables” question.
- **Weak at frequent small updates.** Singleton UPDATE and DELETE statements are inefficient and subject to DML limits. Batch writes or streaming inserts with periodic MERGE are the usual patterns, much like Vertica’s trickle-load cautions.

A one-line answer for the interview: “Yes, Capacitor columnar storage on Dremel. Coming from Vertica, my physical design shifts from projections to partitioning and clustering, and I think about bytes scanned as a cost driver as well as performance.”

---

**You**

Tell me more about nested tables. What is the columnar limit? Remind me about clustering. Assume I will use wide denormalized tables.

---

**Claude**

### Nested and repeated fields

Instead of a fact table joined to child tables, you store the children inside the parent row:

- **STRUCT (RECORD)**: a group of fields embedded in a row. Use it for one-to-one data, such as a `customer` struct with `name`, `tier` and `region`.
- **ARRAY**: a repeated field. Use it for one-to-many data, such as an order’s line items.
- **ARRAY\<STRUCT>**: the main pattern. One order row holds an array of line-item structs.

```sql
CREATE TABLE sales.orders (
  order_id     STRING,
  order_ts     TIMESTAMP,
  customer     STRUCT<id STRING, name STRING, tier STRING, region STRING>,
  line_items   ARRAY<STRUCT<sku STRING, qty INT64, unit_price NUMERIC>>
)
PARTITION BY DATE(order_ts)
CLUSTER BY customer_id_flat, region_flat;  -- see clustering caveat below
```

You query the nested data with dot notation, and flatten arrays with `UNNEST`:

```sql
SELECT o.order_id, o.customer.region, li.sku, li.qty * li.unit_price AS amt
FROM sales.orders o, UNNEST(o.line_items) li
WHERE DATE(o.order_ts) = '2026-10-01';
```

**Why Google pushes this design:**

- Parent and child data are stored together, so the order-to-line-item join disappears.
- Each nested leaf field is still its own column. Selecting `line_items.sku` reads only that one column, so you keep columnar pruning even inside the nesting.

**The cost:**

- Updating one child element means rewriting the parent row.
- Dimensions that change slowly get copied into every row and go stale. In Kimball terms, you are freezing an SCD Type 1 or Type 2 snapshot into each fact row.

### Limits

- **10,000 columns** per table, query result or view, and this includes nested and repeated columns. Every leaf inside a STRUCT counts toward the 10,000.
- **Recently deleted columns** can keep counting toward that total for a while and cause false quota errors until it resets. This matters if your wide tables change schema often.
- **100 MB** maximum row size, approximate, and enforced during certain stages of query execution. A wide table with large nested arrays can hit this.
- **Nesting depth** is capped at 15 levels of STRUCT, as far as I know. Check the docs before quoting it.
- **Partitions** are capped at around 10,000 per table, also worth confirming. Separately, the daily quota on partition modifications cannot be increased, and Google’s fix is coarser partitioning, such as monthly instead of daily.

### Clustering

**How it works**

- BigQuery sorts data by the clustering columns and organizes it into blocks.
- Filters on those columns skip blocks entirely, so fewer bytes are scanned and the query costs less.

**Rules**

- **Up to four clustering columns.** If you need more selectivity, combine clustering with partitioning.
- **Order matters.** Data is sorted by the first column, then the second, and so on, just like a Vertica projection’s ORDER BY. Put your most common filter first.
- **Top-level, non-repeated columns only.** Allowed types include STRING, INT64, NUMERIC, BIGNUMERIC, DATE and DATETIME. You can’t cluster on `customer.region` inside a STRUCT, so you would promote the field to a top-level column. That’s what the `_flat` columns in my example stand for.
- **STRING columns** cluster on only the first 1,024 characters.
- **Maintenance is free.** Automatic reclustering, batch loads and table copies cost nothing. However, changing the clustering specification applies only to new data unless you rewrite the existing data.

**When to use it**

- Tables or partitions larger than about **64 MB** are the ones likely to benefit.
- Partition first only if partitions average around **10 GB or more**. Many small partitions bloat metadata and slow it down.

### Wide, denormalized design in one sentence

Partition on the date you prune by, cluster on up to four top-level filter keys in order of selectivity, nest one-to-many children as ARRAY\<STRUCT>, promote any nested field you filter on to the top level, and remember that every leaf counts toward 10,000 columns and on-demand billing is by bytes scanned, so tell users not to run `SELECT *`.

Sources:

- [BigQuery quotas and limits](https://cloud.google.com/bigquery/quotas)
- [BigQuery quotas (columns limit)](https://cloud.google.com/bigquery-transfer/quotas)
- [Introduction to clustered tables](https://developers.google.com/bigquery/docs/clustered-tables)
- [Troubleshoot quota and limit errors](https://cloud.google.com/bigquery/docs/troubleshoot-quotas)

---

**You**

If I have a customer struct and part of it is PII what's a good strategy?

---

**Claude**

A good default is to keep the struct as it is, put a **policy tag** on each PII leaf field, and add **dynamic data masking** on top. If the requirements are stricter, move the PII out of the wide table entirely.

### Option 1: Policy tags on nested leaf fields (the default)

Column-level security works on individual leaf fields inside a STRUCT, so `customer.email` can be locked down while `customer.tier` and `customer.region` stay open.

1. **Build a taxonomy** in Data Catalog / Dataplex, for example `PII > High (SSN, DOB)` and `PII > Medium (email, phone, name)`.
2. **Tag the leaf fields** in the schema with those policy tags.
3. **Grant Fine-Grained Reader** on each tag only to the groups that need the raw values.
4. **Add data masking policies** to the tags so everyone else gets a masked value instead of an error. Masking rules include SHA-256 hash, nullify, default value, last-four-characters, email mask, and year-only for dates.

Masking matters for usability. Without it, a user who lacks access gets an access-denied error on queries that touch the column, including `SELECT *`. They then have to write `SELECT * EXCEPT(...)`, which is awkward for nested fields. With masking, their queries run and just return masked values.

A **SHA-256 hash mask** is also useful for analytics: analysts can still count distinct customers and join on hashed email without ever seeing the raw value.

### Option 2: Split the PII out (when requirements are stricter)

When regulations, GDPR-style deletion or audit needs demand it, take PII out of the wide table:

- **Wide fact table:** holds `customer.customer_key` (a surrogate or token) plus non-PII attributes.
- **PII vault table:** keyed by `customer_key`, in a separate dataset or project with tight IAM and possibly CMEK encryption.
- **Authorized views:** join the two only for approved consumers.

This trades away some of the join-free benefit of denormalizing. In return:

- The PII has a single home.
- Deleting a customer is a one-row operation rather than a rewrite across every partition of the wide table.
- Access auditing is simple.

### Option 3: Encrypt inside the table

BigQuery’s AEAD functions, together with Cloud KMS-wrapped keys, let you encrypt values inside the row:

- **Deterministic encryption** keeps encrypted values joinable on equality.
- **Crypto-shredding** handles deletion: destroy a customer’s key and their data becomes unreadable, with no row rewrites. This is useful with wide denormalized tables, where rewriting rows across years of partitions is expensive.

### Supporting pieces

- **Sensitive Data Protection (formerly Cloud DLP)** finds PII you didn’t know about, often in free-text fields, and can de-identify data in the pipeline before it lands.
- **Row-level access policies** handle region-based restrictions, such as EU analysts seeing only EU rows. These are separate from column-level controls.
- **VPC Service Controls** around the project limit where data can be exfiltrated to.

### Interview line

“Keep the customer struct for analytics, tag the PII leaf fields with a policy-tag taxonomy, and apply dynamic masking with SHA-256 hashing so analysts can still join and count. For regulated data or right-to-delete, tokenize into a separate PII vault with authorized views, or use KMS-wrapped AEAD encryption so I can crypto-shred instead of rewriting partitions.”

---

**You**

I want to do RBAC, role based, not row based. How many roles push a limit for set joins and transforms? Also is there a masking type that preserves sort order?

---

**Claude**

### RBAC in BigQuery

In practice, RBAC here means mapping groups to sensitivity tiers:

- **Roles become Google Groups**, for example `analysts@`, `finance-pii@`, `support-pii@`.
- **Sensitivity becomes policy tags**, for example `PII-High` and `PII-Medium`.
- **Each tag gets data policies** that bind a group to an outcome: raw access, which needs Fine-Grained Reader, or a specific masking rule.

So you grant roles against tags, not against tables or columns. That design decision is what keeps it manageable.

### Does the number of roles hit a limit?

There is no hard ceiling on roles you’re likely to reach. The limits that matter come from structure and from how masking interacts with joins.

**Hard limits that shape the design**

- **One policy tag per column.** You cannot stack a role-specific tag for each role on the same column. All differences between roles have to be expressed as different data policies on a single tag.
- **Dataplex Attribute Store limits:**
	- 100 taxonomies per region
		- 10,000 attributes in total
		- 50 attributes per table
		- 4 levels of depth per attribute tree
- **IAM allow policies** cap the number of principals per policy, about 1,500 as far as I know. Always grant to groups, never to individual users, and you won’t come near it.

**What really sets the limit: joins on masked columns**

- Masking is applied when each user reads the data, so their joins and transforms operate on the masked values.
- **SHA256 is deterministic.** The same input always gives the same hash, so joins and GROUP BY still match across tables, provided both sides use the same masking rule.
- **RANDOM\_HASH breaks joins.** It adds a random value per query, so the masked output differs every time. Use it when you specifically want to prevent linking across queries.
- **Partial masks break joins on key columns.** LAST\_FOUR, FIRST\_FOUR and EMAIL\_MASK produce collisions, so many rows become `XXXXX@gmail.com`.
- **A user in several groups** gets only one masking rule per tag. BigQuery picks it by a fixed priority order, so check that order in the docs before relying on overlapping roles.

**Practical guidance:** keep it to about 3–5 sensitivity tiers and a handful of access outcomes. Beyond that, the problem is not quotas but that nobody can predict which join results a given person will see.

**For joins and transforms:** build them as authorized views or dbt/Dataform models that run under a service account with raw access. Join on surrogate keys, not on PII, and expose only the results. Then masking affects how values are displayed, not what joins correctly.

### Is there a masking type that preserves sort order?

Not exactly. The predefined rules are:

- SHA256
- ALWAYS\_NULL
- DEFAULT\_MASKING\_VALUE
- LAST\_FOUR\_CHARACTERS
- FIRST\_FOUR\_CHARACTERS
- EMAIL\_MASK
- DATE\_YEAR\_MASK
- RANDOM\_HASH

None of them preserves full sort order. Two preserve it coarsely:

- **DATE\_YEAR\_MASK** truncates dates to January 1 of their year, so year-level sorting still works.
- **FIRST\_FOUR\_CHARACTERS** keeps the prefix, so alphabetical order is preserved at four-character granularity.

**For anything finer, write a custom masking routine.** Data policies accept a custom routine (a UDF) instead of a predefined rule. You can make it coarsen values in an order-preserving way, for example truncating to the month, rounding amounts to bands, or bucketing ages.

**True order-preserving encryption isn’t offered,** and it’s cryptographically weak anyway: sorted ciphertext reveals the distribution of the values. The usual architect’s answer is not to sort on PII at all. Sort on a non-PII column such as the event timestamp or a surrogate key, or keep a coarsened copy as a separate column, for example `dob_year` alongside a masked `dob`.

### Interview line

“RBAC through groups bound to policy-tag data policies, a few sensitivity tiers, deterministic SHA-256 wherever joins must survive masking, and sensitive joins pushed into authorized views on surrogate keys. For sort order, I’d use a custom masking routine that coarsens values, or sort on non-PII columns, because order-preserving encryption leaks the distribution.”

Sources:

- [Dataplex Attribute Store quotas](https://cloud.google.com/dataplex/docs/attribute-store)
- [Column-level access control](https://cloud.google.com/bigquery/docs/column-level-security)
- [DataPolicy REST reference (v2)](https://cloud.google.com/bigquery/docs/reference/bigquerydatapolicy/rest/v2/projects.locations.dataPolicies)
- [PredefinedExpression reference](https://docs.cloud.google.com/ruby/docs/reference/google-cloud-bigquery-data_policies-v1/latest/Google-Cloud-Bigquery-DataPolicies-V1-DataMaskingPolicy-PredefinedExpression)

---

**You**

What's this about SET tables? Is that Teradata or BQ?

---

**Claude**

It’s **Teradata**. BigQuery has no equivalent, and that gap is why it matters in a migration.

### In Teradata

Every table is either SET or MULTISET:

- **SET tables do not allow fully duplicate rows**, meaning rows identical in every column.
	- A single-row `INSERT` of a duplicate raises an error.
		- An `INSERT ... SELECT` drops the duplicates without any error.
- **MULTISET tables allow duplicates**, like most databases.
- **The default depends on session mode.** In Teradata mode a plain `CREATE TABLE` produces a SET table; in ANSI mode it produces MULTISET. Many older Teradata warehouses are therefore full of SET tables that nobody chose on purpose.
- **Checking for duplicates costs performance**, so Teradata DBAs often add a unique primary index or a unique secondary index to make the check cheap.

### In BigQuery

- **Every table behaves like MULTISET.** Duplicates are always allowed.
- **Primary and foreign keys exist but are not enforced.** They are hints for the optimizer, for example to eliminate joins, not constraints.

### Why it breaks migrations

Old Teradata ETL often relies, without saying so, on SET tables silently removing duplicates. You might have reruns that are safe only because duplicates disappear, or overlapping extract windows. Move the same logic to BigQuery and those duplicates land in the table. Row counts grow, and aggregates are quietly overstated.

**How to handle it**

1. **Inventory first.** Query `DBC.TablesV` for SET tables. The BigQuery Migration Service assessment also reports on this.
2. **Replace the implicit deduplication with explicit logic:**
	- Use `MERGE` on the business key for incremental loads. This is the cleanest fix.
		- Or deduplicate in the transform with `QUALIFY ROW_NUMBER() OVER (PARTITION BY <key> ORDER BY <load_ts> DESC) = 1`. BigQuery supports `QUALIFY`, so this ports easily from Teradata.
		- Or use `SELECT DISTINCT` for small, true full-row duplicate cases.
3. **Add data-quality checks** to the pipeline, such as duplicate-key assertions in Dataform or dbt tests, because the database won’t enforce uniqueness for you.

**Interview line:** “Teradata SET tables silently remove duplicates and BigQuery enforces nothing, so I inventory SET tables up front and replace that implicit behavior with MERGE on business keys or QUALIFY ROW\_NUMBER() deduplication, plus uniqueness tests in Dataform or dbt.”

---

**You**

How much of Apache Beam is implemented in Dataflow?

---

**Claude**

Essentially all of it. **Dataflow is Google’s managed runner for Apache Beam**, and it was the reference implementation: Beam started as the open-sourced Dataflow SDK in 2016. In Beam’s capability matrix, Dataflow is the runner with the most complete coverage.

### What Dataflow supports from the Beam model

- **Core transforms:** ParDo, GroupByKey, CoGroupByKey, Combine, Flatten and Partition, plus side inputs and multiple outputs.
- **Windowing:** fixed, sliding, session and global windows.
- **Event-time processing:** watermarks, triggers (early, on-time and late firings) and allowed lateness. This is what separates Beam from simple batch tools.
- **Stateful processing:** per-key state and timers.
- **Splittable DoFn:** the framework for custom, scalable sources and sinks.
- **One programming model for batch and streaming:** the same pipeline code runs either way.
- **Exactly-once processing** in streaming, with an optional at-least-once mode that is cheaper and has lower latency.
- **SDKs:** Java and Python are fully supported. Go works, but its ecosystem is thinner.
- **Cross-language pipelines:** with Runner v2 (the portable runner), a Python pipeline can call Java transforms, such as the Kafka or JDBC connectors.
- **Higher-level layers:** Beam SQL, Beam YAML, the Beam DataFrames API in Python, and `RunInference` for ML models, including GPU workers.

### Where gaps show up

The gaps are rarely in the Beam model itself. They tend to be:

- **Connector maturity by SDK.** Java has the deepest set of I/O connectors. Python sometimes depends on cross-language wrappers around the Java ones.
- **Occasional newer or experimental Beam features** that reach the direct runner before Dataflow, or the reverse. Check Beam’s capability matrix for anything unusual.
- **Updating running pipelines.** Updating a streaming job in place requires compatible changes. Changing pipeline structure often means draining the job and relaunching it.

### What Dataflow adds beyond Beam

The value of the managed service is mostly operational:

- Horizontal **autoscaling** and **dynamic work rebalancing**, which reduces the impact of straggler workers.
- **Streaming Engine** and **Dataflow Shuffle**, which move state and shuffle off the worker VMs to make jobs cheaper and more stable.
- **Flex Templates** for parameterized, reusable jobs, plus Google-provided templates for common pipelines such as Pub/Sub to BigQuery and JDBC to BigQuery.
- Job monitoring through **Cloud Monitoring**.

### How it compares to Dataproc and BigQuery SQL

Choosing among these is a common interview question:

- **BigQuery SQL / Dataform:** for batch ELT where the data is already in BigQuery. It is the simplest and cheapest choice, and the right default for a wide denormalized warehouse.
- **Dataflow:** for streaming with event-time correctness (late data, windows, exactly-once), or heavy transforms before data lands, such as Pub/Sub or Kafka into BigQuery or de-identifying PII on the way in.
- **Dataproc:** when the client already has Spark or Hadoop code to lift and shift, or wants the Spark ecosystem. This is where your VerticaPy-versus-PySpark reasoning applies.

**Interview line:** “Dataflow is the reference runner for Beam and covers the full model, including windowing, triggers, state and timers, and exactly-once streaming, plus managed autoscaling, Streaming Engine and Flex Templates. I’d use it for streaming and pre-landing transforms, BigQuery SQL with Dataform for in-warehouse ELT, and Dataproc when a client has existing Spark.”

---

**You**

Which analytical functions will be missing from GBQ? How often does it need Spark or other external calculation engines? What's the best integration?

---

**Claude**

### Analytic gaps in BigQuery

There are fewer than you might expect, and several recent additions closed the big ones.

**Already covered, despite what older material says**

- Window functions, `QUALIFY`, ROLLUP, CUBE and GROUPING SETS, PIVOT and UNPIVOT, recursive CTEs, and `LAST_VALUE ... IGNORE NULLS`.
- **`MATCH_RECOGNIZE`** for pattern matching over row sequences, released in late 2025. Google presents it as familiar to anyone who has used Teradata’s nPath, which removes a classic Teradata migration blocker.
- **Managed Python UDFs**, generally available since June 2026. They run on BigQuery-managed serverless resources and can import NumPy, SciPy, pandas and scikit-learn directly from a SELECT. This covers much of the “we need a custom calculation” problem.

**Still missing or awkward**, with workarounds:

- **No true aggregate median or percentile.** `PERCENTILE_CONT` works only as a window function. For aggregates you use `APPROX_QUANTILES` or the window form with DISTINCT. There’s also no native MODE.
- **Time-series features like Vertica’s.** There is no `TIMESERIES` clause, no interpolated event-series joins, and no ASOF JOIN as far as I know. Gap filling and bucketing exist in some form, but as-of joins become window tricks or range joins.
- **RANGE window frames take numbers, not intervals.** You convert timestamps with `UNIX_SECONDS()`.
- **Teradata-specific features** such as NORMALIZE, EXPAND ON, the legacy CSUM and MSUM functions, and some PERIOD semantics need rewrites. The migration translator handles many of them.
- **Oracle MODEL clause and CONNECT BY.** CONNECT BY becomes a recursive CTE. MODEL becomes procedural scripting.
- **No multidimensional cube engine.** Essbase-style outlines, member formulas and allocations become SQL or a semantic layer. This is your strongest area of expertise, so it’s worth raising.
- **Iterative and algorithmic work:** graph algorithms like PageRank, optimization solvers, heavy Monte Carlo, and matrix work. BigQuery scripting loops can do it, but slowly and expensively.

### How often you actually need Spark or another external engine

For a typical warehouse migration with wide denormalized tables, **rarely**. Most analytics, ELT and classical machine learning (BigQuery ML) stay inside BigQuery. The Python UDFs have reduced this further.

**When an external engine is justified**

1. **Existing Spark code or a team that knows Spark.** Rewriting working code is often wasteful.
2. **Iterative or algorithmic workloads:** graphs, simulations, large custom ML training.
3. **Heavy processing before data lands:** large raw files, deeply nested JSON, unstructured data, especially in streaming.
4. **Lakehouse requirements:** multiple engines sharing Iceberg tables.

### Best integrations, in order of preference

1. **Native SQL + BigQuery ML + Python UDFs.** No data movement, one billing model, and one governance model, so your policy tags and masking still apply.
2. **BigQuery DataFrames (bigframes).** A pandas-style API that generates SQL and pushes it down to BigQuery. **This is the BigQuery equivalent of VerticaPy and its vDataFrame**, so you can explain it in your own terms.
3. **Remote functions** (on Cloud Run) when the calculation needs an external service or API.
4. **Serverless Spark** (formerly Dataproc Serverless) or **Spark stored procedures** called from BigQuery. Spark reads through the BigQuery Storage Read API, which is fast columnar access with column-level security enforced. For a multi-engine lakehouse, use **BigLake Iceberg tables** as shared storage instead of copying data between engines.
5. **Dataflow** for streaming and event-time work, as discussed earlier.

**Interview line:** “Most of the classic gaps are closed: MATCH\_RECOGNIZE replaces nPath, and Python UDFs cover custom math. My default is to push compute into BigQuery with bigframes, which is essentially VerticaPy for BigQuery. I bring in serverless Spark over the Storage API or BigLake Iceberg only for existing Spark code, iterative algorithms, or lakehouse sharing, so governance stays in one place.”

Sources:

- [Managed Python UDFs GA (Google Cloud blog)](https://cloud.google.com/blog/products/data-analytics/python-udf-in-bigquery-now-generally-available?hl=en)
- [Introducing MATCH\_RECOGNIZE in BigQuery (Google Cloud blog)](https://cloud.google.com/blog/ja/products/data-analytics/introducing-match_recognize-in-bigquery?hl=ja)

---

**You**

I'm thinking that dumping subsets of data into separate narrower 'analytical tables' computed by DuckDB will outperform Pandas, Python and Polars. How clumsy might that be?

---

**Claude**

Your instinct is mostly right about the engine. The awkward parts are moving the data out and losing governance, not DuckDB itself.

### Performance

- **DuckDB versus pandas:** DuckDB usually wins by a wide margin on joins, aggregations and window functions. It’s vectorized, multithreaded and spills to disk, while pandas is single-threaded and limited to memory.
- **DuckDB versus Polars:** roughly even. Results depend on the workload, and either can win a given benchmark. Choose based on whether your team prefers working in SQL or in a dataframe API.
- **Plain Python loops:** no comparison; DuckDB is far faster.

So DuckDB is a reasonable engine for working on extracted subsets.

### Where it gets awkward

1. **Narrow tables gain less in BigQuery than you’d expect.** BigQuery is already columnar, so a query that selects 12 columns from a 3,000-column table reads only those 12. A narrow copy pays off only when it also **pre-aggregates, pre-filters or pre-joins** the data. You can build that inside BigQuery with `CREATE TABLE AS SELECT`, materialized views or Dataform models, with no export at all.
2. **Exporting bypasses your governance.** Once data lands in Parquet files or a DuckDB database, policy tags, masking, row-level policies and audit logs no longer apply. After everything we discussed about PII, this is the issue an interviewer would raise. If you do export, export from masked or authorized views, and treat the extracts as governed assets with their own storage access controls and retention.
3. **Keeping extracts current becomes your job.** Someone has to own refreshes, schedules, incremental logic and checks that each extract still matches its source. Copies tend to multiply without anyone tracking them.
4. **Getting the data out.** You have two options:
	- `EXPORT DATA` to Parquet in Cloud Storage, which DuckDB reads directly.
		- The community DuckDB BigQuery extension, which reads through the Storage Read API. It’s convenient, but Storage API reads are billed and the extension isn’t Google-supported.
5. **Single-node limits.** DuckDB is excellent up to a few hundred GB on a large VM. Beyond that, you’re back to BigQuery or Spark.

### Where it’s worth doing

- **Repeated, interactive iteration on a stable subset**, such as notebooks, feature exploration or model development. With BigQuery on-demand pricing, every query is billed and has a second or two of startup latency, while local DuckDB costs nothing per query and returns in milliseconds.
- **Cost control** for teams that run the same exploratory queries many times.
- **Embedded or edge analytics**, or shipping a self-contained data product to a client.
- **Dev and test environments** that mirror production logic cheaply.

### A sound pattern

1. BigQuery does the heavy lifting and the governance.
2. Dataform or dbt builds narrow, **pre-aggregated, already-masked** marts inside BigQuery.
3. Marts that need fast local iteration are exported to Parquet or Iceberg in Cloud Storage. Exporting to BigLake Iceberg tables lets BigQuery and DuckDB share the same files instead of keeping copies.
4. DuckDB, or MotherDuck for shared use, handles the interactive work.

**For the interview:** 66degrees sells Google Cloud. Present DuckDB as an addition for developer productivity and cost control, not as a way around BigQuery. For example: “I keep compute and governance in BigQuery and push everything I can down with bigframes. For tight iteration loops on governed, pre-aggregated marts, I’ll use DuckDB over Iceberg in Cloud Storage. It’s cheaper per iteration, and the data stays on the same files instead of being copied.”

---

**You**

Remind me of what Dataform is again.

---

**Claude**

Dataform is **Google’s SQL transformation framework built into BigQuery**, essentially Google’s version of dbt. Google acquired it in 2020 and now runs it as a managed service inside the BigQuery console.

### What it does

- **SQLX files:** each file is a SQL `SELECT` plus a config block that declares what it produces, such as a table, a view, an incremental table or an assertion.
- **`${ref("table_name")}`** declares dependencies between models. Dataform uses these to build the dependency graph and run models in the right order, the same way dbt’s `{{ ref() }}` does.
- **Incremental tables** process only new or changed rows, typically by generating a MERGE.
- **Assertions** are data-quality checks, such as uniqueness, non-null and custom conditions. In Teradata migrations, this is where you replace the deduplication that SET tables used to do.
- **Git integration:** repositories, workspaces for development, and pull-request workflows.
- **Scheduling:** release configurations compile a branch, and workflow configurations run it on a schedule. For more complex orchestration, you trigger it from Cloud Composer (Airflow) or Workflows.
- **JavaScript** is used for templating and generating SQL dynamically, where dbt uses Jinja.

### Cost

Dataform itself is free. You pay only for the BigQuery compute its SQL uses.

### Dataform versus dbt

|  | Dataform | dbt |
| --- | --- | --- |
| Warehouses | BigQuery only | Many |
| Templating | JavaScript | Jinja |
| Hosting | Managed in the BigQuery console, no extra cost | dbt Core (self-run) or dbt Cloud (paid) |
| Ecosystem | Smaller | Large: packages, community, semantic layer |
| Governance fit | Native IAM, part of the GCP setup | Requires separate setup |

**When to use each:** choose Dataform for a client that is committed to BigQuery and wants the simplest native option. Choose dbt for a client that uses several warehouses, already has dbt models, or wants its broader ecosystem.

**Interview line:** “Dataform is BigQuery’s native version of dbt. It uses SQLX models with ref-based dependency graphs, incremental tables, assertions and Git workflows, and it costs only the BigQuery compute it runs. I’ve used dbt, and the concepts carry over almost directly; mainly you swap Jinja for JavaScript templating.”

---

**You**

How would I create a region redundant system for GBQ in a 'pilot light' fashion?

---

**Claude**

Pilot light fits BigQuery well. In a pilot light design, data is kept continuously in sync in the second region, while compute and the surrounding pipelines stay minimal or turned off until you fail over. BigQuery offers two ways to do this, at different price points.

### Option A: Cross-region replication (the cheaper pilot light)

**How it works**

- Turn on **cross-region dataset replication** for each dataset you need to protect. The secondary region holds a read-only replica.
- On failover, **you promote the dataset**, one dataset at a time. It’s a soft failover and works with any capacity model.

**Keeping the secondary small**

- In the secondary region, define a reservation with **zero baseline slots and autoscaling**, or just plan to use on-demand pricing there.
- The result: you pay only for replicated storage and replication traffic until something goes wrong.

**Tradeoffs**

- Recovery is slower and manual, because you promote datasets one by one.
- RPO depends on standard replication lag.

### Option B: Managed disaster recovery (the better pilot light, on Enterprise Plus)

**How it works**

- Create a **failover reservation**: an Enterprise Plus reservation in the primary region with a `secondary_location` set.
- **Attach datasets to it.** You can attach up to 1,000.
- Standby compute in the paired region is included in the reservation. However, those slots aren’t usable until you fail over, and stale reads in the secondary need capacity you buy separately.
- Google’s documentation shows exactly the pilot-light shape: `slot_capacity = 0` with an `autoscale_max_slots` ceiling.

**Recovery characteristics**

- **Turbo replication** shrinks the window for data loss, and RPO is defined per dataset.
- **Five-minute RTO** once you start a failover.
- **Two failover types:**
	- *Soft failover* waits until everything committed in the primary has replicated. Use it for planned events and drills.
		- *Hard failover* promotes the secondary immediately. Use it when the primary region is actually down.

**Constraints to mention in the interview**

- Once a dataset is attached, **only Enterprise Plus reservations can write to it**. Reads can use any capacity model.
- Load and extract jobs can’t use the free shared slot pool. You need a PIPELINE reservation assignment.
- Replicated storage is billed at the same list price as primary storage, plus turbo replication charges.

### The rest of the platform

BigQuery replication covers only the datasets. A real pilot light also has to restart everything that runs around them:

- **Infrastructure as code for region two.** Write Terraform for the secondary reservation, IAM, service accounts, Composer, Dataflow and networking. Run `plan` regularly and `apply` only during failover. Keep Composer off in the secondary, because an idle Composer environment costs money.
- **Landing zone:** use dual-region or multi-region **Cloud Storage** buckets so raw files and Parquet exports survive the outage too.
- **Pipelines:** store Dataflow Flex Templates and container images in a multi-region Artifact Registry. Point Dataform release and workflow configurations at the secondary location.
- **Governance:** policy tag taxonomies and data policies belong to a location. Confirm that the secondary has matching taxonomies, so PII masking still works after failover. Otherwise the DR region becomes a governance hole.
- **Clients:** BigQuery jobs specify a location. Make apps and BI tools switch region through a config flag or connection setting, not hard-coded values.
- **Runbook and drills:** run a scheduled soft failover each quarter, and measure the real RTO and RPO against the client’s targets.

### DR is not backup

Replication copies mistakes and corruption to the secondary too, such as a bad `DELETE` or a broken pipeline run. Pair it with:

- **Time travel**, up to 7 days.
- **Table snapshots** or clones for longer retention, ideally in a separate project.

### Interview line

“For pilot light, I replicate datasets cross-region and keep compute at zero baseline in the secondary. On Enterprise Plus I’d use managed DR with a failover reservation: zero baseline slots, an autoscale ceiling, turbo replication, and roughly a five-minute RTO. Around it I keep Terraform ready to stand up Composer and Dataflow, dual-region Cloud Storage, and matching policy-tag taxonomies so masking survives failover. I run quarterly soft-failover drills, and use snapshots and time travel for logical corruption, since replication copies mistakes too.”

Sources:

- [Managed disaster recovery (BigQuery docs)](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery?authuser=1)
- [Migrate to managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/disaster-recovery-migration)
- [BigQuery gets managed disaster recovery (Google Cloud blog)](https://cloud.google.com/blog/products/data-analytics/bigquery-gets-managed-disaster-recovery)

---
Yes. BigQuery keeps a queryable history of past jobs, including each one's executed query plan, for about 180 days.

## 1. `INFORMATION_SCHEMA.JOBS` (the main source)

This is the closest equivalent to Vertica's `v_monitor` tables (`query_requests`, `query_plan_profiles` and the `dc_*` tables). You choose a view by scope:

- `region-us.INFORMATION_SCHEMA.JOBS` or `JOBS_BY_PROJECT`: everything in the project
- `JOBS_BY_USER`: your own jobs
- `JOBS_BY_FOLDER` and `JOBS_BY_ORGANIZATION`: across projects, for platform-level FinOps

**Columns worth knowing**

|Column|What it tells you|
|---|---|
|`query`|The SQL text|
|`creation_time`, `start_time`, `end_time`|Queue time and run time|
|`total_bytes_processed`, `total_bytes_billed`|Cost, under on-demand pricing|
|`total_slot_ms`|Compute consumed, under reservations|
|`cache_hit`|Whether the query was served from cache|
|`job_stages`|**The executed query plan**: per-stage records, wait, read, compute and write time, shuffle, and rows in and out|
|`timeline`|Slot usage over the life of the query|
|`referenced_tables`|Lineage, and which tables are hot|
|`reservation_id`, `labels`|Chargeback by team or pipeline|
|`query_info`|Includes a hash that normalizes literals, so you can group similar queries. Some versions also expose performance insights. Check the column list in your region.|
|`error_result`|Failures|

**Example: the most expensive query patterns in the last 7 days**

```sql
SELECT
  query_info.query_hashes.normalized_literals AS query_hash,
  ANY_VALUE(query)                            AS sample_query,
  COUNT(*)                                    AS runs,
  SUM(total_bytes_billed) / POW(1024, 4)      AS tib_billed,
  SUM(total_slot_ms) / 1000 / 3600            AS slot_hours,
  AVG(TIMESTAMP_DIFF(end_time, start_time, SECOND)) AS avg_secs
FROM `region-us`.INFORMATION_SCHEMA.JOBS
WHERE job_type = 'QUERY'
  AND creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 7 DAY)
GROUP BY query_hash
ORDER BY slot_hours DESC
LIMIT 20;
```

To look at one query's plan, `UNNEST(job_stages)` for that `job_id`. Signs of trouble:

- **Skew:** a stage's maximum compute time is far above its average.
- **Spill to disk:** large shuffle output.
- **Poor pruning:** read time dominates, which often points to partitioning or clustering that isn't being used.

## 2. Console: Execution details

Open any job in **Personal history** or **Project history** and use the **Execution details** tab.

- It shows the **execution graph**: a visual query plan with stages, timing and slot use, plus the **performance insights** that BigQuery generates.
- It's quicker than SQL for diagnosing a single slow query.

## 3. API and logs

- **`jobs.get`** returns `statistics.query.queryPlan`. Monitoring tools read the plan from here.
- **Cloud Audit Logs:** route them to **Log Analytics**, or to a BigQuery dataset with a log sink, to keep history beyond the 180-day retention or to centralize it across projects.
- **Admin resource charts** and the **slot estimator** cover capacity planning for reservations.

## One gap compared with Vertica

There is no true `EXPLAIN` before a query runs. A **dry run** returns only the estimated bytes to be processed, not a plan. You see the plan only after execution, in `job_stages` or the console.

**Interview line:** "INFORMATION_SCHEMA.JOBS gives me about 180 days of jobs with executed plans in `job_stages`. I group on the normalized query hash to rank cost by pattern, check stages for skew and spills, use labels and reservation IDs for chargeback, and export audit logs when I need longer retention. It's the BigQuery version of Vertica's v_monitor plus query profiles."