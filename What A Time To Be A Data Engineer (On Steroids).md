---
title: "What A Time To Be A Data Engineer (On Steroids)"
source: "https://thepipeandtheline.substack.com/p/what-a-time-to-be-a-data-engineer?publication_id=1196229&post_id=188642133&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alejandro Aboy]]"
published: 2026-02-21
created: 2026-02-21
description: "Some reflections on how Data Engineers can become key actors in the AI era."
tags:
  - "clippings"
---
### Some reflections on how Data Engineers can become key actors in the AI era.

> Hi there! Alejandro here 😊
> 
> Subscribe if you like to read about technical data & AI learnings, deep dives!
> 
> Enjoy the reading and let me know in the comments what you think about it 👨🏻💻

## 📝 TL;DR

The article is too short for a TL;DR 🤣

---

There’s a narrative going around that Data Engineers are becoming AI Engineers.

Like a promotion, upgrade or the idea of leaving something behind.

That’s not what’s happening in my opinion.

I’ve been trapped in one of the greatest loops in my career.

I build pipelines, data models, data products and automations as a core, but AI started calling for duty and RAG, semantics, Observability and MCP/Agent toolings became part of the mix.

But nothing of the data engineering scope is gone.

![](https://substackcdn.com/image/fetch/$s_!GqB0!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7a106baa-7884-45ba-a634-7353d5a889c3_1024x1536.png)

Image generated with ChatGPT.

*p.s. I am addicted to combining Claude Skills and ChatGPT to generate these images, it’s so cool.*

---

## Nothing Changes And Everything Looks Different

You build data pipelines to feed AI, you realise it needs better chunks, document cleanup, retrieval performance (you name It) and go back to improve the pipelines. All of that to go back to the AI Agents or tools to go back to the pipelines again.

> *The greatest part: it’s pretty likely that now the pipeline you’re building isn’t for a dashboard but for an agent, a RAG system, an observability annotation round.*

I wrote about this in MetadataOps guest post on Data Gibberish: the consumer of your data changed from analysts to LLMs, and “quality” now means semantic context, not just correct types.

But I want to go further.

> *The best career path to make AI work properly is through data engineering. Is the boring but neccesary skillset that builds the ground everything else stands on.*

---

## How “A Day In Data Engineering” feat. AI

Here’s what my last few months have looked like:

1. I built scripts to sync Metabase lineage to our dbt exposures because we needed end-to-end for Claude Code and for an Analytics Agent to be able to create flexible queries based on context and not static table descriptions. **A data engineering problem that only exists because AI needs to understand the same definitions.**
2. I wrote REST API integrations against observability tools to pull and sanitize model inputs and outputs. Why? Because we needed clean, structured data for annotation rounds on AI projects. **The funniest part? We use Opik MCP to scan through traces, so the sanitization is also for Claude Code to help optimise annotation rounds.**
3. RAG is the new (not so new) ETL for most projects. Instead of giving cleaned tables for analysts we give cleaned Markdowns for LLMs.

When the output was a dashboard, you could get away with mediocre metadata since humans find a way to surf the circumstances. An analyst would ask you what a column means and a LLM will just hallucinate to get the job done.

If you were lucky enough to work on ML training dataset ingestion pipelines, right now It looks completely different since quality, scores and metrics have other meanings.

When the output was a report, you could get away with undocumented business logic.

> *A stakeholder would flag the wrong number. An AI agent will present it with confidence (and the Stakeholder will believe It for months)*

---

## The Data Engineering Files: Exposed Shortcuts

Maybe you know what I am talking about when you read any of these:

We stopped maintaing documentation because nobody cared.

We stopped adding enforced quality tests for sources that were constantly Broken. But hey, ” **if the data is not fresh is data team’s fault.”**

We stopped adding metadata to reports and detailed descriptions because we were asked anyways instead of reading the actual information in front of stakeholders faces.

Fixing those shortcuts is... data engineering mindset at its finest.

My best advice is to let the AI problems come to you, and your value as a data engineer will be limitless.

Every RAG pipeline needs an ETL mindset. Every annotation round needs clean data. Every AI agent needs metadata that actually explains the business. Every observability system needs structured logs that someone has to design, extract, and serve.

You’re becoming the version of yourself that AI systems can’t function without.

And honestly? What a time to be a Data Engineer on steroids ❤️

---

If you enjoyed the content, hit the like ❤️ button, share, comment, repost, and all those nice things people do when like stuff these days. Glad to know you made it to this part!

---

![](https://substackcdn.com/image/fetch/$s_!BvlN!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c07b7dd-718f-4687-8769-56706a030950_1024x1024.jpeg)

*Hi, I am Alejandro Aboy. I am currently working as a Data Engineer. I started in digital marketing at 19. I gained experience in website tracking, advertising, and analytics. I also founded my agency. In 2021, I found my passion for data engineering. So, I shifted my career focus, despite lacking a CS degree. I’m now pursuing this path, leveraging my diverse experience and willingness to learn.*