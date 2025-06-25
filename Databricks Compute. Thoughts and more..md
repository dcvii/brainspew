---
title: Databricks Compute. Thoughts and more.
source: https://dataengineeringcentral.substack.com/p/databricks-compute-thoughts-and-more?publication_id=1224799&post_id=160284821&isFreemail=false&r=7br8e&triedRedirect=true
author:
  - "[[T50/Daniel Beach]]"
published: 2024-12-11
created: 2025-04-02
description: dollar bill 'yall
tags:
  - clippings
---
### dollar bill 'yall

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0fd581f5-f2cf-4a91-aa3d-88937a001d23_1024x1024.png)

There are two things certain in data engineering life: death and taxes, as well as S3 and EC2 (compute) costs. Both storage and compute costs probably make up 80% of most cloud bills for running a Data Platform, I imagine.

Regarding Databricks and compute, the ground shifts underneath you without anyone noticing it. Sometimes, we get stuck in a rut and simply ignore the goings on in the world of new features and “things” being released. We become blissfully unaware of our options and how we should use them to our advantage.

> *I don’t pretend to be a Databricks expert, and I need to remind myself to do my due diligence every year or so. Today, I will **review compute options inside Databricks** for the average semi-informed user.*

It will probably form a semi-coherent blob of half-wrong/half-right information regarding options around Databricks compute, **and how we might avail ourselves of some cost savings.**

*Thanks to [Delta](http://www.delta.io/) for sponsoring this newsletter! I personally use Delta Lake on a daily basis, and I believe this technology represents the future of Data Engineering. Check out their website below.*

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F708be49f-dfaa-498f-a862-8e9810a5fc58_600x123.webp)

If you and I come away with a clearer picture of compute options, when generally to use each, and possible cost savings or best practices … *that’s a win in my book*.

## Databricks Compute Options. (AWS point of view)

Let’s start with a simple, high-level overview of [general compute options for Databricks and their category](https://docs.databricks.com/aws/en/compute/).

- Serverless
- SQL Warehouse
	- both serverless and classic …
- Job
- All-Purpose

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc2c69df8-4746-4690-8517-efd526159e78_1770x1088.png)

> Instead of getting bogged down in the minute details of each compute type and agonizing over which one would save me three pennies over the other one ( *context is always key* ) … I generally stick to the big picture.

- ***Job compute at all times because it’s cheap.***
- ***SQL Warehouse only if you need to support on-demand analytics with third-party apps (like Tableau).***
- ***All-purpose for short-lived Notebook research, etc.***
- ***Serverless for a quick question you want an instant answer to.***

Try to keep it simple and keep to the obvious way of solving problems. A few nuances can either cost you or save you serious amounts of money.

- **Do not overuse All-Purpose compute**. If you are letting All-Purpose compute run for 8 hours a day so you can “do your job,” you are most likely wasting massive amounts of money.
	- If you have a Notebook that runs a query (or set of them), for more than 30 minutes. **Switch it over to a Job!**

It’s not that hard. If you \*NEED to run something in a Notebook, just go to t [he Workflows section of the Databricks UI and create a new Job](https://docs.databricks.com/aws/en/jobs/notebook), select your Notebook, etc., and you’ll save everyone money just like that. S *ee below*.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4ca7c2a5-c296-4071-9ec1-89d6aac296f6_2116x1256.png)

- Avoid Serverless most of the time; use it for short, quick needs that last only a few minutes.
	- There’s a lot of changing, including pricing with Serverless; it’s a black box and unclear when you should and should not use it. ***Be safe and stay away.***
- [If you use a SQL Warehouse](https://docs.databricks.com/aws/en/compute/sql-warehouse/warehouse-behavior), pay attention to what your Scaling looks like. *Do you really need three nodes running at all times?* Start as low as possible and work your way up.
	- Did you know you [can automate the starting and stopping of a SQL Warehouse](https://docs.databricks.com/api/workspace/warehouses/stop)? ( *what would happen if you shut it off between midnight and 5 am??? … you would probably save money, that’s it* )

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Feade3ed5-55fb-4ea1-b7e7-33893c156c50_2116x360.png)

### Besides the obvious, what can we do?

Ok, so what if you already know all about the different types of Databricks compute, and you generally use the right tool for the right job? Is there anything else we can do to lower compute usage and cost?

> *Again, I’m no Databricks savant, but here are a few ideas for you to think about.*

- [Understand the difference between](https://www.confessionsofadataguy.com/fleetclusters-for-databricks-aws-to-reduce-costs/) **SPOT** and **ON-DEMAND** instances, including **WITH FALLBACK**.
	- Almost 99% of Databricks Jobs should use **SPOT** or **SPOT WITH FALLBACK.**
	- [It’s not uncommon to save 80% when switching to SPOT clusters.](https://www.databricks.com/blog/2016/10/25/running-apache-spark-clusters-with-spot-instances-in-databricks.html)
- Use *[FLEET](https://www.databricks.com/blog/introducing-databricks-fleet-clusters-aws)* [Clusters](https://www.databricks.com/blog/introducing-databricks-fleet-clusters-aws) when you can.
	- it [auto-selects the best pricing](https://aws.amazon.com/blogs/apn/enhancing-availability-and-amazon-ec2-spot-utilization-of-databricks-workloads-on-aws/) and availability from a pool for you.
- Cluster re-use with Databricks Workflows.
	- “ [Databricks Workflows is a feature that allows for more efficient use of compute resources when running multiple tasks within a job leading to cost-savings.](https://community.databricks.com/t5/technical-blog/maximizing-resource-utilisation-with-cluster-reuse/ba-p/64331)”
- [Spend 5 minutes tuning your Clusters to the workload.](https://community.databricks.com/t5/data-engineering/performance-tuning-best-practices/td-p/33949)
	- You should, on a regular schedule, simply analyze all your Jobs that run on a regular basis and see if you can tune them to fit the workload better.
- [Turn your auto-shut-off settings on All-Purpose clusters](https://docs.databricks.com/aws/en/compute/clusters-manage#automatic-termination-1) to 5 minutes or less. It defaults to something like 45 minutes or something ridiculous.
- Make people share Clusters or SQL Warehouses for compute.
	- *Not everyone needs their own compute. Duh.*

I think we can stop there for now. That is a good overview of the very basic and most simple things we can do to control and understand Databricks compute costs.

Probably in real life, the answers are a little more nuanced and depend on what your environment looks like and the use cases that most heavily define your workloads.

Like most things in life, it’s the 80/20 rule; the easy stuff probably makes up 80% of the cost overruns or wasted compute that is happening today on your Databricks setup. People getting trigger-happy with their All-Purpose clusters and running them all day, with too many nodes to boot.

> *Make people pretend they are back in kindergarten, and tell them they can all share a Cluster … wouldn’t kill ‘em, and it will save some bucks.*

Overuse Job Compute, if that’s even possible. Turn termination time limits way down. Use **SPOT** everywhere and **FLEET** everywhere. To be honest, it is when we get sloppy and stop paying attention that we get in trouble. That’s when your bill starts creeping the wrong way.