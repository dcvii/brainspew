---
title: "Post by @aakashgupta on X"
source: "https://x.com/aakashgupta/status/2051934004073697343"
author:
  - "[[@aakashgupta]]"
published: 2026-05-06
created: 2026-05-06
description: "Nvidia just figured out how to put an AI data center on the side of your house. And pay you to host it. Each XFRA node packs 16 Blackwell R"
tags:
  - "brain_spew"
---
Nvidia just figured out how to put an AI data center on the side of your house. And pay you to host it.

Each XFRA node packs 16 Blackwell RTX Pro 6000 GPUs, 4 AMD EPYC CPUs, and 3TB of RAM in a Dell PowerEdge rack mounted next to the AC condenser. The homeowner pays nothing for the hardware. They get discounted electricity and internet in exchange for letting Span tap unused capacity on their electrical panel.

This sounds insane until you look at the actual constraint blocking AI infrastructure.

Hyperscalers are not GPU-limited. Nvidia ships them on schedule. They are not capital-limited. They are sitting on hundreds of billions in capex. What they cannot get is grid interconnection. A 100MW data center requires a substation upgrade that takes 4 to 7 years in most US markets. US grid operators have over 2,600 gigawatts stuck in their interconnection queues per Lawrence Berkeley Lab. The wait, not the silicon, is the bottleneck.

Span solved this by going behind the meter.

A new Pulte home has 200A service. That's 48kW of capacity. The home uses 1 to 3kW most hours. The headroom never gets touched. Span's smart panel measures real-time consumption and dynamically routes whatever the home isn't using to the XFRA node. No substation upgrade. No queue. Just slack capacity sitting on the residential side of the meter, already cleared.

Span claims it can deploy 8,000 nodes for one fifth the cost of a comparable 100MW centralized facility, six times faster.

PulteGroup is the wedge. They delivered 29,000 homes in 2025. The XFRA unit goes in during construction next to the smart meter. No retrofit. Pulte gets a feature on the spec sheet and revenue share on the compute that flows through the wall.

The grid was the bottleneck. Pulte just became the workaround.

![Image](https://pbs.twimg.com/media/HHnvGcJa0AAuv_t?format=jpg&name=large) ![Image](https://pbs.twimg.com/media/HHnvGmjacAEfMsT?format=jpg&name=large)

---

To get all my takes without an algorithmic filter, subscribe to my newsletter:

[aibyaakash.com AI by Aakash | Substack](https://t.co/vHdRoFmd5z)

---

## Comments

> **Culture Economy @CultureEconomyX** · [2026-05-06](https://x.com/CultureEconomyX/status/2052036784041910354)
> 
> @grok does this only work with new construction homes or can it be installed in existing homes with smart meter? My condenser is opposite side of house from smart meter.

> **Jonas Hernlund @jonashernlund** · [2026-05-06](https://x.com/jonashernlund/status/2051968596549542296)
> 
> Panel math checks out. Real failure mode is the residential ISP. Home plans cap upload at 35Mbps and ban commercial workloads in TOS. 16 Blackwells pushing inference traffic gets the node throttled or the homeowner kicked off Comcast.

> **Nicolas Nowinski @nicknow** · [2026-05-06](https://x.com/nicknow/status/2052033105074991260)
> 
> Isn’t this just an expensive way around anti-data center regs. Like in any neighborhood you can’t max out power draw on all the homes because they are fed by the same feeder. You could just put all the infrastructure at a main clubhouse and get the compute you need on the same

> **Dumb Money @TeslaDude12** · [2026-05-06](https://x.com/TeslaDude12/status/2052028243063284217)
> 
> The big AI training data centers even the ones behind the meter being powered by natural gas are only paying about five cents a kilowatt hour. Nobody wants to pay residential electric rates for inference.

> **Kislay Parashar @KislayParashar1** · [2026-05-06](https://x.com/KislayParashar1/status/2052049395978535307)
> 
> Putting GPUs next to houses is wild, but the grid workaround part actually checks out. Only question is who deals with the noise, heat, and uptime when this stuff runs 24/7 outside someone’s home ?

> **MDKnight @MDKnight008** · [2026-05-06](https://x.com/MDKnight008/status/2052040847818936425)
> 
> @grok estimates the price of the hardware at $200-300k. If you leave it next to the AC condenser, it’s just asking to be stolen.

> **Derek Colley @DerekColley\_** · [2026-05-06](https://x.com/DerekColley_/status/2052029853470245135)
> 
> I can see these units under the floor, providing free heat in the winter.
> 
> Ppl tried doing this with bitcoin miners too

> **Marilyn Kidd @SunflowerLuv8** · [2026-05-06](https://x.com/SunflowerLuv8/status/2052055961032917146)
> 
> This won’t end well. Too much weather and noise impacts- not to mention will raise elec costs overall.

> **Jacob Tennis @JTRevinc** · [2026-05-06](https://x.com/JTRevinc/status/2052001694582456677)
> 
> New homes will soon come standard with:
> 
> > **Jacob Tennis @JTRevinc** · 2026-05-06
> > 
> > Prediction:
> > 
> > New homes will soon come standard with
> > 
> > \- Solar panels
> > 
> > \- Batteries
> > 
> > \- Electric vehicle charging
> > 
> > \- Local AI inference
> > 
> > \- A home AI
> > 
> > Who’s building this?
> > 
> > @elonmusk @BrianRoemmele x.com/exec\_sum/statu…