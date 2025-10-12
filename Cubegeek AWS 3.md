---
title: Cubegeek AWS 3
source: https://web.archive.org/web/20250211214647/https://www.cubegeek.com/aws/page/3/
author:
  - "[[Cubegeek AWS 3]]"
published:
created: 2025-10-12
description: Big Data Analytics, perspectives from a 25 year practitioner.
tags:
  - clippings
  - cubegeek
---
The Wayback Machine - https://web.archive.org/web/20250211214647/https://www.cubegeek.com/aws/page/3/

### Certs

Although it's annoying to be at the bottom of a new stack of software and methodology, at least now there is a visible ladder. AWS is offering professional certification and I've started on that path. Over my career there have rarely been occasions when I have been drawn to the idea of certification. It's just doing what I do that matters. But I have to say that what Amazon is offering is the first time I have looked at a very practical, large scale computing platform that makes sense in the biggest realm since I studied XNS at Xerox back in the 80s. I'm sure that there were people who saw SNA and the 360 world back at IBM at the same period in time in this comprehensive way - so let me say it bluntly. AWS is what IBM was. The rest is just a matter of time and market share. And you have to look at it at that level - well, if you're stuck with the kind of mindset I'm stuck with you have to keep that perspective.

Microsoft had the same ambition, bless their hearts, but they mistook a compute size for a compute world. That is to say until Dell started building badass servers on the Microsoft platform, MSFT itself was locked into front office computing - and it is the seduction of that money that allowed (Thank God) Linux to leap into the gap. Back in the day DEC was all about that end to end compute platform as well, and HP managed to hobble along. Sun Micro did the exact reverse of Microsoft if you ask me. I cannot understand how SunOS and Solaris never managed to gain a reasonable foothold in the front office. Oh wait, they were overpriced. And the Linux desktop leaped in, almost. Apple did a finely focused job on a few places and were insanely great, but I think it was patience, in the end that allowed the Mac to survive. It's hard to say whether or not Sun could have made a desktop as finely crafted as Apple, but then again, they weren't really trying.

So now we are back to AWS - to huge systems architectures on the scale of XNS, SNA and DECnet. Where those three were closed, AWS is open, piggy backing on the best and probably not dependent on TCP/IP like the rest. I haven't heard the term 'SONNET Ring' in a long time. Nor FDDI. I used to hear a lot of that when I looked at huge architectures, and so I suspect that such network technology is embedded in the AWS Region and Availability Zone architecture. Embedded and invisible where it belongs. I can't say that I generally think this large, and it's rather surprising that I do so as an individual. I never expected that such small teams in such entrepreneurial commerce might think and execute at such large levels. The last time I tried to envision such were when I considered Black Rocket and then the launch of [Joyent](https://web.archive.org/web/20250211214647/https://plus.google.com/u/0/+joyent/posts). These were the guys who said they have the whole web thing licked.

By the way, what I've learned is that Linux hacking is way more important than I ever considered, because in fact few people are inventing new stuff as much as they are cobbling together interesting pieces in interesting combinations. Those pieces often go open, or at least people tend to talk about them openly. But the kind of visions I've been plagued with made me think that there were larger software engineering development teams than there probably are.

So it's clear to me that **AWS** is the place to be. They are the computing platform and I can clearly see a great deal more of IT from the perspective of the infrastructure AWS provides. Consequently I can implement more ideas that make for more comprehensive solutions. The first cert on this pathway is AWS Certified Solutions Architect - Associate Level. And there will be more as soon as they finish developing the curriculum. I'm after the first cert ASAP.

Having passed the preliminaries, it's clear that AWS has evolved in an organic fashion. They have taken logical steps and addressed particular business cases, and I can see that in the shape of the classes so far. The simple products that have been around are now yeilding to more complex offerings, and the integration is good. There are some slightly troublesome areas for us at Full360 but only because we have customers outside of the main US Virginia region. We expect those to be handled over time. So, no big deal.

### Complimentary Combinations

I have just completed some work with a rather massive amount of data, quite enough to say that I have some experience with big data. There are several things I have learned.

**Data Management Matters**  
As a priority in dealing with big data, the less you touch it, the better off you are. Which means, unfortunately, that an iterative approach does not work very well. You need to know exactly how to deal with your data and you need to optimize the processes before you commit to them. A significant number of assumptions one normally takes for granted can no longer be taken. For example, if you have two or three ways to determine how to eliminate duplicate records within your data, you probably need to find \*the\* most efficient method. That means watching explain plans. That means timing a shell script vs a Ruby script. That means working processes 'close to the iron' rather than remotely.

**Sensor Data**  
It's rather obvious in retrospect but when you are dealing with 'sensor data' most of it is numbers. That means there are not a lot of attributes and keys for you to deal with, and compression is not going to go as far as you normally think. Therefore the grain of interest for your end-user queries is of paramount importance. Your time dimension means everything. Know the time scope of your queries and partition your data appropriately.

**[Postgres](https://web.archive.org/web/20250211214647/http://www.postgresql.org/ "PostgreSQL") Rules**  
I have been playing with Postgres for about two years now, and there have been a lot of theoretical benefits for doing so, not the least of which is that it is rather standard and has decent free tools. Now that I do so much more work with Vertica and Redshift, Postgres is my best friend. And I suspect it will remain that way as I start playing with VoltDB. Postgres on my Mac is everything that was once Access, Excel and MSSQL Express. And 95% of my code is portable. It makes a huge difference.

**Rubular Expressionism**  
Everything I need in an ETL, I hand build with Bash, Ruby and Regex. My partner in this exercise in crime is [Rubular.com](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/aws/page/3/Rubular.com) It is the singular most irreplaceable tool in my kit. I now have a large string of parsing templates in Ruby, many of which simply require just the right regular expression. But let me go into detail for a moment.

**Digital Industrialism**  
I am convinced that the Digital Renaissaence is just about over. There are a lot of innovations left in our imagination, but the fundamental leap forward in handiwork is just about complete. In a way, we coders are all like stonemasons in a world increasing dominated by poured concrete. There are two ways to look at this, and I look at it, despite my proclivities towards hand-building, as a good thing. On the one hand, you don't build cathedrals with poured concrete, on the other hand, you do build giant factories and skyscrapers. Cathedrals are spectacular and fascinating. Skyscrapers and factories are mundane and boring. But the work that runs the world happens in the utility buildings. You may be inspired to pray for safety in the cathedral, but you build airbags in the factory.

So now that our tools are all grown up, we are moving from the Digital Renaissance to the Digital Industrial Revolution. I'd like to think of myself (with any luck) as a digital industrialist. This would be in contrast to a Digital Impressario or a Digital Tourguide. I have to say that at long last I look at Social Media as an evolutionary dead end. (Another Story)

What I mean by having my tools all grown up is precisely what I've been talking about with database interoperability and multiple database systems. We at Full360 are very serious about building open platform systems in which we ingest data into massive storage, manage data and security with key-value store databases, process transactions with tech like [VoltDB](https://web.archive.org/web/20250211214647/https://www.youtube.com/embed/w2hCJIZz3n8) and serve [big data analytics](https://web.archive.org/web/20250211214647/https://en.wikipedia.org/wiki/Big_data "Big data") with Redshift and Vertica. Is that wild or what?

By the way we are looking to be on the verge of hacking virtual platforms as well. We have already seen AMIs working in VirtualBox and VMWare. It's only a matter of time before we can spin up databases of platforms for databases. We are deeply into that kind of customization. So yeah, that's another one of my old geek dreams coming true - what I used to call '3DB systems', then thinking of multidimensional, relational and object oriented databases in one system. (The impetus for this dream was a lack of a CORBA toolset for requirements we got from I2 Technologies 15 years ago - prior to the release of the Java API for custom Essbase functions, but I digress). The dream was downgraded to a desire to get 'double DBAs' working for Arberion...

So I want to be a digital industrialist now that I'm all grown up and that means realizing the dreams of 'operational business intelligence' or in other words, dealing with the larger scale structured transactional data previously off limits to non-shardable analytic database engines. OMG it's like rural electrification. There is so much data we can now deal with. Not long ago we in the industry talked about 'subject specific data warehouses', now we're talking about multiples of that at a price mid-market companies can handle.

For me, I've always preferred working with aerospace and manufacturing companies. Why? Because when you have tooled up a factory, you already know what data matters and the analytic value of it (if you could only capture and use it all). So now we can put the equivalent of a mainframe on the factory floor, in the engineering labs, and connect marketing and finance people too. Awesome.

**Mobile Alerts**  
The more I live with my iPhone, the more I realize that all I really need when it comes to business mobile computing, are alerts. So I'm going to go out and find something that delivers me IOS badges. Something a bit more specific and sophisticated than Twitter, but not much.

**What's Next?**  
Aviation.

### What I've Been Up To

What tumultuous times!

I've got to say it has been really weird looking at the empty space that is Cubegeek for the past 60 days or so. But one of my goals for the year is actually going to be convergence. I've finally put so many things in philosophical order in my life, at long last, that I don't feel the necessity to separate all of my avocations from my vocations. Plus I worked out a good deal with my own skills, my intentions and the good folks at Dreamhost. But there's a lot of ground to cover.

The huge news, of course, is Amazon Redshift which throws a big 500 pound gorilla wrench in everybody's business model. A number of pundits have pooh-poohed the whole thing but I have to tell you, this is a major part of the future, whether you like it or not. Redshift is Moore's Law for databases. It's impossible to ignore. Quite frankly I'm not even sure how I can deal with the fact of its existence, because basically somebody with a reasonable amount of skills can put together a data warehouse, quickly. The upshot is that a lot of consulting can be done at home, the way I do it, and a lot of cheap - even throwaway DWs can be built. This has scary implications for the quality of said DWs and nobody knows exactly what sections of the market Redshift will come to dominate, but I can tell you this, our friends in the database world are defacating building materials.

I have been working with Redshift for several weeks now and its strengths are many. Primarily, I'm all focused on its elascticity and its price. Additionally I like that I can script everything at the API level. I haven't done all that yet, but I know that I can. It is lacking some nice developer tools at the Toad level, and if I were one of the guys at Panic Software, I'd make sure that is my next project. As much as I love the Bootstrap web interface that Amazon has got running, nothing beats a finely honed fat client. Anyway, the biggest strength of Redshift right now is its ability to load data from S3, and we're thinking up some techniques and product designs that are going to take advantage of that. So check back with me in six months and ask about Project Kleiglight. In the meantime, we are learning by doing in Redshift.

Here's my first opinion. Everybody who is using MySQL or MSSQL should migrate to Redshift as soon as they think they're ready for more performance. Period. Whatever market that is, I'll take it.

Here's my second opinion. Teradata is toast.

\--

My Ruby-fu is up marginally. I picked up the Nokogiri gem and am now working a bit smarter with File. I've done some nice integration with standard unix command and also with loggers. So I would call myself competent with XML, YAML and JSON. I still haven't swung back to improve my Cucumber but am plenty comfortable with **rspec**. I'm working on a utility gem of my own for some text manipulation stuff that I do all the time. Next I'm going to play with the **parallel** gem to see how I can scale up certain ops.

I'm lagging on my seal book - the OReilly on Exploring with R, and I'm finally getting rid of the paranoia that sent me wheeling two months ago. Nevertheless, I still read Darkside and attend a couple security hacker meetups.

I've seriously upped my Chef game in the past couple months. Working on our elasticPM code has gotten me fairly deep into the implementation end of orchestration. It is now clear to me that much of what we have been doing is so utterly advanced - we've been on the edge in many ways of what Chef can do with Windows, and our unorthodox approach has been what has been making Chef's learning curve more difficult than what I expected. In addition, working more with Vagrant has improved my capabilities with virtualization. [The next version of Vagrant](https://web.archive.org/web/20250211214647/http://docs.vagrantup.com/v2/why-vagrant/index.html) is going to be awesome, I hear. So I've got about a dozen VMs here on my Mac. As they become migratable into AWS AMIs it's going to be awesome.

Speaking of which, I did get a chance to migrate an AMI across a region via the (2 month) old way of moving core snapshots. So before I could write code to automate that (but I've been busy) Amazon introduced a way to do it directly. So I haven't done it the newest way, but there's one more barrier to internationalization knocked over.

You have to realize that these days I consider myself to be something of an IT guy in the biggest IT shop on the planet, which is AWS. The new architecture is improving every month. More on this separately.

\---

The reintegration project starts with me getting into a couple, three web architectures. I've gotten the static blog thing worked out with Jekyll and Octopress. So I'll probly migrate all this Cubegeek stuff under the single new site. But I really have to get this Node.js and Rails thing knocked out so I can speak that language to customers as well. You see a lot of our business comes from people with low resistance to moving their assets to the cloud - since a lot of them have used colocation before. I'm going to try to head a lot of them off at the pass since Amazon has DynamoDB, RDS, Redshift and Hadoop, three of which I've had my hands on. So a lot of the confusion I used to have over MongoDB, Cassandra, Riak, CouchDB and SOLR, I no longer have. I just ape the party line and say go Dynamo.

\--

Vertica has been very very good to me. So my take on this in splitting the difference goes something like this. Redshift is for when you have invested \*some\* time into your DW and you want something low maintenance. Vertica is for when you need to tune the crap out of your system and you want near-realtime stuff. Basically, Vertica has all the bells and whistles for extreme computing. Redshift is more like MSSQL to Vertica's Oracle. Sorry, I hate analogies too, but that's about as close as I want to get to a hardball assessment in this post. I've played with a lot of databases in my time and I love Essbase and Vertica for the same reasons - their internals are beautiful and they enable an entirely new class of computing. However, I like Redshift for the same reason I like MSSQL, simplicity and elegance - except I know Redshift has a lot more upside than MSSQL.

I have worked with just about every major database technology going back to something called BCC out of Utah. Right now is the golden age, because today we have all the major technologies available in stacks that can be built on Amazon. It a very exciting time to be a data architect.

### What's New This June

The past couple weeks' geekery has been focused primarily on [RSpec](https://web.archive.org/web/20250211214647/http://rspec.info/ "RSpec") and improving the quality of my Ruby objects. So while I've been knocking out some practical stuff with the RightAWS API from a top-down, procedural programming paradigm, I've had to rethink in order to refactor. That means applying some different principles to my coding.

In some ways, RSpec makes that very easy, in other ways it's complicated by the inner and outer loop priorities of using it with Cucumber. One is behavior driven and the other is test driven, rspec being the latter - and when I know exactly what I'm doing in the context of an embedded system, one is pretty much the same as the other. What I'm missing, of course is the vocabulary of Web based programming with its object models and its brokers, controllers and whatnot - abstracts for generality. My bias, of course, goes to having the damned code do what I want it to do, and I have generally known how to make that happen, living off of code from Christmas Past.

But since I'm not familiar with all the objecty things I can do with Ruby or how marvelously it abstracts up with elegant constructions, all this Cucumbering and RSpecing can be pretty useful. Now just combine that with not only git but git-flow, and you've got something. Well, I've got something - a handful of tools which are starting to feel natural in my hands. So now while I'm still a sophomore journeyman, I'm starting to use more vocabulary, and getting even a bit wonky perhaps. We'll see. I've got code reviews coming. Still, I did get a chance to eyeball some code that was totally perplexing just nine months ago, and I have the nerve to be haughty about how it ought to go. What's clear is that we're starting to gel as we generate more code, common language and recognize each others' coding style.

In the meantime, I just concluded the Vertica Bootcamp. And I forgot to ask for stickers.

Everybody has seen the [Wikibon](https://web.archive.org/web/20250211214647/http://wikibon.org/ "Wikibon") (or was it Gartner) report that Vertica is number one for big data market share. Right about now, as they are newly on version six, I would say that they are about as advanced as Essbase was - technology-wise, at its version six a dozen years ago. But Vertica is a much smaller company and big data seems to be a newer market. So that's all to the good. Their technology is baked and almost nobody is pushing their limits. I predict, of course, that the big data market will swallow the rest and not much of what lives in todays relational stores will remain relevant for very long. The technology is being tested, by the likes of Zynga as everybody knows, but will do much more as people wrap their heads around what is possible.

That leaves me thinking about a number of things. The first is the availability of cheap vizualization tools. So I'll add that little task onto my part-time plate. The second is a review of what is actually possible. And since I'm cool with the open sourceable, that means looking at NASA's new technology transfer portal. But there's also the obvious.

What's obviously possible is the upgrade path of the mediocre. I shouldn't care as much as I do, but I don't like the idea that Microstrategy might just now finally have a backend that makes all of its promises actually work. Sucking up that back-end business ought to be a no-brainer, and if HP or anyone here in the States can make heads or tails of exactly what it is that Autonomy is supposed to be accomplishing (The company reminds me so much of ePiphany.com, that it's creepy) then maybe it will get sucked into that marketing. But I try not to worry about that, because I still have my own ideas.

So next I'm off to master a bit more resource management for Vertica and then bring some of my old models along and see how well they work. I'll tell you this for sure in a heartbeat, Vertica is perfect, and I do mean scary perfect for Essbase drill-through. In fact, I'm fairly certain that I could make it work in a hybrid cube. So maybe if I have some time, I might try that out with the latest Essbase Studio. I just love the idea that for Vertica, entry-level means a three server database cluster with 5TB of data.

So that's what's new, Magoo.

By the way, [Cringely is right](https://web.archive.org/web/20250211214647/http://www.cringely.com/2012/06/20/surface-tablet-intro-no-moses-event-for-microsoft/) about Microsoft Surface. The new MacBook Pro is not worth my money but still brilliant. Google Plus is fading into my background but remaining high quality. And I think **Evernote** is going to remain a winner.

[« Previous](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/aws/page/2/)

## Categories

- [AWS (24)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20250211214647/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20250211214647/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20250211214647/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |