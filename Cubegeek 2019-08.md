---
title: "Cubegeek"
source: "https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2019/08/index.html"
author:
  - "[[Cubegeek]]"
published:
created: 2025-10-12
description: "Big Data Analytics, perspectives from a 25 year practitioner."
tags:
  - "clippings"
---

The Wayback Machine - https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2019/08/index.html

[« January 2019](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2019/01/index.html) | [Main](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/) | [April 2020 »](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2020/04/index.html)

### Three Years Later...Kafka

So it looks like I'm going to go back to heads down. That's a good thing, I suppose. The reason is that I get to learn something new. Yay. The thing I will be learning is Kafka streaming and all that I need to know about how to do Fast Data. And the good thing is that this will be very new - and I have to tell you that I never liked writing logic for commits and rollbacks in SQL. It just wasn't languagey enough. So I expect that within a few months I will be dangerous, and within a year I'll be first rate if not world class. My secret is my nose. I have a good nose for the pure flavor as well as strategic import. What I don't have are years to sit down in a fulltime gig and wait for my boss to ask me to do something interesting. Anyway. I need to write this preface in order to jumpstart the emotional part of this memory as I go forward so one day when I look back on my learning process I can say "Oh yeah I remember how shit I felt not getting that F job because they wanted somebody who was better than me at saying 'I live transactions'".

Anyway, in order to add to this frustration. Here is me mumbling about Kinesis and Kafka in May of 2016 (wow that was a long time ago).<iframe allow="autoplay; fullscreen" allowfullscreen="" src="https://web.archive.org/web/20240526115108if_/https://player.vimeo.com/video/356076774" width="640" height="564" frameborder="0"></iframe>

At the time, I was very enthused about transaction processing. Here I wrote [Dreaming about Streaming](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2016/05/dreaming-about-streaming.html).

> A couple weeks ago I presented a webinar in which I discussed one of our realtime apps which is attached to online gaming. On the back end of this architecture we are processing about 30,000 transactions per minute with a small two shard cluster of VoltDB. This setup hardly makes a peep over 25% CPU utilization running 24/7 with no downtime in two years. Cool enough, but then you realize that is handling more mobile transactions per year than PayPal. I did the math. And oh what fun it is to do this kind of math and realize what's computable for the kind of analytic data frameworks we build.

And [Transactions, The Final Frontier](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2016/05/transactions-the-final-frontier.html)

> I am newly aware of the idea of immutable data, but I have yet to work with such a designed data set. What I have seen are transaction systems that generate records that are overwritten to 'the latest state'. Consider the following idea. I have a plan. The plan meets my boss. I change my plan. The plan meets the enemy. I change my plan again. The plan meets resource constraints and a series of unknown unknowns and it changes yet again. It is finally set. Now comes the implementation, and something else entirely changes. This is a chain of events that are almost never conceived of in the design of the system expressed to generate the transactions. And yet we are called to audit and analyze such strings of transactions all of the time in our analytical applications. Most likely thing that happens? Add an adhoc field to the end of the transaction and have humans interpret that at the end of the day. There have been seven alterations of the planned activity, but you only have three records. The initial plan, the final plan, the actual transaction.

It is on this last point that I was particularly trying to express, recently, the idea that I had to go back and build window functions that created a new semantic layer in to post-processed transaction data and then output that to a user queryable exhibit. It would have been nicer, of course, to put that layer ahead of my DW consumer, neh? So now I should get the chance as we will be, as I said, 'cloudifying a mainframe'. In otherwords re-engineering an IBM MQ based message system with Kafka. This is actually something I've been wanting to do since.. NARDW. (for further reference, put date here.) NARDW was build in 2005? And it's when I scratch-built the workflow for 17 data marts in an ERP integration with IBM guys.

So I've run some basics. I put together and then tore down AWS MSK and a client machine. I also put together a console producer and consumer for a test topic on a new machine in my home setup. Now I've got a couple books to read. See ya.

### The Logos Project

For about 20 years I have been saying that I have 2 or 3 original ideas. Today I'm going to share them in one giant tarball. I'm going to call it the Logos Project. The reason I'm calling it the Logos Project is because of Jordan Peterson's big book Maps of Meaning. It was a very rambly book but it was one that lay behind all of my most profound interests. In one way you could say it represented a reconciliation between faith and reason, which is ultimately the combination of religion and science. What could be more fundamental to the prospects of Western civilization? The one Bible piece I've been able to quote was the beginning of the Book of John. **In the beginning was the word**. And it seems that many of us have abandoned the word, and that needs to be addressed. Social media falls short. We need to build logical media. We need to transform our computer mediated communications into something that serves the purpose of social maintenance of the commons. This is a management problem which is poorly served by the faint number of actions that social media spaces allow us to perform. We are trapped in Twitter because of what Twitter is, and because we have given it over to the builders of Twitter to be the masters of Twitter, Twitter doesn't belong to the people. Anyway, there are a lot of problems like this and the aim of the Logos Project is to solve each and every one of them.

![](https://www.youtube.com/watch?v=tRvERaQAgRM)

This is something I'm ready to contribute to for the rest of my career. And at this moment I am particularly excited about the Intellectual Dark Web, in that they are finally doing what I've been hoping would be done. Of course I've been creating all kinds of content but I couldn't quit my day job. Now is about that time to see if I can integrate all I've been building and thinking into something both concrete and sticky. I'm sure I'll need others to help me pour the concrete, and this teaser is the sticky part. So please do check it out and put in your comments and criticism.

## Categories

- [AWS (24)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20240526115108/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20240526115108/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20240526115108/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |