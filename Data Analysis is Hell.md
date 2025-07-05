---
title: Data Analysis is Hell
source: https://dataengineeringcentral.substack.com/p/data-analysis-is-hell?utm_source=post-email-title&publication_id=1224799&post_id=157927136&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email
author:
  - "[[T50/Daniel Beach]]"
published: 2025-02-27
created: 2025-02-27
description: ... nothing you can do about it.
tags:
  - clippings
---
![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5dfe229e-4175-48ba-a9b4-47855bdb7709_1024x1024.webp)

I’ve been in and around data analysis of one kind of another, in a professional capacity since about 2014. This one thing as stayed true and steady. From giant corporations to tiny startups, and everything in between.

*Data Analysis is Hell.*

**Let me explain.**

Working in and around tech, starting in the Data Warehouse space and what we used to call “Business Intelligence” before Data Engineering was thing, I accumulated my fair share of battle scars. Most all those scars could be attributed to Data Analysis in some form or other.

Sure, it can be hard to see the dividing line between Analytics and Data Engineering these days, but there is a difference. To this day it appears to me that Analytics eats up and spits people out on a regular basis, like clock work.

Thanks for reading Data Engineering Central! This post is public so feel free to share it.

[Share](https://dataengineeringcentral.substack.com/p/data-analysis-is-hell?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTU3OTI3MTM2LCJpYXQiOjE3NDA3MDEwNjksImV4cCI6MTc0MzI5MzA2OSwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.giAeHwA9F2z1NHdjcMzfhhr00AXaVEhlrhIViL150TA)

I have my theories as to why. They are numerous and varied, but I think we can find veins of truth, like gold, buried in there, and it might be possible to mine out some precious truths and solutions to whey **Data Analysis is Hell**.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F096be83b-364d-41d8-a878-d525ad92c1db_1690x832.png)

I’m going to just start listing things, because who doesn’t love lists. Then at the end, if I’m feeling spicy, I will give you my two cents on how to address said problems.

I should also state an assumption before I start, I see “Analytics” as a broad stroke, but generally assume the following tasks and people usually fall into this bucket.

- *Data Analysts, Data Scientist, and any sort of Report or Dashboard development.*
- *Target audience is usually end users or the business.*
- *End result of make Data Warehouse or Lake House platforms.*

Anyways, onto the main topic for today.

- Most\* data quality is simply poor
- Poor data modeling
- “The Business” doesn’t communicate needs or requirements well
- Every business has “special needs” that increase complexity
- Analytics tasks are ALWAYS under scoped in terms of time and complexity
- Analytics systems are typically less best (*developer*) practice driven
- Operating close the business comes with a certain amount of chaos
- One-off and priority requests out of nowhere are normal operating procedure.
- It’s hard to get bunches of people to agree on \*anything

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa9174647-3fec-4681-84e3-c424d540d48c_1580x860.png)

> *I could go on but I should probably stop here. If you’re an astute reader I’m assuming you can find some veins of continuity buried in there.*

Nothing earth shattering just real life down in the data trenches. I count myself blessed that I managed to un-entangle myself from \***most** analytics, besides for the odd task that comes up in which I pat myself on the back and say … “*There, there, it’s ok. It’s just an hour two, you can do it.*”

From my perspective some of these issues can be lessened, some alleviated, but most of them are simply par for the course. Sometimes things are what they are and you must accept a certain level of chaos.

Thanks for reading Data Engineering Central! This post is public so feel free to share it.

[Share](https://dataengineeringcentral.substack.com/p/data-analysis-is-hell?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTU3OTI3MTM2LCJpYXQiOjE3NDA3MDEwNjksImV4cCI6MTc0MzI5MzA2OSwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.giAeHwA9F2z1NHdjcMzfhhr00AXaVEhlrhIViL150TA)

Let’s see if we can come up with a few approaches that might be able to make the life of those moving in the Analytics world a little less burdensome and less chaotic.

I think this is the key to most things in life, including Analytics, we should try to reduce any sort of chaos that is inserting itself in the process. Reduce chaos.

- **Most\* data quality is simply poor**

- This is probably the most easily addressed problem that plagues many Data Platforms and causing nightmares for downstream consumers including Analytics.

- *Look into tools like Soda, Great Expectations, etc.*
- **Poor data modeling**

- Lack of forethought and insight into how the data will be consumed downstream. This is very simple to fix in theory. If you are will to simply spend the time doing some redesign and refactor
- **“*****The Business*****” doesn’t communicate needs or requirements well**

- This has and always will be the case. You can learn to do a few things better to help alleviate and deal with this issue, not solve it.

- *Have more requirements meetings*
- *Have regular progress checkins and reviews*
- *Work on cross team communication*
- **Every business has “*****special needs*****” that increase complexity**

- This is part of life and Analytics. The best you can do is simply increase your estimates to account for this complexity.

- *Don’t pretend like stuff is easy when it’s not. Don’t say it will take a day when it will take three.*
- **Analytics tasks are ALWAYS under scoped in terms of time and complexity**

- Related closed to above, this can be easy fixed. Stop saying “*Oh, no problem, that’s easy, I know how to do that.*” You know there will be “things” that come up.

- *If the task involves analytics, add a few days to deal with the people and complexity issues.*
- **Analytics systems are typically less best (*****developer*****) practice driven**

- This is 90% the case most of the time. Many folk working in and around Analytics simply don’t come from a classic Software Engineering background.

- This leads to not following well-known best practices. Testing, good development life cycles, clean code, etc.

- *It’s easy enough to teach these things, simply take the time to do it.*
- **Operating close the business comes with a certain amount of chaos**

- You can’t escape this you can only mitigate it by planning ahead and being firm.

- *Have more meetings, request clarity, request documentation or tickets for work. Learn emotional intelligence, learn to be kind but firm.*
- **One-off and priority requests out of nowhere are normal operating procedure**

- This will always be the case when interfacing with the business and working with analytics.

- Again, be firm by kind, request they follow due process, request tickets, bring up these problems in team meetings.

- *If you teach the business that you won’t drop everything at all times without some sort of process, the chaos will never end.*
- **It’s hard to get bunches of people to agree on \*anything**

- This is really just about learning to bring people together, make hard decisions, make tradeoffs, communicate well, and meeting in the middle.

- *This are soft skills that can be learned and taught.*

Thanks for reading Data Engineering Central! This post is public so feel free to share it.

[Share](https://dataengineeringcentral.substack.com/p/data-analysis-is-hell?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTU3OTI3MTM2LCJpYXQiOjE3NDA3MDEwNjksImV4cCI6MTc0MzI5MzA2OSwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.giAeHwA9F2z1NHdjcMzfhhr00AXaVEhlrhIViL150TA)

> There you have it, the solutions to all your analytics problems … well, not really, but maybe a little.

Control the controlables, and there are plenty of them that you can get your hands around that will at least bring a semblance of balance to the constant chaos you might be experiencing.

To boil it down.

- *Enforce Software Engineering best practices in the Analytics context.*
- *Increasing communication and expectations around processes.*
- *Be realistic when planning and estimating projects.*
- *Have people formally learn to up-skill themselves in the area of “soft skills” like communication etc.*

From the technical side you can reduce a lot of analytics problems by implementing Data Quality tools, bringing DevOps, CI/CD, Testing, and other such things into the Analytics process. This will disappear a whole host of issues.

From the human side you simple need to inject a little rigor into the process, the business will balk, like they always due, but if you get %50 of your wants in place, you will all be the happier.

Be firm but kind about one-off and chaotic requests, increase the amount of inter-team communication (*via Slack, face-to-face meetings, etc*).