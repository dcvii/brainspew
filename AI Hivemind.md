---
title: Thread by @alex_prompter
source: https://x.com/alex_prompter/status/2031395606644896100
author:
  - "[[@alex_prompter]]"
published: 2026-03-10
created: 2026-03-11
description:
tags:
  - brain_spew
  - AI_Skeptic
---
**Alex Prompter** @alex\_prompter [2026-03-10](https://x.com/alex_prompter/status/2031395606644896100)

🚨 BREAKING: Researchers at UW Allen School and Stanford just ran the largest study ever on AI creative diversity.

70+ AI models were given the same open-ended questions. They all gave the same answers.

They asked over 70 different LLMs the exact same open-ended questions.

"Write a poem about time." "Suggest startup ideas." "Give me life advice."

Questions where there is no single right answer. Questions where 10 different humans would give you 10 completely different responses.

Instead, 70+ models from every major AI company converged on almost identical outputs. Different architectures. Different training data. Different companies. Same ideas. Same structures. Same metaphors.

They named this phenomenon the "Artificial Hivemind." And the paper won the NeurIPS 2025 Best Paper Award, which is the highest recognition in AI research, handed to a small number of papers out of thousands of submissions.

This is not a blog post or a hot take. This is award-winning, peer-reviewed science confirming something massive is broken.

The team built a dataset called Infinity-Chat with 26,000 real-world, open-ended queries and over 31,000 human preference annotations. Not toy benchmarks. Not math problems.

Real questions people actually ask chatbots every single day, organized into 6 categories and 17 subcategories covering creative writing, brainstorming, speculative scenarios, and more.

They ran all of these across 70+ open and closed-source models and measured the diversity of what came back. Two findings hit hard.

First, intra-model repetition. Ask the same model the same open-ended question five times and you get almost the same answer five times.

The "creativity" you think you're getting is the same output wearing a slightly different outfit. You ask ChatGPT, Claude, or Gemini to write you a poem about time and you keep getting the same river metaphor, the same hourglass imagery, the same reflection on mortality.

Over and over. The model isn't thinking. It's defaulting to whatever scored highest during alignment training.

Second, and this is the one that should really alarm you, inter-model homogeneity. Ask GPT, Claude, Gemini, DeepSeek, Qwen, Llama, and dozens of other models the same creative question, and they all converge on strikingly similar responses.

These are models built by completely different companies with different architectures and different training pipelines.

They should be producing wildly different outputs. They're not. 70+ models all thinking inside the same invisible box, producing the same safe, consensus-approved content that blends together into one indistinguishable voice.

So why is this happening? The researchers point directly at RLHF and current alignment techniques. The process we use to make AI "helpful and harmless" is also making it generic and boring.

When every model gets trained to optimize for human preference scores, and those preference datasets converge on a narrow definition of what "good" looks like, every model learns to produce the same safe, agreeable output. The weird answers get penalized.

The original takes get shaved off. The genuinely creative responses get killed during training because they didn't match what the average annotator rated highly. And it gets even worse.

The study found that reward models and LLM-as-judge systems are actively miscalibrated when evaluating diverse outputs. When a response is genuinely different from the mainstream but still high quality, these automated systems rate it LOWER. The very tools we built to evaluate AI quality are punishing originality and rewarding sameness.

Think about what this means if you use AI for brainstorming, content creation, business strategy, or literally any task where you need multiple perspectives. You're getting the illusion of diversity, not the real thing.

You ask for 10 startup ideas and you get 10 variations of the same 3 ideas the model learned were "safe" during training. You ask for creative writing and you get the same therapeutic, perfectly balanced, utterly forgettable tone that every other model gives.

The researchers flagged direct implications for AI in science, medicine, education, and decision support, all domains where diverse reasoning is not a nice-to-have but a requirement.

Correlated errors across models means if one AI gets something wrong, they might ALL get it wrong the same way. Shared blind spots at massive scale.

And the long-term risk is even scarier. If billions of people interact with AI systems that all think identically, and those interactions shape how people write, brainstorm, and make decisions every day, we risk a slow, invisible homogenization of human thought itself. Not because AI replaced creativity.

Because it quietly narrowed what we were exposed to until we all started thinking the same way too.

Here's what you can actually do about it right now:

→ Stop accepting first-draft AI output as creative or diverse. If you need 10 ideas, generate 30 and throw away the obvious ones

→ Use temperature and sampling parameters aggressively to push models out of their comfort zone

→ Cross-reference multiple models AND multiple prompting strategies, because same model with different prompts often beats different models with the same prompt

→ Add constraints that force novelty like "give me ideas that a traditional investor would hate" instead of "give me creative ideas"

→ Use structured prompting techniques like Verbalized Sampling to force the model to explore low-probability outputs instead of defaulting to consensus

→ Layer your own taste and judgment on top of everything AI gives you. The model gets you raw material. Your weirdness and experience make it original

This paper puts hard data behind something a lot of us have been feeling for a while. AI is getting more capable and more homogeneous at the same time.

The models are smarter, but they're all smart in the exact same way. The Artificial Hivemind is not a bug in one model. It's a systemic feature of how the entire industry builds, aligns, and evaluates language models right now.

The fix requires rethinking alignment itself, moving toward what the researchers call "pluralistic alignment" where models get rewarded for producing diverse distributions of valid answers instead of collapsing to a single consensus mode.

Until that happens, your best defense is awareness and better prompting.

![Image](https://pbs.twimg.com/media/HDD3iZ3a0AAY9Ku?format=jpg&name=large)