---
title: "On the Rationality of Deterring ASI — LessWrong"
source: "https://www.lesswrong.com/posts/XsYQyBgm8eKjd3Sqw/on-the-rationality-of-deterring-asi"
author:
published: 2025-03-05
created: 2025-03-22
description: "I’m releasing a new paper “Superintelligence Strategy” alongside Eric Schmidt (formerly Google), and Alexandr Wang (Scale AI). Below is the executive…"
tags:
  - "clippings"
---
I’m releasing a new paper “ [Superintelligence Strategy](https://www.nationalsecurity.ai/) ” alongside Eric Schmidt (formerly Google), and Alexandr Wang (Scale AI). Below is the executive summary, followed by additional commentary highlighting portions of the paper which might be relevant to this collection of readers.

## Executive Summary

Rapid advances in AI are poised to reshape nearly every aspect of society. Governments see in these dual-use AI systems a means to military dominance, stoking a bitter race to maximize AI capabilities. Voluntary industry pauses or attempts to exclude government involvement cannot change this reality. These systems that can streamline research and bolster economic output can also be turned to destructive ends, enabling rogue actors to engineer bioweapons and hack critical infrastructure. “Superintelligent” AI surpassing humans in nearly every domain would amount to the most precarious technological development since the nuclear bomb. Given the stakes, superintelligence is inescapably a matter of national security, and an effective superintelligence strategy should draw from a long history of national security policy.

## Deterrence

A race for AI-enabled dominance endangers all states. If, in a hurried bid for superiority, one state inadvertently loses control of its AI, it jeopardizes the security of all states. Alternatively, if the same state succeeds in producing and controlling a highly capable AI, it likewise poses a direct threat to the survival of its peers. In either event, states seeking to secure their own survival may preventively sabotage competing AI projects. A state could try to disrupt such an AI project with interventions ranging from covert operations that degrade training runs to physical damage that disables AI infrastructure. Thus, we are already approaching a dynamic similar to nuclear Mutual Assured Destruction (MAD), in which no power dares attempt an outright grab for strategic monopoly, as any such effort would invite a debilitating response. This strategic condition, which we refer to as Mutual Assured AI Malfunction (MAIM), represents a potentially stable deterrence regime, but maintaining it could require care. We outline measures to maintain the conditions for MAIM, including clearly communicated escalation ladders, placement of AI infrastructure far from population centers, transparency into datacenters, and more.

## Nonproliferation

While deterrence through MAIM constrains the intent of superpowers, all nations have an interest in limiting the AI capabilities of terrorists. Drawing on nonproliferation precedents for weapons of mass destruction (WMDs), we outline three levers for achieving this. Mirroring measures to restrict key inputs to WMDs such as fissile material and chemical weapons precursors, compute security involves knowing reliably where high-end AI chips are and stemming smuggling to rogue actors. Monitoring shipments, tracking chip inventories, and employing security features like geolocation can help states account for them. States must prioritize information security to protect the model weights underlying the most advanced AI systems from falling into the hands of rogue actors, similar to controls on other sensitive information. Finally, akin to screening protocols for DNA synthesis services to detect and refuse orders for known pathogens, AI companies can be incentivized to implement technical AI security measures that detect and prevent malicious use.

## Competitiveness

Beyond securing their survival, states will have an interest in harnessing AI to bolster their competitiveness, as successful AI adoption will be a determining factor in national strength. Adopting AI-enabled weapons and carefully integrating AI into command and control is increasingly essential for military strength. Recognizing that economic security is crucial for national security, domestic capacity for manufacturing high-end AI chips will ensure a resilient supply and sidestep geopolitical risks in Taiwan. Robust legal frameworks governing AI agents can set basic constraints on their behavior that follow the spirit of existing law. Finally, governments can maintain political stability through measures that improve the quality of decision-making and combat the disruptive effects of rapid automation.

By detecting and deterring destabilizing AI projects through intelligence operations and targeted disruption, restricting access to AI chips and capabilities for malicious actors through strict controls, and guaranteeing a stable AI supply chain by investing in domestic chip manufacturing, states can safeguard their security while opening the door to unprecedented prosperity.

## Additional Commentary

There are several arguments from the paper worth highlighting.

**Emphasize terrorist-proof security over superpower-proof security.**

Though there are benefits to state-proof security (SL5), this is a remarkably daunting task that is arguably much less crucial than reaching security against non-state actors and insider threats (SL3 or SL4).

**Robust compute security is plausible and incentive-compatible.**

Treating high-end AI compute like fissile material or chemical weapons appears politically and technically feasible, and we can draw from humanity’s prior experience managing WMD inputs for an effective playbook. Compute security interventions we recommend in the paper include:

- 24-hour monitoring of datacenters with tamper-evident cameras
- Physical inspections of datacenters
- Maintaining detailed records tracking chip ownership
- Stronger enforcement of export controls, larger penalties for noncompliance and verified decommissioning of obsolete or inoperable chips
- Chip-level security measures, some of which can be implemented with firmware updates alone, circumventing the need for expensive chip redesigns

Additionally, states may demand certain transparency measures from each other’s AI projects, using their ability to maim projects as leverage. AI-assisted transparency measures, which might involve AIs inspecting code and outputting single-bit compliance signals, might make states much more likely to agree to transparency measures. We believe technical work on these sorts of verification measures is worth aggressively pursuing as it becomes technologically feasible.

We draw a distinction between compute security efforts that deny compute to terrorists, and efforts to prevent powerful nation-states from acquiring or using compute. The latter is worth considering, but our focus in the paper is on interventions which would prevent rogue states or non-state actors from acquiring large amounts of compute. Security of this type is incentive-compatible: powerful nations will want states to know where their high-end chips are, for the same reason that the US has an interest in Russia knowing where its fissile material is. Powerful nations can deter each other in various ways, but nonstate actors cannot be subject to robust deterrence.

**“Superweapons” as a motivating concern for state competition in AI.**

A controlled superintelligence would possibly grant its wielder a “strategic monopoly on power” over the world—complete power to shape its fate. Many readers here would already find this plausible, but it’s worth mentioning that this probably requires undermining mutual assured destruction (MAD), a high bar. Nonetheless, there are several ways MAD may be circumvented by a nation wielding superintelligence. Mirroring a [recent paper](https://www.rand.org/pubs/perspectives/PEA3691-4.html), we mention several “superweapons”—feasible technological advances that would question nuclear deterrence between states. The prospect of AI-enabled superweapons helps convey why powerful states will not accept a large disadvantage in AI capabilities.

**Against An “AI Manhattan Project”**

A US “AI Manhattan Project” to build superintelligence is ill-advised because it would be destructively sabotaged by rival states. Its datacenters would be easy to detect and target. Many researchers at American labs have backgrounds and family in rival nations, and many others would fail to get a security clearance. The time and expense to secure sensitive information against dedicated superpowers would trade off heavily with American AI competitiveness, to say nothing of what it would cost to harden a frontier datacenter against physical attack. If they aren’t already, rival states will soon be fully aware of the existential threat that US achievement of superintelligence would pose for them (regardless of whether it is controlled), and they will not sit idly by if an actor is transparently aiming for a decisive strategic advantage, as discussed in \[ [1](https://situational-awareness.ai/),  [2](https://darioamodei.com/on-deepseek-and-export-controls#export-controls) \].