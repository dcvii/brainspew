---
title: "5 Steps to go from Data Engineer -> AI Engineer"
source: "https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?publication_id=1224799&post_id=189674475&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[By Daniel Beach]]"
published:
created: 2026-04-01
description:
tags:
  - "brain_spew"
---
Look, you don’t have to, but if you want to, here we go. Also, you should probably go find one of those elusive AI Engineers that are now showing up on LinkedIn full of wisdom and foresight. *Maybe they know what’s going on.* Either way, I’ve built a few multi—agent POCs, some on the Databricks platform and others more bespoke.

> I’ve poked and prodded enough “AI stuffy stuff” **to at least make myself dangerous**. Put me in, coach.

I’m just a dude on the internet who’s noticed the uptick in jobs involving “AI” or “Gen AI,” as the hipsters call it. And, heck, why not throw my hat in the ring? Everyone is already freaking out about losing their jobs to AI.

Today’s post is sponsored by **[Estuary](http://estuary.dev/?utm_source=podcast_dec&utm_medium=paid_audio&utm_campaign=signups_spring_2026)**.

Without them, content like this isn’t possible. The best way to support this Newsletter is to check out what **[Estuary](http://estuary.dev/?utm_source=podcast_dec&utm_medium=paid_audio&utm_campaign=signups_spring_2026)** has to offer and click the links below.

![](https://substackcdn.com/image/fetch/$s_!rU1J!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F00a76be4-9417-4a2e-a637-2ca539c08b8c_1384x280.png)

### Build millisecond-latency, scalable, future-proof data pipelines in minutes.

[Estuary is the Right-Time Data Platform that integrates all of the systems you use to produce, process, and consume data.](http://estuary.dev/?utm_source=podcast_dec&utm_medium=paid_audio&utm_campaign=signups_spring_2026) Also, providing best in class CDC (Change Data Capture).

[Estuary](http://estuary.dev/?utm_source=podcast_dec&utm_medium=paid_audio&utm_campaign=signups_spring_2026) unifies today’s batch and streaming paradigms so that your systems – current and future – are synchronized around the same datasets, updating in milliseconds.

### AI Hype

Even those filthy rich stinking [bankers](https://www.dailymail.co.uk/yourmoney/article-15662461/hsbc-ai-job-cuts-bank-layoffs.html) are cashing in on the hype of AI, putting thousands of jobs on the chopping block of AI.

Heck, even our [old friend Zuck seems to be getting swept up](https://www.reuters.com/business/world-at-work/meta-planning-sweeping-layoffs-ai-costs-mount-2026-03-14/) into the craze, like a lemming; they must all jump from the same cliff. Once one goes, you know the rest will follow soon. [Meta is reporting record profits](https://finance.yahoo.com/news/meta-rakes-record-revenue-profits-210711445.html?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAID9b4om-ybQX8WNQXMPybzdrvhkMiQlM6sK7_G9tqmAJGAJ0TrLH6QpR6WEJuoMhwu8-cEU3kVh5aFW7GpWxJTMVpvlm36guI7H2xvqg06vfaokZlSKv6GSMSq9PqhnPC8ufRoWh1yLPYHLVaxQ3_ztgZm0bCFcv1ePFLVOJK6D), but that ain’t stopping them, no sir Sunny Jim, once a hole in the ye ole’ dam has been poked, the waters start to flow quickly.

Well, where does that leave peons like us? Fighting for scraps in the post-apocalyptic future, most likely.

Either way, I prefer to find the bright spots if I can. They are out there if you know where to look. A little pragmatic attitude, half-glass-full sort of stuff goes a long way in overcoming obstacles of all sorts.

> *I guess if we can’t beat em’, we must join em’.*

I’m not talking about simply using AI as part of your software development workflow; **I’m talking about building AI and Agentic systems.** Pull back the curtains and see what Oz is up to.

I certainly have my ideas about what a Data Engineer must learn to become an AI Engineer, but instead of guessing, let’s head over to LinkedIn and run an informal search for the skills and tech companies that are asking for in “AI Engineer” job descriptions.

At the end of the day, if you want to be a Gen AI Engineer, then we have to have and learn the skills that are being hired for. Let’s do this like proper engineers.

> Old school. Heck, we might even write this code ourselves, \*gasp.

I scraped 30 AI Engineer job listings from LinkedIn into text files. What we can do is just do a simple Word Count, maybe with a Word Cloud, and actually see which skills are required for this job.

[All this code, including the text data for the jobs, is here on GitHub.](https://github.com/danielbeach/AIEngineerJobAnalysis) Enjoy.

Thanks for reading Data Engineering Central! This post is public so feel free to share it.

[Share](https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTg5Njc0NDc1LCJpYXQiOjE3NzUwNjI2NjAsImV4cCI6MTc3NzY1NDY2MCwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.CL2UuI5tagB_jn23PQae3xhllDWczfKr5kDzL4H9_Zo)

### The Code.

Here is a sample of one of the text files.

So, now let’s write some Rust to do the dirty work, find out what in the world all these AI Engineer jobs are all about.

Now, I found the results very surprising and funny, not what I was expecting. I mean, indeed, there were things in there like RAG and Agents, but I was assuming I would see words like … ***inference, langchain, langgraph, api, frontend, etc, etc.***

Indeed, it was the opposite.

In a good way, I’ve seen firsthand that building AI systems is more about systems design and architecture, with a few specific tools thrown into the mix.

And the word cloud …

I’m not sure what this says more about: the AI landscape as a whole, or companies’ take on what makes a good AI Engineer.

Again, as someone who has built my fair share of Agentic systems in Databricks and elsewhere, I pretty much agree with the requested skills list. It’s easy to pick up a framework, like LangChain; it’s not easy, without experience, to have Systems Design experience that assists with building multi-agent workflows … ***because that is what you are dealing with … multiple systems tied together.***

Let’s dive into our findings and summarize what is needed to move to an AI Engineer position.

## Top 5 Skills for AI Engineer

I want this to be practical from my experience over the last few years building AI systems, as well as what the actual data says, pun intended. Good intentions are just that, but seeing this word analysis of 30 job descriptions for AI Engineers helps solidify that we are going down the right path.

(*To be honest, it just sounds like a good data engineer, which, from my experience, is true, besides a sprinkle of odd toolsets*.

### 1\. Understand Systems Design (architecture)

When I first started playing around with Agentic and AI systems, building them, that is, I noticed something I was not expecting. Basically, I was building a bunch of separate “systems” that needed to talk to one another and work together.

We see this playing out in the fact that the most common word in AI Engineer job descriptions is “ **systems.**” Why? Because the business use case for LLMs and Agents in real life often requires data and integration across a suite of cloud resources, endpoints, and tools.

Each is a separate system that must work together to complete a task. If you are curious what this might look like, read my article, [Agentic AI for Dummies](https://dataengineeringcentral.substack.com/p/agentic-ai-for-dummies), or maybe my article [Building Agentic AI … Fancy](https://dataengineeringcentral.substack.com/p/building-agentic-ai-fancy).

Clearly, to make the leap to AI or Gen AI Engineer, you must be adept and comfortable with Systems Design, something that has been around for a long time.

Talking to databases, APIs, endpoints, tools, MCP servers, vectors, other agents, the list goes on. Add in the complexities of logs, traceability, monitoring, performance … across these complex workflows and apps that do all of the above … **those are classic system design problems.**

[Share](https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTg5Njc0NDc1LCJpYXQiOjE3NzUwNjI2NjAsImV4cCI6MTc3NzY1NDY2MCwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.CL2UuI5tagB_jn23PQae3xhllDWczfKr5kDzL4H9_Zo)

### 2\. Understand Multi-Modal Data (and generally data)

I had to laugh a little when I saw it, but this is also something I’ve commented about a number of times. Building LLM and AI systems is 90% data pipelines, sprinkled with a little orchestration. ***Data** shows up as the second most common word.*

Most\* AI and Agentic systems I’ve dealt with are very heavily reliant on data. Could be Lake House data in Delta Lake or Iceberg, Postgres tables, RAG-backed non-tabular data like PDFs, etc. Either way, these AI Agents typically require substantial context and interaction with data, vector- or otherwise, to be considered noteworthy.

We live in a data-driven world; it’s been this way for a long time, and the AI boom has only intensified. No surprise that building AI systems requires an expert-level understanding of data.

Here is where classic Data Engineering diverges from what is needed for AI systems. Yeah, we can hook up that tabular data in Postgres for the Lake House via numerous connectors, but a large portion of the data needed for integration into LLM systems isn't tabular.

For example, read the article below where I built a Databricks Knowledge Assistant on top of PDFs and Word Docs. This is not normal data engineering.

> *Most of use are not used to dealing with messy and unstructured data like this. You can’t just throw it all in a S3 bucket, I mean maybe you could, but long term and scalability wise, not a good idea.*

With the rise of Agentic workflows, we are no longer dealing with classical data models where tabular data rules. Well, yeah, we are, but we are also now dealing with audio, video, PDFs, … just a large swath of data we historically haven’t been integrating into our data platforms.

For example, this is an excerpt from an AI Engineering job description.

… or from another one …

At the end of the day, AI Engineers appear to be Systems architects, specializing in data and data movement across these systems.

If you’re curious about strangely shaped data, hard problems, and what the future might look like, [read this article from Byoyant Data.](https://www.buoyantdata.com/blog/2026-02-03-multimodal-delta-lake.html)

[Share](https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTg5Njc0NDc1LCJpYXQiOjE3NzUwNjI2NjAsImV4cCI6MTc3NzY1NDY2MCwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.CL2UuI5tagB_jn23PQae3xhllDWczfKr5kDzL4H9_Zo)

### 3\. The Cloud is King

This one I was kinda surprised at, not sure why, it sorta makes sense, but at the same time it seems like table stakes. Every once in awhile I run into a poor soul who hasn’t had the pleasure of being smashed upon the rocks of AWS and IAM.

Usually, it’s some corporate thing, where “the cloud” is kept under lock and key, and far away from the prying fingers of a thousand mildly bored devs.

> **I can feel that CTO’s axiety.**

To be honest, I’m not going to spend a lot of time here, other than to say that, yeah, anyone working on AI systems is probably going to be working at a “ *forward-thinking company* ” that relies heavily on cloud infrastructure for all operations.

My personal opinion is that “cloud” in this context has something to do with …

Here are some excerpts from the AI Engineering job descriptions …

It’s just them saying what we already know: if you’re going to be an AI Engineer, you’re going to be working in a lot of the public clouds (AWS, GCP, Azure), etc. As well, using many SaaS provided services, maybe for inference, that exist in someone else’s cloud.

It’s honestly just a good reminder that if you still don’t have much experience working with and deploying to major cloud providers like AWS, you should probably set up an account and start playing around.

### 4\. Workflows

Not going to lie, when I saw this word show up at the top of the list, I might have let a little squeal escape my lips. It felt like validation, a lifetime of Data Engineering that actually turns out to be useful.

Also, validation about what I’ve felt about building Agentic systems. Building these AI systems is an exercise in building pipelines and workflows.

For example, read this [article on some of the challenges of building multi-agent systems.](https://dataengineeringcentral.substack.com/p/deterministic-agentic-data-systems)

At the core, we are building workflows between data systems and agents. Agents use tools in workflows; user interaction happens through workflows; and the data and logic used are wrapped in workflows.

If someone has never built workflows, especially large data workflows, it would be difficult to be dropped into the title of AI Engineer, knowing that a large part of the job would be building workflows to support the AI systems and Agents.

> *The difference between good and bad agentic systems and their workflows is nuanced, and that knowledge comes from experience.*

The truth is, as well, with the rise of Agents, not only for code generation but also as entities taking actions and completing workflows themselves.

A person should be familiar with workflows if they are going to build Agents and AI tools to complete or participate in them. How do you monitor, observe, and measure the outputs or results of those black box agentic workflows?

This is a new sort of frontier with a lot of exploration; everyone and their mother is building Agents and letting them loose to “do things,” which usually means completing a set of tasks, also known as a workflow.

This raises all sorts of interesting questions, like [how do you build “deterministic” AI systems?](https://dataengineeringcentral.substack.com/p/deterministic-agentic-data-systems)

And so, we can all agree that “workflows” indeed make sense as one of the top skills required for an AI Engineer. Onwards and forward.

[Share](https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTg5Njc0NDc1LCJpYXQiOjE3NzUwNjI2NjAsImV4cCI6MTc3NzY1NDY2MCwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.CL2UuI5tagB_jn23PQae3xhllDWczfKr5kDzL4H9_Zo)

### 5\. Frameworks and Python

I sort of cheated and wrapped these last two skills into a single one, because they are basically the same thing. ***Python*** and ***Frameworks*** basically tied.

Sure, all the Rust hobbits will turn their noses up, but that’s nothing new. Python has been running the Machine Learning world long before LLMs were a thing, and will continue to do so for the foreseeable future.

> Why “frameworks” and “Python?”

Well, the AI world is still young, but you can already see solidification in which frameworks are most often used. I’m sure things will rise and fall in popularity, but if you want to be an AI Engineer, you need to be familiar with the people frameworks (mostly Python) used to build these AI systems.

Here are some excerpts from the job postings.

And the list goes on.

This is really no surprise at all. If you were a front-end engineer, they would ask you for the latest and hottest JavaScript framework, or whatever.

If you were a Rust engineer, they would expect you to be an expert with Cargo, or maybe Tokio for async operations. If you want to be an AI Engineer, then you need to use and be familiar with the tools and frameworks commonly used.

## So what are you waiting for?

Well, I found that interesting, even if you didn’t, you little complainer. With all the AI hype + doom and gloom, it’s easy to get caught up in the world-is-ending hype train. What can I say, I’m a sucker for it too.

> Either way, I guess we can all use the escape hatch of transitioning to “AI Engineer,” if all else fails.

Now that we have pulled the curtains back on that elusive job and seen what skills are required, it’s a little less scary. Maybe.

Methinks, probably because I’m biased, that Data Engineers are well-suited for these roles of AI Engineer. Working with data, workflows, frameworks, systems … this has been our life for a long time.

I do not know what the future holds for programmers and vibe coders. The layoffs are coming hard and fast. I happen to think it has a lot more to do with cost savings and convenience than AI. But it’s also true that software development has changed forever, like it or not.

Let me know what you’re worried about regarding AI.

POLL

### What's your greatest fear about AI?

Nothing. Bring it.

Loss my job.

Become irrelevant.

Can't keep up.

2 VOTES ·

Thanks for reading Data Engineering Central! This post is public so feel free to share it.

[Share](https://dataengineeringcentral.substack.com/p/5-steps-to-go-from-data-engineer?utm_source=substack&utm_medium=email&utm_content=share&action=share&token=eyJ1c2VyX2lkIjoxMjMwNTgyMiwicG9zdF9pZCI6MTg5Njc0NDc1LCJpYXQiOjE3NzUwNjI2NjAsImV4cCI6MTc3NzY1NDY2MCwiaXNzIjoicHViLTEyMjQ3OTkiLCJzdWIiOiJwb3N0LXJlYWN0aW9uIn0.CL2UuI5tagB_jn23PQae3xhllDWczfKr5kDzL4H9_Zo)