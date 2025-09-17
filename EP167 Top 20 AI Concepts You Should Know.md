---
title: "EP167: Top 20 AI Concepts You Should Know"
source: "https://blog.bytebytego.com/p/ep167-top-20-ai-concepts-you-should?publication_id=817132&post_id=165907323&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2025-06-14
created: 2025-06-14
description: "Which other AI concept will you add to the list?"
tags:
  - "clippings"
---
## WorkOS: Scoped Access and Control for AI Agents (Sponsored)

![](https://substackcdn.com/image/fetch/w_424)

AI agents can trigger tools, call APIs, and access sensitive data.  
Failing to control access creates real risk.

Learn how to:

- Limit what agents can do with scoped tokens
- Define roles and restrict permissions
- Log activity for debugging and review
- Secure credentials and secrets
- Detect and respond to suspicious behavior

Real teams are applying these practices to keep agent workflows safe, auditable, and aligned with least-privilege principles.

---

This week’s system design refresher:

- Top 20 AI Concepts You Should Know
- The AI Application Stack for Building RAG Apps
- Shopify Tech Stacks and Tools
- Our new book, Mobile System Design Interview, is available on Amazon!
- Featured Job
- Other Jobs
- SPONSOR US

---

## Top 20 AI Concepts You Should Know

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_424)

No alternative text description for this image

1. Machine Learning: Core algorithms, statistics, and model training techniques.
2. Deep Learning: Hierarchical neural networks learning complex representations automatically.
3. Neural Networks: Layered architectures efficiently model nonlinear relationships accurately.
4. NLP: Techniques to process and understand natural language text.
5. Computer Vision: Algorithms interpreting and analyzing visual data effectively
6. Reinforcement Learning: Distributed traffic across multiple servers for reliability.
7. Generative Models: Creating new data samples using learned data.
8. LLM: Generates human-like text using massive pre-trained data.
9. Transformers: Self-attention-based architecture powering modern AI models.
10. Feature Engineering: Designing informative features to improve model performance significantly.
11. Supervised Learning: Learns useful representations without labeled data.
12. Bayesian Learning: Incorporate uncertainty using probabilistic model approaches.
13. Prompt Engineering: Crafting effective inputs to guide generative model outputs.
14. AI Agents: Autonomous systems that perceive, decide, and act.
15. Fine-Tuning Models: Customizes pre-trained models for domain-specific tasks.
16. Multimodal Models: Processes and generates across multiple data types like images, videos, and text.
17. Embeddings: Transforms input into machine-readable vector formats.
18. Vector Search: Finds similar items using dense vector embeddings.
19. Model Evaluation: Assessing predictive performance using validation techniques.
20. AI Infrastructure: Deploying scalable systems to support AI operations.

Over to you: Which other AI concept will you add to the list?

---

## The AI Application Stack for Building RAG Apps

![graphical user interface, application](https://substackcdn.com/image/fetch/w_424)

graphical user interface, application

1. Large Language Models  
	These are the core engines behind Retrieval-Augmented Generation (RAG), responsible for understanding queries and generating coherent and contextual responses. Some common LLM options are OpenAI GPT models, Llama, Claude, Gemini, Mistral, DeepSeek, Qwen 2.5, Gemma, etc.
2. Frameworks and Model Access  
	These tools simplify the integration of LLMs into your applications by handling prompt orchestration, model switching, memory, chaining, and routing. Common tools are Langchain, LlamaIndex, Haystack, Ollama, Hugging Face, and OpenRouter.
3. Databases  
	RAG applications rely on storing and retrieving relevant information. These vector databases are optimized for similarity search, while relational options like Postgres offer structured storage. Tools are Postgres, FAISS, Milvus, pgVector, Weaviate, Pinecone, Chroma, etc.
4. Data Extraction  
	To populate your knowledge base, these tools help extract structured information from unstructured sources like PDFs, websites, and APIs. Some common tools are Llamaparse, Docking, Megaparser, Firecrawl, ScrapeGraph AI, Document AI, and Claude API.
5. Text Embeddings  
	Embeddings convert text into high-dimensional vectors that enable semantic similarity search, which is a critical step for connecting queries with relevant context in RAG. Common tools are Nomic, OpenAI, Cognita, Gemini, LLMWare, Cohere, JinaAI, and Ollama.

Over to you: What else will you add to the list to build RAG apps?

---

## Shopify Tech Stacks and Tools

Shopify handles scale that would break most systems.

![](https://blog.bytebytego.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/801cc519-68cc-4e1d-88b6-b9821b5e6b52_1222x1600.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:1600,%22width%22:1222,%22resizeWidth%22:null,%22bytes%22:null,%22alt%22:null,%22title%22:null,%22type%22:null,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null,%22offset%22:false%7D)

On a single day (Black Friday 2024), the platform processed 173 billion requests, peaked at 284 million requests per minute, and pushed 12 terabytes of traffic every minute through its edge.

These numbers aren’t anomalies. They’re sustained targets that Shopify strives to meet. Behind this scale is a stack that looks deceptively simple from the outside: Ruby on Rails, React, MySQL, and Kafka.

But that simplicity hides sharp architectural decisions, years of refactoring, and thousands of deliberate trade-offs.  
  
In this newsletter, we map the tech stack powering Shopify from:

- the modular monolith that still runs the business,
- to the pods that isolate failure domains,
- to the deployment pipelines that ship hundreds of changes a day.
- It covers the tools, programming languages, and patterns Shopify uses to stay fast, resilient, and developer-friendly at incredible scale.

A huge thank you to Shopify’s world-class engineering team for sharing their insights and for collaborating with us on this deep technical exploration.  
  
🔗 Dive into the [full newsletter here](https://blog.bytebytego.com/p/shopify-tech-stack).

---

## Our new book, Mobile System Design Interview, is available on Amazon!

Book author: Manuel Vicente Vivo

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_424)

No alternative text description for this image

What’s inside?

- An insider's take on what interviewers really look for and why.
- A 5-step framework for solving any mobile system design interview question.
- 7 real mobile system design interview questions with detailed solutions.
- 24 deep dives into complex technical concepts and implementation strategies.
- 175 topics covering the full spectrum of mobile system design principles.

Table Of Contents  
Chapter 1: Introduction  
Chapter 2: A Framework for Mobile System Design Interviews  
Chapter 3: Design a News Feed App  
Chapter 4: Design a Chat App  
Chapter 5: Design a Stock Trading App  
Chapter 6: Design a Pagination Library  
Chapter 7: Design a Hotel Reservation App  
Chapter 8: Design the Google Drive App  
Chapter 9: Design the YouTube app  
Chapter 10: Mobile System Design Building Blocks  
Quick Reference Cheat Sheet for MSD Interview

---

## Featured Job

**Founding Engineer** @ [dbdasher.ai](http://dbdasher.ai/)

**Location:** Remote (India)

**Role Type:** Full-time

**Compensation:** Highly Competitive

**Experience Level:** 2+ years preferred

**About dbdasher.ai:** dbdasher.ai is a well-funded, high-ambition AI startup on a mission to revolutionize how large enterprises interact with data. We use cutting-edge language models to help businesses query complex datasets with natural language. We’re already working with two pilot customers - a publicly listed company and a billion-dollar private enterprise and we’re just getting started.

We’re building something new from the ground up. If you love solving hard problems and want to shape the future of enterprise AI tools, this is the place for you.

**About the Role**: We’re hiring a **Founding Engineer** to join our early team and help build powerful, user-friendly AI-driven products from scratch. You’ll work directly with the founders to bring ideas to life, ship fast, and scale systems that power real-world business decisions.

If you are interested, [apply here](https://forms.gle/mBLMzKCa8DWjcz4U8) or email Rishabh at [rishabh@dbdasher.ai](http://rishabh@dbdasher.ai/)

---

## Other Jobs

We collaborate with [Jobright.ai](http://jobright.ai/) (an AI job search copilot trusted by 500K+ tech professionals) to curate this job list.

**This Week’s High-Impact Roles at Fast-Growing AI Startups**

- [Senior Software Engineer, Search Evaluations](https://jobright.ai/jobs/info/684b67131981744e3f959f04?utm_source=1118&utm_campaign=alex&utm_id=684b67131981744e3f959f04) at OpenAI (San Francisco, CA)
	- Yearly: 245,000 - 465,000USD
	- OpenAI creates artificial intelligence technologies to assist with tasks and provide support for human activities.
- [Staff Software Engineer, ML Engineering](https://jobright.ai/jobs/info/684a1477c64d4c2806ab67a8?utm_source=1118&utm_campaign=alex&utm_id=684a1477c64d4c2806ab67a8) at SmarterDx (United States)
	- Yearly: 220,000 - 270,000USD
	- SmarterDx is a clinical AI company that develops automated pre-bill review technology to assist hospitals in analyzing patient discharges.
- [Software Engineering Manager, Core Platform](https://jobright.ai/jobs/info/684a242166f3958ef0641068?utm_source=1118&utm_campaign=alex&utm_id=684a242166f3958ef0641068) at Standard Bots (New York, NY)
	- Yearly: 220,000 - 240,000
	- Standard Bots offers advanced automation solutions, including the RO1 robot, to help businesses streamline their operations.

**High Salary SWE Roles this week**

- [Web UI Engineer (L4)](https://jobright.ai/jobs/info/684b3154cb6a43977f3ab5c3?utm_source=1118&utm_campaign=alex&utm_id=684b3154cb6a43977f3ab5c3) at Netflix (Los Gatos, CA)
	- Yearly: 100,000 - 720,000USD
- [Principal Switch Engineering Architect](https://jobright.ai/jobs/info/682ecfac5839695667c60403?utm_source=1118&utm_campaign=alex&utm_id=682ecfac5839695667c60403) at NVIDIA (Westford, MA)
	- Yearly: 272,000 - 425,500USD
- [Staff iOS Engineer, Banking Mobile](https://jobright.ai/jobs/info/684b54a19ab1780ff6cfe1c8?utm_source=1118&utm_campaign=alex&utm_id=684b54a19ab1780ff6cfe1c8) at Square (United States)
	- Yearly: 263,600 - 395,400USD

**Today’s latest ML positions - hiring now!**

- [Senior/Principal Machine Learning Engineer](https://jobright.ai/jobs/info/684b67131981744e3f959f00?utm_source=1118&utm_campaign=alex&utm_id=684b67131981744e3f959f00) at Red Hat (Raleigh, NC)
	- Yearly: 170,770 - 312,730USD
- [Applied Machine Learning Engineer](https://jobright.ai/jobs/info/684b1ffaf2de8740c0cc2ff8?utm_source=1118&utm_campaign=alex&utm_id=684b1ffaf2de8740c0cc2ff8) at Jobot (Roseville, CA)
	- Yearly: 200,000 - 270,000USD
- [Machine Learning Engineer](https://jobright.ai/jobs/info/684b6b0dba7c1e7bafd4eb12?utm_source=1118&utm_campaign=alex&utm_id=684b6b0dba7c1e7bafd4eb12) at Docusign (Seattle, WA)
	- Yearly: 157,500 - 254,350USD

---

## SPONSOR US

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **sponsorship@bytebytego.com**