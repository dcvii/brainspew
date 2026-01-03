---
title: 1TB of Parquet files. Single Node Benchmark. (DuckDB style)
source: https://dataengineeringcentral.substack.com/p/1tb-of-parquets-single-node-benchmark?publication_id=1224799&post_id=182238422&isFreemail=false&r=7br8e&triedRedirect=true
author:
  - "[[Daniel Beach]]"
published: 2025-12-28
created: 2025-12-28
description: Haters gonna hate.
tags:
  - clippings
  - duckdb
---
### Haters gonna hate.

![](https://substackcdn.com/image/fetch/$s_!hC1L!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fce8b8952-030a-486f-b759-c08e570e6416_1024x1024.png)

I give the people what they want; I’m a slave to clicks and the buzz of internet anger and mayhem. Not so long ago, I tried, with limited success, *to convince a legion of engineers who were raised on the Snowflake and Databricks teat*, that salvation lay right at their feet; all they must do is lean down and **put their hand to the plow.**

> When you’ve been doing what I’ve been doing (*writing whatever you damn well please*) for over a decade, the list of haters grows ever longer and longer. *Get in line pickles.*

A little stone tossed into the pond, where do the ripples go? Apparently, [my first article on the matter](https://dataengineeringcentral.substack.com/p/650gb-of-data-delta-lake-on-s3-polars) stirred the monsters in the deep. My mamma always told me, [haters gonna hate](https://www.linkedin.com/posts/ehsan-totoni-44928286_650gb-of-data-delta-lake-on-s3-polars-activity-7396999596201357313-glo-?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAACCGWeMBpzyTjCHWjac5iobhsbGE41GBhto).

![](https://substackcdn.com/image/fetch/$s_!4Zz2!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F68879f35-aeea-4b01-b1b5-c6705b46c3de_1658x700.png)

I mean, writing such things is the teaching of heresy in the inner circles of the **distributed devils** and **warmongers**, whose purse strings are tied **inextricably** to the masses of data engineering **peons** passing on their ***tithe in compute*** to the inner sanctum of the data illuminati bent on bringing me to account for my many sins.

- I’ve made many a power enemy for you, the 99%, yet here I am, still trudging along in the trenches to bring the good word to waiting converts. [Midwest boys raised on the river and in the woods](https://prairiemeditations.substack.com/p/grandma-house) don’t bow the knee very easily. [The Single Node Rebellion awaits you.](https://dataengineeringcentral.substack.com/p/the-single-node-rebellion?utm_source=publication-search)

![](https://substackcdn.com/image/fetch/$s_!BKCF!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc24b5b2e-618a-4dab-8a4e-57204efc7c26_1300x558.png)

---

## Generating 1TB of Parquet files with Rust.

I’ve got nothing much else today on this wonderful holiday break besides oiling my muzzleloader and waiting for deer season to start, just as well [break out cargo and spin up some Rust.](https://github.com/danielbeach/rustGenerate1TB)

Head over to the [GitHub repo](https://github.com/danielbeach/rustGenerate1TB) and see for yourself.

![](https://substackcdn.com/image/fetch/$s_!bIUQ!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F60e7b989-d831-469f-adf8-d6354d458cc2_2066x694.png)

I went ahead and generated 1 TB of data and put it into an S3 bucket using the above Rust code.

![](https://substackcdn.com/image/fetch/$s_!hFx-!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0f86a90d-b5cd-42d6-b55e-a31188355ca7_1600x708.png)

![](https://substackcdn.com/image/fetch/$s_!DwQi!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F819119b5-7b7f-4ed7-b1c5-05f9214dda5f_2420x700.png)

And the schema generated is straightforward.

![](https://substackcdn.com/image/fetch/$s_!efGR!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff2acab62-5a5e-4192-89fc-ac9ee4084427_2400x1116.png)

- *transaction\_id*
- *datetime*
- *customer\_id*
- *order\_qty*
- *order\_amount*

> We should be able to run a straightforward SQL query to piddle with this **1TB of data** and see what gremlins, or not, we can sus out.

Many sorry saps, complainers, anons, milk toast programmers, and the like, where complaining in my last benchmark that I didn’t *FORCE* the tools to use every single column and gulp the entire dataset … (*why wouldn’t you, that doesn’t happen in production*), but to shut the dirty mouths of all those goblins, **our query will include every single column of the dataset.**

- Using [Linode](https://cloud.linode.com/dashboard), we will spin up LittleStinker (*named affectionately after all my haters*)

![](https://substackcdn.com/image/fetch/$s_!jLtM!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdcf5aa68-691c-4a5c-836c-a21415374840_1532x532.png)

Hold your breath: a gigantic **16 CPUs and 64 GB of RAM**. We are going to light ‘er up, make ‘er burn red hot.

```markup
>> curl -LsSf https://astral.sh/uv/install.sh | sh
>> uv init stinkers
>> cd stinkers
>> uv add duckdb pyarrow boto3
>> nohup uv run main.py > script.log 2>&1 &
```

Let’s get to the simple code.

---

## DuckDB gobbles 1TB of Parquets in S3.

If anyone can do this deed, it’s [DuckDB](https://duckdb.org/), our feathered and weathered friend of SQL. Why pick [DuckDB](https://duckdb.org/)? Well, we need something that won’t blow up memory, of course, and DuckDB allows us to do two things …

- *spill to disk as needed*
- *set MEMORY limits*

> *There is nothing really complicated about this code at all, simply normal DuckDB with the added local disk spill crud and setting the memory limit at 50GB.*

![](https://substackcdn.com/image/fetch/$s_!foUa!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff184ab5d-24c8-42de-a86e-a7d768b79c15_1600x2458.png)

This is part of the attraction. Before we get to results, the more important part that many engineers seem to miss … is the simplicity of this architecture.

- *No Spark clusters, no complicated installs, dependencies, or JARs, no backflips to use Apache Commet with some JAR to speed up Spark, no Docker images needed.*
```markup
There is not only real cost savings here in terms of compute ... a single 64GB node vs some oversized cluster at a very high-priced charge. There is real savings in complexity and architecture.
```

It’s hard to imagine anything simpler than a single EC2 instance, or whatever compute, with two extra requirements …

- uv or pip
- [DuckDB](https://duckdb.org/)

There is no free lunch. I say this as someone who relishes using big-data platforms on Spark that gobble up whatever you throw at them. But it comes at a cost, both real and otherwise.

![](https://substackcdn.com/image/fetch/$s_!8VBM!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F26c4d3b0-68a9-4333-88a2-174a32d63aae_1432x690.png)

The hidden cost of using distributed systems for everything is more than just the large compute bill at the end of the month. Complexity, complexity, complexity, it spills out into every part of the data stack, from top to bottom.

Everything becomes complicated “with scale,” no matter how hard they try to hide the pea under the mattress. The truth is that ***less code == fewer bugs*** (generally). The truth is that ***simple*** ***infrastructure == fewer problems***.

I’m not saying you CAN’T use those platforms. **I’m saying some of you DONT HAVE TO**.

There are simple options, such as DuckDB and a reasonably sized Linux instance. Literally, a 3- or 4-line install later, there is nothing left to do but work on the data.

---

### Results

DuckDB does just what we tell it to do with that 1TB of parquet data in S3; ***it makes that Linode 64GB instance sing a song of joy—sitting around 48GB of memory used while in the thick of it.***

![](https://substackcdn.com/image/fetch/$s_!aibF!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb5d2af12-01d0-4a04-a8b5-ec77e78b0b8b_2000x520.png)

Heck, we aren’t really tuning anything either. I’m sure there’s work to be done, but it’s the holidays, and we're lazy.

> *Here is what you’ve been waiting for, probably, ignoring all my comments about the existential questions of overall data platform design with a focus on simplicity.*

![](https://substackcdn.com/image/fetch/$s_!YjRA!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F43ec39ce-fdfa-4e3e-98b5-f1defc2e2e17_1600x670.png)

**A little less than 20 minutes.** Of course, it wrote out the results to the CSV file as well.

![](https://substackcdn.com/image/fetch/$s_!uYwB!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff5876c10-1a49-4e5d-a5e8-25f4b0896ee3_1440x616.png)

I don’t see why we couldn’t keep cranking up the data sizes as well. I’m sure nothing would change but the runtimes. Most of ‘yall ain’t crunching a literal TB in a single query anyway.

> *What do you think, DuckDB is the only tool that can do such black magic? Not so.*

## Daft gobbling 1TB of Parquet files in S3.

The truth is, there are plenty of tools that can do this (*besides Polars … more to come on that later; it failed this task*). We live in a C++ and Rust world where single-node data frameworks are the new law of the land, many of which are more than capable of crunching large datasets.

[Daft is one of those Rust-based tools](https://docs.daft.ai/en/stable/) that doesn’t get enough love. It’s always fast and straightforward.

![](https://substackcdn.com/image/fetch/$s_!yM7L!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3c8a816d-ef19-4830-b275-3b93ca65e284_1600x2122.png)

If you are interested in both the DuckDB and Daft code (*I’d be curious to know if you can make it run faster*), [you can find it on GitHub.](https://github.com/danielbeach/duckdbAndDaftEat1TB)

![](https://substackcdn.com/image/fetch/$s_!jdcT!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F98728620-c61f-4581-ae87-008ec785193a_2084x698.png)

Daft appears to be much slower than DuckDB, but it's probably my fault; who knows? ***Under 30 minutes for 1TB on a single node, no complaints at the end of the day.***

![](https://substackcdn.com/image/fetch/$s_!Xgma!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe67bb6c2-202c-4cdf-9907-4b0118f00bb7_1600x708.png)

---

## What’s the problem, bruv?

I still don’t get it; it must be some distributed brain rot that is connected to money, fame, fortune, who knows … that causes people to fight against this so hard. *Maybe it’s just the folks who have Panda’s brain or something.*

> *Ignoring the fact that we are living in the age of swift and capable single-node processing frameworks is like burying one’s head in the sand. Polars, DuckDB, Daft … these tools are going nowhere and will continue to be widely adopted as time goes by.*

![](https://substackcdn.com/image/fetch/$s_!m7kz!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F50dc9d88-2cc3-40a3-93a7-c1f2e8f426e2_1600x558.png)

Maybe old habits are hard to break, new patterns of thought and solutions can be complicated to adopt once you’ve tread the same path year after year.

- A little open-mindedness to consider alternative approaches and solutions is what drives innovation and success.

It’s clear these tools and scale way beyond what we did today. I’m trying to make a conceptual point that apparently is hard to swallow for some. **Either way, haters gonna hate.**

You, friend, be a healthy learner: *always consider all options, push things to the edge, and never take no for an answer. The future is bright and full of interesting things; never forget to turn over the rocks and see what’s underneath.*

Ignore the smart, pretentious, loud, doubters, haters who lurk in the shadows and suck all joy and life out of all that is good in this data life we live.

<iframe src="https://www.youtube-nocookie.com/embed/8NvwEToKJcg?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen="true" width="728" height="409"></iframe>