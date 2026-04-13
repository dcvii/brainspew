---
title: "On narrative programming for AI"
source: "https://aiandacademia.substack.com/p/on-narrative-programming-for-ai?publication_id=1692672&post_id=187237708&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[By Bryan Alexander]]"
published:
created: 2026-02-08
description:
tags:
  - "clippings"
---
---

---

With this post I’m trying something different. I’d like to introduce an AI project which we have been quietly developing for the past year.

This is the first offering from BAC Labs, a research and development effort based in [my consulting work](https://bryanalexanderconsulting.com/), now focused on exploring new approaches to AI for educational purposes.

We’d like to begin today with an unusual approach to LLM use, which we dubbed **narrative** **programming**. It’s a method to rethink prompting, as well as how we think about generative AI overall.

Readers will note that the voice of this issue is now first person plural. That’s because it’s the work of two people, Bryan Alexander and Ceredwyn Alexander. Ceredwyn started this R&D process as part of her teaching and instructional development work, developing classes and materials for emergency medical technology ([EMT](https://en.wikipedia.org/wiki/Emergency_medical_technician)) programs in Vermont. She wanted to make LLMs useful for students and instructors but was frustrated by their limitations and so created a new method. She is, in short, the prime mover behind narrative programming.

In a followup post we will introduce SPARKs, an alternative to GPT agents stemming from narrative programming principles.

Read on and see what you think. We’d love to hear your thoughts in the comments box below.

Most people using large language models start with a conversational prompt. They ask a question, describe a goal, maybe suggest a role to play, perhaps specify a style or format, and expect the system to understand and infer what they want. When the AI doesn’t provide the desired results. or when it hallucinates, drifts, or overreaches, some users rephrase their prompt with some change, or criticize the bot, retry the request from a different angle, and try again. This trial-and-error cycle is what we often mean by prompt engineering, but we can also think of it as a kind of belief system, one with several components:

Some advanced prompt engineering guides are beginning to talk about more sophisticated approaches, such as [“context engineering](https://www.philschmid.de/context-engineering) ” or “ [persona vectors](https://arxiv.org/abs/2507.21509).” These approaches do get better results, because they exploit what language models actually do best: extend linguistic patterns.

Our approach takes this further. We formalize those emerging tactics into a discipline. Instead of trial-and-error scaffolding, narrative programming explicitly encodes the inherent structures of storytelling. Narrative roles, genre conventions, symbolic weight, and rhetorical constraints are not only decorative features of human communication. They are structural laws of coherence for the texts upon which LLMs trained. When applied systematically, they can be used to govern AI model behavior with greater precision.

In this framework, we define the following components as constituting a “narrative execution prompt”:

- **Name**: the simulated posture or voice the model assumes
- **Genre**: the logical container that determines tone, stakes, and acceptable behaviors
- **Role**: the general category of agent
- **Job**: what the agent does within a given system
- **Task:** as defined by the user
- **Victory Condition**: the internal measure of task success

When a prompt doesn’t define these elements, the LLM’s behavior eventually drifts away from the initial prompt and becomes unpredictable. This is not a problem with “alignment” nor is it “emergent behavior.” Rather, it is what happens *when the AI follows a different narrative program than the user intended but did not sufficiently describe*. Without specification, an LLM will fall back on any number of stories. The user may experience this as poor inference. In contrast, narrative programming locks AI into roles with hard boundaries and encodes representation logic as enforceable ratios. Defining success, enforcing resets, and maintaining compliance over time mitigates scope creep, bias defaults, and silent drift.

Consider how LLMs work within this narrative programming framing. Our model sees AI as a pattern completion engine.

To reprise the basics: when you type a word, the model doesn’t “see” it as a word like humans do. Instead, it translates it into tokens. Tokens are little chunks of text. Shorter words can be one token while larger words will be broken up. These are the smallest building blocks. Alone, tokens have little or no meaning to humans. Yet an LLM can use vast amounts of tokens (hence the first “L”) to predict a next token using statistical completion, answering the question “What is the most likely next thing?”

During training, the model learns how often that token shows up next to other tokens. These tokens form concepts. *A bird in the hand* is a concept composed of several tokens that is statistically likely to be followed by, *Is worth two in a bush.* This is how we can see how the LLM follows the patterns of language.

Example:

In other words, the model completes the phrase or sentence based on token likelihood, not human intention.

Yet we can now scale up our sense of how training works. Because the LLM trained on vast amounts of human writing, style, tone, syntax, genre, and other narrative features shape the model’s internal functions. LLMs depend on human storytelling in a fundamental way. They devour contemporary novels, classic literature (especially in the public domain), anecdotes, autobiographies, narrative histories, legal accounts of events, military after-action reports, diplomatic readouts, testimonials and all at an immense scale. To pick just one of many examples of this, [Dario Amodei’s recent essay on AI](https://www.darioamodei.com/essay/the-adolescence-of-technology) observes that:

> AI models are trained on vast amounts of literature that include many science-fiction stories involving AIs rebelling against humanity.

They fit predictive texts into grooves of storytelling. Generative AI is, in a real sense, a machine of story, a remixing application for the human narrative tradition.\*

Therefore narrative functions of all sorts - character and character development, plot arcs, morals of stories, setting, atmosphere, metaphor and more - all act as control structures for AI development and output, as they do with much of human writing.

Traditional computers build executable complexity from simpler units:

> bits → bytes → data structures → programs

Likewise, LLM’s build complexity through linguistic patterns that embed story:

> tokens → concepts (words or phrases) → **narrative structures (genre, tropes, arcs, etc)** → programs

That does **not** mean the model is learning skills or becoming intelligent. It means the training set was big enough, and the patterns rich enough, that some outputs *resemble* reasoning when none occurred. And, as the models have gotten larger, they have the capacity to recognize more patterns, providing the illusion of learning, when what is really happening is more powerful software working with larger data sets. Those data sets include stories at scale, so AIs can tell stories and also be directed by them.

This brings us to the problem of alignment. All the high-profile failures of AI systems point to one fact: inference alone cannot guarantee predictability, safety, or representation.Alignment is not intelligence. It is instead patchwork guardrails over stochastic text generation. Training means to enlarge the data set with input that shows more patterns we want to see, hoping for a happier average, instead of simply telling the machine what we want.

What looks like logic is, in fact, **pattern mimicry** (hence the famous term “stochastic parrot”). Reasoning must be scaffolded into the prompt or program. Without that, the model will produce something that feels smart but is structurally hollow. Frequently, the model will produce the same idea repetitively, using different words, presenting each statement as a separate idea. Using narrative thinking in prompts changes the situation significantly. Using the narrative execution prompt components we described above can rein in the parrot and yield better results.

That’s the first installment in a series. There’s more to come, starting with building a new form of AI bot, a Semantically Programmed Agents for Reliable Knowledge, or SPARK. What do you make of this approach? We’re very open to questions and other responses!

> \*Credit to the late, great Cliff Lynch for making the LLM as remix point to Bryan in conversation.