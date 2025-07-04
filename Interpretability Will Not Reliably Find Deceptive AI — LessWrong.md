---
title: "Interpretability Will Not Reliably Find Deceptive AI — LessWrong"
source: "https://www.lesswrong.com/posts/PwnadG4BFjaER3MGf/interpretability-will-not-reliably-find-deceptive-ai"
author:
  - "[[Neel Nanda]]"
published: 2025-05-04
created: 2025-05-28
description: "Disclaimer: Post written in a personal capacity. These are personal opinions and do not in any way represent my employer's views • TL;DR: …"
tags:
  - "clippings"
---
*Disclaimer: Post written in a personal capacity. These are personal opinions and do not in any way represent my employer's views*

**TL;DR:**

- I do not think we will produce **high reliability methods** to **evaluate or monitor the safety of superintelligent systems** via current research paradigms, with interpretability or otherwise.
- **Interpretability still seems a valuable tool** and remains worth investing in, as it will hopefully *increase* the reliability we can achieve.
- However, interpretability should be viewed as part of an overall **portfolio** of defences: a layer in a **defence-in-depth strategy**
- **It is not the one thing that will save us**, and it still won’t be enough for high reliability.

*EDIT: This post was originally motivated by refuting the claim "interpretability is the only reliable path forward for detecting deception in advanced AI", but on closer reading this is a stronger claim than Dario's post explicitly makes. I stand by the actual contents of the post, but have edited the framing a bit, and also emphasised that I used to hold the position I am now critiquing, apologies for the mistake*

## Introduction

There’s a common argument made in AI safety discussions: **it is important to work on interpretability research because it is a realistic path to high reliability safeguards on powerful systems** - e.g. as argued in Dario Amodei’s recent “ [The Urgency of Interpretability](https://www.darioamodei.com/post/the-urgency-of-interpretability) ”.[^1] Sometimes an even stronger argument is made, that interpretability is the *only* realistic path to highly reliable safeguards - I used to believe both of these arguments myself. **I now disagree with these arguments.**

The conceptual reasoning is simple and compelling: a sufficiently sophisticated deceptive AI can say whatever we want to hear, perfectly mimicking aligned behavior externally. But faking its internal cognitive processes – its "thoughts" – seems much harder. Therefore, goes the argument, we *must* rely on interpretability to truly know if an AI is aligned.

I am concerned this line of reasoning represents an **[isolated demand for rigor](https://slatestarcodex.com/2014/08/14/beware-isolated-demands-for-rigor/)**. It correctly identifies the deep flaws in relying solely on external behavior (black-box methods) but implicitly assumes that interpretability doesn't suffer from equally fundamental problems. **There are many deep issues in interpretability that prevent very confident conclusions,** even if we assume models cannot deliberately obfuscate their thoughts, e.g. superposition and the inherent error in our best tools and techniques. **The challenges of interpretability do not seem qualitatively easier to solve than the big issues in black box tests**, especially with more creative black-box tools like monitoring or editing the system’s chain of thought.[^2]

Should we give up on interpretability? No! I still think it has the potential to add a lot of value, and we will have better safeguards with interpretability as part of our portfolio. Even if it adds no value for making superintelligence safer [^3], if it can add value for pre-superintelligence transformative systems that would be enough to justify investment. I just think that we should be more pragmatic about interpretability’s likely impact, and accept that while we can generally improve our safeguards we will likely not reach high reliability.

## High Reliability Seems Unattainable

Based on the current state and foreseeable trajectory of the field without major paradigm shifts, I think that **neither interpretability nor black box methods offer a high reliability** [^4] **path to safeguards for superintelligence**, in terms of evaluation or monitoring. This is due to fairly fundamental limitations of both methods, unless there are substantial breakthroughs, e.g. via using pre-superintelligence systems. This also stems from a general prior that being highly confident in any complex property of a complex system in a range of unpredictable situations is fairly implausible.

However, I am pretty pessimistic in general about *reliable* safeguards against superintelligence with any methods, given how exceptionally hard it is to reason about how a system far smarter than me could evade my plans. As I see it we must either not create superintelligence, rely on pre-superintelligent automated researchers to find better methods, or deploy without fully reliable safeguards and roll the dice, and do as much as we can now to improve our odds.

This doesn't mean we should give up! It means **we need a pragmatic perspective.** We should aim to build the **best possible monitoring and evaluation portfolio** we can, using *all* available tools, while accepting that high reliability might be out of reach. Interpretability can add a valuable source of de-correlated signal, or augment black box methods. The goal shifts from achieving near-certainty to maximizing the *chances* of catching misalignment, making deception *harder* and *riskier* for the AI, even if we can't guarantee detection.

Further, methods that add significant safety to pre-superintelligent transformative systems still add significant value even if they don’t scale to superintelligence - one of the key insights behind [the AI control agenda](https://arxiv.org/abs/2312.06942). Early transformative systems seem likely to be far easier to evaluate and control, but may still be very dangerous if unchecked, and extremely useful if under control. And **when evaluating methods according to how much they help with early transformative systems, interpretability is just one among several reasonable methods** (and probably not my first choice - things like chain of thought monitoring seem like lower hanging fruit)

## Why Won’t Interpretability be Reliable?

**Caveat**: The following is my inside view for the deep reasons why interpretability will never be truly reliable for human science, no matter how much the field progresses. This is a very strong statement, so I'm not that confident here - while it’s obvious that current techniques are unreliable, this is a question of forecasting future research progress, a highly questionable endeavour. It’s very hard to say what might be possible with a paradigm shift in how LLMs are trained, or how we do interpretability.

More importantly, I do not feel able to reason about the effects of lots of AGIs doing AI research. "Thousands of years of mech interp geniuses in a data center" is a crazy anomaly that I can't reason well about, and seems reasonably likely to happen before superintelligence, so I want to hedge. Not only could the research lead to unexpected breakthroughs, it opens up all kinds of weird strategies leveraging the existence of the AGIs like inspecting every SAE latent in detail - though I'd imagine scalable oversight/control schemes using the AGIs should be higher priority than interp. I also think we should be fairly uncertain about what safety research directions the automated researchers will find to be most promising.

That aside, reasons I won't be comfortable relying on interpretability:

- **We miss things**: We're still figuring out the basics. Concepts like superposition mean important features can be smeared across many neurons in non-obvious ways. Our tools like SAEs or transcoders have error and often miss things. We can misinterpret the features found, or only explain a fraction of the model's behavior.
- **It’s hard to measure progress**: We don’t have a ground truth for what’s actually going on, and must inevitably use a range of proxies of varying quality. This means it’s hard to ever be confident you really understand what’s happening.
- **The Long Tail Problem**: Models seem to have both some clean, interpretable structure *and* a massive, messy "long tail" of weird heuristics, special case handlers, and half-learned, noisy behaviours. I’d personally guess that important capabilities, including deception, are in the clean part, but can’t say for sure!
- **How to prove a negative**: We can find *evidence* for or against a hypothesis, but rigorously *proving* the *absence* of deception circuits seems incredibly hard. How do you know you didn't just miss it? How much of the model do you need to understand? 90%? 99%? 99.99%? The required level of certainty for high-stakes deployment feels far beyond our current capabilities.
	- I’m more optimistic about interpretability as a way to potentially *demonstrate* misalignment, but failure to do so tells us little.
- **Scalability Questions**: Most of our best results are on toy models or yesterday's LLMs. I think that scaling is a tractable problem, but likely involves a bunch of LLM labour assisting, another source of error and uncertainty.
- **Potential for Obfuscation**: While maybe harder than faking outputs, a smart AI could potentially learn to structure its internal computations to be opaque to our specific interpretability tools.

## The Potential of Black-Box Methods

Black-box methods, i.e. things that engage with the model’s inputs and outputs, have clear issues: [models can already tell when they’re being evaluated](https://www.lesswrong.com/posts/E3daBewppAiECN3Ao/claude-sonnet-3-7-often-knows-when-it-s-in-alignment), or [realise when they need to instrumentally fake obedience](https://arxiv.org/abs/2412.14093). But I think there’s also a lot of clever tricks you can do to strengthen them, and they might go a long way. This is more a question about [AI control](https://arxiv.org/abs/2312.06942) than my areas of expertise, but some thoughts on directions I find promising:

- Reading the chain of thought (with another LLM) and looking for sketchy intent [^5]
- Editing the model’s chain of thought so it e.g. thinks it concluded that it’s not in an evaluation
- Asking questions to many copies of the same model and look for inconsistencies while they can’t coordinate.
- Finetuning the model to e.g. be more truthful or forthcoming, or [to insert misleading beliefs and trick it](https://alignment.anthropic.com/2025/modifying-beliefs-via-sdf/).
- Creating honeypots that try to trick the model into revealing its intent

## The Role of Interpretability

So, where does interpretability fit into this pragmatic portfolio? I see several key roles, viewing it not as a standalone solution, but as a valuable component.

Firstly, safeguards can be categorised as follows:

1. **Evaluation**: We take a system and perform extensive tests on it for undesired properties, like a tendency towards misalignment or sandbagging
2. **Monitoring**: When we deploy a system we are always running some checks at inference, which try to catch and mitigate bad behaviour
	1. Importantly, this needs to be cheap to be run in production, while evaluations can be more expensive and slow

How can interp help?

1. **A Layer of Swiss Cheese:** I think the right monitoring schemes have several layers of defence (a la the [swiss cheese model](https://en.wikipedia.org/wiki/Swiss_cheese_model)), with different cost to accuracy trade-offs.
	- Interpretability techniques like probes for known dangerous features are extremely cheap, [and surprisingly effective](https://www.lesswrong.com/posts/4uXCAJNuPKtKBsi28/negative-results-for-saes-on-downstream-tasks#Using_SAEs_for_OOD_Probing), and can serve as a good first layer of defence, which call more expensive tests (e.g. an LLM reading the chain of thought) if they fire.
	- Interpretability techniques like SAEs or cross-layer transcoders may have the potential to be more expensive but accurate ways to audit what’s going on and look for anything unexpected.
	- Even if interpretability is not more accurate, so long as it has some signal and is de-correlated, then it adds value, even if it’ll miss many things.
2. **Enhancing Black-Box Evaluations:** Interpretability might make our external checks more effective. For example:
	- Could we use steering vectors identified via interpretability to **manipulate whether the model thinks it’s in an eval?** Maybe we can test it more effectively if we can trick it into thinking it's *not* in a honeypot or evaluation setting.
	- Can we use interpretability to better elicit information from token forcing? We can make the model say “my secret plan is”, and even if it tries to internally suppress awareness or obfuscate the output perhaps interpretability can prevent that?
	- Interpretability may provide a sanity check that our black box methods are not missing something, e.g. whether a model is passing an eval only because it knows it’s in one and is deliberately underperforming.
3. **Debugging mysterious behaviour**: One particularly interesting form of evaluation (or offline monitoring) is taking particularly weird or unexpected examples of model behaviour, e.g. it seeming to put vulnerabilities in critical code, and trying to debug what’s going on and see if it’s real alignment or not. I think interpretability methods may prove very good at raising unexpected hypotheses, and piecing together what’s happening (e.g. [this proof of concept](https://transformer-circuits.pub/2025/attribution-graphs/biology.html))
	- I expect these kinds of potential warning shots to happen, and anything that can add more signal here would be great.
	- Even if we don’t trust the interpretability method fully, the hypotheses generated can be verified by other means.

These applications aren't guaranteed to work or be ungameable, but they represent concrete ways *internal* understanding could augment *external* validation, creating a more robust overall system than either alone.

## Conclusion

Let's stop framing interpretability as the *one true path* to reliably detecting AI deception, a view often born from an isolated demand for rigor against flawed black-box methods. Neither approach offers high reliability against superintelligence without fundamental breakthroughs, but flawed methods can still be useful. For the powerful pre-SI systems that concern us now, let's focus on building the best **pragmatic portfolio** of imperfect defenses we can. Interpretability is a useful part of that portfolio – offering unique angles of analysis and potential synergies with other methods – but it's one tool among many, not a substitute for a comprehensive, defense-in-depth strategy. We need to leverage every imperfect signal we can get, from both inside and outside the box.

*Thanks to my co-author Gemini 2.5 Pro*

---

[^1]: While this post was inspired by Dario's post and ensuing discussion, this is a common belief I've encountered, and this post is not intended to call out him specifically!

[^2]: More specifically, I basically think the only way we might get high reliability is by using pre-superintelligent systems that are sufficiently aligned/controlled to either do a ton of automated research and find some breakthroughs, or by using them as a core part of a monitoring or scalable oversight scheme. But the human research trajectory is hard.

[^3]: Defining “safety” is kinda messy, for the purposes of this post you can interpret it as evaluating ‘is the model thinking misaligned thoughts’ or monitoring for ‘is the model currently knowingly taking high-stakes actions against what we want’

[^4]: I’m not sure what the best precise definition of highly reliable is here, maybe 99.9% chance of stopping a catastrophic outcome? It’s not key to my argument.

[^5]: Obviously, [Chain of Thought can fail to reflect the model’s true reasoning](https://arxiv.org/abs/2503.08679). But I think that for tasks at the limits of its ability it likely needs to use the chain of thought for intermediate steps in the computation, creating an incentive to store key info in there. Of course, there are many ways this can fail.