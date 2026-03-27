---
title: "ISTD vs Medallion"
source: "https://tessellations.substack.com/p/istd-vs-medallion"
author:
  - "[[By Michael David Cobb Bowen]]"
published:
created: 2026-03-27
description:
tags:
  - "brain_spew"
---
Several years ago I ventured into the strange and wonderful world of columnar analytical database design on AWS. Originally I started with Vertica, a fascinating product that the market forgot. I would say that I’m a master of that amount of small data, which was then considered big data. Our motto was BIG, FAST, WIDE and our aim was to migrate on-prem analytical systems to AWS. We did well, iterating to something we called the PITbull Architecture for Elastic Data Warehouse. Our primary difference was that we expected smart DBAs (like us) to determine when and how much the hot layer of the database was expanded or contracted rather than have the system make that determination itself.

We always did structured data lake. We always did materialized views for end user queries. We always did wide tables. We always did hot/cold mix. We always had control over all of that. So in 2016 I wrote the following in the informal data-bro language familiar to us all.

**October 2016**

### Vertica Idempotent Set Transformational Denormalized Design Standards

At Full360, we have developed a best practice around our design of greenfield and re-engineered DW applications. The following is a high level guide to how we accomplish this in Vertica. Vertica optimization is something we have pursued with vigor at Full360. There are several different levels at which this can be pursued. Implicit is the modularization of the applications so that the major functions of our data management philosophy can be expressed discretely. But let’s get to the $10 words, shall we?

**Idempotency**  
Both I and JDub could go on at to absurd lengths about how important this is to the modularization of DW design. I will simply, which characteristic casualness, tell you that it makes all of our stuff idiot proof, in that it makes our data provision dependencies kind of go away. The basic idea is that *in application units* (which basically means the chunks at which the data to be consumed makes process and business sense) you make your input streams discrete. So when your input streams are discretely chunked, you can run your process over and over without concern about whether it has been done once, twice or never. You just run that independent data provision job and it creates the right sized bucket of data.

**Set Transformational**  
VLDB folks are probably familiar with why you do ELT rather than ETL. The simple way of saying it is that database developers are more stingy and efficient with data than ETL developers. I developed a taste for hand-crafted ‘ETL’ back in the days when Informatica was a baby, and having my Unix biases, I always loved moving files around. At the time, my focus was on Essbase which had not ETL hooks, even though Arbor should have purchased an ETL company cheap. Interestingly tangential, Wall Street has never been very long in ETL companies. Anyway, I expect that Informatica and Talend will not like to hear that their days are numbered, but then neither did Carleton and DataStage, and they used to rule the world. The bottom line is that moving data from table to table using SQL rather than in a GUI that does not is going to be, in certain databases, much faster and more human readable than in third party tools. So we do set transformation, and even regex stuff, inside Vertica. One day we may even benchmark UDFs against external programs.

**Denormalized**  
Vertica like Redshift is not a transaction database. It is columnar and it easily handles 600, 800, 1200 column tables. It was designed to. So there is no reason to do a lot of silly little joins in silly little tables to get juicy fat data. We make all that part of the ingestion process, which gives us what we want. Think about it for a minute. Consider the volatility of lookup tables and dimensions as compared to the volatility of atomic facts and transactions, aggregated or otherwise. The facts will be bigger and more fluid. So why spend join energy on query exhibits over the long haul when you can easily have all the columns you want? You don’t have to. There are no table scans from hell, that’s what columnar solves. So we go big.

**Production**  
I’m not going to talk about the guts of Production other than to mention it briefly here. Production is some of the genius and we have a bag of tricks that is ever-expanding as we deal with realtime, near-realtime, and other odd types of data sources. Yes we lambda with streams and lakes, but we smart lambda. Again with whatever tech makes sense. Right now we’re playing with Kinesis and Kafka and our own custom Actor models which we’re sure will evolve over time. We’re also looking at how to use Redis and other superfast KV stores. So I suspect we will grow many efficient tentacles as we Produce standardized data for ingestion into our columnar DW apps. Nuff said.

### Ingestion

#### \_SRC

We ingest data into source tables for each schema as they come to us. No matter how many fields, large or small, we will take them in using a COPY from produced files. Whether in Vertica or Redshift we standardize on UTF-8 with vertical bars delimited and a backslash escape. In some cases, if we’ve munged up variable length stuff from our own custom regex routines or other JSON, AVRO or semi-structured effluvia, we will have an additional pre-step using Vertica Flex Tables. We are coming up with best practices there too.

These source files should also retain the original names of the fields of the produced data when possible. This assists in debugging with the original developers.

#### \_STG

All of the data that is to be used in the application should then be mapped to a view. This is the staged data. Staged data should be of the increment of ingestion (discretely chunked in application consumption units). That is to say that your \_SRC and \_STG will carry the same number of records although they are likely to carry a different number of fields once the ingestion is done.

### Transformation

#### \_CLN

The clean tables should be materialized tables with human-readable fields that are conceptually discrete. This is generally accomplished through a direct insert from one or more *STG views. Clean tables can be defined with blank fields for further rule application. Clean tables that contain all history for the query space should have the term \_HIST* CLN, otherwise one should assume that a clean table is the same size as an ingestion increment. Clean tables should be optimized for the scope of the transactions that take place in their creation. When you are looking at the clean tables, you have all of the data you need from all of the sources presented in the way you as a developer think about the data. There should be very little ambiguity at this point, it’s your best look at the details before they are aggregated and rationalized.

#### \_LKP

Lookup tables are straightforward. They should be optimized for their transaction capacity with clean tables.

#### \_IFT

In a complex model, clean tables can be made into Intermediate Fact tables. The intermediate fact tables are materialized tables with all of the necessary dimensions that support measures that can be made across the full query space. These may or may not be exhibited directly, but should be useful in a partial analysis of the particular measures they contain. An intermediate fact table should be the place where window functions are applied. They should be the place where obscure field conditions are made into explicit attribute and status fields. It is important to know that an application may have dependencies of different measures that seem to be dimensionally equivalent, but actually aren’t. So by using IFTs we unburden ourselves of the very idea of a single massive star or snowflake that might have holes. Also, we can capture all of the attributes of a set of measures completely without concerning ourselves with the weight of them in the final presentation layer.

So think about this. A clean look of the data will probably not have sensible status fields they will have codes. There may be multiple ways to interpret a certain combination of fields. So whatever you need to support a the full scope of consumable data, even if it means synthetically remastering transactions, you can do with IFTs beforehand. Building these are the real guts of the DW application, and it’s where the fun of working with sharp analysts come in, especially when it comes to data integration projects. I will apply all of the reasonable and semi-reasonable business rules here. This is where I have enough detail to point machine learning, because at this point the data is explicit and human readable. It will reveal the more interesting cases and outliers. And here it should be very rich - beyond human comprehension, so yeah maybe you don’t go full wide with these tables, only add 4 of the 50 psychographic customer tags you have against their ID, because, security.

#### \_XBT

Exhibit tables are materialized views in some cases but generally views that are presentable to the end user. These should be indexed and optimized for query retrieval. Security access rules are applied to user groups, etc only to exhibit tables. It should be assumed that none other than dbadmin processes will have access to any tables or views but the exhibit tables.

So there it is. This is rather the state of the art that I have internalized in five years of cloud based columnar data warehousing. Maybe I should write a book.

Since then, Snowflake and Databricks have done well in the market. Databricks is closer to doing open-source agnostic stacks, and they have done well. But I’m tending to think I’m more of a purist. So here I asked Claude 4.5 Opus to compare and contrast what you see above with their Medallion Architecture. Here’s what it said.

#### Comparison: Idempotent Set Transformational Denormalized Design Standards vs. Medallion Architecture

Both architectures address data warehouse design patterns but come from different eras and contexts. Here’s a detailed comparison:

**Historical Context**

- ISTD Standards: From 2016, designed for Vertica columnar database with emphasis on traditional data warehousing
- Medallion Architecture: Coined and popularized by Databricks in the 2010s, designed for modern data lakehouse environments

**Core Philosophy**

**ISTD Standards** emphasizes four key principles:

1\. Idempotency: Making data processes repeatable and dependency-free

2\. Set Transformational: Using SQL-based transformations within the database (ELT approach)

3\. Denormalized: Leveraging columnar storage for wide, joined tables

4\. Modular Design: Discrete application units for data consumption

**Medallion Architecture** focuses on progressive data refinement through three layers (Bronze, Silver, Gold) to incrementally improve data quality and structure.

**Data Flow Architecture**

ISTD Standards uses a 6-layer approach:

- \_SRC: Raw source data ingestion
- \_STG: Staged views for transformation
- \_CLN: Clean, materialized tables with human-readable fields
- \_LKP: Lookup tables for dimensions
- \_IFT: Intermediate fact tables with business rules applied
- \_XBT: Exhibit tables for end-user consumption

Medallion Architecture uses a 3-layer approach:

- Bronze: Raw, unvalidated data ingested from various sources in original formats
- Silver: Cleaned, validated, and conformed data with enterprise view of business entities
- Gold: Business-ready aggregated data optimized for analytics and reporting

**Key Similarities**

1. ELT Approach: Both favor ELT methodology over ETL, performing transformations within the data platform rather than external tools
2. Progressive Refinement: Both architectures improve data quality through successive layers
3. Idempotency: Both emphasize repeatable, dependency-free processes
4. Columnar Optimization: Both leverage columnar storage capabilities for analytics

**Key Differences**

**Modern Relevance**

ISTD Standards remains relevant for:

Medallion Architecture is better suited for:

- Large volumes of diverse data types, flexible business requirements, compliance needs, and data lakehouse strategies
- Cloud-native environments with elastic compute
- Organizations implementing modern data mesh principles

**Conclusion**

ISTD Standards represents a more granular, database-specific approach optimized for traditional analytical workloads, while Medallion Architecture provides a simpler, more flexible framework designed for modern cloud-based data lakehouses. Both share the core principle of progressive data refinement, but Medallion’s three-layer simplicity has made it more widely adopted in contemporary data engineering practices.

I’m not going to debate these points. People have built what they have built. Everybody’s reasons are good until they ain’t. Most never do greenfields again. But I think that’s where ISTD stands out, because it’s not so tool specific, since now there are more columnar stores, including the in-memory stuff in Apache Arrow and DuckDB. I think Clickhouse works this way as well.

**BUT DataLake Formats**  
Essentially we can debate the applicability of data lakehouse concepts separately. And I think that’s where the larger differences are. I absolutely did nothing with Athena, and very little with Parquet or Orc sink for our producers. For us, CSV was king primarily because it compressed so nicely, but we also did a lot of KV. Iceberg still isn’t complete, and it may not become a standard.

At any rate, I aim to target the <50TB space. Quite frankly I’m in favor of the Small Data Revolution as I talked about in Kermadec. In the meantime, I hope this help explain where I’m coming from. I think there are exciting new tools to instrument ISTD including Temporal. More later.