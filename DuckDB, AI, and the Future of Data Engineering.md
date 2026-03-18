---
title: "DuckDB, AI, and the Future of Data Engineering"
source: "https://dataengineeringcentral.substack.com/p/duckdb-ai-and-the-future-of-data?publication_id=1224799&post_id=190151530&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2026-03-18
created: 2026-03-18
description: "with Staff Engineer, Matt Martin"
tags:
  - "brain_spew"
---
<video><source src="https://dataengineeringcentral.substack.com/api/v1/video/upload/5a679a05-32f6-42e4-8d40-1d627a7497f8/src?token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTkwMTUxNTMwLCJpYXQiOjE3NzM4Mzk0NTUsImV4cCI6MTc3NjQzMTQ1NSwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.3pPUQ3chYh_I1s9RfrVmOMacaUbdwVtWN0ad43GtrlI&amp;override_publication_id=1224799&amp;preview=false&amp;type=hls" type="application/x-mpegURL"> <source src="https://dataengineeringcentral.substack.com/api/v1/video/upload/5a679a05-32f6-42e4-8d40-1d627a7497f8/src?token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTkwMTUxNTMwLCJpYXQiOjE3NzM4Mzk0NTUsImV4cCI6MTc3NjQzMTQ1NSwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.3pPUQ3chYh_I1s9RfrVmOMacaUbdwVtWN0ad43GtrlI&amp;override_publication_id=1224799&amp;preview=false&amp;type=mp4" type="video/mp4"></video>

0:00

/

0:00

Transcript

0:00

SPEAKER 3

I would say a few things. Cost is definitely a factor. You always got to, especially from an enterprise perspective, put your FinOps hat on and make sure that your costs are in line.

0:14

SPEAKER 1

Welcome to the Data Engineering Central Podcast. I'm Dan Beach, your host. Today we've got Matt with us. How's it going, Matt? Good. Awesome. So I know you from LinkedIn. I know you now as the DuckDB guy. I don't know. It's just do.

0:33

SPEAKER 3

Yeah, no, I mean, it's a great platform. I've lived and breathed it now for a few years, and I sit there and I'm like, I wish I had this back in 2010 when I was an analyst at home. This would have made my life so much easier.

0:50

SPEAKER 1

So for people who don't know who you are, just give them like a 30 second. You're on Substack LinkedIn data stuff. Just give them a quick high level of what you talk about and do.

0:59

SPEAKER 3

Sure. So my name is Matt Martin. I work for State Farm as a staff engineer, work primarily on big data engineering cloud stuff. Um, pretty active on LinkedIn and I write on Substack from time to time to help kind of get my thoughts out.

1:19

Um, other than that, got a wife and three kids and, uh, I row as a hobby, not on the water.

with Staff Engineer, Matt Martin

In this episode, I sit down with **Matt Martin**, Staff Engineer, data architect, ETL practitioner, and author of a new book on DuckDB coming soon, to talk about the past, present, and future of **data engineering**.

> Matt has spent decades building and architecting data platforms across technologies such as **SQL Server, Oracle, DB2, Hadoop, Redshift, and BigQuery**, and now focuses on modern tools such as **DuckDB and single-node analytics**.

![](https://substackcdn.com/image/fetch/$s_!JaMR!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3e8993f7-12a1-45e1-bb52-03833100f73a_1592x684.png)

We discuss how the data industry has evolved, what actually makes data platforms succeed, and where tools like **DuckDB, Polars, Databricks, and Snowflake** fit into the future of analytics.

We also dive into the impact of **AI on coding and data engineering**, and whether distributed compute clusters will remain dominant — or if more workloads will move toward **high-performance single-node systems**.

---

## Topics Covered

- Matt’s early career and journey into data engineering
- The evolution of data warehousing and ETL frameworks
- Traditional enterprise data systems vs modern cloud platforms
- DuckDB and the rise of single-node analytics
- Polars vs DuckDB: where each tool shines
- Databricks vs Snowflake
- AI-assisted coding and its impact on engineers
- The current data engineering job market
- Lessons learned from decades of building data systems
- Writing a book on DuckDB