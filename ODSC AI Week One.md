---
title: "ODSC AI Week One"
source: "https://tessellations.substack.com/p/odsc-ai-week-one?publication_id=1655845&post_id=185475266&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2026-01-22
created: 2026-01-22
description: "Whirlwind of practical knowledge."
tags:
  - "clippings"
---
### Whirlwind of practical knowledge.

One of my problems is that I’m one of those guys who generally gets the gist of something very quickly, then I put it into a bucket on the shelf and may never get back to it. On the good side, I get to the bottom line and solve a lot of problems on the job and then circle back if it’s not on the critical path. On the down side when it’s not on the critical path I probably won’t get back to it. That’s why I need to be solving interesting problems.

The good side of that is that I’m a packrat. I literally have code from 1978 that I just found. My first paying job as a FORTRAN programmer. Anyway, all that is to say that now I have some very practical models and a growing understanding of agentic theory and practice. That owes to my participation this week in the ODSC-AI online conference where I’ve done nine sessions.

- Agentic Overview
- Agentic w/ Claude
- RAG to Agent
- Cognee
- Agent Loops
- Scaling RAG with Ray
- Agentic Governance
- Agent Memory Systems
- AG2 Patterns

**No Query Plan**  
Each of these was useful to my understanding, but the one that really got me behind the curtains was run this morning by a cat named **Emre Okcular**. He got down into the computer science of it, which is figuring out how to run these damnable things efficiently. So he really killed it explaining Context Engineering, concepts and techniques. Essentially what LLMs don’t have is the equivalent of query planners that keep database systems honest. So basically nobody knows what it’s going to cost until it has run, and what’s crazy is when I mentioned ‘token budgets’ to the Claude person, they didn’t really know what I meant. Okcular definitely did.

My AI weakness is that I’ve been abusing my strength which is the everyday use of **Warp** as a super terminal. So rather than chunking prompts and contexts down an API’s piehole, I just point the interactive conversation to my context folder to run (generally) a single large prompt, even when it is iterative. But I expect now that I could go code-first and use my API keys in code, I can return some performance, and realtime feedback from my prompts in progress.

As I already break things down into steps and have conditionals inside my prompts, a code-first orientation (via Temporal) can give me more control over the execution. So then I can look closer and examine things like the following:

![](https://substackcdn.com/image/fetch/$s_!JtTv!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb397312b-ad1c-49a9-9d33-3de2d52614b3_939x410.png)

There are specific programming patterns that will fix these things that make AI use inefficient and inaccurate. And guess what, these experts are confident that hallucinations are a thing of the past. Here’s the analogy I’ve gotten from beyond the industry speak of AI.

![Charles V, Holy Roman Emperor quote: I speak Spanish to God, Italian to women, French to...](https://substackcdn.com/image/fetch/$s_!nkVI!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F42255f31-37ce-4c1b-84ef-e9256daaf666_850x400.jpeg)

Charles V, Holy Roman Emperor quote: I speak Spanish to God, Italian to women, French to...

German, being the language that demands compliant obedience from dogs and horses, you have to ‘Germanize’ your prompts.

---

**Watch out Deloitte**
I had a great conversation last evening with Sam in Long Beach. Sam is an ontologist looking to move up the ladder from AWS. It was astonishing that I found someone who understands the possibilities of SHACL, me having just discovered it. But there is nothing quite so exciting to me as the ability to categorize expert systems with SHACL ontologies and state machines. That plus the evolution of Iceberg and Arrow is going to make a helluva quick and responsive data tier to embed into agentic workflows. I think I’m really starting to get this stuff, and I just embraced the slop a few months ago.

Now you combine that with what structured prompting can do to generate tactics and strategies and I see possibilities for the rapid evolution of specific methodologies and management philosophies tailored to a company’s actual capacities. So basically you can get an executive committee to have a meta-prompter and then senior management become the only humans in the loop of overseeing structural change in their businesses. Suddenly every major company with a significant token budget doesn’t need management consultants any longer.

Except for super SMEs in specialty fields like Oil & Gas or Aviation, a lot of smaller agile consulting companies are going to be able to execute corporate change management without the assistance of large consulting companies. And the feedback loops will be computer quick. This is huge. You heard it here first, maybe.

---

I just found out my old boss is starting up a new company. Things are popping off all over.