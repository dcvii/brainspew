---
title: Review of Data Orchestration Landscape
source: https://dataengineeringcentral.substack.com/p/review-of-data-orchestration-landscape
author:
  - "[[T50/Daniel Beach]]"
published: 2024-12-11
created: 2025-04-06
description: ... and honest one ...
tags:
  - clippings
---
### ... and honest one...

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6cf83f4d-3e83-45d0-9fbf-eff22842c7d5_1536x1024.png)

Sometimes, I force my old caveman self to do things I do not want. Believe it or not, reviewing the landscape as it relates to data orchestration frameworks is not something on the top of my list. People, including me, have their own pet favorites when it comes to orchestration platforms, and it’s hard to be unbiased.

> *Does it matter what tool you choose? If it works, it works; if it doesn’t, it doesn’t; it’s not like we don’t have a plethora to choose from.*

Either way, I suppose something like this could be helpful for those new to the Data Engineering world or those looking to build greenfield projects or migrations.

One of the most distasteful aspects of comparing tooling, in this case, orchestrators, is the desire of folks to simply get a side-by-side list of features. ***Different tools are good at other things, and a simple side-by-side checkbox list is usually misleading.***

Whatever, I’m not sure how to compare different orchestration tools, but I want to cover the high-level things. Then, I’m assuming you will “gravitate” towards one or the other based on your needs. That should be good enough for both of us.

*Mostly, I want to provide an unbiased comparison without any marketing drivel blocking the way.*

***Thanks to [Delta](http://www.delta.io/) for sponsoring this newsletter! I personally use Delta Lake on a daily basis, and I believe this technology represents the future of Data Engineering. Content like this would not be possible without their support. Check out [their website](http://www.delta.io/) below.***

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F708be49f-dfaa-498f-a862-8e9810a5fc58_600x123.webp)

Now that we are done with that business let’s get down to it.

## Orchestration Tooling Options

We should probably start at the top, simply listing our options, good and evil; I’m sure I will forget someone’s favorite, but so be it. Also, it’s hard to know where to draw the line, so to speak; some tools are pure orchestrators, and some are bent more toward data processing but act as orchestrators.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F60fa134a-2610-4b32-8008-0f399fd35f98_1670x878.png)

- [Apache Airflow](https://airflow.apache.org/)
	- AWS MWAA
	- GCP Composer
	- Astronomer
- [Dagster](https://dagster.io/)
- [Prefect](https://www.prefect.io/)
- [Mage](https://www.mage.ai/)
- [Metaflow](https://docs.metaflow.org/introduction/what-is-metaflow)
- [Flyte](https://flyte.org/)
- [Databricks Workflows](https://www.databricks.com/product/data-engineering/workflows)
- [AWS Step Functions](https://aws.amazon.com/step-functions/)
- [Luigi](https://github.com/spotify/luigi)
- [Kestra](https://kestra.io/)
- [Argo](https://argoproj.github.io/)
- [Orchestra](https://www.getorchestra.io/)

Another great way to make people angry and break up the playing field into something more manageable is to break the entire group up by open source vs. not … ***this is a crucial distinction when thinking about options***

> There are technically three different types of tools, like it or not. I expect to hear some pushback, and talking heads take me to task on this, but whatever.

- Closed ( *100% SaaS* )
- Semi-Open Sourced ( *Both Managed (paid) and some open-source* )
- Open-Source

As Data Engineers and Data Platform builders, we must know whether any tool we use, including these orchestration tools, is a semi-open source**.** What I mean by that is … do the parties that control the “open-source” GitHub also offer it as a paid service?

> This can be both a good AND a bad thing. We have to be realists; we live in a world filled with humans who do human things. **Will the best features be reserved for the paid versions? Will they pull the rug without warning?**

Pretending like this stuff doesn’t happen is naive and dangerous. I don’t know if this is 100% correct, but here is my take on it. ( *Everything under the Open/Closed category appears to be offered by the makers as a paid/hosted product* ).

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F969e2027-43c4-4774-821d-99e8aacc02f9_1672x1054.png)

Sure, some companies take the open-source part more seriously than others, and you can run their tooling yourself and get the best features, but you can’t, or you get the rug pulled at some point. **You should just be aware of where things stand.**

## How to compare Orchestration Tools

Before we can compare and contrast some of these tools, we should cross some off the list. Before you light your torches and grab the pitchforks, hear me out.

> *If we’re here to pick out a new tool, you start by finding out which tools won’t work for most folk.*

How can we do this? Here are some criteria.

- Small community and not widely used ( ~~cross it off the list~~ )
	- ***unless you’re feeling spicy, we don't pick immature tooling.***
- We want full-feature tools, not those operating on a narrow fringe.

Anything else is fair game, although we will review other vital needs later. Based on the above, let’s cross a few off the list.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0e3fb49a-dae8-437e-81a9-34f33438d34c_1672x1054.png)

Why did I cross off metaflow, luigi, argo, and aws step functions? Because they are either too narrow or simply not widely used enough to have a thriving community.

- [metaflow](https://metaflow.org/) has been growing a lot, but it is more focused on data science and ML workflows and hasn’t been around long enough.
- [argo](https://argoproj.github.io/) is made to be run with Kubernetes; although popular, it’s too narrow in implementation.
- [Luigi](https://github.com/spotify/luigi) has been around for some and does get used, but has lost out to other tools for good reason.
- [AWS Step Functions](https://aws.amazon.com/step-functions/) just aren’t fully featured enough, and it’s totally closed source.
	- *if you think that’s not a problem, go read about what happened to AWS Data Pipeline.*
- Orchestra - just strange mix of open-source and paid.

Again, when picking between tools, we have to make cuts somewhere; these guys just didn’t make the cut.

Just because I’m curious I want to look at two stats on GitHub for all these tools so we can see them side by side, GitHub Stars ( *which means less and less these days* ), and Open Issues ( *this is a stronger indication of usage* ).

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F83ad8af0-1ee4-4794-800d-57312b074a9d_1188x744.png)

Ok, based on this I think we can cross some more off the list, it’s a brutal world we live in uh? Sorry if you’re favorite is getting the boot.

- flyte appears to be low usage in comparison to our other options.
- Kestra strangely has a lot of stars (??) but appears to have little usage based on issues. Also, [some recent notes on reddit](https://www.reddit.com/r/dataengineering/comments/1hmfxrg/airflow_vs_kestra/) indicate the OSS version isn’t full featured and lacks community support.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F41c7b40a-945d-4b29-8cfd-45129501e360_1360x640.png)

This is the sort of thing we talked about in the beginning, and need to look out for. **That brings us down to the mighty 4.**

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa939c4e0-4843-4244-bd93-f373903907a7_1674x1116.png)

We are left with …

- Prefect
- Mage
- Dagster
- Airflow

Honestly, I’m not surprised, that is where I would expect to end up, if you work in the Data landscape, these tools are not unfamiliar to you. In my opinion, that means we are doing our review correctly.

**If you think about it, this is really the single behemoth, Apache Airflow, vs the upstarts tying to get a piece of that action.**

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa36ce656-fd91-4f1f-9829-6c60d60b4cfa_1564x516.png)

> Now my intention isn’t to give you a how-to on each one of these tools, but let’s take a look at how to operate and their core concepts so YOU can get an idea of which tool resonates with YOU more.

***In the end any of these tools you chose, if they work for you, is fine.***

## Concepts

Now, I’m no expert in all these tools, I just know how to read documentation and draw conclusions. I’ve read the documentation for these tools and come up with some thoughts to help us understand **The Big Four**.

> *It’s clear that these tools approach Workflow Orchestration from different perspectives, which makes sense, they are different tools, no surprise there.*

- **DAG-based approach**
- **Code-centric based approach**

Both Airflow and Dagster focus on the DAG as an abstraction to write and orchestrate your needs. ***Mage and Prefect focus on more on code and the integration between code and the workflow is tight, not as much abstraction.***

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc26b9098-baeb-465c-afe4-2cadf85491f6_1564x632.png)

To help that idea sink in, here is an example, from their own docs, of a Workflow/DAG for each tool so you can see what I mean.

### Airflow

[DAG example.](https://airflow.apache.org/docs/apache-airflow/2.2.3/_modules/airflow/example_dags/tutorial.html)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbe322f69-5732-4f3c-b0fc-11510cacf17e_2000x2458.png)

### Dagster

[JOB example.](https://medium.com/@antongw1p/navigating-data-workflows-with-dagster-exploration-for-beginners-f92bf07c2cc6)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc7d00865-7380-4a41-9a65-88fcc5ee77c5_2000x1414.png)

Just as a side note, Dagster sorta rides the rail between Airflow classic DAG setup and code centric approach. But, they look awful similar don’t they?

### Mage

[Pipeline example. (Mage uses Notebooks for code).](https://www.linkedin.com/pulse/building-simple-data-pipeline-mage-beginners-guide-sheharyar-amir-trzuf/)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd2e8c670-bf0a-4e43-bb92-2c4c38772abd_2000x2606.png)

### Prefect

[Pipeline example.](https://docs.prefect.io/v3/tutorials/pipelines)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F908d6351-96c2-4660-aae0-35f6e141cc8b_2000x2122.png)

What do you notice about Prefect and Mage? The are code centric and use decorators to build out pipelines.

### Core concepts of Mage.ai …

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa1d9f60b-8cc1-49ce-8399-42412046b9aa_2598x958.png)

#### Pipeline

- A pipeline contains references to all the blocks of code you want to run, charts for visualizing data, and organizes the dependency between each block of code.

#### Block

- A block is a file with code that can be executed independently or within a pipeline. Together, blocks form a Directed Acyclic Graph (DAG), which we call pipelines.
- There are 8 types of blocks …  
	*Data loader, Transformer, Data exporter, Scratchpad, Sensor, dbt, Extensions, Callbacks.*

### Core concepts of Prefect…

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F36ad87b8-a0ce-495e-a039-3d154a8a215d_2598x958.png)

#### Flows

- A Prefect workflow, modeled as a Python function.

#### Tasks

- Discrete units of work in a Prefect workflow.

#### Results

- The data returned by a flow or a task.

Similar concepts, but that is not a surprise, anyone building a workflow orchestration tool with Python would expect something similar. There is only so much abstraction that can be done.

### What do people say about these tools in the wild?

***Mage …***

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0ce5608c-eb49-445f-ac93-37a0c8910867_1408x632.png)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F31e900c7-51cc-4806-8053-5efcb20d6dd1_1408x350.png)

***Prefect …***

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F13816742-fc9f-4b8c-afb5-30275c4b8c50_1408x338.png)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4e4f7fb0-44a3-48a6-95dd-d46a0fbf55ef_1392x482.png)

### We should probably talk about Dagster.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F85a2b69e-da43-4e1d-9c68-424641d3bede_2598x894.png)

We haven’t given Dagster much attention yet, but we probably should, since it’s one of The Big Four.

#### Dagster Concepts

#### Asset

- An `asset` represents a logical unit of data such as a table, dataset, or machine learning model. Assets can have dependencies on other assets, forming the data lineage for your pipelines.

#### Graph

- A `GraphDefinition` connects multiple `ops` together to form a DAG. If you are using `assets`, you will not need to use graphs directly.

#### IO Manager

- An `IOManager` defines how data is stored and retrieved between the execution of `assets` and `ops`. This allows for a customizable storage and format at any interaction in a pipeline.

#### Job

- A `job` is a subset of `assets` or the `GraphDefinition` of `ops`. Jobs are the main form of execution in Dagster.

#### OP

- An `op` is a computational unit of work. Ops are arranged into a `GraphDefinition` to dictate their order. Ops have largely been replaced by `assets`.

***What are people saying?***

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7322d274-67e6-4f81-8280-30b43d5ea8ba_1392x678.png)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F95c7ff5f-2579-41fa-9ec7-065621dd5ee8_1400x388.png)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc4f46cf2-b23d-454d-90a1-ea246b373bf7_1400x870.png)

## More Thoughts.

It’s my personal opinion that Apache Airflow is the go to for orchestration only, **in the most classic sense of the word**. It’s the 500lb gorilla in the room that has a massive community, lots of integrations and is “easy” to use. *Easy to use in the sense of a massive community, a tutorial covering anything you could dream up exists somewhere.*

**But, it’s just that. Orchestration.**

Anytime you wander into use cases that actually call for the manipulation and processing of data ON that orchestration platform, as your primary use-case, you will find a better solution in Prefect, Dagster, or Mage.

Which should you choose, Prefect, Dagster, Mage? **How would I know?** You need to use them and test them against your main use case, only that will answer your question.

> Speaking of integrations, we should poke at a minute, because that is one of the MAJOR selling points of Apache Airflow. Because of its wide usage and community, it has simply and to use integrations for everything under the sun, which makes life easy in the Modern Data Stack.

[Dagster appears to have, on the surface every kind of integration one could image.](https://dagster.io/integrations) AWS and all its services (s3, EC2, etc, etc). Databricks, DBT, DuckDB, Kubernetes, Snowflake, Tableau, etc.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7228c444-1a29-458d-bae2-351a75c39750_2606x1252.png)

Mage integrations appear to be wide, but maybe not as all inclusive as Dagster? ***In their own documentation in integrations they don’t even list Databricks.*** It lists AWS s3 but not EC2, etc. Again, what do I know, just going off what they tell me.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F597d0525-94e2-4eff-a1f9-25994e36f6b6_2414x1014.png)

What does [Prefect list](https://docs.prefect.io/integrations/integrations)?

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F441210cb-aa96-4f89-8dc4-ecd0a453edc0_2414x1114.png)

[The Prefect list of integrations](https://docs.prefect.io/integrations/integrations) isn’t huge, but it does appear to cover all the big stuff, Snowflake, AWS, Azure, Databricks etc.

> *We don’t need to go over Airflow integrations because they are as far and wide as the sea.*

## The end of it all.

To be honest you could simply list every feature of all these orchestration tools side by side, but you will most likely only find that in marketing content. The truth is that picking an workflow orchestration tool is a complex task and requires a lot of nuance.

> *That nuance usually involves the specific use case of a Data Platform. For example, I crossed of Argo early on during this discussion because it was solely focused on Kubernetes. But, I’m sure there are many teams (even mine a few years ago), that mostly work on Kubernetes and would benefit greatly from Argo.*

At the end of the road we should NEED a reason to stray off the beaten path. The beaten path in this case being …

- **Apache Airflow**
- **Prefect**
- **Dagster**
- **Mage**

One should probably also simply start with Airflow or one of it’s SaaS versions, [AWS MWAA](https://aws.amazon.com/managed-workflows-for-apache-airflow/), [GCP Composer](https://cloud.google.com/composer?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-skws-all-all-trial-e-dr-1710134&utm_content=text-ad-none-any-DEV_c-CRE_665665942528-ADGP_Hybrid+%7C+SKWS+-+MIX+%7C+Txt-Data+Analytics-Cloud+Composer-KWID_43700081227765919-kwd-427702736595&utm_term=KW_cloud%20composer-ST_cloud+composer&gad_source=1&gclid=CjwKCAjwzMi_BhACEiwAX4YZUGVxKBIqKfjzvKjZCbGxmRCZCvh5tpOqchGiMrLj-WuLi7jCY5WxfBoC8pkQAvD_BwE&gclsrc=aw.ds), or [Astronomer](https://www.astronomer.io/pricing/?utm_term=astronomer%20io&utm_campaign=brand-lg&utm_source=adwords&utm_medium=ppc&hsa_acc=4274135664&hsa_cam=21865965763&hsa_grp=169329542789&hsa_ad=720266268904&hsa_src=g&hsa_tgt=kwd-2267742422584&hsa_kw=astronomer%20io&hsa_mt=p&hsa_net=adwords&hsa_ver=3&gad_source=1&gclid=CjwKCAjwzMi_BhACEiwAX4YZUC0i2nhGA1CkWKJ5s_ViqcQzAcuiKkivP5kKbEOl_WvSgz4aRJXUuxoCV-YQAvD_BwE). It will most likely cover most use cases. **But, there are aways the brave few looking to push the edges and boundaries of what’s possible.** For these, something like Prefect, Dagster, or Mage are the order of the day.

> Everyone is probably asking which one is “better,” Mage, Prefect, Dagster. That’s like asking what is the best cloud platform like AWS, Azure, or GCP. ***There is no REAL answer to that other than you can make each platform what you make of it.***

Many successful and large Data Platforms are run on AWS, Azure, or GCP. Many data teams use Dagster, Prefect, or Mage to great effect. It’s more about the team’s needs and their execution rather than the specific tool.