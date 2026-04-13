---
title: "Cubegeek: Essbase"
source: "https://web.archive.org/web/20240407184741/https://www.cubegeek.com/essbase/"
author:
published:
created: 2026-04-07
description: "Big Data Analytics, perspectives from a 25 year practitioner."
tags:
  - "brain_spew"
---
The Wayback Machine - https://web.archive.org/web/20240407184741/https://www.cubegeek.com/essbase/

### Dodeca Rules Again

Tim Tow of [AppliedOLAP](https://web.archive.org/web/20240407184741/http://www.appliedolap.com/) is one of those guys you know in the industry that reminds you that excellence is its own reward. He has been one of the go-getters that I've always admired working with and knowing. We spoke together on the phone today for the first time in years and his baby, Dodeca, is all growed up.

As part of our strategic marketing at Full360 we will begin developing vertical markets for our data platform and go after those customers. After a long time of feeling rather sorry for Essbase and the EPM part of our business, the progress of Dodeca and its customer successes have warmed my old cold cockles. I've taken some notes about the things I most specifically need in Dodeca for a customer or two I'm thinking about. But here's the turning point. Dodeca has proven to me today that the true spirit of Essbase has not been lost and buried in the competition for the market domination of Oracle Middleware, which has been a battle royale for mid-tier technology in the enterprise market for years. What did Dodeca do today? It convinced me once and for all that Essbase can dominate with a single fat client reporting platform based on the world-beating concept of the spreadsheet. It's all the front-end Essbase will ever need.

For many years, there seemed to be nothing capable of beating the simple, pure combination of Essbase and the Excel Add-In. It was simple, fast and powerful. Then came a bunch of big front-end integration ideas that made sense on paper and passed muster of integration test, but lost the spirit and speed of discovery. Then, before ASO, Essbase itself was starting to show signs of fatigue in dealing with larger higher order dimensional models. And once that was overcome, came the problem of drill-through, which still had some security problems four years ago, not to mention timeout issues with APS when the data got big. Today, I believe firmly that a one-two punch of EAS driven Essbase and Dodeca's current version is all anybody on the planet needs for that holy grail of multiuser-concurrent-multidimensional read/write data with security down to the cell level. Ladies and gentlemen, welcome to the return of speed of thought, brought to you by C# fat client.NET brilliance. This is not a slow clap. This is a little bit of giddy excitement, and I'm really too old for that.

While Full360 has been plunging the depths of new paradigms of data management, parallelization and asynchronous data streams, real-time processing and massive query spaces, we've lagged a bit behind on the current comings and goings of the datamart world. In other words, we've been fulfilling our mission of being cloud-focused data experts. Now with some renewed spirit, our longtime friendship and partnership with ApplieOLAP brings to mind a lot of interesting possibilities.

So.. to wit.  
  

Highlights

- \- Essbase Java API
- \- All versions of Essbase since 6.5.3
- \- JDBC support
- \- custom starting points by user
- \- xcopy for.NET deployments to Citrix
- \- APS and/or straight TCP connection to Essbase
- \- MySQL, MSSQL or Oracle repository, no special server-side scripting
- \- Highly scalable to thousands of users.

Dodeca is the best way to get fast data out of Essbase. It is extremely configurable in ways that serve user requirements over technology requirements. It is a.NET based product that takes a bottoms-up approach to getting Essbase multidimensional data into grids. It has extended the ability of Essbase to deliver tens of thousands of rows at the old 'speed of thought' speeds. It is a managed spreadsheet environment under complete administrative control with hybrid drill-through capabilities.

Dodeca is entirely spreadsheet-centric and is exhaustively so. It uses highly specific defined data areas to perform multiple multi-sourced retrieves from data sources. It has control of all events both local and specific to Essbase API and remote JDBC operations. This allows a multi-layering, multi-query ability to draw data into the spreadsheet exactly where it is needed. Dodeca can employ any of the 300+ Excel functions to manage front-end calculations.

AppliedOLAP has re-engineered the spreadsheet interface and allowed Essbase to work to its full potential writing with C# that which used to be VBA. The product is clearly superior to all other Essbase front-ends. If you want to work with data in the spreadsheet paradigm, it is the gold standard. Dodeca's performance is remarkable and handles 100,000 row retrievals with ease. Its ability to cascade data into multiple tabs of a spreadsheet is beyond anything I've ever seen. It has managed both to allow highly complex database operations as well as keep basic ones fast and simple.

Mastery of Dodeca will take time. It clearly is aimed, for more sophisticated applications, towards.NET programmers comfortable with that level of detail and control. If you have complex workflow rules and highly detailed report requirements, you're going to have such people in IT anyway. But I see every indication that a quickstart implementation and its ability to use basic Excel templates support rapid prototyping any VBA competent guy can pull off with ease at smaller companies. No doubt AppliedOLAP with its long and deep roots in the Oracle customer community has plenty of third-party developers at hand.

I am impressed with Tim's direction in making a tool that, with its flexibility, makes for simpler implementation leveraging the dynamism of the Essbase query space, rather than fill up servers with canned reporting each with a single query statement. It's a win. And suddenly Essbase is way more interesting again.

### What's New This June

The past couple weeks' geekery has been focused primarily on [RSpec](https://web.archive.org/web/20240407184741/http://rspec.info/ "RSpec") and improving the quality of my Ruby objects. So while I've been knocking out some practical stuff with the RightAWS API from a top-down, procedural programming paradigm, I've had to rethink in order to refactor. That means applying some different principles to my coding.

In some ways, RSpec makes that very easy, in other ways it's complicated by the inner and outer loop priorities of using it with Cucumber. One is behavior driven and the other is test driven, rspec being the latter - and when I know exactly what I'm doing in the context of an embedded system, one is pretty much the same as the other. What I'm missing, of course is the vocabulary of Web based programming with its object models and its brokers, controllers and whatnot - abstracts for generality. My bias, of course, goes to having the damned code do what I want it to do, and I have generally known how to make that happen, living off of code from Christmas Past.

But since I'm not familiar with all the objecty things I can do with Ruby or how marvelously it abstracts up with elegant constructions, all this Cucumbering and RSpecing can be pretty useful. Now just combine that with not only git but git-flow, and you've got something. Well, I've got something - a handful of tools which are starting to feel natural in my hands. So now while I'm still a sophomore journeyman, I'm starting to use more vocabulary, and getting even a bit wonky perhaps. We'll see. I've got code reviews coming. Still, I did get a chance to eyeball some code that was totally perplexing just nine months ago, and I have the nerve to be haughty about how it ought to go. What's clear is that we're starting to gel as we generate more code, common language and recognize each others' coding style.

In the meantime, I just concluded the Vertica Bootcamp. And I forgot to ask for stickers.

Everybody has seen the [Wikibon](https://web.archive.org/web/20240407184741/http://wikibon.org/ "Wikibon") (or was it Gartner) report that Vertica is number one for big data market share. Right about now, as they are newly on version six, I would say that they are about as advanced as Essbase was - technology-wise, at its version six a dozen years ago. But Vertica is a much smaller company and big data seems to be a newer market. So that's all to the good. Their technology is baked and almost nobody is pushing their limits. I predict, of course, that the big data market will swallow the rest and not much of what lives in todays relational stores will remain relevant for very long. The technology is being tested, by the likes of Zynga as everybody knows, but will do much more as people wrap their heads around what is possible.

That leaves me thinking about a number of things. The first is the availability of cheap vizualization tools. So I'll add that little task onto my part-time plate. The second is a review of what is actually possible. And since I'm cool with the open sourceable, that means looking at NASA's new technology transfer portal. But there's also the obvious.

What's obviously possible is the upgrade path of the mediocre. I shouldn't care as much as I do, but I don't like the idea that Microstrategy might just now finally have a backend that makes all of its promises actually work. Sucking up that back-end business ought to be a no-brainer, and if HP or anyone here in the States can make heads or tails of exactly what it is that Autonomy is supposed to be accomplishing (The company reminds me so much of ePiphany.com, that it's creepy) then maybe it will get sucked into that marketing. But I try not to worry about that, because I still have my own ideas.

So next I'm off to master a bit more resource management for Vertica and then bring some of my old models along and see how well they work. I'll tell you this for sure in a heartbeat, Vertica is perfect, and I do mean scary perfect for Essbase drill-through. In fact, I'm fairly certain that I could make it work in a hybrid cube. So maybe if I have some time, I might try that out with the latest Essbase Studio. I just love the idea that for Vertica, entry-level means a three server database cluster with 5TB of data.

So that's what's new, Magoo.

By the way, [Cringely is right](https://web.archive.org/web/20240407184741/http://www.cringely.com/2012/06/20/surface-tablet-intro-no-moses-event-for-microsoft/) about Microsoft Surface. The new MacBook Pro is not worth my money but still brilliant. Google Plus is fading into my background but remaining high quality. And I think **Evernote** is going to remain a winner.

### Essbase Studio Is Half Secure

The purpose of this document is to explain what we consider to be a gaping hole in the security capability of Essbase Studio which makes it quite impractical for consideration in any real enterprise applications. I will explain why this is a fundamental oversight.  
  
**The Essential Problem**  
Oracle Hyperion Essbase, as the premier multidimensional database establishes itself as head and shoulders above relational solutions for many reasons. One of the most important reason, and why it excels in financial applications, is because its security model is so powerful. One can, if desired, restrict users to see any specifiable set of cells in the cube through the power of multidimensionally aware filters. These filter definitions have been expanded over the years to include the powerful meta\_read facility that even restricts users from knowing which parts of the cube they don’t have access to. Relational database security, by comparison, is crude.  
  
So with that high standard of security modeling in mind, I have put together a design for a significant Oracle customer which expands their user’s view into detail data by using Essbase Studio and offering several drill through reports. I presumed that the Oracle security model would somehow extend beyond Essbase through Essbase Studio’s drill through facility. It does not. In fact, there is essentially no way to secure drill through.  
  
From a user’s perspective, all of the aggregate data in the cube is very useful, and the detail below is useful as well. For this application, which will serve on the order of 300 users nation wide, it represents the single version of the financial truth. They will be assigned security on a need-to-know basis, and we expect there to be somewhere around 30 to 50 different access categories. The users see Essbase and Drill Through as a single application, as they should. They will access it through SmartView, which they love. It’s all Hyperion branded product and it should all work together. However when the details, for example, of sensitive expenses cannot be secured, it throws into question the entire value of Essbase Studio.  
  
**The Key Requirement**  
For our design we have a singularly important requirement. Our drill through reports must provide auditability of detail over broad selections. Our users don’t want to just look at the journal entries for one account, but for several accounts. Our users don’t want to check the P.O.s for one vendor, but for several vendors. So the key requirement has arisen that the drill through reports should allow a user to select a dimension at a high level and bring back all of the level zero detail. We don’t expect to bring back just 10 rows for a single account or department, but hundreds and even thousands of rows.  
  
So our key requirement is that custom SQL code for the drill through be constructed such that any arbitrary combination of parents in any of several dimensions may be selected and all detail below those parents are brought back. Here’s a two dimensional example.  
  
The director of a sales business unit that includes several departments wants to view the detail of all Travel & Expense accounts. This includes two dimensions, Organization and Account. The secured dimension in this case is Organization and the Business Unit director has access to a total of 12 departments. He also has access to all accounts in that dimension and ‘Travel & Expense’ is also an aggregate of a dozen lower level accounts.  
  
The sales director is given permission to see only data in his business unit and below. In this case Texas. His 12 departments correspond to 12 cities and regions in Texas. All of this security can be very easily accomplished in Essbase with the following filter.  
  
meta\_read @IDESCENDANTS("Texas")  
  
Thus the Texas sales director cannot see any account data above Texas and all account data at and below the Texas level in the cube. But when it comes to drill through, all of that changes.  
  
**The Details**  
Drill though reports are defined in Essbase Studio in three ways. The first is by dimensional context, the second is by SQL code, and the third is by model association. The dimensional context tells the system when the user can drill through, the SQL code determines what data will be brought back, and the model association tells the system which Essbase cubes are enabled for the report. In dealing with our security issue, the dimensional context is key.  
  
For our drill through we may have six, seven or more dimension contexts defined. A typical set of contexts for a drill through would be Organization, Account, Product, Project, Period, Year & Source. In the design we have specified both Fixed and Variable Contexts. The Fixed Context is one in which the specific dimension selection works like a filter. Select June, for example and you get only June data in the retrieval. For our purposes, Organization is a Variable Context. Pick Texas and you get Texas and all of the children of Texas. We have created special logic tables on the back end to facilitate this feature and we have prototyped several other solutions to the matter of Variable Contexts. All perform well.  
  
The problem with security manifests itself in the following manner.  
  
We have secured the Organization dimension and there are several other levels of access granted. For example the Regional Sales Director can see all of the Southwestern states including AZ, OK, NM, & CO. This requires, essentially that we allow users to drill down from any level in that dimension. But the problem exists as long as there is more than one level of access granted in any secured variable context dimension.  
  
The Texas director navigates freely in the cube via SmartView. At organization levels higher than Texas, he can only see ‘#NoAccess’ in the displayed cells. However, Essbase Studio’s dimensional context definition for the drill through report allows him to select a cell that says ‘#NoAccess’ and execute that report!  
  
That means he can select ‘Southwest’ and the drill through report will execute the variable context and show all the detailed information for TX, AZ, OK, NM & CO. In fact, there is nothing stopping this user from selecting even higher in the organization dimension and seeing everything.  
  
No access means no access in Essbase. To Essbase Studio drill through it means nothing. As long as there is a legal context, the drill through report will execute regardless of what Essbase security says.  
  
**Failed Workarounds**  
We have tried several different ways around this problem.  
1. Perhaps we could create a number of different drill through reports and segregate users according to their level of access in the secured hierarchy.
2. No. Drill through reports are not items that Shared Services can provision to. The lowest level of access in Essbase Studio grants access to run all drill through reports.
3. Perhaps we could identify the cell contents and pass a parameter back to the SQL definition so that when we see #NoAccess, we return no rows.
4. No. There is no way to communicate that parameter back to Studio.
5. Perhaps we could identify the Essbase user and send pass that back as a parameter back to the SQL definition and attempt to replicate Essbase security in the relational source.
6. No. There is no way to communicate that parameter back to Studio.
  
So essentially we are put in the position of communicating to our customer that even though this is an Essbase application, security cannot be enforced.  
  
It appears to us that there is a relatively simple fix somewhere in the product stack. Clearly SmartView is aware, and making judgments in real-time about the legality of contexts. We have observed that selecting any data cell after an Essbase retrieval will show the availability of none, one or more drill through reports. So we see that SmartView is plenty smart enough to block access to drill through. We’re just absolutely shocked that it doesn’t.  
  
We hope that Oracle will find a way to overcome this gaping security hole in Essbase Studio / Essbase / APS / SmartView. It’s one application. It should work with one security model.

### APB-1 Benchmark Results

*(from the archives)*

Now here's something we haven't seen in a while.

[Download OLAP Benchmark Comparison\_3](https://web.archive.org/web/20240407184741/http://cobb.typepad.com/files/olap-benchmark-comparison_3.pdf)

[Download OLAP Benchmark Results Summary\_3](https://web.archive.org/web/20240407184741/http://cobb.typepad.com/files/olap-benchmark-results-summary_3.pdf)

### Select Star

File this under:

HOW DID I NOT KNOW THAT?

I have been selling the Essbase SQL interface short for many years. Apparently, if you put everything into the top SELECT window, you don't have to put any code into the FROM and WHERE windows.

I have been performing complex SQL in SQLNET clients and spooling them to text to be picked up by load rules precisely because I was told that Essbase' SQL interface could not do the complex queries. I always thought it was a stupid waste of and ODBC connection if all one could do is simple selects, and I have gotten on the nerves of more than one DBA whose indignation at the suckitude of such an interface was righteous. It turns out that, at least in 9.3.1 and above, the SQL interface can handle the complex stuff. You just put it all in the top window.

Simple!

### Spelunking Through The Stack

Today I start building my massive server in earnest. As we speak I'm dowloading a big hunk of software from Oracle. They were very smart to do some of what Hyperion did which was to put all of their supported versions in one place so the customer base could get at it. But they went one further which was to rely on their legal teams and not their DRM to control distributions. So I've got access to the entire stack of software which I can use as a developer and not worry about calling 15 different people to negotiate a developer's license. I'm glad that era is over.

That doesn't change the fact that it takes time to assemble all of the right pieces and installation and certification of the installation is a bear. So that's where I am now. I'm getting OBIEE, Essbase, Informatica, Analyzer and Warehouse Builder. That should allow me to recreate, as is my intent, a big library of my greatest hits. Which is to say, I'm going to, as time permits, put together the biggest collection of demo apps the space has ever seen (if I say so myself). See I've got over 100 different customer histories in Vault 107, and I intend to strip them down, very carefully so as not to violate that sacred trust between developer and customer, and remake the salient pieces of their applications into a thing of complex beauty. Half of my task is to pick 20 from the 150 odd and prioritize. But that's just half the fun.

I remember doing this the first time when I moved from Pilot Software over to Arbor back in 1996. I was amazed at how easy it had become to build what had taken months in just a matter of days. So if these products are all that, I should be able to build in a matter of weeks, the best of what I've been doing the past 11 years. What's going to help is that I'm going to use my new Java skills (fingers crossed) to flesh out a multidimensional data generation tool whose core code I've already written in Perl. With any luck, I'll be able to figure out the API pieces and get it to read an Essbase outline. So this is my private project for 2009, which is to build a rather sophisticated data generator that will read your outline, and generate fake data so you can do performance testing. So far as I know, no such tool exists.

What I really want is a database scale visualizer - something that parses the Essbase index and then gives a navigable kind of heat map or something which allows developers to quickly asses what data is doing in cubes. For example, wouldn't it be cool to have a visualizer that allows you to see a calc as it's processing? Something like that. I know that it's stupid ambitious, but hey. I'm getting bored with politics and freeing up my time to do technical things.

In the meantime, the installation continues.

### New Year New Essbase

I bought myself a new server for Christmas. It's a Dell. I'm probably going to buy a new one every three months until I have a nice rack in my home office. I've grown tired of waiting for the guys at corporate to get the virtual lab working. I think I have a better chance of getting a little farm working that I have full access to.

The first task is done. I've got the AV and the network connected. As we speak I'm downloading Essbase 11. I'll follow Tim and the other Ace directors' instructions and put the damned thing together. 2009 is going to be a very deeply technical year for me. I'm just very happy in my job and feel like I've got lots of time and don't need to be such a careerist like I used to be. I can focus on getting deep into some technical matters.

What I'd really like to see is a good understanding, as I said before, of the Java interfaces. I have an old licensed copy of Dodeca around here somewhere. Maybe I'll play with that. But what I really expect to have a lot of fun with is generating a model library complete with fake data for various aspects of the energy industry. I'm so very pleased that my parent company is deep into the energy business, especially with the new acquisition of Piocon. I had a chance to work for Shell Services in Houston way back in the day and it was so cool to work with a company that had the resources to do things right. Same with Northwest Utilities. Back then I used to have to worry about shortcomings with the product. Now there are very few - it's more capable than most IT guy's imaginations - so we'll see if the Oracle engineers have done right by the great spirit of Essbase. I believe they have, which means the new Essbase is going to be all that. Match me up with the right company in energy and it's going to be delicious.

In that vein it will be interesting to see how these carbon management programs get going. I think that anybody who is serious about that is going to go through several generations of thinking their way through managing best practices. That's tailor made for Essbase EPM. Fingers crossed.

### Just Enough Essbase To Be Dangerous

Essbase is a rare and beautiful thing. It doesn’t take much to get it, as most financial oriented managers have learned. Anybody who loves Excel, and there are millions of us, love Essbase for what it does. Nobody should ever forget that the ESS in Essbase stands for Extended Spread Sheet. It was designed to be the multidimensional database that organizes all of your spreadsheets, and it is still brilliant at that.

But Essbase is also a fully mature multidimensional database system. Not just a spreadsheet backend, but an enterprise class backend to every numerical report any company can think of, and a whole lot more that most never think of. The problem is that few people have just the simple Essbase, they have System 9 Essbase and soon will be dealing with Oracle’s Essbase 11. I must say that I do love the sound of that, ‘Oracle Essbase 11’. It is the fulfillment of many dreams. But it’s also damned complex.

Among the biggest mistakes made by newbs in the Essbase world are:

1\. Sitting Essbase under the CFO’s desk and out of the sight of IT.  
2\. “Boiling the ocean” and putting everything in one cube.  
3\. Not hiring an Essbase programmer.  
4\. Building with Essbase with a DW methodology.  
5\. Building Essbase without a methodology.

Let’s talk about mistake number one, which is almost always associated with numbers three and five. This is the ‘just enough to be dangerous’ scenario. It marks the limited utility of Essbase, by cementing in place those practices that make it almost impossible to expand the scope of Essbase applications.

Essbase is the most scalable multidimensional database system ever. It has been for seven years, ever since parallel calcs and multi-server partitioning were enabled in version 6. But the combination of newbie mistakes 1,3 and 5 conspire against its scalability. But because Essbase is a rare and beautiful thing, and always an order of magnitude more usable than the systems it replaces, scalability is not what’s on functional user’s minds. It’s all about linking up those spreadsheets. Lock and Send. Drill down, pivot. These are the verbs of interest, not ‘automate’, ‘partition’ or ‘architect’.

It was the culture of Hyperion that sold the ease of use of Essbase. Unfortunately, the ubiquity of finance people who desired ease of use was no match for the ubiquity of SQL programmers who defied ease of use. So in walked the legions of Business Objects folks who have dominated most of the front-ending of data streams issuing from relational database systems, as well as a skewing of what BI has become. Or rather, what OLAP has become. People forget that OLAP was all about working with data, not just presenting it. And because of the shortcomings of 4GLs like SQL, working with data has happened mostly in BI at a slow, semantic level. And we have drowned in a sea of semantics which has now grown up into its own beast, codenamed ‘business rules’. Here’s a rule, if no more than five people can describe them in plain English, something is likely to be overcomplex.

Try this one on for size. If a company wants weekly data because cashflow is an issue, ask whether or not they are working on a 4-4-5 calendar. This has been the best practice way to deal with fiscal data on a weekly basis since the MBA was invented, and probably before. If they are not, the reason why is very likely because they would have to reprogram a mountain of business rules across a bunch of database and reporting systems. Nightmare right? Not with Essbase. I could convert it all in a day – end to end. That’s what working with data means. 4-4-5 was not invented yesterday. There’s no good reason why dealing with it should be difficult, but it is, because SQL is a general purpose language whose generalities constrain the way business managers look at their own data. This is a sad thing. Your systems should not limit your imagination or constrain your vision, they should enable it. Unfortunately, too many of us are all too happy just to see some numbers in a familiar format. Lucky for BI, stultifying for OLAP.

But let’s get back to the newbie problem, which is not ramping up on the IT side and knowing just enough about the technology to be dangerous. There are several expensive consequences of underinvestment in your Essbase tech.

1\. Over reliance on external support.  
2\. Under development of the language of BPM.  
3\. Failure to understand product capabilities.

The obvious results of consequence 1, is that you pay for expensive consultants to develop your applications. The temptation is always to skimp. Either buy a ‘wholesale’ consultant or skimp on the project plan with national consultants. There are innumerable ways for companies to short-change themselves by managing project to the penny rather than to the objective. I won't get into that exhuastive list. But the bottom line is there aren't many ways to avoid the pain of reforming your business practices, and if that's not the aim of your installation of BI and OLAP, then you're just buying software for the pretty charts.

The more insidious difficulty is with consequence number 2. Like everything else in this industry, technology is moving forward quickly. And because all of the big companies are driving product requirements from the now-consolidated product vendors, product offerings get more complex. That means understanding of what features are built into the products follows. In other words, this is not like buying cars where the more expensive car is just more of the same. It's more like buying a seven course meal in a French restaurant - you can't just eat it the same way you chow down a Big Mac.

EPM is the rallying point for all of the marketing associated with what was once merely BI, and people have little choice but to have their favorite products and technologies merged into stacks that make sense from an EPM perspective at the enterprise scale. The era of small perfections is over, now is the era of interoperability of OLAP in industry specific verticals and enterprise class systems, meaning enterprise class politics and governance. Meaning opportunities for gobbledygook to confuse and clutter all talk about your systems. If you don't understand where the industry is going, where EPM is going, you're going to have a hard time getting the attention of the best and brightest consultants.

Consequence three of underinvestment is a failure to keep up. I think we're all guilty of that to a certain extent. I don't know enough MDX to save my soul and Aggregate Storage? Heh. I know about 10% more than your Oracle salesguy knows. That's not a problem for me, because I get it quick and I have at least 5 new projects every year. But at your company, technology gets stale and you get behind. How many of you are on Essbase 6, raise your hands. That's 7 years old people. You have two conversions to go and one of them is painful.

I hope this is an incentive for you to get a bit closer to your Essbase technology. It is the king and world-beater and it is, as it always has been, a very satisfying product to know as well as use. Don't hedge your bets. It's Oracle now.

### An Essbase Support Model

(also from the archives - circa 1998)

i've seen a bit, being out and about in the field.

Here are some of the things I think would be crucial to an ongoing Essbase support function. In no particular order of importance.

1. Centralized account authority. Someone who centrally issues accounts and monitors activity on all servers. This should be someone separate from those who gives access to the individual cubes and filters within.
2. A high level person who maintains an ongoing dialog with DW / and or legacy systems folks. Sooner or later there is going to be some conflict over the best way to deliver end-user applications. You need to get ahead of this process and negotiate the efficiencies of OLAP access vs relational access for all users. Right now we are at the beginning of the OLAP application development period. Just because it's Finapps now doesn't mean its not Call Center Apps tomorrow.
3. Also metadata planning and repository stuff should also be a primary function of this liason with data production staffs. You need to insure that all data production issues are related to the OLAP staff. If your company is just moving to client/server, NT or ERP this is especially important. Know where the data is coming from at an enterprise level, and be on the cc: list for changes to dataflow.
4. A Business Systems Analyst should have some Essbase experience, or at least have a good idea of what kind of systems could be built in the OLAP area. Get someone who knows where all the analytical bones are buried.
5. A centralized liason to Arbor. This is the person whom should track all calls to tech support, be aware of maintenance, license and patch issues. Should be in touch with Arbor regarding seminars, Dimensions, product introductios, enhancements, 3rd parties, OEM vendors and other Essbase users in your industry and geography.
6. Get a high priced OLAP DBA and guarantee job security. Pay your own employees now, or pay $100/hr consultants who don't know your business later. I guarantee you it will become an issue within one year of your first implementation. Not because Essbase is not a Porsche, you just don't want your Porsche wrapped around a tree.
7. Leverage Essbase training (formal or informal) with every group you do business with. If you create an app with the Inventory folks, overtrain one of the power users.
8. Create cross-functional decision teams for each project. Gut a business guy who could care less about technology but is focussed on the bottom line. Get a technophobic nudge who cares about fonts, colors, ease of use, and how many 'clicks' they have to do. Get a power user who wants to do everything and revolutionize the whole company. Get a hotshot developer who keeps saying 'yeah we can do that'. Get an old-head skeptic from IS who won't be convinced even after the system is built. Get used to the dynamic of balancing all these demands and be determined to build a first-rate system that will last for at least 3 years.

Roll out functionality quick, get feedback from the nudge. Get the business guy's chalktalk and use his terms - show that the system logically follows his idea of how the business is supposed to be run. Get a clear idea from hotshot how fast she can deliver new code. Listen for the skeptic's warnings and prove him wrong. Show him why.

Deliver chunks of success which please coaltions of these folks, get \*them\* to roll it out to the end users. Take all blame, share all credit.

Next time you ask to create a functional team, you'll see a kindergarten forest of raised hands.

\--

Now. A seasoned Essbase DBA (somebody who has taken all the courses and built and maintained at least 2 cubes), should be able to recognize potential OLAP apps everyware. Such a person should not be afraid of tuning, and should be able, independently to handle anything technical that Arbor tech support recommends. You should get all your Excel macro jockeys, Access programmers, Foxpro pros, and SQL Server folks prepared to report into that DBA. They should be responsible for being able to know and represent business rules in the Essbase paradigm. To understand the cycle of (Build, Load, Calc, Report ) Anybody who is prepared to call themselves an NT expert should learn something about Essbase, because Essbase is what makes NT valuable, not the other way around.

Such a DBA, in a non-distributed environment, should be able to handle all the cubes needed. If you are going to use distributed OLAP and go cross-platform then you'll need two, in my opinion - especially if you build an NT&UNIX multi-partition application.

However in any case, that DBA should be able to understand, once explained, the business rules and businss model of any cube, but they should not be responsible for generating specs for that and maintaining all that. So I am suggesting that your main Essbase DBA be more of a data architect not a specialist in Finapps or Inventory or Manufacturing. That way you can leverage the NT specialists (macro jockeys, VB programmers) interests in familiarity with Essbase the same way they would be of SQL understanding thats where the more serious enterprise-wide/mission critical planning apps are built.

So if you could have a DBA who is capable of describing Essbase comprehensively to a VB guy who understands with the aid of a Business Analyst all the reporting, analysis, modelling, and planning needs for a particular department - then you have the basic team of 3 which can build a first rate app. Then you leverage the interests of the VB/front end programmer and the Analysts in Essbase knowledge, and you can do well.

If you have a more formal project planning culture and require a project leader and gantt charts and all that, then you should have two \*real\* programmers on the team. Again, Essbase is not idiot proof. Yes, you can go 60 mph in first gear in a Porsche...

### Essbase Security Provisioning: Welcome To The Jungle

I am currently only about 1/3 as happy with Essbase as I usually am, and that is because of outsourcing. Yes, Essbase security has been outsourced to external authenticators - and it is an outsourcing job I have studiously avoided since day one. Although I can say without hesitation that I have done a couple migrations of Essbase native users over to MSAD, I am deep into the jungles of it now dealing with a non-trivial case with thousands of users, hundreds of groups, scores of cubes and a half dozen Essbase servers in multiple environments. Welcome to the Jungle.

There is a lot to be learned in such a situation and I have yet to learn it all or even enough to feel moderately dangerous. That is primarily because as of 9.3.1, MAXL has been emasculated and mastery of this most wonderful language is not enough to get you through the day. Instead, you must master a different kind of beast if you don't want to be clicking buttons in a Java Console for the rest of your life. That beast is CSSImport, a command line utility of sorts that allows you to modify the mind of Shared Services.

The problem is that the mind of Shared Services has only one portion of the information necessary and the mind of Essbase has another portion. Keeping track of which knows what is a small nightmare. That's because, no matter how complex it gets, at least you can go back to EAS and the Shared Service Console and click your way through. Dealing with it on a large scale is a large nightmare because you simply cannot.

Now being a geek is probably not the best way to approach this part of the Oracle stack, because to us geeks, things have to make logical sense and basically work. And if it doesn't you should be able to RTFineM and figure it out, and failing that check Google Groups or some such helpful place. But those who know are apparently not saying, and most folks don't know. And so geek sweat. See it? All over my keyboard. But given my partial knowledge and desire to get \*some\* public information out there, I will endeavor to give a few pointers.

First of all, somewhere there is a master switch that tells EAS and Essbase to shut off half of its security brain and outsource such matters to Shared Services. I think this switch is irreversible, and probably after 9.3.1 it may not be an option. The outsourced functions have to do with creating users, creating groups and populating groups with users and other groups. So the following line of MAXL, once that master switch has been switched, no longer works or makes any sense:

*create or replace user joeblow as external;*

instead you will do something like this:

*#user  
id,provider,login\_name  
joeblow,LDAP1,joeblow*

And those three lines are stored in an input file. In addition to the input file, you need a configuration properties file and then you run a command something like this at the DOS prompt (or unix command line):

*CSSImport.sh properties\_file*

So now you have let the Shared Services brain know that joe blow exists in the company LDAP named LDAP1. I would show you the properties file, but I don't want you to be daunted yet. The Shared Services brain knows, Essbase does not know. So Joe is only part way into the system.

Next, you need to enter Joe into a group. If you think the jungle is bad now, imagine what it would be like without groups. Believe me, you don't want to go there. The short way of understanding this is to make a hard and fast rule that you will only provision users to Essbase applications via groups. It makes organizational sense.

'Provision' is a ten dollar word for 'grant access', sorta. I say sorta because I think it rather does dual duty between granting access and granting recognition. But that may be due to a partial understanding on my part. Since there are two brains to think about, it's hard to know which brain sees what and which brain grants what. Here's what I'm talking about.

What I believe is the following. When you use external authentication:

1. Maxl cannot be used to create or delete users.
2. Maxl cannot be used to create or delete groups.
3. Maxl cannot be used to add members to groups or add groups to groups.
4. CSSImport can be used for all of the above.
5. ~~When CSSImport is correctly used to import users and groups, Essbase cannot see them. EAS cannot see them either. So unless and untill a user does actually logon to Essbase, the user will not show up in EAS.~~

So this is a seeming paradox. You would think, now that Essbase has given up the right to create users, that as soon as Shared Services does create them, that they would send a little message over to Essbase and say 'Hey, lookee, new users!". ~~But in fact, you can create users in Shared Services AND THEN CLICK THE SYNCHRONIZE BUTTON in EAS and Essbase still won't know who these users are or that they exist. Forget about giving the new users access to anything, Essbase itself still doesn't know that they exist.~~

Oh wait, check that, that was a bug (ya think) that was patched yesterday.

In our installation, we have a particular issue which is that there are multiple user directories. We have two MSADs. Unless you patch Shared Services, this situation breaks everything. Well not everything, but a whole lot of things that are almost impossible to troubleshoot. See?:

> When two or more providers of the same type (LDAP, MSAD, etc.) are configured in the search order (for example, LDAP1 and LDAP2) and users from both of these providers are included in a Native Group that is provisioned to Essbase, only users from the last provider (i.e., LDAP2) are returned to Essbase.

That broke a whole lot of things for us, and only just now are we beginning to see the light. I will continue this series as I get closer to hacking through this jungle once and for all.

[Next »](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/essbase/page/2/)

## Categories

- [AWS (24)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20240407184741/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20240407184741/https://www.typepad.com/ "TypePad")

## Search

## Recent Posts

- [It Begins Again](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2023/05/it-begins-again.html)
- [Boxtag 060 - Lurkers, Scribbling & Proxy](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2021/03/boxtag-060-lurkers-scribbling-proxy.html)
- [Boxtag Idea #059 - Highlights](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2021/03/boxtag-idea-059-highlights.html)
- [Boxtag Idea #058 - The Greylist](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2021/03/boxtag-idea-058-the-greylist.html)
- [Boxtag Idea #057](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2021/03/boxtag-idea-057.html)
- [Revival](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2021/03/revival.html)
- [Day 17](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2020/05/day-17.html)
- [Closures in Go + Some Memories](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2020/04/closures-in-go-some-memories.html)
- [A New Leaf](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2020/04/a-new-leaf.html)
- [Three Years Later...Kafka](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2019/08/three-years-laterkafka.html)

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20240407184741/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |