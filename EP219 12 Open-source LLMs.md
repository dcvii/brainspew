---
title: "EP219: 12 Open-source LLMs"
source: "https://blog.bytebytego.com/p/ep219-12-open-source-llms?publication_id=817132&post_id=202318529&isFreemail=true&r=of68&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2026-06-20
created: 2026-06-21
description: "Twelve models worth knowing in 2026, each with one standout strength."
tags:
  - "brain_spew"
---
## Your agents are still missing the context they need (Sponsored)

![](https://substackcdn.com/image/fetch/$s_!C9g-!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fed136b2a-d0ff-46a1-ae2a-e6744c493ae4_1600x840.png)

AI shows up in 60% of engineering work. But only about a fifth of it can be handed off without someone babysitting the output. That’s because agents are missing context.

This 8-stage context maturity model gives a real answer on why you still get inconsistent output for all the tokens burned.

[Join Unblocked live on June 24 (FREE)](https://go.bytebytego.com/Unblocked_062026) to learn:

- Why more MCPs provides agents access but not understanding
- What it takes to deploy agents you can trust without supervision
- How a context layer solves for quality, efficiency and cost

---

This week’s system design refresher:

- Claude Fable 5: Everything You Need to Know! (Youtube video)
- 12 Open-source LLMs
- SLMs vs. LLMs, Clearly Explained
- Single Agent vs. Multi-Agent Architecture
- 7 Permission Modes Every Claude Code User Should Know

---

## Claude Fable 5: Everything You Need to Know!

![](https://www.youtube.com/watch?v=-H6Q97_9cKY)

---

## 12 Open-source LLMs

![Image](https://substackcdn.com/image/fetch/$s_!BYbF!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F220c32aa-4313-4278-ae43-4d2d1b5b8875_2508x3000.png)

Twelve models worth knowing in 2026, each with one standout strength.

1. Llama 4 Scout: Meta's first natively multimodal open-weight model.
2. DeepSeek V4: A Mixture-of-Experts model under MIT license with a native million-token context window. Near-frontier performance at a fraction of the cost per token.
3. Qwen3: Alibaba's flagship open-weight model with switchable thinking and non-thinking modes, all under Apache 2.0.
4. Gemma 4: Google's open-weight family released under Apache 2.0, with the widest language coverage of any model on this list.
5. Phi 4: Microsoft’s compact model trained almost entirely on synthetic, curated data. A practical choice for edge and on-device deployment.
6. Mistral Small 3.1: A VLM with a long context window that fits on a consumer laptop.
7. Nemotron 3 Super: NVIDIA’s hybrid MoE with a million-token context window. Fully open weights, datasets, and recipes, with strong results on agentic coding benchmarks.
8. GLM 5.1: The first open-weight model to top SWE-Bench Pro. Released under MIT with no commercial restrictions.
9. Kimi K2.6: Competitive with leading closed models on coding while costing far less per million tokens. Available on Hugging Face under a Modified MIT license.
10. StarCoder2: One of the most transparent code models available.
11. OLMo 2 (AI2): The most complete example of open-source reproducibility on this list. Weights, training data, code, and full recipes all released under Apache 2.0.
12. Falcon 3: A family of lightweight open-weight models built to run on a single GPU.

Over to you: which open-source model would you add to this list?

---

## FeatureOps Summit 2026 - Feature management in the AI Era (Sponsored)

![](https://substackcdn.com/image/fetch/$s_!Cdnl!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa538c4d4-b3be-401d-b3d0-948593dbcd5f_3200x1680.png)

Speed without control is a false economy. As AI code-generation accelerates software delivery, the FeatureOps Summit 2026 is here to ensure that when we ship more, we break less.This premier virtual event brings together engineers, architects, and product leaders from companies like Samsung, Lloyds Banking Group, Wayfair, Visa, AWS, Allianz and many others, to explore the infrastructure of fearless delivery.

**Key Themes:**

- **AI Safety Nets:** Guardrails for the flood of automated code.
- **Edge Resilience:** Sub-millisecond evaluation at scale.
- **Continuous Flow:** Moving past the “fixed-release” mindset. Register today to master the tools and patterns required for a fail-safe release environment.

---

## SLMs vs. LLMs, Clearly Explained

![](https://substackcdn.com/image/fetch/$s_!HMwY!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6af9e24b-9be2-4a45-9f81-14ec6f4330ca_2484x3002.png)

Big models cost more. Small models do less. Here's how SLMs and LLMs differ across the dimensions that matter in production:

1. Architecture: SLMs are usually under 10B parameters and run on a laptop or phone. LLMs sit at 10B+ with deeper layers and more attention heads, built for broad reasoning across tasks.
2. Task Complexity: SLMs work well on simple tasks but fail on complex multiple reasoning steps. LLMs handle difficult math, multi-step code, and long-horizon planning.
3. Long Context Recall: SLMs lose the thread across long documents or extended conversations. LLMs reliably track and connect information across large inputs.
4. Latency and Cost: SLMs run on consumer hardware with low response times and significantly lower inference costs. LLMs require GPU and carry higher costs per request.
5. Deployment and Privacy: SLMs run on-device or on-premise. LLMs are typically cloud-hosted, which adds data governance complexity.
6. Where each fits:  
	SLMs: on-device assistants, real-time classification, or privacy-sensitive applications  
	LLMs: complex reasoning, agent workflows, or broad knowledge tasks.

Are you using SLMs, LLMs, or a hybrid setup in production?

---

## Single Agent vs. Multi-Agent Architecture

Some tasks need a single agent. Others need a whole team. Knowing the difference is the skill.

![Image](https://substackcdn.com/image/fetch/$s_!Z5zI!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5233378c-3c59-40b1-9de2-6515b9d3e928_2484x3002.png)

Single-agent system: One reasoning LLM that plans, picks a tool, and loops on its own until the task is done. Use a single agent when:

- the task is a clear, linear sequence
- one agent can hold the whole problem in its head
- you want something simple to build and easy to debug

Multi-agent system: An orchestrator that splits a task into subtasks and routes each one to a specialized agent. Use multi-agent when:

- subtasks can run in parallel
- one agent writes and another independently verifies the work
- the problem is too big for one agent to coordinate alone

Single agents are cheaper and easier to build, but they hit a ceiling on complex work.

Multi-agent systems are more capable and more reliable, but they add coordination cost.

Start with a single agent. Move to multi-agent only when context or reliability become the bottleneck.

Over to you: Are you running single-agent or multi-agent systems in production?

---

## 7 Permission Modes Every Claude Code User Should Know

![](https://substackcdn.com/image/fetch/$s_!U8C6!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1b849efb-0467-4a5d-b735-f2296b125e9f_2484x3002.png)

1. plan: The model drafts a plan. Nothing executes until the user approves.
2. default: Standard interactive use. Most tool calls require user approval.
3. acceptEdits: Edits in the working directory are auto-approved. Other shell commands still prompt.
4. auto: An ML classifier decides on requests that miss the fast path.
5. dontAsk: No prompts shown. Deny rules are still enforced.
6. bypassPermissions: Most prompts are skipped. Safety-critical guards still apply.
7. bubble: A subagent escalates its permission request to the parent.

Only 5 modes are user-selectable. “auto” is gated by a feature flag, and “bubble” is internal.

Over to you: Which mode do you reach for most, and what made you pick it?