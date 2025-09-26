---
title: "Honest review of MotherDuck"
source: "https://dataengineeringcentral.substack.com/p/honest-review-of-motherduck"
author:
  - "[[Daniel Beach]]"
published: 2025-09-22
created: 2025-09-22
description: "pluck em' feathers"
tags:
  - "clippings"
---
### pluck em' feathers

![](https://substackcdn.com/image/fetch/$s_!g0Ju!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F02515ee1-5ece-468d-a652-1c8c9b5280ad_1328x596.png)

Well, I enjoyed my recent review of Polars Cloud so much that I figured I would keep the streak going, you know, like your grandpa said, “Strike while the iron is hot.” With such a thing fresh in our mind and on our fingertips, I thought to myself, what about that DuckDB and MotherDuck, why not taste of that fruit as well.

> *So here we are again, today, not so much to review DuckDB, with which we are all familiar, but to pluck a few feathers from that MotherDuck and stick them into our hunting hat.*

Similar to Polars Cloud, I’m really not interested in performance, but just generally, how good of a job has MotherDuck done providing DuckDB as a service (**DaaS)??**

What am I looking for? I’m unsure, but at least …

- ***Onboarding experience***
- ***UI experience***
- ***Easy of development and deployment***
- ***Concepts***
- ***Documentation***
- ***Integrations, etc.***

In short, in the Era of Databricks and Snowflake, what is MotherDuck offering as far as developer experience.

---

## Attention!

Because you’re all cheapskates and I spend my hard earned money burning AWS and Databricks compute for you ungrateful hobbits, [I’m offering 50% OFF a Yearly Subscription](https://dataengineeringcentral.substack.com/0bb7a7ee) to you my most ungrateful subjects.

#### $27.50 for a year of my genius??!!

![](https://substackcdn.com/image/fetch/$s_!15gH!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb56fd75d-690f-4342-8ef3-c2a45d3d28a2_1328x596.png)

---

## Back to MotherDuck

Ok, so after my un-shameful reminder to get %50 off, let’s start pulling the puffed plumage of MotherDuck and see if the care and beautify of the open-source DuckDB translates to its money hungry mother.

> *First, because we have no choice, let’s see what MotherDuck calls themselves. I always find this interesting, how does a SaaS vendor see themselves, what are the core tenants they sell you out of the gate.*

The following is pulled straight from the [MotherDuck homepage](https://motherduck.com/get-started/?utm_term=motherduck&utm_campaign=Search+%7C+MotherDuck+Trial&utm_source=adwords&utm_medium=ppc&hsa_acc=6957541599&hsa_cam=21632707132&hsa_grp=165143078606&hsa_ad=710818339164&hsa_src=g&hsa_tgt=kwd-1961442647038&hsa_kw=motherduck&hsa_mt=b&hsa_net=adwords&hsa_ver=3&gad_source=1&gad_campaignid=21632707132&gbraid=0AAAAApg_UmAjPGqPxXSvWndJKe60c7gJJ&gclid=CjwKCAjwz5nGBhBBEiwA-W6XRAbdwZVIYc3AdaMwU5cWWhASL15jy-qn4jNUybeUcFo557Z944-3XBoCgmIQAvD_BwE).

```markup
With MotherDuck and DuckDB you get:

- Ergonomic Querying: 
Autocorrect SQL Typos with FixIt and Take a Bird’s Eye View of Your Data with Column Explorer and Pivots

- Analytics: Share Data with your Team Simply and Securely

- Data Ingestion: 
Supports Parquet, CSV, JSON, Iceberg, Delta, and more

- Pricing: 
Billing at the CPU Minute and Automated Query Planning Across Local + Cloud with Dual Execution
```

“Fast, Scalable Analytics without the overhead” - [MotherDuck](https://motherduck.com/get-started/?utm_term=motherduck&utm_campaign=Search+%7C+MotherDuck+Trial&utm_source=adwords&utm_medium=ppc&hsa_acc=6957541599&hsa_cam=21632707132&hsa_grp=165143078606&hsa_ad=710818339164&hsa_src=g&hsa_tgt=kwd-1961442647038&hsa_kw=motherduck&hsa_mt=b&hsa_net=adwords&hsa_ver=3&gad_source=1&gad_campaignid=21632707132&gbraid=0AAAAApg_UmAjPGqPxXSvWndJKe60c7gJJ&gclid=CjwKCAjwz5nGBhBBEiwA-W6XRAbdwZVIYc3AdaMwU5cWWhASL15jy-qn4jNUybeUcFo557Z944-3XBoCgmIQAvD_BwE)

So, that’s pretty much what I expected, not sure about you. What I do find interesting is that they aren’t exactly, or explicitly, ***saying anything about Lake House or Data Warehouse.***

> I mean they sort of say it, don’t say it, when they say make big data feel small and run scalable analytics. But that could just be me reading between the lines.

***Thanks to [Delta](http://www.delta.io/) for sponsoring this newsletter! I personally use Delta Lake on a daily basis, and I believe this technology represents the future of Data Engineering. Content like this would not be possible without their support. Check out [their website](http://www.delta.io/) below.***

![](https://substackcdn.com/image/fetch/$s_!wmd9!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F708be49f-dfaa-498f-a862-8e9810a5fc58_600x123.webp)

### Going through the onboarding workflow.

![](https://substackcdn.com/image/fetch/$s_!vqOl!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdd6caaa0-6c91-466a-8858-0d39f78459ed_1389x691.png)

I’m not going to lie, after that janky nightmare of onboarding with Polars Cloud and that horrid UI, the MotherDuck signup flow is incredible.

It’s a beautiful UI, step by step, snappy. Everything you would expect from something built in this century, and bodes well for the things we have yet to do.

One of the first things you will notice is the nice clean layout, one that doesn’t leave you wondering where to click next or what to explore.

> *The first thing I’m going to do is connect my data in S3. So I will use their nice UI and add my AWS creds.*

![](https://substackcdn.com/image/fetch/$s_!L8zi!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1e5c6727-69f7-4aae-aa53-884c1fe7dd30_2448x1582.png)

I also shouldn’t fail to mention their top-tier documentation, not surprising of course, but it’s well laid out, thoughtful, and you can find whatever you need right away.

![](https://substackcdn.com/image/fetch/$s_!oVfd!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffc9b1d2d-bc9e-4856-a2c8-e6b4ba4da785_2448x1582.png)

But, before I start playing with my data in S3, I probably got ahead of myself, let’s take a moment to in a more academic manner, ***understand some core concepts***, at least from my 10,000 foot view and understanding as a new user.

> *I have little practical experience with DuckDB, other than what I’ve done playing around with it on this blog, and zero experience with MotherDuck, so take this with a grain of salt.*

![](https://substackcdn.com/image/fetch/$s_!VLja!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6e2afcdc-3ca0-41f7-9cc2-b5e66d0e9b98_1574x1018.png)

If you made me try to summarize MotherDuck for you, from my perspective, **as to what it actually is**?

![](https://substackcdn.com/image/fetch/$s_!v_fm!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3ae995a1-aaab-4b9d-9f20-46c1a8dd7e48_1600x520.png)

With the caveat that they did release [DuckLake](https://dataengineeringcentral.substack.com/p/duckdb-enters-the-lake-house-race?utm_source=publication-search), so you are more than welcome to store your data with MotherDuck as well, if you want and end-to-end experience.

You can read my unkind and spicy take on DuckLake below. May the good Lord forgive me.

![](https://substackcdn.com/image/fetch/$s_!wrFa!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4cbb6d46-c4d1-4f4d-b556-47c2da284264_1816x1016.png)

Anywho, they (MotherDuck) doesn’t push it down your throat, and this is probably why they will win.

- The make a nice clean product by which you can easily move and compute data in and out of any Cloud Provider.
	- aka … no hard vendor lock-in

> Ok, back to the matters at hand. What I really need to do (*whether I want to or not*), is to create an Airflow DAG that can do a “data thing” with MotherDuck.

When it comes down to brass-tacks, it’s of course easy enough to ***oohh*** and ***ahhh*** our way through a nice UI, but at the end of the day I should be able to setup a simple data pipeline with Apache Airflow for ANY data tool worth its salt.

If it works well, you have a good thing on your hand, if it struggles or is hard to do, than you have found out all you need to know.

---

### Building a MotherDuck pipeline with Apache Airflow.

Well, first things first lets mosey over into the Notebook UI that MotherDuck stole from the GOAT Databricks.

![](https://substackcdn.com/image/fetch/$s_!cT9W!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F86271c63-ad23-4dc6-9a75-b54b89d362f6_978x400.png)

I created a Database to hold my tables, ***pickles*** of course. But, if we are going to Airflow this @!@$# then let’s find where we can create a TOKEN for the authentication.

![](https://substackcdn.com/image/fetch/$s_!DXzc!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3c2b93b9-9489-4fdb-805e-6a8b3e76899c_1340x735.png)

Easy enough once you find the settings page.

---

#### The Airflow Part.

Ok, let’s start writing the Airflow DAG that can do the MotherDuck work for us. Once we have that scaffolded we can write the DuckDB code itself.

Lucky for us, that much lauded [Astronomer has some examples we can peak at.](https://www.astronomer.io/docs/learn/airflow-duckdb#step-2-create-a-dag-using-the-duckdb-python-package)

![](https://substackcdn.com/image/fetch/$s_!XZiW!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff75e1c0b-e8a8-4901-bac7-167a3318c03a_1281x629.png)

We will have to add our logic to connect to MotherDuck, but we can worry about that later.

![](https://substackcdn.com/image/fetch/$s_!rWwZ!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb9fd6b30-d5e6-4a2d-88e8-88a2ee1ea53d_1600x522.png)

Now for the DAG, maybe at the same time we will write the DuckDB/MotherDuck crap and talk about it all at once.

> *BTW, we are going to use 50GB of CSV hard drive data in s3 to let DuckDB crunch on. Can’t make it easy, you know what I’m saying??’*

![](https://substackcdn.com/image/fetch/$s_!8cFg!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5e155574-aa58-43a7-9b40-dc6cfe87ce99_1281x629.png)

Anywho, Airflow DAG + MotherDuck + DuckDB logic. [Code on GitHub.](https://github.com/danielbeach/MotherDuckwithApacheAirflow/tree/main)

![](https://substackcdn.com/image/fetch/$s_!ZW-f!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8244a523-95fa-4726-a05b-ab1e6dbdd2c3_1814x2122.png)

Well, I do have to admit … kinda looks nice don’t it?? Hold on, going to send a picture of this my mother, make her proud and all.

> What a match made in heaven, that MotherDuck and Airflow, to think all the poor saps out there tripping over FiveTran when you can write this sort of thing.

Let’s be honest, connecting your code to MotherDuck vs running it locally is lit.

```markup
con = duckdb.connect(f"md:{MD_DB}?motherduck_token={MD_TOKEN}")
```

I mean seriously, MotherDuck is a genius. **Ain’t nobody else by a mile who is making it this EASY to move from development code to production.**

Also, you hobbits ain’t going to believe how fast that crap ran.

![](https://substackcdn.com/image/fetch/$s_!TjgL!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6b9934d0-20a4-418e-8142-d591774eb73d_1308x592.png)

To top it all off, check the results in the UI was easier and smoother than your hair with all the gel at prom in 9th grade.

![](https://substackcdn.com/image/fetch/$s_!Wcrb!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7a5b2246-b559-4373-b071-1125b2c6a42f_1386x781.png)

---

### Sign me up buttercup.

This MotherDuck thingy is such a beauty it brings a tear to me old eye. You have no idea how many new tools (maybe you do) I agonize over while trying to bring you the good, the bad, and the ugly.

> ***They are always ugly and take copious amounts of time to get working correctly.***

What MotherDuck has done with with DuckDB in the cloud is insane, the entire experience end to end is bullet and idiot proof. As per usually everything DuckDB touches turns to gold.