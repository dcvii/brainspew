---
title: "Moving away from Fivetran due to cost: Massive Salesforce ingestion to Snowflake at scale — what are our real alternatives?"
source: "https://www.reddit.com/r/dataengineering/comments/1w0khin/moving_away_from_fivetran_due_to_cost_massive/"
author:
  - "[[onksssss]]"
published: 2026-08-28
created: 2026-08-31
description: "My company wants to replace Fivetran with easier and cheaper alternative. Context & Stack: Stack: Snow"
tags:
  - "brainspew"
---
My company wants to replace Fivetran with easier and cheaper alternative.

**Context & Stack:**

- **Stack:** Snowflake, dbt, Fivetran
- **Major Ingestion:** Salesforce (4 production instances) -> Snowflake

We are looking for alternatives to Fivetran due to escalating ingestion costs. We strictly need an ingestion tool (we handle all transformations via dbt).

**What We've Tried (and why it failed/didn't fit):**

- **Matillion:** Failed at our scale (couldn't handle 15-minute syncs).
- **Airbyte:** Failed at scale.
- **ETLWorks:** Cost.
- **Informatica / IDMC:** Already in-house, but trying to sunset due to high costs.
- **Airflow:** Already in-house, but too much custom configuration overhead.
- **Boomi:** Already in-house, but on-prem and costly.
- **Hevo Data:** Lacks the necessary scale.

**Our Current Top Contender:** **Openflow** is being heavily pushed by upper management. They have a soft spot for it, likely because Snowflake is making it lucrative/incentivizing adoption to build their user base.

**Our Core Requirements:**

- Ingestion-only focus (dbt handles transformations) (imp)
- High scalability and cloud-native performance (imp)
- Fast execution with simple configuration, yet deep integration options
- Rich catalog of connectors
- MCP and AI capabilities (optional)

Do we have any other realistic solutions or shall go with Openflow?

We are okay to try modern solutions like utilizing skills / agents to create connectors on the fly etc but these solutions we have known to be not much scalable..

Any help is appreciated..

---

## Comments

> **mr\_buildmore** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dnb1s/) · 120 points
> 
> I wrote a dlt pipeline to handle Salesforce at my workplace. Works great! A few notes I'd share:
> 
> - Salesforce backend is strongly typed, so you can map those types to Arrow and use `simple-salesforce` to query the Bulk 2.0 API which yields CSV pages
> - Salesforce schema evolution is a train wreck because sales managers have 0 impulse control, so imo pass the buck to the transformation pipeline
> - Salesforce Data Cloud has the ability to natively yield Arrow and is probably worth having if you have 4 instances with God-only-knows in them
> 
> > **molodyets** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6meh1e/) · 3 points
> > 
> > Same here. 
> > 
> > Only change we tweaked from the default dlt salesforce source was adding routing for object type since history objects don’t use sys mod stamp etc
> > 
> > > **mr\_buildmore** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6mez7j/) · 2 points
> > > 
> > > Did you use simple-salesforce as a wrapper to implement the object/resource definitions or did you query the API directly? My org doesn't strictly need the history tables but I'd be curious to talk through someone else's implementation of the same solution.
> > > 
> > > > **molodyets** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6mkudm/) · 3 points
> > > > 
> > > > Yep, I did the same exact thing, but then just modified it so it was kind of similar to the Zedek pipeline that they have where there was a list of sets with the configuration
> > > > 
> > > > So for each object we pull in I have the object name what the target table name I want is the ID column a flag if it’s incremental, and then which column to check against for pulling the incremental.
> > > > 
> > > > Then just use the dynamic resource generator.
> 
> > **wiktor1800** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dowbs/) · 8 points
> > 
> > This is the way
> > 
> > > **baby-wall-e** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dwfb6/) · 5 points
> > > 
> > > This is the way

> **Grukorg88** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dnrow/) · 25 points
> 
> Have you looked at the native integration that allows you to use snowflake shares? [https://www.snowflake.com/en/blog/bi-directional-data-sharing-snowflake-salesforce-ga/](https://www.snowflake.com/en/blog/bi-directional-data-sharing-snowflake-salesforce-ga/)
> 
> > **AdamDobrawy** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e79um/) · 8 points
> > 
> > Alternativelly, you can take look on zero-copy connectors: [https://docs.snowflake.com/en/user-guide/data-integration/zero-copy/salesforce/setup](https://docs.snowflake.com/en/user-guide/data-integration/zero-copy/salesforce/setup)

> **coldflame563** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dsady/) · 33 points
> 
> If you use data cloud on Salesforce there’s a new native tool in snowflake. Zero copy etl instant sync etc.
> 
> > **Existing\_Wealth6142** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f950a/) · 4 points
> > 
> > yeah seconding that zero copy data shares are the best option here
> > 
> > > **coldflame563** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f9h6f/) · 2 points
> > > 
> > > It’s unidirectional (the new one) only ingest. The old one (still available I think) was bidirectional. Interestingly enough it was just a shared iceberg table behind the scenes
> 
> > **Pine-apple-pen85** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fu6zc/) · 2 points
> > 
> > This is the way. Very easy to setup up both on Salesforce and snowflake side.

> **TheOriginal1984** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6doilm/) · 13 points
> 
> Realistically you’ve named all the top contenders and more except DLT. Once teams get to the requirements you have, most the end up rolling their own using an orchestration engine like airflow, prefect, dragster etc, drop DLT in there, and execute that way. If you’re already using airflow to orchestrate dbt, DLT is a reasonable choice. Sling is also a great choice depending on the integrations you need.
> 
> > **RoobyRak** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dsy3y/) · 6 points
> > 
> > Never deployed sling in production. But if (for some reason) the pythonic side to DLT is too much overhead for them, sling would be my second choice too.

> **Edd037** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dumxw/) · 18 points
> 
> Currently moving all our workloads off Fivetran. They've basically quadrupled the price over the space of about 18 months. Their account managers are fleeing like rats of a sinking ship. What the hell is going on there?
> 
> > **hornyforsavings** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6gsta4/) · 1 points
> > 
> > which vendor are you moving to?
> > 
> > > **Edd037** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6gtus9/) · 2 points
> > > 
> > > Combination of things. Where Databricks has an in built connector (e.g. Salesforce), we will use that. We've found its a quarter of the cost of Fivetran, but they have fewer connectors and they tend to be less mature. Otherwise, vibe-coded API calls, which are so easy these days that it takes away half of Fivetran's USP.
> > > 
> > > > **FUCKYOUINYOURFACE** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6lz12a/) · 1 points
> > > > 
> > > > Fivetran has an anti-moat.

> **AndriusVi7** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dn38l/) · 14 points
> 
> Why not ingest through apis and only pay for the compute?
> 
> > **Prestigious\_Pace2782** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dzr8x/) · 5 points
> > 
> > Yeah that’s what we do. Just python stored procs. Pretty decent throughput if you build it resilient.

> **Outrageous\_Let5743** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dzsa7/) · 6 points
> 
> dlt has a native salesforce source. It is free and open source.

> **unexpectedreboots** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6eclxu/) · 6 points
> 
> I'm kind of curious how Airbyte "failed at scale".
> 
> Four SF instances, regardless of how many custom objects you have, isn't big data.
> 
> > **antraxsuicide** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6esaz4/) · 3 points
> > 
> > Yeah, we manage way more than 4 SF instances and Airbyte has mostly been fine for getting data to Snowflake. Sure, in 7 years, they’ve botched something once or twice but that’s not a bad track record

> **GrumDum** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dlx6j/) · 21 points
> 
> dlt
> 
> > **rycolos** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dr5rx/) · 13 points
> > 
> > If they’re afraid of custom work overhead, I don’t think dlt is in the cards.
> > 
> > > **Outrageous\_Let5743** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dzypf/) · 10 points
> > > 
> > > Open claude code. Ask make a dlt salesforce connection. Wait a few minutes and done.
> > > 
> > > **RoobyRak** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6drz9w/) · 15 points
> > > 
> > > Some basic Python skills is not overhead. It’s open source and well documented.
> > > 
> > > This is a no brainer.
> > > 
> > > > **rycolos** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dwjqq/) · 12 points
> > > > 
> > > > Hey, I agree with you! But if they’re afraid of Airflow config…
> > > > 
> > > > > **Additional\_Candy\_400** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dyxvu/) · 10 points
> > > > > 
> > > > > God forbid someone writes some code!
> > > > > 
> > > > > **RoobyRak** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e3pz2/) · 3 points
> > > > > 
> > > > > Afraid of there own shadow too tbh

> **Nekobul** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dym3a/) · 8 points
> 
> Fivetran is also known as the king of easy. That's why they became so popular in the first place. Now the bill has to be paid.

> **FirstBabyChancellor** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dp6mn/) · 4 points
> 
> Look into either Estuary (if you want a cheaper, managed alternative to Fivetran) or dlt (if you're okay with owning the ELT pipeline yourself?.

> **CingKan** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dq139/) · 3 points
> 
> Fivetran got massive market share then got greedy they'l now pray the price. For your problem whats your data size ?

> **shreyankj267** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dsnw0/) · 3 points
> 
> We have currently designed and deployed Openflow for the same specific use case and it is a breeze. It does everything an ideal elt pipeline should and is self sustaining. The only caveat is its still a nuanced product being developed by Snowflake internally. And cost is another huge aspect. Our end goal is to use Zero Copy via D360 PrivateConnect between Snowflake and Salesforce as thats more robust, cost effective and bi-directional. But, yes Openflow is easier to design and maintain once you get around the configuration of parameters and monitoring it consistently.

> **Kobosil** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dumnh/) · 3 points
> 
> > **Airflow:** Already in-house, but too much custom configuration overhead.
> 
> what overhead is there?
> 
> Airflow has a Salesforce package to handle connection and bulk operations

> **nloding** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e3mvn/) · 3 points
> 
> If you’re looking for a Fivetran-like experience in terms of ease of use and configuration and support, check out Matia (Matia.io). Full disclosure: I work there, I won’t make any larger pitch here, but if you have any questions DM me!

> **josejo9423** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fitkr/) · 3 points
> 
> What is your scale?

> **Nottabird\_Nottaplane** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6j7x9l/) · 3 points
> 
> Snowflake has a direct Salesforce connector. If all you care about, mainly, is Salesforce syncs, why not use that? It was announced just earlier at Summit.

> **mintskydata** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dn172/) · 6 points
> 
> Estuary

> **siddartha08** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ebr4i/) · 4 points
> 
> Have you thought about databricks? I haven't either but all their damn sales ppl have.

> **limartje** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dy3pj/) · 2 points
> 
> Can you give more detail on why the scaling fails? I don't know the volumes at hand, but most well-known solutions shouldn't have difficulties with extracting data from Salesforce.

> **dasnoob** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ebo73/) · 2 points
> 
> We just have a python script I wrote that lives in a VM and uses the bulk API to do it.

> **marclamberti** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6enskt/) · 2 points
> 
> Can you develop on Airflow? What do you mean by too much custom config overhead

> **WhoDunIt1789** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6epi5e/) · 2 points
> 
> Haven't used these guys personally but I've seen their pitch and they look like a real up and coming contender. [https://www.matia.io/](https://www.matia.io/)
> 
> > **SomeSmith** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6jg8ne/) · 1 points
> > 
> > We use them. Still in very much a start-up phase, but issues are addressed quickly and everyone is always willing to jump on a call first thing. We spent a lot of time debating rolling our own connectors, and decided to pay someone else to do the work. They also have some very interesting DQ and observability tooling that has been helpful with our DQ folks.

> **chagrinoustic** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fnpdf/) · 2 points
> 
> I’d say careful with Openflow, inspect the cloud costs before you turn that on instead of Fivetran. We actually saved on cost switching to Fivetran away from Openflow for one of our use cases. Openflow charges a daily flat rate for having a deployment open, then a daily flat rate for having a runtime open depending on the size of the nodes you configure.

> **sotgouli** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dofvj/) · 3 points
> 
> Probs dlt, although I feel they got too sloppy recently.
> 
> Otherwise Airflow. Low cost is the trade-off for Dev overhead.
> 
> > **Outrageous\_Let5743** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e07f0/) · 12 points
> > 
> > Airflow is an orchestrator, not an extraction tool. Using orchestrators as anything else will suck a lot when you extent.
> > 
> > > **Warbird01** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6eru5x/) · 1 points
> > > 
> > > Bingo
> 
> > **RoobyRak** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ds7wb/) · 3 points
> > 
> > Sloppy how?
> > 
> > > **sotgouli** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dvcet/) · 1 points
> > > 
> > > Their source scaffolding used to be very good. Choose an official source or templated one, add some creds/params and it was ready to go.
> > > 
> > > Last time I tried their AI generated official sources (for marketing providers for example) the scaffolding kept hallucinating the required parameters and couldn't follow the template properly.
> > > 
> > > Edit: fixing autocorrect mistakes
> 
> > **VitrumTormento** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dort8/) · 2 points
> > 
> > Id interested in what do you mean by too sloppy? Ive been thinking of trialing it on a new project but on the fence
> > 
> > > **sotgouli** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dvqqd/) · 1 points
> > > 
> > > Give it a try! I'm a bit salty cause the dev experience regressed a bit.
> > > 
> > > Their scaffolding used to be very good, but last time I tried their new AI generated sources, the scaffold kept hallucinating parameters and breaking the template.
> > > 
> > > That was a few months ago though. They could have improved on it already.
> > > 
> > > **molodyets** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6mdgzh/) · 1 points
> > > 
> > > We’re all in on it with no issues. 20 sources. Not sure what the feeling of getting sloppy is coming from
> 
> > **unexpectedreboots** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6eccpm/) · 2 points
> > 
> > > airflow
> > 
> > Huh

> **Ok\_Exchange1148** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6gt09r/) · 2 points
> 
> Hey, Founder Meltano Cloud here 👋
> 
> Our platform and team could be a good scale for stack. I think we deliver on the connector scalability and having moved a number of FiveTran salesforce customers over I’m pretty confident we’re there on functionality. We nail the open / integration too.

> **Fizmeister** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6doko1/) · 2 points
> 
> Take a look at Qlik Replicate.
> 
> It supports automated, batch and real-time data movement and high-performance CDC between a wide variety of database sources, cloud platforms, and data warehouses with key features like automatic schema evolution, zero-footprint architecture, and no manual ETL coding. If you prefer a SaaS solution, Qlik Talend Cloud Project Pipelines do the same thing.

> **Fraznist** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dmo01/) · 1 points
> 
> Could check out [ingestr](https://getbruin.com/docs/ingestr)
> 
> . Or bruin as the managed platform around it. They are rather new but it was easy to use and I was happy with it for personal projects. Their catalog is decently sized as well.

> **alt\_acc2020** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dozx5/) · 1 points
> 
> What’s the data size?
> 
> Why not just spin up some compute, run a dlt script off of it?

> **Ok-Sentence-8542** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dq27g/) · 1 points
> 
> A few years ago we used datafactory salesforce connector via bulk load api. Not sure if its still available but worked perfectly. You can also load via delta load.

> **Hour-Measurement-835** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ds915/) · 1 points
> 
> Pull the MAR breakdown per table before you pick anything. On Salesforce it's usually Task, EmailMessage and the History objects doing most of the bill, and almost none of those need 15 minute syncs.

> **NovelSine5874** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dumg0/) · 1 points
> 
> We made a custom Airflow operator for Salesforce using simple Salesforce module and bulk. Extraction runs every hour. To handle schema evolution we store all the data of a row in JSON in our target table. Nothing breaks if a column is added.  
> The transformation layer handles shredding of JSON and expose only the required columns.

> **prokid1911** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e186b/) · 1 points
> 
> I've used another product called Datachannel, they are a small company providing similar features as Fivetran. You can pull data from various sources into Snowflake, write DBT models and push them into a Git Repo and make use of the DBT orchestration available in their ecosystem.
> 
> This might come under self-promotion, but I'm not associated with them. Just a thing that I've worked with.
> 
> I've also worked with OpenFlow in the past and the UI is kinda non-intuitive (IIRC, it is built on top of Apache Ni-Fi), pipeline debugging could be a PITA as well, especially custom Python scripts. We used it for a similar reason, Snowflake sales guy pushed it hard to the leadership.

> **magixmikexxs** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e1nnp/) · 1 points
> 
> Hevodata works well

> **akozich** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e6qr9/) · 1 points
> 
> Dagster + dbt + dlt or Airbyte or direct python.
> 
> Airbyte failing at scale surprisingly.
> 
> I would suggest Airbyte if you want self service for your consumers. If it’s centrally managed - dlt
> 
> If you don’t already use dagster for dbt - you missing out, this is a good chance to get it going.

> **GAC0** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6e8tzk/) · 1 points
> 
> Spark or pure Python Pandas/Polars depending on data the dada.  
> *No* expensive graphic tools.

> **Ucspe** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ea5mr/) · 1 points
> 
> AWS app flow. Couldn’t be easier/more reliable. We mirror over 100 salesforce objects for ~$30/month

> **EnthusiasmOk8533** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6eh62i/) · 1 points
> 
> Cdata - You don't pay for amount of data moved ,they give fixed cost plan.

> **kakoni** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ei60n/) · 1 points
> 
> Apache Seatunnel has salesforce connector + snowflake sink.

> **kaalaakhatta** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6emfwv/) · 1 points
> 
> Look at Snaplogic.

> **jonas-weld** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6enxbn/) · 1 points
> 
> [Weld.app](http://weld.app/)
> 
> is definitely worth a look here. We’re built for exactly this kind of ingestion use case, including Salesforce → Snowflake, with pricing that can be ~10x lower than Fivetran depending on volume.
> 
> Happy to set you up with a trial and let you benchmark it against your current setup.
> 
> *Disclaimer: I work at Weld, but the pricing comparison is based on actual customer usage.*

> **Old-Fishing1973** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ex02q/) · 1 points
> 
> What’s your annual spend on Fivetran? Ask your AM for the best discount or tell them you’ll move away. Estuary is a good alternative. Hevo is the most unreliable.

> **URZ\_** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6ezqqx/) · 1 points
> 
> The issue here is not the tools, its the team.

> **discord-ian** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f13w4/) · 1 points
> 
> Open Flow or Open Source Ni Fi are going to be your best options to try next.
> 
> You want a tool that ingests data using Snowpipe or Snowpipes streaming. Insert records is too expensive at scale. We found these methods to be 50 - 100x cheaper than inserting records with Airbyte and our usage levels.
> 
> Your three options are a home grown solution like Airflow (or your own service), Ni Fi based option, and Kafka Connect. We use Kafka Connect, which if you can buy from Confluent is fairly easy to configure. There aren't really any other options that scale in a coat effect way - At least that I am aware of.

> **peterxsyd** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f3jcm/) · 1 points
> 
> With that many syncs, are you predominantly running batch ETL still or are you wanting/preferring a fully live DAG? 

> **mistanervous** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f4s59/) · 1 points
> 
> We just rolled our own hitting the salesforce API in airflow

> **ksco92** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f87nv/) · 1 points
> 
> Well I’d do it arrow and the Salesforce Python library if there’s dev capacity.
> 
> However I do have to say that even though Matillion has certainly fallen behind in a lot of things, their SF integration was really good. We introduced a ton of parallelization and object loops that even made our sales rep go “wtf how are you even doing that”. We were doing large scale extraction every 5 mins. For everything else it sucked. 😂

> **jdl6884** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6f8e31/) · 1 points
> 
> Dagster on k8

> **Yuki100Percent** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fge5o/) · 1 points
> 
> My ingestion tool selection:  
> \- dlt  
> \- Airbyte  
> \- Estuary  
> \- Portable

> **MrGoFaGoat** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fgin4/) · 1 points
> 
> Posthog has a Fivetran competitor, they are expanding their destination stuff to match Fivetran. And they are usually super cheap with great support
> 
> > **PostHogTom** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6flxu0/) · 1 points
> > 
> > Hey! Thanks for the mention - yep, I'm building this out at PostHog right now, sync your salesforce data direct to Snowflake, coming very soon! Pull requests to watch: [https://github.com/PostHog/posthog/pull/86986](https://github.com/PostHog/posthog/pull/86986)
> > 
> > and [https://github.com/PostHog/posthog/pull/87962](https://github.com/PostHog/posthog/pull/87962)

> **mksym** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fk095/) · 1 points
> 
> I’m with Etlworks. We can handle your four Salesforce instances into Snowflake at 15-minute intervals, and we’re open to negotiating the price (which by the way is flat).
> 
> Happy to talk if you’re interested.

> **krakenant** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6fsyp3/) · 1 points
> 
> Gonna ask the question because I haven't seen anyone else ask it. Given 15 minutes intervals, are you doing incremental updates instead of full table updates? Salesforce should have last modified fields on every table to facilitate this.

> **Puzzleheaded\_Dig2499** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6g448w/) · 1 points
> 
> Oracle fdi

> **DjexNS** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6hdyen/) · 1 points
> 
> Does it have to be a cloud tool?
> 
> Can you rent a VPS somewhere and host a tool?

> **blueadept\_11** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6hrplg/) · 1 points
> 
> Our contract engineer can write a connecter with AI every 1.5days and our 12 connectors across hundreds of accounts costs $300 per month to process in databricks. We have multiple accounts per connector so DLT doesn't work for us, but even without it, the cost is minimal.

> **Budget-Minimum6040** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6i3gct/) · 1 points
> 
> > We strictly need an ingestion tool
> 
> > What We've Tried: Airflow
> 
> 🤯

> **sjjafan** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6idqg9/) · 1 points
> 
> Try Apache Hop.

> **PsychologicalOne752** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6j03wh/) · 1 points
> 
> How many tables? What size data every, 15 mins?

> **tossedsalad9696** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6j68jc/) · 1 points
> 
> Just drop some tables that no one uses and go to Fivetrans unlimited plan. And be done with it. Or as you listed look at all the shittier versions. Or build it yourself and get shit on when it breaks

> **Dissident-Contrarian** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6jrhek/) · 1 points
> 
> We moved to Matia and it was able to handle our scale, Airbyte failed in our POC. Worth checking out

> **rikkie\_09** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6k5bzh/) · 1 points
> 
> +1 on dlt like others have mentioned. i've been working on a solution that allows agents to automatically maintain dlt code as the data source changes or downstream needs change. you get the best of both worlds basically. If this sounds interesting would love to chat, DM'd

> **molodyets** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6md9jo/) · 1 points
> 
> What does “scale” mean here? 
> 
> just use dlt. At any scale your limitation will be the Salesforce api.

> **ethan-aaron** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6naiuw/) · 1 points
> 
> Portable is fixed fee and supports Salesforce at scale.
> 
> 1700 other connectors, but most clients that move from Fivetran to Portable for Salesforce love the predictability of pricing

> **Ok\_Principle\_9459** · [2026-08-29](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6o8xfp/) · 1 points
> 
> What cloud provider are you on? Tbh these orchestration frameworks can be overkill. Just run the workload on ECS fargate / cloud run jobs / whatever the azure equivalent is.

> **Timely-Coffee-6408** · [2026-08-30](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6trxb5/) · 1 points
> 
> I would recommend Airbyte

> **samstone21** · [2026-08-30](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6uepbj/) · 1 points
> 
> Switch to native saalesforce cdc on databricks

> **Prestigious\_Bank\_63** · [2026-08-31](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6wge74/) · 1 points
> 
> Boomi acquired Rivery almost 2 yrs ago and it is a cloud based solution. Boomi is also available in the cloud, not just on-premise
> 
> [https://siliconangle.com/2025/06/23/boomi-rivery-automation-data-pipelines-boomiworld/](https://siliconangle.com/2025/06/23/boomi-rivery-automation-data-pipelines-boomiworld/)

> **ExternalStandard4362** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dmz2u/) · 1 points
> 
> kafka?
> 
> > **byeproduct** · [2026-08-28](https://reddit.com/r/dataengineering/comments/1w0khin/comment/p6dvn5t/) · 1 points
> > 
> > Is this possible?