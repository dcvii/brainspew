---
title: "Building a DuckLake ... Open Source Style."
source: "https://dataengineeringcentral.substack.com/p/building-a-ducklake-open-source-style?publication_id=1224799&post_id=180551944&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2025-12-22
created: 2025-12-22
description: "behold"
tags:
  - "clippings"
---
### behold

![](https://substackcdn.com/image/fetch/$s_!2QG6!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F97893564-439d-4346-896d-b2d882c15392_1024x1024.png)

I am sort of an addict for a good Lake House; it’s just an incredible architecture that is a joy to build and use daily. No more SQL Server or Oracle, you know what I’m saying if you were born in the right decade.

Truth be told, at this point in the Modern Data Stack lifecycle, you pretty much have two major Lake House storage layers that dominate the landscape: Iceberg and Delta.

> *I was surprised when DuckDB/MotherDuck threw their hat in the ring with DuckLake. Didn’t see that coming at the time.*

![](https://substackcdn.com/image/fetch/$s_!lhJh!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F477d6a0a-df62-4949-a67f-1e1f8b766b0f_1672x700.png)

Like anything done by DuckDB, it’s always top-notch and for a good reason. They have a knack for doing things right. Ever since I wrote that first article, *I’ve been meaning to return to DuckLake and try it out in a more open-source setting again.*

> *What I mean by that is can I use maybe a RDS Postgres instance and back DuckLake on AWS S3.*

I mean, if someone is actually looking to use DuckLake in the open as a viable alternative to Iceberg and Delta Lake, then that is the game.

***Checkout today’s sponsor*** [Carolina Cloud](https://carolinacloud.io/)

*One-click notebooks, genomics tools, and Ubuntu VMs at 1/3 the cost of AWS with no egress fees*

![](https://substackcdn.com/image/fetch/$s_!IC2g!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F64ba35a1-edb6-413f-9dc4-3247e9935295_1254x588.png)

**If you enjoy Data Engineering Central, please check out our [sponsor's website above](https://carolinacloud.io/). It helps us a lot!**

---

Also, since it’s been a while since I’ve looked at DuckLake, one telling note we will look for is: has there been any adoption of frameworks in the broader data community? Aka, can I read DuckLake with Polars, Daft, Airflow, whatever?

![](https://substackcdn.com/image/fetch/$s_!tEQP!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F61c0428f-31f1-45be-a6a2-2b21048e7f9d_1400x520.png)

---

### Simple Review of DuckLake

Again, there are better places than here to l [earn about DuckLake in depth](https://thefulldatastack.substack.com/p/tech-review-ducklake-from-parquet). That’s not my focus today, as usual, I want to simply throw a problem at the DuckLake architecture, turn over a few rocks, and see what crawls out.

![](https://substackcdn.com/image/fetch/$s_!fobU!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd8d82b50-3469-4e04-b72c-d2085e0635ef_1144x509.png)

DuckLake is built on simplicity, of course, and that appears to be one of its main features.

- Built on top of parquet
- SQL database for catalog/metadata

Of course, they will give you a myriad of other reasons to use DuckLake, but at the end of the day … simplicity.

![](https://substackcdn.com/image/fetch/$s_!S0eH!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F195af55a-0884-4666-a1ed-f1c8372f506a_2392x778.png)

[As I wrote before,](https://dataengineeringcentral.substack.com/p/duckdb-enters-the-lake-house-race?utm_source=publication-search) this seems to be one of the main differences between say DuckLake and Apache Iceberg. Below is the concept visually, no more hosting a complicated Catalog.

![](https://substackcdn.com/image/fetch/$s_!jJ75!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcbd99103-0726-4df0-8609-c97895b0bf42_1752x1160.png)

DuckLake lets you use pretty much any SQL database as the metadata and catalog. Easy. That’s the point. No spinning up an instance to host some heavy catalog, or worse yet, having to pay for SaaS Catalogs.

This lowers the barrier to entry.

---

### Setting up DuckLake on AWS (S3 + RDS Postgres)

There is no time like the present, so let’s dive in and see if we can get DuckLake up and running on an AWS setup, far away from that feathery MotherDuck, *to see if indeed DuckLake is open-source-worthy.*

> *Either it will be easy and boring, or it will be bumps in the night.*

We need two things to make this work, **in true open source style.**

- RDS Postgres instance.
- S3 bucket.

![](https://substackcdn.com/image/fetch/$s_!2Dlh!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F349435b5-780e-4456-9f83-3e3e9882d92e_779x164.png)

We can use my gigantic and massive RDS instance, which I use for various sundry projects, a mighty **db.t4g.micro**. That little blighter costs me like *$.50* per day to run.

![](https://substackcdn.com/image/fetch/$s_!sHCn!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff9f71e04-7222-4648-938d-2152df0b3714_670x429.png)

Also, we will attempt to use my S3 bucket, ***s3://confessions-of-data-guy,*** as the data path for DuckLake to store the parquets it generates.

- *In theory, this DuckDB/DuckLake command will look something like this.*

![](https://substackcdn.com/image/fetch/$s_!JOZ8!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2430cb21-1fb0-407b-96dc-81ca69bb896f_1700x670.png)

Of course, I will have to ensure that AWS credentials are available and that Postgres is available for DuckDB. Hold onto your seatbelt, Rita, here we go.

![](https://substackcdn.com/image/fetch/$s_!JbsS!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F52af6566-31c1-4500-ab60-cdcf4bb9e162_1700x3352.png)

A lot of code, but it appears to run fine with UV.

![](https://substackcdn.com/image/fetch/$s_!9e50!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F925c40d3-6867-4ed3-bcf8-b0ae01f9e38e_723x106.png)

Well, that was dissapointly easy. I know you all come here from the mess and mayhem. Not today, at least not yet. Let’s get some of that [Divvy Bike trip data from the ole’ iterwebs](https://divvy-tripdata.s3.amazonaws.com/index.html), and see if can shove that data in there.

![](https://substackcdn.com/image/fetch/$s_!Aa4w!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe7dae88c-9f30-4cac-842a-a5e35f736b0e_944x221.png)

After munging the code a bit, this seemed to work like a charm.

![](https://substackcdn.com/image/fetch/$s_!avPT!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1f5c6548-9b72-48f4-8b04-410b4fff6ceb_1700x5586.png)

> *Heck, to make sure I wasn’t hallucinating, I checked S3 and can see the files written there for our DuckLake.*

![](https://substackcdn.com/image/fetch/$s_!hjVo!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc92d4f5c-a3b4-4e26-bf75-4cd62d08da18_2642x1082.png)

They are there, and the results of those sample queries appear to be running fine.

![](https://substackcdn.com/image/fetch/$s_!2UgS!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff640b910-a228-40d9-ad8e-d4c01ba2fd63_510x632.png)

Please leave it to DuckDB and MotherDuck to make this a boring article, those little rats. They could have made me try a little bit harder, you know? Indeed, DuckLake is a valid Lake House option in the open source world if you’re looking for a lightweight option.

> *Don’t get no lighter than that. No Big A$$ catalog needed here.*

If you want to do this yourself, [all the code is available on GitHub.](https://github.com/danielbeach/DuckLakeonS3andPostgres)

![](https://substackcdn.com/image/fetch/$s_!gARq!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb3b285ea-050c-40f0-94a0-d4bc1fced5ba_2002x850.png)

---

### More thoughts on DuckLake

That went better than I expected, although I should have learned my lesson; DuckDB rarely gets anything wrong, and the same applies to DuckLake. You never know how a tool will react to trustworthy open source. *I enjoyed the fact that I could use an RDS Postgres database for the metadata and a random S3 location for the data storage.*

> *What remains to be seen is whether MotherDuck and DuckDB will push for first-class support in other popular tools, such as Polars and Daft.*

It looks like some of this is already underway, but time will tell whether it keeps chugging forward.

![](https://substackcdn.com/image/fetch/$s_!8Uhm!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3bd9a39d-ccf5-4eb3-a2c6-b5c1053714cd_1756x580.png)

It’s hard to imagine anyone giving Delta Lake and Apache Iceberg a run for this money. Still, with Data Catalogs now and in the future heavily integrated into those tools, there might come a day when people have had enough and look for an easier option, DuckLake being one, as long as it has broad tooling adoption.