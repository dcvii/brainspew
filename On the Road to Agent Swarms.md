---
title: "On the Road to Agent Swarms"
source: "https://juhache.substack.com/p/on-the-road-to-agent-swarms"
author:
  - "[[Julien Hurault]]"
published: 2026-01-23
created: 2026-01-25
description: "Ju Data Engineering Weekly - Ep 94"
tags:
  - "clippings"
---
### Ju Data Engineering Weekly - Ep 94

I wrote about my agent workflow struggles in last week’s newsletter:

I found myself trapped in a constant back-and-forth, acting as a manual bridge between different agents.

I felt less like a developer and more like a manager micromanaging engineers.

And I don’t like it.

It got me obsessed with a single question: how do I scale my agent usage?

I don’t want to manage 1–5 agents in parallel; I want to manage 20 or 30.

Last Sunday, I came across Steve Yegge’s *[GasTown](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04)* Medium post from early January.

I remembered reading it before, but it didn’t click at the time.

This time, I got that “aha” moment (writing last week’s post probably helped it land).

So I went down a rabbit hole to understand how the craziest vibe coders on the planet are leveraging coding agents.

By the end of the month, I want to have good “agent swarm” infra in place—enough to run 20–30 sessions in parallel.

In this post, I share what I added to my stack this week and my first exploration of agent orchestration tools.

If you still need convincing, try watching this:

<iframe src="https://www.youtube-nocookie.com/embed/zuJyJP517Uw?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen="true" width="728" height="409"></iframe>

## What happened this week

### I ditched my IDE

Yeah, I never thought that would happen…

I almost didn’t open VS Code (or Cursor) this week.

I run everything in tmux now and can jump super easily across sessions.

![](https://substackcdn.com/image/fetch/$s_!Wunu!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0f72e3f1-5a3e-4b73-85ee-ceabd0279edc_3438x934.png)

I split each session into panes and windows, which makes it really easy to run several Claude Code sessions in parallel.

How do I check code? nvim + Neo-tree.

![](https://substackcdn.com/image/fetch/$s_!w47R!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d1a5a67-e359-436f-ae86-772aa624c149_2292x2166.png)

I feel likea true coder now… but I don’t write any code:)

How do I check diffs? directly in GitHub.

## Beads in the mix

As I mentioned in my last post, I was struggling to coordinate multiple agents working on the same problem—each tackling sub-stories in parallel.

I started using Beads, and it works pretty well.

(So well, in fact, that Anthropic seems to have incorporated it directly into Claude Code yesterday.)

![](https://substackcdn.com/image/fetch/$s_!PFQa!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff38bc8d3-4fc3-467b-8c34-4fd4caddee4e_784x1052.png)

Now I plan first: a quick back-and-forth with an agent until we land on a solid plan using [OpenSpec](https://github.com/Fission-AI/OpenSpec).

Once the specs are ready, I ask my planning agent to transcribe them into Beads, then let it do 3 back-and-forth rounds with Codex via the Codex CLI.

Stories are linked in a DAG, so Claude Code can then spin up x sub-agents.

![](https://substackcdn.com/image/fetch/$s_!JGAu!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6d085afb-a4c5-495e-859b-2a2f693d983f_912x560.png)

With this setup, I’ve been able to run 5–10 sessions in parallel.

And honestly, it’s been working pretty well—but I still need to jump in too often:

Things aren’t properly tested.

Simple bugs go through.

Simple architecture decisions aren’t made.

And these stupid permission requests… Speaking of witch:

### Sandboxing: no clean solution

I tested the sandboxing solution in Claude Code, but it was too restrictive—for example, the agent couldn’t access localhost.

So I ended up using the --allow-dangerously-skip-permissions flag.

It works great, but it doesn’t feel very… safe.

Any tips?

### Browser Interaction

I started to use [broser-agent](https://github.com/vercel-labs/agent-browser) from Vercel and it’s really good, much faster than claude code chrome feature.

## Next Week, Next Level

Next week, I want to take this setup to the next level.

To do that, I looked into a few agent orchestration frameworks:

\- [multiclaude](https://github.com/dlorenc/multiclaude) (312 ⭐)

\- [GasTown](https://github.com/steveyegge/gastown) (5.2k ⭐)

\- [claude-flow](https://github.com/ruvnet/claude-flow) (12.6k ⭐)

I don’t want to describe them in detail in this post but instead understand how they solve these problems:

- Coordination
- Parallel Execution
- Merging

Let’s go!

## Coordination & Task Tracking

All three projects follow a similar approach: one agent has a dedicated planning role—it pulls the current open tasks and assigns them.

**Multiclaude**

![](https://substackcdn.com/image/fetch/$s_!tSV_!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe8784cb9-ab75-4cee-8762-9bd27a56e414_992x610.png)

Agents communicate by writing messages to files.

The planner drops tasks into each worker’s folder. A daemon prompts workers to check for new tasks; they execute them and write results back.

No fancy tools—just files and polling.

**GasTown**

![](https://substackcdn.com/image/fetch/$s_!r6cM!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01abc09f-9a24-4307-b46f-fc5c78e897cb_966x470.png)

Agents exchange messages and do not get polluted by others

GasTown uses a dedicated MCP mail system.

Each agent gets a mailbox and can send/receive messages via that MCP mailbox.

GasTown uses this for all communication:

- Agent starts → a hook reads the inbox → picks up work.
- Done → the agent updates the inbox.

Agents don’t talk to each other directly—only via mail—so each agent’s context stays clean and doesn’t get polluted.

**Claude-Flow**

Claude-flow, on the other end of the spectrum, is more complex:

No files, no mail—everything is coordinated in memory by a hierarchy of planner agents.

A strategic planner breaks work down into tasks, and a router assigns each one to the best worker, learning over time which agent type performs best.

Workers claim tasks from a shared registry. If an agent dies, the task is released and picked up by another worker.

## Parallel Execution & Isolation

20 agents touching the same codebase = chaos.

Multiclaude and GasTown avoid that by leaning on Git worktrees.

For each feature, the planning agent:

- creates a worktree in a central location (e.g., ~/.multiclaude/ or ~/gt/)
- creates a dedicated tmux session

Claude-flow takes a different approach:

No worktrees—just a shared codebase, where agents claim tasks.

A claim means: “I’m working on this, don’t touch it.”

If an agent dies, the claim is released and another agent can pick the task up.

## Diff Merging

20 agents = 20 branches.

How do changes land in main?

This “merge wall” gets brutal at 20+ parallel workers: every merge shifts the baseline, and later PRs end up targeting code that’s already changed.

**Multiclaude**

The Multiclaude philosophy puts CI front and center.

If it passes, the code goes in—and the next PRs need to adapt.

The resolution workflow looks like this:

![](https://substackcdn.com/image/fetch/$s_!QAJG!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F69b89e9e-b55c-4712-9319-52f4f7d07861_990x460.png)

The daemon regularly asks the planner to check PR status.

If it detects a failing PR, the planner assigns the fix to the original worker.

**GasTown**

GasTown, on its end, leverages Beads queues.

Each time a worker finishes, it pushes to GitHub and adds a new message to the review queue.

A dedicated agent, running in its own worktree, polls the review queue, merges PRs that can be merged, and sends a message to the planning agent if conflicts occur.

The planning agent then asks the initial worker to resolve them.

![](https://substackcdn.com/image/fetch/$s_!mPCo!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F679b0689-415b-4de6-9213-d68be222f2c8_998x508.png)

Claude-flow takes a different approach: no branches, no worktrees, just a shared codebase coordinated through task claims.

Agents claim work to avoid conflicts, propose changes, and rely on a consensus mechanism—rather than Git—to decide what gets merged.

---

I have limited experience with these frameworks so far, but it’s interesting to see where the real problems are—and how they’re being solved today.

Some solutions might be over-complexified, but they still offer a lot of ideas you can borrow and implement in your own workflows.

One thing is clear: agents need to communicate with each other, especially for conflict resolution.

That’s a key piece, and I really like the mail MCP approach. It’s an elegant solution that could scale to team collaboration as well. If one developer has 20 agents working on a repo, then a team of 5 has ~100 agents on the same codebase… that’s a *lot* of conflicts to resolve 😅

Within a few months, Claude Code and Codex will probably integrate these patterns natively, hiding most of the complexity from the user.

What I’m less sure about is whether they’ll allow orchestration across providers—which I think has a lot of value, for example:

- easy tasks for OSS models
- hard tasks for Codex
- regular implementation work for Claude Code

Finally, all of this is currently centered around pure software engineering.

But in the data world, what does it mean to have dozens of agents running in parallel?

I see only one way: truly adopt git-for-data approaches across the stack and properly isolate agents.

---

Thanks for reading,

\-Ju

![](https://substackcdn.com/image/fetch/$s_!RKXu!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F74b337d0-6c9a-4476-8eef-127b3abd5485_300x300.png)