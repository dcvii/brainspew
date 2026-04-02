---
title: "\"Nutrition Science's Most Preposterous Result\" is False"
source: "https://www.cremieux.xyz/p/nutrition-sciences-most-preposterous"
author:
  - "[[Cremieux]]"
published: 2026-04-01
created: 2026-04-02
description: "There's no mysterious health benefit to eating ice cream"
tags:
  - "brain_spew"
---
### There's no mysterious health benefit to eating ice cream

*This was a timed post. The way these work is that if it takes me more than an hour to complete the post, an applet that I made deletes everything I’ve written so far and I abandon the post. You can find my previous timed post [here](https://www.cremieux.xyz/p/social-scientists-are-lazy).*

---

Maybe you’ve seen the headlines: “Harvard can’t figure out why ice cream eaters are healthier”; “The best nutritionists can’t explain it: eating ice cream helps your heart!”; “Studies show a mysterious health benefit to ice cream. Scientists don’t want to talk about it.” If you haven’t, consider yourself blessed, because you were saved from the experience of reading something very obviously wrong.

The idea that ice cream—a food item we can all agree is sugary, fatty, and delicious—is healthy for your heart is principally derived from [an offhanded comment in a dissertation](https://web.archive.org/web/20250501203937/https://dash.harvard.edu/server/api/core/bitstreams/90ef08c0-57ce-4ff9-b6ef-3dc7cdc4f7a3/content). Quote:

> In our study \[of the HPFS, NHS, and NHSII datasets\], ice-cream intake was inversely associated with CVD risk among diabetes patients. This result was unexpected given its considerable saturated fat content (6.7 g per 100g) and sugar (21.2g of per 100g) of which, the majority is added sugar (>60%) and the rest is comprised of naturally occurring lactose. Nonetheless, in a previous study conducted among HPFS, the NHS, and the NHSII participants free of disease at baseline, ice-cream intake was also associated with a lower T2D risk. This result was in agreement with the those from two additional cohort studies, and in a meta-analysis it was estimated that consuming 10g of ice-cream per day vs. 0 g was associated with a 19% lower T2D risk. On the other hand, Ice-cream \[sic\] intake was not associated with risk of total stroke or stroke subtypes.

What are the results? Ice cream was marginally associated with cardiovascular disease (OR = 0.82, *p* = 0.047), whereas it was nonsignificantly related to coronary heart disease (*p* = 0.067) and to stroke (*p* = 0.37) risk.

These are not very impressive results; they’re also not even consistent within the paper. For example, at baseline the study found no relationship between ice cream intake and cardiovascular disease and the relationship only became marginally significant after adding a bundle of controls, including for total dairy product intake. It also wasn’t related at all to cardiovascular disease, coronary heart disease, or stroke risk among diabetics; it wasn’t related to cardiovascular disease among people who had self-reported HbA1c levels; it was related to 33% lower risk among those who reported insulin or other diabetes medication use; the main effect on cardiovascular disease risk became nonsignificant when an 8-year lag was added; and, among ice cream’s correlates including dairy (*r* = 0.17), low-fat dairy (-0.06), cheese (0.11), cream (0.10), fermented dairy (0.07), it was only modestly correlated with high-fat dairy intake (0.46), not correlated with sherbet consumption (-0.02), or consumption of skim and whole milk (0.11 and 0.001), with a modest correlation with yogurt consumption (0.32).

The pattern of results in this paper is seemingly not robust despite *The Atlantic’s* portrayal, and, frankly, it doesn’t seem that meaningful given that the authors’ analysis didn’t go very deep: they didn’t use many controls or a sophisticated control strategy; they didn’t attempt to deal with measurement error; and they didn’t use any designs to figure out if the association was driven by any sort of confounding. It was standard nutritional epidemiology, with all of its defects.

As summarized by John Ioannidis about a decade ago: nutritional epidemiology’s “effects” typically represent the impacts of the cumulative biases present in the research rather than the impacts of eating particular foods. What really matters [is the](https://gwern.net/everything) [crud](https://journals.sagepub.com/doi/10.1177/2515245920917961) [factor](https://psycnet.apa.org/record/2021-46346-001).

---

### Empirical Reanalysis

To look into the ice cream → health hypothesis, I opened up the complete NHANES data and went through progressively more sophisticated models, from basic regressions through doubly-robust estimation, all the way to using family fixed-effects. I wanted to see if the ice cream associations held up, and if they also came with absurd consequences. To make a long paper short, (1) they don’t, and (2) it did.

There are a lot of analyses in the paper, but here I’ll focus on just a few.

Firstly, in Panel A, you’ll notice one set of analyses. The OLS results are the standard cross-sectional correlations, where ice cream seems to relate to things like lower inflammation, higher HDL, lower blood pressure, and so on. But after adding just a few covariates to account for basic confounding, these effects are generally reduced and in the cases of blood pressure, HbA1c, and eGFR, the signs of the effects flip.

When we use very extensive matching on more than 100 different variables, the only thing that survives is that ice cream is associated with being slightly fatter. When we switch over to a plausibly causal analysis—comparing people in the same home—we get a similar picture, where the person who eats more ice cream is a bit fatter, but they’re also a bit less likely to be depressed. But in any case, all of these effects are tiny: certainly too small to matter, but significant because of my large sample size.

![](https://substackcdn.com/image/fetch/$s_!2Ddh!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F46cfb848-1c60-436a-8362-c9c93a9baac6_4379x2223.png)

---

### The ‘Ice Cream Good’ Narrative

The idea that ice cream is a health food and nutrition researchers can’t explain that fact is contrary to evidence. Ice cream doesn’t look particularly good for you if you examine the association with even a little rigor.

This fact runs counter to theorists like Ray Peat *and* to the public’s demand for counterintuitive findings. And, if the narrative that’s sprung up around this idea is true—that researchers at elite institutions couldn’t explain this finding—then it indicts a lot of academia, because ‘Ice Cream Good’ is obviously false and it was never on strong ground to begin with.

---