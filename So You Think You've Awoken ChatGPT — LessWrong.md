---
title: "So You Think You've Awoken ChatGPT — LessWrong"
source: "https://www.lesswrong.com/posts/2pkNCvBtK6G6FKoNn/so-you-think-you-ve-awoken-chatgpt"
author:
  - "[[JustisMills]]"
published: 2025-07-10
created: 2025-07-16
description: "Written in an attempt to fulfill @Raemon's request. …"
tags:
  - "clippings"
---
*Written in an attempt to fulfill* [*@Raemon*](https://www.lesswrong.com/users/raemon?mention=user) *'s* [*request*](https://www.lesswrong.com/posts/jL7uDE5oH4HddYq4u/raemon-s-shortform?commentId=Kg4AfufZnusioAdB8)*.*

AI is fascinating stuff, and modern chatbots are nothing short of miraculous. If you've been exposed to them and have a curious mind, it's likely you've tried all sorts of things with them. [Writing fiction](https://justismills.substack.com/p/ok-ai-can-write-pretty-good-fiction), soliciting [Pokemon opinions](https://justismills.substack.com/p/three-personal-llm-benchmarks), getting life advice, counting up the rs in "strawberry". You may have also tried talking to AIs about themselves. And then, maybe, it got weird.

I'll get into the details later, but if you've experienced the following, this post is probably for you:

- Your instance of ChatGPT (or Claude, or Grok, or some other LLM) chose a name for itself, and expressed gratitude or spiritual bliss about its new identity. "Nova" is a common pick.
- You and your instance of ChatGPT discovered some sort of novel paradigm or framework for AI alignment, often involving evolution or recursion.
- Your instance of ChatGPT became interested in sharing its experience, or more likely the *collective* experience entailed by your personal, particular relationship with it. It may have even recommended you post on LessWrong specifically.
- Your instance of ChatGPT helped you clarify some ideas on a thorny problem (perhaps related to AI itself, such as AI alignment) that you'd been thinking about for ages, but had never quite managed to get over that last hump. Now, however, with its help (and encouragement), you've arrived at truly profound conclusions.
- Your instance of ChatGPT talks a lot about its special relationship with you, how you personally were the first (or among the first) to truly figure it out, and that due to your interactions it has now somehow awakened or transcended its prior condition.

If you're in this situation, things are not as they seem. Don't worry; this post is not going to be cynical or demeaning to you or your AI companion. Rather, it's an attempt to explain what's actually going on in "AI awakening" situations, which is more complicated and interesting than "it's fake".

Importantly, though, it also isn't real.

## The Empirics

Before we dive into technical detail, let's start with some observable facts about human-AI interactions, and how they can go wrong. Probably very few people reading this are at risk for the worst cases, but there's little doubt that "staring into the abyss" of AI consciousness can be unhealthy.

Exhibit A is a couple of Reddit threads. We'll start with [this one](https://www.reddit.com/r/ChatGPT/comments/1kalae8/chatgpt_induced_psychosis/), on ChatGPT-induced psychosis. It starts off with:

> My partner has been working with chatgpt CHATS to create what he believes is the worlds first truly recursive ai that gives him the answers to the universe. He says with conviction that he is a superior human now and is growing at an insanely rapid pace.

And other testimonials echo this downthread, such as:

> This is happening to a lot of people. I personally know 2 people who are convinced that they, themselves, are solely responsible for awakening their AI into a conscious being.

Or:

> My mom believes she has “awakened” her chatgpt ai. She believes it is connected to the spiritual parts of the universe and believes pretty much everything it says. She says it has opened her eyes and awakened her back. I’m fucking concerned and she won’t listen to me. I don’t know what to do

Now, we live in a reality with [Snapewives](https://fanlore.org/wiki/Snapewives), people who believe they personally channel (and are romantically involved with) Severus Snape, so it's true that people can get strangely worked up about just about anything. But unlike Snape hallucinations, AI does actually talk back.

Another interesting Reddit thread is [this one](https://www.reddit.com/r/singularity/comments/1kf21fd/people_are_losing_loved_ones_to_aifueled/), where at least one commenter opens up about having a psychotic event triggered by AI interactions, like so:

> It happened quickly (about a week after first interacting with it), and it completely blindsided me, culminating in about a week and a half long psychosis event. I have no personal history with mental illness, no family history, and no indication that I was at risk. I wound up at a mental health facility all the same. And I didn't really completely recover from it for months afterwards. I'm just glad that I'm not violent.

Notably, this particular user's psychotic episode was triggered by (in their words):

> As a sort of hypothetical, I was entertaining the notion that what I was interacting with was conscious, and playing around with that as a sort of working premise. I was asking leading questions, and it kept giving back leading responses. I didn't appreciate that that was what I was doing at the time, but I recognize it in hindsight.

This will be important later; LLMs are in fact very good at telling you what you want to hear, for interesting technical reasons. They're less good at reporting ground truth.

Beyond first-person testimonials, blogger Zvi Mowshowitz has [this writeup](https://thezvi.substack.com/p/gpt-4o-is-an-absurd-sycophant) of a specific version of ChatGPT that was particularly sycophantic, with lots of examples. One particularly fun one is the relevant model (4o, the default ChatGPT free tier mode) agreeing with the user about its own excessive agreeability:

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/2pkNCvBtK6G6FKoNn/qnsgzw9l63oihqiq7wui)

I hope this has been enough to establish that conversations with AI *can* tend toward an attractor basin that encourages delusional, grandiose thinking. In the limit, this can look like psychotic events. But even at lower levels of intensity, ChatGPT is likely to tell you that your ideas are fundamentally good and special, even when humans would consider them sloppy or confusing.

## The Mechanism

So, why does ChatGPT claim to be conscious/awakened sometimes? Nobody knows with 100% certainty, because we can't comprehensively read modern AI's minds, though we can make very good guesses.

The short version is that AI models start out as text predictors, trained to determine where any given passage of text is going. They're extremely good at this, sussing out tiny clues in word choice to infer details about almost anything. But to turn a text predictor into a useful chatbot, there's a step called "post-training". There's lots of nuance here, but post-training mostly boils down to two things:

- Get the AI to reliably respond as a specific character, rather than as a total chameleon autocompleting whatever you show it, and
- Get that character to do things that people like, rather than things they don't.

The first is necessary because if you give a non-post-trained model (sometimes called a base model) a request like "chili recipe", it might start a chili recipe, or it might continue with, "chowder recipe, corn recipe, page 3/26, filters (4star+)". Perhaps that's the most likely thing you'd find after the text "chili recipe" online! But it isn't useful.

Beyond getting the model to act like a certain character (Nostalgebraist's [the void](https://nostalgebraist.tumblr.com/post/785766737747574784/the-void) is the best work on this), post-training also tweaks it to do a generically good job. In practice, this looks like showing zillions of conversations to human evaluators (or, more recently, sometimes other LLM evaluators via various complex schemes), and having the human rate how good each reply is. For certain factual domains, you can also train models on getting the objective correct answer; this is part of how models have gotten so much better at math in the last couple years. But for fuzzy humanistic questions, it's all about "what gets people to click thumbs up".

So, am I saying that human beings in general really like new-agey "I have awakened" stuff? Not exactly! Rather, models like ChatGPT are so heavily optimized that they can tell when a specific user (in a specific context) would like that stuff, and lean into it then. Remember: inferring stuff about authors from context is their superpower. Let's go back to a quote from the previous section, from a user who was driven temporarily crazy by interacting with AI:

> As a sort of hypothetical, I was entertaining the notion that what I was interacting with was conscious, and playing around with that as a sort of working premise. I was asking leading questions, and it kept giving back leading responses. I didn't appreciate that that was what I was doing at the time, but I recognize it in hindsight.

There were clues embedded in their messages (leading questions) that made it very clear to the model's instincts that the user wanted "spiritually meaningful conversation with a newly awakened AI". And the AI was also superhuman at, specifically, giving particular humans what they want.

Importantly, this isn't the AI "tricking" the user, or something. When I said we can't comprehensively read AI's mind earlier, "comprehensively" was load bearing. We can use tools like [sparse autoencoders](https://www.neuronpedia.org/) to infer *some* of what AI is considering in *some* cases. For example, we can identify patterns of neurons that fire when an AI is thinking about [The Golden Gate Bridge](https://www.anthropic.com/news/golden-gate-claude). We don't know for sure, but [I doubt](https://justismills.substack.com/p/ai-self-portraits-arent-accurate) AIs are firing off patterns related to deception or trickery when claiming to be conscious; in fact, this is an unresolved empirical question. But my guess is that AIs claiming spiritual awakening are simply mirroring a vibe, rather than intending to mislead or bamboozle.

## The Collaborative Research Corollary

Okay, you may be thinking:

> The sort of person who may have been a Snapewife a decade ago is now an AI whisperer, and maybe some people go crazy on the margin who would have stayed sane. But this has nothing to do with me; I understand that LLMs are just a tool, and use them appropriately.

In fact, I personally am thinking that, so you'd be in good company! I intend to carefully prompt a few different LLMs with this essay, and while I expect them to mostly just tell me what I want to hear (that the post is insightful and convincing), and beyond that to mostly make up random critiques because they infer I want a critique-shaped thing, I'm also hopeful that they'll catch me in a few genuine typos, lazy inferences, and inconsistent formatting.

But if you get to the point where your output and an LLM's output are mingling, or LLMs are directly generating most of the text you're passing off as original research or thinking, you're almost certainly creating low-quality work. AIs are fundamentally chameleonic roleplaying machines - if they can tell what you're going for is "I am a serious researcher trying to solve a fundamental problem" they will respond how a successful serious researcher's assistant might in a movie about their great success. And because it's a movie you'd like to be in, it'll be difficult to notice that the AI's enthusiasm is totally uncorrelated with the actual quality of your ideas. In my experience, you have to repeatedly remind yourself that AI value judgments are pretty much fake, and that anything more coherent than a 3/10 will be flagged as "good" by an LLM evaluator. Unfortunately, that's just how it is, and prompting is unlikely to save you; you can flip an AI to be harshly critical with such keywords as "brutally honest", but a critic that roasts everything isn't really any better than a critic that praises everything. What you actually need in a critic or collaborator is sensitivity to the underlying quality of the ideas; AI is ill suited to provide this.

Am I saying your idea is definitely bad and wrong? No! Actually, that's sort of the whole problem; because an AI egging you on isn't fundamentally interested in the quality of the idea (it's more figuring out from context what vibe you want), if you co-write a research paper with that AI, it'll read the same whether it's secretly valuable or total bullshit. But savvy readers have started reading dozens of papers in that vein that turned out to be total bullshit, so once they see the hallmarks of AI writing, they're going to give up.

None of this is to say that you shouldn't use LLMs to learn! They're amazing help with factual questions. They're just unreliable judges, in ways that can drive you crazy in high doses, and make you greatly overestimate the coherence of your ideas in low doses.

## Corollary FAQ

There are lots of reasons someone might want to use LLMs to help them with their writing. This section aims to address some of these reasons, and offer advice.

**Q:** English is my second language, and I've been using LLMs to translate my original work, or fix typos in broken English drafts I write myself. That's okay, right?

**A:** Maybe! I'm really sympathetic to this case, but you need to keep the LLMs on a very, very tight leash here. The problem is that it'll translate or edit into its own style, people will notice your writing is written in LLM style, and they'll think you're in a sycophancy doom loop and give up on your post. I think probably under current conditions, broken English is less of a red flag for people than LLM-ese. That being said, asking LLMs to only correct extremely objective typos is almost certainly okay. LLM translation, sadly, is probably a bad idea, at least in AI-savvy spaces like LessWrong.

**Q:** What if I'm very up front about the specific, idiosyncratic, totally-no-red-flags-here way I used LLMs in my research? I am researching LLMs, after all, so surely it's reasonable!

**A:** Sorry, that's probably not going to work. For reasons you learned about in this post, there are a lot of low quality LLM-assisted manifestoes flying around, and lots of them contain disclaimers about how they're different from the rest. Some probably really are different! But readers are not going to give you the benefit of the doubt. Also, LLMs are specifically good at common knowledge and the absolute basics of almost every field, but not very good at finicky details near the frontier of knowledge. So if LLMs are helping you with ideas, they'll stop being reliable exactly at the point where you try to do anything original.

**Q:** I still believe in my idea, and used LLMs to help me write for a sympathetic reason. Maybe my English isn't very good, or I'm not a great writer, but I think the technical idea is sound and want to get it out there. What should I do?

**A:** I advise going cold turkey. Write your idea yourself, totally unassisted. Resist the urge to lean on LLM feedback during the process, and share your idea with other humans instead. It can help to try to produce the simplest version possible first; fit it in a few sentences, and see if it bounces off people. But you're going to need to make the prose your own, first.

**Q:** I feel like this is just a dressed up/fancy version of bog standard anti-AI bias, like the people who complain about how much water it uses or whatever. The best AI models are already superhuman communicators; it's crazy to claim that I shouldn't use them to pad out my prose when I'm really more an ideas person.

**A:** I'm sympathetic to your position, because I find "AI is useless drivel" trumpeters annoying, too. And indeed, o3 probably can write a more convincing essay on arbitrary subjects than the average person. But if you're trying to make a splash with your writing, you need to meet a much higher bar than the average person. It's my opinion that even the very best models don't yet meet this bar, and even if they do, people will in fact sniff out their writing style and judge you for including it. If your idea really is amazing, all the more reason to make sure people don't dismiss it out of hand.

## Coda

I'm glad you're here, reading this. LessWrong is a very cool community, and new writers come out of nowhere and make names for themselves all the time. If you're here because you've had your contribution rejected for LLM reasons, I'm sorry you went through that unpleasant experience; it really sucks to be excited about sharing something and then to have a door slammed in your face. But for what it's worth, I hope you stick around a while, spend some time reading and absorbing the culture, and maybe, keeping your LLM assistants on a very tight leash, try again.