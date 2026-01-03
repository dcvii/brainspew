---
title: (13) Post | LinkedIn
source: https://www.linkedin.com/posts/frode-nilssen-94123692_dataengineering-ai-enterprise-activity-7411032129523834880-rDor/?rcm=ACoAAAAAC8EBi_lxU_6Klz2yl1UUE_kf5p8oALU
author:
published: 2d
created: 2025-12-30
description:
tags:
  - clippings
  - Palantir
---
I spent a week going through Palantir's software. Here's what their "$10M enterprise AI platform" actually does.  
  
Course 1: Ontology Management  
Create object types from database tables, define foreign key relationships in a GUI, add form actions to update records.  
  
Translation: ER modeling with visual tooling.  
  
Course 2: AIP Workflow (RAG Pipeline)  
Extract text from PDFs, chunk into 512-character segments, call GPT-4 for entity extraction, generate embeddings, store in tables for vector search.  
  
Translation: Standard RAG pipeline. LangChain does this in 100 lines.  
  
Course 3: "Agentic AI"  
User creates patient record → automation triggers → single LLM API call with structured prompt → parse JSON response → update database.  
  
Translation: \`IF record\_created THEN call\_openai() END\`  
  
The Fundamental Contradiction  
  
Palantir's pitch: Government-grade security, data sovereignty, compliance infrastructure, air-gapped deployments.  
  
Their training: Send your data to OpenAI APIs for embeddings and LLM calls.  
  
These cannot coexist in regulated environments.  
  
The "Agent" Evaluation  
  
Testing methodology for clinical trial eligibility:  
\- 3 test cases  
\- First run: 2/3 pass (GPT-4)  
\- Second run: 3/3 pass (same model, no changes)  
\- Conclusion: "Ship it"  
  
Model non-determinism treated as validation. For healthcare data. With regulatory implications.  
  
No false positive analysis. No bias testing. No production monitoring strategy.  
  
What You're Actually Buying  
  
Technology: Pre-built connectors, GUI workflows, governance tracking, object-relational mapping.  
  
Actual value: Sales relationships with procurement, risk transfer from internal teams to vendor, "no one gets fired for buying Palantir."  
  
The Real Cost  
  
Build equivalent functionality:  
\- PostgreSQL + pgvector: $0  
\- Airflow/Prefect: $0  
\- LangChain: $0  
\- Development: 2-4 weeks  
  
Palantir: $10M+ with 18-month timeline.  
  
The 1000x markup isn't for superior technology.  
  
Rebrand ER diagrams as "ontology." Call ETL "transformations." Wrap LLM API calls as "agentic AI." Add enterprise UI. Charge enterprise prices.  
  
If you're evaluating this platform: Look past buzzwords. Ask about lock-in, cost, and whether you could build this in a sprint.  
  
The impressive part isn't the technology. It's convincing enterprises that standard data engineering is worth $10M because it has consultants who speak procurement language.  
  
Good software shouldn't need this much rebranding.  
  
[hashtag#DataEngineering](https://www.linkedin.com/search/results/all/?keywords=%23dataengineering&origin=HASH_TAG_FROM_FEED) [hashtag#AI](https://www.linkedin.com/search/results/all/?keywords=%23ai&origin=HASH_TAG_FROM_FEED) [hashtag#Enterprise](https://www.linkedin.com/search/results/all/?keywords=%23enterprise&origin=HASH_TAG_FROM_FEED) [hashtag#BuildVsBuy](https://www.linkedin.com/search/results/all/?keywords=%23buildvsbuy&origin=HASH_TAG_FROM_FEED) [hashtag#MachineLearning](https://www.linkedin.com/search/results/all/?keywords=%23machinelearning&origin=HASH_TAG_FROM_FEED) [hashtag#MLOps](https://www.linkedin.com/search/results/all/?keywords=%23mlops&origin=HASH_TAG_FROM_FEED) [hashtag#SoftwareEngineering](https://www.linkedin.com/search/results/all/?keywords=%23softwareengineering&origin=HASH_TAG_FROM_FEED) [hashtag#TechLeadership](https://www.linkedin.com/search/results/all/?keywords=%23techleadership&origin=HASH_TAG_FROM_FEED) [hashtag#RAG](https://www.linkedin.com/search/results/all/?keywords=%23rag&origin=HASH_TAG_FROM_FEED) [hashtag#LLM](https://www.linkedin.com/search/results/all/?keywords=%23llm&origin=HASH_TAG_FROM_FEED) [hashtag#OpenSource](https://www.linkedin.com/search/results/all/?keywords=%23opensource&origin=HASH_TAG_FROM_FEED)  
  
\*\*P.S.\*\* Their training sends clinical trial patient data through external OpenAI APIs while positioning for regulated industries. That gap between marketing and reality tells you everything.