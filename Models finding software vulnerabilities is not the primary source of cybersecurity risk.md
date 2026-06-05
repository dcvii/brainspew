---
title: "Models finding software vulnerabilities is not the primary source of cybersecurity risk"
source: "https://www.lesswrong.com/posts/gutiw8MBrYDiD2u5z/models-finding-software-vulnerabilities-is-not-the-primary"
author:
  - "[[lc]]"
published: 2026-05-13
created: 2026-06-04
description: "I have tried and failed to write a longer post since 2024, so here goes a short one with less detail. …"
tags:
  - "brain_spew"
---
I have tried and failed to write a longer post since 2024, so here goes a short one with less detail.

Discourse has primarily focused on models' ability to develop new exploits against important software from scratch. That capability is impressive, but the tech industry has been dealing with people regularly finding 0-day exploits for important pieces of software for more than [twenty years](https://en.wikipedia.org/wiki/Pwn2Own). Having to patch these vulnerabilities at a 10xed or even 100xed cadence for a fixed period of time is well within the resources of Mozilla, the Linux Foundation, and Microsoft. The lag time between "patch shipped" and "patch reverse engineered and weaponized by a criminal organization" was already so long that most people didn't notice new bugs when they came out. And such capabilities are dual use; defenders already have access to them and will be using the models to prevent their engineers from releasing new bugs.

There are lots of capabilities that are not like this, however:

- **Weaponizing recently patched exploits for common software.** Right now, for widely used C projects, we get enough publicly disclosed vulnerabilities to develop exploits with. Every amateur computer hacker has had the experience of seeing a CVE for a version number currently in use by a service, getting excited, and being surprised when it's totally useless.  
	  
	Part of that is because lots of CVEs are inflated, but part of it is just that modern memory protections mean that it's months of hard work to actually exploit these "high" severity CVEs for your favorite product. But AI reduces that down to hours, and [will even help you with worm development if you want](https://web.archive.org/web/20260512174712/https://github.com/g00dfe11ow/Shai-Hulud-Open-Source). If the output of "stop-the-presses" vulnerabilities for SaaS vendors slows down to its 2025 cadence, but each such vulnerability is now exploited in the wild as soon as open source projects ship a patch, that seems like a lasting loss for defense.
- **AI-enabled social engineering.** Right now black hat groups can only run really sophisticated, long term compromise attempts on Guillermo Rauch. But when the bottleneck for conducting such attacks is no longer labor, and the price of intelligence gets low enough, they can and will begin elaborate campaigns to scam and hack more ordinary people. The ease with which attackers will soon be able to generate high fidelity internet legacies, and the amount of apparent effort they will be able to put in creating relationships with marks, will break a lot of peoples' assumptions about trust over the internet at the same time - especially normies who do not read or care much about AI, and might be behind the times on what people can do.
- **"Post-exploitation", or "the stuff attackers do after they already have access to a given target and can begin exploiting their resources, public projects, etc."**, is IMO the most important risk. There is a fundamental logistical problem that every botnet operator throughout history has run into called "command and control", or roughly, "how to maintain control over and reap rewards from all of the stuff you've pwned." It used to be that the worst thing these people could do was launch DDoS attacks against a particular target, or send spam email, or scrape for crypto and credit cards, because even if you manage to create a worm that spreads over the internet, you can't personally review every individually owned laptop for goodies.  
	  
	But if you put your sociopath goggles on, the average software engineer sure has access to a lot of software repositories that *could in principle* be leveraged for further attacks, along with many online accounts & emails with which to abuse trust relationships. With sufficiently intelligent post exploitation, an AI could probably hop from that software engineer to >2 close friends with similar access and keep going, actively hacking each target until a large percentage of the wider graph is compromised. And once it is, AIs can be a lot more strategic & effective about making money from each target in the most profitable way.

These vectors, which have already gotten worse over the last six months, will become a more pressing issue over the next 24 months, and are more important causes for concern than vulnerability research, in part because they have no obvious solutions like vulnerability research does.

\[Thanks to Chris Hacking (real name) for talking through some of these ideas in conversation with me\]