---
title: "Southwall Update"
source: "https://tessellations.substack.com/p/southwall-update"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2025-11-06
created: 2025-11-24
description: "Sorry I'm late."
tags:
  - "clippings"
---
### Sorry I'm late.

Sometimes I forget how much I process and at what speed. So when I explain myself verbally, I take so many shortcuts, unless I have powerpointed the whole thing up, I have no idea if people are following my ramble. Here’s what’s new.

**AI Update**  
I have backed down off of AI integration on the front end, and have begun to tread a bit more deeply into **declarative programming**. I’m going to go backward, I think. Basically get a guy I know who has been a systems software engineer since 1984 to teach me software engineering abstractions like “distributed backpressure” and then do smallish prompts to pieces of code that are under 500 lines. That’s the first plan anyhow.

I’m starting to catalog prompts from [Nate](https://natesnewsletter.substack.com/). And I’m really happy about my shifting towards vibe coding because it is becoming a lot more clear that this is the way to go. Still behind in my reading.

Met a guy named Aaron who’s running an AI healthcare startup somewhere in Los Angeles at Tech Week. Where’d he go?

**Logos Update**  
No news, except that now I think I can build this in my spare time. Like really rapidly for Boxtag. Now I just need a kind of css scraper to perfect my stuff.

**DE Update**  
In the news is that the **Kafka** streaming market is full to the brim and prices are dropping. Also I heard good news on **Unity Catalog**, and kind of bad news for Databricks. Somebody has figured out how to do the former without the latter. Every day more respect for **Postgres**.

I just found some old stuff for the equivalent of **Pandas for Go**. So anything I can do to leave Python is good news. I think in the small data future there’s no need for any of that. Yeah and [there’s this](https://github.com/jordandelbar/go-polars). Haven’t tried it yet.

**Data Update**  
I looked once again at indices for **DuckDB**. Indicies!? It turns out that I have been working around the weak upserts for **Vertica** too long. So I’ve never seen the construct of ON CONFLICT clause. Could be useful.

I’m building an ingestor against Tiingo and need to debug it, but that’s going to be nice once it’s done. Again, my angle is using Go cli-s that can just as easily be run from shell scripts as from agents. It’s the basic construct for me going forward. Not thinking about WASM, but some other ducktitioners have done cool things.

**Southwall Update  
**I just finished installing **Vault** and **Gitlab-CE** for my homelab. That’s going to save me money on private repos on Github. I also completed a **Netbox** install. So things are shaping up. It turns out that my little Firebat server is a better deal than I thought. Maybe no more NUCs.

I’m stalled in the middle of my **Twingate** config. I’m definitely going in that direction and getting rid of **NoMachine** and **ZeroTier**. That plus Ubiqiti network hardware should shape me up pretty well. **Rustdesk** is my new goto.

I also am going to put together some **nginx** reverse proxies so that I can publish data safely. And finally, [metrodecisions.com](http://www.metrodecisions.com/) is up and halfway configured. Don’t sign up yet. It hasn’t got approval from the DEI board…

![](https://substackcdn.com/image/fetch/$s_!cn3E!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F782caa17-a9fb-4354-8225-f10bc81313df_1024x1024.jpeg)