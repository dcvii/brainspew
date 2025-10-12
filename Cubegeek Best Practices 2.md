---
title: Cubegeek Best Practices 2
source: https://web.archive.org/web/20160513031811/http://www.cubegeek.com/best_practices/page/2/
author:
  - "[[Cubegeek Best Practices 2]]"
published:
created: 2025-10-12
description: Big Data Analytics, perspectives from a 25 year practitioner.
tags:
  - clippings
  - cubegeek
---
The Wayback Machine - https://web.archive.org/web/20160513031811/http://www.cubegeek.com/best\_practices/page/2/

[Blog](https://web.archive.org/web/20160513031811/http://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20160513031811/http://www.typepad.com/ "TypePad")

## Search

## May 2016

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 2 | 3 | [4](https://web.archive.org/web/20160513031811/http://www.cubegeek.com/2016/05/transactions-the-final-frontier.html) | 5 | 6 | 7 |
| 8 | 9 | 10 | 11 | [12](https://web.archive.org/web/20160513031811/http://www.cubegeek.com/2016/05/red-vs-blue.html) | 13 | 14 |
| 15 | 16 | 17 | 18 | 19 | 20 | 21 |
| 22 | 23 | 24 | 25 | 26 | 27 | 28 |
| 29 | 30 | 31 |  |  |  |  |

### Producers, Consumers & Dynamic Data Warehousing

So we have a bunch of big ideas around here at [Full360](https://web.archive.org/web/20160513031811/http://www.full360.com/) and it seems that I have been doing them rather than talking about them. That's what I like about work. Here's what we're doing now.

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

### Longitude

Part of my interest is in the upscaling of Business Intelligence. No, I don't mean scalability in the classic computer science context, I mean in the class contest from going middle class to upper middle class and beyond. What I'm saying is that most of BI is downright dowdy. But dowdy as compared to what? Well how about this dashboard to start?

[![Aids](https://web.archive.org/web/20160513031811im_/http://cobb.typepad.com/.a/6a00d834515ae969e2017c34340744970b-500wi "Aids")](https://web.archive.org/web/20160513031811/http://cobb.typepad.com/.a/6a00d834515ae969e2017c34340744970b-popup)  
It is impossible for someone like me to look at this and see it as a dashboard with several database feeds behind it. But I know that it is not a dashboard, which is to say there are not live database feeds behind it. It is merely a picture. Granted, it is a marvelously pretty picture and it is worth 1000 words, but it is also a one shot deal. It is good for a month and then it is out of date, which means that everything about the business model for its creation is also a one shot deal. Get it out to as many people as possible and change their minds NOW. Forget about tomorrow and nevermind yesterday. This is static, and it's exactly the kind of stuff journalists do most of the time.

What if you got somebody like the graphic designer who put this brilliant snapshot in place with somebody like me who could set up live database feed behind all that data, with another front-end specialist who could add controls to tools that consumed that data. Wouldn't that be marvelous? It would, but it would only be a proof of concept. What it would not be is something anyone could rely on. That is because the world of people whose business is journalism do not generally communicate with the world of people whose business is business intelligence. But maybe that can change.

In this post, I'm going to jump on journalists for a moment. From here on out, every time I meet a journalist I am going to ask them if they have any longitudinal interests. We know folks like [Michael J. Totten knows the Middle East](https://web.archive.org/web/20160513031811/http://www.worldaffairsjournal.org/blogs/michael-j-totten) and we will always, always have a pressing need for essays, dispatches, and compelling writing of all sorts. But when it comes to communicating data, editors of journals need to do a much better job, otherwise their move into internet media is only half-assed. Seriously. What happened to classified ads is a classic case in point. Not only has that little marketplace shifted but its dynamism has increased tremendously since it left the hands of print journalists.

However, print journalists have a monsterous and massive advantage. And that is that they have attention span, context and connections. That makes them curators and that's how the best of them get to be the 'papers of record'. Bloggers can be excellent, but blog real-estate is not necessarily longitudinal.

What we need is an editor's hand at putting the history of matters in context for what essentially is a permanent exhibit. If you are the editor of the crime desk in Seattle, when is murder ever going to be uninteresting. Or as I was saying the other day to a journalist, how did milk cartons become the medium of choice for a search network of missing children. Every bureau in every newspaper has the capacity for becoming the data source of record, but only if they try. Who is going to try?

If you think I'm only talking about charts and graphics, you don't get me yet. Check out [Homicide Wach in DC.](https://web.archive.org/web/20160513031811/http://homicidewatch.org/) There are dynamic charts and graphics to go along with those, but this is social media hosting as well. Every aspect of a story needs to be put in place, and 'four column inches' is not the whole solution. What doesn't become referencable multimedia at the 'newspaper' website becomes market share for someone with the foresight to use all the technology. Now that there is AWS compute on demand for all such tech, there is no excuse. Again. It's all about the editors with foresight.

### Ouroboros

[![200px-Ouroboros-simple](https://web.archive.org/web/20160513031811im_/http://cobb.typepad.com/.a/6a00d834515ae969e20168eb208b4b970c-320wi "200px-Ouroboros-simple")](https://web.archive.org/web/20160513031811/http://cobb.typepad.com/.a/6a00d834515ae969e20168eb208b4b970c-popup) Somewhere in the sands of time that represent my association with Essbase, HP had something to do with a log analysis tool. Or maybe it was Dell. I don't remember. But the bottom line is that they decided that subjecting Essbase database logs to Essbase analysis - like a snake eating its own tail.

The model has User, Action, Server, App/Database, Date, DayOfWeek, Hour of Day.

When you have 300 users of an application and logs going back several years you can make some awesome histograms.

One of the forgotten arts surrounding Essbase development is the [use case](https://web.archive.org/web/20160513031811/http://www.techopedia.com/definition/25813/use-case "Use Case") approach to reporting. So often, the constraint of development resources and more importantly environmental constraints stop organizations from building specific data marts for specific use cases. When this happens IT teams overcommit to building a single cube for all users. This follows an unfortunate misinterpretation of 'a single version of the truth' when in fact it's more like 'too big to fail'. Enormous amounts of time, energy and frustration go into making sure that one cube doesn't disappoint, and yet it inevitably does. It's got one dimension that 70% of the users don't use. It's got a whole slew of old accounts in the dimension that are no longer active. It's carrying history that nobody actually queries. It's not ready for the crush of activity at month end close. And nobody wants to make any changes in production.

All these problems can be solved by re-engineering the cube and our team is working to make all of that easy again. Ouroboros is our extended analytic tool that takes Essbase logs, both the database log and the Essbase agent log and convert them into two Essbase cubes that show user activity. This is nothing particularly earth shattering or novel, but it's part of a more comprehensive package of performance monitoring at the ***application level*** that lends itself to making more information available to everyone. This information is actionable because we are drastically reducing the cost of redesign, rearchitecture and our key attribute ***elasticity***. Add this to performance monitoring and application migration at the ***system level*** and you gain the ability to add arbitrary amounts of capacity on demand. All with objective evidence generated by the platform itself.

### Clay Shirky on Process

There's a lot of text I'm going to get out of this idea. I know it well. One of the things I always see when I get started with a customer is the belief that implementing this system will solve their problems. It means they have fresh memories of the sales presentation. The promptly forget, because they don't know how to read, the embedded and implied caveats of the salesman's speech, and they specify what they want built to me. I listen and nod. As a designer and architect, I can make it happen. Here's what never gets discussed: process. So at the end of the customer's speech they finally give me the $10 question. Can we really accomplish all this? My answer is (now) "If you really want it."

Or let me put it more snarkily. I'm going to show you how to do more, with less, faster and more accurately, and you are going to tell me no, because it makes you uncomfortable.

It always comes down to that. If you want change, you have to change your process. The technology only facilitates change. It doesn't make change. You have to change.

[The Guardian Activate Summit: Clay Shirky Keynote](https://web.archive.org/web/20160513031811/http://fora.tv/v/c15544) from [The Guardian](https://web.archive.org/web/20160513031811/http://fora.tv/partner/Guardian) and [The Paley Center for Media](https://web.archive.org/web/20160513031811/http://fora.tv/partner/Paley_Center_for_Media) on [FORA.tv](https://web.archive.org/web/20160513031811/http://fora.tv/)

### Deadly Cancer

[![Pitstop3-big](https://web.archive.org/web/20160513031811im_/http://cobb.typepad.com/.a/6a00d834515ae969e20163031b98ee970d-320wi "Pitstop3-big")](https://web.archive.org/web/20160513031811/http://cobb.typepad.com/.a/6a00d834515ae969e20163031b98ee970d-popup) Back in 1980 I was a squid.

If you had a motorcycle in LA and you were young, chances are you were like me, the last of the tuners just before the era of the superbike. Me, I had a Suzuki GS 550 and my mechanic at Three Start Sport Cycles on La Cienega hooked me up with the Yoshi pipe, clipon bars, and tweaked my cam. One year earlier I got the fever haning out with the Wednesday Night crew at the Crenshaw Burger King. It's one of those stories that got blended into the mythology via Hollywood, but the whole world and culture will never be known.

One of the legends of the era was a dude whose name I remember to be Glen. He lived around the corner from me on Somerset. His car was a matte black 1969 Camaro called Deadly Cancer. Obviously the man had worked on it for years, but rarely ever raced it. He said it was a 10 second car and I believed him - it was scary loud and he could smoke those dragstrip tires. It was faster than my motorcycle, and my motorcycle scared me.

One Wednesday Glen took the car out to Jefferson, down in what is now known as Playa Vista. This was, at the corner of Beethoven St, our drag strip proving ground. He killed his competitor on the first run. Second run, he threw a timing chain. Mighty Casey struck out. Fortunately, I had no money to bet with, having spent it all on stereo equipment. Glen never put Deadly Cancer back together. It was over.

I think about the prospects for garage software in the enterprise. Once upon a time, and periodically, I wished that I could work for three or four years on a single enterprise wide Hyperion project. I have to be the most proud of the handbuilt ETL I put together many years ago. And of course I'm immensely enjyoing my Ruby hacking. How would I feel if somebody came in and told me that my design was crap and I'm about to throw a timing chain? Not very friendly, probably.

This year I found myself over at SpaceX. I am enthralled by the possibility that we may start again in space. Elon Musk built the electric car that all of Detroit couldn't do, and basically didn't do. And now he's demonstrating that space exploration can be capitalized in the private sector where once it was only the province of governments, and he's working smarter. So once again, all things aerospace get my blood up. So in that spirit I watched a documentary on the life of the Concorde SST. Another thing we don't do any longer, proving once more quite clearly that stupid politics can triumph over brilliant engineering.

They said it was a 12 inch piece aluminum that fell off a creaky old DC-10 sitting on the runway that caused the crash of the Concorde in France that fateful day. But with airplane crashes, enterprise software systems and scratch built drag racers, it's never one thing. It's a combination of small things just slightly out of whack that creates, on that one rare fateful occasion, the perfect failure.

If only the block size were slightly smaller and the hit ratio on the index cache was retarded enough to free up cache memory, and that one hierarchy in the accounts dimension wasn't dynamic and that one user didn't query three years instead of two... Every binary 'if' doubles the possibilities but most systems design choices are not binary. There are five or six possibilities - we get weary counting them. So rationally we focus on the big things. What's the dense/sparse config? Are these tables denormalized? Is this process multithreaded?

But its the aggregate of small things too. We need to get the big things right or the small ones won't matter, but when the big things are right, we still need to perfect the small ones. They creep into the system like cancer...

NASCAR and F1, but mostly F1 is my gearhead fix. It is awesome to me to know that these small teams can change major parts of a race car in a matter of seconds. There's no way a thrown timing chain could end a racing career. That's because the team works together to win and they practice, practice, practice selflessly together so that everybody knows everything. That's how a system gets to live another day. Everybody knows everything. That's the difference between the proprietary garage work and the great power of open source. That's what is being proven in the field every day. It's the difference between survival and triumph.

### Lesson of the Day - Ruby Serialization

[From Skorks](https://web.archive.org/web/20160513031811/http://www.skorks.com/2010/04/serializing-and-deserializing-objects-with-ruby/):

> Ruby has two object serialization mechanisms built right into the language. One is used to serialize into a human readable format, the other into a binary format. I will look into the binary one shortly, but for now let’s focus on human readable. Any object you create in Ruby can be serialized into [*YAML*](https://web.archive.org/web/20160513031811/http://ruby-doc.org/core/classes/YAML.html) format, with pretty much no effort needed on your part.

### More Cloud, More Chef

I’ve been talking about my cloudy future for a while and it looks like this fourth quarter I will be crossing the chasm and spending more and more of my compute work up in those clouds. I’ve had an Amazon AWS account for a couple years but finally the time I’m spending working in those is clouds is closing on the amount of time I spend working in traditional environments.

  
To solidify all that I will be adding another ninja tool to my belt which is [Opscode Chef](https://web.archive.org/web/20160513031811/http://www.opscode.com/). In a couple weeks I’ll be heading to Opscode’s bootcamp in NYC. Chef is basically a framework and toolset for configuring entire environments, something you almost never think about as a consultant who has to sit around and wait for infrastructure specialists or customer IT staffers, but once you get liberated of all that you think about a bit more.  
  
If you’re an Oracle or any sort of EPM consultant you know that the result of the thin client multitier inter-operative strategic directions taken a decade ago has introduced you to that dreaded word ‘stack’. No longer do you just deal with a product, but with a stack of services that support and interoperate with a suite of this that and the other. The days of simple client-server are over, or they are for the time being until you can use tools like Chef to configure your stack on the fly.  
  
So what we’ve already done at [Full360](https://web.archive.org/web/20160513031811/http://www.full360.com/) is make it brain dead simple to throw up an instance of Oracle 11.1.2 EPM or Vertica + Jaspersoft on AWS. That means, and believe me because just did it this month, I can do a POC in a week, just like in the old days. I can’t describe how liberating it is to be free of concerns about environment configuration and just focus on the application. But even more cool is how powerful I can be once I start taking for granted that I can use big and multiple virtual hardware any way I want. And this is where Chef comes in.  
  
What I’m going to do is come up with optimum configurations for all of the different sorts of BI, DW and EPM stacks I’m going to use. This means [Palo](https://web.archive.org/web/20160513031811/http://www.jedox.com/en/home/overview.html). This means Essbase. This means [Vertica](https://web.archive.org/web/20160513031811/http://www.vertica.com/). (OK I’m database centric, I admit it) This means a rightsized environment I can tweak over time and replicate with Chef recipes whenever I need it. My Ruby is a little crusty but I’m not particularly worried about it.  
  
Not to pat myself too hard on my back but a dozen years ago I was the first bloke to publish a capacity planning guide for Essbase. If I can remember how to think as sharply as I used to, this is going to be very cool as we at Full360 work with Amazon, Opscode and our elasticBI & elasticEPM customers to craft and maintain the ultimate environments.  
  
Can’t wait.

### Attribute Drilling

When you are creating a custom drill through report, there are some pretty cool things that are possible. One of the things I didn't think was possible but can be done is to use attribute dimensions instead of the root dimension for setting the context for a drill through.

It gives rise to a cool idea that almost was.

Imagine that you have three attribute dimensions on product. Color, Size, Type. It's a paint inventory, so color is the obvious biggie, but you have multiple sizes and spray, tube, can, and pail for your types. You want to select a bunch of paints without getting into shades of burnt sienna, so your high level attribute of color is brown, then you have light brown, medium brown and dark brown. Cool. But to drill down into inventory you don't want to have to pick the product sku. The answer is that you can use one or more attributes to narrow that selection in Essbase, but what about drill through?

We considered the problem for a couple hours with some previous work we had done. One of the cool things we did was design custom parameterized stored procedures that fit nicely into our design for drill through sql templates. For example:

select \* from getMonths("Apr","YTD") -> {"Jan","Feb","Mar","Apr"}

With functions like this in mind we figured we could do the same thing with attributes against a target table that didn't actually have the attributes as keys (saving us some time). So the function imagined went something like this:

select \* from getProducts("Dark Brown","8gal","Pail") -> {..long list of products..}

So here's the trick. With attributes, users don't necessarily have to bring all of them into the spreadsheet query context. In Smartview, I can bring in only Color, or Color and Type. Of course I could leave attritbutes out. So we figured how about extending the function to handle all possibilities, including those where you select the product outright?

getProducts2($$Product-VALUE$$,$$Color-VALUE$$,$$Size-VALUE$$,$$Type-VALUE$$)

would be the syntax within the SQL template.

Wouldn't it be cool if we could have smart iterations of the combinations drive context legality? So we could build drill through reports that allows you to select any attribute, any two attributes, or any three attributes or any four attributes, or just the product.

Sounds good in theory, except that you absolutely \*do\* have to know which parameter(s) you are passing from Smartview over to Studio. And that parameter set has to match the context definitions of the drill through. So even though we were thinking SQL NVL so that we could accept nullable parameters, we were constrained.

The other idea that sounded great at the time was that if we made a matrix of possibilities and then designed multiple DT reports with slightly different context definitions, then depending upon which context the user selected, the right report would show up. So for example, Report 3 would be binary 011 which represents notColor, Size, Type. Report 4 would be binary 100 which represents Color, notSize, notType. The problem is that any time you selected more than one parameter you would create legal contexts for several reports instead of just one report. (I leave that proof to you as an exercise).

So right now it seems to be an all or nothing deal, but there may have been something else we overlooked. Still, it did sound like a cool idea, neh?

### The Add-In Who Knew Too Much

I just wanted to make a little note about Smartview remembering things that perhaps it should not. This is especially the case if you happen to use different IDs for your Dev, QA and Production environments.

I have not been able to determine with any accuracy when Smartview decides to remember SSO information or when it does not, but I would say that it does remember more often than not. In fact, here is a problem a client just placed before me.

A user tried to login to a database and got an error saying that he did not exist. So he used another user ID and password and got in. His security was subsequently updated to make sure that he had the proper access to the cube in question, and got the same error again. What's quite amazing about this phenomenon is that it counts for what you would think is a blank spreadsheet. In other words, Book1 Sheet1 gets remembered by Smartview as if it were a template you have already used and connected with before.

So the little tip is to follow this instruction. Before you even talk to APS by bringing up the Data Source Manager, open up and save your spreadsheet to a new odd name you've never used before. Then open your data sources and connect to a cube. That will provide a cleaner slate. Try it.

### Clay Shirky On Tagging

Just had to have this particular one in my own domain.

[« Previous](https://web.archive.org/web/20160513031811/http://www.cubegeek.com/best_practices/) | [Next »](https://web.archive.org/web/20160513031811/http://www.cubegeek.com/best_practices/page/3/)