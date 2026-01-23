---
title: "Apache Arrow for the Database"
source: "https://dataengineeringcentral.substack.com/p/apache-arrow-for-the-database?publication_id=1224799&post_id=183096607&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2026-01-16
created: 2026-01-16
description: "ADBC Drivers"
tags:
  - "clippings"
---
### ADBC Drivers

![](https://substackcdn.com/image/fetch/$s_!FE-v!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbb5db293-c168-4f99-a16b-194351a099df_1024x1024.png)

Apache Arrow has been slowly sticking its fingers into every corner of the data world for the last few years. Today, we examine one of those dusty corners, namely, [database drivers built with Apache Arrow.](https://arrow.apache.org/adbc/current/index.html)

I suppose this makes sense, with Arrow being used up and down the stack for in-memory data, a [s the foundational building block for a myriad of tools.](https://dataengineeringcentral.substack.com/p/apache-arrow-is-eating-the-world)

![](https://substackcdn.com/image/fetch/$s_!zvja!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1a1c770f-da9e-4415-a436-77e50fd95127_2122x786.png)

Yeah, we live in a Lake House world, but relational databases are still the bread and butter of many a Data Platform, or at least a portion of the data storage and movement. Postgres ain’t going nowhere. [Heck, with the advent of Lakebase](https://www.databricks.com/product/lakebase), *its never-ending reign is pretty much set in stone now.*

> If I were to play the devil’s advocate for a minute, why would one even care about using Apache Arrow as a database driver?

- *Many tools already use Arrow; adding it at the database layer reduces friction and data copies/conversions.*
- *Arrow is fast as crap*
- *SQL support*

It seems beneficial only if one is already using an Arrow-based tool, but Arrow **database** drivers may be that much faster, making them worth using anyway.

Let’s look for the answer to this question by simply playing around with an Arrow database driver, pushing a bunch of data back and forth (*to and from the database*), and seeing what it’s like to use Arrow as a database driver in general.

---

### Python Arrow database driver with Postgres.

The easiest way to test this out is going to be using Python + Postgres to see not only if *the ADBC driver option* is fast, faster than other options, but generally speaking, **if it’s a pleasure to use.**

> *I’m only mildly interested in performance; I mean, fast is always lovely, but the aesthetics and developer “friendliness” of a tool are almost more important.*

- How does it install?
- What tools does it integrate with?
- What are the ergonomics?

It’s a little strange talking about an ADBC database driver in this context (if you’ve been around for the ODBC/JDBC nightmares), but nonetheless, onward.

So, let’s get to it. Data first.

Let’s gather [some 2025 data from the Divvy Bike Trips open source dataset.](https://divvy-tripdata.s3.amazonaws.com/index.html)

![](https://substackcdn.com/image/fetch/$s_!yUqS!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F057e4246-98e3-4e17-a821-4f91109ccc13_1536x382.png)

![](https://substackcdn.com/image/fetch/$s_!-kHn!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcbe84edc-fff4-4498-a21a-b3d5e4b61b7f_2088x404.png)

Very standard data, and we shall do a very standard thing with these files. Read them all and shove them into a Postgres database. This isn’t going to be a well-thought-out or bulletproof test, but more of an exploration.

We will compare Arrow’s ADBC driver with Python and DuckDB (non-Arrow) to just get a baseline.

- [psycopg2](https://wiki.postgresql.org/wiki/Using_psycopg2_with_PostgreSQL)
- Python ADBC driver
- DuckDB

> More than anything, I want to get a sense of what it’s like to use each tool to shovel data, generally what performance is like as well.

It’s “each to his own,” you may do as you please, but it’s better to know our options rather than be stuck in the same old stuff.

---

## The Code

Let’s dive into using Apache Arrow ADBC drivers to shove data into Postgres. We will use a local Docker instance for the database. Also, we will use PyArrow to read and prepare the data for insertion, and we will add timers only for the INSERT part.

> *[All the code is available on GitHub, along with a README if you want to follow along.](https://github.com/danielbeach/testingArrowADBCdrivers)*

We will only be inserting `4,758,124, so not much, but it will do.`

```markup
>> docker-compose up -d
>> uv run pyarrow_adbc_driver.py
Connecting to Postgres at localhost:5432/postgres...
Testing connection to Postgres...
✓ Connected successfully! Postgres version: PostgreSQL 16.11 (Debian 16.11-1.pgdg13+1) on aarch64-unknown-linux-gnu
Reading all CSV files from data/uncompressed...
Read 4,758,124 total rows from dataset
Creating table: CREATE TABLE "divvy_tripdata" ("ride_id" TEXT, "rideable_type" TEXT, "started_at" TIMESTAMP, "ended_at" TIMESTAMP, "start_station_name" TEXT, "start_station_id" TEXT, "end_station_name" TEXT, "end_station_id" TEXT, "start_lat" DOUBLE PRECISION, "start_lng" DOUBLE PRECISION, "end_lat" DOUBLE PRECISION, "end_lng" DOUBLE PRECISION, "member_casual" TEXT)
Inserting 4758124 rows into divvy_tripdata...
Insert completed successfully in 17.33 seconds (274,633 rows/sec)
Verification: 4758124 rows in divvy_tripdata
```

Of course, we aren’t sending anything over the wire, but still, over four million records in 17 seconds is very fast indeed. *[Remember, you can look more closely at this code on GitHub.](https://github.com/danielbeach/testingArrowADBCdrivers)*

![](https://substackcdn.com/image/fetch/$s_!lVhU!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9e3f04cb-8519-427b-9b18-34e9d742b3fe_1800x5734.png)

Really, if you get rid of all the fluff, the magic is in the simplicity of Arrow itself end to end, and also the ease of using the ADBC driver for Postgres.

![](https://substackcdn.com/image/fetch/$s_!uAh-!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2097c06b-16ce-466a-ad41-519f2aa029cb_1400x818.png)

Doesn’t get cleaner than that, \* **I think.**

Let’s try `psycopg2 without any Arrow, this probably isn’t the fairest test, but whatever. `[You can see the full code here](https://github.com/danielbeach/testingArrowADBCdrivers)`, but here is the core of it.`

```markup
Inserting 4758124 rows into divvy_tripdata_psycopg2_noarrow...
Insert completed successfully in 60.23 seconds (79,003 rows/sec)
```

![](https://substackcdn.com/image/fetch/$s_!lhbC!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2b11698e-2d6c-466c-8419-85d8cd2a3335_1800x1042.png)

If you are interested in reading more about `psycopg2 inserts, and performance, check out the below post.`

![](https://substackcdn.com/image/fetch/$s_!FCi9!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8cebe370-653a-475a-8c1d-783ed03d0c2a_1636x1074.png)

The previous 60 seconds were super slow, so let’s at least try to speed them up to appear non-biased in this review. Most people know that using COPY statements is a good way to get the bytes screaming.

![](https://substackcdn.com/image/fetch/$s_!F_jc!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9bbab1ea-bbb8-4d24-a0e5-437c4b6f4b4e_1800x1676.png)

```markup
Inserting 4,758,124 rows into divvy_tripdata_psycopg2_noarrow...
Insert completed successfully in 24.48 seconds (194,375 rows/sec)
```

Dang, down to 24 seconds. Still not the 17 seconds of the ADBC driver, ***and note the difference in code complexity between the two!*** Never underestimate code complexity or the importance of simple solutions.

> *Now out of curiosity we must use DuckDB to get a good baseline on how vanilla Python and ABDC Arrow drivers compare to that GOAT of Data Engineering tools, DuckDB.*

![](https://substackcdn.com/image/fetch/$s_!NYy1!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb699bfee-6073-4c31-806d-579f4baec38f_1800x3946.png)

Good Lord.

```markup
Insert completed successfully in 4.12 seconds (1,155,454 rows/sec)
Total rows inserted: 4,758,124
```

Holy Batman, that’s fast.

While we are at it, did you know that you can use Polars + the ADBC driver? [Check the GitHub repo for the full code](https://github.com/danielbeach/testingArrowADBCdrivers) … basically, it uses ADBC in Polars.

![](https://substackcdn.com/image/fetch/$s_!jR98!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F87dceb39-b4ab-4a41-992c-9765ba3bcb70_1200x596.png)

```markup
Inserting 4,758,124 rows into divvy_tripdata_polars...
Insert completed successfully in 22.18 seconds (214,534 rows/sec)
```

Not bad. Slightly faster than vanilla Python.

![](https://substackcdn.com/image/fetch/$s_!_ObB!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F858eb144-d7d1-49f6-a5b0-bed77f6f3d93_1188x726.png)

I mean, if we pretend DuckDB doesn’t exist, ADBC Arrow drivers are the best option, and don’t forget that the code was extremely simple.

---

## Thoughts

I think that Arrow, on the whole, is probably the future of a lot of Data Engineering; it already is at this point. The only reason it isn’t a “mainstream” conversation is that Arrow is used to build many tools underneath the hood, so it isn’t always obvious to someone that they are using Arrow.

> *I was excited to hear about the ADBC Arrow drivers for the databases.*

Pushing data to and from databases has always been a bottleneck in many data pipelines and processes. The idea of using Arrow in memory with certain tools, then pushing data back and forth across time-sensitive processes, is a great option.

In my play benchmark, ADBC drivers with Python beat out vanilla Python easily enough, but didn’t come close to touching DuckDB. Competition and options are good things in life, it will only push the data community farther, together, for the good of all.