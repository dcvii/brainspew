---
title: "A Response to Our Reader Survey"
source: "https://www.dataengineeringweekly.com/p/a-response-to-our-reader-survey?publication_id=73271&post_id=194314526&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Ananth Packkildurai]]"
published: 2026-04-15
created: 2026-04-15
description: "Your feedback prompted us to review 233 articles across 25 issues, clarify our editorial scope, and raise the bar for what belongs in Data Engineering Weekly."
tags:
  - "brain_spew"
---
### Your feedback prompted us to review 233 articles across 25 issues, clarify our editorial scope, and raise the bar for what belongs in Data Engineering Weekly.

Thank you to every reader who took a few minutes to fill out the survey. Your feedback is the clearest signal we have — and this round gave us a lot to act on.

One piece of feedback came through clearly enough that we’d be wrong to gloss over it: several of you feel we’ve leaned too heavily into AI coverage. That’s a fair critique. So we did what data engineers do: we audited ourselves.

We reviewed 233 articles published across 25 issues, from July 2025 through April 2026. The audit made one thing clear — while the majority of our content has remained relevant to data engineers, we have not been as precise as we should be. That precision gap showed up in 44 articles, or 18.9% of the total, which we now classify as outside the newsletter’s editorial scope: prompting tutorials, generic agent framework walkthroughs, model-release commentary, and LLM inference economics that follow the AI news cycle more than the data engineer’s day-to-day reality.

The survey also returned encouraging numbers. Data Engineering Weekly earned a ***Net Promoter Score of +17.3, and 79.6% of respondents rated their experience as Satisfied or Very Satisfied***. We don’t take those numbers for granted. They reflect real signals from practitioners who are selective about where they invest their attention. But the critique is what drove this post, and the critique is what we are acting on.

---

## What the Data Says

Across 233 articles published in 25 issues: Category Articles Share of the total 233 articles

1. Core DE 99 42.5%
2. Adjacent but Relevant 60 25.8%
3. Not DE 44 18.9%
4. Context Engineering (DE extension) 30 12.9%

The 44 out-of-scope articles are the problem we are fixing. The 189 in-scope articles are the standard we are holding ourselves to.

The survey revealed two truths at once: readers were right to call out drift, and we still believe that some of the work at the intersection of data infrastructure and AI belongs squarely within the future of data engineering. The rest of this post explains exactly where we draw that line — and what changes now.

You can read the complete analysis here  
**[https://docs.google.com/spreadsheets/d/1kLq\_touW4Z0SXDjCWEg4zt1DZzBoZFyTM2d2KJAR\_tQ/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1kLq_touW4Z0SXDjCWEg4zt1DZzBoZFyTM2d2KJAR_tQ/edit?usp=sharing)**

---

## Our Editorial Categories

Our test is straightforward: if a working data engineer cannot reasonably connect a piece to the systems they build, operate, govern, or evolve, it does not belong in the newsletter.

We use four categories to apply that test. They are not new instincts — they formalize the editorial judgment we have always tried to apply, and they give us, and you, a shared framework for accountability.

### Core DE

**Classical data engineering topics: ingestion, storage, orchestration, batch/streaming, table formats, query engines, data modeling, quality, governance, and platform reliability.**

This is the foundation. Articles in Core DE cover the systems data engineers’ own every day — pipeline architecture, storage layer decisions, table format trade-offs, query engine internals, data quality frameworks, and the operational realities of running data infrastructure at scale.

### Context Engineering (DE extension)

**Context/semantic layers, ontologies, knowledge graphs, NL-to-SQL, data agents, and other systems that turn enterprise data into governed machine-usable context.**

One category deserves a more explicit explanation, because it sits at the center of both the feedback we received and the direction this field is heading.

The reader survey did not change my view that Context Engineering belongs in Data Engineering Weekly. It forced a more disciplined articulation of that view — and a much stricter standard for what qualifies.

If you have read **[ETL is Dead](https://www.dataengineeringweekly.com/p/etl-is-dead)** or **[Data Engineering After AI](https://www.dataengineeringweekly.com/p/data-engineering-after-ai)**, you know where I stand. AI coding agents are reshaping how we work with data, and that shift is not temporary. The data engineer’s value is migrating from pipeline reliability to semantic reliability — from “the job ran” to “the meaning is right.” ETL is dead, the way landlines are dead: the pipelines still run, but nobody builds their data strategy around them anymore. The new leverage lies in designing systems that make AI-generated code trustworthy and grounded in a governed, machine-usable context. Extract, Contextualize, Link rather than Extract, Transform, Load.

I would not be doing justice to our Data Engineering Weekly community if I excluded the engineering questions that come with that shift. The issue was never whether DEW should cover AI-adjacent work. The issue was whether each piece remained grounded in the systems, semantics, governance, and infrastructure that data engineers actually own.

That is the line. In scope: systems that make enterprise data structured, governed, semantic, and machine-readable. Out of scope: prompting tactics, agent framework tutorials, model release commentary, and generic application-layer AI workflows.

### Adjacent but Relevant

**AI/ML platform, feature store, search/retrieval infrastructure, eval/observability, or AI governance topics that materially touch DE skills or infrastructure without being pure DE.**

Data engineers do not work in isolation. The systems they build feed ML platforms, power search infrastructure, and underpin AI governance frameworks. We include this category selectively — only when the infrastructure implications are concrete, the engineering depth is substantial, and the connection to a working data engineer’s responsibilities is immediate rather than abstract. An article on feature store architecture belongs here. A think-piece on the AI market does not.

### Not DE

**Prompting, generic agent frameworks, model-news / benchmark/market commentary, app-layer AI orchestration, pure ML modeling, or other pieces with no substantial data-infrastructure center of gravity.**

This is the content we are eliminating. It may be technically credible and widely read, but it is not written for data engineers and does not serve your work.

---

## What Changes Now

Here is what is different, starting with the next issue:

**Zero Not DE articles per issue.** Every article will be evaluated against the four categories above before publication. If it does not clear the bar, it does not go in.

**A stricter standard for Adjacent but Relevant.** The infrastructure angle must be concrete, the engineering substance must be real, and the relevance to a working data engineer must be direct — not abstract or aspirational.

**Strict vendor neutrality.** Data Engineering Weekly will remain strictly vendor-neutral. We generally exclude content published primarily to promote a product, platform, or company, with rare exceptions for work of exceptional technical depth and broad practitioner value. The content we select is written by practitioners for practitioners and published on personal blogs, company engineering blogs, or open platforms, where the goal is to share real experience, not to drive adoption.

**Periodic transparency reports.** We will share our category breakdown across recent issues so you can hold us to this standard.

---

## Help Us Build the Signal

Data Engineering Weekly is a community effort. The best issues are shaped by readers who surface work worth sharing.

If you have read something — a post, an engineering deep-dive, a company blog — that fits clearly within Core DE, Context Engineering, or Adjacent but Relevant, submit it. Contributions are reviewed weekly, and we read everything that comes in. The process is lightweight: open a pull request with the article title, link, author details, and topic tags using our **[Contributing Guide](https://github.com/Data-Engineering-Weekly/dataengineeringweekly?tab=readme-ov-file#contributing-guide)**. The same editorial categories and vendor-neutrality standard described here apply to all submissions.

As we advance, each issue should feel sharper, more grounded, and more consistently useful to working data engineers. That is the standard we are setting for ourselves, and the standard we invite you to hold us to.

If you have feedback on this policy or on individual articles, reply directly to any issue. We read every response.

---

*All rights reserved, Dewpeche Private Limited. I have provided links for informational purposes and do not suggest endorsement. All views expressed in this newsletter are my own and do not represent current, former, or future employers’ opinions.*