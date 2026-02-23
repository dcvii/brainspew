---
title: "Before You Go Model Shopping: A Guide to Understanding What You Actually Need"
source: "https://promptkit.natebjones.com/20260221_l1e_guide_main"
author:
published:
created: 2026-02-23
description:
tags:
  - "clippings"
---
---

The post laid out why models are different now. Gemini 3.1 Pro reasons harder. Opus 4.6 works longer and uses tools better. Codex 5.3 codes faster in its lane. Six axes of difficulty. A landscape that's finally differentiated enough to reward specificity.

And I know exactly what some of you are about to do with that information. You're going to open four new tabs, sign up for two more AI subscriptions, and spend the next three weeks bouncing between models trying to figure out which one is "best." You'll end up overwhelmed, behind on actual work, and no closer to using any of them well.

I've watched this happen. I've done it myself.

So before you go model shopping, let's do something more useful. Let's figure out what you actually need — and whether the tool you already have can do it.

---

## The Real Problem

Here's what I've learned working with hundreds of people on AI adoption: the bottleneck is almost never the model. It's the person's understanding of what they're asking the model to do.

Most people describe their work in terms of tasks. "I write reports." "I manage projects." "I review contracts." "I build presentations." That's fine for a job description. It's useless for figuring out how AI can help you.

Why? Because a single task — "prepare a board presentation" — might involve four completely different kinds of difficulty. The financial modeling is a reasoning problem. Gathering data from twelve sources is an effort problem. Getting input from five departments is a coordination problem. Figuring out what the board actually cares about is an ambiguity problem. Each one responds to AI differently. Each one requires a different approach, different prompting, different expectations.

If you don't decompose the task, you'll throw the whole thing at your AI tool, get mediocre results, and conclude the tool isn't good enough. Then you'll try another tool. Same mediocre results. Repeat until frustrated.

The tool wasn't the problem. The ask was.

---

## Step 1: Pick One Task

Not your whole job. Not your role. One task.

Pick something you do regularly — at least weekly. Something that takes real time or energy. Something where you've thought "AI should be able to help with this" but haven't cracked it yet, or where you're using AI but the results feel inconsistent.

Write it down in one sentence. Keep it specific.

**Too vague:** "Do research"

**Better:** "Compile competitive intelligence on three rivals before our quarterly strategy meeting"

**Too vague:** "Write content"

**Better:** "Draft the weekly project status update that goes to the executive team"

**Too vague:** "Analyze data"

**Better:** "Review last month's customer churn data and identify the top three patterns driving cancellations"

One task. That's it. Everything else in this guide flows from this single choice.

---

## Step 2: Decompose It

Now pull that task apart across the six axes from the post. For each one, give yourself an honest rating: **None**, **Some**, or **This Is the Hard Part**.

Here's what you're looking for:

**Reasoning** — Does this task require genuine multi-step logical deduction? Working through chains of cause and effect? Holding multiple variables in tension and arriving at a conclusion that isn't obvious from the surface? If you took away all the other friction and just had to think through the core problem, would the thinking itself be hard?

**Effort** — Is this task hard mostly because it's big? Lots of inputs to process, lots of documents to review, lots of data to organize? Would a competent person be able to handle any individual piece without difficulty — the challenge is just doing all of it thoroughly without dropping things?

**Coordination** — Does this task require getting information, input, alignment, or approval from multiple people or teams? Is the difficulty less about the work itself and more about navigating dependencies, conflicting priorities, or information that lives in other people's heads?

**Emotional Intelligence** — Does this task involve reading people, managing relationships, calibrating tone, navigating politics, or handling sensitive dynamics? Is part of the difficulty knowing not just what to say but how and when to say it?

**Domain Expertise** — Does this task require knowledge that comes from years of experience in your specific field? Not general reasoning ability — specific pattern recognition, tacit knowledge, the kind of thing you know because you've seen it a hundred times before?

**Ambiguity** — Is the hardest part of this task figuring out what the actual question is? Are you dealing with incomplete information, conflicting signals, or a situation where multiple interpretations are plausible and you have to make a judgment call about which one to pursue?

Write down your ratings. Be honest. Most people overestimate the reasoning component and underestimate the ambiguity and coordination components.

Let me be concrete. Here's what this might look like for our "competitive intelligence" example:

- **Reasoning:** Some — comparing strategic positions requires analytical thinking, but it's not novel multi-step deduction.
- **Effort:** This Is the Hard Part — pulling data from earnings calls, press releases, product announcements, industry reports, job postings, patent filings. The sheer volume is the bottleneck.
- **Coordination:** Some — need input from sales on what they're hearing and from product on which features matter.
- **Emotional Intelligence:** None for this task.
- **Domain Expertise:** Some — need to know what matters in your industry to filter signal from noise.
- **Ambiguity:** Some — competitors don't announce their strategy. You're reading tea leaves.

Look at that breakdown. If you threw this whole task at any AI model with the prompt "do competitive intelligence on my three main competitors," you'd get slop. Not because the model is bad — because the prompt treats a multi-axis problem as a single-axis one.

But now you can see the shape of it. The hard part is effort. Which means you need to think about how to use AI for systematic information gathering and synthesis — not for strategic brilliance.

That changes everything about how you approach it.

---

## Step 3: Pressure-Test Your Current Tool

This is where most people skip straight to model shopping. Don't.

Whatever tool you're using right now — Claude, ChatGPT, Gemini, whatever — you are almost certainly underusing it for the specific kind of difficulty you just identified. Not because you're bad at AI. Because you haven't had a reason to think about it this way before.

Here's what to try, based on which axis is your primary bottleneck:

**If your bottleneck is Effort:**You need to think about breaking the task into systematic sub-steps and letting AI grind through them. Most modern models can handle large context windows, process long documents, and sustain work across extended conversations. Are you actually using that? Or are you giving the model a single prompt and expecting magic?

Try: Break the task into its component parts. Feed each part to the model separately with clear instructions. Use the model to process, organize, and synthesize — the work nobody wants to do but everybody needs done. The goal isn't creative output. It's thoroughness at scale.

**If your bottleneck is Reasoning:**You need to give the model room to think and the constraints to think well. Are you providing enough context for the model to reason from? Are you defining what a good answer looks like? Are you letting it work through the problem step by step, or expecting the answer in a single shot?

Try: Give the model the full context of the problem, including the variables and constraints. Ask it to reason through the problem explicitly before giving you a conclusion. Then stress-test the reasoning — ask it to identify where its own logic might be wrong. You'd be surprised how often the model you already have can handle the reasoning if you structure the prompt to let it.

**If your bottleneck is Ambiguity:**AI is your thinking partner here, not your answer machine. The model won't resolve your ambiguity. But it can help you map it. It can generate multiple interpretations, explore the implications of each one, and help you see the decision landscape more clearly.

Try: Describe the ambiguous situation and ask the model to generate three to five distinct interpretations of what's going on. For each one, have it map the implications. You're not looking for the answer. You're looking for better questions. Let the model help you see what you might be missing.

**If your bottleneck is Domain Expertise:**This is where you need to be careful. The model can simulate domain knowledge from training data, but it doesn't know what it doesn't know — and neither do you when you're outside your own expertise. Use AI to augment your domain knowledge, not replace it.

Try: Use the model as a research partner. Ask it to identify considerations you might be missing, surface relevant frameworks, or challenge your assumptions with counter-evidence. But validate anything that matters against your own experience or trusted sources. The model is useful here for breadth. Depth is still yours.

**If your bottleneck is Coordination:**This is mostly a human problem. AI can help with the artifacts of coordination — drafting communications, summarizing decisions, tracking dependencies, preparing people for meetings — but it can't navigate the politics or build the relationships. Be honest about what you're actually asking for.

Try: Use AI to draft the coordination artifacts. The status update that aligns six teams. The meeting prep document that gives everyone context. The summary email that captures decisions and action items. These are high-effort, high-value communication tasks that AI handles well — and getting them done faster frees you up for the actual coordination work that only you can do.

**If your bottleneck is Emotional Intelligence:**AI won't help with the hard part — reading the room, calibrating trust, knowing when to push and when to back off. But it can help you prepare and process. You can use it to think through scenarios, draft difficult conversations, pressure-test your approach, or debrief after a tough interaction.

Try: Describe the situation and ask the model to help you think through it. What are the other person's likely concerns? What might they be reacting to that they haven't said? What are three ways this conversation could go, and how would you navigate each one? Use AI as a rehearsal space, not a replacement for judgment.

---

## Step 4: Find the Real Gap

You've decomposed the task. You've tried using your current tool with the right approach for the right axis. Now — and only now — ask honestly: is there something my current tool genuinely can't do here?

Maybe there is. If your primary bottleneck is sustained autonomous work over hours — processing thousands of documents, running code across multiple files, managing complex multi-step workflows without you babysitting every step — you might need an agentic model that's purpose-built for that. If you're hitting a wall on genuine novel reasoning at the scientific or mathematical frontier, a model optimized for deep thinking might make a real difference.

But notice how specific that question is now. You're not asking "which AI is best." You're asking "I need a tool that can sustain effort across a large surface area with minimal supervision" or "I need a tool that can reason through multi-step logical deductions in tax law." That specificity means you know exactly what you're looking for, exactly what to test for, and exactly how to tell whether the new tool is actually better for your problem or just different.

Most of the time, though, you'll find something else: the gap isn't the tool. The gap is in how you're framing the task, structuring the context, or setting expectations for output. That's the real win of this exercise. Not a model recommendation — a clearer understanding of what you're asking for and how to ask for it.

---

## Step 5: Repeat

Pick another task. Run it through the same process.

Over time, you'll build something the post called a "routing map" — but it won't be a spreadsheet matching models to tasks. It'll be an intuition. You'll start to feel the shape of a problem before you even open your AI tool. You'll know when you're dealing with an effort task that needs systematic grinding versus a reasoning task that needs room to think versus an ambiguity task that needs exploration, not answers.

That intuition is worth more than any model subscription. Because models change every quarter. The ability to decompose a problem and match it to the right approach — that compounds.

And here's the thing: by the time you've done this for five or six tasks, you'll know whether you actually need a different tool or not. You won't be guessing. You won't be chasing announcements. You'll know because you'll have specific, concrete evidence — "my tool handles my effort tasks and reasoning tasks well, but I keep hitting a wall when I need sustained autonomous coding across multiple files." That's a real gap. That's worth acting on.

Everything else is noise.

---

## The Honest Truth

The AI landscape is moving fast enough that keeping up with one tool is a full-time project. Every week brings new features, new capabilities, new things your existing tool can do that it couldn't do last month. The people who are getting the most value from AI right now aren't the ones using five tools. They're the ones who understand one tool deeply and know exactly what to ask of it.

The post showed you that models are built for different kinds of hard. That's true and important. But the actionable insight isn't "go subscribe to everything." It's the opposite: understand your work well enough to know what kind of hard you're dealing with, get specific about what you need, and squeeze everything you can out of what you have before you go looking for more.

You might discover you need Gemini's reasoning depth for a specific quarterly analysis. You might discover Opus's agentic mode unlocks a workflow that was eating three hours of your week. Great. Now you're making a decision based on evidence, not hype.

Or you might discover — and this is more common than anyone wants to admit — that you've been sitting on top of a tool that can already do most of what you need. You just hadn't asked it the right way.

Start with one task. Decompose it. Pressure-test your current tool. Find the real gap, if there is one.

That's the work. And it's more valuable than any model comparison.