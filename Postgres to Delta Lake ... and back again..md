---
title: Postgres to Delta Lake ... and back again.
source: https://dataengineeringcentral.substack.com/p/postgres-to-delta-lake-and-back-again?publication_id=1224799&post_id=163175767&isFreemail=false&r=7br8e&triedRedirect=true
author:
  - "[[T50/Daniel Beach]]"
published: 2024-12-11
created: 2025-05-12
description: back and forth
tags:
  - clippings
---
### back and forth

![](https://substackcdn.com/image/fetch/w_424)

Strangely enough, or maybe not so strange, when you find yourself working in a Lake House environment, it’s not uncommon to find the odd Postgres database hanging around the edges. You know, like the third wheel at the party in the corner looking awkward.

I think it’s one of those things; the whole RDMBS ← → Lake House is something everyone does, and no one talks about for some reason. Too dull, too many ways to do it? Who knows.

On a semi-regular basis I find myself doing one of two things.

- *pushing data from Delta Lake into Postgres*
- *pull data from Postgres into Delta Lake*

I mean, it’s the classic Data Engineering problem, right? Running old and new technology beside each other makes **them play nice together!**

Very often, our data systems as a whole are made up of various pieces and parts, and the Lake House + RDMBS is one that often crosses paths.

> So today, we will examine this problem and try to solve it using several different technologies. We will s *ee which one we like best.*

## The classic Spark + Postgres.

Surprisingly enough, I see a lot of people reach for that old trusty friend of us all, [psycopg2](https://pypi.org/project/psycopg2/). Pre-Lake-House world when Data Engineering started to become a thing and the Data Warehouse roamed the land, psycopg2 was the tool of choice.

> *A lot of folk still us it, stuck in the old way of their forefathers.*

When it comes to PySpark, the current king of the Data Engineering hill, provides something nice called the [.jbdc() writer on a DataFrame](https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.DataFrameWriter.jdbc.html).

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/eeceb946-5a5b-411f-86e0-e261af7d8c13_2138x1010.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:688,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:309801,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://spark.apache.org/docs/latest/api/python/reference/pyspark.sql/api/pyspark.sql.DataFrameWriter.jdbc.html%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Feeceb946-5a5b-411f-86e0-e261af7d8c13_2138x1010.png%22,%22isProcessing%22:false,%22align%22:null})

I mean this beautiful snippet of code you see following allows the simple muggle to take a DataFrame and push it straight into a Postgres table, existing or not, append or truncate etc.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/153f73f8-1d76-4949-83c4-08a035a3a99f_1766x1228.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1012,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:311570,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F153f73f8-1d76-4949-83c4-08a035a3a99f_1766x1228.png%22,%22isProcessing%22:false,%22align%22:null})

This has been my go-to for a long time, it’s just so simple and easy to use. I don’t care about the speed or efficiency that much (*it is annoyingly slow*), just let the method rip and it will get the job done.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/3b209369-bd4a-459f-83b9-8a63478b219b_1360x446.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:446,%22width%22:1360,%22resizeWidth%22:null,%22bytes%22:99764,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3b209369-bd4a-459f-83b9-8a63478b219b_1360x446.png%22,%22isProcessing%22:false,%22align%22:null})

It’s hard to argue with simple code, you can keep your fancy stuff.

## Other options?

Curious about other options, I would hope there are plenty considering the lineup of new tooling we have to work with these days, DuckDB, Polars, Daft and the like.

> *Since we have already talked about [DuckDB + Delta Lake](https://dataengineeringcentral.substack.com/p/duckdb-delta-lake), it shouldn’t be that hard to extend it to Postgres eh?*

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/6f86160e-9745-44c4-96a0-49e815d15c9d_2138x1010.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:688,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:980173,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://dataengineeringcentral.substack.com/p/duckdb-delta-lake%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6f86160e-9745-44c4-96a0-49e815d15c9d_2138x1010.png%22,%22isProcessing%22:false,%22align%22:null})

Can DuckDB be used?

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/0d445033-d361-44e6-914b-114f5a8aa75a_1900x1266.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:970,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:248950,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0d445033-d361-44e6-914b-114f5a8aa75a_1900x1266.png%22,%22isProcessing%22:false,%22align%22:null})

What’s even more impressive for all you Postgres lovers is that DuckDB supports that wonderful COPY command, back and forth between DuckDB and Postgres.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/26416925-10c0-4cab-9295-fc3052c340d7_1766x424.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:350,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:106582,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://duckdb.org/docs/stable/extensions/postgres.html%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F26416925-10c0-4cab-9295-fc3052c340d7_1766x424.png%22,%22isProcessing%22:false,%22align%22:null})

Kinda hard to argue with that one. Little bit more code using DuckDB, but it is an option.

### Polars with Postgres and Delta Lake.

I mean I expect a lot out of Polars simply because it is Rust based and also made to act a lot like good ol’ PySpark, so we should have a simple and smooth option.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/fa639fb3-9511-40e6-ab7a-41c7d98f3784_1900x708.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:543,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:173320,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffa639fb3-9511-40e6-ab7a-41c7d98f3784_1900x708.png%22,%22isProcessing%22:false,%22align%22:null})

Of course Polars did not disappoint. [The DataFrame write\_database() option](https://docs.pola.rs/api/python/stable/reference/api/polars.DataFrame.write_database.html) pretty much mirrors Spark in it’s simplicity and implementation.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/91c73632-dd42-478c-b2af-afd00aae9ee4_2126x846.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:579,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:279195,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://docs.pola.rs/api/python/stable/reference/api/polars.DataFrame.write_database.html%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F91c73632-dd42-478c-b2af-afd00aae9ee4_2126x846.png%22,%22isProcessing%22:false,%22align%22:null})

Also, since Polars has such a seamless integration into Delta Lake, this one is a kind of a no brainer as well.

### The old fallback.

Of course you can fall back onto that old hunka-junka psycopg2 with plain old Python. One could read Delta Lake with any package, deltalake, polars, duckdb, daft, spark, etc … and simply collect the records as a Arrow table or Python list.

> From there it isn’t that hard to write a performant INSERT statement if you know what to do and what to reach for.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/d84a0a61-4b77-4e92-9243-8d18a36bfcc3_2126x1460.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1000,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:335339,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://www.confessionsofadataguy.com/performance-testing-postgres-inserts-with-python/%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/163175767?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd84a0a61-4b77-4e92-9243-8d18a36bfcc3_2126x1460.png%22,%22isProcessing%22:false,%22align%22:null})

This is probably much faster than many of the alternatives.