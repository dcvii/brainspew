---
title: "Anti-Vaxxers Are Innumerate"
source: "https://www.cremieux.xyz/p/anti-vaxxers-are-innumerate?publication_id=1163860&post_id=219636536&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[Cremieux]]"
published: 2026-10-09
created: 2026-10-12
description: "Anecdotes have quantitative implications"
tags:
  - "brainspew"
---
Today’s post is brought to you by my sponsor, [Mechanize](https://www.mechanize.work/?utm_source=cremieux&utm_campaign=2026-05-21). They’re [hiring junior software engineers](https://mechanize.work/apply/software-engineer/?utm_source=cremieux&utm_campaign=cremieux) at $300K/year base salary.

---

![New Pneumococcal Vaccines: Important Facts to Know | VaxCare](https://substackcdn.com/image/fetch/$s_!tJ7F!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8c0f6b7d-ec6a-4de7-8615-338fd6a91bb5_739x415.jpeg)

New Pneumococcal Vaccines: Important Facts to Know | VaxCare

It’s widely understood that anti-vaccine activism is predicated on illiteracy, conspiracist ideation, and a resistance to updating in response to empirical findings, but it’s less well-known that anti-vaccine activists (anti-vaxxers, colloquially) are also generally innumerate and—despite their invocation of drawn-out arguments, biological mechanisms, and chains of causation—they don’t think through the numbers they like to cite. The evidence of this is everywhere in their arguments, but nowhere is it more distinct than when they try to invoke statistics in support of anecdotes. Consider the McDowell triplets.

[The story goes](https://archive.li/S84SO):

> All three of Brenda McDowell's triplets, she attests, 'shut down' within hours of each other after receiving their routine pneumococcal vaccines — later to be diagnosed with Autism Spectrum Disorder.

[Alternatively](https://archive.li/Yb8Fy):

> Healthy triplets. One pneumococcal vaccine. One single day. Within hours, all three babies changed forever.  
>   
> Claire screamed uncontrollably… then went completely silent.  
>   
> Her brothers Richie and Robbie lost their smiles, their sounds, their milestones.  
>   
> All three diagnosed with severe autism. Only one has ever partially recovered.

And on the odds, anti-vaccine activists have provided three estimates. [For example](https://archive.li/8aQON), “A geneticist explained that the chance to this happening to 2 of our triplets would be 1 in 4 million. It happened to all 3.” Alternatively, anti-vaccine activist Steve Kirsch has proffered two probabilities: “ [The chance of that happening if autism is happens randomly to kids is less than 1.66e-13](https://archive.li/IQftN) ” and, [from the same person](https://archive.li/GC97g):

> To see 3 (or more) events in a specific 24-hour window when you expected to see 3e-5 events is:
> 
> `>>> poisson.sf(2,3e-5)   4.499898751214992e-15`
> 
> We’d want to multiple this by 1,000 since it could happen on any of the days for the first child. This is still orders of magnitude from ever happening.

All of this might sound convincing if you ignore the discrepancies [^1] and also don’t think about it for even a few seconds. But if you put any amount of thought into this, it falls apart. It *obviously* does not demonstrate any risk from vaccines. Think about it: if this is true, and vaccination caused all of these children to suddenly become autistic, what would the implied effect of vaccination be on the odds of autism? We can calculate that![^2]

If 90% of people get vaccinated and the prevalence of autism is 1%, the implied odds ratio is 4.89 [^3]. Moreover, the rate of autism among the unvaccinated should be 0.22% versus 1.09% for the vaccinated, meaning that 77.6% of all autism is directly caused by vaccines, and in particular, by the vaccine these children received, the pneumococcal conjugate vaccine (PCV). Is this prediction even remotely plausible? No.

We know that PCV is unrelated to autism in [individual-level](https://www.acpjournals.org/doi/10.7326/ANNALS-25-00997) [data](http://www.jpeds.com/article/S0022-3476\(13\)00144-3/fulltext) —a clear prediction failure—and that autism doesn’t spike in the years after the vaccine is introduced—a causally-informative prediction failure![^4] Take a look:

![](https://substackcdn.com/image/fetch/$s_!kC0S!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdc213622-95cd-4b6f-9086-09680d6ef5e4_3750x3563.png)

Where does this leave the anecdote? Well, it’s obviously wrong and the extreme numbers cited by proponents of it must be off. We *know* this is the case, because it must be the case given the observed numbers. For it to be any other way, the autism rate would have to be enormously understated or the vaccination rate overstated or… something else that’s obviously not happening.

What’s really happening in this anecdote is that autism runs in families—it’s highly heritable—to the tune of younger siblings of autistic children having a 10-20% chance of having autism themselves ([this study](https://publications.aap.org/pediatrics/article-abstract/128/3/e488/30689/Recurrence-Risk-for-Autism-Spectrum-Disorders-A) estimated 18.7%) and the timing of vaccination coincides with roughly the time when many parents notice their kids are autistic. Across millions of vaccinated families, large numbers of parents will begin to notice their kids’ autism around the time they get shots, and if they’re all getting their appointments together like these triplets were, then a coincidence of diagnostic timing is to be expected.

The story of the McDowell family relies on vividness to make it seem like something is amiss and vaccines are to blame, but it’s statistically quite probable. In fact, we can just work through Kirsch’s spectacular numbers to get at why we *do* expect to see examples like this. Here’s a diagram:

![](https://substackcdn.com/image/fetch/$s_!NHWG!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1293d5d8-3bf5-4678-b6e4-2c9fa5b174e5_3900x2100.png)

From left to right, we have estimates from different scenarios. On the left, you have Kirsch’s implausibly small probability estimate that he—as we’ve shown, improperly—believes establishes that vaccines cause autism. This estimate comes from his tweet and it’s based on taking an autism risk of 1 per 100 by age 4 in 2007 with onset somewhere between ages 1 and 4 (i.e., 1,095 days), noting three kids means 3e-5 expected cases per day, and then computing the Poisson chance of three or more events on one day as poisson.sf(2, 3e-5) and multiplying by 1,000 for “any of the days”, giving roughly 4.5e-12, but using the per-child rate, giving 1.66e-13. This estimate assumes children are independent, that autism begins on a specific, datable day, that every day in the window is equally likely and dated separately per child, and that nobody went looking for the family—all incorrect.

The next estimate to the right simply takes his inputs and computes the number based on his assumptions correctly. The assumptions remain wrong; the point, however, is to show that an implausibly small number still follows from them even when you do the calculation correctly. But what happens when we start correcting the erroneous assumptions? The next estimate removes independence: given the first child is autistic, the next child has an 18.7% chance of also being autistic. From the same study, we also see that, given two siblings are affected, the risk for the third one is 32%. Incorporating this alone raises the probability by about 600 times, and this *understates* how much the probability should improve, because triplets also share a womb and birth timing.[^5]

The number to use isn’t 1/1,095²—”three independent onset days”—, but *q*, the chance that parents tie three events to one visit. This means, given three autistic, same-age siblings vaccinated together, we expect this outcome to happen in approximately 1-in-6,700 triplet sets. We know this for a few reasons: autism doesn’t begin on a single day (it’s developmental); triplets share developmental timing and appointments; and parents date the onset of autism after diagnosis and anchor to memorable events like well visits. In other words, diagnoses are not independent draws![^6]

Finally, we have the probability of at least one family like the McDowells. This is based on an extremely conservative calculation taking 30,000 U.S. triplet sets born between 2000 and 2020 [^7] and multiplying by the previous probability of 1.5e-4. P(at least one) = 1 - (1 - p)ᴺ ≈ 1 - e⁽ᴺᵖ⁾ ≈ 0.99 (0.83 to >0.999). Even this is conservative, as it assumes families are independent, it leaves out quadruplets, other countries, and it omits both earlier and later years.

We can confidently state that this anecdote is uninformative because a case like this *is expected* by chance. At most it could move the odds very slightly. Once we also acknowledge that its implied effects aren’t realized in the general population data, we’re left with the realization that this whole thing was pointless to bring up.[^8]

---

### This is All They Have

This sort of poor-quality evidence stated without any caveats or rigorous interrogation is all that anti-vaccine activists have to go off. They cite lurid anecdotes and don’t check their implications; [they get confused by confounded and selected associations](https://www.cremieux.xyz/p/fast-fact-check-does-hep-b-vaccination); [they fail to recognize the role of institutions in driving reporting on disease](https://x.com/cremieuxrecueil/status/1970216663812321719); and they very generally do not understand the conditions they’re talking about. To end on an example, consider the fact that [the apparent ‘rise’ in autism is entirely due to diagnostic drift](https://www.cremieux.xyz/p/an-autism-challenge). This is well-established, and yet anti-vaccine activists try to explain it: they blame it on vaccines, even though there’s nothing to explain!

---

*This was a timed post. The way these work is that if it takes me more than an hour to complete the post, an applet that I made deletes everything I’ve written so far and I abandon the post. You can find my previous timed post [here](https://www.cremieux.xyz/p/still-discriminating).*

---

**A message from my sponsor, Mechanize:**

[We’re hiring](https://mechanize.work/apply/software-engineer/?utm_source=cremieux&utm_campaign=cremieux) software engineers to build environments and evals that frontier AI labs use to train coding agents.

To get a better sense of the work we do, you can check out [GBA Eval](https://gbaeval.com/), where we had models build Game Boy Advance emulators from scratch and scored their performance.

Base pay starts at $300K/year for junior software engineers, with more for senior roles, plus equity and performance bonuses. [Apply here](https://mechanize.work/apply/software-engineer/?utm_source=cremieux&utm_campaign=cremieux).

∙

[10 Restacks](https://substack.com/note/p-219636536/restacks?utm_source=substack&utm_content=facepile-restacks)

[^1]: Some anti-vaccine activists even claim that the vaccine that was used on the McDowell triplets was the MMR, but in most reporting and per the parents in interviews, it was PCV.

[^2]: Here:

```
implied_or <- function(prev = 0.01, cov = 0.90, n_kids = 3, thr = 0.5) {
  rr <- 1 / (1 - thr^(1 / n_kids))        # RR at which P(all n cases vaccine-caused) = thr
  p0 <- prev / (cov * rr + 1 - cov)       # unvaccinated risk, holding overall prevalence fixed
  p1 <- rr * p0                           # vaccinated risk
  data.frame(coverage   = cov,
             RR         = rr,
             OR         = (p1 / (1 - p1)) / (p0 / (1 - p0)),
             risk_unvax = p0,
             risk_vax   = p1,
             PAF        = 1 - p0 / prev,          # share of all autism caused by vaccines
             excess_pp  = 100 * (prev - p0),      # percentage points of the overall rate
             max_BF     = (1 / cov)^n_kids)       # most the anecdote can favour any effect over none
}
rbind(implied_or(cov = 0.90), implied_or(cov = 0.92))
```

[^3]: At 92% coverage as a robustness check, it’s also 4.89. I invite you to fiddle around with the code in Footnote 2.

[^4]: This data comes from my soon-to-be-released global autism-vaccination causal study and data-gathering project. It’s not quite done yet, as I’m still gathering data from jurisdictions and waiting on requests for data and FOI requests to be processed, but it will be done soon and the pictured results are firm and easily checked.

[^5]: If we also use today’s prevalence of roughly 1-in-36 rather than 1-in-100, this row would move up by about three times more.

[^6]: In this calculation, I set *q* to 25% and the ends of the bars depict 10-50%, so even at a low 10%, the number would be much higher than Kirsch’s. It is worth noting that given about 10% of children are unvaccinated, we should shave off an additional tenth of the probability. Also, regardless, this is the probability a family like this appears, not the probability vaccines cause autism.

[^7]: For reference on how conservative this is, NCHS recorded 5,967 triplet births in 2007 alone.

[^8]: This anecdote could represent an actual case of vaccine-induced autism if there’s a rare susceptibility factor affecting, say, 1-in-10,000 kids, but a single anecdote doesn’t provide us with the ability to rule that in.