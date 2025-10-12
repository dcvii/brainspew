---
title: Cubegeek
source: https://web.archive.org/web/20250807070326/https://www.cubegeek.com/
author:
  - "[[Cubegeek 2021-03]]"
published:
created: 2025-10-12
description: Big Data Analytics, perspectives from a 25 year practitioner.
tags:
  - clippings
  - cubegeek
---
The Wayback Machine - https://web.archive.org/web/20250807070326/https://www.cubegeek.com/

### A Barbell Strategy

*The barbell strategy is a risk management and investment approach that involves focusing on the two extremes of a spectrum while avoiding the middle. It's often visualized as a barbell, with weights on either end and nothing in the middle. This strategy can be applied in various contexts, but it's most commonly discussed in finance and risk management.*

I never got introduced to a lot of technical things formally. Back in the 80s when I did my undergrad, systems were much more primitive, limited and you basically had to learn a lot more to do whatever could be done. I was shocked and amazed back in 2010 when I learned that there was a different job for database administrators and database developers. What fresh divided and conquered hell was this?

Yet and still there was so much of computering that I felt I understood in the realms of applications but little that I actually wanted to pursue. So as it turned out, on the technical side, I have not had to look for work since somewhere around 2003. There was always somebody who knew me from my enterprise software stuff, specifically multidimensional database design, development, etc. I grew accustomed to billing $100 per hour on my own and double that working for reputable consulting organizations. Why learn anything more? The only thing new to learn was AWS - but primarily so that I could configure all of the above on my own without the constraints of some customer’s limited on-premise hardware, networks, security, storage and general lack of UNIX literate functional people.

That was then. Now it’s safe to say we are in a programmer’s glut during times of uncertainty.

So I have a barbell strategy. To paraphrase John Boyd shoot for the stars and dig a bomb shelter. In order to be free you can be rich or you can reduce your needs to zero. So I’m putting my 25 years of experience on a resume directed towards making me a director or analytics. I am also building my homelab and becoming the next generation of full stack developer. Crazy right?

As long as people covet data, there will be data pipelines to be dug and maintained. These are the sewers and aqueducts of the next digital generation. It will be structured, unstructured, generated, crowdsourced and scraped. That’s a lot of integration. And since there are millions of coders, there are going to be hundreds of packages and partial solutions. But here’s the other thing. I think as I’ve said before, that enterprise and academic sized problems can be modeled and built by the next generation full stack developer on a homelab.

This past week I started using a few new tools to start building **XRepublic**  and documenting, finally, [the systems I dream of building](https://web.archive.org/web/20250807070326/http://mdcbowen.info/visions/).

**Vue.js**  
I already use Warp which talks to the frontier AIs and I’m very comfortable using o3 for configuration tasks. So basically all of the UNIX admin stuff I never had the patience to memorize I have. I’ve taken the next step and am in the process of choosing between **Cursor**  and  **Windsurf**  for my AI assisted coding. As such I’m having it build modules under Vue.js, but I’m using Typescript and Python. What’s really new for me is having to spin up frontends and backends on different instances. That’s because of something called  **CORS**. I learn something new every week. But one of those is that  **uv**  doesn’t often work well here. I may ditch it. Still, Zed is my primary IDE, and I still use  **Claude 3.7**  along with standalone  **GPT 4o**. I don’t trust any of them; I make them fight it out in front of me. I may have to get Gemini in that battle too.

**Databricks + SAP**  
This either explains a mystery that my old boss saw coming and he kept it from me, or that completely blindsided him. Either way I predict the eventual end of HANA or upping the price of an unnecessarily complex stack; a deeper form of lock in than ever.

**Collate**  
I’m going to use this and/or **OpenMetadata** as my standard. I’ve already got 500+ repos and god knows how many data models. I really have to get my own data catalog working. I admit that this is a cry for help. But that’s the first step, right?

**Dodeca + DuckDB**  
I have completely dropped that ball. I apologize. But I will pick it up. I promise. Speaking of DuckDB, hints are dropping that **Motherduck**  is going to breakthrough distributed ducklings to the next level. I basically am sold and don’t believe there’s anything these guys cannot do. Well, they can’t get the market for ducktitioners like me going fast enough. But I will have 2 years of experience this Christmas. I should actually try out the new connectivity to  **PowerBI**. But I still haven’t figured out ragged dimensional hierarchies. Hmm.

**NSBE Mentorship  
**I should be connecting soon with this year’s mentee\[s\]. I think I have been a good influence and answered a few questions. It has more recently resonated with me how few black American computer science dudes there are. In the whole of my career, after 30 years, I have only worked with fewer than a dozen.

### Eye Candy

![](https://web.archive.org/web/20250807070326im_/https://substackcdn.com/image/fetch/w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc2f1eba4-5dda-4770-8957-64f3521b0ae1_1024x1024.jpeg)

I must confess that there’s a lot of cool stuff out there. If I were a PhD or genuine science-type computer scientist I would be super stoked about the revolution. But since I am a humble practitioner, it’s a bit of hell, especially because I can’t tell which of these hot technologies (or are they cool?) are going to be significant in the market. You know, so I can bank money on it. So here’s a top five, among all of them that I find the most interesting and am going to put the most time and effort into gaining a comprehensive understanding.

**DuckDB**  
This package continues to delight and satisfy. It’s changing my ideas, which you already know, about “Try this at home”. because its extensions are so wonderful. With or without MotherDuck, this thing rocks. Now it turns out that it has a UI built in **and**  it scans DeltaLake  **and** it has something called DuckPGQ.

**SlateDB**  
Just found out about this this morning. Brilliant idea which could obviate S3 Tables. I have particularly liked GBQ because if your data just sits for a long time, it’s cheap to operate. I don’t know why but that’s one of the things I love about it. I’ve been using GBQ to catalog my (small) stuff and paying next to nothing. But if SlateDB does what it claims, then I can keep my stuff in R2 (just recently discovered, and almost as good as B2 or S3) then we get even closer to free.

**DeltaLake & Unity Catalog**  
I just think this is going to be the winner. Databricks is a thought leader and the more they push open standards, the more they will win as well. Still, CockroachDB is more approachable.

**MCP**  
The thing that made the most sense is that data pipelines are going to get more complicated as people kludge AI + ML + DW + Streams. It’s all going to get ugly, but MCP is going to be the next API of the future, even if people are just asking it stupid things. So I think it’s going to be the thing to master in the near term, even though it will be impractical for the next six months.

Now here are the guys I’m reading because I’m just scared not to.

- Daniel Beach at
- Chris at
	[Materialized View](https://web.archive.org/web/20250807070326/https://open.substack.com/pub/materializedview)
- Nate
	[Nate’s Substack](https://web.archive.org/web/20250807070326/https://open.substack.com/pub/natesnewsletter)
	(but what’s up with that hat, dude?)
- [Asianometry](https://web.archive.org/web/20250807070326/https://www.youtube.com/c/Asianometry/videos)
- [AI Explained](https://web.archive.org/web/20250807070326/https://www.youtube.com/@aiexplained-official)

### Restart (Again)

While most of my work is proprietary, I have come into several good reasons for thinking out loud about skills and practice. And since I own this domain, I am doing so as part and parcel of establishing some training 'influencing' in this new and exciting (and confusing) time in all things data. So I will be talking about MCP and data cataloging and small (monolithic DuckDB) data. In the short term you can alternate between here at Tessellations which is going to be some duplication back and forth, because data and publication is cheap.

### It Begins Again

Ah. So many changes, so little time.

I think that when I look at all of the things I've learned about myself and technology over my career it is that there are two things I love the most. The first is having my hands on good technology and building a system everybody is proud of. The second is sitting down with project sponsors and proving to them that the technology I am selling absolutely does what I say it can do.

Before I do the second thing, I generally need to do the first thing. But the industry has changed. More of these components have goodies built for them or with them in mind to make all of that building so easy that it is almost unnecessary. On the other hand, there is so much more variety, size and shape of data to be integrated into new architectures that what was once simple implementation has become much more complex. This is especially the case with security and privacy concerns.

What I'm doing these days is taking what I have learned in DevOps and shrink wrapping it around my favorite database, which is Vertica. It has the most powerful engine for data warehousing. Data warehousing is still the king of structured data. And the toolset for structuring up unstructured data is improving all the time. So I'm going to go with structure. No surprise there. What it surprising is the extent to which the speed of data transformation can take place. I'm talking about Kafka, which is still a bit clumsy, but capable of great things.

Of course you know I have to talk about LLMs. Well all I'm going to say is the following. I find it difficult to believe that LLMs as a service will not pop up everywhere. For me, the trick is to find a way for individual companies, especially large ones, to enable private LLMs to become referential to every pool of data they own. In other words, this thing I'm coming to understand as Prompt Engineering will soon become the most extraordinary UI ever, and a lot of interactive prompting and responding with become the SQL of the future. So I'm looking at the probabilities of architecting NLP interactive stuff to bring back references to curated structured data.

### Boxtag 060 - Lurkers, Scribbling & Proxy

There are three edge cases to end of life exits of a named member on Boxtag.

The first is **lurking**. A member may choose to go dark or participate at a low level with a limited number of weigh-ins on a comment. If they volunteer to do so, it should be indicated in their profile and perhaps visually with their visible votes / weigh-ins on comments. Six months is a reasonable period for them to be inactive without changing their status. Lurking periods may be recorded if it can be done efficiently.

The second is **proxy**. A proxy is a high level change of ownership of the member. In order to preserve the anonymity of someone who wishes to disown their prior comments and votes, they may elect to proxy to an anonymous identity. In this case, in order to preserve the integrity of conversations, the ownership of those comments and votes is turned over to the system. An anonymized account is given as the pseudonym of the member and all PII associated with the original member is erased and delinked. While someone might make a screenshot of an original comment or a person might become notorious for a comment attributed to them before the proxy, the system will not allow that to be proven.

The final is the **scribble**. A scribble essentially is a non-reversible disconnection of OPs, comments and votes from their contexts. (Votes? box-votes? ). In the case of a scribble, the original content will be preserved, but all comments are delinked from OPs and votes given and received are deactivated from tallies. Essentially the system will have to recalculate the dimensional scores of all entities. This recalculation is something done regularly so those associated with scribbling should not be taxing on the system.

### Boxtag Idea #059 - Highlights

Hat tip to Alok on this piece. This feature is all about parsing through the text of a comment or an OP that allows a critic / commenter to be more specific about his votes in the Boxtag. It should work like the highlighting function of the Kindle app that allows that. It makes sense that extended annotations can generate new content and that can be established in a proper UI. However there should be some limit. I'm happy to make the limit along the lines of whatever it might have been in Nelson's Xanadu.

It occurs to me as I visualize that the inheritance of 'subtexts' can be navigated through on a left-side panel which resembles the pages of a PDF file as a multipart entity. The way this displays in Mac Preview (several versions up to and including Big Sur) is illustrative. So the new OP, which is a comment, displays front and center. Annotations are on the right-side panel and mousing over them highlights the highlighted text. This would be similar to how such annotations are done in Google Docs. The point is that we extend the critical range beyond the OP into the comments. But we also extend the critical range of the OP itself by allowing people to highlight its strong, weak and off-topic points.

### Boxtag Idea #058 - The Greylist

I just attended the Bellingcat / Persuasion / RDI webcast and a perfect extension to Boxtag occurred to me. Right now I'll call it the greylist.

There's a battle against ad spam and spam in general. But right now the corpuses built are strictly black and white. How about a greylist? What if we added Boxtag karma components to OPs and comments and attached those metadata to corpuses of email addresses? Well that's the basic idea. This means that there needs to be a backlink to certifiably credible documents in some evidentiary chain, but once this is established it would only grow. The first customer for this will be organizations like Bellingcat, but also the circle of independent journalists and NGOs and ex-officio individuals associated with doing all of this.

A good model might be a different way of parsing out IMDB as a test corpus. I've done it many times - you look to find what movies a particular star, or even a particular second unit director is associated with. Wouldn't it be cool to do the same thing by adding their critics into the mix. Well David Denby said X about this film. An easy tangent would be to connect these up to Golden Globe and Academy Awards. So that's the basic idea. Expand the reach of Boxtag karma components to various corpuses and establish gradations of credibility that reach beyond a single website's comment section and trace back to registered dimensions. (Ultimately these registered dimensions will be the IP, rather like Pantone registers colors. We can have many shades of the dimensions of credibility and interest).

### Boxtag Idea #057

These days I am doing double duty, reaching out to individuals through Clubhouse and Lunchclub to extend my reach surrounding the subjects of the Logos Project as well as my daily duties for Full 360. I have been pleased with the reception, from polite to enthusiastic, I have received for various aspects of Logos. One person has gotten deep into the current (raggedy) state of prototyping for XRepublic and several have considered the implications for Boxtag. But I have to give full marks to Sumeet R. for recognizing something about Boxtag that I never considered.

I'll get more into Boxtag as time goes by for those who don't know it beyond the idea of 'multidimensional karma for comments' over time. As much as I'd like to spend my early retirement building the entire thing myself, various economic dislocations and personal miscalculations have made early retirement a diminishing possibility. So I'm being as open as someone non-famous can be. Thus the revival of Cubegeek and the upcoming establishment of the Logos Group however small it may be. Never underestimate the power of one man and twelve disciples.

At any rate, Sumeet related a story about the difficulties with meta-moderation at StackOverflow, with some note about how a subject may be answered and the frozen, or some response might be considered out of bounds. Whether or not Boxtag was originally implemented at StackOverflow, it can be implemented in retrospect which allows meta-moderation over and along with the original one dimensional karma system. Boxtag itself will offer incentives for postfacto meta-moderation in a way 'similar' to that of Wikipedia so that subjects that are considered 'dead' may come to life once again. This will be especially useful in **solving the oracle problem**. It can be crowdsourced if meta-moderation is done right. We think Boxtag will be meta-moderation done right.

Thanks Sumeet. You're brilliant.

### Revival

It has been a while. I will update Cubegeek as I continue doing mealy-mouthed development and discoveries like those reaction videos. Ooh look what's so cool about the Rust compiler. So anyway. This is newly dedicated to the people I am reaching out to in order to get any traction possible for my Logos Projects - as long as it takes for that to happen.

What's going on these days? My company has pivoted from primarily managed services to product + professional services. This allows us to consider more customers despite the fact that we are picky and competitive. The good news is that we've passed our latest ISO 27K audit with sprinting colors (they weren't quite flying but they set an admirable pace.) This means we can indeed take on a more significant class of customers as we've always wanted to do. BTW this is our third years passing. For me that means more work in the columnar space. Since MFGP just signed an agreement with AWS, stuff can start popping (including the stock). That means it will be great for me to get back deep into the internals of Vertica, as I did in 2012, and help workloads scream.

On the Logos front, I've enjoyed the reactions I've gotten from the folks I talk to, and I'm encouraged to push forward. So I need to do a bit more drawing on UI and perhaps as I become fluent in React, while it's still relevant, I can make a shell around my database models. Or maybe I'll stick to the database models. As we move forward with eDW and integrate **Singer** and **dbt**, stuff will go a lot faster. So I aim to put up something at least once a week here. That will keep me focused.

### Day 17

I discovered Urbit today. I have always been here. I have just discovered the other people who think like me. I'm not trying to be afraid that this is very much what I've been all about for quite some time, but I think perhaps I can have some cred as these entities get to know me. This is day 17, arbitrarily, of my new engergy and dedication to building this world I have envisioned. I am so pleased to find that Urbit suits my purposes rather exactly as I had hoped someone would. So I'm there. I'll let you know what planet I'm on as soon as I understand this universe a little bit better.

[Next »](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/page/2/)

## Categories

- [AWS (24)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/aws/)
- [Best Practices (47)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/current_affairs/)
- [DB Tech (4)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (75)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20250807070326/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20250807070326/https://www.typepad.com/ "TypePad")

## Search

## May 2025

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  | 1 | 2 | 3 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| [11](https://web.archive.org/web/20250807070326/https://www.cubegeek.com/2025/05/a-barbell-strategy.html) | 12 | 13 | 14 | 15 | 16 | 17 |
| 18 | 19 | 20 | 21 | 22 | 23 | 24 |
| 25 | 26 | 27 | 28 | 29 | 30 | 31 |