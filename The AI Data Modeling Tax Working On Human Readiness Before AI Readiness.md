---
title: "The AI Data Modeling Tax: Working On Human Readiness Before AI Readiness"
source: "https://moderndata101.substack.com/p/the-ai-data-modeling-tax?publication_id=1170209&post_id=187759551&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alejandro Aboy]]"
published: 2026-04-08
created: 2026-04-11
description: "The opportunity cost behind adding AI on top of your Data."
tags:
  - "brain_spew"
---
#### About Our Contributing Expert

## Alejandro Aboy | Senior Data & AI Engineer, Writer

![](https://substackcdn.com/image/fetch/$s_!CCpR!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbaf2ba75-effb-49d2-b5a6-23235a2e7010_1600x900.png)

[Alejandro](https://www.linkedin.com/in/alejandro-aboy/) is a Senior Data & AI Engineer and the voice behind *[The Pipe & The Line](https://thepipeandtheline.substack.com/)*, a technical newsletter where pipelines meet product thinking. With a career that began in marketing and web analytics, he transitioned into modern data engineering, bringing with him a sharp instinct for business context, experimentation, and stakeholder alignment.

At Workpath, Alejandro serves as the main owner of the Data Platform & AI stack. He builds AI agents with RAG architectures (Pgvector on Aurora), designs MCP-based tool ecosystems, and implements production-grade AI observability. His work spans dbt modelling, orchestration with Airflow, Slack-to-Tableau automation, and secure backend design for agentic systems.

Alejandro is deeply engaged in the open data community. He has collaborated with OpenMetadata on agentic data modelling and metadata-first architectures, co-authoring end-to-end implementations that connect lineage, governance, and AI tooling through MCP. His writing is frequently featured by Modern Data 101 and other leading data publications. We’re thrilled to feature his unique insights on [Modern Data 101](https://moderndata101.substack.com/)!

> *We actively collaborate with data experts to bring the best resources to a [20,000+ strong community](https://www.moderndata101.com/) of data leaders and practitioners. If you have something to share, reach out!  
> 🫴🏻 Share your ideas and work: [community@moderndata101.com](http://community@moderndata101.com/)*

###### \*Note: Opinions expressed in contributions are not our own and are only curated by us for broader access and discussion. All submissions are vetted for quality & relevance. We keep it information-first and do not support any promotions, paid or otherwise.

---

## Let’s Dive In

![The hidden tax of the agentic data stuck: thumbnail image for Modern Data 101 article in collaboration with Alejandro Aboy](https://substackcdn.com/image/fetch/$s_!ijY7!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdc430f83-466f-46bb-a2d9-adc17e31ed99_2198x1216.png)

In July 2025, I wrote a guest post framing data professionals as orchestrators of the agentic data stack, with all the new possibilities that implied.

It’s been a while in terms of AI technology progress, but we still hear that AI will replace data engineers, automate modeling, and democratize analytics. But I see we ended up in a different place: a lot of new shiny productivity tools that create a silent workload around them.

6 months ago, my stack was dbt with some Cursor rules. Now I have 7 skills & 5 hooks with Claude Code, Postgres, Miro, and Atlassian MCPs, and I still put the same level of attention.

And that scenario exposed how messed up we are on so many levels, but since AI can’t assume accurately, now the symptoms look worse than before.

> #### Before AI readiness, human readiness. That’s it. That’s the whole thing.

![The image shows how a scenario exposed how messed up we are on so many levels, but since AI can’t assume accurately, now the symptoms look worse than before. | Modern Data 101](https://substackcdn.com/image/fetch/$s_!kCbl!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F59801aa6-1ce0-4ddd-880f-ae54ee676f47_2192x1216.png)

The changing direction of attention | Adapted from concepts shared by the Author, curated by Modern Data 101

---

## TL;DR

- **AI didn’t automate work. It redistributed it.** You’re not coding less. You’re maintaining AI toolchains and validating output.
- **The five false promises that led us here**: context windows replace schemas, denormalization fixes everything, agents infer structure at runtime, MCP learns your business, and skipping modeling fundamentals.
- **Your data stack now serves two customers with incompatible needs.** Humans muddle through ambiguity. AI hallucinates through it. That gap is the tax.
- **The silver lining**: Making data “AI-ready” accidentally made it better for humans, too. The BIG question is how far companies are from understanding their own context, regardless of AI.
- **Tools will catch up. Human readiness won’t.** The teams that win aren’t the ones with the best tools — they’re the ones that were ready before the tools arrived.

---

## The Five False Promises

### 1\. “Context Windows Are the New Schema.”

“200K tokens means AI can just read everything!”

Your 47-table schema without table/column descriptions will just make non-determinism burn all your tokens or give awful answers with 5 JOINs in the best-case scenario.

> **This one is still a problem and I like to keep it that way since the solutions around it make more sense.**

### 2\. “One Big Table for AI.”

**“Denormalize everything! AI loves simple!”**

I tried that, it’s better. But denormalization without semantic clarity is the same mess, just centralized.

> **The same way a human will find this overwhelming, there won’t be any difference with AI.**

### 3\. “Just-In-Time Modeling.”

**“AI agents will infer structure at runtime!”**

You can’t “vibe” your way through data modeling without a discovery workflow or useful query patterns that could serve as a few-shot examples for business use cases.

> **Tools like cube.dev MCP or dbt semantic layer skills make runtime schema discovery more reasonable, but only when the foundations are documented first.**

### 4\. “AI Will Learn Your Business.”

**“MCP + metadata catalogs = autonomous design!”**

This one is a false promise, but not because of AI, but because of how companies operate.

I connected Claude to OpenMetadata via MCP. It was really good. But data lifecycles and business logic are evolving rapidly without robust workflows, which will make this approach stale since it’s not maintained.

> **Someone has to put metadata in place, define domains, connect assets through lineage and make sure their owners are well labeled. Data governance is useless for AI if you rely on AI figuring out the blanks.**

#### 5\. “No Need to Learn Data Modeling.”

**“Just describe what you want in English!”**

Text2SQL has improved. With MCPs, semantic layers, and metadata catalogs on top, you get decent results.

But not being able to spot shuffling queries, unnecessary partitions, or table JOINs that are already covered in other models will just make modeling with AI the greatest data garbage-in-garbage-out ever.

> **Get familiar with schemas, don’t rush to physical implementation if conceptual doesn’t feel right. Use AI to think through it, you can just talk to it because now it can draw stuff on boards!**

---

## The AI Data Modeling Tax

Your data stack now serves two customers with incompatible needs.

- Humans tolerate ambiguous naming, navigate tribal knowledge, work around incomplete docs, ask questions when confused.
- AI requires explicit naming, has zero tribal knowledge, treats documentation as a contract, and never asks questions. It just hallucinates.

![The image shows a comparison between how a human data consumer is served vs how a machine data consumer is served. | Modern Data 101](https://substackcdn.com/image/fetch/$s_!w1oF!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbe41011e-fc21-467a-ab39-929e6e76a4ec_2217x1216.png)

The AI Data Modeling Tax | Adapted from concepts shared by the Author, curated by Modern Data 101

> 🔖 **Related Reads**

While AI can handle complexity, it can’t handle **our** complexity.

Think of the **shortcuts**: The *customer\_id* that means three different things depending on which Slack thread you read from in 2023. That’s the worst type of debt: silent. But we got used to it.

Then we got AI, so as long as you define things correctly, it will follow them properly (most of the time). All the good things we started adding to improve our data modeling setups made them powerful and a huge debt accumulator.

- **Before AI:** A new column on a backend table meant adding a new table on a dbt model, then tracking which dashboard was using it and updating charts.
- **After AI:** Add metadata catalog, semantic layer, AI context docs, MCP configs, validation rules, example queries. Skip any step and AI won’t be as good.

![The image shows how the attention of engineering teams is redirected towards new efficiencies like how after AI we need to Add metadata catalog, semantic layer, AI context docs, MCP configs, validation rules, example queries. Skip any step and AI won’t be as good. | Modern Data 101](https://substackcdn.com/image/fetch/$s_!VpEk!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F61a12b99-afb4-4eae-8f91-c5863e2b3b9b_2212x1216.png)

The reality of the AI Stack | Adapted from concepts shared by the Author, curated by Modern Data 101

**“But you can tell AI to auto-maintain everything around it.”**

True, but every new change brings new constraints, and with the industry's current pace, it’s becoming hard even to tell it to consider X or Y next time.

> **We added new cool stuff to automate lots of work, and now we need to automate tools to maintain the tools that automate things for us.**

![The image shows how the commencement and penetration of AI in engineering spaces and teams have redistributed the workloads instead of automating it. | Modern Data 101](https://substackcdn.com/image/fetch/$s_!0Sd4!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcc1f5126-ce21-4057-99d4-ce68588a1352_2176x1216.png)

How expectations from data engineers have changed | Adapted from concepts shared by the Author, curated by Modern Data 101

---

## The Silver Lining

Preparing data, no matter if it’s for data analytics workflows, internal BI, or AI, accidentally makes it better for humans, too.

![The image shows a venn diagram and the intersection between requirements for AI readiness and the cures for human-generated technical debt and how both requirements intersect to create a state of "human readiness" for AI problems and environments | Modern Data 101](https://substackcdn.com/image/fetch/$s_!azpQ!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdd967815-855e-4ce9-b1ba-02e5b91d3abb_2619x1216.png)

Achieving “human-readiness” | Adapted from concepts shared by the Author, curated by Modern Data 101

Unambiguous naming, explicit documentation, semantic layers, clear relationships: all the stuff we should have been doing but didn’t, because humans could muddle through.

But it goes deeper. As I wrote in *[How AI Can Improve Your Data Modeling (And What’s Still Missing](https://thepipeandtheline.substack.com/p/how-ai-can-improve-your-data-modeling)*), the BIG question is how far companies are from understanding their own context, regardless of AI.

Decision rationale lives in Miro boards, Slack threads, and people’s heads. When you treat your schema as a product with a hybrid consumer on the other side (human and AI), you start capturing the “why” by default.

![The image shows how AI exposes the technical debt and data debt that data teams and operational teams have been able to ignore for a long time but can no longer do so due to specific requirements from AI or machine consumers of data that need the foundations to be stronger and devoid of tech debt | Modern Data 101](https://substackcdn.com/image/fetch/$s_!7WPt!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F96711cca-51a7-486b-92a3-8fda8014222c_2220x1216.png)

What lies underneath the “simplicity” of AI | Adapted from concepts shared by the Author, curated by Modern Data 101

It’s amazing how many tools were added to the stack, how we are more productive in so many ways. We are still lifting up the carpet and finding issues that should have been solved before this.

> AI exposed, in most cases, that we never had a structure at all. We were “vibing” before vibe coding.
> 
> But I am happy that one way or another, AI opened a lot of challenges that we wouldn’t have tackled at all if it wasn’t for AI readiness needs.

---

## Final Note

In July 2025, we wrote about data professionals becoming orchestrators of the agentic stack. Eight months later, the prophecy landed, but just not where we expected.

Tools will catch up. Context windows will grow. MCPs will improve. When that happens, the teams that invested in human readiness will be ready. The ones that didn’t will pay the tax if they want to play the AI game.

> **The real orchestration about managing AI agents relies on managing the readiness that makes agents useful.**

---

### MD101 Support ☎️

If you have any queries about the piece, feel free to connect with the author(s). Or connect with the MD101 team directly at **community@moderndata101.com** 🧡

### Author Connect

![](https://substackcdn.com/image/fetch/$s_!MG30!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1ece4a12-eea3-4fae-b2c0-c9cf9ff3cb98_1600x900.png)

Connect with [Alejandro Aboy on LinkedIn](https://www.linkedin.com/in/alejandro-aboy/) 💬 | Or find more of his work on Substack:

 [![](https://substackcdn.com/image/fetch/$s_!vmrQ!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4d5b2131-da28-4621-ad6f-9574cbc41a1e_500x500.png) The Pipe & The Line](https://thepipeandtheline.substack.com/?utm_source=substack&utm_campaign=publication_embed&utm_medium=web)

[Hands-on guides, tools, and experiments to sharpen your Data & AI Engineering skills from someone who learned it all in the wild.](https://thepipeandtheline.substack.com/?utm_source=substack&utm_campaign=publication_embed&utm_medium=web)

---

*From MD101* *team* 🧡

### 🌎 Global Modern Data Report 2026

The **[Modern Data Report 2026](https://www.moderndata101.com/modern-data-report-2026)** is a first-principles examination of why AI adoptions are getting blocked inside otherwise data-rich enterprises. Grounded in direct signals from practitioners and leaders, it exposes the structural gaps between data availability and decision activation.

![](https://substackcdn.com/image/fetch/$s_!vF-0!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F75fae11e-d9ff-4ed9-a09e-4d460ff0f9db_2970x2238.avif)

With hundreds of datapoints from **[540+ data leaders and experts from across 64 countries](https://www.moderndata101.com/modern-data-report-2026)**, this report reframes AI readiness away from models and tooling, and toward the conditions required and/or desired for reliable action. Already [downloaded 1000+ times](https://www.moderndata101.com/modern-data-report-2026), this report is enabling key insights for several industry practitioners this year. Join the discussions!