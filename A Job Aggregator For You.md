---
title: "A Job Aggregator For You"
source: "https://tessellations.substack.com/p/a-job-aggregator-for-you"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2026-03-24
created: 2026-03-24
description: "Making looking for a job less painful and more efficient."
tags:
  - "brain_spew"
---
### Making looking for a job less painful and more efficient.

I have to mention **LinkedIn** because that’s the lovely place where I click on a job and discover that there are 400 other applicants, 41% of which have masters degrees. What a shame. Well, if you’re like me and you’re sick of complaining about the way the employment market has been taken over by bots and other impersonal mechanism, I cannot tell you how to feel about it. But I can show you what I’ve done about it. I may soon open source it or put it in a low-cost container.

**The Use Case**  
I’m a backend data guy. What that means is I could practically do just about any database backend type job that doesn’t require moving > 5TB per month. I could do just about any analytical type job that doesn’t require me to do realtime fast Fourier analysis. So I’m looking at the following keywords {“analytics”, data analyst”, “business intelligence”, “data engineer”, “DBA”, “data warehouse”}. I could be broader because I’ve done practice management, enterprise technical pre-sales and product marketing, but I know algorithms are not holistic. Maybe HR is not either. I miss actual management, you know, by people.

**The Solution  
**I have an application that allows me to subscribe to as many job listing spammers as I please. The app scans and ingests all of my email, deduplicates it and puts it into a database that gives me a screen like this:  

![](https://substackcdn.com/image/fetch/$s_!NWms!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7473e7a7-4951-4c19-9770-17df191cd77c_1887x916.jpeg)

In other words, it’s my personal aggregator of Robert Half, Indeed, Monster, Dice, LinkedIn, Jobot and Glassdoor. I can look at a lot of information, especially when they put the entire job description in. I can then glance at each job listing rate and rank them and easily filter on jobs that I tag as I please. Here’s my tag management screen:

![](https://substackcdn.com/image/fetch/$s_!ny0D!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fae5eb0dc-492f-473a-88bf-d237f907cb2b_1898x984.jpeg)

As my wife says, these look a lot better in person. But I like Solarized Light and this works well for me.

**What’s Next**  
Obviously I’ll be fine tuning it for a while, but already I’m improving my productivity 5x at least. It takes me about a minute to review a listing and mark it and I don’t miss opportunities. I also don’t get very frustrated when a job is not for me. This tool helps me focus.

The next thing is to tie this to something I already built, which is my **block & tackle agent** which runs through my entire career, including side gigs and a number of full and half-competencies which it evaluates on a case by case basis for each job description I feed it. It poops out the following hardball answers and gives me reasons why:

```markup
Step 5 - Synthesis and Recommendation
Provide one of:
A) We are GO
B) We are HOLD
C) We are LOW BALL
D) We are NO GO
Pick one. Support it with explicit references to Steps 1–4. No hedging.
```

I find that I skew this pessimistically, but I also have a ‘thirsty’ prompt for when I’m feeling desperate. Whether on GO or HOLD the agent generates a custom resume and cover letter, which I always have to review for accuracy and exaggerations.

**The Colophon Magic  
**Behind the scenes is the `msgvault` MCP service, which I have running day and night (via Temporal) to keep my several GMail accounts synced down to my Mac. So it can handle basically any number of emails I get and ingest them idempotently to my local Postgres server. I could probably use SQLite just as well, but I didn’t, and there’s no reason to use DuckDB with such small numbers. But I will be adding vector affinities in the near future, so Postgres.

The whole thing is Go based and it works with Oz (local) or Claude (not fully tested). I have started breaking out my agentic best practices, so this is one of the first apps where I took what I learned a couple weeks ago on **Figma** and applied it to the new **Google Stitch** which outputs Tailwind and HTMX, whatever that is. (Hat tip to Joe)

---

Overall I’m pretty happy with this. I’ve spent a bit on tokens and upgraded my Claude subscription, but I’m glad to know the difference between agentic cheap and blowing a token budget. Seeing as I have paid \[stupid\] LinkedIn for whatever that premium crap is, I love sicking my bot against theirs.

Stay tuned.