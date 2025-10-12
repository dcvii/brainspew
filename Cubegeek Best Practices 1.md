---
title: Cubegeek Best Practices 1
source: https://web.archive.org/web/20250615175312/https://www.cubegeek.com/best_practices/
author:
  - "[[Writings/Cubegeek]]"
published:
created: 2025-10-12
description: Big Data Analytics, perspectives from a 25 year practitioner.
tags:
  - cubegeek
---
The Wayback Machine - https://web.archive.org/web/20250615175312/https://www.cubegeek.com/best\_practices/

### Restart (Again)

While most of my work is proprietary, I have come into several good reasons for thinking out loud about skills and practice. And since I own this domain, I am doing so as part and parcel of establishing some training 'influencing' in this new and exciting (and confusing) time in all things data. So I will be talking about MCP and data cataloging and small (monolithic DuckDB) data. In the short term you can alternate between here at Tessellations which is going to be some duplication back and forth, because data and publication is cheap.

### Deep Variances in Essbase

(from the archives - Fall 1996)

In my travels, I have just come upon a neat trick. I've never seen it posted anywhere and it solves a problem I remember being unable to solve a few years ago.

Consider a simple model with a geographic dimension 5 levels deep, a measures dimension of sales, and a scenario dimension with actual, plan and variance. How can I get the model to indicate 'deep variances' without having to drill down to them if my high level variances are within spec?

Create 'red flag' and '%red flags' in the scenario dimension.

Let's say that I have a 10% absolute value variance tolerance set.

The member formula for redflag would be

```
if (@abs(variance%>=10)
    redflag = 1;
else
    redflag = 0;
endif
```

Create a 'neutral flag' member in the variance dimension and hardcode the member formula to be 1;

```
redflag% = redflag % neutralflag; (two pass)
```

| geo | actual | plan | variance | variance% | redflag | redflag% |
| --- | --- | --- | --- | --- | --- | --- |
| NY | 100 | 115 | (15) | (15%) | 1 | 100% |
| NJ | 100 | 97 | 3 | 3% | 0 | 0% |
| CT | 100 | 85 | 15 | 15% | 1 | 100% |
| East | 300 | 297 | 3 | 1% | 2 | 67% |

Notice that even though your high level variance is only 1%, 67% of your lower level forecasts are out of bounds with two red flags.

simple, neat.

### Amazon as Conglomerate

Here's the highlight reel. When Peter Drucker invented the MBA part of the idea of professional business management was that ordinary individuals could be trained to run a business. Not a generalized business, but a specialized business in some category. (NAICS codes). The way Harvard has been teaching case studies was that within the scope of business and product analysis such a cadre would be measured and their public company made an indicator by P&L and balance sheet metrics to the public shareholders. IE, IBM competes in its NAICS sector, becomes a market leader taking product share away from competitors, then you know to buy the IBM ticker. All the analysis is around product competition and market share and the effectiveness of management has everything to do with its ability to execute in that narrow area.

So there are only a few management teams, relatively speaking, who know how to make a company profitable on narrow profit margins. A conglomerate can have a balanced portfolio of businesses that won't suffer the business cycle. That's how Berkshire Hathaway makes money. By running multiple businesses in different NAICS and not making their whole company dependent on a killer app. Each of these businesses, after a time, contribute to a large pool of funds that allows the directors to make experimental buys in new areas, instead of mergers in the same area. Bezos has said specifically that Amazon can afford to make billion dollar mistakes, because the underlying businesses are already fully capitalized and don't need to keep growing or be leveraged before they are mature.

People have wanted AWS to be spun off from Amazon for years, and Wall Street has been hedging on the stock price because before it became a market leader, he never broke out it's P&L and balance sheet from the whole of the company. Wall Street for the most part doesn't know how to do company management analysis either. That's why index funds are winning. Anyway, conglomerates are safer from hostile takeovers because the executives actually understand how to run their businesses and there is no incentive to sell out the business. That's why a class of Silicon Valley VCs and entrepreneurs loathe the idea of working for Amazon. There's no exit strategy. You don't exit conglomerates. They scale horizontally.

It's interesting how well Bezos has run it as a conglomerate, given the bad news recently about GE. I don't think, outside of P&G, that most Americans understand conglomerates. So I'm hoping that Amazon does a stock split and gets listed on the Dow.

### How To Cloud A Mainframe

[![Mainframe](https://web.archive.org/web/20250615175312im_/https://cobb.typepad.com/.a/6a00d834515ae969e201b7c92b58ff970b-320wi "Mainframe")](https://web.archive.org/web/20250615175312/http://cobb.typepad.com/.a/6a00d834515ae969e201b7c92b58ff970b-popup) Once upon a time there was a mainframe computer. I ignored it. So did you. We were wrong.

My mighty mainframe was a CDC Cyber running NOS. It was such a craptastic machine that I hated doing homework precisely because the damned thing wasn't reliable enough for me to slack off until I was ready. Surely when I got into a groove of programming in fricking ADA, it would be broke. I hated my college's datacenter and the frogs who worked there. It was enough to make me love microcode and BNF. But that was 30 years ago, literally. Nevertheless, it left a bad taste in my mouth particularly because I loved DEC Vaxen and client server. After all, I did work at Xerox.

But while I was at the big X, I did come to love and appreciate VM/CMS. What a cool idea. And there was always a weird kind of appeal to ISPF, I have to say. Plus it was also very cool to use a channel attached Overland Data tape drive that worked with IND$FILE. Ok enough reminiscing. We all know that IBM was an early embracer of Linux, and became even cool again when I read about something called a Beowolf cluster of Linux nodes running on a System 390. And of course the RS 6000. Yada. Yeah. They understand hardware. I even listened up to the time when they started on about The Grid and grid computing in general. Why? Because I have always been a big data fanatic. Ok, devotee.

So this morning I'm talking to my engineering manager colleague down in LATAM and he's helping me to understand what sharp elements of his team have been doing over the past few years. I know a bit about it, but now I'm responsible to communicate that. Non trivial. It turns out that they've essentially been packing puffy clouds around mainframes. Huh? What?

***We have come up with a way to put legacy mainframe data systems into cloud native architectures.***

One of the things we do is work with airlines. I don't have to tell you again. You know. And a whole lot of airline reservation information, flight routing, frequent flyer currency, etc are on a multiplicity of divergent systems and architectures. We don't have patience with all of that. We're a systems integrator doing what needs doing in the AWS cloud. Of course a lot of this data is deeply embedded in complex systems that it will never make sense to re-engineer. So we said, leave it where it stands. We built stuff around it. Our offerings are called **API Modernization** and **Middleware Modernization Blueprint**. And what we've been able to do is engineer and rationalize what lives best where in an extended hybrid cloud environment. One of the things we've done is applied [Scala Akka](https://web.archive.org/web/20250615175312/https://akka.io/) frameworks to create RESTful interfaces and [GraphQL](https://web.archive.org/web/20250615175312/http://graphql.org/)  to smooth out the rough edges of ancient mainframe subsystems and scale them up to deal with the new real world of cloud & webscale applications. Another thing we've done is take complex business rule logic which was once a legacy monolith, generalized and retooled it to work in multiple applications. We've augmented or replaced IBM MQ message queues and worked them into both Kafka and Kinesis. We prefer the headache free [Kinesis](https://web.archive.org/web/20250615175312/https://aws.amazon.com/kinesis/). We don't have patience with zookeeping. Naturally, we've used the power of Cloudwatch to provide more reliable and customizable system monitoring capabilities, and of course we've used the power of AWS Availability Zones to make the whole thing robust against failure. So yeah, we can think of your mainframes as a middleware component in our ever-evolving data management architecture.

Obviously this is not cutting and pasting technology. It requires deep thought, patience and understanding. We've got our share of that and it's working out nicely. It's not easy to communicate all of those details, but I wanted to give you a heads up so you could consider some of the interesting directions our quest for data perfection has taken us. It has taken us back to the legacy of centralized computing, and we have recast that command and control to fit into contemporary cloud architecture. What a journey. Hey mainframe, we're pals again.

### It's Not About the Chart

I think many people are unaware of the fact that data analysis is designed to establish a broad consensus and that consensus is supposed to reflect an approximation of reality over time.

That means firstly that everyone must be reminded that they are modeling reality, not representing reality. There are assumptions about the model which need to be kept in mind. If these assumptions are not appropriately understood and well communicated, there is likely to be discord in the ‘now what?’ phase of decision making.

This also means that assumptions may change, and reality may change. So new models must be made. Older ones should not necessarily be discarded, but remembered as heresies against the new regime. There is always value in studying heresies because one cannot always validate assumptions and certain assumptions may revert back over time.

When people are focused on charts and graphics and technologies without paying attention to the process and social dynamics of decision making, they are only seeing a fraction of the problem they are trying to solve. These are the reasons why aphorisms exist like:

*"There are three kinds of* *lies**:* *lies**, damned* *lies, and statistics**."*

The most difficult and vexing questions to answer are:  
1\. What were we thinking when we made that decision?  
2\. Who knew what and when did they know it?  
3\. Why were we not paying attention to X?

These questions always show up in the wake of a disaster, and the inability for people to address them shows the incompleteness of their thinking around the matter of modeling a changing reality, establishing consensus, and keeping track of the appropriateness of assumptions.

In other words, governance of the decision making process is very valuable and often overlooked (or assumed to be automatic) when a system of analysis is successfully put in place.

### The Functional Revolution

[![The_high_queen_by_chriscold-d4zub1s](https://web.archive.org/web/20250615175312im_/https://cobb.typepad.com/.a/6a00d834515ae969e201b7c8bac45d970b-320wi "The_high_queen_by_chriscold-d4zub1s")](https://web.archive.org/web/20250615175312/http://cobb.typepad.com/.a/6a00d834515ae969e201b7c8bac45d970b-popup) A couple weeks ago, something profound occurred to me about enterprise software. I realized that when it is priced by server or by processor, that it's a ripoff. When it is priced by data usage, it's a bargain. You are paying for the potential of being able to use 8 cores even when you are not using them. Admittedly this is rather easy to see if you have experience working in the cloud and then take a turn doing on-premise practices, but it seemed rather profound to me. Imagine, if this is not obvious to you, that you pay a standard or premium license fee to your mobile phone carrier based upon whether you are using a brand new smartphone or an old one. Right. It makes no sense to pay money for anything but the minutes you use on the phone. Mobile phone billing is done right. You pay for minutes. All software could be that way, so that you're not paying for servers, but for functions that spring to life do your bidding, charge you a fractional penny and then die.

This week my boss sent me a link to a guy named **swardley** who likes ducks. It turns out that this character is quite capable of blowing my tiny mind. He's done it twice already, and so now I have the burden of a speck of enlightenment. It is an enlightenment which is commensurate with my understanding of (Wladawsky-Berger 1999) n-tier computing and then (Vogels 2008) horizontal scaling. So since I've been doing cloud for six years, I now understand what's happening next. God save us all.

Tying software development to economics and cost accounting has long been the stuff of magic, SWAG and charlatans. At least that's what it seemed like for most of my career. But I think Simon Wardley has the solution. He has outlined an ecosystem and a framework for understanding how one can iterate (captive) algorithms towards mutual value for the developers and the customers. He calls it FinDev.

Like most useful thinking on the progressive edge of IT, one must assume AWS. That is to say, very little of what exists in the world that is not part of AWS's ecosystem can be thought of as having great potential in the future of computing. AWS is beyond doing things very well, they are evolving at a monstrous pace and at enormous scale. As an aside, I asked some Agilists last night at El Torito why Amazon manages its businesses so well. He said it's because Amazon is a collection of relatively small businesses that work on a common billing system, and that's what keeps it simple to manage. They are not only eating, but profiting from their own dogfood, which is the fully meticulous tracking of compute resource costing, and now with Lambda, down to the function. All the hardware is a sunk cost. Cloud computing is a utility. What matters now is billing by the function. Simply assume the cloud. It's already done.

So there is a scary aspect to this which is something we all should have been afraid of all the time. It is what happens to craft when things become industrialized. Your personal touch matters less in a market which is defined towards optimization, cost-cutting and efficiency. Nobody cares how you show off the horse, we're all driving cars now. Nobody cares about your budget system, we're all using SAP now. Nobody cares about your fat client, we're all using browsers now. What's coming is a COTS revolution in which your college professor optimized the Towers of Hanoi solver and now owns the moneyTicker on the algo. In a global library of cloud interoperable functions, the scope of what you get to work on gets narrower and narrower. The good news is that we are 20 years away from lockdown. The V8 of compute engine economies is invented. Say hello to the next 50 years. You Wankels don't stand a chance. When I was an undergrad, I used to think of software as the same thing as law. There are lots and lots of lawyers but only a few legislators. The assumption was that the best lawyers at some point got to legislate and the rest just interpreted and borrowed citations for the benefit of those who never read the law. I believe there will be some measure of *stare decisis* in the new FinDev ecosystem.

So the future belongs to engineers who really know their customer's needs. The economy of FinDev provides value to developers and customers only to the extent that something can be built (at scale in the cloud) that customers want to use. When you charge by the use, that's a different business model than anything we've seen. Chances are it will be disruptive because it will go after captive inefficiently spent money. But there's greenfield out there too. More hopefully, there are new places computing can and will go once we wean ourselves from the economics of capacity planning, system depreciation, outsourced consulting and all that. I think AWS will be capable enough to handle global innovation in this regard; they're certainly leading. Now is the time to work our way towards best practices, evolving towards the revolution.

keyword: REDQUEEN

memetics:

In Martin Cruz Smith's Arkady Renko series, the protagonist, Renko informally adopts an orphan who is a chess genius. Playing at the genius level, the kid doesn't require a board or pieces. He, and those like him, can just recite moves. He has a virtual queen and doesn't even need hardware. If you're thinking about physically moving pieces, you're not playing chess.

### A Old Step Towards Anonymity

COINTELPRO

It's probably the most famous classified operation of the US Security agencies known to man. At the moment the details are hazy to me, though known to be sinister and sneaky. Of course that's what intelligence services do. So what else is new? Well, what's new is that [Black Mirror](https://web.archive.org/web/20250615175312/https://en.wikipedia.org/wiki/Black_Mirror) is showing some of the possibly dystopian consequences of what we know these new technologies might unleash on society given the new ubiquity of powerful IT tools and techniques. We're kind of sliding into it sideways without, I think, an adequate amount of useful terminology in the public mind.

So let me slide sideways a minute and go back to 9/11. When that happened, I was hanging out with a group called Brainstorms, and one of the members of the group was connected to the intelligence community. We asked this dude to help us understand what we have now come to know as 'asymmetrical warfare' and it was very difficult to get straight answers. That was a combination of his commitment to secrecy and our relative ignorance of the context of the intel warrior's job. Well one of the things that is very difficult to grasp is how many tens of thousands of programmers there are who now understand and have access to the kind of technology the intelligence services deploy. The asymmetrical warfare of small, agile coders with excellent software is on the other foot, as it were. The short term advantage is with the little guy.

So it occurs to me that as I get better at securing data for my clients, I should add a level of abstraction. Especially when it comes to describing best practices, it's very useful over the long term to talk about the customer in a way that isolates them. So I'm going to help anonymize my customers by giving their projects codenames. Nothing particulary spooky but spookish nonetheless.

So now I can tell you about

- GREENRIVER
- DOGLEG
- HIGHSTICK

without having to kill you.

### Wonking Through Consul Constellations

I first heard of **[Consul](https://web.archive.org/web/20250615175312/https://www.consul.io/)** sitting over a wooden table in New Orleans three summers ago. I understood about 27.5% of what was being said, but the fact that it was said with such excitement was clearly impressive. I know more now of what I didn't know, but did appreciate then.

My task now is to roll my own fractional Cloudwatch. I am on-premise and have several clusters of sharded databases to look after, many of whose nodes can be flaky. So I've set up a datacenter in consul to keep multiple eyes on multiple services, including NFS. I have a combination of RHEL and Centos servers as well as a Mac and a couple virtual Ubuntus to help me out. It turns out that I am hesitating in writing everything in **bash.** But I don't want to pull down a full kit of Ruby based containerized apps, even though it would help me digest working with json everywhere. So there's that. I'm also working with **consul-alerts**, a third-party Go app I've installed on my Mac. It's a bit much to learn the fundaments of Go, but now that I've stepped up my VM game, I'm not so afraid to experiment. My customers are staffing up to make moves into [DevOps](https://web.archive.org/web/20250615175312/https://en.wikipedia.org/wiki/DevOps "DevOps"), so there is a growing coterie here of people who can appreciate the various fruits of the.io trees out there, but still many of them are forbidden. I've already done a simple **Slack** integration, but Slack is unknown to this enterprise. I tread slowly.

In the meantime, I am appreciating yet again, the other side of the business I've been engaging for decades. The duality of operations which, like war, consists of long periods of boredom punctuated by moments of sheer terror. Hedging against the terror is the 80/20 risk management, complicated by the political arcanities of the budgeting process. It's a different kind of sanity, I'll tell you that.

I'm learning how much I may actually come to appreciate HTTP APIs. Jury is still out, but I already love KV stores. More later.

### Vertica Idempotent Set Transformational Denormalized Design Standards

At Full360, we have developed a best practice around our design of greenfield and re-engineered DW applications. The following is a high level guide to how we accomplish this in Vertica. Vertica optimization is something we have pursued with vigor at Full360. There are several different levels at which this can be pursued. Implicit is the modularization of the applications so that the major functions of our data management philosophy can be expressed discretely. But let's get to the $10 words, shall we?

**Idempotency**  
Both I and JDub could go on at to absurd lengths about how important this is to the modularizationf DW design. I will simply, which characteristic casualness, tell you that it makes all of our stuff idiot proof, in that it makes our data provision dependencies kind of go away. The basic idea is that *in application units* (which basically means the chunks at which the data to be consumed makes process and business sense) you make your input streams discrete. So when your input streams are discretely chunked, you can run your process over and over without concern about whether it has been done once, twice or never. You just run that independent data provision job and it creates the right sized bucket of data.

**Set Transformational**  
VLDB folks are probably familiar with why you do ELT rather than ETL. The simple way of saying it is that database developers are more stingy and efficient with data than ETL developers. I developed a taste for hand-crafted 'ETL' back in the days when Informatica was a baby, and having my Unix biases, I always loved moving files around. At the time, my focus was on Essbase which had not ETL hooks, even though Arbor should have purchased an ETL company cheap. Interestingly tangential, Wall Street has never been very long in ETL companies. Anyway, I expect that Informatica and Talend will not like to hear that their days are numbered, but then neither did Carleton and DataStage, and they used to rule the world. The bottom line is that moving data from table to table using SQL rather than in a GUI that does not is going to be, in certain databases, much faster and more human readable than in third party tools. So we do set transformation, and even regex stuff, inside Vertica. One day we may even benchmark UDFs against external programs.

**Denormalized**  
Vertica like Redshift is not a transaction database. It is columnar and it easily handles 600, 800, 1200 column tables. It was designed to. So there is no reason to do a lot of silly little joins in silly little tables to get juicy fat data. We make all that part of the ingestion process, which gives us what we want. Think about it for a minute. Consider the volatility of lookup tables and dimensions as compared to the volatility of atomic facts and transactions, aggregated or otherwise. The facts will be bigger and more fluid. So why spend join energy on query exhibits over the long haul when you can easily have all the columns you want? You don't have to. There are no table scans from hell, that's what columnar solves. So we go big.

\--

**Production**  
I'm not going to talk about the guts of Production other than to mention it briefly here. Production is some of the genius and we have a bag of tricks that is ever-expanding as we deal with realtime, near-realtime, and other odd types of data sources. Yes we lambda with streams and lakes, but we smart lambda. Again with whatever tech makes sense. Right now we're playing with Kinesis and Kafka and our own custom Actor models which we're sure will evolve over time. We're also looking at how to use Redis and other superfast KV stores. So I suspect we will grow many efficient tentacles as we Produce standardized data for ingestion into our columnar DW apps. Nuff said.

### Ingestion

#### \_SRC

We ingest data into source tables for each schema as they come to us. No matter how many fields, large or small, we will take them in using a COPY from produced files. Whether in Vertica or Redshift we standardize on UTF-8 with vertical bars delimited and a backslash escape. In some cases, if we've munged up variable length stuff from our own custom regex routines or other JSON, AVRO or semi-structured effluvia, we will have an additional pre-step using Vertica Flex Tables. We are coming up with best practices there too.

These source files should also retain the original names of the fields of the produced data when possible. This assists in debugging with the original developers.

#### \_STG

All of the data that is to be used in the application should then be mapped to a view. This is the staged data. Staged data should be of the increment of ingestion (discretely chunked in application consumption units). That is to say that your \_SRC and \_STG will carry the same number of records although they are likely to carry a different number of fields once the ingestion is done.

### Transformation

#### \_CLN

The clean tables should be materialized tables with human-readable fields that are conceptually discrete. This is generally accomplished through a direct insert from one or more \_STG views. Clean tables can be defined with blank fields for further rule application. Clean tables that contain all history for the query space should have the term \_HIST\_CLN, otherwise one should assume that a clean table is the same size as an ingestion increment. Clean tables should be optimized for the scope of the transactions that take place in their creation. When you are looking at the clean tables, you have all of the data you need from all of the sources presented in the way you as a developer think about the data. There should be very little ambiguity at this point, it's your best look at the details before they are aggregated and rationalized.

#### \_LKP

Lookup tables are straightforward. They should be optimized for their transaction capacity with clean tables.

#### \_IFT

In a complex model, clean tables can be made into Intermediate Fact tables. The intermediate fact tables are materialized tables with all of the necessary dimensions that support measures that can be made across the full query space. These may or may not be exhibited directly, but should be useful in a partial analysis of the particular measures they contain. An intermediate fact table should be the place where window functions are applied. They should be the place where obscure field conditions are made into explicit attribute and status fields. It is important to know that an application may have dependencies of different measures that seem to be dimensionally equivalent, but actually aren't. So by using IFTs we unburden ourselves of the very idea of a single massive star or snowflake that might have holes. Also, we can capture all of the attributes of a set of measures completely without concerning ourselves with the weight of them in the final presentation layer.

So think about this. A clean look of the data will probably not have sensible status fields they will have codes. There may be multiple ways to interpret a certain combination of fields. So whatever you need to support a the full scope of consumable data, even if it means synthetically remastering transactions, you can do with IFTs beforehand. Building these are the real guts of the DW application, and it's where the fun of working with sharp analysts come in, especially when it comes to data integration projects. I will apply all of the reasonable and semi-reasonable business rules here. This is where I have enough detail to point machine learning, because at this point the data is explicit and human readable. It will reveal the more interesting cases and outliers. And here it should be very rich - beyond human comprehension, so yeah maybe you don't go full wide with these tables, only add 4 of the 50 psychographic customer tags you have against their ID, because, security.

#### \_XBT

Exhibit tables are materialized views in some cases but generally views that are presentable to the end user. These should be indexed and optimized for query retrieval. Security access rules are applied to user groups, etc only to exhibit tables. It should be assumed that none other than dbadmin processes will have access to any tables or views but the exhibit tables.

\--

So there it is. This is rather the state of the art that I have internalized in five years of cloud based columnar data warehousing. Maybe I should write a book.

### A Quick Review of AWS Questions

I just put together a quick casual video covering five questions about trends in markets and customers that we're seeing. It's nice to see that our experience is exactly dovetailing with theresearch put out by Gartner's latest Magic Quadrant

.![](https://www.youtube.com/watch?v=mnUzsOd3Dj0) [![Screenshot 2016-08-05 14.51.43](https://web.archive.org/web/20250615175312im_/https://cobb.typepad.com/.a/6a00d834515ae969e201bb09273d8d970d-320wi "Screenshot 2016-08-05 14.51.43")](https://web.archive.org/web/20250615175312/http://cobb.typepad.com/.a/6a00d834515ae969e201bb09273d8d970d-popup)

[Next »](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/best_practices/page/2/)

## Categories

- [AWS (24)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/aws/)
- [Best Practices (47)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/current_affairs/)
- [DB Tech (4)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (75)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20250615175312/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20250615175312/https://www.typepad.com/ "TypePad")

## Search

## May 2025

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  | 1 | 2 | 3 |
| 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| [11](https://web.archive.org/web/20250615175312/https://www.cubegeek.com/2025/05/a-barbell-strategy.html) | 12 | 13 | 14 | 15 | 16 | 17 |
| 18 | 19 | 20 | 21 | 22 | 23 | 24 |
| 25 | 26 | 27 | 28 | 29 | 30 | 31 |