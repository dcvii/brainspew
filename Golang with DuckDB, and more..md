---
title: "Golang with DuckDB, and more."
source: "https://dataengineeringcentral.substack.com/p/golang-with-duckdb-and-more"
author:
  - "[[Daniel Beach]]"
published: 2025-06-17
created: 2025-06-20
description: "absent from Data Engineering"
tags:
  - "clippings"
---
### absent from Data Engineering

![](https://substackcdn.com/image/fetch/w_424)

Recently, I was reading through some documentation on DuckDB and came across information about Golang. I’ve never gotten bit by the Golang bug, as clearly seen when looking at my [109 public GitHub repo, only 5 of those little blighters are written in Golang](https://github.com/danielbeach?tab=repositories&q=&type=&language=go&sort=).

> That, and it was 2022, the last time some Golang slipped through my fingers. **Why is that?**

I’ve found more use with Rust than Golang, *but I’m no Golang hater*; I can see the beauty in its simplicity and speed. Sometimes, it is quite confusing as to WHY it never caught on in Data Engineering or data context.

I mean, I did write an article about why Golang lost to Rust in the battle for Data Engineering supremacy. One would like to think it boils down to something as simple as Garbage Collection, but that can’t be true in a data world awash with Python.

[(code on GitHub)](https://github.com/danielbeach/GolangDuckDB)

![](https://substackcdn.com/image/fetch/w_424)

Clearly, the reasons must be more complicated and deeper as to why Golang couldn’t get its claws into the data space.

Even the hungry rabble on Reddit can’t deny that [Golang simply isn’t suitable for most Data Engineering work.](https://www.reddit.com/r/golang/comments/178cmfx/go_for_data_engineering/)

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/7314f3a3-bb35-40f5-86b3-506c9b943763_1904x428.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:327,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:124536,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://www.reddit.com/r/golang/comments/178cmfx/go_for_data_engineering/%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7314f3a3-bb35-40f5-86b3-506c9b943763_1904x428.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

In theory, you CAN do anything you like, but there is a difference between being able to do something vs ***should you do something.***

> To me, it’s clear why Golang hasn’t caught on in data, and the above Reddit comment gives you a glaring clue as to why. ***Integrations*** and ***interoperability***.

#### Data is a land built upon the bones of a thousand tools; SDKs and integrations are at the core of a data engineering toolset.

The simple truth is that for a long time, Golang simply lacked first-class support for the myriad of tooling, SDK, and APIs that make up most of what Data Engineer is … namely, using a plethora of tools to manipulate “stuff.”

Sure, that may have changed now, but it’s too late; the fact that Polars, DataFusion, etc., etc. got to the SQL and Dataframe-centric world of Data Engineering first sealed the fate of Golang in data. Sad but true.

Back in 2022, [I did test the ONLY option at the time for Dataframes in Golang](https://www.confessionsofadataguy.com/gandalfs-beard-dataframes-in-golang/) … and it wasn’t pretty. Slow, clunky, and just not fun. No one in their right mind would put themselves through that pain when much better options exist.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/e8afc372-43a6-4846-8de0-5bbe4a945906_1904x916.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:700,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:924081,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://www.confessionsofadataguy.com/gandalfs-beard-dataframes-in-golang/%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe8afc372-43a6-4846-8de0-5bbe4a945906_1904x916.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

Anywho, time grows short, and I wax poetic; today, I thought I would like to revisit Golang in regards to some of the more popular tools today, and see what gives after a few years have passed.

DuckDB. Delta Lake. Dataframes. ← Golang.

Has anything changed? Probably, let’s find out.

## DuckDB with Golang.

I’m honestly just curious, more than anything, what it looks like to write some Golang these days and attempt to use a newish package like DuckDB. *Is the code clean and nice? Is it a pain? What about versions and working stuff together?*

I don’t know; it doesn’t seem special by any means; one could argue that boring is good.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/bc6d6516-32be-4c0c-9594-e7feb1ce0c9d_2000x2270.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1653,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:414951,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbc6d6516-32be-4c0c-9594-e7feb1ce0c9d_2000x2270.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

Using Golang doesn’t seem much different than using Golang in Python or whatever else, that probably says more about DuckDB than Golang.

> *I want to use something new like DuckLake with Golang, but the default Golang-DuckDB package doesn’t come with the latest DuckDB version that would ALLOW you to use DuckLake + Golang. I tried. Doesn’t work.*

I fought it for a little bit but gave up.

Indeed, this is one of the main reasons Golang is not widely adopted in Data Engineering. When the community is smaller (e.g., Golang) than Rust, Python, Scala, Java, etc., **in terms of data-centric tooling, it will fall behind, and it’s a self-fulfilling prophecy.**

BTW, below is my Docker container if you’re interested in doing the same thing.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/6f1b0884-c593-4729-93fa-c33b06817b11_2000x1526.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1111,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:354127,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6f1b0884-c593-4729-93fa-c33b06817b11_2000x1526.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

> *I guess that’s sorta the point with Golang and tools like DuckDB and DuckLake. DuckDB is relatively new, DuckLake even newer, and Go is somewhat obscure in the context of data engineering and tooling. Hence, I encountered strange errors related to the official DuckDB Golang package.*

[(Code on GitHub)](https://github.com/danielbeach/GolangDuckDB)

One could say I’m not trying very hard, and that is true, but at this point in Data Engineering, I don’t need to try hard. Every other known tool and platform in Data Engineering runs DuckDB like a champ without.

## Golang with Dataframes.

After my weak attempt with Golang and DuckDB, I will pretend like that never happened. I was curious after a few years, if Golang had finally caught up in what I would call the “Dataframe” centric space.

This is important.

To be taken seriously in the Data world, a language would have to have at least a few easy-to-use Dataframe tools. Why? Because the data world revolves around tabular data, Dataframes or SQL is the preferred abstraction.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/223baf75-4b9b-4d47-a79d-ba020890b075_2200x1162.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:769,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:263676,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://github.com/go-gota/gota%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F223baf75-4b9b-4d47-a79d-ba020890b075_2200x1162.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

[gota](https://github.com/go-gota/gota) is at the top of the list on Google. Simply looking at the examples makes my toes curl. There isn’t a soul on God’s green earth who would raise their hand and say they want to filter a Dataframe like this.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/a0ee1904-f8ad-4da2-874b-de96ee0aa09c_2200x934.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:618,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:216303,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa0ee1904-f8ad-4da2-874b-de96ee0aa09c_2200x934.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

I mean, [even writing Rust with Polars to do Dataframe stuff](https://docs.rs/polars/latest/polars/) isn’t that ugly.

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/5925c9cb-0611-4ec4-b893-e5f39f8a4dea_2232x920.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:600,%22width%22:1456,%22resizeWidth%22:null,%22bytes%22:272591,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:%22https://docs.rs/polars/latest/polars/%22,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:%22https://dataengineeringcentral.substack.com/i/165909036?img=https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5925c9cb-0611-4ec4-b893-e5f39f8a4dea_2232x920.png%22,%22isProcessing%22:false,%22align%22:null,%22offset%22:false})

Heck, if you google “golang with sql” you get a whole lotta nothing. And that, my friend, is where Golang + data goes to die a slow death, or fast one.

### Listen Up.

Hey, man, I’ve got nothing against Golang. I’ve written it a few times; it seems nice and has a low learning curve compared to Rust. So, why did I choose to learn Rust instead of Golang?

Community. Tooling. Wide support. Integrations.

Just saying.

> *I know Golang has its use cases, has been used to build awesome things, and probably will be used more in the future. But that future isn’t in Data Engineering I don’t think.*