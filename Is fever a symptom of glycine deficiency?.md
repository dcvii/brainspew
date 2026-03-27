---
title: Is fever a symptom of glycine deficiency?
source: https://www.lesswrong.com/posts/87XoatpFkdmCZpvQK/is-fever-a-symptom-of-glycine-deficiency
author:
  - "[[By Benquo]]"
published:
created: 2026-03-24
description:
tags:
  - brain_spew
  - health
---
*Curation Notice by Raemon*

Curated. I was personally more excited for the "glycine and/or cysteine maybe help with sleep" suggestion than for the fever reduction speculation, although the latter is an interesting idea.

I haven't done a super deep epistemic spot check here\[1\] but I did a few rounds of asking LLMs and colleagues whether the claims checked out (which warned that the evidence for some of them isn't very robust and some are misleading\[2\]).

But this is a genre of post I'd like to see more of – a nice practical combo of engaging with science literature while reasoning about underlying mechanisms, and what sort of goals actually make sense. And, it provides both an immediate practical takeaway as well as an interesting path for further study.

There's also a bit of an interesting connection between "treating the symptom vs disease" and "addressing an indicator vs the underlying phenomena", with parallels to other Benquo work about not destroying information and ability to communicate (in more classical social/intellectual contexts). I don't have an immediate takeaway from that but feel a vague sense that it added some depth to an existing frame.

I find myself curious whether the original orexin post was a major motivator for this post, or if Benquo would have likely written this up anyway. (Regardless, I appreciate a 4 year old post getting some followup)

*\[1\] We don't have time to vet curations at a "serious review" level*

*\[2\] In particular, the claims about "body produces 3 grams a day, and needs 10-60 grams" are coming from a few low powered studies that aren't all studying the same thing. And, the post focuses more on glycine than on cysteine and I'm not sure why. [See full llm transcript](https://claude.ai/share/5ab2ffd0-f8de-4982-ba5c-9fc84eab6131)*

---

A 2022 LessWrong post on [orexin and the quest for more waking hours](https://www.lesswrong.com/posts/sksP9Lkv9wqaAhXsA/orexin-and-the-quest-for-more-waking-hours) argues that orexin agonists could safely reduce human sleep needs, pointing to short-sleeper gene mutations that increase orexin production and to cavefish that evolved heightened orexin sensitivity alongside an 80% reduction in sleep. Several commenters discussed clinical trials, embryo selection, and the evolutionary puzzle of why short-sleeper genes haven't spread.

I thought the whole approach was backwards, and [left a comment](https://www.lesswrong.com/posts/sksP9Lkv9wqaAhXsA/orexin-and-the-quest-for-more-waking-hours?commentId=yogySdS6icfjnrXW3):

> Orexin is a signal about energy metabolism. Unless the signaling system itself is broken (e.g. narcolepsy type 1, caused by autoimmune destruction of orexin-producing neurons), it's better to fix the underlying reality the signals point to than to falsify the signals.
> 
> My sleep got noticeably more efficient when I started supplementing glycine. Most people on modern diets don't get enough; we can make ~3g/day but can use 10g+, because in the ancestral environment we ate much more connective tissue or broth therefrom. Glycine is both important for repair processes and triggers NMDA receptors to drop core temperature, which smooths the path to sleep.

While drafting that, I went back to Chris Masterjohn's page on [glycine requirements](https://chrismasterjohnphd.com/blog/balancing-methionine-and-glycine-in-foods-the-database/). His estimate for total need is 10 to 60 grams per day, with the high end for people in poor health. I had just written that glycine lowers core temperature. What if those are connected?

Is fever what happens when you are too glycine-depleted to fight infection through the more precise mechanisms glycine enables?

## Glycine helps us sleep by cooling the body

The established explanation for glycine improving sleep is that it lowers core body temperature. Glycine helps activate NMDA receptors in the brain's master circadian clock (the suprachiasmatic nucleus, or SCN). This causes blood vessels near the skin to widen, dumping heat from the core to the surface. The body needs its core temperature to drop in order to fall asleep, and glycine accelerates that drop. In rats, surgically destroying the SCN eliminates glycine's sleep-promoting and temperature-lowering effects.

## Glycine cleans our mitochondria as we sleep

Your mitochondria produce energy, and as a byproduct they generate reactive oxygen species (ROS), chemically aggressive molecules that damage proteins, lipids, and DNA. ROS accumulate during wakefulness. Amber O'Hearn's 2024 paper " [Signals of energy availability in sleep](https://pmc.ncbi.nlm.nih.gov/articles/PMC11390529/) " synthesizes the evidence that this accumulation is a key signal driving the need for sleep: wakefulness generates ROS, ROS buildup triggers sleep, and sleep clears them.

A [Drosophila study](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.2005206) tested multiple short-sleeping mutant lines with mutations in unrelated genes. All were more vulnerable to oxidative stress than normal flies. When the researchers forced normal flies to sleep more, those flies survived oxidative stress better. And when they reduced ROS specifically in neurons, the flies slept less, as if the need for sleep had partly gone away. Their conclusion: oxidative stress drives the need for sleep, and sleep is when the body does its oxidative cleanup.

The body's main intracellular antioxidant is glutathione, a small molecule made from three amino acids: glutamate, cysteine, and glycine. In many contexts, glycine is the [bottleneck for glutathione production](https://pmc.ncbi.nlm.nih.gov/articles/PMC9879756/): you have plenty of the other two ingredients, but not enough glycine to keep up. If you are glycine-deficient, you cannot make enough glutathione, you clear ROS more slowly during sleep, and you need more sleep to achieve the same degree of clearance. That is a complete mechanistic chain from glycine deficiency to increased sleep need, and it is entirely independent of the NMDA temperature pathway.

## Most people could use more glycine

Glycine is classified as a "non-essential" amino acid because the body can make it, primarily from another amino acid called serine. But the body only produces about 3 grams per day. Estimated total requirements range from [10 to 60 grams per day](https://chrismasterjohnphd.com/blog/balancing-methionine-and-glycine-in-foods-the-database/) depending on health status, <sup><a href="https://www.lesswrong.com/posts/87XoatpFkdmCZpvQK/is-fever-a-symptom-of-glycine-deficiency#fn-8oiJooaAs2FY3fJQf-1">[1]</a></sup> because glycine is consumed in enormous quantities by the production of glutathione, creatine, heme, purines, bile salts, and collagen.

In the ancestral environment this was not a problem. Traditional diets included connective tissue such as skin, tendons, cartilage, and bone broth, all rich in collagen, which is about one third glycine by amino acid count and one quarter by weight. Modern diets, built around muscle meat and discarding connective tissue, cut glycine intake dramatically.

One group of researchers estimated that most people adapt to this deficit by [reducing collagen turnover](https://www.westonaprice.org/health-topics/abcs-of-nutrition/beyond-good-and-evil/), letting damaged collagen accumulate with age, and that this may contribute to arthritis, poor skin quality, and other consequences of aging. Others have noted that markers of glycine deficiency appear in the urine of vegetarians, people on low-protein diets, children recovering from malnourishment, and pregnant women.

## Fever is plan B for fighting infection; glycine supports plan A

Fever slows pathogen replication, makes immune cells move faster and multiply more, helps them engulf pathogens more effectively, triggers the production of protective stress-response proteins, and speeds antibody production. But it is metabolically expensive (roughly 10 to 13% increase in metabolic rate per degree Celsius) and causes significant collateral discomfort and tissue stress.

Glycine enables several cheaper alternatives to the same functions.

Macrophages are the immune cells that eat pathogens and coordinate the inflammatory response. They have [glycine-sensitive chloride channels](https://pmc.ncbi.nlm.nih.gov/articles/PMC10379184/) on their surfaces. When glycine binds these channels, it calms the cell down: chloride flows in, shifting the cell's electrical charge in a way that suppresses the calcium signaling needed to produce inflammatory molecules. These molecules are called cytokines (the important ones here are TNF-alpha, IL-1-beta, and IL-6), and they are what drive the fever response. Glycine dampens the production of these pro-inflammatory cytokines while increasing production of the anti-inflammatory cytokine IL-10.

Pyroptosis is a form of inflammatory cell death where immune cells fighting an infection blow themselves up, releasing their inflammatory contents into surrounding tissue. This is useful for eliminating pathogens but causes collateral tissue damage. Glycine [prevents macrophages from bursting open](https://www.nature.com/articles/s41419-019-1559-4) during pyroptosis without blocking the internal machinery that kills the pathogen inside the cell. The macrophage can do its job without self-destructing. In animal sepsis models, glycine treatment has improved survival.

Then there is the extracellular matrix. Collagen, the most abundant protein in the body, forms the structural matrix of tissues and acts as a physical barrier against pathogen spread. Collagen is one-third glycine. A [three-year study of 127 volunteers](https://www.sciencedirect.com/science/article/pii/S1756464620305429) (not randomized or blinded, so take it cum grano salis) found that among the 85 who took 10 grams of glycine daily, only 16 had viral infections, all in the first year and with reduced severity and duration. The control group reported no change in infection frequency. The proposed mechanism is that adequate glycine supports collagen turnover, maintaining the extracellular matrix as a mechanical barrier against viral invasion.

A glycine-replete organism can fight infection through these targeted mechanisms and does not need to escalate as aggressively to raising core temperature. A glycine-deficient organism cranks the thermostat higher and longer.

Elevated temperature directly impairs pathogen replication. Bacteria really do grow slower at 39°C (102°F) than at 37°C (98.6°F). No survivable amount of glycine changes that biochemistry. But the *degree* and *duration* of fever may be substantially modulated by glycine status, because many of the things fever accomplishes systemically (immune cell function, inflammation control, tissue protection) are things glycine accomplishes through targeted molecular mechanisms.

This leads to a testable prediction: people with high glycine and glutathione status should mount lower fevers for equivalent infections while maintaining equivalent or better outcomes. I am not aware of anyone having studied this directly, because nobody frames the question this way. But the mechanistic pieces are all published. Some are well-established (glycine's role in glutathione synthesis, macrophage chloride channels), others more preliminary (the ECM/infection study). They are just sitting in different literatures (sleep biology, amino acid metabolism, innate immunology, pyroptosis research) and nobody has connected them.

## Glycine's cooling effect via the SCN is unrelated to its immune benefits

Remember the NMDA temperature pathway from the beginning of this essay, the one that made me notice the coincidence? It turns out to be a red herring as a link between sleep and immunity. The sleep pathway (glycine acting on NMDA receptors in the SCN to cool the core) and the immune pathway (glycine acting on chloride channels on macrophages to prevent pyroptosis) are completely independent. They involve different receptors, different cell types, and different organ systems.

So when I noticed that glycine lowers temperature and that sick people need more glycine, I was right that they were connected, but for none of the reasons I initially thought. The NMDA pathway had nothing to do with it. I had a true belief ("glycine, temperature, and illness are linked") that happened to be true, but my justification ("because NMDA receptors and thermoregulation") was wrong. A [Gettier case](https://iep.utm.edu/gettier/)!

But the wrong reason led me to the right question.

## Glycine turns out to be a legitimate antipyretic after all

In [rabbit experiments](https://pubmed.ncbi.nlm.nih.gov/6781712/), glycine injected directly into the brain's fluid-filled cavities reduced fever caused by two different triggers: substances released by white blood cells during infection (leukocytic pyrogen) and prostaglandin E2, which is the specific molecule the brain's thermostat uses to raise the temperature setpoint during illness. This is a different operation from the sleep-onset mechanism. The sleep pathway lowers the thermostat from 37°C (98.6°F) to 36.5°C (97.7°F) to help you fall asleep. The antipyretic effect prevents the thermostat from being cranked up to 39°C (102°F) during infection.

So glycine suppresses fever directly (which might confound the testable prediction above), and unrelatedly lowers core temperature before sleep, and unrelatedly improves specific immune response in ways that reduce the infection-related inflammation that raises body temperature. Three independent pathways, with no apparent mechanistic connection, all drawing on the same pool of one simple, cheap amino acid that modern diets undersupply.

## Practical considerations

Glycine powder is cheap, roughly 2 to 3 cents per gram. It is mildly sweet and dissolves easily in water. There is no known toxicity at supplemental doses aside from gastrointestinal upset at high doses; 60 grams per day has been used in schizophrenia trials. For most people, 10 to 15 grams per day in divided doses (some with meals, some before bed) would address the estimated deficit. Three grams before bed is the dose studied for sleep improvement specifically.

This is not comprehensive nutritional advice. For instance, cysteine is the other bottleneck for glutathione production, and people who eat little animal protein or are acutely ill may benefit from supplementing NAC (N-acetylcysteine) alongside glycine.

Alternatively, you can eat the way your ancestors did: bone broth, skin-on poultry, oxtail, pork rinds, and other collagen-rich foods. One gram of collagen for every ten grams of muscle meat protein roughly restores the ancestral glycine-to-methionine ratio.

Before reaching for a pharmaceutical intervention to override a biological signal, it is worth asking whether the signal is accurately reporting a problem you could fix with inputs. Orexin tells your body about its energy metabolism. Fever tells your body about its immune status. If you are not providing the substrates those systems need to function, the signals will reflect that, and the right response is to supply the substrates, not to shoot the messenger.

1. The ~3g/day endogenous synthesis figure and ~10g/day shortfall estimate come from [Meléndez-Hevia et al. 2009](https://link.springer.com/article/10.1007/s12038-009-0100-9), a peer-reviewed metabolic flux analysis that explicitly accounts for glycine recycling in the procollagen cycle. 3g before bed is the dose studied for sleep improvement ([Inagawa et al. 2006](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1479-8425.2006.00193.x), [Yamadera et al. 2007](https://onlinelibrary.wiley.com/doi/full/10.1111/j.1479-8425.2007.00262.x)). 15g gelatin before exercise doubled a collagen synthesis marker in blood ([Shaw et al. 2017](https://pubmed.ncbi.nlm.nih.gov/27852613/)). Glycine at around 200 mg/kg/day (roughly 14g for a 70kg person) has been used in isovaleric acidemia, a rare metabolic disorder where glycine conjugates toxic organic acids for excretion ([Tajima et al. 2018](https://pmc.ncbi.nlm.nih.gov/articles/PMC6282653/)). 0.8 g/kg/day (about 60g for a 75kg person) has been used in multiple double-blind schizophrenia trials, where it was well tolerated over the study period and produced significant reductions in negative symptoms ([Heresco-Levy et al. 1999](https://pubmed.ncbi.nlm.nih.gov/9892253/), [2004](https://pubmed.ncbi.nlm.nih.gov/14732596/)).