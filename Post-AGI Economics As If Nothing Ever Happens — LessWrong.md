---
title: "Post-AGI Economics As If Nothing Ever Happens — LessWrong"
source: "https://www.lesswrong.com/posts/fL7g3fuMQLssbHd6Y/post-agi-economics-as-if-nothing-ever-happens"
author:
  - "[[Jan_Kulveit]]"
published: 2026-02-04
created: 2026-02-08
description: "When economists think and write about the post-AGI world, they often rely on the implicit assumption that parameters may change, but fundamentally, s…"
tags:
  - "clippings"
---
When economists think and write about the post-AGI world, they often rely on the implicit assumption that parameters may change, but fundamentally, structurally, not much happens. And if it does, it’s maybe one or two empirical facts, but nothing too fundamental.  
  
This mostly worked for all sorts of other technologies, where technologists would predict society to be radically transformed e.g. by everyone having most of humanity’s knowledge available for free all the time, or everyone having an ability to instantly communicate with almost anyone else. [^1]  
  
But it will not work for AGI, and as a result, most of the econ modelling of the post-AGI world is irrelevant or actively misleading [^2], making people who rely on it more confused than if they just thought “this is hard to think about so I don’t know”.

## Econ reasoning from high level perspective

Econ reasoning is trying to do something like projecting the extremely high dimensional reality into something like 10 real numbers and a few differential equations. All the hard cognitive work is in the projection. Solving a bunch of differential equations impresses the general audience, and historically may have worked as some sort of proof of intelligence, but is relatively trivial.

How the projection works is usually specified by some combination of assumptions, models and concepts used, where the concepts themselves usually imply many assumptions and simplifications.  
  
In the best case of economic reasoning, the projections capture something important, and the math leads us to some new insights.[^3] In cases which are in my view quite common, non-mathematical, often intuitive reasoning of the economist leads to some interesting insight, and then the formalisation, assumptions and models are selected in a way where the math leads to the same conclusions. The resulting epistemic situation may be somewhat tricky: the conclusions may be true, the assumptions sensible, but the math is less relevant than it seems - given the extremely large space of economic models, had the economist different intuitions, they would have been able to find a different math leading to different conclusions.

Unfortunately, there are many other ways the economist can reason. For example, they can be driven to reach some counter-intuitive conclusion, incentivized by academic drive for novelty. Or they may want to use some piece of math they like.[^4] Or, they can have intuitive policy opinions, and the model could be selected so it supports some policy direction - this process is usually implicit and subconscious.  
  
The bottom line is if we are interested in claims and predictions about reality, the main part of economic papers are assumptions and concepts used. The math is usually right. [^5]

## Econ reasoning applied to post-AGI situations

The basic problem with applying standard economic reasoning to post-AGI situations is that sufficiently advanced AI may violate many assumptions which make perfect sense in human economy, but may not generalize. Often the assumptions are so basic that they are implicit, assumed in most econ papers, and out of sight in the usual “examining the assumptions”. Also advanced AI may break some of the intuitions about how the world works, breaking the intuitive process upstream of formal arguments.  
  
What complicates the matter is these assumptions often interact with considerations and disciplines outside of the core of economic discourse, and are better understood and examined using frameworks from other disciplines.  
  
To give two examples:

**AI consumers**

Consumption so far was driven by human decisions and utility. Standard economic models ultimately ground value in human preferences and utility. Humans consume, humans experience satisfaction, and the whole apparatus of welfare economics and policy evaluation flows from this. Firms are modeled as profit-maximizing, but profit is instrumental—it flows to human owners and workers who then consume.

If AIs own capital and have preferences or goals of their own, this assumption breaks down. If such AIs spent resources, this should likely count as consumption in the economic sense.

**Preferences**

Usual assumption in most econ thinking is that humans have preferences which are somewhat stable, somewhat self-interested, and what these are is a question mostly outside of economics. [^6] There are whole successful branches of economics studying to what extent human preferences deviate from VNM rationality or human decision making suffers from cognitive limitations, or on how preferences form, but these are not in the center of attention of mainstream macroeconomy. [^7] Qualitative predictions in case of humans are often similar, so the topic is not so important.  
  
When analyzing the current world, we find that human preferences come from diverse sources, like biological needs, learned tastes, and culture. A large component seems to be ultimately selected for by cultural evolution.

Post-AGI, the standard econ assumptions may fail, or need to be substantially modified. Why?  
  
One consideration is the differences in cognitive abilities between AGIs and humans may make human preferences easily changeable for AGIs. As an intuition pump: consider a system composed of a five year old child and her parents. The child obviously has some preferences, but the parents can usually change these. Sometimes by coercion or manipulation, but often just by pointing out consequences, extrapolating children’s wants, or exposing them to novel situations.  
  
Also preferences are relative to world model: standard econ way of modelling differences in world models is “information asymmetries”. The kid does not have as good understanding of the world, and would easily be exploited by adults.

Because child preferences are not as stable and self-interested as adults, and kids suffer from information asymmetries, they are partially protected by law: the result is patchwork of regulation where, for example, it is legal to try to modify children’s food preferences, but adults are prohibited to try to change child’s sexual preferences for their advantage.

Another ”so obvious it is easy to overlook” effect is child dependence on parent’s culture: if parents are Christians, it is quite likely their five year old kid will believe in God. If parents are patriots, the kid will also likely have some positive ideas about their country. [^8]  
  
When interacting with cognitive systems way more capable than us, we may find ourselves in a situation somewhat similar to kids: our preferences may be easily influenced, and not particularly self-interested. The ideologies we adopt may be driven by non-human systems. Our world models may be weak, resulting in massive information assymetries.

There even is a strand of economic literature that explicitly models parent-child interactions, families and formation of preferences. [^9] This body of work may provide useful insights I’d be curious about - is anyone looking there?

The solution may be analogous: some form of paternalism, where human minds are massively protected by law from some types of interference. This may or may not work, but once it is the case, you basically can not start from classical liberal and libertarian assumptions. As an intuition pump, imagine someone trying to do “macroeconomy of ten year olds and younger” in the current world.

**Other core concepts**

We could examine some other typical econ assumptions and concepts in a similar way, and each would deserve a paper-length treatment. This post tries to mostly stay a bit more meta-, so just some pointers.

***Property rights.*** Most economic models take property rights as exogenous - “assume well-defined and enforced property rights.” If you look into how most property rights are actually connected to physical reality, property rights often mean some row exists in a database run by the state or a corporation. Enforcement ultimately rests on the state’s monopoly on violence, cognitive monitoring capacity and will to act as independent enforcer. As all sorts of totalitarian, communist, colonial or despotic regimes illustrate, even in purely human systems, private property depends on power. If you assume property is stable, you are assuming things about governance and power.

***Transaction costs and firm boundaries**.* Coase’s theory [^10] explains why firms exist: it is sometimes cheaper to coordinate internally via hierarchy than externally via markets. The boundary of the firm sits where transaction costs of market exchange equal the costs of internal coordination. AI may radically reduce both— making market transactions nearly frictionless while also making large-scale coordination easy. The equilibrium size and structure of firms could shift in unpredictable directions, or the concept of a “firm” might become less coherent.

***Discrete agents and competition**.* Market models assume distinct agents that cooperate and compete with each other. Market and competition models usually presuppose you can count the players. AGI systems can potentially be copied, forked, merged, or run as many instances, and what are their natural boundaries is an open problem.

***Capital vs. Labour.***Basic concepts in 101 economic models typically include capital and labour as concepts. Factors is production function, Total Factor Productivity, Cobb-Douglas, etc. Capital is produced, owned, accumulated, traded, and earns returns for its owners. Labour is what humans do, and cannot be owned. This makes a lot of sense in modern economies, where there is a mostly clear distinction between “things” and “people”. It is more ambiguous if you look back in time - in slave economies, do slaves count as labour or capital? It is also a bit more nuanced - for example with “human capital”.  
  
When analyzing the current world, there are multiple reasons why the “things” and “people” distinction makes sense. “Things” are often tools. These amplify human effort, but are not agents. A tractor makes a farmer more productive, but does not make many decisions. Farmers can learn new tasks, tractors can not. Another distinction is humans are somewhat fixed: you can not easily and quickly increase or decrease their counts.

Post-AGI, this separation may stop making sense. AIs may reproduce similarly to capital, be agents like labour, learn fast, and produce innovation like humans. Also maybe humans may own them like normal capital, or more like slaves, or maybe AIs will be self-owned.

**Better and worse ways how to reason about post-AGI situations**

There are two epistemically sound ways to deal with problems with generalizing economic assumptions: broaden the view, or narrow the view. There are also many epistemically problematic moves people take.  
  
Broadening the view means we try to incorporate all crucial considerations. If assumptions about private property lead us to think about post-AGI governance, we follow. If thinking about governance leads to the need to think about violence and military technology, we follow. In the best case, we think about everything in terms of probability distributions, and more or less likely effects. This is hard, interdisciplinary, and necessary, if we are interested in forecasts or policy recommendations.  
  
Narrowing the view means focusing on some local domain, trying to make a locally valid model and clearly marking all the assumptions. This is often locally useful, may build intuitions for some dynamic, and fine as long as a lot of effort is spent on delineating where the model may apply and where clearly not.  
  
What may be memetically successful and can get a lot of attention, but overall is bad, is doing the second kind of analysis and presenting it as the first type. Crucial consideration is a consideration which can flip the result. If an analysis ignores or assumes away ten of these, the results have basically no practical relevance: imagine for each crucial consideration, there is 60% chance the modal view is right and 40% it is not. Assume or imply the modal view is right 10 times, and your analysis holds in 0.6% worlds.

In practice, this is usually not done explicitly - almost no one claims their analysis considers all important factors - but as a form of motte-and-bailey fallacy. The motte is the math in the paper - follows from the assumptions and there are many of these. The bailey are the broad stroke arguments, blogpost summaries, tweets and short-hand references, spreading way further, without the hedging.

In the worst cases, various assumptions made are contradictory or at least anticorrelated. For example: some economists assume comparative advantage generally preserves relevance of human labour, and AIs are just a form of capital which can be bought and replicated. However, comparative advantage depends on opportunity costs: if you do X, you cannot do Y at the same time. The implicit assumption is you can not just boot a copy of you. If you can, the “opportunity cost” is not something like the cost of your labour, but the cost of booting up another copy. If you assume future AGIs are similarly efficient substitutes for human labour as current AIs are for moderately boring copywriting, the basic “comparative advantage” model is consistent with labour price dropping 10000x below minimum wage. While the comparative advantage model is still literally true, it does not have the same practical implications. Also while in the human case the comparative advantage model is usually not destroyed by frictions, if your labour is sufficiently low value, the effective price of human labour can be 0. For a human example, five year olds or people with severe mental disabilities unable to read are not actually employable in the modern economy. In the post-AGI economy, it is easy to predict frictions like humans operating at machine speeds or not understanding the directly communicated neural representations.

**What to do**

To return to the opening metaphor: economic reasoning projects high-dimensional reality into a low-dimensional model. The hard work is choosing the projection. Post-AGI, we face a situation where the reality we are projecting may be different enough that projections calibrated on human economies systematically fail. The solution is usually to step back and bring more variables into the model. Sometimes this involves venturing outside of the core of econ thinking, and bringing in political economy, evolution, computational complexity or even physics and philosophy. Or maybe just look at other parts of economic thinking, which may be unexpectedly relevant. This essay is not a literature review. I’m not claiming that no economist has ever thought about these issues, just that the most common approach is wrong.

On a bit of a personal note. I would love it if there were more than 5-10 economists working on the post-AGI questions seriously, and engaging with the debate seriously. If you are an economist… I do understand that you are used to interacting with the often ignorant public, worried about jobs and not familiar with all the standard arguments and effects like Baumol, Jevons, lump of labour fallacy, gains from trade, etc. Fair enough, but the critique here is different: you’re assuming answers to questions you haven’t asked. If you are modelling the future using econ tools, I would like to know your answers/assumptions about “are AIs agents?”, “how are you modelling AI consumption?”, “in your model, do AIs own capital?” or “what is the system of governance compatible with the economic system you are picturing?”  
  
*Thanks to Marek Hudík, Duncan Mcclements and David Duvenaud for helpful comments on a draft version of this text. Mistakes and views are my own. Also thanks to Claude Opus 4.5 for extensive help with the text.*

x

Post-AGI Economics As If Nothing Ever Happens — LessWrong

[^1]: Gordon, Robert J. The Rise and Fall of American Growth.

[^2]: Examples of what I'm critizing range from texts by Nobel laureates - eg Daron Acemoglu [The Simple Macroeconomics of AI](https://economics.mit.edu/sites/default/files/2024-04/The%20Simple%20Macroeconomics%20of%20AI.pdf) (2024) to posts by rising stars of thinking about post-AGI economy like Philip Trammell's [Capital in the 22nd Century](https://substack.com/home/post/p-182789127).

[^3]: Sane economists are perfectly aware of nature of the discipline. For longer discussion: Rodrik, Dani. [Economics Rules: The Rights and Wrongs of the Dismal Science](https://www.economicas.uba.ar/wp-content/uploads/2016/03/Economics-Rules-Dani-Rodrik.pdf). W.W. Norton, 2015.

[^4]: Also this is not a novel criticism: Romer, Paul. “ [The Trouble with Macroeconomics.](https://paulromer.net/trouble-with-macroeconomics-update/WP-Trouble.pdf)” The American Economist 61, no. 1 (2016): 31-44.

[^5]: *“So, math plays a purely instrumental role in economic models. In principle, models do not require math, and it is not the math that makes the models useful or scientific.”* Rodrik (2015)

[^6]: Classic text by Robbins (1932) **defines preferences as out of scope** *“Economics is the science which studies human behavior as a relationship between given ends and scarce means which have alternative uses.”* Another classical text on the topic is Stigler & Becker (1977) “De Gustibus Non Est Disputandum.” As with almost any claim in this text: yes, there are parts of econ literature about preference formation, but these usually do not influence the post-AGI macroeconomy papers.

[^7]: De Grauwe, Paul, and Yuemei Ji. “ [Behavioural Economics is Also Useful in Macroeconomics](https://cepr.org/voxeu/columns/behavioural-economics-also-useful-macroeconomics).” VoxEU, January 2018.  
Driscoll, John C., and Steinar Holden. “ [Behavioral Economics and Macroeconomic Models](https://www.sciencedirect.com/science/article/abs/pii/S016407041400072X).” Journal of Macroeconomics 41 (2014): 133-147.

[^8]: Bisin, Alberto, and Thierry Verdier. “The Economics of Cultural Transmission and the Dynamics of Preferences.”

[^9]: Becker, Gary S. A Treatise on the Family.

[^10]: Coase, Ronald H. “ [The Nature of the Firm.](https://ios23.classes.ryansafner.com/files/readings/Coase-1937.pdf)” Economica 4, no. 16 (1937): 386-405