---
title: "Data Contracts: A Missed Opportunity"
source: "https://www.dataengineeringweekly.com/p/data-contracts-a-missed-opportunity?publication_id=73271&post_id=185210924&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Ananth Packkildurai]]"
published: 2026-01-20
created: 2026-01-20
description: "The Conversation We Should Have Had—Before Thought Leadership Replaced System Design"
tags:
  - "clippings"
---
### The Conversation We Should Have Had—Before Thought Leadership Replaced System Design

Over the last couple of years, the data industry has been having a conversation about data contracts that never quite went where they needed to.

There was no shortage of activity around the topic. Definitions were proposed and refined. Conceptual boundaries were drawn and redrawn. Data contracts were compared to APIs, governance frameworks, data mesh primitives, and ideas teams already “sort of” implemented in practice.

> *The discussion was energetic and well-intentioned, but it tended to stay at the level of classification rather than construction.*

What was largely absent was sustained engagement with the engineering consequences of taking data contracts seriously. Questions about enforcement, evolution, compatibility, and failure modes appeared only briefly before the conversation moved on. The result was an industry consensus that data contracts were “interesting,” without a shared understanding of what it would actually mean to build platforms around them.

In hindsight, this matters—not because the debate was unproductive, but because of what happened in parallel.

---

## The Shift Happening Elsewhere

![](https://substackcdn.com/image/fetch/$s_!7mSh!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3dcd1ddb-f6d6-4190-a234-23cc6febd34d_2048x1126.png)

While the data community was debating what data contracts *were*, the software engineering world was converging—quietly and pragmatically—on a different organizing principle: **specifications as the primary unit of system design**.

This wasn’t a philosophical shift so much as an operational one. As systems became more distributed, more automated, and more interdependent, informal agreements stopped scaling. Documentation drifted. Assumptions diverged. Human coordination became the bottleneck.

The response was not more process, but more precision.

APIs began with schemas rather than code. Infrastructure moved from scripts to declarative specifications. Compatibility rules were automatically encoded and enforced. In these systems, the specification was no longer an artifact produced alongside the system—it *was* the system.

More recently, AI agents have accelerated this trend. Agents do not operate on intent, convention, or context. They operate on explicit, machine-readable, and verifiable data. Where specifications exist, agents can reason deterministically. Where they do not, agents approximate—and approximation is rarely acceptable in core infrastructure.

This is where the connection to data contracts becomes unavoidable.

---

## Data Contracts as Specifications, Not Concepts

![](https://substackcdn.com/image/fetch/$s_!1ja9!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe050308d-37ed-4cde-8b4e-ce1dfb8c784e_1536x1024.png)

Viewed through the lens of spec-driven development, data contracts stop looking like a data-specific innovation and become a familiar pattern applied to a different domain.

A properly implemented data contract is a specification:

- It defines structure, semantics, and invariants
- It establishes compatibility guarantees over time.
- It is versioned, validated, and enforced programmatically.
- It creates a stable interface between independently evolving systems.

This is exactly what spec-driven development has optimized for in software engineering.

The difference is not conceptual—it is operational. Software engineering treated specifications as executable constraints. The data industry often treated contracts as descriptive artifacts. As a result, contracts were discussed as governance tools or communication mechanisms, rather than as interfaces with failure semantics.

That framing limited how far the idea could go.

---

## Where the Two Worlds Diverged

Spec-driven systems force early clarity around hard problems.

- How does change propagate?
- What is allowed to evolve independently?
- What breaks compatibility, and how is that detected?
- Where does enforcement occur, and what happens when it fails?

In software systems, these questions are answered in code and tooling. In data systems, they were often answered socially. Producer–consumer agreements existed, but they lived in tickets, meetings, and tribal knowledge rather than in executable form.

Many teams compensated by building partial solutions: strong schemas, upstream quality checks, and informal SLAs. These patterns worked, but they relied heavily on human intervention. They were resilient, but not legible to machines.

As long as humans were the primary integrators, this was manageable. As soon as AI agents enter the workflow, it becomes a constraint.

---

## Why Spec-Driven Thinking Changes the Next Phase

AI agents make an implicit demand of data platforms: **make your rules explicit**.

Agents can generate schemas, propose transformations, reason about compatibility, and enforce policy—but only if the platform exposes contracts in a form they can execute against. Without that, agents revert to inference, which introduces uncertainty precisely where determinism is required.

This is the practical implication of spec-driven development for data engineering. It’s not about adopting a new paradigm. It’s about recognizing that the platform already behaves like a system of interfaces—and formalizing those interfaces accordingly.

Teams that have already internalized contract discipline will find this transition incremental. Teams that have not will experience it as friction.

---

## What We Should Do Next

At this point, the terminology matters less than the mechanics.

Whether we call them data contracts, data interfaces, or executable schemas, the path forward is the same:

- Treat schemas as specifications, not documentation
- Encode quality, semantics, and compatibility as executable rules
- Enforce contracts at clear system boundaries, preferably early.
- Version data interfaces with the same rigor as APIs
- Make ownership and accountability explicit and machine-readable.

This is not about adding process. It is about making systems legible to other systems.

---

## Closing Thought

The original data contracts conversation wasn’t wrong. It just stopped too early.

Spec-driven development has shown that explicit, enforceable interfaces are not optional in complex, automated systems. Data platforms are now at that same inflection point.

Data contracts were never the destination.

They were the missing layer that would have made everything else easier to build.

The opportunity is still there—but only if we’re willing to treat contracts as infrastructure, not ideas.

## References

***[https://www.thoughtworks.com/insights/podcasts/technology-podcasts/data-contracts-what-why](https://www.thoughtworks.com/insights/podcasts/technology-podcasts/data-contracts-what-why)***

**[https://airbyte.com/data-engineering-resources/data-contracts](https://airbyte.com/data-engineering-resources/data-contracts)**

**[https://soda.io/blog/what-are-data-contracts](https://soda.io/blog/what-are-data-contracts)**

**[https://atlan.com/data-contracts/](https://atlan.com/data-contracts/)**

**[https://en.wikipedia.org/wiki/Spec-driven\_development](https://en.wikipedia.org/wiki/Spec-driven_development)**

**[https://medium.com/software-architecture-in-the-age-of-ai/why-interfaces-and-contracts-are-not-the-same-and-why-that-matters-with-10-examples-408524f6d17c](https://medium.com/software-architecture-in-the-age-of-ai/why-interfaces-and-contracts-are-not-the-same-and-why-that-matters-with-10-examples-408524f6d17c)**

**[https://arxiv.org/abs/2507.21056](https://arxiv.org/abs/2507.21056)**