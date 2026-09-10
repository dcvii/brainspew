---
title: "Culture Becomes a Dark Forest"
source: "https://www.theintrinsicperspective.com/p/culture-becomes-a-dark-forest?triedRedirect=true"
author:
  - "[[Erik Hoel]]"
published: 2026-09-09
created: 2026-09-10
description: "“Wallfacing” to solve Navier-Stokes"
tags:
  - "brainspew"
---
![](https://substackcdn.com/image/fetch/$s_!AZxo!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F926100ad-bf39-416b-9cf8-8f95384d2408_4436x1462.png)

The metaphor of a “dark forest” comes from Liu Cixin’s *The Three-Body Problem* trilogy, which is the best sci-fi released in China, or frankly anywhere else, in the past two decades. Unfortunately, all the interesting Chinese-specific aspects were butchered in the ham-fisted American TV adaptation, stripped of its slow intellectualism and civilizational scale (try the vastly superior original Chinese adaptation, which you can find on Amazon).[^1] In the second book of the trilogy, *The Dark Forest*, Liu reveals the true nature of the book’s universe:

> The universe is a dark forest. Every civilization is an armed hunter stalking through the trees like a ghost, gently pushing aside branches that block the path and trying to tread without sound. Even breathing is done with care. The hunter has to be careful, because everywhere in the forest are stealthy hunters like him. If he finds other life—another hunter, an angel or a demon, a delicate infant or a tottering old man, a fairy or a demigod—there’s only one thing he can do: open fire and eliminate them. In this forest, hell is other people. An eternal threat that any life that exposes its own existence will be swiftly wiped out. This is the picture of cosmic civilization. It’s the explanation for the Fermi Paradox.

And now, it is our turn to become a dark forest. Here on Earth, at least, people producing the content of our culture—especially scientists and writers and mathematicians—are now living in a dark forest, all thanks to AI.[^2]

![](https://substackcdn.com/image/fetch/$s_!LYnV!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff6d7f8ed-ea57-486c-8cea-e99e5dcf5b6b_3066x1136.png)

The Hunt in the Forest by Paolo Uccello (1490)

We are seeing the dark forest play out in math right now. Enter Navier-Stokes: one of six remaining Millennium Problems in math. It was just announced on the brink of being solved yesterday, by two mathematicians, one employed at Anthropic, the other a mathematician at NYU, who were tackling the project on their personal time. Their year-long attempt used AI, but it was *not* done autonomously. It used various AIs as tools, and Professor Tristan Buckmaster at NYU—the academic half of the pair—says the idea “is not the direction one arrives at in a few days by giving a model the problem statement.” He [released a statement](https://cims.nyu.edu/~tristanb/statement.pdf) saying that:

> The program this fits into was not started by us nor was it proposed by a Large Language Model. The credit for the basic idea of this program goes to Diego Córdoba and Luis Martínez-Zoroa, who for several years have been exploring the construction of forced blow ups. We took their work as a starting point, using Large Language Models to push their program to completion…. The ideas making this line of attack possible are due to Córdoba and Martínez-Zoroa….

His pretty shocking letter implies that OpenAI found out about the pair’s work, and then rushed to scoop them, and so the pair is being forced to release several related proofs early, some of which is in a state of “AI slop” (their actual Navier-Stokes solution, or rather their proposed solution of a version of the problem, is being formalized). OpenAI later released its own claim to a solution yesterday afternoon. Here’s the preview of the release from the company.

![](https://substackcdn.com/image/fetch/$s_!QQ4h!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6a35239d-ccf2-4304-8327-8dc4fdedf96c_1096x630.png)

Yet the statement by Professor Buckmaster offers a rare inside view of this process that contradicts a lot of the official narratives. First, the letter raises the open question of whether companies have been siccing teams of elite human mathematicians on problems, assisted by AI or using AI as tools, with lots of high-level direction (“vibe math”), and then claiming or at least implying the results were fully autonomous. E.g., Buckmaster says that the pair were first told “very little human input” went into OpenAI’s result on Navier-Stokes, but:

> This turned out not to be true…. it emerged that an entire team had been working on the problem….

It’s unclear what this team did exactly,[^3] but what is clear is that the previous work of the pair could have been in the training data since they used OpenAI models in their year-long process. The letter directly asks whether OpenAI used their chats (as the pair were using OpenAI models), either explicitly, or by training the models on their chats.

> I asked whether the model had been trained on, or had access to, our sessions in Codex, into which we had been putting all our drafts for the whole of this project. I was told the model did not look up user data. I asked again, about training, and I did not get an answer.

How often does a human mathematician’s work-in-progress on a problem get fed into the machine? [Here’s an example](https://arxiv.org/pdf/2609.05746) from September: from what I understand, a prominent mathematician who had been working on solving the Jacobian conjecture had a draft accidentally up on the web *since 2025.* The posted AI verification of Anthropic’s much-touted Jacobian conjecture (verified by another company—sorry this is confusing!) contains notational overlap with that work-in-progress, indicating that when AIs reason or write about things like the Jacobian conjecture, the models can be so sensitive to previously-seen works-in-progress that even notation can leak through.

One can become a conspiracist about this easily, but in a sense the pair had been hunting Diego Córdoba and Luis Martínez-Zoroa, who had been doing their work in the open. Then, OpenAI started hunting the hunters.

Of course, what scientists call “scooping” is one thing, but to really earn the moniker a Dark Forest requires a kind of cosmic horror. It has to be worse than just “stuff is fast and competitive now.”

A few days ago, mathematician Terence Tao [wrote some thoughts](https://mathstodon.xyz/@tao/117207855800042681) worth reading on why it’s so much worse. He asks: are these new automated proofs going to be informative? Or are they “odorless” (Tao’s term) when it comes to the normal smelly human insight that accompanies proofs? It’s verifiable if an AI proves something, but it’s unverifiable if that proof generates insight in the way a human’s proof would. Analogously, right now, I could ask GPT 6 to pen me an entire fantasy trilogy. And at this point, it could do it! It could create all the characters, it could trace out and follow a plot, it could keep everything straight, and it could even render me an old-school fantasy map in SVG to go at the beginning. Would it be *the kind of fantasy book* I’d like to read? Probably not. So too now, ChatGPT can prove a mathematical theorem. Is it *the kind of proof* that other mathematicians want to read, given what they’d want out of solving a famous problem? I can’t personally judge this stuff, but the reactions from the mathematical community appear to be no, for many of these problems. Open math problems are now a “non-renewable resource” (Tao’s term), because AI decouples the normal insights that come from human consciousness.

![](https://substackcdn.com/image/fetch/$s_!keab!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8b80a5c3-4648-42e2-8fb0-c3c8a4d7a08f_3552x1320.png)

But why stop at math? All subjects are subject to the rules of the dark forest. It used to be possible to, say, go to a scientific conference to present unfinished work, or go online and get feedback on your idea for a fantasy novel. The walls of effort, of old-fashioned normal human effort, were predictable, and scooping ideas required putting in that same effort, and if you got scooped it would at least result in similar insights. And while insights or generative capacity for the rest of culture is harder to quantify and track than insight from math progress, *it still exists*, and examples abound (e.g., Tolkien creating the modern fantasy genre). People used to say: “We’re a start-up in stealth.” Now *all* thinking must be in stealth.

And yes, obviously, this outcome is vampiric and enervating and sad, but frankly, this has been the mode of this technology from the beginning. Human culture always led naturally to more human culture—it was kind of like crop rotation, which is slow but infinitely sustainable. AI looks more like slash-and-burn agriculture, where you purposefully reduce the existing natural growth to ashes, grow a couple years of crops on it, and then move on to the next plot. The only way to counteract the situation is for all of us to become what Liu Cixin called “wallfacers” in *The Three-Body Problem* —if you are working on something interesting, then wallfacing is necessary. You must face the wall, and so leak nothing, give away nothing.

It’s hard to notice social commons until they are gone, but remember how delightful it was to be able to talk about an intellectual work-in-progress in public? Or just float a good idea to get opinions about it first? Remember that? Go ahead, violate the dark forest. Take that brilliant idea you’ve been sitting on for years, the one for an app, or a book, or a game, or a scientific paper. Take that little thought that is dear to you and post about it on social media. See what happens. See what hunters shoot.

And yes, sure, books will still be published, papers still written, new programs and applications launched. But the future of intellectual work is to be crouched behind a tree, frantically trying to complete your contribution as silently as possible. You’ll feel the pressure of being hunted, since all it takes is a prompt to produce an almost-as-good version of what you’re attempting to make great, and so to mine away the inspiration and insight and reward. Quite often, staggering successes are erected in the forest, but they are never done collaboratively or in the open. You’ll never see anything being built anymore. Instead you’ll find the results at dawn, a gleaming sculpture in a glade, of unclear origin, and with features brutally beautiful. And then once the sparkle fades everyone will rush back to their respective trees, to their fumbling amid the loam, to their slick-wet roots, to their dark.

![](https://substackcdn.com/image/fetch/$s_!77up!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fef04fb66-b68b-4482-b982-c9095e5a82bb_3250x1204.png)

---

∙

[55 Restacks](https://substack.com/note/p-214563044/restacks?utm_source=substack&utm_content=facepile-restacks)

[^1]: How big of a deal is the *Three-Body Problem* in China? Consider that the rights involved [a literal murder](https://www.nytimes.com/2024/04/01/world/asia/china-three-body-problem-murder.html), of precisely the kind that would happen in *The Three-Body Problem*. Apparently, a billionaire Mr. Lin was determined to oversee the intellectual property into television and other media.

> Mr. Lin’s fate would change when he hired Mr. Xu, a lawyer, in 2017 to head a subsidiary of Yoozoo called The Three-Body Universe that held the rights to Mr. Liu’s novels. But not long afterward, Mr. Xu was demoted and his pay was cut, apparently because of poor performance.

Disgruntled, Mr. Xu, the lawyer, then *began experimenting on dogs and cats* *to develop poisons in a secret lab*, which he then used to poison and murder Mr. Lin.

[^2]: I didn’t know this, but a few years ago there was [a trend](https://charlottedune.substack.com/p/the-dark-forest-theory-of-the-internet) to say that AI would make the internet a dark forest because users would retreat into walled gardens (one of the [better essays](https://www.wrecka.ge/against-the-dark-forest/) arguing against it uses the Uccello painting as a lead image). It’s an interesting piece of internet lore to check out, but personally, that overarching metaphor doesn’t make much sense to me. You’re supposed to feel *sniped* in a dark forest, not *annoyed* by slop.

[^3]: Regarding the “team of humans” situation: It should be said that the head of this effort at OpenAI has tried to thread the needle, and [admitted](https://x.com/SebastienBubeck/status/2097379415747342689) on social media there was indeed a human team, but also basically said that the team of world-class mathematicians lacked previous experience on Navier-Stokes and so therefore couldn’t “meaningfully contribute to the mathematical content.” But what content? Didn’t contribute to the solution *as written in the paper*? Or to the process? Two very different things. But the fact that we don’t know anything beyond vague pronouncements, and probably won’t ever, is a travesty.