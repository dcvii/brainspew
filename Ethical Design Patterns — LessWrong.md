---
title: "Ethical Design Patterns — LessWrong"
source: "https://www.lesswrong.com/posts/E9CyhJWBjzoXritRJ/ethical-design-patterns-1%5D"
author:
  - "[[AnnaSalamon]]"
published: 2025-09-30
created: 2025-10-13
description: "Related to: Commonsense Good, Creative Good (and my comment); Ethical Injunctions. …"
tags:
  - "clippings"
---
Related to: [Commonsense Good, Creative Good](https://www.lesswrong.com/posts/cEnJsoxQ3ziJEohnP/commonsense-good-creative-good) (and [my comment](https://www.lesswrong.com/posts/cEnJsoxQ3ziJEohnP/commonsense-good-creative-good?commentId=c8EKsfhv9wqhPtqgD)); [Ethical Injunctions](https://old-wiki.lesswrong.com/w139/index.php?title=Ethical_injunction&_ga=2.261354573.191592178.1758319709-847014459.1552449575).

*Epistemic status: I’m fairly sure “ethics” does useful work in building human structures that work. My current explanations of* how *are wordy; I think there should be a briefer way to conceptualize it; I hope you guys help me with that.*

## Introduction

It is intractable to write large, good software applications via spaghetti code – but it’s comparatively tractable using design patterns (plus coding style, attention to good/bad codesmell, etc.).

I’ll argue it is similarly intractable to have predictably positive effects on large-scale human stuff if you try it via straight consequentialism – but it is comparatively tractable if you use ethical heuristics, which I’ll call “ethical design patterns,” to create situations that are easier to reason about. Many of these heuristics are honed by long tradition (eg “tell the truth”; “be kind”), but sometimes people successfully craft new “ethical design patterns” fitted to a new circumstance, such as “don’t drink and drive.”

I will close with a discussion of what I think it would take to craft solid ethical heuristics near AI development, and to be able to thereby put energy into AI safety efforts in a way that is less in a fight with others’ desires to avoid totalitarianism, economic downturns, or other bad things.

## Intuitions and ground truth in math, physics, coding

We humans navigate mostly by intuition.[^1] We can do this, not because our intuitions match up with the world from birth (they mostly don’t), but because:

1. We check our intuitions against data, and revise those that make wrong predictions; and
2. We design our built world to be intuitively navigable.

I’ll spell this out a bit more in the case of math, physics, and coding. Then, with this example in hand, I'll head to ethics.

## We revise our intuitions to match the world. Via deliberate work.

Humans predict math and physics using informal/intuitive guesswork (mostly) and observation and formal proof (occasionally, but with higher credibility when we do check).

How do we get good-enough intuitions to make this work? Partly, we start with them: humans have some intuition-reality match from the get-go. Partly, we revise them fairly automatically with experience, as we play around and "get a feel for things."

But also, partly, we revise them on purpose, with full verbal consciousness: great physicists from [Archimedes](https://www.karlin.mff.cuni.cz/~halas/WSHM/Teziste-dukazy.pdf) to [Galileo](https://www.reed.edu/math-stats/wieting/mathematics537/Dialogue1.pdf) to [Einstein](https://users.physics.ox.ac.uk/~rtaylor/teaching/specrel.pdf) have pointed out incoherences in our starting intuitions about physics, and have actively worked to help us set up new ones. Good teachers enjoin students [to acquire good intuitions on purpose](https://enlightenedidiot.net/random/feynman-on-brazilian-education-system/), and help show how.[^2] [^3]

Intuitions are deliberately crafted parts of a scientist's power.

## We design our built world to be intuitively accessible

In addition to revising our intuitions to better match what’s true, we also design "what's true" (in our built world, where we can) to be more intuitive. This happens even in math (which I might've thought "isn't built"): in math, we search out terms, definitions, etc that will make math's patterns intuitive.

For example, as a kid I wanted 1 to be considered a "prime;" it seemed initially more elegant to me. Maybe it seemed that way to early mathematicians too, for all I know! But it is in fact more elegant to exclude 1 from the set of "primes," so we can have "unique prime factorization". Mathematicians layered many many design choices like this to make it more natural for us to " [think like reality](https://www.lesswrong.com/posts/tWLFWAndSZSYN6rPB/think-like-reality)."

The same holds, in a more extreme way, for coding large software applications – many design choices are made in concert, using much cleverness and tradition, such that somehow: (a) the software can fit in one's head; and (b) one can often add to or change the software in ways that still leave it fitting in one's head (rather than the number of \[interactions to keep track of\] growing exponentially).

## Intuitions and ground truth in ethics

Most people, in our personal lives, make at least some use of ethical heuristics such as “tell the truth,” “be kind,” “don’t drink and drive.”

Also, many human organizations (especially large, long-lasting ones) make use of “ethical design patterns” such as “let promotion and pay increases be allocated fairly, and be linked to high-quality work.”

What process produces these “ethical heuristics”?

## We revise our ethical intuitions to predict which actions we’ll be glad of, long-term

So, I unfortunately do not fully know what process produces our ethical heuristics, and even insofar as I do know, the answer is partly “it’s complicated.” [^4] But part of it is: we sometimes act in a manner that is either: (a) saliently guided by a traditional ethical heuristic, such as “tell the truth”; or (b) saliently in violation of a traditional ethical heuristic, such as “tell the truth.” Later, we notice our action's impacts (what happened to us, to other parties, to our relationships) and aftertastes (how it feels in us). And, if we like/dislike these impacts and aftertastes, we adjust our trust in this heuristic upward or downward – especially if, after meditating on the example, we come to understand a “physics” that would systematically produce results like the one we observed.

“Tell the truth,” for example, is often passed to children with accompanying reasons: “so people will trust you,” “so you’ll feel good about yourself,” “so you’ll become a person of good character,” “so you can have real friends and allies.” This makes it easier for the kid to track whether the heuristic is paying rent, and to update toward it insofar as it’s valid.

To give a different sort of example: communism was plausible to many intellectuals in the early 1900’s, and I found “ [The Internationale](https://www.youtube.com/watch?v=9LbziknNpCE) ” (a communist anthem) ethically and aesthetically attractive when I first heard it as a teen. But after studying the history of the Soviet Union, my intuitive reaction to this music became more wary.

## Ethics helps us build navigable human contexts

Human cities, with their many purposes and people and associations, are even more complicated than large software projects.

Perhaps relatedly, many actions among humans can “backfire” from their intended result, to the point where it’s hard to predict the sign of one’s effect. For example:

- Political assassinations often have unintended, hard-to-predict effects;
- Trying to pressure or manipulate a family member into a particular action/viewpoint may well backfire;
- Trying to pressure or manipulate a large segment of the public into a particular action/viewpoint (via a well-funded campaign of some sort) may well backfire;
- Attempts to make a thing more affordable via price controls typically backfire.
- Efforts to reduce covid deaths via covid vaccines and mask mandates seem to have had mixed effects.
- And, to pick the example I most care about: efforts to decrease existential risk from AI [seem AFAICT](https://x.com/AnnaWSalamon/status/1793719602792497298) to have backfired fairly often.[^5]

Interestingly, though, many things *aren’t* tangled and confusing in this way.

Some places where people mostly *can* act, with predictable results:

- People can mostly do what we like with our own property. Eg I wanted tea, so I bought tea, and now I predictably have tea and can make myself tea when I want to.
- People can often locate and share factual information, especially in non-politicized contexts. Eg most scientific work.
- People can often make friends, and can do things with their friend that please both parties.
- People can sometimes create community infrastructure that they and others want, on purpose (eg park clean-up campaigns; volunteer fire departments in small towns; bake sales for kids' sports; ultimate frisbee meet-ups).
- When “rule of law” is working well, people can often start businesses, and can expand those businesses where they manage to locate a profitable niche. (In contrast, in countries without much rule of law, expanding businesses generally face a need to bribe more and more officials, to the point where they often can’t exist/expand.)

AFAICT, the above are all areas where a person can usually pursue what they want without getting much in the way of what somebody else wants. This greatly reduces the odds of backfire.

How did it come about, that people can act in the above ways without tangling with somebody else’s plans? Via deliberate ethical design work, I think. For example, “property rights” were worked out on purpose (via “don’t steal,” patterns for disincentivizing stealing, patterns for making it clear whose property is whose, etc.), and this is how it came about that my tea-getting plans predictably didn’t tangle with anyone else’s plans.

## We use "ethical design patterns" to create institutions that can stay true to a purpose

To see this design work more sharply, consider institution design. Suppose, for concreteness, that you would like to build a postal service (and suppose you’re a bureaucrat of enormous power, who has a shot at this). You want your postal service to deliver mail well, and to stay true to this purpose for a long time.

How do you do this? You employ some standard-issue ethical design patterns:

- You choose a clear, simple purpose (“deliver mail cheaply and reliably”) that everyone in and out of the organization can see as valuable.
- You take the time to locate and spread an especially memorable phrasing of this purpose. Perhaps via rhyme or alliteration.
- You work to create a culture of visibly fair and outcome-linked hiring, pay, and promotion.
- You work to incentivize honesty and accurate tracking, several ways:
	- Getting many people many places to say honesty is valuable.
	- Making things easy to measure (with many sets of eyes who can double-check).
	- Whistleblower policies.
	- Making a negative example of those who lie or distort the tracking data, and a positive example of those who speak up about it.
- You work to create a culture within the postal service where staff are kind and respectful to one another (because it'll be easier for staff who are well-treated by their fellows to care, vs being alienated and bitter), and where staff care about the postal service’s success.
- By these and other means, you could try to create a context where:
	- Many, varied people can easily tell which parts of the postal service are working well/poorly, and can see eye to eye about it;
	- Individual staff members’ goals align with one another, with the postal service’s mission, and with the postal service’s continued existence and funding;
	- The postal service is fairly robust to a small number of incompetents, bad actors, or other trouble; it has an ability to recover.

Insofar as you succeed in this design work, you’ll create a context where an individual postal worker can be wholehearted about their work: the thing that is good for them personally will also be good for the postal service, and vice versa (at least mostly). You’ll also create a context where the postal service as a whole can be mostly in alignment with itself as it heads toward or away from particular changes that would make it better/worse.

(Without such ethical design work, the postal service would be more likely to degenerate into bureaucratic politics in which some parties gain local power, and set up feifdoms, at the expense of the organization as a whole.)

## Ethics as a pattern language for aligning mesaoptimizers

More generally, it seems to me that ethical heuristics can be seen as a pattern language for causing “mesaoptimizers” within a person, and “mesaoptimizers” that arise in the politics across people, to direct their energies in a way that benefits both the mesa-optimizer in question, and:

- the person as a whole;
- the person’s workplace, eg the postal service;
- the person’s family;
- the person’s nation; etc.

“Ethics,” here, is not an unchanging list of rules that the institution-designer should always obey, any more than design patterns in computer science are a list of rules to always obey. It’s a [pattern language](https://en.wikipedia.org/wiki/Pattern_language), honed over long experience, with patterns that work best when selected for and tailored to context.

## Examples: several successfully crafted ethical heuristics, and several “gaps”

## Example of a well-crafted ethical heuristic: “Don’t drink and drive”

In the case of drunk driving, “Mothers Against Drunk Driving” (MADD) did a lot to create and propagate visceral heuristics that made it “obvious at a glance” that people shouldn’t drink and drive. They imbued these in phrases such as:

- “Drunk driver” (calls to mind: vice; irresponsibility; recklessness; stories of innocents being killed)
- “Friends don’t let friends drive drunk” (calls to mind: caring about the would-be drunk driver; being upright relative to surrounding society)
- “Give me your keys” / “Can you walk in a straight line?” (less offensive, because of the above; prior to MADD’s efforts this would have been more of a personal power struggle)
- “Designated driver”(helped bridge between “don’t drink and drive” and conflicting “but how else can we get home?” intuitions)

After MADD’s work, it became easier to be wholeheartedly against drunk driving (vs feeling conflicted, where your desire to avoid tension with your friends was in conflict with your fear that they’d kill someone, say); it also became more likely that a person’s self-interest near questions of drinking and driving would line up with what was good for others (via laws punishing drunk drivers; via laws making bartenders sometimes responsible for drunk drivers; via social heuristics causing disapproval for driving drunk and approval for those who help prevent it; etc).

## Example of well-crafted ethical heuristic: “Earning to give”

The phrase “earning to give” (and the EA community’s support of this phrase) makes it viscerally obvious how a person in eg finance expects to make the world better. This makes it easier for a person to do such work wholeheartedly, and easier for the EA community to feel visceral approval for people doing such work.

## A partial example: YIMBY

I’ve been mostly-impressed with the YIMBY movement’s crafting of ethical heuristics, although it is recent and has not yet produced deeply-embedded ethical heuristics on the level of MADD. Relevant ethical intuitions it has produced (at least some places):

- Visceral indignation at the plight of young families who can’t afford a home;
- Visceral horror/disgust at cities that forbid building (since they're depriving young families of housing);
- Understanding that “if you build more housing, prices drop”
- Understanding that lower housing prices is good, helps build abundance.

These intuitions could use pithy phrases. They could use more embedded obviousness, and more spread. They could use more synthesis with potentially conflicting intuitions about upsides of zoning, and about how falling house-prices will be costly for existing homeowners’ life savings. But it’s on path.

I can tell it’s on path not only because it’s producing some of the house-construction change it’s after, but because it isn’t particularly polarizing, and it seems to be moving many peoples’ intuitions in a quiet, non-dramatic way (“huh, yeah, it *is* good if people can afford housing”).

## A historical example of gap in folks’ ethical heuristics: Handwashing and “childbed fever”

I'd like also to look in some detail at situations where people *didn't* have adequate ethical heuristics.

In 1840s Vienna, Ignaz Semmelweis became justifiably confident (via experimentation and an abundance of data) that the ~7% death rate among delivering mothers could be greatly reduced if doctors would wash their hands in a chlorinated lime solution. This claim was difficult to assimilate within Viennese society at the time.

We can tell this claim was hard to assimilate sanely, because:

- Despite the strength of his evidence, Semmelweis’s extensive and iterated efforts to communicate this point did not result in the hospital adopting handwashing. Rather, it resulted in Semmelweis being fired.
- When Semmelweis continued to try to communicate, he apparently became both “more loudly ignored” and more agitated. Eventually, many claimed he was crazy, including sort of his wife, and he was forcibly involuntarily committed and died two weeks later of gangrene, probably as a result of being beaten while being captured.
- Most tellingly, from my POV: one of the few doctors who took Semmelweis’s claims seriously, Gustav Michaelis, later killed himself out of guilt for he had probably previously caused the deaths of many delivering mothers, including his cousin.

([Source: Wikipedia](https://en.wikipedia.org/wiki/Ignaz_Semmelweis))

You might ask why I say “the claim was hard to assimilate sanely” rather than, say, “the Viennese establishment pursued their (corrupt) interests sanely but sadly.” One reason is that Semmelweis and Michaelis seem also to have had trouble acting sanely (even premised on the medical establishment acting as it did).

You might also ask why I believe the difficulty assimilating the claim was partly an ethics gap. Partly, the difficulty assimilating Semmelweis’s claim was because germ theory wasn’t yet known (which I'd call a "science gap," not an "ethics gap"). Semmelweis's data should have been persuasive anyhow, since the effect size was huge, the number of patients was huge, and it would've been low-cost for skeptical doctors to try handwashing for a month and count patient deaths. But I expect the science gap made it easier for people to not-see the effect (if they wanted to avoid seeing it), and harder for people to form common knowledge about it (even where they wanted to). So I expect the science gap made it harder for ethics to work here.

Still, most peoples’ guesses (and mine, though I’m fairly uninformed) is that people found it difficult to socially metabolize “high-prestige Viennese doctors have been causing patients’ deaths, via being unclean”, for reasons that were at least partly about social and ethical templates and power structures.

Rephrasing: my guess is that the 1840’s Viennese people mostly tried not to see part of what they could see, and/or mostly tried not to care about part of what they cared about, because they did not know how to look and care about everything all at once. Particularly not in public. Relatedly, I suspect many [flinched from](https://www.lesswrong.com/posts/EFQ3F6kmt4WHXRqik/ugh-fields) tradeoffs they found agonizing, e.g. “shall I ignore that doctors may be killing people, or be loud about how my doctor friends are maybe so bad they should be shunned / should maybe kill themselves, even though I’m not sure?”

They were in a context that had not yet been engineered to work well with their intuitions.

Next, I’d like to look in some detail at a situation where I believe our own time and place lacks adequate ethical heuristics. This example will make it harder for us to avoid being “mindkilled”, and it brings some risk of getting into a social battle within LW or with distant others. But I’d like to give us a chance to experience all this from the inside, before I go on to the (still more difficult, IMO) situation around AI development.

The example I pick: public discussion of group differences.

The tricky thing about group differences discussion, it seems to me, is that there are two ethical heuristics that each pay some rent, that we mostly do not know how to care about simultaneously. Namely:

*Heuristic A: Avoid speech that may inflame racism.*

- Many practice and endorse an ethical heuristic against drawing attention to particular differences in group outcomes, or similar, lest such attention inflame racial hatred or ethnonationalism.

*Heuristic B: Allow free inquiry and conversation everywhere, especially anywhere important that’s widely specifically-not-discussed; talk about any “elephant in the room.”*

- Many practice and endorse ethical heuristics against the censure of speech on any topic, especially any salient and politically relevant topic, lest such censure mess with our love of truth, or our ability to locate good policy options via the free and full exchange of ideas, or our freedom/autonomy/self-respect broadly.

What do people normally do when two rent-paying ethical heuristics collide? Such collisions happen often: there are situations where it’s difficult to be fully honest and fully kind at once (at a given skill-level), or to fully simultaneously adhere to almost any other pair of useful ethical heuristics.

To help navigate such collisions, people have created a huge number of “bridging” ethical heuristics, which prescribe how to respond when two valued ethical heuristics can’t both be followed at once. Sometimes, these bridging heuristics involve one heuristic overriding the other within a delimited region, as with a “white lie,” or with “ [pikuach nefesh](https://en.wikipedia.org/wiki/Pikuach_nefesh) ” (a rule in Judaism that one should break the Sabbath, and many other rules, if it might save a life). Some other times, the bridging heuristic states that a given case is officially a “judgment call” in which a responsible party is supposed to weigh several goods against the circumstances, according to their their individual judgment.[^6]

Regardless, **the crucial feature of a “bridging” ethical heuristic is that it allows the two heuristics** (if we understand these heuristics as memes, with their own ~agency) **to peaceably share power, and to support one another's continued existence.** It’s a bit like a property line: both memetic neighbors can support one another's validity in particular regions, without a “war of all against all.” Humans who care about Heuristic *A* and humans who care about Heuristic *B* can see eye to eye around the bridging heuristic, and can appreciate one another's reasonability. **A “bridging heuristic” is thus the opposite of a** [**scissors statement**](https://www.lesswrong.com/w/scissors-statements)**.**

Several symptoms convince me that I, and many relevant “we”s, have insufficient ethical heuristics to be sane about how to speak publicly about group differences – and, more exactly, that we lack an adequate bridging heuristic between ethical heuristics *A* and *B*:

- It’s hard to have a conversation on this topic in mixed company. When people try, they sometimes run into “ [scissors statements](https://www.lesswrong.com/w/scissors-statements),” analogous to [the conversation that destroyed New Atheism](https://en.wikipedia.org/wiki/Rebecca_Watson#%22Elevatorgate%22).
- I noticed the gap in my own heuristics in ~2014, when a friend asked me to comment privately on their draft public writing, and, despite my endorsed belief that long-term goodness in a democracy requires free inquiry on all topics, and despite my friend’s writing being polite and reasonable AFAICT… I still noticed my heart wasn’t fully on board. To endorse my friend’s writing, I found myself dissociating a little, or having a “ [missing mood](https://www.econlib.org/archives/2016/01/the_invisible_t.html).” (My phrasing at the time: “Huh, wokism has somehow captured the narrative high ground… even in my own heart, even though I disagree with it?”) [^7]
- Single-culture groups do sometimes have a fairly easy time having conversations on the topic… but in my limited experience the group often has a “missing mood” of one sort or another, and, if they have an easy time discussing heuristic *A*, often mostly-omit discussion of *B*; or vice versa.
- Since 2014, it is both the case that taboos against non-Woke speech have become less universal, and the case that ethnonationalism has (I think?) become considerably more prominent, which I take as at least limited evidence that such heuristic *A* was paying rent.
- Across many years, I’ve sometimes watched people (reasonable people, normally sane people) seem oddly triggered (oddly non-agentic / self-defeating / something) when they tried to speak in public on the topic.[^8]

So, I think many of us (and especially, many polities taken as a whole) are missing an adequate set of ethical heuristics to allow our viscera, hearts, minds, etc to all orient sanely about all of what matters near public discussion of group differences.[^9]

## Gaps in our current ethical heuristics around AI development

Now for the hardest example, and the one I will get most wrong, despite having tried: let’s discuss what ethical heuristics already help us think sanely and publicly about AI development, and where the gaps are.

To review: my claim is that an adequate set of ethical heuristics here would allow us to:

- i)Take in all “obvious” info, without needing to be willfully blind anywhere;
- ii) Care about everything worth caring about, without needing to be willfully indifferent or have a “missing mood” anywhere.

They would also help us create group contexts where:

- iii) Our visceral perceptions of what’s good mostly line up with our explicit calculations about what’s good;
- iv) One can discuss things easily in public without running into scissors statements;
- v) The incentives on individuals, and on political and memetic actors, mostly line up with what’s long-term good for lots of people;
- vi) We can act to try to cause better long-term outcomes from AI (if we want to) without large risks of backfire.

(Why should it be possible to find ethical heuristics that do all or most of the above at once? I don’t fully know. But I believe from examples in other ethical domains that it generally is possible. I don’t fully know why design patterns are often viable in coding, either.)

## Existing progress

Here are some ethical heuristics that’re already worked out (and are new in the last couple decades), that I think help.

- “Many top researchers and industry-leaders assign double-digit chances that building AI will cause human extinction”.
	- This helps because it's obviously true, whereas "there is risk" is not *obviously* true in an NPOV sense.
	- And so it provides a fact *everyone* can see, that other bits of policy discussion can reference.
- Katja’s post [Let’s think about slowing down AI](https://www.lesswrong.com/posts/uFNgRumrDTpBfQGrs/let-s-think-about-slowing-down-ai), in which she argues that, if we think AI has a good chance at destroying the world, maybe we should be trying to slow it down.
	- Weirdly, this position was AFAICT mostly outside the Overton window until Katja posted it in late 2022, partly because at the time it was somehow harder to hold the ethical heuristic “maybe we should root for the not-building of a thing that might kill us all” at the same time as the ethical heuristics “murder \[including of AI researchers\] is bad,” “totalitarianism is bad,” and “don’t create conflict with your friends \[who may work at AI companies\].” Katja’s essay goes into detail on how these pairs of ethical heuristics can be bridged, linking each bit up to mundane ethical common sense, and I suspect her efforts to bridge ethical heuristics are a good chunk of why her essay was able to move the Overton window.
	- I'm putting her post in my "examples of progress toward adequate ethical heuristics" because of the bridging work she did within the essay, and because I could see the effect that work had on enabling grounded public discussions.
- “ [Safetywashing](https://www.lesswrong.com/posts/xhD6SHAAE9ghKZ9HS/safetywashing) ” (by analogy to “greenwashing”)
- The notion that one should often do good, normal human things while caring about AI risk, as in [this quote by CS Lewis](https://fscsmn.org/email-article/very-applicable-to-today-written-by-cs-lewis-in-1948/) or [this blog post by me](https://www.lesswrong.com/posts/mmHctwkKjpvaQdC3c/what-should-you-change-in-response-to-an-emergency-and-ai).[^10]

I believe all four of these examples make our available ethical heuristics more "adequate" in the sense of *i-vi* above. (This is not an exhaustive list.)

## Where we still need progress

Here’s an ethical heuristic (at least, *I think* it’s an ethical heuristic) that I personally care about:

- *Heuristic C: “If something has a >10% chance of killing everyone according to most experts, we probably shouldn’t let companies build it.”*

IMO, it’s hard to get a consensus for Heuristic C at the moment *even though it kind of seems obvious.* It’s even hard for me to get my own brain to care wholeheartedly about this heuristic, to feel its full force, without a bunch of “wait, but …”.

Why?

I’m not sure, but I’d guess it’s at least partly because we lack good “bridging heuristics” between Heuristic C and some other key ethical heuristics. Such that people go to try to affirm *C* (or to endorse people/movements who affirm C) but then hesitate, because they’re afraid that heuristic C will gather a bunch of social momentum, and then trample something else that matters.

In particular, I’ve heard many (including many I respect) speak against *C* because they fear  *C* will damage some of these heuristics:

- *Heuristic D: “Do not seek centralized/governmental control of technology, nor of the free flow of scientific research, lest you enable totalitarianism or other abuses.”*
	- Governments are unaligned optimizers; if you summon a government by checking that it “says it’ll help you with X”, you may well get one that is doing alignment faking and is using your movement as a fig leaf to consolidate power. See the history of communism, which did not in fact help poor people.
- *Heuristic E: “Be on the side of progress – of people getting things they want, of economic activity, and of people learning stuff they want to learn and acquiring more capacity.”*
	- Do this not only for the object-level good stuff it’ll create, but also because:
		- It’ll help you become capable – you’ll learn to build, you’ll make friends with people who’re making neat stuff
		- It’ll help you root for people, have good values, be on the side of life.
	- If you ever stop practicing heuristic D, expect both your skills/energy and your heart to be badly damaged.
- *Heuristic F: “Give serious positive consideration to any technology that many believe might save billions of lives.”*
- *Heuristic H: “Do not try to personally control the whole universe; seek rather to team up, and to split the gains from trade. Relatedly, do not fear the freedom of other sentient actors, but seek rather to ally yourself with their freedom.”*
- *Heuristic I: “If faced with an alien intelligence that isn’t immediately dangerous, such as today’s LLMs, try to get to know it, and to play around a lot in friendly ways if you can safely do so, rather than allowing yourself to fear it and to keep it at a distance only.”*

For example, Peter Thiel [worries](https://sfstandard.com/2025/09/23/spilled-peter-thiel-s-antichrist-secrets-now-s-banned-lectures/) existential risks will be used as an excuse for an anti-progress totalitarian government to seize power. (Heuristics *D*, *E*, *F*, I think.)

Alexandros Marinos (a long-time LWer who I respect, and who used to be into LW/MIRI-style safety efforts) opposes these efforts now, arguing that LWers are naive about how governmental power seizure works, that AI safety can be used as a fig leaf for power the government wants anyhow, that governmental involvement increases risk, and that AI is already partway through its takeoff and LWers aren't paying attention. ([One tweet](https://x.com/alexandrosM/status/1707442305991602386); but his views are scattered across many.) Alexandros’s views seem to me to be a combination of  *D* and  *I*, mostly.

(I think I’ve seen many other examples, from both thinkers I respect and randos on *X*, that I classed in these ways – but I’m low on time and want to post and have had trouble tracking these down, so perhaps I’m wrong about how common this is, or perhaps it really is common and some of you will post examples in the comments?)

## Can we “just ignore” the less-important heuristics, in favor of ‘don’t die’?

We *could* try to work out "bridging heuristics", to allow heuristic *C* to co-exist stably with heuristics *D/E/F/G/H*. But, how badly do we need such bridges?

That is: In the absence of such heuristics, how well does it work to say: "Heuristic *C* is more important than the others, so, if we can't honor all the heuristics, let's make sure we honor *C*, at least"?

It seems to me that while a person *can* say that (and while it might sometimes be the best path, even), there are large costs. Here's my attempt to list these costs (I'm focusing here on totalitarianism *(D)*, for readability, but I could write exactly analogous sentences about other heuristics). If we proceed without bridging heuristics:

- We increase the odds of totalitarianism
	- (And we do so more than necessary, because without bridging heuristics it's hard for an AI safety movement to care properly about the costs of slightly-increased totalitarianism) [^11]
- Some who hate totalitarianism will oppose AI safety efforts (maybe extra, a la motive ambiguity and runaway political dynamics on their side), which may make it harder for us to:
	- Arrive at an accurate shared picture of how safety risks work (since some opponents will treat arguments like soldiers, muddy our waters),
	- Oppose AI risk together,
	- Not have our efforts run into lots of unpredictable-to-us "backfire effects".
- The part of our own hearts which hates totalitarianism will be less on board with AI safety work, which will make us worse at it, in two senses:
	- We'll have less energy for it;
	- We'll be stupider about it (because we won't have as much of our mind engaged).
- In the course of deciding not to oppose totalitarianism here, we may lose track of some useful, rent-paying ethical patterns that are somehow “entangled with” the anti-totalitarianism heuristics. Eg it may become harder for AI safety advocates to respect and value human freedom even where we *can* afford to respect it. (I.e., we may partake slightly of [anti-epistemology](https://www.lesswrong.com/w/anti-epistemology), or of its companion "anti-caring.") [^12]
- Folks who want totalitarianism for other (bad, power-seeking) reasons may find AI safety a useful “cover story” with which to consolidate power – and AI safety advocates may mistake such folks for actual allies, and help hand power to forces who cannot understand or protect or care about AI safety.

I suspect there are analogous costs to failing to synthesize other key ethical heuristics, also.

## These “gaps” are in principle bridgeable

Most pairs of ethical heuristics contradict one another sometimes – it is sometimes challenging to be both honest and kind at once, etc.

Still, many ethical heuristics get along with one another just fine, with the aid of “bridging heuristics,” as discussed earlier.

I would bet at decent odds that the tension currently existing between proponents of heuristic C, and proponents of D/E/F/G/H/I, is not a necessary thing, and can be eased with some sort of additional work (work I imagine many are already in progress on). That is, I suspect it is humanly possible to care about all the good things at once, and to take in all the obvious truths at once, without "missing moods" -- if it's currently hard to fit in all our heads all at once, we can locate stories and examples that make "here's one way we could care about all of it" concrete.

I also think there's been good continuing work on such bridging heuristics for as long as there's been an AI safety movement; I'm writing this essay to try to bring a bit more theory or explicit modeling to a thing that is probably already on many todo lists, not to introduce a whole new project. On this note, I quite enjoyed Joe Carlsmith's series [On Otherness and Control in the Age of AGI](https://www.lesswrong.com/s/BbAvHtorCZqp97X9W), and believe he is chipping away at the Heuristic C/ Heuristic H collision.

That said, many domains (such as Covid policy) seem to get more scissors-y rather than bridgey.

To restate my main thesis: I think *ethical design patterns are a pattern language for aligning mesaoptimizers*, including mesaoptimizers within a human, and mesaoptimizers within a set of human politics, so as to get functional human structures (such as a postal service that delivers mail, rather than one that degenerates into politics; or a human being who has [something to protect](https://www.lesswrong.com/posts/SGR4GxFK7KmW7ckCB/something-to-protect), rather than one who's a random bag of impulses).

I most care about building functional human structures for not all dying of AI. But I also care about buildling functional human structures for various subproblems of this, such as "aggregating information sensibly about AI safety stuff."

One smaller puzzle, there, concerns the collision of these ethical heuristics:

- I) Take all arguments at face value; don't impune the motives of a fellow debater (even if they are taking money/compute/etc from the AI industry);
- II) If you are taking money/compute/etc from the AI industry, try not to alienate them unnecessarily (eg by talking about how a pause would be good);
- III) If lots of (smart/senior) people seem to dismiss an idea, assume there's something wrong with it \[even if most of the smart/senior people are doing local work that makes it locally disincentivized for them to seem not to dismiss that idea, eg because it would annoy Ai companies\].

I believe both that each of these three heuristics does useful work for us on average, and that their collisions have sometimes caused us to believe false things, as evidenced by eg [this exchange between me and Tomás B](https://www.lesswrong.com/posts/b7JXJWY7R2jNtHerP/slowing-down-ai-progress-is-an-underexplored-alignment?commentId=WLvhekENFaToodwp7). I worry also that they make us more manipulable by AI companies. Finding a way to keep most of the upsides of each heuristic, while not having our epistemics messed with, is an easier ethics puzzle, and still useful.

[^1]: In math, for example, mathematicians tend to guess which theorems are true before they can formally prove them, and they tend to guess which proof structures may work out before those proofs have been completed. (Navigating without intuitions, and doing instead a brute force search to locate proofs, would be impossibly slow, combinatorially slow.)

[^2]: If you’d like to get a taste of how this works, and haven’t, you might check out the book [Thinking Physics](https://www.amazon.com/Thinking-Physics-Understandable-Practical-Reality/dp/0935218084), which allows a reader to reason their own way to high school physics almost purely via riddles and thought experiments, with surprisingly little need of observations or of teachers' say-so.

[^3]: Anytime you find a place where your starting intuitions predict wrongly, you can dwell on it until you intuitions come to predict it rightly. I was taught this explicitly as a high school student, at Glenn Stevens’s [PROMYS](https://promys.org/about/) program; Prof. Stevens emphasized that after becoming confident we had proven a given conjecture, we should not stop, but should instead persist until we could “see at a glance” why the conjecture had to be true, ie until the new theorem's insight becomes an automatic part of one's visualized mathematical world. Eliezer [recommends similarly](https://www.lesswrong.com/posts/tWLFWAndSZSYN6rPB/think-like-reality) about physics.

[^4]: As an example of "it's complicated": adults have more memetic power than children, and I suspect this is part of why "honor your parents" is a more traditional piece of ethical advice than "cherish your children." There are probably many places received ethical heuristics are bent toward "that which advantages the ethics memes, or the meme-spreaders" rather than toward that which would aid the recipients of the meme.

[^5]: Richard Ngo [argues](https://x.com/RichardMCNgo/status/1810495607590543701) that achieving the opposite of one's intended effect is common among ideologies and activists.

[^6]: There are also other sorts of bridging heuristics. If the leader of a country sends soldiers into battle, he is expected to publicly honor those of his soldiers who die, to provide for those who become disabled, and to be careful not to lose their lives unnecessarily; this bridges between "countries should be able to defend themselves" and "lives are sacred." This is an example of a more complex and prescribed sharing of power between two heuristics.

[^7]: Conversely, when I refrained from other non-woke speech for fear of social reprisal, I tended also to dissociate a bit, with a different “missing mood.

[^8]: I caught up with a college friend after many years, and he told me he'd realized he's a "congenital comedian": "You know how everybody has sensors that detect what not to say, and make them not say it? Well, I have those too -- except the sign is reversed. This explains my life."  
  
"Congenital comedian" is the thing I've actually observed in some friends on this topic. For example, my friend "Bob" was once with me in a room full of near-strangers who he didn't want to make a bad impression on. And he said something slightly awkward that was slightly-near the topic of race and IQ. And then he tried to clarify, and made it worse, and tried again to clarify, and made it double worse, for like *four* iterations of trigger (without anybody else saying much of anything), while turning increasingly red.

[^9]: As an aside, I like Kelsey’s recent small ethical innovation, where she now advocates saying true things even when they aren’t important, and are likely to cause mild social annoyance/disapproval, so that they won’t only be said by people in other information bubbles. Discussed in the first half of [her recent dialog with Zack](https://www.lesswrong.com/posts/FaGaNhXhFEtXkfyud/interview-with-kelsey-piper-on-self-censorship-and-the-vibe).

[^10]: Eliezer and Nate’s new book is palpably compatible with this heuristic, IMO, which I appreciate. This makes me feel better about recommending their book to relatives, as I more expect that reading the book will be okay for my relatives. We can see here an example of better ethical heuristics improving incentive-alignment for different people: because IABIED contains this improved ethical heuristic, it’s more in my relatives’ interest to inform themselves about this part of the world (since they’ll be less wrecked by it), and it’s more in my interest to tell them about it.

[^11]: Cf [failing with abandon](https://www.lesswrong.com/posts/HpHnMEiHYzSZiYk6g/failing-with-abandon), [motive ambiguity](https://www.lesswrong.com/posts/L6Ktf952cwdMJnzWm/motive-ambiguity); the fact that [high-level actions do not screen off intent](https://www.lesswrong.com/posts/nAMwqFGHCQMhkqD6b/high-level-actions-don-t-screen-off-intent) and so if we can't properly care in our hearts about (totalitarianism-risk and death-risk at once, or whatever), we probably also can't fully act right.

[^12]: In anti-epistemology, part of epistemology becomes explicitly attacked by the planning self (“it’s wrong to want evidence, and right to have faith, about religion.”) I believe there is an anlogous phenomon that I call “anti-caring”, where part of one’s own caring becomes explicitly attacked by the planning self.