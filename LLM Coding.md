---
title: "Thread by @esrtweet"
source: "https://x.com/home"
author:
  - "[[@esrtweet]]"
published: 2026-01-29
created: 2026-01-29
description:
tags:
  - "clippings"
---
**Eric S. Raymond** @esrtweet [2026-01-29](https://x.com/esrtweet/status/2016849708254179501)

Things That Puzzle Me, item #4632: why is there such a huge variance in results from using LLM assistance for programming?

For me, it has been dead easy and I've gotten spectacularly positive results basically from day one. There was the usual minor friction of learning new tools, but it was certainly easier than (say) learning a new programming language.

The only really new working method I had to wrap my head around was always maintaining a spec document that I write my design thoughts into as I have them, so the LLM can load that into its context.

I'm not seeing a high error rate in generated code, either.

And yet, others report being lost In a wilderness of LLM hallucinations, crappy generated code, and failure to get a real grip on their problem domain.

I have no idea what's going on here.

The obvious theory would be that LLMs reward super-competence in programmers using them and I'm super-competent. This is a seductive idea because it feels good, and because...er, well, there are other lines of evidence suggesting that I am in fact a super-competent programmer.

Besides the fact that I'm automatically suspicious of any explanation that feels that good, this one founders on the fact that I've heard many reports of failure and frustration from people who don't seem to be incompetent.

So, um, what's going on here? What possibilities can we eliminate?

It's probably not the case that I'm having low friction because the problems I work on are simple. I gravitate towards problems with high algorithmic complexity and complex data structures, because I have mathematician brain and that's what mathematician brain likes to chew on.

Anyway, I do frequently write simple tools to assist my complex projects (like my most recent new project, a batch mode spell checker for documentation in software source trees), and I don't notice that the LLMs are any better at the simple code or any worse at the complex stuff.

It's not the LLMs or LLM tools I'm using because I'm using the same ones as lots of other people. Currently ChatGPT 5.2 via Codex. I'm not doing the fancy stuff like agent flocks yet because I haven't yet seen a need to.

I've considered the theory that the key variable is the ability to write clearly in English. Again, this would be an easy feel-good explanation for me, as I've done several successful books and a New York Times bestseller; for this very reason I distrust it.

I think being able to write clear high-quality prose to LLMs used to be more important than it is now. I notice that my prompts have been getting shorter and less explicit without a fall-off in the quality of my results, and I think that's the models getting better at correctly interpreting ambiguous instructions.

One possibility I haven't eliminated is that LLMs reward system-architect skill, having good intuition and taste about design. I know some very capable programmers that don't have this; they can do routine work and maintenance and debugging, but don't originate projects and don't thrive if you ask them to design in areas where they don't have established practice and a lot of precedent to fall back on.

It's not easy to tell from a distance who has system-architect skill and who doesn't. Well, except that the design leads of successful major projects pretty much have to have at least some of it, or the projects couldn't succeed. Because I can't tell who has it, I can't judge that people constantly having bad interactions with LLMs don't have it.

The main problem with this theory is elsewhere; that I can't figure out how system-architect skill could translate to behaviors that are visible to an LLM through its text stream input.

So, none of the possibilities I've considered are persuasive. I continue to be puzzled.