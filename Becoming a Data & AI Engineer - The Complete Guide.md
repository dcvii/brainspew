---
title: "Becoming a Data & AI Engineer - The Complete Guide"
source: "https://thepipeandtheline.substack.com/p/becoming-a-data-and-ai-engineer-the-complete-guide?publication_id=1196229&post_id=193149106&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alejandro Aboy]]"
published: 2026-04-15
created: 2026-04-16
description: "Around a year of failing & learning with AI production projects, combining vision, strong opinions, tools and demo projects based on real work."
tags:
  - "brain_spew"
---
> Hi there! Alejandro here 😊
> 
> Subscribe if you like to read about technical data & AI learnings, deep dives!
> 
> Enjoy the reading and let me know in the comments what you think about it 👨🏻💻

*Every AI article I’ve written for data engineers, organized into one learning path from RAG fundamentals to production agents.*

*This is Part 2. For the narrative behind these ideas, read [Becoming a Data & AI Engineer: An Honest WIP Report](https://thepipeandtheline.substack.com/p/becoming-a-data-ai-engineer-an-honest-wip-report) to see what the transition actually looks like and what I’ve learned.*

---

## 📝 TL;DR

- Part 1 describes the loop: pipeline → AI breaks it → fix the data → repeat. This is the map of everything behind that loop
- RAG is the most direct on-ramp because the mental model is identical to ETL. The 4-part series covers it end to end
- Security, MCP, and SKILLs each have a series that ends with a repo you can clone and run
- Production lessons from 1+ year of building agents: what broke, what worked, what I’d do differently
- 6 collaborations across 5 publications covering observability, MetadataOps, and the agentic data stack

---

> ![](https://substackcdn.com/image/fetch/$s_!Folz!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F439bd36f-353b-4da5-911c-58f20da1a929_2024x926.png)
> 
> *This article is sponsored by [OpenXData](https://www.openxdata.ai/)*
> 
> *If you’re a data engineer figuring out how your pipelines, models, and metadata actually serve AI systems in production, **OpenXData** is running a free virtual conference built around exactly that.*
> 
> ***April 29, 9am–3pm PT.***
> 
> *Technical sessions and workshops that go beyond design slides to what holds up in production. From engineers at Uber, Meta, Booking, Snowflake, Anthropic and many others.*
> 
> *The kind of problems we talk about here every week, discussed by the teams solving them at scale.*

---

> *⚠️ **Disclaimer**: Some articles were written 6 months ago, which in AI times that means like 5 years ago 😅. Note that I always focus my approach on fundamentals and core ideas so its easy to transfer knowledge, but it’s also possible there’s a more efficient and new shiny way of doing some things, so feel free to drop a comment about it and we can discuss it!*

## Article Series

In Part 1 I mentioned that RAG is the ETL of AI, that security is an architecture decision, and that MCP changed how I work across the full stack. These three series are the deep dives behind those claims.

### RAG for Data Engineers (4 parts)

> ***[Start here: LLM Limitations, Fundamentals, Alternatives](https://thepipeandtheline.substack.com/p/rag-intro-for-data-professionals)***

Four articles covering why RAG exists, vector databases and embeddings, similarity search with metadata filters, and a full hands-on implementation with OpenAI, Agno and PgVector. The series ends with a working pipeline you can clone from the [companion repo](https://github.com/alejandroaboy/rag-data-engineers).

> *The data engineering part defines 80% of the project. Don’t rush it. Craft it properly.*

Only fine-tune if prompting and RAG fall short. 100 precise examples outperform 1,000 mediocre ones.

> ***[Introduction To Fine Tuning Pipelines For Data Engineers](https://thepipeandtheline.substack.com/p/fine-tuning-pipelines-for-data-engineers)***

---

### Secure LLMs for Data Engineers (4 parts)

> ***[Start here: Structured Outputs](https://thepipeandtheline.substack.com/p/secure-llms-structured-outputs)***

Four articles: structured outputs for reliability, prompt injection prevention, secure design principles (least privilege, scoped tools), and a hands-on guardrails implementation with Agno. Clone the [ShamanAI repo](https://github.com/alejandroaboy/shamanAI) for working examples of all four security layers.

> *Scope your agent’s permissions at the architecture stage. An agent can’t drop a production table it doesn’t have access to.*

---

### MCP & SKILLs (4 parts)

> ***[Start here: He Built an MCP Server So You Can Talk to AI About Any Substack Author](https://buildtolaunch.substack.com/p/69f7f07b-fd30-44a8-8a29-8a3491e31f7f)***

The origin story, then the architecture breakdown ([Behind Substack Author MCP](https://thepipeandtheline.substack.com/p/behind-substack-author-mcp-resources)), the concept of SKILLs as progressive disclosure for agents ([What’s the real deal about SKILLs](https://thepipeandtheline.substack.com/p/whats-the-real-deal-about-skills)), and a full hands-on build ([Building a Substack Agent with SKILLs and MCP](https://thepipeandtheline.substack.com/p/hands-on-building-a-substack-agent)). The final article ships a working agent with 5 SKILLs and remote MCP tools.

> *SKILLs encode the judgment for using tools. Publishing them through MCP makes that judgment available to every connected client.*

---

## Hands-On Projects

Part 1 mentions that context engineering is just data modelling with a new name. These collaborations explore what that means in practice: metadata as prompts, agents as data products, and organizational readiness.

> ***[End To End Agentic Data Modeling: Using AI and OpenMetadata MCP](https://pipeline2insights.substack.com/p/end-to-end-agentic-data-modeling-with-openmetadata-and-mcp)** — with* [Erfan Hesami](https://open.substack.com/users/277538242-erfan-hesami?utm_source=mentions) *\-* [Pipeline to Insights](https://open.substack.com/users/42238863-pipeline-to-insights?utm_source=mentions)

When dbt meets AI agents and a metadata platform, a single schema change triggers full downstream visibility. [GitHub repo](https://github.com/aboyalejandro/agentic-data-modeling).

We also talked about spending more time working *on* the system that writes code. These are the concrete workflows behind that shift.

> ***[Intro To Claude Code For Data Engineers (Skills, MCPs & Hooks)](https://thepipeandtheline.substack.com/p/intro-claude-code-for-data-engineers)***

The map of how MCP servers, Skills, and Hooks chain together into custom data engineering workflows.

> ***[Hands-On Claude Code for Data Engineers: Data Modeling with dbt, Miro & PostgreSQL](https://thepipeandtheline.substack.com/p/claude-code-for-data-engineers-data-modeling-dbt-miro-postgresql-skills-mcp)***

Miro MCP reads requirements, Data Toolbox explores the database, a Skill translates both into dbt models, with an approval step before writing any SQL.

*90% of data modeling happens outside the tools that implement it. This workflow brings the design and the code into the same session.*

> ***[Pytest for Data: Fixtures, Mocks, CI/CD, and Claude Code Hooks](https://thepipeandtheline.substack.com/p/i-learned-pytest-after-testing-in)***

Testing data pipelines with pytest, and hooking tests into Claude Code so they run automatically before every commit.

---

## Production Lessons

The instinct gap from Part 1: AI identifies the error but suggests removing Pandas entirely. These articles cover what actually breaks in production and how to build the judgment layer around it.

> ***[Learnings From 1 Year of Building AI Agents](https://thepipeandtheline.substack.com/p/learnings-from-1-year-of-building)***

Less system prompt equals more consistency. Tool design is critical because each description is a prompt itself.

Had a 1,000-line prompt. Cut it to 250. Users said “now it gets what you want.” Less is genuinely more.

> ***[The Untold Pains About Building AI Agents On Production](https://thepipeandtheline.substack.com/p/the-untold-pains-about-building-ai)***

pgvector is probably all you need for RAG. Model updates will break your agent. Pin versions, always have a rollback plan.

> ***[How AI Can Improve Your Data Modeling (And What’s Still Missing)](https://thepipeandtheline.substack.com/p/how-ai-can-improve-your-data-modeling)***

The article that started the conversation. AI keeps improving but data development workflows are still missing real AI-assisted context.

---

## Vision On The AI & Data Engineering Profile

> ***[Data Engineers Are Becoming MetadataOps Engineers (And You Don’t Even Know It Yet)](https://www.datagibberish.com/p/data-engineers-are-becoming-metadataops-engineers)** — with Data Gibberish*

The consumer changed from analysts to LLMs. Documentation is now a prompt. Vague metadata equals hallucinations.

> *Add “Can an AI understand this?” to your definition of done. That’s MetadataOps.*

---

> ***[Behind the Scenes of AI Observability in Production](https://www.decodingai.com/p/behind-the-scenes-of-ai-observability)** — with Decoding AI Magazine*

Implementing observability on a production agent with 50+ tools. The 3 biggest mistakes teams make and a framework for annotation sessions that actually improve your agents.

---

### The Agentic Future of Data — with Modern Data 101

Three articles exploring the same question from different angles: what happens when AI agents become permanent residents of the data stack.

> ***[Agentic Data Stack: A New Era For Data Professionals](https://moderndata101.substack.com/p/agentic-data-stack-new-era-for-data-professionals)***

The vision: agents as first-class citizens across ingestion, transformation, and governance.

> ***[How Long Until We Call AI Agents Data Products](https://moderndata101.substack.com/p/data-products-as-ai-agents)***

The operational shift: treating agents like data products with users, feedback loops, and a roadmap.

> ***[The Vision of Vibe Data Modeling: Are Organisations Ready?](https://moderndata101.substack.com/p/vibe-data-modeling)***

The readiness check: the tooling is almost there, but metadata, governance, and team culture are the actual blockers.

---

If you enjoyed the content, hit the like ❤️ button, share, comment, repost, and all those nice things people do when like stuff these days. Glad to know you made it to this part!

---

![Alejandro Aboy's avatar](https://substackcdn.com/image/fetch/$s_!pntI!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fde90c745-7f5a-404e-b2d6-eaab9420dd98_881x881.png)

Alejandro Aboy's avatar

*Hi, I am Alejandro Aboy. I am currently working as a Data Engineer. I started in digital marketing at 19. I gained experience in website tracking, advertising, and analytics. I also founded my agency. In 2021, I found my passion for data engineering. So, I shifted my career focus, despite lacking a CS degree. I’m now pursuing this path, leveraging my diverse experience and willingness to learn.*