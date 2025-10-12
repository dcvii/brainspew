---
title: Cubegeek AWS 2
source: https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/page/2/
author:
  - "[[Writings/Cubegeek]]"
published:
created: 2025-10-12
description: Big Data Analytics, perspectives from a 25 year practitioner.
tags:
  - cubegeek
---
The Wayback Machine - https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/page/2/

### Fast Data in the AWS Cloud with VoltDB and Full360

[![Panigale-1_2139601b](https://web.archive.org/web/20240526111507im_/https://cobb.typepad.com/.a/6a00d834515ae969e201b7c85ed42c970b-320wi "Panigale-1_2139601b")](https://web.archive.org/web/20240526111507/http://cobb.typepad.com/.a/6a00d834515ae969e201b7c85ed42c970b-popup) Here's a link to the webinar I did last week with VoltDB. Having Volt as part of our architecture has enabled us to think about a whole new class of applications. Right now, I would say that we're at the point where we're really ready to deal with massive IOT streams. It's just a matter of getting the right people together. These days I'm brainstorming this kind of stuff, excited as I am by looking at real-time events and figuring out what I need to drive those data dogies.

[Fast Data Choices: 5 Strategies for Evaluating Alternative Business and Technology Options](https://web.archive.org/web/20240526111507/https://voltdb.com/resources/video/fast-data-choices-5-strategies-evaluating-alternative-business-and-technology#sthash.am8PMgH3.uzbe "Fast Data Choices: 5 Strategies for Evaluating Alternative Business and Technology Options").

In this presentation I talk about three different apps that are part of our Fast Data portfolio. All of them are real customers using this technology in production as part of Full360's manage service offerings. We designed these apps and built them as well. All of them run securely and reliably in AWS VPCs and customers love them. These are exemplary of our multi-tier DW framework that we call elasticBI. Why Panigale? Because this is all about making very fast decisions in real time. A second late is too late.

### Dreaming About Streaming

One of the brilliant things about working closer to the technology as I do at Full360 is that every once in a while you get to see things in a completely different light once you know that you have a certain capability. Right now, I do a lot more thinking about transactions per second and streaming real time data. So I am extending this thinking primarily through **Amazon Kinesis** and **VoltDB**. I'm only halfway through the exercise of building a prototype for a new demo I'm thinking about but it's the thinking about applications that's most interesting to me now.

A couple weeks ago I presented a webinar in which I discussed one of our realtime apps which is attached to online gaming. On the back end of this architecture we are processing about 30,000 transactions per minute with a small two shard cluster of VoltDB. This setup hardly makes a peep over 25% CPU utilization running 24/7 with no downtime in two years. Cool enough, but then you realize that is handling more mobile transactions per year than PayPal. I did the math. And oh what fun it is to do this kind of math and realize what's computable for the kind of analytic data frameworks we build.

So what about telephone calls? Well there are about 10M people in LA County and according to some research I did, they make and average of 10-15 phone calls a day. That's 150M transactions per day, divided by 86400 (86400 being a new number I think about: the number of seconds in a day) gives me an average just under 1800 TPS. That's a decent enough stream, but really not difficult for Volt to handle, since I know Volt has a massive ingestion capacity and nice interfaces to stuff like Kafka, and Kinesis can be thought of as a flavor of Kafka. My idea here is to design a multi-tier database framework using Volt and Vertica that employs a lambda style architecture for two levels of analysis. The example is a terrorist watchlist. I've picked this example because it's something that is memorable and it offers a lot of interesting details along the way.

So first a couple clarifications.

If we chunk fast data processing down into three classes, let's call them real-time, streaming, and micro batching. I have come upon this distinction in the process of building a fake data engine for my application. My engine is a sensor and that sensor is something I have embedded in the telephone infrastructure. Using the [Cisco Unified Communications Manager](https://web.archive.org/web/20240526111507/http://www.cisco.com/c/en/us/td/docs/voice_ip_comm/cucm/service/7_1_2/cdrdef/cdradmin/cdrex.html#wp1250441) standard release 7.1 as the basis, I have identified the CDRs. Call detail records will tell me who is calling whom and for how long they speak. In researching this, I discovered another way to think about 'big data', It turns out that these CDR databases are flatfiles and they can contain a max of 2 million records or 6GB large. But I'm not going to batch out those big suckers, I'm going to tail them and spit them out record by record.

A real-time system is something I generally would say is something purpose built, IE there's a special OS kernel that does not interrupt the main job of the software. So basically embedded systems, right? Anything that's not software purpose built for hardware that too is purpose built is streaming at best. That's the conceptual distinction in my mind and I like that. Practically speaking, you can stream at 10ms increments, or even down to 2 or 3ms which is pretty damned near real time, but it's actually not a real-time system from our POV because we're doing analytics, not onboard AI. Consider the fact that 25ms is considered a good standard for online gaming, we are basically looking at the limits of human perception. How fast is that? [Here's a good place](https://web.archive.org/web/20240526111507/http://jsfiddle.net/QGmBy/) for you to test what's fast in terms of your own perception between 1 and 320ms. So if I'm presenting data to a human being for a decision, nobody's going to expect you to make other than a hand-eye coordination twitch style decision in under 100ms. So if you're a drone pilot, you're dealing with a streaming system. A batch system is one that basically runs on a periodic basis beyond a couple minutes or so.

The system I created to generate phone records is a micro batching producer into a Kinesis stream. Now I can generate 50,000 records in about 1.7 seconds; that's clearly way more than I need for my peak TPS target of 5x 1800 = 9000TPS in the LA County phonecall scenario. Also, the Kinesis API expects me to send records at a max of 500 records per call. So that ingestion is kind of slow. Then again, I'm single threading that push. Even so, as I batch up 16 pushes for the peak of 8000, I get that done in 7 seconds. So the lag on the Kinesis side from my single producer isn't really a big deal considering that I'm generating the original 8000 with the same single timestamp. So I'm effectively catching 1100 TPS through Kinesis which is providing a bit of input delay, then again, I'm only running 3 shards of Kinesis and I'm not sending parallel sets of data. I'm sure I could step that up, and in fact I know that I could push records way faster directly to VoltDB if I wanted to. But I really wanted to demonstrate Kinesis and Volt. Right now, I don't know the economics of the two.

Additionally, I know that Kinesis will spit faster than it sucks. So our interesting performance will be seen on the next phase which is the ingestion speed of VoltDB as a Kinesis consumer. I should have some results for you next week. The cool thing was that I basically got the Kinesis part running in under an hour. As soon as I figured out that I was using an old version of the aws-sdk, all my problems went away and I was able to do what I needed. Now I suspect that in the long run I will likely be much happier doing the high performance thing directly with Volt. And as I have legoed these components together I can already see some cracks in the idea.

Nevertheless, here's the scenario. I have a watchlist of 50 phone numbers. I start up my demo which kicks off a container with my phone record generator. The generator cranks out half a million phone calls simulated phone calls. I ingest them into Kinesis. 8 minutes later, I've got half a million stashed into Kinesis. Now I push the next button and this represents a situation in which Volt is eating the Kinesis stream as if it were the originator of the streamed data. I don't quite understand the reason for the asymmetry of Kinesis' slow read and its fast write speed, but... In this phase, VoltDB is getting streamed transactions at a pretty low latency. According to my stats, I'm doing an average approaching 60ms ingestion latency into Kinesis. The output latency is more like <1 on the scale they're showing me. So that will be how I simulate a fast streaming dump. Obviously I could get Volt to read the half million records from a flat file, but that's not really streaming is it?

So once the streaming records start hitting VoltDB, I will trigger events based upon my watchlist. And that will represent real-time flags on phone calls. Now the glitch here is that basically the phone calls are over by the time I have the CDR, but we'll ignore that for the moment. Again, I'm just simulating a fast stream. But for demo purposes, you can see that we will be able to immediately flag the phone calls on the watchlist. What we're also going to do is map the source or target phone calls and immediately add them to the watchlist. That's the second VoltDB task. Now all subsequent alert records are pushed downstream to Vertica where we do some historical surveillance. How many calls did our subjects make? What about the second order subjects? It's in the Vertica database where we add a bunch of metadata and do deeper analysis, but in the stream that we catch our perpetrators in the act. All this without actually checking the content of the phone calls.

That's the state of the demo right now. I'm only using one kind of CDR out of the 50 or so that exist, so I'm not checking for conference calls or hangups. I also am mixing up area codes at about a.47 ratio of inter- to extra-area code calls, because right now the purpose is to identify cells in Los Angeles County. I'll probably throw in some international style calls and that could be a third rule for flagging an alert in Volt.

### Red vs Blue

[![Screenshot 2016-05-12 11.33.16](https://web.archive.org/web/20240526111507im_/https://cobb.typepad.com/.a/6a00d834515ae969e201bb08fd30b4970d-320wi "Screenshot 2016-05-12 11.33.16")](https://web.archive.org/web/20240526111507/http://cobb.typepad.com/.a/6a00d834515ae969e201bb08fd30b4970d-popup)

I'm browsing in an attempt to understand my marketing job a little bit better. Look what I found

So if you want to know the difference between **real clouds** and **fake clouds**, here is a sample. First, sadly, I got an email today from ODTUG and found the acronym EPCRS or something like that. So I went to the [Oracle website](https://web.archive.org/web/20240526111507/http://docs.oracle.com/cloud/latest/eprcs_common/eprcs_videos.htm) and found this non-embeddable animation on what it's about. So literally, they don't even show the product, and what they do show isn't even compatible with blogs. I mean it comes up in a popup window on Oracle's own website and it's crap. It doesen't even show the animation in a decent window.

Then there's Domo, which is a client of ours. They have their own YouTube channel. They understand social media. Oracle looks like The Hartford Insurance Company by comparison. I have seen Domo tech and it's very cool. The backend is even more interesting than the front-end, which is formidable. These guys get it.

![](https://www.youtube.com/watch?v=qO4NgGR3iWA)

### Three DB - Disposable Datawarehouses

I just did something remarkably easy that reminds me about why Amazon is winning and will continue to win. I started up three different databases and then threw them away. For anyone who has worked in the Amazon ecosystem, this may seem like just an ordinary thing. Indeed it is, but let me take you back in time.

In 1985, I took my second summer internship at Xerox in El Segundo, CA. I reported to a guy named Jack Starkey who was one of those starched-shirt engineers of the first order. I loved the guy. My assignment was to build a data dictionary for the parts and service database that Xerox used to keep track of the maintenance of their top of the line laser printers. Xerox was considering migrating from an IBM VSAM hierarchical database to something called Focus, a new fangled relational database. My job was to insure that I had all of the definitions correct. I asked Jack if I could use the new Xerox Star Workstation in order to complete my job, which was essentially all about documentation. He agreed.

My first internship was more interesting because it was more technical. I actually wrote a financial modeling program. But my boss was loathed and feared in that area and a lot of people hoped everything he did would fail. That guy, whose name I actually cannot remember Jim somebody, was a notorious pipe smoker back in those days when you could smoke in the office. He liked something called Amphora Green.My project did not fail, although there were some interesting twists. My job was specifically to make a realtime pricing model that salesmen could use to develop a quote for customers based upon the way they actually did their electronic printing. At the time, most computer printing came out of printers attached to mainframes and the most popular one was the IBM 3800. But the Xerox printer had duplex and quadplex, meaning it could print on both sides of the same sheet of paper. My program would show the long term economic benefits of using the Xerox tech which often came down to power and supply costs. So I learned 'Total Cost of Ownership' at a fairly young age. The MBA intern with whom I was working had her HP calculator. My code was being held up because she was late in delivering a 'cost matrix' to me. I sat down with her finally to discover that she had just been plugging numbers into a formula run on her HP 12C. The MBAs didn't sit with the engineers, you see, so getting this meeting took weeks. I had to explain to her that this CP/M based computer could actually do that kind of formula calculation. She was shocked that Xerox actually made a computer that could do the same things as an HP 12C. We all learned a little something. I recall later on that a cat named Burkhart, whom I seem to have never forgiven in person, got the chance to present the wonders of my completed program to Xerox folks in London, while I went back to school that September.

But that was the pace of things in the mid 80s. Another dude I vaguely recall had the radical attitude I might have enjoined were I not so desperate to drive a BMW. He advised me to get all my hacking done before the implementation of ACF2. What we were dealing with was the gap between the time you could get engineers to understand a technology, the time it took them to implement it, the time it was adopted by the business, and the time that an actual payoff could be seen. Then there was the time it took for the capacity of the business to exceed the design limits of the system in place and the time it took for that problem to arise to the level of necessity and a new replacement process begun.

In the 80s, all of that was glacial. Moore's Law kept us all expectant about the future, mostly in terms of how much of all of the business processes could be captured outside of the pocket calculators of MBAs, but the process of business adaptation as well as the process of re-sizing systems have continued to be slow all the way to the current day. Amazon has emerged to understand these kinds of problems very well because of how e-commerce begat DevOps. And yet the majority of businesses still use 'Enterprise' architecture in their systems implementations. 'Enterprise', for all intents and purposes, was the term used to convince IT buyers that UNIX based servers could handle all of the business once only owned by the sort of mainframe computers that spit data out to Xerox and IBM printers. And then came e-business which introduced the 'n-tier' solutions, multiple tiers required because no single vendor, not even IBM, could provide hardware, networking and software solutions for the new class of applications being envisioned and built.

I don't have a buzzword we could reliably depend upon to be what this time of transition to cloud architecture will be. 'Post-Enterprise' is all I will hazard. However, what processes can and will be improved is a lot clearer. So I hope to speak to you, my fellows still using the systems designed with on-premise Enterprise class architectures in mind. That's my aim for this year, to help you see what I see and what my company, Full360, can do to help you realize some of the promises of computing that were made a long time ago and have been a long time coming.

So what I just did, single-handedly, today and yesterday, was build three different database servers Oracle 11g, MySQL and Microsoft SQL Server. They were each 4 core 15GB servers with at least 300GB of SSD. They took about 15 minutes to configure and secure, with automated backups in an alternate data center. I was able to connect to them directly through a secure VPN I had previously setup with my RazorSQL client using JDBC. Today, I'm shutting down the Oracle and MySQL services because my customer only has the MSSQL license. But it was actually fun playing with the alternatives. Fun!

What's going to happen next is that I will start using AWS Config to keep track of all of my compute and networking assets for my customers. I'll be able to tell, at a glance, which server is doing what in which stack in which VPC. I will be able to manage services to an even greater extent for this and my other customers.

Back in 2001, I had a dream about a company I might work for in the future. I called the company 3DB because as a fundamental competency I wanted people who understood object, relational and multidimensional database technologies. We could then build the kinds of systems I envisioned. Now I work at Full360, but the 3DB concept is reality. We use multiple database technologies in our data management framework called ElasticBI. I didn't envision them running in a cloud architecture, but that is even better. Stay tuned.

### Full360 Architects at Re:Invent 2015

![](https://www.youtube.com/watch?v=7fN4FnlyP9A)

### Beyond BI

This is my blog, but it's also a kind of unofficial blog for [Full360](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/page/2/www.full360.com). Very interesting things are going on.

About a year ago, at a hotel room in the Venetian Hotel, we began a discussion about what we wanted to build into the Full360 elasticBI platform. We have been very successful. This year, we've had more time and people put into that process and in consideration of what we want, what our customers have had us build and what's happening in the market, we have a very different outlook than just a year ago.

It's really time to say that BI is just a part of what we're all about. It's a big part, but..

I think the simplest way to understand is to know that we have responsibility to funnel information to executive decision makers. That means, as systems integrators, we get to know a lot about all of the different kinds of source data in enterprise data flows. We have made it our business to re-architect enterprise paradigms to the AWS cloud. Our success in understanding and implementing that has far reaching consequences for what we can do, and therefore who we are.

This year at AWS Re:Invent, Amazon introduced several groundbreaking products, not the least of which is their new BI tool, QuickSight. As we have been talking to people and prospects, we've heard them say 'slice and dice, bar chart blah blah blah', and we get that. So we've always said that we are the cloud architects on the back end, which we are. We thought that by saying, "We are next-generation data warehouse', that it would be quite enough to distinguish us. It does but only when you start looking closely at the technology and what we're doing with it. I'll fill you in on that later. The point here is that our DWAAS platform and methodology is forcing us to invent new terms that the market can understand. I am continuing that responsibility. Fingers crossed.

Our experience is that we have been two steps in front of Amazon and four steps in front of the industry. This year we are only one step in front of Amazon and expect that they will start formalizing products around technology integrations we have done next year. What is that technology integration? Let's call it ETL. We have taken ETL to the next level - higher performance, lower cost. But we haven't launched it as a product, rather made it available as a service. Everything we do is a service in a systems integration and managed services framework. That's how we do business. We are focused on function in the context of the AWS cloud environment and architecture. That's not software you load on servers so much as it is API calls in an highly customized environment configuration. The bottom line is that with the elasticBI Framework we can get data from complex source to high performance destination at a scale and speed unthinkable in traditional architectures. While I'm on that point let me describe Multi-Tier DW.

Multi-Tier Data Warehousing is what we all our practice of combining multiple data storage and database technologies in a single analytic application. Imagine this example. A Full360 client has a website that generates 1 million unique customer hits a day from customer interactions. We use our ***Dragonfly*** realtime rules engine to score these customers as they use the website and add new attribute data at peak rate of  30,000 REST API transactions per minute. This is powered by [VoltDB](https://web.archive.org/web/20240526111507/https://voltdb.com/), our fast data in-memory database partner. This data is staged into a multi-node [Vertica cluster](https://web.archive.org/web/20240526111507/https://www.vertica.com/) that integrates internal financial data and industry benchmark data purchased from a third party. Additionally we have added ***custom widgets*** to the website to capture additional data. It is made immediately available through our ***custom IOS app*** to mobile employees around the globe. History is automatically archived to S3 for low cost high availability and then efficiently batch loaded into [Amazon Redshift](https://web.archive.org/web/20240526111507/https://aws.amazon.com/redshift/) to process billion row queries on demand. We serve this data on one or more of our BI partner tools, perhaps Tableau, perhaps TIBCO Spotfire, perhaps Jaspersoft. That's a multi-tier DW solution.

But notice how we have extended back by providing our own microservices in our client's website. Notice how we have extended forward into our client's user base with IOS apps. Notice how with Dragonfly we have added a new dynamic dimension of data to our client's CRM. Now we could stop there and say, as a systems integrator we have demonstrated a larger aegis of control. We could stop there and say by employing in-memory, object-store and column store data management we have evolvled into next-gen Data Warehousing. But that would be incomplete, because we have done more than that.

So it leaves us with something of a marketing problem. Let's talk about the more.

One of the first operating principals of Full360 was that we are a DevOps company. We have reduced the cycle time of our data management. We can move applications from development to production in a matter of hours. Need to double your database staging mechanisms? Right away, sir! One of the things we do in our standard delivery is employ Cloudwatch to not only monitor server performance (remember everything isn't a server these days) but service performance. So we monitor the latency of the *data process* and can dynamically scale when necessary. We know when our customer's data sources are choking long before our customers do.

Another principle is that we will use Open Source and be vendor agnostic using the best technology and best architectures available for our client's projects. Architecturally speaking, nobody holds a candle to AWS. Azure might be worth consideration in a couple years time, but right now we're all about AWS. They are thought leaders as well as innovators. For Full360 that means we incorporate excellent technologies like [Hashicorp's Vault, Terraform and Consul](https://web.archive.org/web/20240526111507/https://hashicorp.com/), to help secure, configure and communicate in the elasticBI platform. For our virtualization, we've been using combinations of Vagrant, Docker, veewee and Virtual Box. For our orchestration we've been using Chef and CloudFormation and Terraform is next.

This is just the beginning, but I need to keep this blogpost bite sized. I'm going to help you understand in the short term.

### Stepping Out of the Elephant's Shadow

Hadoop.

Where do I begin to tell the story? How about we go from the epiphany backwards? This morning I read [this](https://web.archive.org/web/20240526111507/https://www.evernote.com/l/AAbpECOZellFmZy3mjW93HYEY72Gi7LsoPE) from Dave Sisk.

> Hadoop is not even in the same ballpark as any of the CDBMS's that have been mentioned. It's not even a database, for that matter...it's a giant MPP ETL process...which is a great thing IF you use it as a giant MPP ETL process instead of trying to use it as a database. I've examined HBase closely, and looked at a colleague's implementation...it has to be the only key/value store that I can think of that is a worse piece of crap than MongoDB. (At least MongoDB is better than something.) My colleague's company's 60-node implementation of HBase (on big honkin' enterprise hardware) struggles to insert 2000 rows of data second (I can insert at 10-20 times that into PostgreSQL running in a VM on my friggin' laptop), and reports run for hours (sometimes days). You can do the same work in a good columnar RDBMS 2-3 orders of magnitude faster...as in milliseconds or seconds (minutes at worst), instead of hour or days.  
>   
> At a prior company, we used Vertica to consume hundreds of thousands of rows per second, and could return results from billion row high-reduction queries in a few hundred milliseconds (from about 5 hefty nodes)...Hadoop/Hive/HBase with hundreds of nodes could not come within 2 orders of magnitude of that kind of performance, no matter how much hardware you throw at it.

That is what I've been waiting to hear for years. So I wrote back.  
  

> Finally thank you for helping me understand what I didn't, that there is a massively huge performance gap between Vertica and Hadoop. I've been wondering why I never meet Hadoop folks in my space (Business Intelligence) and I've been listening to the guys at MAPR tell me theories of why their Amazon-approved version of EMR is going to be a world beater. I have assumed that all Hadoop is simply a very large scalable file system (and I've started to call it HDFS) + some clunky tools that lack a semantic layer. But I assumed that a reasonably competent Java programmer (who wants to be that?) could make it perform at a good clip. No matter what the performance, I expected that it was mostly ETL class tech. BUT I figured sooner or later somebody was going to build a semantic layer of SQL onto it and then it would be serious competition for columnar DBs, primarily because of mind and market share.  
>   
> However, if Hadoop is little more than a glorified giant file system and map reduce is to HDFS as regex grep sed & awk + perl is to ordinary file systems, then there's no way it will ever compete on performance and cost efficiency to columnar tech.  
>   
> I'm going to assume HDFS is a data lake from here on out, unsuitable for BI queries.

That assumption means a great deal in my world and it erases a class of insecurity I've been having over every discussion of 'big data' I've been a part of for several years. You see none of my customers have Hadoop or ask for Hadoop. All of them can form the syllables. They know about Hadoop. Hadoop \*is\* big data, as far as the layman's world (and another world that is not BI). So I haven't had a \*reason\* outside of great curiosity to build anything with Hadoop.

First of all, I have S3. There's no bigger data lake I've ever needed. Terabytes are not a problem. I mean I've got terabytes at home. But under [ElasticBI](https://web.archive.org/web/20240526111507/http://www.full360.com/2014/12/11/full360-data-platform.html), I've got S3 whipped into shape and smartly integrated to every database I care about. (Vertica, Redshift, Essbase, VoltDB). So I never have to concern myself with running out of space for staging or moving massive amounts of data. It's always about database optimization. That requires structure, structure requires purpose, and I know how to get that from my customers. Hadoop is about unstructured data.

Now when I start talking about unstructured data, I mean web data that has a volatile structure. And in that space I see tools like MongoDB, Cassandra and CouchDB with Couch as the winner. I've heard horror stories about Mongo, and that Cassandra is a big tease that never quite gets all of her drama together. There's also Riak which is heavyweight champion in the space, so I hear and believe. But I'm not building ecommerce websites and I don't need to manage volatile content and serve up XML to be rendered, so I have no need for that class of data management. Not right now anyway. I want to be the master of all data management, data store and database worlds, but I have to deal with one continent at a time, and I can accept that Riak and Couch are on another planet. Planet Unstructure.

But when they say they're going to put on SQL clothing and take their big data + analytics into the Data Warehouse realm, that's war of the worlds. I don't like the prospects of that imminent invasion. Because, really, websites are the masters of handling 10,000 simultaneous concurrent users. I can't do anything like that. Those guys must know something.

Well, so did LAMP stackers at one time. I'm going to take a gamble and commit HDFS and all that manipulation to the back porch. It's not competition in BI, and it never really was, but that was really in my mind a matter of market focus. Now I understand technically that there are hard limits to what all of that can ever do and strong technical reasons why what I do with my database tech is not threatened by these other systems.

I still want to know. I still want to spend some hands on time and eyeball some NoSQL tech in the context of their own systems. I wish I knew a guy, personally. But maybe our paths haven't crossed for good reasons. Either way, I am stepping out of the shadow of the elephant. Hadoop is just a data lake fallback for collecting a lot of stuff that may or may not be map reduced into something coherent. It's a specialty ETL transform that we at [Full360](https://web.archive.org/web/20240526111507/http://www.full360.com/) will do with realtime streams. So maybe if my Colorado River data pipeline fails, it will form a Hadoopified Salton Sea while we fix the levee. What it most definitely is not, is Fast Data. Meaning it has no place in the IoT future and is an artifact of what we will inevitably call something along the lines of JBOD. Lakes are meant to be drained. And now I've completely introduced heterogeneous metaphors into this. But that's kind of how epiphanies work, neh?

I'm out of the shadow of the elephant who drinks up lakes with that weird trunk of his. Yay circus tricks!

### Seven Rules for Saving All Your Stuff

The most important thing about backing up important files is that you do it yourself, fairly often and redundantly in different media. That way, over time, you'll have opportunities to rescue data that is important to you, and then you'll have practical experience.  
  
I have been doing this for about 20 years. I have used everything from magtape to 8 inch floppies, to zip and jaz drives, to cds, dvds, memory sticks, external hard drives and USB devices. I've used RAID NAS, and a couple generations of cloud services.  
  
The most important thing I've learned is that when it comes right down to it the things you value most, you probably don't even have digital copies.  
  
So I went through this exercise a long time ago (1989) when there was a fire two doors down from my apartment. I had already done the drill so I already had prioritized what I was prepared to lose in a fire, and what I could not bear to lose. My priority was my written diary and personal photos. I had it all in four milk crates and was ready to evacuate in under 10 minutes. Everything else, books, records, cds, clothes - were all replaceable.  
  
**Rule #1 Go through all of your stuff and see what's irreplaceable.**  
  
Pretend you have a $1,000,000 fire insurance policy and your house burns down. OK. Whatever you can buy a better new version of is basically disposable. Actually, insurance companies (and police departments) would like you to go through this very exercise. If you have lived through a home burglary or fire, you'll know this. Everybody should know exactly where that irreplaceable stuff is. My dad's college beer steins. My silver framed wedding picture. My autographed bass guitar. The cuff links from my wedding.  
  
Next, you would think official documents and stuff would be pretty valuable, but in fact it's mostly sentimental. Tax returns, death certificates, citizenship papers, passports, birth certificates, check stubs, medical receipts, degree certificates. All on record somewhere else. Disposable. Inconvenient if you don't have them, but really... that's only because you're in a hurry and you didn't plan. Admit it. And I have to say, if I had been divorced, or lost custody of my kids, those papers I probably wouldn't want around.  
  
The big pain in the neck is scanning your important personal papers. Just do it. Once you've done it, print them out again and store them in boxes. Now you have originals, digital copies and physical copies. Store the physical copies at a relative's house. If you don't have any relatives, rent a big safe deposit box at a bank (preferably a bank downtown) and put the most personally valuable ones in their vault.  
  
Now with your digital copies, buy an external hard drive and dump them all over into them. Next buy a premium account with Evernote and send them all into Evernote. Obviously you want to use PDF. It's probably the most robust digital version of anything, although JPG is pretty damned good as well. Next backup your spinning hard drive with Backblaze or Carbonite. Finally put the most important, important sentimental docs also into Dropbox and Amazon S3.  
  
That's for documents. Next for pictures.  
  
It shouldn't take long to scan all of your prints. If you have color slides, they are the most troublesome. If you have super 8 or 16mm film, Kodak has an (expensive) processed to digitize all that. I would also search around for a local camera shop that converts Hi8 and VCR tapes to DVD. That's expensive but worth it. Movies of your kids are priceless, no matter how insipid the action.  
  
I've converted thousands of my own and my father's photographs. I have to say that unless they are 8x10 or larger prints, then once they are scanned, that's the best format. So don't bother getting reprints, you'll enjoy them more online anyway. For those exceptions, there is Shutterfly (I think). Remember redundancy. Make your favorite pictures gifts to other folks. We make picture calendars and Christmas pictures every year and send them to friends and family. Funny how those show up 15 years later. Right now Flickr is the best service for my money. Google + screwed up what was wonderful about Picasa, and Amazon is coming up with a new service. Apple photostream is a brilliant idea, well-executed, but that's just 1000 pix.  
  
**Rule #2: Prioritize what is irreplaceable.**  
  
It will turn out that 'all of your digital stuff' will fall into the area that Taleb calls 'Mediocristan'. Basically there will be a predictable bell curve distribution for the number of digital assets you will find irreplaceable. For example, if you pick your favorite movies, chances are you'll have anywhere from 50 to 200. But you are very unlikely to have 2000 favorite movies. Similarly you are very unlikely to have 20,000 favorite songs or 10,000 favorite pictures. Your entire library might be that big, but not your favorite, irreplaceable ones.  
  
The good news is that your favorite movies and songs are probably going to be other people's favorites as well. So movies and songs are likely to be disposable. So is software, except for the stuff you've written yourself.  
  
All that said, I've got some 50,000 photos all over the place redundantly, but about 2300 that I keep redundantly in Dropbox, Flickr, on DVD, on USB sticks and in S3. All of them are synched to my phone, and some fraction of them I've posted to Facebook and in my blog. I have it covered.  
  
**Rule #3: Be Redundantly Redundant.**  
  
If you don't eat a Big Mac, you'll forget what a Big Mac tastes like. But you probably won't because there's a McDonalds everywhere. You should periodically visit your favorite digital assets just to make sure you can. I like looking at my resumes from college and pictures of my wife 30 pounds ago. I like listening to Beethoven's Moonlight Sonata and I could watch the Fifth Element another hundred times. (Multipass!) There's no point in stuff being digital unless you checkup on it. Go eyeball those CDs you burned 10 years ago. Mount that old Porsche Design 150MB hard drive. See what's on that old memory stick.  
  
**Rule #4: Review and Recycle.**  
  
Put old media into new media. Put new media into old media. Look at those old Grand Canyon pictures, are they really so precious. Your priorities change. You \*should\* overspend on your redundancy until you get to the point where you know you have too many copies of that one song and it's costing you too much money to store it. Then you reprioritize again. See if there's a better storage deal out there.  
  
**Rule #5: Plan for the Disaster**.  
  
After the disaster happens, are you really going to care about all that stuff? Maybe you could admit that somebody else has a better collection than you? Have you really had a garage sale forced on you because you were desperate for money? Then you know that #3 wood you used to hole the Par 3 at the municipal course is actually only worth about $20 bucks.  
  
I learned these lessons because every year without fail for about five years straight, one or more of my hard drives would fail. I got really good at using recovery utilities to get data out, which is why I have thousands of songs titled like Recovered\_00493.mp3. And oh by the way, the open source MP3 guys were right all along. So remember that the open source stuff lasts longer. And also do NOT waste your money on anybody's NAS. If you think RAID5 will save your bacon, think again. (Up your's Iomega!). Just check around for what people charge for recovering hard drives. It's highway robbery.  
  
**Rule #6: Do it yourself, plus the Rich get Richer.**  
  
The best kind of redundancy is the kind where you can depend on other people's self interests being aligned with your own. Find the big dog market leaders and place bets on their technology, but be smart about it. Pay attention to where other people are placing their bets. Amazon right now is a sure thing, and over the past 3 years have kicked Apple's ass when it comes to storing your music. But not long ago Apple's iMatch was boss. Flickr is great for pictures, but pro photogs like other services. Don't follow the crowds, follow the pros, but keep doing it your own way too. A little paranoia goes a long way when it comes to disaster planning. It might even change the way you look at everything.  
  
**Rule #7: Expect Failure, and get over yourself**.  
  
If everything you did were so precious, people would line up to do this crap for you. Ask Bruce Willis if he has enough pictures of himself and his ex-wife. I know right? Every system fails. This is all about cost/benefit analysis. But in the end, we all die, and your surviving ex-wife is going to do things in your house that would set your teeth on edge. So recognize it's all small stuff, except for this chair.  
  

![](https://www.youtube.com/watch?v=w2X3vVMdh-s)

### Three Databases

I just did something remarkably easy that reminds me about why **Amazon** is winning and will continue to win. I started up three different databases and then threw them away. For anyone who has worked in the Amazon ecosystem, this may seem like just an ordinary thing. Indeed it is, but let me take you back in time.

In 1985, I took my second summer internship at **Xerox** in El Segundo, CA. I reported to a guy named Jack Starkey who was one of those starched-shirt engineers of the first order. I loved the guy. My assignment was to build a data dictionary for the parts and service database that Xerox used to keep track of the maintenance of their top of the line laser printers. Xerox was considering migrating from an **IBM VSAM** hierarchical database to something called **Focus**, a new fangled relational database. My job was to insure that I had all of the definitions correct. I asked Jack if I could use the new Xerox Star Workstation in order to complete my job, which was essentially all about documentation. He agreed.

My first internship was more interesting because it was more technical. I actually wrote a financial modeling program. But my boss was loathed and feared in that area and a lot of people hoped everything he did would fail. That guy, whose name I actually cannot remember Jim somebody, was a notorious pipe smoker back in those days when you could smoke in the office. He liked something called Amphora Green. My project did not fail, although there were some interesting twists. My job was specifically to make a realtime pricing model that salesmen could use to develop a quote for customers based upon the way they actually did their electronic printing. At the time, most computer printing came out of printers attached to mainframes and the most popular one was the **IBM 3800**. But the Xerox printer had duplex and quadplex, meaning it could print on both sides of the same sheet of paper. My program would show the long term economic benefits of using the Xerox tech which often came down to power and supply costs. So I learned ' **Total Cost of Ownership** ' at a fairly young age. The MBA intern with whom I was working had her HP calculator. My code was being held up because she was late in delivering a 'cost matrix' to me. I sat down with her finally to discover that she had just been plugging numbers into a formula run on her HP 12C. The MBAs didn't sit with the engineers, you see, so getting this meeting took weeks. I had to explain to her that this CP/M based computer could actually do that kind of formula calculation. She was shocked that Xerox actually made a computer that could do the same things as an HP 12C. We all learned a little something. I recall later on that a cat named Burkhart, whom I seem to have never forgiven in person, got the chance to present the wonders of my completed program to Xerox folks in London, while I went back to school that September.

But that was the pace of things in the mid 80s. Three months just to build the equivalent of a DDL script to help move data from one database technology to another. **Today I do that in realtime**. Another dude I vaguely recall had the radical attitude I might have enjoined were I not so desperate to drive a BMW. He advised me to get all my hacking done before the implementation of ACF2. What we were dealing with was the gap between the time you could get engineers to understand a technology, the time it took them to implement it, the time it was adopted by the business, and the time that an actual payoff could be seen. Then there was the time it took for the capacity of the business to exceed the design limits of the system in place and the time it took for that problem to arise to the level of necessity and a new replacement process begun.

In the 80s, all of that was glacial. Moore's Law kept us all expectant about the future, mostly in terms of how much of all of the business processes could be captured outside of the pocket calculators of MBAs, but the process of business adaptation as well as the process of re-sizing systems have continued to be slow all the way to the current day. Amazon has emerged to understand these kinds of problems very well because of how e-commerce begat **DevOps**. And yet the majority of businesses still use 'Enterprise' architecture in their systems implementations. 'Enterprise', for all intents and purposes, was the term used to convince IT buyers that UNIX based servers could handle all of the business once only owned by the sort of mainframe computers that spit data out to Xerox and IBM printers. And then came e-business which introduced the 'n-tier' solutions, multiple tiers required because no single vendor, not even IBM, could provide hardware, networking and software solutions for the new class of applications being envisioned and built.

I don't have a buzzword we could reliably depend upon to be what this time of transition to cloud architecture will be. ' **Post-Enterprise** ' is all I will hazard. However, what processes can and will be improved is a lot clearer. So I hope to speak to you, my fellows still using the systems designed with on-premise Enterprise class architectures in mind. That's my aim for this year, to help you see what I see and what my company, Full360, can do to help you realize some of the promises of computing that were made a long time ago and have been a long time coming.

So what I just did, single-handedly, today and yesterday, was build three different database servers Oracle 11g, MySQL and Microsoft SQL Server. They were each 4 core 15GB servers with at least 300GB of SSD. They took about 15 minutes to configure and secure, with automated backups in an alternate data center. I was able to connect to them directly through a secure VPN I had previously setup with my RazorSQL client using JDBC. Today, I'm shutting down the Oracle and MySQL services because my customer only has the MSSQL license. But it was actually fun playing with the alternatives. Fun!

What's going to happen next is that I will start using AWS Config to keep track of all of my compute and networking assets for my customers. I'll be able to tell, at a glance, which server is doing what in which stack in which VPC. I will be able to manage services to an even greater extent for this and my other customers.

Back in 2001, I had a dream about a company I might work for in the future. I called the company 3DB because as a fundamental competency I wanted people who understood object, relational and multidimensional database technologies. We could then build the kinds of systems I envisioned. Now I work at [Full360](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/page/2/www.full360.com), but the 3DB concept is reality. We use multiple database technologies in our data management framework called ElasticBI. I didn't envision them running in a cloud architecture, but that is even better. Stay tuned.

### Producers, Consumers & Dynamic Data Warehousing

So we have a bunch of big ideas around here at [Full360](https://web.archive.org/web/20240526111507/http://www.full360.com/) and it seems that I have been doing them rather than talking about them. That's what I like about work. Here's what we're doing now.

If you're going to handle big data, sooner or later you're going to get massive amounts that really are too bothersome to keep on your database server in any other form than IN the database. The cheapest place in the world to keep your data is at the NSA, they'll scrape it and store it for you free, indefinitely if you encrypt it. But the cheapest *accessible* place to keep your data is in Amazon S3. So our theory of DW says, keep your permanent record on S3, and build dynamic data warehouses as needed. What? Dynamic data warehouses? Yes, we shall explain but we're not there just yet.

The massive amounts of data on permanent record generally comes in a stream or in multiple streams. In fact, we have abstracted all of our dataflows essentially to streams and have build standard operations around those streams. There is some precise language that I have around here but the purpose of this blog is to just give an overview. Suffice it to say that there are timing and chunking issues between the way data is produced at the source and the way it is consumed into the data warehouse. Therefore, producers and consumers.

A Producer is a chunk of code that aims itself at a source of a datastream, periodically scrapes off a chunk and then stores an {compressed, encrypted, UTF-8'd, versioned} file set onto a time-hierarchally organized S3 bucket. Let's say that your stream was POS transactions from McDonalds. Every hour, you would make a smart query of the transactions based on a time window (which may or may not be redundant) and then send your results to S3. At the end of the day, you'll have 24 flatfiles in the path mickeyd-bucket-name/POS/2014/2014-01/2014-01-09\_0100\_MickeyDPOS.txt or some such. Easy to get, can handle millions of files, no problem. But the point of the producer is that it is synchronized to the actual production of data, whatever the source and chunks it appropriate to the most efficient manner of database ingestion.

Producers have smart sub-features. For example, it is the responsibility of the producer to translate XML or JSON to CSV. We like vertical bars (since we are a Vertica shop, nyuk nyuk) but we call it text file or a flat file anyway. Basically all of the cleansing REGEX, bogus character detection, and internal record consistency stuff takes place in the producer. The producer can be made smarter with regard to time (to avoid redundancy) by tying its query to the DW control table. Most importantly, the producer process itself can be scaled horizontally for scalability and/or redundancy.

The producers create a text-based data warehouse in S3 which is rationalized to the largest set of data any data warehouse can handle. It is all history, all fields, all streams. The consumers determine what goes live and queryable at what rate.

The Consumer is a chunk of code which generates smart efficient updates and merges to the data warehouse in synch with the way that data is consumed by the DW users. So it is the more conventional driver of database operations. In fact, you can think of the actual database production lifecycle in terms of the consumer. As my old good habits dictate, each of these are discrete operations that are verbs.

- Capture
- Ingest
- Cleanse
- Stage
- Merge
- Calc
- Errorfy
- Report
- Distribute

Errorfication is something we've done before but it is a concept that needs a bit of explaining. I'll do that in another post. The rest are basically self-explanatory. Notice that from Ingestion through Merging, we increase the complexity of the operations but reduce the volume of records we ultimately work on. Since we're using columnar shardable database tech, this scales rather well, even though merging will always be a CS nightmare.

Note that the producers and consumers work together in real-time but you can choke them up or down. This is determined by the commit stamps on your control table. So let me talk about that a little bit.

Each file processed into the S3 buckets is going to be registered into a control table. This control table will let us trace all of our records back to S3. IE it is a key into the DW that gives us the provenance of the ETL process. You might be producing on the daily but consuming over the weekend in a 4 hour batch window. Nothing exists to the DW until it is registered which is done immdiately after a bulk copy of a file is loaded to the appropriate source table. Assuming the source table lives until the next step of ETL, the control table will know everything it needs to know about the content of the file loaded into the system. This control table's information is used to throttle the size of consumption chunks. I could go back 2 days, 30 days or two years on my consumer depending upon how much I want to burden my merge process. I could measure those two days by transaction stamps in the datafiles themselves or by the days they were produced to S3. Or I could just rebuild the entire warehouse from scratch or stream by stream.

These are the fundamentals of the dynamic data warehouse. Its great efficiency is that database servers are not burdened with local data - transfers from S3 to the VPC being cheap. It allows near-realtime data loads from disparate external sources, sometimes halfway around the world, and it allows for the exciting possibilities of adding open data into corporate DWs with relative ease. Naturally, dumped DWs can be published elsewhere. It's very cool, sez me.

[« Previous](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/) | [Next »](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/page/3/)

## Categories

- [AWS (24)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20240526111507/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20240526111507/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20240526111507/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |