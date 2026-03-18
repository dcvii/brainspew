---
title: "Grok"
source: "https://x.com/i/grok?conversation=2034279148118835636"
author:
  - "[[X (formerly Twitter)]]"
published:
created: 2026-03-18
description: "Grok is a free AI assistant designed by xAI to maximize truth and objectivity. Grok offers real-time search, image generation, trend analysis, and more."
tags:
  - "brain_spew"
---
Is there an area in statistics that suggests that the likelihood of any reasonable bet to payoff increases with time?

Searching the web

36 results

No, there is no area in statistics that broadly suggests the likelihood (probability) of any reasonable bet paying off reliably increases purely with time or the number of trials.The closest concepts people sometimes misinterpret in this direction come from probability and statistics applied to repeated betting/investing, but they do not support the idea that time itself makes a payoff more likely for a given bet (or even a sequence of similar bets). Here's a breakdown of the relevant areas:1. Law of Large Numbers (LLN)This is the most commonly invoked theorem here.  
The LLN states that as the number of independent trials → ∞, the sample average return converges (in probability or almost surely) to the true expected value per trial.
- If a bet has positive expected value (EV > 0, a "reasonable" +EV bet), then over many repetitions your average return per bet will approach that positive EV → almost surely you'll be ahead in the long run (assuming you don't go bankrupt first due to variance or poor sizing).
- If EV = 0 (fair game), average return → 0.
- If EV < 0 (most casino/sportsbook bets after vig), average return → negative → you'll lose in the long run.
Importantly:
- The probability that any single bet pays off does not change with time or past outcomes (assuming independence).
- The probability that your total wealth is positive (or above starting point) after many bets does increase toward 1 if EV > 0 and you use proper bet sizing (e.g., Kelly criterion or fractional Kelly to avoid ruin).
- But even with +EV, ruin is possible (though probability → 0 as trials → ∞ in many models).
People sometimes loosely say "the longer you play a +EV game, the more certain you are to win," but this refers to cumulative performance converging to positive, not any individual bet becoming more likely to pay off.2. Kelly Criterion & Long-Run GrowthIn betting/investment sizing literature (e.g., Kelly criterion), repeatedly betting a fixed fraction of your bankroll in a +EV game maximizes the long-run geometric growth rate of wealth.  
Over time, the probability that your wealth exceeds any fixed level → 1 (almost surely), provided EV > 0 and you don't over-bet.Again: this is about long-run compounded wealth trending upward, not individual bets becoming more likely to succeed.3. Common Misconceptions / Related Fallacies
- Gambler's Fallacy — Believing a bet is "due" after a losing streak → false (for independent bets). Time does not increase the chance the next bet pays off.
- Reverse — Some people think long horizons guarantee profit in +EV situations, but ergodicity issues show ensemble averages (what you'd see betting many people once) differ from time averages (what one person experiences betting repeatedly). In non-ergodic processes, even +EV bets can lead to almost-sure ruin for the individual despite positive ensemble expectation.
- In investing (e.g., stocks, SIPs in some markets), people sometimes say "probability of profit increases with holding time" because of positive drift + mean reversion/volatility effects over long periods → but this is domain-specific (equity risk premium), not a general statistics principle for "any reasonable bet."
Bottom LineIf "reasonable bet" means positive expected value, then yes — in the limit of infinite repetitions (very long time), statistics (via LLN + martingale/renewal theory) tells us you'll almost surely end up profiting on average / in total, and the probability of being ahead grows toward 1 (with proper risk management). But the likelihood that any particular bet (or the next one) pays off does not increase with time. The per-bet probability stays fixed; only the cumulative story improves for +EV games.If the bet has zero or negative EV, time only guarantees convergence to loss (casinos love this). So the answer is no to a general statistical area claiming that for arbitrary reasonable bets — but yes in the narrow, qualified sense of long-run +EV repeated betting under LLN/Kelly-like frameworks.

Apply this mathematical understanding to the following assertion. “Some observers have argued that Ehrlich could have won if the bet had been for a different period, or if the start date had been different. Ehrlich wrote that the five metals in question had increased in price between the years 1950 and 1975.\[3\] Asset manager Jeremy Grantham wrote that if the Simon-Ehrlich wager had been for a longer period (from 1980 to 2011), then Simon would have lost on four of the five metals. Economist Mark J. Perry noted that for an even longer period of time, from 1934 to 2013, the inflation-adjusted price of the Dow Jones-AIG Commodities Index showed "an overall significant downward trend" and concluded that Simon was "more right than lucky". Kiel et al. (2010) claimed that when considering all possible time periods from 1900 to 2008, Simon would have won the bet in only 38.4% of all cases, while Ehrlich would not only have won more often but also by a wide margin. They viewed the period from 1980 to 1990, during which the bet was active, as one of the 15 worst periods over the entire study period from 1900 to 2008. Contrary to popular public opinion, they posited, the conclusion of the bet is not that there is no such thing as a shortage of raw materials, but rather that when it comes to betting, it is better to have luck on your side than expertise.”

No, the assertion does not undermine the relevant statistical principles — it actually illustrates them, with an important qualification on horizon length.The Simon–Ehrlich wager was a single 10-year bet on whether the inflation-adjusted prices of a fixed bundle of five metals (copper, chromium, nickel, tin, tungsten) would rise (Ehrlich) or fall (Simon). Simon won decisively. Kiel et al. (2010) examined the same bundle over the entire 1900–2008 period using rolling 10-year windows (starting every year, yielding ~98 overlapping intervals). They found Simon’s side would have won in only 38.4 % of those windows; Ehrlich won more often and by larger average margins. The actual 1980–1990 window was one of the 15 strongest price-drop periods in the whole dataset — unusually lucky for Simon.

[ideas.repec.org](https://ideas.repec.org/a/eee/ecolec/v69y2010i7p1365-1367.html)

This looks like a classic “luck over skill” story at first glance. But applying the mathematical framework from before (Law of Large Numbers, drifted time-series processes, dependence of trials) shows why the assertion is incomplete and, in one key respect, backwards.1. The “trials” are not independent repeated bets
- The Kiel windows overlap by 9 years each. They are extremely autocorrelated observations on one single historical path, not i.i.d. draws like repeated coin flips or casino bets.
- Counting “38.4 % Simon wins” is simply the empirical frequency of negative 10-year real returns in that century. It tells us volatility and business cycles dominated short horizons — prices rose in most 10-year stretches — but it does not estimate a true unchanging probability that can be fed into a Law of Large Numbers argument.
- You cannot treat this as “Ehrlich was right more often, therefore his model is superior.” That would be like saying a stock with +5 % annual drift “usually goes up in any given month” and declaring the drift irrelevant.
2\. Horizon length (time) does change the payoff probability — exactly as the original statistical principle predictsIf real commodity prices follow a process with long-run negative drift μ ≤ 0 (Simon’s core claim: human ingenuity expands supply faster than demand), the mathematics is straightforward. For log-prices modeled as Brownian motion with drift:$P(\text{price}_{t+T} < \text{price}_t) = \Phi\left( \frac{-(\mu - \sigma^2/2)\sqrt{T}}{\sigma} \right)$
- μ < 0 (downward drift) + larger T → the argument inside Φ grows large positive → probability → 1.
- Short fixed T = 10 years: volatility (σ) swamps the drift; you can easily get P < 50 % (as Kiel found).
- Very long T: the trend dominates almost surely (LLN on the average return per unit time).
This is precisely the area of statistics where “likelihood of a reasonable bet paying off increases with time.” The bet is “reasonable” if it aligns with the true long-run drift. Kiel et al. only examined fixed short windows; they did not test longer horizons.3. Evidence on the actual long-run drift
- Mark Perry’s inflation-adjusted Dow Jones-AIG Commodities Index (1934–2013) showed a significant downward trend — Simon wins over that multi-decade horizon.
	[en.wikipedia.org](https://en.wikipedia.org/wiki/Simon%E2%80%93Ehrlich_wager)
- “Time prices” (hours of labor needed to buy the same basket) fell ~87 % from 1900–2019; Simon wins ~54 % of periods (70 % excluding war years).
	[humanprogress.org](https://humanprogress.org/luck-or-insight-the-simon-ehrlich-bet-re-examined/)
- Even raw real metal prices since 1900 are roughly trendless despite enormous production growth — consistent with Simon’s abundance thesis, not Ehrlich’s scarcity explosion.
Grantham’s counter-example (1980–2011, longer period, Ehrlich wins 4/5 metals) is just one draw that happened to catch a commodity super-cycle; it does not refute the drift mathematics.Bottom lineThe assertion is right that the 1980–1990 start date was lucky timing for a fixed 10-year bet — short horizons are noise-dominated, and most such windows favored price rises. But that is not a general statistical refutation of Simon’s view or proof that “luck beats expertise.”When you apply the correct tools (drifted time series + Law of Large Numbers), the probability that a bet on falling real resource prices pays off increases with the length of time if Simon’s long-run drift is correct — which the century-scale data (especially time prices and long indices) support far more than the rolling 10-year count suggests. The 1980–1990 bet was one noisy realization; the deeper insight about abundance over time is the one that strengthens as the horizon lengthens. Kiel et al. showed variability in short windows; they did not disprove the trend that makes the payoff probability rise with time.

Quick Answer