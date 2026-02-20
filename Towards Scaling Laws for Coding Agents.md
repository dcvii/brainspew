---
title: "Towards Scaling Laws for Coding Agents"
source: "https://vizops.ai/blog/agent-scaling-laws/"
author:
  - "[[Pushpendre Rastogi]]"
published: 2026-02-09
created: 2026-02-19
description: "We reverse-engineered the scaffolding behind Anthropic's Claude-built C compiler and ran our own experiments to explore scaling laws for parallel coding agents."
tags:
  - "clippings"
---
[Back to Blog](https://vizops.ai/blog)

ai-agents scaling-laws coding-agents claude-code

![Pushpendre Rastogi](https://vizops.ai/assets/team/pushpendre.jpg)

Pushpendre Rastogi

CTO & Co-Founder

February 8, 2026

6 min read

Share:

![Towards Scaling Laws for Coding Agents](https://vizops.ai/assets/blog/agent-scaling-laws/image1.png)

Anthropic recently [demonstrated](https://www.anthropic.com/engineering/building-c-compiler) that claude-code with parallel agents can build a C compiler in Rust from scratch in just 14 days. The headline numbers are attention-grabbing — roughly **200,000 lines** of code, capable of compiling the Linux kernel and other software like Doom and postgres!

I immediately paid attention to this article since [Nicholas Carlini](https://en.wikipedia.org/wiki/Nicholas_Carlini) was the author on the blog. He is well-known in AI red-teaming, and adversarial attacks. And from my past interactions with him at Google DeepMind, I know how strong a researcher he is.

Usually for human developed code a lot of design decisions for why something was done is tribal knowledge so it's not really possible to figure out "Why" something was done? Fortunately however the [way this code was developed](https://github.com/anthropics/claudes-c-compiler) makes it possible to do something rare: **code archaeology**. Because of the meticulous book-keeping of ideas and tasks by the agents, it was entirely possible to analyze how the system evolved, decision by decision, layer-by-layer. By analyzing the full commit history we were able to model the scaffolding that was used to generate the repository and do some simple analysis of scaling laws for parallel claude-code agents.

---

## 1\. Code Archaeology

Our first task was to understand how the 16 agents interacted to evolve the code for the compiler over time. To do so it helps to visualize how the code evolved over time. My first step was to create a time-lapse video of the entire 14-day development window, visualizing commit density, active agents, and subsystem focus. You can see the video here:

**Time-lapse video:**[https://youtu.be/c9P89fe4WQk](https://youtu.be/c9P89fe4WQk)

The full code and the original interactive HTML is also available at [https://github.com/pushpendre/claudes-c-compiler](https://github.com/pushpendre/claudes-c-compiler)

Some interesting takeaways from this visualization are that within the first 4 hours, the LLM had already written the first 10K lines of code focusing almost exclusively on the parser. Borrowing an analogy from chess, it felt like the LLM was blitzing through well known theory.

Even though the video is good to get a sense of what was going on, unfortunately, it's too quick and not "information dense" enough. The following graph does a much better job of conveying a lot of information. This graph plots as a function of time: a) the test pass rate for different tests suites, b) The number of commits and the lines of code, and c) The number of commits per hour. It also marks the times where the tasks were cleared, either manually or automatically because the progress was stagnating.

![Code archaeology timeline showing test pass rates, commit density, and lines of code over the 14-day development window](https://vizops.ai/assets/blog/agent-scaling-laws/image1.png)

Code archaeology timeline showing test pass rates, commit density, and lines of code over the 14-day development window

We can clearly see within just 24 hours the compiler was already passing 95% of tests. The progress quickly asymptoted on the tests after 2 days but curiously a lot more code was added between hours 50 and 100 (i.e. days 3 and 4). Turns out the agents were reset and tasked with improving the runtime performance of the compiler. In hours 100 to 150 the compiler was primarily bringing up the x86 backend. Hours 150 to 250 were devoted to refactoring, reducing tech debt, and optimizing generated code. Finally for hours 250 onwards the dependency on GCC's assemblers and linkers was removed.

---

## 2\. Agent Scaling Laws: Actors vs Time

Although Anthropic did not release the scaffolding for the compiler it is possible to reverse engineer it because of the meticulous note-taking by the agents which maintained the `ideas/` folder as an intake queue for proposed tasks, and the `current_tasks/` folder which listed the tasks. This information was sufficient to take a stab at reproducing the scaffolding that would have generated the compiler. We have open sourced the scaffolding code at [https://github.com/vizopsai/async\_compiler\_factory](https://github.com/vizopsai/async_compiler_factory)

In order to keep the budget low, we only ran it with one agent for 60 minutes and tested its progress on a small suite of just 18 tests. Using this scaffolding we can extrapolate some "inference time" scaling laws! For example, we can measure whether the test-pass rate improves linearly as we add more agents or if it is better to keep the number of agents low and let it work for a longer period of time.

To test the scaffolding, I ran a small test to compare the efficacy of one agent running for two hours vs two agents running for one hour and the results are below. Both of the agents were tasked with passing 16 tests that involved compiling programs like fizzbuzz, basic recursion, pointers, arrays, structs etc. The reproduced scaffolding was able to pass these tests within the first 20 minutes, and in fact one agent running longer produced more lines of code. So the jury on the utility of parallel agents is still out.

These two runs cost $153 in total. The scaffolding, the produced code, and the analysis code and plots are also open sourced and available at [https://github.com/vizopsai/async\_compiler\_factory](https://github.com/vizopsai/async_compiler_factory)

![Comparison of 1 agent running for 2 hours vs 2 agents running for 1 hour showing test pass rates and lines of code](https://vizops.ai/assets/blog/agent-scaling-laws/image2.png)

Comparison of 1 agent running for 2 hours vs 2 agents running for 1 hour showing test pass rates and lines of code

---

## Conclusion: Engineering Under Acceleration

The [software factory](https://simonwillison.net/2026/Feb/7/software-factory/) is here and it's here to stay. At the very least, the current demonstration by Anthropic can be seen as a "semantic transpiler" that receives just a 205 line long prompt, and very minimal scaffolding and is able to convert software from one language to another. This also opens up another direction for scaling laws of agents to compare the number of actors vs duration for a single actor.

One thing that becomes very clear from comparing the code that my scaffolding generated vs the commits from anthropic's C compiler is just how important the test-suite and the initial guidance is. The original CCC project had thousands of tests from the GCC torture suite, build verification for 48 real-world projects (SQLite, Redis, FFmpeg, DOOM), and a GCC oracle for differential testing during kernel compilation. Our reproduction had 16 hand-written tests. The agents passed all 16 and then spent the remaining time adding features with no feedback signal telling them whether those features actually worked. The test suite is what turned a weekend hack into a Linux-compiling compiler, and building that test infrastructure required deep domain expertise that the agents themselves do not have — at least not yet.

On parallel scaling, our experiment offers a cautionary data point. The 1-agent run reached 16/16 tests at minute 9. The 2-agent run took until minute 20 — more than twice as long — because the agents interfered with each other: one agent rewrote the AArch64 code generator that the other had just built, temporarily dropping the pass rate from 8 to 6 before recovering. The original CCC project showed the same pattern. Despite having 16 agents available, the first hour of commits was effectively single-threaded because bootstrapping a compiler from an empty repo is inherently serial. Parallelism only became useful once the test suite provided hundreds of independent failing tests that could be distributed across agents. The scaling law is not agents x time = progress. It is closer to agents x independent\_tasks\_available = progress, and the number of independent tasks is a function of the test infrastructure, not the scaffolding.

Share:

![Pushpendre Rastogi](https://vizops.ai/assets/team/pushpendre.jpg)

### About Pushpendre Rastogi

CTO & Co-Founder at VizopsAI

Senior Scientist at Google DeepMind and Amazon Alexa with PhD from Johns Hopkins. Expert in reinforcement learning, NLP, and multi-objective optimization.

Reinforcement Learning Multi-Objective Optimization Natural Language Processing Deep Learning

PhD in NLP, Johns Hopkins University | B.Tech, IIT Delhi

## Related Articles

vibe-coding security 5 min

[

### The BBC Just Proved Our Thesis: Vibe-Coded Apps Are Production Time Bombs

](https://vizops.ai/blog/bbc-proved-our-thesis-vibe-coded-time-bombs/)

A BBC reporter watched a security researcher take over her machine live on air through a vibe-coding platform. That same week, a DeFi protocol lost $1.78M to an AI-written smart contract. These aren't anomalies — they're the thesis.

Pushpak Pujari Yesterday

92

ai-agents autonomous-agents 5 min

[

### The Autonomous Build Loop Playbook: 8 Lessons From Letting AI Build an Enterprise App

](https://vizops.ai/blog/autonomous-build-loop-learnings/)

We ran 85 autonomous AI tasks to build an enterprise CLM application. Here are the 8 architectural lessons, the build loop checklist, and the 60/40 budget rule we learned the hard way.

Pushpak Pujari 5 days ago

0

ai-agents vibe-coding 5 min

[

### 19 Bugs in 2 Hours: What Happens When You Actually Try to Use Your AI-Built Enterprise App

](https://vizops.ai/blog/vibing-lessons-clm-build/)

We let an autonomous AI build an enterprise CLM app — 85 tasks, 16 hours, zero human intervention. Then I tried to log in. Here's the chronological war story of every bug I found, in order, with timestamps.

Pushpak Pujari 5 days ago

0