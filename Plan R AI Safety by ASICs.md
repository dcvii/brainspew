---
title: "Plan R: AI Safety by ASICs"
source: "https://www.lesswrong.com/posts/n8u3BfqFoGh4jnzpo/plan-r-ai-safety-by-asics"
author:
  - "[[Roko]]"
published: 2026-09-25
created: 2026-10-29
description: "Much of the civilization-scale risk we are seeing in AI in 2026 comes from the following combination: we created a single institution (the \"Frontier…"
tags:
  - "brainspew"
---
Much of the civilization-scale risk we are seeing in AI in 2026 comes from the following combination: we created a single institution (the "Frontier AI Company") that has two properties:

A. It is set up to create very powerful and/or self-replicating entities that may exceed the capabilities of the entirety of the rest of civilization and come with extraordinary risks

B. It gets to own an unbounded financial claim on the resulting surplus

All the technical stuff about AI, AI alignment, etc can be rolled up into point (A) above. My claim is that having point (A) on its own, without point (B) is probably okay. Nuclear technology and bioweapon technology both approximate (A) and they are mostly okay because without (B), there isn't an incentive for people controlling them to push their luck on safety.

But with Frontier AI Companies, we mixed the two.

The key claim of this post is that we can probably get rid of most of AI risk without doing anything other than separating out the bookkeeping, physical footprint and institutions so that there is no single org with both properties. And with a little help from ASICs, maybe we can also have a very productive AI industry that actually delivers most the benefits of AI to boot. No busy-waiting pause, no "banning AI", etc.

What a typical AI disaster scenario currently looks like (e.g. those by Daniel Kokotajlo):

- AI company builds lots of compute and does research, with goods and services flowing in from the human economy.
- Human economy mostly gets IOUs in return ("Stock")
- AI company is incentivized to push forward as fast as possible so that it can sell more IOUs
- AI company and/or its leading model (which is misaligned) takes over the world
- IOUs are not respected, because now the misaligned superintelligence is more powerful than the mechanisms that were supposed to enforce the IOUs
- Everyone dies, The End

Obviously, the humans made a mistake in letting the AI company write the IOUs to them. But once there's a system for stocks, banking, money, etc, letting people write you IOUs is the default and it's hard to stop.

So, here's how I would separate the two. Create two new kinds of entity:

(1) - AI research and development (AI R&D) organizations.

(2) - AI deployment companies

AI R&D orgs would do everything that involves training, distilling, testing, and aligning frontier AI models. They would be heavily legally restricted and unable to issue equity. Maybe they could get debt financing, I will have to think more about this.

AI deployment companies would do all the consumer-facing stuff, or B2B work. They would run inference at scale. They would handle the UI/UX, and also anything that doesn't require gradient descent, so they could organize AI agents into swarms, attach databases, etc. Some AI deployment companies could sell AI hardware direct to consumer or integrate them into robots and laptops.

AI deployment companies would be able to issue equity and they would pay the AI research and development organizations for the models. Also of note: these AI deployment companies would potentially have a lot of intimate knowledge about the real world and real people, either via the web interfaces or perhaps customer data from robots. The AI R&D orgs would not be allowed to have that kind of data. This makes an global AI takeover from an AI R&D org much harder, because the organization as a whole simply doesn't have this goldmine of blackmail material and intel on people just sitting around for the taking.

Now fortunately the technology underlying AI allows us to enforce this distinction at a hardware level - an AI R&D org would work on a model and once they were done with it and it had passed whatever evals we deem necessary, they would burn it into an ASIC. This would be a fixed-function ASIC whose physical circuitry implements a particular model, the way a human brain has physical connections that implement a human mind. It would have some specific input-output type, such as text in/text out, or video in/motor controls out. That ASIC has some run size R units produced, and those are then sold. Then the model is deleted or encrypted and not allowed to run in the AI R&D org any more. In the most paranoid case, one could try to make a run size of R=1 or some small integer. But I am imagining runs of tens or hundreds of thousands.

All high-spec compute that exists outside the AI R&D orgs would be in the form of ASICs. So whole categories of AI risk simply disappear. There is no compute overhang that a rogue AI can capture. It is stuck with CPUs or maybe GPUs (though maybe there is a way to change how GPUs work so that they can't run AI models - more to do here).

The AI R&D orgs would have an airgapped, high security perimeter containing their general purpose GPU/TPU compute, with physically enforced multi-hour latency connections to the outside world including to their own research floor. This physically enforced latency is done in a way that makes it impossible to get data in or out in less than say 12 hours, even if you wanted to. This means that models that are undergoing training do not have a low-latency channel to the real world, which severely restricts the damage they can do, including things like the recent Hugging Face hack.

In addition to these AI R&D orgs not having equity, they would have some amount of abnormal scrutiny. Perhaps not full research transparency, but that is on the table. They might have mandatory write-once logging, for example. They should probably be completely disconnected from the internet at a physical level - not even the research floor has internet. There might be rules on what you can and cannot do during training. There might be other technologies or systems for regulating dangerous AI work. Whatever it is, it goes here.

AI Deployment orgs continue to run on Silicon Valley rules. Move fast and break things.

AI R&D orgs are run like nuclear weapons labs mixed with Global Systemically Important Banks (G-SIBs)

What about recursive self-improvement? Well, a simple rule that might help seriously blunt that risk is that the AI R&D orgs would not be allowed to use their own models - neither the versions that are running on general purpose compute, nor the ASICs that are for sale. But they are allowed to use ASICs from other AI R&D orgs. This is "Anti-dogfooding" - you are not allowed to eat your own dog food.

This would allow *humanity as a whole* to recursively improve its AI tech base, though of course each iteration would be limited by how quickly new models could be certified and ASICs could be made. But it would prevent any one AI company from "going nuclear" on its own, because its research floor is only allowed to use AI ASICs from other companies - which must legally also be available to the general market. So if one AI R&D org pulls ahead, inferior ASICs from other companies slow it down.

In this system, no entity gets to own an unbounded financial claim on The Singularity.

But the AI deployment companies can still use these AI ASICs to do useful work. AI is not banned. You can still have ChatGPT - it just gets served from an ASIC. People can still try to cure cancer and aging. Robots can still have AI brains, either in place or remotely. We can still use AI for military applications. But there is a very strong separation between inference and training, enforced at the hardware level. ASICs cannot compute gradients, so they cannot train. They cannot change what model they are running, so they cannot be taken over by rogue AIs. Insider risk at the AI R&D orgs is reduced because model X cannot be used to help train model X+1. You have to use someone else's model.

For additional safety, ASIC adoption by AI R&D labs could be lagged - so an ASIC must spend say 3 months working on a variety of real world tasks before it can be considered for use in an AI R&D org. This should hopefully add something to safety as real world use allows a run of ASICs to collect a track record, and it will put a speed limit on the Singularity.

An international agreement would be needed to enforce this system (call it "Plan R") globally, but since the industry currently really only exists in two countries I think that is feasible. I think this "Plan R" is much better than both "Plan S" (total AI research shutdown) and "Plan A" from the point of view of the large relevant international actors. There may nevertheless be bargaining frictions at play, but I feel like analyzing them is not appropriate here.

The philosophy behind Plan R is a sort of "AI Safety by skeuomorphism" - instead of trying to work out how to make the world safe with arbitrarily powerful and general AIs, change what an AI is so that it behaves more like a human, which the world is already set up to deal with. ASICs that lock a particular algorithm to a specific piece of hardware are more human-like than GPUs which allow a single algorithm to "grab" massive amounts of new compute at almost "instant speed".

See also:

[https://www.lesswrong.com/posts/BHGoF7tPqtLo9mXFL/plan-r-diversity-escrow-and-political-rights-for-asics](https://www.lesswrong.com/posts/BHGoF7tPqtLo9mXFL/plan-r-diversity-escrow-and-political-rights-for-asics)

[https://www.lesswrong.com/posts/uwtnWvnJAEccksKNk/skeuomorphic-ai-safety-2](https://www.lesswrong.com/posts/uwtnWvnJAEccksKNk/skeuomorphic-ai-safety-2)