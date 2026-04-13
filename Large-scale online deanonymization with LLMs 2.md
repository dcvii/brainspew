---
title: "Large-scale online deanonymization with LLMs"
source: "https://arxiv.org/abs/2602.16800"
author:
  - "[[Simon Lermen]]"
  - "[[Daniel Paleka]]"
  - "[[Joshua Swanson]]"
  - "[[Michael Aerni]]"
  - "[[Nicholas Carlini]]"
  - "[[Florian Tramèr]]"
published:
created: 2026-02-26
description: "Abstract page for arXiv paper 2602.16800: Large-scale online deanonymization with LLMs"
tags:
  - "clippings"
---
\[Submitted on 18 Feb 2026\]

## Title:Large-scale online deanonymization with LLMs

Authors:, , , , ,

[View PDF](https://arxiv.org/pdf/2602.16800) [HTML (experimental)](https://arxiv.org/html/2602.16800v1)

> Abstract:We show that large language models can be used to perform at-scale deanonymization. With full Internet access, our agent can re-identify Hacker News users and Anthropic Interviewer participants at high precision, given pseudonymous online profiles and conversations alone, matching what would take hours for a dedicated human investigator. We then design attacks for the closed-world setting. Given two databases of pseudonymous individuals, each containing unstructured text written by or about that individual, we implement a scalable attack pipeline that uses LLMs to: (1) extract identity-relevant features, (2) search for candidate matches via semantic embeddings, and (3) reason over top candidates to verify matches and reduce false positives. Compared to prior deanonymization work (e.g., on the Netflix prize) that required structured data or manual feature engineering, our approach works directly on raw user content across arbitrary platforms. We construct three datasets with known ground-truth data to evaluate our attacks. The first links Hacker News to LinkedIn profiles, using cross-platform references that appear in the profiles. Our second dataset matches users across Reddit movie discussion communities; and the third splits a single user's Reddit history in time to create two pseudonymous profiles to be matched. In each setting, LLM-based methods substantially outperform classical baselines, achieving up to 68% recall at 90% precision compared to near 0% for the best non-LLM method. Our results show that the practical obscurity protecting pseudonymous users online no longer holds and that threat models for online privacy need to be reconsidered.

| Comments: | 24 pages, 10 figures |
| --- | --- |
| Subjects: | Cryptography and Security (cs.CR); Artificial Intelligence (cs.AI); Machine Learning (cs.LG) |
| Cite as: | [arXiv:2602.16800](https://arxiv.org/abs/2602.16800) \[cs.CR\] |
|  | (or [arXiv:2602.16800v1](https://arxiv.org/abs/2602.16800v1) \[cs.CR\] for this version) |
|  | [https://doi.org/10.48550/arXiv.2602.16800](https://doi.org/10.48550/arXiv.2602.16800)  arXiv-issued DOI via DataCite (pending registration) |

## Submission history

From: Daniel Paleka \[[view email](https://arxiv.org/show-email/8821233b/2602.16800)\]  
**\[v1\]** Wed, 18 Feb 2026 19:02:50 UTC (1,555 KB)  

## Bibliographic and Citation Tools

Bibliographic Explorer *([What is the Explorer?](https://info.arxiv.org/labs/showcase.html#arxiv-bibliographic-explorer))*

Connected Papers *([What is Connected Papers?](https://www.connectedpapers.com/about))*

Litmaps *([What is Litmaps?](https://www.litmaps.co/))*

scite Smart Citations *([What are Smart Citations?](https://www.scite.ai/))*

## Code, Data and Media Associated with this Article

alphaXiv *([What is alphaXiv?](https://alphaxiv.org/))*

CatalyzeX Code Finder for Papers *([What is CatalyzeX?](https://www.catalyzex.com/))*

DagsHub *([What is DagsHub?](https://dagshub.com/))*

Gotit.pub *([What is GotitPub?](http://gotit.pub/faq))*

Hugging Face *([What is Huggingface?](https://huggingface.co/huggingface))*

Papers with Code *([What is Papers with Code?](https://paperswithcode.com/))*

ScienceCast *([What is ScienceCast?](https://sciencecast.org/welcome))*

## Demos

Replicate *([What is Replicate?](https://replicate.com/docs/arxiv/about))*

Hugging Face Spaces *([What is Spaces?](https://huggingface.co/docs/hub/spaces))*

TXYZ.AI *([What is TXYZ.AI?](https://txyz.ai/))*

## arXivLabs: experimental projects with community collaborators

arXivLabs is a framework that allows collaborators to develop and share new arXiv features directly on our website.

Both individuals and organizations that work with arXivLabs have embraced and accepted our values of openness, community, excellence, and user data privacy. arXiv is committed to these values and only works with partners that adhere to them.

Have an idea for a project that will add value for arXiv's community? [**Learn more about arXivLabs**](https://info.arxiv.org/labs/index.html).

[Which authors of this paper are endorsers?](https://arxiv.org/auth/show-endorsers/2602.16800) | [Disable MathJax](https://arxiv.org/abs/) ([What is MathJax?](https://info.arxiv.org/help/mathjax.html))