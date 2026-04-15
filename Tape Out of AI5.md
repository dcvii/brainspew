---
title: "Thread by @shanaka86"
source: "https://x.com/shanaka86/status/2044348592350224596"
author:
  - "[[@shanaka86]]"
published: 2026-04-15
created: 2026-04-15
description: "Nine billion miles of driving data just became a chip. Tesla AI5 is finalized for production. The design files are at Samsung in Texas and"
tags:
  - "brain_spew"
---
**Shanaka Anslem Perera** @shanaka86 [2026-04-15](https://x.com/shanaka86/status/2044348592350224596)

Nine billion miles of driving data just became a chip.

Tesla AI5 is finalized for production. The design files are at Samsung in Texas and TSMC in Arizona. The transistors are locked. There is no going back. Tape-out is the hardest gate in semiconductor engineering because everything before it is reversible and everything after it is silicon.

How this particular chip was designed is the most interesting part.

Nvidia builds general-purpose GPUs. They pack transistors into a full-reticle die, ship it with CUDA, and let customers figure out which operations matter. Blackwell B200 delivers 4.5 petaFLOPS at up to 1,000 watts. It runs any model for any customer. That generality is the moat and the tax. Every workload pays for circuits it never uses.

Tesla designed AI5 backward. They started with 9 billion miles of FSD inference data and asked one question: where does the neural network waste cycles? The answer was softmax computation and quantization precision loss. Two specific mathematical operations that consume disproportionate silicon area and power in every general-purpose GPU on Earth. Operations that Nvidia cannot optimize away because other customers need those transistors for different workloads.

Tesla hardened them. Burned custom quantization and softmax accelerator blocks directly into the die. Five times more efficient on those operations than any general-purpose equivalent. Then they added 10 times the raw compute and 9 times the memory capacity relative to AI4. The result: a single AI5 system-on-chip delivers roughly 5 times the useful compute of the current dual-chip AI4 configuration at an estimated 250 watts. Musk has framed a single AI5 as Nvidia Hopper class and dual AI5 as Blackwell class for Tesla workloads, at 3 to 5 times better power efficiency and roughly 10 times better performance per dollar.

This is not a chip designed to compete with Nvidia. This is a chip designed to run one thing: the learned differentiable physics engine that emerged from 9 billion miles of camera observation. Every transistor serves that engine. No wasted silicon. No generality tax. The neural network wrote its own hardware.

The chip goes to two foundries. Samsung in Taylor, Texas. TSMC in Arizona. Both American. Musk thanked both this morning and added: “It will be one of most produced AI chips ever.”

Samples arrive late 2026. Volume targets H2 2027. In the same post, Musk confirmed AI6, Dojo3, and “other exciting chips” are in active development. The 9-month cadence is real. AI6 targets tape-out by December. Dojo3 restarts on the unified architecture after Musk shut down Dojo2 last August as an “evolutionary dead end.” Intel joined Terafab eight days ago for advanced packaging. The $16.5 billion Samsung deal runs through 2033.

The chip that taped out this morning is not a product. It is the physical crystallization of 9 billion miles of learned physics into transistors optimized for the exact mathematical operations that physics requires. The software trained on the road. The silicon was designed from what the software learned. And the factory that will mass-produce it is being built in the same city where the cars that generated the training data roll off the line.

The loop is closed.

![Image](https://pbs.twimg.com/media/HF78NCOaYAAajG0?format=jpg&name=large)

---

**Wanderersimage** @wanderersimage [2026-04-15](https://x.com/wanderersimage/status/2044415337534570934)

Tape out is the hardest? You don’t seem to know anything about semiconductor manufacturing. I worked on EDA, photomask, FEOL (incl. litho), BEOL and advanced packaging (incl. HBI), I would say EDA (designing) is the easiest among them.

---

**Ben the Sage** @ben\_sage\_1788 [2026-04-15](https://x.com/ben_sage_1788/status/2044421168359158060)

This is a superb example of two Big Lessons from modern infotech. 1) The Real World is analog; digital infotech requires massive data and analysis to understand it reliably. 2) AI ONLY works reliably when it runs on 100% accurate data, meaning digitized Real World.

---

**Vishnu** @vishivishx [2026-04-15](https://x.com/vishivishx/status/2044419149020144041)

A humongous moment, not just for Tesla but the Semicon industry as a whole - this is the first chip that's going to be manufactured at Terafab scale

But @shanaka86 - one correction - Musk clarified later that this chip is mostly meant for Optimus & Supercomputer workloads - AI4

---

**Greg Griffing** @GregGriffing2 [2026-04-15](https://x.com/GregGriffing2/status/2044427231376851389)

So if AI5 is comparable in performance to a NVIDA H100 what does the NVIDA H100 cost per grok:

Current Purchase Prices (as of April 2026)

H100 80GB PCIe: Typically $25,000 – $31,000 per GPU. Some resellers list it around $30,970.

---

**Ben** @benrwright [2026-04-15](https://x.com/benrwright/status/2044396068545138855)

So what we are seeing is that FSD never stood a chance of working on HW4, let alone HW3. Hell, they can’t even say for sure it’ll work on AI5 as they haven’t tested it yet.