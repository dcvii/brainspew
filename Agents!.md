---
title: "Agents!"
source: "https://tessellations.substack.com/p/agents"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2025-10-30
created: 2025-11-24
description: "I think I get it."
tags:
  - "clippings"
---
### I think I get it.

![](https://substackcdn.com/image/fetch/$s_!YcmG!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F47fd1aec-7e33-47d4-9d4d-4a1e3eaadf11_1920x1080.jpeg)

So basically I’m following the carefully scripted presentation of [Network Chuck](https://notegpt.io/share/e0eb8c0f8), as I have before, with regard to the evolution of Southwall. This big step is basically me doing some coordinated multi-tasking with multiple AI agents doing multiple things.

Simply stated, I’m kind of all-in for using the three frontier models for specific tasks, and this is rearranging what I used to do with regard to vibe coding, which I now take a bit more seriously. So today I had a couple conceptual breakthroughs.

- codex - this is for strategic analysis and criticism of the best laid AI plans
- gemini - this is for discovery of whatever is out there, comparing and contrasting
- claude - this is for getting into the weeds of code and configuration

What’s new from NChuck is the idea of using two different folders in every repo.

- context - three files, independently modified by each agent then combined/merged so that each has the full context of what any of them has done.
- agents - a role specific directive with extended verbiage as in the above three bullets

All of these run under Warp which is kinda sorta my master control until I get comfortable with each of them doing their own thing. Plus Warp auto selects whatever model.

**Twingate  
**The first old project is to integrate what was my three NUCs into themselves with Ansible and two new Mac Minis. + My workstation and another small server that was going to be a hardware based firewall into a coherently managed cluster of things. I futzed around with Twingate and the people I was going to invite into my new safe domain had other things to do. So I kind of fell back to **ZeroTier** which I actually only rarely use. But now I’m very satisfied with Rustdesk, which I installed all around and the probability of remote access is back on the table. This will especially be the case when I build a proxy server for my DuckElephant which is Postgres with the DuckDB extension that I talked about last essay.

**The Aha Moment  
**Once I decided to move forward with Go, I recognized that my agents could find all of the libraries I wanted that I thought perhaps only existed in Python. Once I realized that, I found the all I needed to be able to do was read Go and think in Go, rather like I do in English. The more I read, the better I’ll get at reading. So now all I want to do is read Go as my goto idiom. I can vibe code all of the work I want to do. Nowadays when I look at Rust, it looks like overkill, and Python looks like a sloppy scripting language. And this is only a couple weeks in.

This was coupled with the concept of making something of Nate B. Jones’ library of prompts. But it was really watching Network Chuck put it all together in a terminal window on a machine he controls which sold me the entire bill of goods. That plus the [Kim & Yegge](https://duckduckgo.com/?q=kim+%26+yegge&atb=v472-1&ia=images&iax=images) book I bought yesterday.

I think it’s all about the metaprogramming. I kind of has to be. I think it’s the only way to stay sane.

The last bit is the [Jevons Paradox](https://en.wikipedia.org/wiki/Jevons_paradox). I absolutely believe it’s true. The lowered cost of programming and systems administration provided by AI will create new jobs. But it also keeps me busy doing stuff I didn’t have the patience to do before.