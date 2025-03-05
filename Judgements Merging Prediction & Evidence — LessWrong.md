---
title: "Judgements: Merging Prediction & Evidence — LessWrong"
source: "https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/judgements-merging-prediction-and-evidence"
author:
  - "[[abramdemski]]"
published: 2025-02-23
created: 2025-03-01
description: "I recently wrote about complete feedback, an idea which I think is quite important for AI safety. However, my note was quite brief, explaining the id…"
tags:
  - "clippings"
---
*I recently wrote about* [*complete feedback*](https://www.lesswrong.com/posts/3ag99iJEgFFwyj64Z/complete-feedback)*, an idea which I think is quite important for AI safety. However, my note was quite brief, explaining the idea only to my closest research-friends. This post aims to bridge one of the inferential gaps to that idea. I also expect that the perspective-shift described here has some value on its own.*

---

In classical Bayesianism, prediction and evidence are two different sorts of things. A prediction is a probability (or, more generally, a probability distribution); evidence is an observation (or set of observations). These two things have different type signatures. They also fall on opposite sides of the agent-environment division: we think of predictions as supplied by agents, and evidence as supplied by environments.

In [Radical Probabilism](https://www.lesswrong.com/posts/xJyY5QkQvNJpZLJRo/radical-probabilism-1), this division is not so strict. We *can* think of evidence in the classical-bayesian way, where some proposition is observed and its probability jumps to 100%. In the betting-market analogy, this is like the judge resolving a betting contract. However, Radical Probabilism encourages us to think of "softer" evidence, which pushes our beliefs some distance in a direction but not to 100% or 0%.

We can think of a judge in a betting market as just another market participant, who happens to have arbitrarily much money. Resolving a bet is like offering to buy out the contract for its payout value. If we think of the opposite side of the bet as a short, the value of the short goes to zero, because the judge will tirelessly buy up the other side of that short.<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fnk0hrldn7a3s" class=""><span>[1]</span></a></span></span></sup>

This means we can think of some market participants as hypothesis-like, and others as evidence-like. The hypothesis-like market participants are profit-seekers who attempt to use their own wits to predict future prices. The evidence-like market participants are not profit-motivated; instead, they spend their money on ensuring that the market prices reflect the truth. They perceive external events and buy up the corresponding market goods; when they see X, they buy shares in X. 

However, the main point here is not to make the distinction, but rather, to point out that it is fuzzy and not absolute. I propose the term ***judgement*** to unify prediction & evidence, because "judging a judgement" makes sense (IE, judgements can intuitively play either the prediction role or the evidence role or both).

If everything so far made perfect sense, you get the idea. If you're curious for more, read on.

## Warm-up: Prices as Prediction & Evidence

If the idea of a combined prediction-evidence object still feels confusing, think about a *price*. If Alice buys a stock at price p, this can be regarded as a prediction that future prices will rise; if she is able to sell it to Bob later at q>p, we can think of this as confirmation that the prediction was correct (and quantitatively more correct, the higher q is). The sale to Bob is evidence in relation to the earlier prediction. Similarly, then, when Alice first buys the stock at p, this is evidence about the correctness of earlier prices.

A price, therefore, plays both a "prediction" role and an "evidence" role.

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/3hs6MniiEssfL8rPz/bcdedolp0qcttjc9xers)

You might initially think this double nature is because prices are where supply and demand meet. However, I don't think so: *the demand itself* can be seen as either a prediction or evidence. You can think of supply as a prediction that prices will go down (otherwise you wouldn't want to sell now), and demand as a prediction that prices will go up (otherwise you wouldn't want to buy).<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fnjhfcvrfrts" class=""><span>[2]</span></a></span></span></sup> Similarly, you can think of supply as evidence against higher prices / for lower prices, and demand as the reverse.

Bayesian updates are more like the special case when a final buyer purchases something and holds it forever, so that there is no prediction-nature left, only evidence-nature wrt previous prices.

## Generalization: Traders as Judgements

We can generalize from thinking of individual buy/sell actions as "prediction-evidence" to thinking of trading strategies. A "trading strategy" (as per [the Logical Induction paper](https://arxiv.org/abs/1609.03543)) is a function from prices to a list of buy/sell actions.

So, for example, a "judgement" can buy if prices fall below 3 cents, or sell if prices go above 5 cents, and otherwise do nothing. 

We can generalize even further to a sequence of trading strategies over time, an object which the Logical Induction paper terms a "trader". A trader can think longer and change its trading strategy over time. I also want to allow traders to change their minds based on external evidence, like in a betting market; these traders have some connection to the broader environment.<sup><span><span><span></span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fns39komdegkb" class=""><span>[3]</span></a></span></span></sup>

For example, the Deductive Process of a logical inductor. This is the thing that sets prices to 1 when a proposition has been proven, and 0 when it has been refuted. We can also imagine a Deductive Process which sets special empirical propositions to 1 or 0 based on input from, EG, a camera. 

The Logical Induction paper models the Deductive Process in a special way, but we could instead think of it as a market participant with infinite wealth, who uses that wealth to buy out specific positions. This special trader is considered as "ground truth" by us, outside the system; but, this is only our subjective view, based on the fact that we especially trust this trader. (Indeed, that is why we are comfortable giving it infinite wealth.)

A second example: Occam Traders. These traders internally look for algorithmically simple descriptions of sentences, and then buy simple sentences proportionally to how simple they are. Whereas the Deductive Process is all "evidence-nature" because it completely buys out positions, Occam Traders have some prediction-nature and some evidence-nature: we might expect many especially simple propositions to later turn out to be true (enriching the Occam traders), but we also expect that some sentences purchased by Occam traders will remain undecidable. In those cases, we somewhat trust the Occam heuristic, so we see the Occam traders as providing useful partial evidence to the market, shaping it towards true beliefs.

## Collector-Investor Continuum

The Deductive Process is a "pure collector" who buys up things based on their "intrinsic value" -- if we imagine it personified as a human, it is a human who spends their prediction-market currency purely to act as "judge", making sure that "good predictions" of other traders get rewarded.

Occam Traders are also pretty far on the "collector" side of the collector-investor continuum; they have their own notion of the "intrinsic value" of a proposition (which, from the outside of the system, we somewhat trust). They might later be rewarded when something they believed turns out to be true (or, put more subjectively, ends up highly valued by the rest of the market); but, in some sense, they aren't trying to do this; their notion of value isn't shaped by the market.

We expect other traders in Logical Induction to be more "investor-like", speculating about the dynamics of the market, buying and selling in patterns more optimized for profit. 

This is connected to Anna Salamon's notion of ["live money" vs "dead money"](https://www.lesswrong.com/posts/xtuk9wkuSP6H7CcE2/ayn-rand-s-model-of-living-money-and-an-upside-of-burnout) -- live money is investor-like, responding to market demands. Dead money is collector-like, focusing on money as a means to an end; buying things up based on some sense of intrinsic value rather than monetary gain. However, the live/dead distinction somewhat vilifies dead money in favor of live money -- collectors are seen as shortsighted and lacking in contact-with-reality, while investors are the heroes willing to continue using money for extrinsic gain. I would critique this vilification as itself being shortsighted; the "value" which investors maximize must itself come from somewhere (ie from others acting as "collectors").

Profit-motivated companies are like pure investors, seeking only external validation of value, and neglecting any intrinsic value or disvalue they produce by way of the well-being of workers, or positive/negative impacts on the world that cannot be easily monetized. 

Recognizing the dual role of Judgements as prediction and evidence clarifies the role of "philosophical intuition" in reasoning: a philosophical intuition plays a strong evidence role, helping us to judge the plausibility of a philosophical theory, but it is too fallible to treat as Bayesian evidence. Our philosophical intuitions are revised in a prediction-like way in response to other philosophical intuitions, and in response to stronger types of evidence (or rather, stronger types of Judgement). Logical Induction is a theory of how these Judgements interact and cohere over time.

## Implications for AI

My thesis is that, in order for AI systems of the future to be appropriately truth-oriented, they need to be designed in a way which accounts for the deal nature of Judgements as prediction and evidence.

For example, [modern RL-powered LLMs](https://www.lesswrong.com/posts/BEFbC8sLkur7DGCYB/o1-is-a-bad-idea) can be trained on tasks for which we have good feedback (like mathematical problem-solving, and to a lesser extent, programming), but this paradigm doesn't work so well for squishier questions where the feedback we can get is fallible enough that the evidence provided by reasoning is on-par in strength with the evidence we have about the final answer. 

For such problems, I suppose that AI systems need to be trained in a way which accounts for stronger and weaker arguments, modeling individual arguments as a Judgement which provides some evidence but is also itself accountable to other evidence.

## Technical Questions

I think there is more to be said about the technical question of when we can analyze a trader as more collector-like vs more investor-like. I expect that a rich mathematical theory of this could be developed. Viewing a trader as a collector vs an investor depends on a subjective choice of how to view traders as agentic; I don't expect a fully objective criterion, but rather, a criterion parameterized by some subjective thing.

Intuitively, I expect that judging collector-nature vs investment-nature itself relies on a Judgement. EG, from the outside, we trust the Deductive Process; this Judgement of ours feeds into how we interpret traders. 

Another interesting technical question is connected to the practice of giving the Deductive Process infinite money. You might intuitively think that giving some traders infinite money will break the Logical Induction property, because traders with infinite money can flood the market, arbitrarily distorting things. However, there is no such problem in the case of the Deductive Process, because when the Deductive Process decides that something is 1 or 0, it never changes its mind. As a result, it doesn't flood the market with money; it only transfers money between the "winners" and "losers" in the rest of the market. Those who bet against the eventual opinion of the Deductive Process will lose their money to those who bet in favor.

More generally, it seems like traders who are "inexploitable" in a specific sense are OK to give infinite money. The Deductive Process is inexploitable by virtue of only sending things to 1 or 0 and never changing its mind after. More generally, a trader could decide that some proposition X is "at least .05" and spend its money enforcing that, like Occam traders do. These should also be safe to give infinite money to (but not if we *also* give the Deductive Process infinite money, since the Deductive Process will sometimes disagree with the Occam traders).

This notion of "exploitability" has to be different from the one studied in the Logical Induction paper, however; EG, no constant belief distribution is inexploitable in the Logical Induction sense, but trading strategies which enforce constant prices seem inexploitable in the sense relevant here. So, my "inexploitability" needs to be weaker than the Logical Induction sense.

1. <sup><strong><span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fnrefk0hrldn7a3s"><span>^</span></a></span></strong></sup>

More precisely, buying a share of not-X can be thought of as selling a share of X.

Let's assume that all bets are standardized to pay out $1 per share (so if you want to bet for a larger amount, you can buy multiple shares), and the price of a share of X is p.

- Buying a share of not-X: pay $(1-p) now, get $1 later if the judge decides X is false.
- If X turns out to be true, you paid $(1-p) and gained nothing.
- If X turns out false, you paid $(1-p) and gained $1, so you net $p overall.
- Selling a share of X: gain $p now, pay $1 later if the judge decides X is true.
- If X turns out true, you got $p, but you paid $1, so you lost $(1-p) overall.
- If X turns out false, you got $p and lost nothing, so you net $p overall.

So, ignoring the question of *when* the money comes in or goes out, the two transactions are the same. If you wanted to buy a share of not-X but the market only offers shares of X, you can short X (accept $p now in exchange for promising to deliver a share of X later), and also set $1 aside for later; this will be like paying $(1-p) now for a possible $1 gain if X turns out to be false. (The $1 you set aside becomes your prize if X turns out to be false, or you use it to buy the share you promised if X turns out to be true.) Simply put: buying not-X is just like shorting X plus setting money aside to deal with the risk of shorting.

If we know the judge will definitely decide one way or the other (X or not-X), the price of a share of X plus the price of a share of not-X should never be less than $1, because then someone can make easy money by buying both for a definite payout of $1. (This ignores transaction fees as well as inflation.)

If we know that the judge will only cause either bets for X to pay out or bets for not-X to pay out, the price of a share for X plus the price of a share for not-X should never exceed $1, either. If they do, someone could make guaranteed money by shorting the market, essentially becoming a market-maker by finding people who want to bet different ways and selling the paired X and not-X shares for a discounted price.

If we eliminate the special role of the judge, and instead think of the judge as just another market participant:

- "X turns out to be true" becomes "a wealthy market participant buys out all shares of X for $1 each"
- Shareholders can sell their shares for (at least) $1, getting their payout. Since they originally paid $p, they make a profit of $(1-p).
- Those who short X (selling a promise to provide a share of X at a later date) must now pay (at least) $1 to obtain the promised share of X. Since they originally made $p on the sale, they face a net loss of $(1-p).
- If we want to remove the "(at least)" from the two bullet points above, we can also suppose the wealthy market participant shorts any prices higher than $1.
- "X turns out to be false" becomes "a wealthy market participant shorts X at any value higher than $0".
- Shares in X become worthless, so people who bought X at $p lost $p on net.
- Those who shorted X keep the $p they made from shorting as pure profit.

As discussed earlier, "purchasing a share of not-X" becomes selling a share of X but setting aside $1 to mitigate the risk (although this only works if we assume that the price of X can't go above $1). This inherently makes the "price" of not-X exactly $(1-p).

And, of course, the punchline: if we think of things in this way, we can also imagine "softer" judge-like traders who don't pump prices all the way up to $1 or all the way down to $0, instead applying gentler pressure in a direction.

Actually, there are two distinct dimensions of "softness": whether the trader pushes to 0 or 1 vs something in the middle, and whether the trader expends arbitrarily large amounts of money towards this end or only smaller quantities.
2. <sup><strong><span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fnrefjhfcvrfrts"><span>^</span></a></span></strong></sup>

I'm focusing on things like stock prices or durable collector's items, as opposed to food or machines which are typically purchased in order to be used.
3. <sup><strong><span><a href="https://www.lesswrong.com/posts/3hs6MniiEssfL8rPz/#fnrefs39komdegkb"><span>^</span></a></span></strong></sup>

"Some connection to the broader environment" may or may not be modeled in the Bayesian way; IE, we might think of the traders as themselves making Bayesian observations of some "external" fact. However, since we are in the business of questioning such strong Bayesian assumptions, we might as well think of the traders as having more generalized connections to information; they "somehow" change their mind; they have "some" connection to the environment.