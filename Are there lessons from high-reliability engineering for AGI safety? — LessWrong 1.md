---
title: "Are there lessons from high-reliability engineering for AGI safety? — LessWrong"
source: "https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi"
author:
  - "[[Steven Byrnes]]"
published: 2026-02-02
created: 2026-02-26
description: "This post is partly a belated response to Joshua Achiam, currently OpenAI’s Head of Mission Alignment: …"
tags:
  - "brain_spew"
---
## 

[LESSWRONG](https://www.lesswrong.com/)

[LW](https://www.lesswrong.com/)[

Are there lessons from high-reliability engineering for AGI safety?

](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#)

10 min read

•

[1\. My qualifications (such as they are)](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#1__My_qualifications__such_as_they_are_)

•

[2\. High-reliability engineering in brief](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#2__High_reliability_engineering_in_brief)

•

[3\. Is any of this applicable to AGI safety?](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#3__Is_any_of_this_applicable_to_AGI_safety_)

•

[3.1 In one sense, no, obviously not](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#3_1_In_one_sense__no__obviously_not)

•

[3.2 In a different sense, yes, at least I sure as heck hope so eventually](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#3_2_In_a_different_sense__yes__at_least_I_sure_as_heck_hope_so_eventually)

•

[4\. Optional bonus section: Possible objections & responses](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#4__Optional_bonus_section__Possible_objections___responses)

+[AI Safety Cases](https://www.lesswrong.com/w/ai-safety-cases)[Security Mindset](https://www.lesswrong.com/w/security-mindset)[AI](https://www.lesswrong.com/w/ai)[

Curated

](https://www.lesswrong.com/recommendations)

[2026 Top Fifty: 27%](https://manifold.markets/LessWrong/will-are-there-lessons-from-highrel)# 108

# [Are there lessons from high-reliability engineering for AGI safety?](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi)

by [Steven Byrnes](https://www.lesswrong.com/users/steve2152?from=post_header)

2nd Feb 2026

[AI Alignment Forum](https://alignmentforum.org/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi)

10 min read

[9](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#comments)# 108

# Ω 52

This post is partly a belated response to Joshua Achiam, currently OpenAI’s Head of Mission Alignment:

> If we adopt safety best practices that are common in other professional engineering fields, we'll get there … I consider myself one of the x-risk people, though I agree that most of them would reject my view on how to prevent it. I think the wholesale rejection of safety best practices from other fields is one of the dumbest mistakes that a group of otherwise very smart people has ever made. —[Joshua Achiam on Twitter, 2021](https://x.com/jachiam0/status/1370980495920533506)
> 
> “We just have to sit down and actually write a damn specification, even if it's like pulling teeth. It's the most important thing we could possibly do," said almost no one in the field of AGI alignment, sadly. … I'm picturing hundreds of pages of documentation describing, for various application areas, specific behaviors and acceptable error tolerances … —[Joshua Achiam on Twitter (partly talking to me), 2022](https://x.com/steve47285/status/1609232759100248066?s=20)

As a proud member of the group of “otherwise very smart people” making “one of the dumbest mistakes”, I will explain why I don’t think it’s a mistake. (Indeed, since 2022, some “x-risk people” *have* started working towards these kinds of specs, and I think *they’re* the ones making a mistake and wasting their time!)

At the same time, I’ll describe what I see as the kernel of truth in Joshua’s perspective, and why it should be seen as an indictment not of “x-risk people” but rather of OpenAI itself, along with all the other groups racing to develop AGI.

# 1\. My qualifications (such as they are)

I’m not *really* an expert on high-reliability engineering. But I worked from 2015-2021 as a physicist at [an engineering R&D firm](https://www.draper.com/), where many of my coworkers were working on building things that *really had to work* in exotic environments—things like [guidance systems for submarine-launched nuclear ICBMs](https://www.draper.com/market-areas/strategic-systems/navy-strategic-systems), or a [sensor & electronics package that needed to operate inside the sun’s corona](https://www.draper.com/media-center/featured-stories/detail/27373/touching-the-sun-with-the-parker-solar-probe).

To be clear, I wasn’t directly working on these kinds of “high-reliability engineering” projects. (I specialized instead in very-early-stage design and feasibility work for [dozens](https://sjbyrnes.com/pub_lidar_cleo_2020.pdf) [of](https://arxiv.org/abs/1804.06535) [weird](https://patents.google.com/patent/US10157692B2/) [system](https://doi.org/10.1364/OE.381575) [concepts](https://patents.google.com/patent/US20200020501A1/en) and associated algorithms.) But my coworkers *were* doing those projects, and over those five years I gained some familiarity with what they were doing on a day-to-day basis and how.

…So yeah, I’m not really an “expert”. But as a [full-time AGI safety & alignment researcher since 2021](https://sjbyrnes.com/agi.html), I’m plausibly among the [“Pareto Best In The World”](https://www.lesswrong.com/posts/XvN2QQpKTuEzgkZHY/being-the-pareto-best-in-the-world)™ at simultaneously understanding both high-reliability engineering best practices and AGI safety & alignment. So here goes!

# 2\. High-reliability engineering in brief

Basically, the idea is:

- You understand exactly what the thing is supposed to be doing, in every situation that you care about.
- You understand exactly what situations (environment) the thing needs to work in—temperatures, vibrations, loads, stresses, adversaries trying to mess it up, etc.
- You have a deep understanding of how the thing works, in the form of models that reliably and legibly flow up from component tolerances etc. to headline performance. And these models firmly predict that the thing is going to work.
	- (The models also incorporate the probability and consequences of component failures etc.—so it usually follows that the thing needs redundancy, fault tolerance, engineering margins, periodic inspections, etc.)
- Those models are compared to a wide variety of both detailed numerical simulations (e.g. [finite element analysis](https://en.wikipedia.org/wiki/Finite_element_method)) and physical (laboratory) tests. These tests are designed not to “pass or fail” but rather to spit out tons of data, allowing a wide array of quantitative comparisons with the models, thus surfacing unknown unknowns that the models might be leaving out.
	- For example, a space project might do vibration tests, centrifuge tests, vacuum tests, radiation exposure, high temperature, low temperature, temperature gradients, and so on.
- Even after all that, nobody *really* counts on the thing working until there have been realistic full-scale tests, which again not only “pass” but also spit out a ton of measurements that all quantitatively match expectations based on the deep understanding of the system.
	- (However, I certainly witnessed good conscientious teams make novel things that worked perfectly on the first realistic full-scale attempt—for example, the [Parker Solar Probe component](https://www.draper.com/media-center/featured-stories/detail/27373/touching-the-sun-with-the-parker-solar-probe) worked great, even though they obviously could not do trial-runs of their exact device in outer space, let alone inside the solar corona.)
- When building the actual thing—assembling the components and writing the code—there’s scrupulous attention to detail, involving various somewhat-onerous systems with lots of box-checking to make sure that nothing slips through the cracks. There would also be testing and inspections as you build it up from components, to sub-assemblies, to the final product. Often specialized software products like [IBM DOORS](https://en.wikipedia.org/wiki/DOORS) are involved. For software, the terms of art are [“verification & validation”](https://en.wikipedia.org/wiki/Software_verification_and_validation), which refer respectively to systematically comparing the code to the design spec, and the design spec to the real-world requirements and expectations.
- And these systems need to be supported at the personnel level and at the organizational level. The former involves competent people who understand the stakes and care deeply about getting things right even when nobody is watching. The latter involves things like deep analysis of faults and near-misses, red-teaming, and so on. This often applies also to vendors, subcontractors, etc.

# 3\. Is any of this applicable to AGI safety?

## 3.1 In one sense, no, obviously not

Let’s say I had a single top-human-level-intelligence AGI, and I wanted to make $250B with it. Well, hmm, Jeff Bezos used his brain to make $250B, so an obvious thing I could do is have my AGI do what Jeff Bezos did, i.e. go off and autonomously found, grow, and run an innovative company.

(If you get off the train here, then see my discussion of [“Will almost all future companies eventually be founded and run by autonomous AGIs?” at this link](https://www.lesswrong.com/posts/LJD4C7KAr64onL8fq/response-to-dileep-george-agi-safety-warrants-planning-ahead#3_2_On__keeping_strong_AI_as_a_tool__not_a_successor___Will_almost_all_future_companies_eventually_be_founded_and_run_by_autonomous_AGIs_).)

Now look at that bulleted list above, and think about how it would apply here. For example: *“You understand exactly what the thing is supposed to be doing, in every situation that you care about.”*

No way.

At my old engineering R&D firm, we knew *exactly* what such-and-such subsystem was supposed to do: it was supposed to output a measurement of Quantity *X*, every *Y* milliseconds, with no more than noise *Z* and drift *W*, so long as it remains within such-and-such environmental parameters. Likewise, a bridge designer knows *exactly* what a bridge is supposed to do: not fall down, nor sway and vibrate more than amplitude *V* under traffic load *U* and wind conditions *T* etc.

…OK, and now what *exactly* is our “AGI Jeff Bezos” supposed to be doing at any given time?

Nobody knows!

Indeed, the fact that nobody knows is the whole point! That’s the very reason that an AGI Jeff Bezos can create so much value!

When Human Jeff Bezos started Amazon in 1994, he was obviously not handed a detailed spec for what to do in any possible situation, where following that spec would lead to the creation of a wildly successful e-commerce / cloud computing / streaming / advertising / logistics / smart speaker / Hollywood studio / etc. business. For example, in 1994, nobody, not Jeff Bezos himself, nor anyone else on Earth, knew how to run a modern cloud computing business, because indeed the very idea of “modern cloud computing business” didn’t exist yet! That business model only came to exist when Jeff Bezos (and his employees) invented it, years later.

By the same token, on any given random future day…

- Our AGI Jeff Bezos will be trying to perform a task that we can't currently imagine, using ideas and methods that don't currently exist.
- It will have an intuitive sense of what constitutes success (on this micro-task) that it learned from extensive idiosyncratic local experience, intuitions that a human would need years to replicate.
- The micro-task will advance some long-term plan that neither we nor even the AGI can yet dream of.
- This will be happening in the context of a broader world that may be radically different from what it is now.
- And our AGI Jeff Bezos (along with other AGIs around the world) will be making these kinds of decisions at a scale and speed that makes it laughably unrealistic for humans to be keeping tabs on whether these decisions are good or bad.

…And we’re gonna write a detailed spec for that, analogous to the specs for the sensor and bridge that I mentioned above? And we’re gonna ensure that the AGI will follow this spec by design?

No way. If you believe that, then I think you are utterly failing to imagine a world with actual AGI.

![2-column table contrasting properties of AI as we think of it today, with properties of future AGI that I'm thinking about](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/4basF9w9jaPZpoC8R/cziczguyma3nifu1x3th)

## 3.2 In a different sense, yes, at least I sure as heck hope so eventually

When we build actual AGI, it will be like a new intelligent species on Earth, and one which will eventually be dramatically faster, more numerous, and more competent than humans. If they want to wipe out humans and run the world by themselves, they’ll be able to. (For more on AGI extinction risk in general, see the [80,000 hours intro](https://80000hours.org/problem-profiles/risks-from-power-seeking-ai/), or [my own intro](https://www.lesswrong.com/posts/4basF9w9jaPZpoC8R/intro-to-brain-like-agi-safety-1-what-s-the-problem-and-why).)

Now, my friends on the [Parker Solar Probe project](https://www.draper.com/media-center/featured-stories/detail/27373/touching-the-sun-with-the-parker-solar-probe) were able to run certain tests in advance—radiation tests, thermal tests, and so on—but the first time their sensor went into the actual solar corona, it had to work, with no do-overs.

By the same token, we can run certain tests on future AGIs, in a safe way. But the first time that AGIs are autonomously spreading around the world, and inventing transformative new technologies and ideas, and getting an opportunity to irreversibly entrench their power, those AGIs had better be making decisions we’re happy about, with no do-overs.

All those practices listed in §2 above exist for a reason; they're the only way we even have a chance of getting a system to work the first time in a very new situation. They are not optional nice-to-haves, rather they are the bare minimum to make the task merely “very difficult” rather than “hopeless”. If it seems impossible to apply those techniques to AGI, per §3.1 above, then, well, we better [shut up and do the impossible](https://www.lesswrong.com/posts/nCvvhFBaayaXyuBiD/shut-up-and-do-the-impossible).

What might that look like? How do we get to a place where we have deep understanding, and where this understanding gives us a strong reason to believe that things will go well in the (out-of-distribution) scenarios of concern, and where we have a wide variety of safe tests that can be quantitatively compared with that understanding in order to surface unknown unknowns?

I don't know!

Presumably the “spec” and the tests would be more about the AGI’s motivation, or its disposition, or something, rather than about its object-level actions? Well, whatever it is, we better figure it out.

We're not there today, nor anywhere close.

(And even if we got there, then we would face the *additional* problem that all existing and likely future AI companies seem to have neither the capability, nor the culture, nor the time, nor generally even the desire to do the rigorous high-reliability engineering (§2) for AGI. See e.g. [Six Dimensions of Operational Adequacy in AGI Projects](https://www.lesswrong.com/posts/keiYkaeoLHoKK4LYA/six-dimensions-of-operational-adequacy-in-agi-projects) (Yudkowsky 2017).)

# 4\. Optional bonus section: Possible objections & responses

**Possible Objection 1:** Your §3.1 is misleading; we don’t need to specify what AGI Jeff Bezos needs to *do* to run a successful innovative business, rather we need to specify what he needs to *not* do, e.g. he needs to *not* break the law.

**My Response:** If you want to say that “don’t break the law” etc. counts as a spec, well, nobody knows how to do the §2 stuff (deep understanding etc.) for “don’t break the law” either.

And yes, we should tackle that problem. But I don’t see any way that a 300-page spec (as suggested by Joshua Achiam at the top) would be helpful for that. In particular:

- If your roadmap is to make the AGI obey “the letter of the law” for some list of prohibitions, then no matter how long you make the list, a smart AGI trying to get things done [will find and exploit loopholes](https://deepmindsafetyresearch.medium.com/specification-gaming-the-flip-side-of-ai-ingenuity-c85bdb0deeb4), with [catastrophic results](https://www.lesswrong.com/w/nearest-unblocked-strategy).
- Or if your roadmap is to make the AGI obey “the spirit of the law” for some list of prohibitions, then there’s no point in writing a long list of prohibitions. Just use a one-item “list” that says “Don’t do bad things.” I don’t see why it would be any easier or harder to design an AGI that *reliably* (in the §2 sense) obeys the spirit of that one prohibition, than an AGI that *reliably* obeys the spirit of a 300-page list of prohibitions. (The problem is unsolved in either case.)

**Possible Objection 2:** We only need the §2 stuff (deep understanding etc.) if there are potentially-problematic distribution shifts between test and deployment. If we can do unlimited low-stakes tests of the exact thing that we care about, then we can just do trial-and-error iteration. And we get that for free because AGI will improve gradually. Why do you expect problematic distribution shifts?

**My Response:** See my comments in §3.2, plus maybe my post [“Sharp Left Turn” discourse: An opinionated review](https://www.lesswrong.com/posts/2yLyT6kB7BQvTfEuZ/sharp-left-turn-discourse-an-opinionated-review). Or just think: we’re gonna get to a place where there are millions of telepathically-communicating super-speed-John-von-Neumann-level AGIs around the world, getting sculpted by continual learning for the equivalent of subjective centuries, and able to coordinate, invent new technologies and ideas, and radically restructure the world if they so choose … and you really don’t think there’s any problematic distribution shift between that and your safe sandbox test environment??

So the upshot is: the gradual-versus-sudden-takeoff debate is irrelevant for my argument here. (Although for the record, [I do expect superintelligence to appear more suddenly than most people do](https://www.lesswrong.com/posts/yew6zFWAKG4AGs3Wk/foom-and-doom-1-brain-in-a-box-in-a-basement).)

Maybe an analogy is: if you’re worried that a nuclear weapon with yield *Y* might [ignite the atmosphere](https://en.wikipedia.org/w/index.php?title=Effects_of_nuclear_explosions&oldid=1333919751#Atmospheric_ignition), it doesn’t help to first test a nuclear weapon with yield 0.1×*Y*, and then if the atmosphere hasn’t been ignited yet, next try testing one with yield 0.2×*Y*, etc.

![](https://www.lesswrong.com/reactionImages/nounproject/x.svg)

[AI Safety Cases2](https://www.lesswrong.com/w/ai-safety-cases)[Security Mindset2](https://www.lesswrong.com/w/security-mindset)[AI3](https://www.lesswrong.com/w/ai)[

Curated

](https://www.lesswrong.com/recommendations)\+ Add Wikitag

# 108

# Ω 52

[Are there lessons from high-reliability engineering for AGI safety?](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#)

[9leogao](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#YrdFRGLPgeGyqvAQv)

[1ButICouldBeWrong](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#CG4yhewt9tMnyf9hF)

[5RogerDearnaley](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#mP3rHPWuzLHbKev24)

[4Raemon](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#vkR7tAfn4FQWLHSED)

[4ozziegooen](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#pzDG5LE4mLwXhzAwm)

[5Steven Byrnes](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#nR27cTAgjFjRssSfw)

[4ozziegooen](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#GCMjYjaDmEkfCz77p)

[3Dagon](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#oMcksgwavMg3hfjWN)

[1RedMan](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#FkbB8TzARBBsG5CBS)

New Comment

  

9 comments, sorted by

top scoring

Click to highlight new comments since: Today at 2:36 PM

\[\-\][leogao](https://www.lesswrong.com/users/leogao)[24d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=YrdFRGLPgeGyqvAQv)Ω690

i broadly agree with this take for AGI, but I want to provide some perspective on why it might be counterintuitive: when labs do safety work on current AI systems like chatgpt, a large part of the work is writing up a giant spec that specifies how the model should behave in all sorts of situations -- when asked for a bioweapon, when asked for medical advice, when asked whether it is conscious, etc. as time goes on and models get more capable, this spec gets bigger and more complicated.

the obvious retort is that AGI will be different. but there are a lot of people who are skeptical of abstract arguments that things will be different in the future, and much more willing to accept arguments based on current empirical trends.

Reply

\[\-\][ButICouldBeWrong](https://www.lesswrong.com/users/buticouldbewrong)[23d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=CG4yhewt9tMnyf9hF)10

Current LLMs seem to be relatively easy to align by writing those kinds of specifications and mostly don't try to do harmful things, at least not those of the frontier labs. I just think that soon after LLM-based AGI gets developed, one of the first tasks given to the LLM will probably be to develop novel more efficient AI architectures in order to reduce the high energy usage of current architectures. Because LLM-based AGI will probably consume even more energy than current LLMs.

And the LLM might not be as careful as safety researchers when it tries to find more efficient architectures, especially when pressured by humans to try test new approaches anyway despite the risks involved that the LLM might be aware of, but the human is focused more on the positive potential of the technology.

My guess is that it will end up with some approach that will use neuralese and not be language-based, because language is ambiguous, loses meaning and most importantly limits AIs thinking to concepts known to humans, which does not include all the possible concepts in the very vast "concept-space" of superintelligent understanding. And not only the concepts but also the very nature of human reasoning, which is most likely not the most effective way to find a solution to a given problem.

So basically at some point too high energy demands will pressure AI development to switch from language models to neuralese models, which are hard to align, let alone understand.

Except if the LLM is tasked with finding a breakthrough in fusion power, that might then let us sustain LLM training and inference.

Reply

\[\-\][RogerDearnaley](https://www.lesswrong.com/users/rogerdearnaley)[24d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=mP3rHPWuzLHbKev24)52

We are clearly not in a position to do high reliability AI safety engineering now. But in O(5) years, either we will then be doing that sort of work, or we will have paused AI in order to give us time to figure this out, or shortly after that we'll be playing Russian Roulette with the existence of our species. So I do hope people in the field realize they have signed up for an area that is going to need to become detailed, painstaking, and meticulous rather quickly. Doing some background reading into how other complex system safety engineering fields do this sort of thing seems usefully (personally I come from a high-reliability distributed systems background: I know how to turn 2-nines into 4-nines or even 5-nines, but I haven't worked at 6-nines or above).

One issue is that if, say, 99.9% of our ASI personas are aligned (or all are aligned 99.9% of the time), and 0.1% isn't, then this becomes more like an exercise in building reliable systems from unreliable components, or reliable institutions from unreliable people, or like superintelligent law enforcement work, or superintelligent mental health work — all of which are fields we know something about. We're not trying to align **one** ASI CEO, we're trying to align a whole datacenter full of them: and that gives us access to useful redundancy and fault tolerance approaches that we don't have for a single one. And of course also to "who watches the watchmen?" problems.

Reply

\[\-\][Raemon](https://www.lesswrong.com/users/raemon)[4h](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=vkR7tAfn4FQWLHSED)40

Curated.

I've previously been interested in looking to [high reliability organizations](https://www.lesswrong.com/posts/FBoyR2rt29oYvazsE/high-reliability-orgs-and-ai-companies) as a source of life-lessons for AI companies. I liked that this post dug more into the details of high reliability **engineering**, in particular, laying out some specific gears about how it works in practice, and articulating why those reasons are hard to transfer to the AI safety domain (which should give us some pause).

Reply

\[\-\][ozziegooen](https://www.lesswrong.com/users/ozziegooen)[19d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=pzDG5LE4mLwXhzAwm)Ω340

I appreciate that you're engaging in this question, but I have a hard time taking much away from this.

Quickly:  
  
1\. I think we're both probably skeptical of what Joshua Achiam is approaching. My hunch is that he's representing a particularly niche view on things.  
  
2\. It feels to me like there's a gigantic challenge of choosing what *scale* to approach this problem. You seem to be looking at AGI and it's effects from a very high-level. Like, we need to run evals on massive agents exploring the real world - and if this is too complex for more regular robust engineering, then we better throw out the idea of robust engineering. To me this seems like a bit complaining that "Robust engineering won't work for vehicle safety because it's won't be able to tackle the complex society-wide effects of how vehicles will be used at scale."  
  
I think that the case for using more robust methods for AI doesn't look like straightforwardly solving all global-scale large-agent challenges, but instead achieving high reliability levels on much narrower tasks. For example, can we make sure that a single LLM pass has a 99.99% success rate at certain kinds of hacks.

This wouldn't solve all the challenges that would come from complex large systems, similar to how vehicle engineering doesn't solve all challenges with vehicles. But it might be able to still be a big part of the solution. 

You might then argue that a complex system composed of robust parts wouldn't have any benefit from that robustness, because all the 'interesting' stuff happens on the larger scales. My quick guess is that this is one area where we would disagree, perhaps there's a crux here. 

Reply

\[\-\][Steven Byrnes](https://www.lesswrong.com/users/steve2152)[17d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=nR27cTAgjFjRssSfw)Ω350

(Thanks!) To me, your comment is like: “We have a great plan for robust engineering of vehicles (as long as they are at on a dry, warm, indoor track, going under 10kph).” OK that’s better than nothing. But if we are eventually going to be driving cars at high speed in the cold rain, it’s inadequate. We did not test or engineer them in the right environment.

This is not a complex systems objection (e.g., it’s not about how the world changes with billions of cars). It’s a distribution shift objection. Even just one car will fail at high speed in the cold rain under those circumstances.

If there’s a distribution shift (test environment systematically different from deployment environment), then you need sufficiently deep understanding of the system to allow extrapolation across the distribution shift.

In the AI case, the issue is: there’s a strong (quadrillion-dollar) economic incentive to make a type of AI that can found, run, and staff innovative companies, 100% autonomously, for years on end, even when the company is doing things that nobody has thought of, and even in a world possibly very different from our own.

And then there’s a huge distribution shift between the environment in which we expect such AIs to be operating, and the environment(s) in which we can safely test those AIs.

My actual opinion is that this type of AI won’t be an LLM, which e.g. have issues with long context windows and don’t do human-like continual learning.

…But even if it were an LLM (or system that includes LLMs), I think you’re going wrong by treating “reliability” and “robustness” as synonyms, when LLMs are actually much stronger at the former than the latter.

We can make a car that’s 99.99% “reliable” on a warm dry indoor track, but after you distribution-shift into the cold rain, it might be 10% or 0% reliable. So it’s not “robust” to distribution shifts. By the same token, I’m willing to believe that LLMs can be made 99.99% “reliable” (in the sense of reliably doing a specific thing in a specific situation). But in weird situations, LLMs sometimes go off the rails; e.g. nobody has yet made an LLM that could not be jailbroken, despite years of work. They’re not very “robust”.

You’re sorta implying that I’m against robustness, but in the OP I was saying the opposite. I think we desperately need robustness. I just think we’re not gonna get it without deeper understanding, because of distribution shifts.

Reply

\[\-\][ozziegooen](https://www.lesswrong.com/users/ozziegooen)[16d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=GCMjYjaDmEkfCz77p)42

I imagine we'd both agree that there can and should be a lot of evals and attempts at robustness / reliability for small / low-level systems?   
  
It seems like the disagreement is in how useful such work will be for critical and broader alignment challenges.

Reply

![](https://www.lesswrong.com/reactionImages/nounproject/check.svg)1

\[\-\][Dagon](https://www.lesswrong.com/users/dagon)[24d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=oMcksgwavMg3hfjWN)30

Having worked on large-scale non-safety-critical (think massive enterprise and infrastructure-support systems at large cloud providers) for a long time, one of the biggest lessons is the shape of the cost-to-reliability curve.

after about 3 9s, each increment of an -ity (availability, data durability, security, etc.) is far more expensive than the improvement (which is already exponential). This cost is not just financial, it's a cost in features (don't add stuff that's not simple enough to prove correct), in agility (can't add things quickly, everything requires more specification and implementation proof than you think), and in operations (have to watch it more closely, react to non-harmful anomalies, etc.).

I suspect Moloch will prevent any serious slowdown-for-safety desires. Anyone truly serious about being safe will get outcompeted and be made irrelevant. To that analogy, once the knowledge existed to create the bomb, it was inevitable that SOMEONE would risk igniting the atmosphere, so it probably should be us, now, rather than delaying 5-10 years so it can be Russia (or now, China).

Reply

![](https://www.lesswrong.com/reactionImages/nounproject/x.svg)1

\[\-\][RedMan](https://www.lesswrong.com/users/redman)[24d](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi?commentId=FkbB8TzARBBsG5CBS)10

I think I've talked about Nancy Leveson's STAMP, STPA, and CAST frameworks for using control theory to prevent industrial accidents here.  I think it's relevant to AI safety, you don't necessarily need to overspecify every little thing the system does, you just need to carefully specify the unwanted outcomes, and the states of the system where that outcome is possible due to things outside the control of the system.

Eg: 'my thing can't be allowed to get hit by lightning, so if the system's state is 'outside during a thunderstorm', we consider that as something the system should have been engineered to prevent'.  

Reply

[Moderation Log](https://www.lesswrong.com/moderation)

More from [Steven Byrnes](https://www.lesswrong.com/users/steve2152)

156[Why we should expect ruthless sociopath ASI](https://www.lesswrong.com/posts/ZJZZEuPFKeEdkrRyf/why-we-should-expect-ruthless-sociopath-asi)

[Ω](https://alignmentforum.org/posts/ZJZZEuPFKeEdkrRyf/why-we-should-expect-ruthless-sociopath-asi)

[Steven Byrnes](https://www.lesswrong.com/users/steve2152)

8d

[Ω](https://alignmentforum.org/posts/ZJZZEuPFKeEdkrRyf/why-we-should-expect-ruthless-sociopath-asi)

55

101[The brain is a machine that runs an algorithm](https://www.lesswrong.com/posts/eKGjwRSQD3BLxmBcu/the-brain-is-a-machine-that-runs-an-algorithm)

[Steven Byrnes](https://www.lesswrong.com/users/steve2152)

9d

17

112[The nature of LLM algorithmic progress (v2)](https://www.lesswrong.com/posts/sGNFtWbXiLJg2hLzK/the-nature-of-llm-algorithmic-progress-v2)

[Steven Byrnes](https://www.lesswrong.com/users/steve2152)

21d

23

[View more](https://www.lesswrong.com/users/steve2152)

Curated and popular this week

108[Are there lessons from high-reliability engineering for AGI safety?](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi)[Ω](https://alignmentforum.org/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi)

[Steven Byrnes](https://www.lesswrong.com/users/steve2152)

3h[Ω](https://alignmentforum.org/posts/hiiguxJ2EtfSzAevj/are-there-lessons-from-high-reliability-engineering-for-agi)

9

322[Did Claude 3 Opus align itself via gradient hacking?](https://www.lesswrong.com/posts/ioZxrP7BhS5ArK59w/did-claude-3-opus-align-itself-via-gradient-hacking)

[Fiora Starlight](https://www.lesswrong.com/users/fiora-starlight)

5d

35

201[The Spectre haunting the "AI Safety" Community](https://www.lesswrong.com/posts/LuAmvqjf87qLG9Bdx/the-spectre-haunting-the-ai-safety-community)[Gabriel Alfour](https://www.lesswrong.com/users/gabriel-alfour-1)

5d24

[9Comments](https://www.lesswrong.com/posts/hiiguxJ2EtfSzAevj/#comments)

9

x

Are there lessons from high-reliability engineering for AGI safety? — LessWrong<iframe xmlns="http://www.w3.org/1999/xhtml" id="intercom-frame" style="position: absolute !important; opacity: 0 !important; width: 1px !important; height: 1px !important; top: 0 !important; left: 0 !important; border: none !important; display: block !important; z-index: -1 !important; pointer-events: none;" aria-hidden="true" tabindex="-1" title="Intercom"></iframe>