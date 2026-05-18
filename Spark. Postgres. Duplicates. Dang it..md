---
title: "Spark. Postgres. Duplicates. Dang it."
source: "https://dataengineeringcentral.substack.com/p/spark-postgres-duplicates-dang-it?publication_id=1224799&post_id=197358825&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Daniel Beach]]"
published: 2026-05-17
created: 2026-05-18
description: "a lesson in fundamentals"
tags:
  - "brain_spew"
  - "geopolitics"
  - "Iran"
---
![](https://substackcdn.com/image/fetch/$s_!NlDm!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F139b421b-d0ea-4744-ace4-6505f7a2c2e3_1414x786.png)

I recently came across the most classic Data Engineering problem of the last 50 years. **Duplicates records.** It was some “ *old code* ”, if you call 5-year-old Databricks Spark code old, which is like 15 years in Databricks years. To me, it was the perfect example of taking time, a lesson in the most basic fundamentals of data.

> *It’s not a particularly earth-shaking problem in and of itself, rather boring, but it’s a story that re-enforces the age old ideals.*

Since the [days of my data youth](https://www.confessionsofadataguy.com/2018/02/), heck, harkening back to my [LAMP stack](https://www.reddit.com/r/webdev/comments/18htpfi/anyone_else_miss_the_good_ole_lamp_days/) years in college, data duplication has been an issue that somehow manages to creep into database tables of all shapes and sizes.

History is doomed to repeat itself; programming and logic errors, conundrums, and slipups are par for the course. I mean, those little blighter **LLMS were literally trained on our collective sins**, so what makes you think things will get any better?

That’s what I thought.

---

```markup
Thanks to Delta for sponsoring this newsletter! I use Delta Lake daily, 
and I believe it represents the future of Data Engineering. Content like this 
would not be possible without their support. Check out their website below.
```

![](https://substackcdn.com/image/fetch/$s_!wmd9!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F708be49f-dfaa-498f-a862-8e9810a5fc58_600x123.webp)

---

## We start at the beginning.

What is your life really like if at some point during the past 365 days you get a message from someone “on the business side” that so-and-so is showing duplicate records? A tale as old as time, this.

- *First off, and before you throw a fit, hear me out: **What is a duplicate record?***

That is indeed NOT a stupid question. Didn’t your middle school teacher ever tell you that there is NO such thing as a stupid question? It’s true. **When it comes to data, you simply cannot assume anything**. Like anything … at all.

Sometimes duplicates are by design. It might have been a faulty assumption or a bad decision, *but by design in many cases*. One of the recurring fundamentals of data, when you encounter a new, or a new-to-you dataset, should be the question … “ *What is the grain of this dataset?*”

![](https://substackcdn.com/image/fetch/$s_!UvZk!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff2a24833-233d-4cf6-8459-8c1ac549eba4_1600x596.png)

Before running off to solve any duplicate data problem or looking for a bug that might not exist, one should start from the ground floor. It’s just good table manners, and good for you as a technical person.

> It’s hard to solve a problem, especially a data problem involving duplicates, unless you have solved the many times tricky problem of ***figuring out what makes each record in the dataset unique.*** It’s never the same for any two datasets, or rarely is.

Also, before we talk about the problem I encountered, I think we should break down another great way to approach duplicate data to ease the stress of solving issues that can be buried in a complex and large system.

We should separate any data system or duplicate data research into three big boxes. These boxes can help us narrow down the scope of the problem and where to best unleash the Claude hounds to find it.

1. Source
2. Transformation
3. Destination

![](https://substackcdn.com/image/fetch/$s_!xQrP!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbe010de4-d3a1-445a-af10-3f09b504aad3_1476x848.png)

- This may seem painfully obvious, but when we approach a problem like duplicate data in large, complex systems, finding the bug can be overwhelming. Being able to logically and technically differentiate where a problem is, or isn’t, will make our jobs and time to resolution much quicker and less stressful.

---

## Back to the problem at hand.

So, back to my boring storing of trying to solve an intermittent duplicate data issue within a few short hours, so I could get back to the AI salt mines.

Here’s what I knew.

1. *Duplicate data issue showing up inconsistently in a Web UI.*
	1. *Some days there are duplicates, some days are not.*
2. *Pipeline from source to finish included …*
	1. *Delta Lake House*
		2. *Databricks Spark transformation*
		3. *Python script to push said data to Postgres.*
		4. *Web App pulling data from Postgres.*

Now, logically, the data problem could be anywhere, although the intermittent nature of the duplicate data would probably preclude problems in the Web App.

Also, when working in large data systems, the best you can do is control the controllables rather than blame others. My plan was simply to eliminate the possibility of duplicates insofar as the data systems I CONTROL.

> *A good rule of thumb for data, and life … control the controlables, don’t worry about the rest until you have too.*

![](https://substackcdn.com/image/fetch/$s_!b2TT!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb0821467-8399-4c8a-8de0-1dfb346d476d_2028x642.png)

When I first heard the word “intermittent”, I had some suspicions in my mind. But, being the fundamentalist I am, I started with the Delta Lake Table.

![](https://substackcdn.com/image/fetch/$s_!UGMz!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F755cde9a-0fb4-407c-9d1b-08d0d90c2715_193x299.png)

The first thing I noticed is that this Lake House table didn’t leverage the [Primary Key definitions available in Databricks](https://www.databricks.com/blog/primary-key-and-foreign-key-constraints-are-ga-and-now-enable-faster-queries). This is both understandable and not, but in classic fashion, tech debt builds up and eventually bites your rear end.

![](https://substackcdn.com/image/fetch/$s_!SGkV!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3c475f5c-91e2-459a-97e7-93ddb35a9183_851x375.png)

If any storage systems offer you some form of primary key definition, you should take advantage of it. Also, at the very least, if it does not, you should simply create your own composite primary key and call it ***{something}\_primary\_key***, even if it is not enforced, for the simple reason of declaring and documenting the data grain in each dataset.

- *When you don’t do this very basic task, then someone like me or you will end up spending a lot of time deciding what the primary key should be on the dataset.*

(*This was mistake #1*)

### Moving along the data pipeline.

So, let’s say for the sake of argument, and in fact I did do this, confirm that indeed the source data was not the problem. The grain of data is identified and found satisfactory; nothing is 100%, but it's clearly unlikely that the problem was in the source data.

Harkening back to our 3-box diagram from the start, it’s time to move on down the pipeline. Transformation, data munging, whatever is happening to that data in Spark.

![](https://substackcdn.com/image/fetch/$s_!bYxf!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb1e6d40a-7ff0-4434-80be-49d45d37b6a3_273x311.png)

To keep this as short as possible, I will fly by this part as well. More or less, in this case, there was very little data transformation. No JOINS that would explode things, etc.

> But, that being said, the ole’ saying “ [Write, Audit, Publish](https://dataengineeringcentral.substack.com/p/introduction-to-write-audit-publish),” exists for a reason.

(*This was mistake #2*). Not having an audit trail of the data before and after every step (most large steps) makes it hard to debug.

---

### End of the line.

At this point, I still had not found the root cause of the problem, and I wasn’t sure it really mattered. Especially once I started checking the Postgres database that was accepting the dataset that was feeding the UI.

- I ran into this beauty involving PySpark, PyArrow, and psycopg. (*This ends up being the probable cause*)

![](https://substackcdn.com/image/fetch/$s_!iVWm!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8f10503a-85e5-4b0e-89ab-6f71f3f21648_2000x1378.png)

This caused me to look at the Postgres table. Why? There is no reason under the sun for a Postgres table to have a duplicate row if you put in a minimal amount of effort into the data model.

I put the following fix in right away.

![](https://substackcdn.com/image/fetch/$s_!kpsl!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff375cd5b-6576-4cba-90a1-2d3201c81984_1040x260.png)

![](https://substackcdn.com/image/fetch/$s_!MHOG!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9cc2f72d-79f4-4946-8ed4-f4e3bb673848_1128x56.png)

I mean, simple solutions are the best, aren’t they?

- *If I know the primary key, it should be enforced.*
- *If, by some data Gremlin, a duplicate data point makes it this far, on INSERT, ignore it.*

Sure, some would argue that you could drive harder towards the real issue, which, based on the intermittent issue and the absence of duplicates elsewhere, seems to be that Spark partitions are being recomputed and reinserted into the Postgres table at random times.

> The solution to that problem would require much more code changes then the 2-liner.

---

### The moral of the story.

When the chickens come home to roost, there is no avoiding it. If we, as data folk, sorta whistle and kick rocks through our projects, ignoring the boring fundamentals, there is a high chance that someone, somewhere, at some point, is going to have to deal with it.

Trying to find the perfect data set, data platform, or set of data pipelines is impossible. Doesn’t exist. We live in a day-to-day system that piles up tech debt. PR’s slip past us; we don’t notice the little things.

We forget to think about the grain of data, we forget that a table should never exist without a primary key, because “we are so confident” at some point in the past. **We forget that the chicks always come home to roost.**

I know this was not a particulary earth shattering or interesting discussion on the finer points of data problems. But at the same time, it is the perfect lesson that needs to be taught and that we all need to re-learn at various points.

- *Nothing and no one is the exception.*
- *Know Thy Data*
- *Enforce what can be enforced with every tool at your disposal.*
- *Don’t seek perfection; seek out reasonable solutions.*
- *Always compartmentalize your problems and architecture into boxes.*

Anywho, happy coding, my friends.