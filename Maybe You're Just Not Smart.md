#Cremieux 

Test anxiety is more about low IQs than anxiety interfering with performance

---

By Cremieux
Aug 08, 2024 06:13 PM
11 min. read
View original

---

You’ve probably met or heard of someone who claimed to be ‘bad at tests,’ to be ‘anxious about test-taking,’ or some other euphemism for ‘I score poorly.’ The typical explanation for poor scoring is self-serving and naturally has less to do with the person being unintelligent and more to do with anxiety interfering with their ability to show their skills or with tests being unfair.

Researchers have taken this to its logical conclusion with concepts like “[stereotype threat](https://psycnet.apa.org/record/1996-12938-001),” “[cognitive interference](https://psycnet.apa.org/doiLanding?doi=10.1037%2F0022-3514.46.4.929),” and “[self-fulfilling](https://www.taylorfrancis.com/chapters/edit/10.4324/9781315617367-3/fear-academic-failure-self-fulfilling-prophecy-dietrich-wagner-taiga-brahm)[prophecies](https://psycnet.apa.org/record/1974-10487-001).” These theories have intuitive appeal. Everyone has felt anxious before, and they _know_ that people can slip up thanks to that feeling. ‘Choking’ during an interview, speech, or important moment of a competition is another human near-universal, so when people hear about these theories, they’re quick to accept them.

But intuitive appeal isn’t enough to skate by on. Theories must be tested.

### Threatening Stereotype Threat

Stereotype threat was first introduced [in 1995 by Steele and Aronson](https://psycnet.apa.org/doiLanding?doi=10.1037%2F0022-3514.69.5.797) and since then it’s been widely considered to be a means of explaining the approximately one Cohen’s _d_ Black-White gap in test score performance in the United States. Steele and Aronson proposed that Blacks might perform worse in tests because they were at risk of “confirming, as self-characteristic, a negative stereotype about [their] group.” They affirmed this effect’s existence in a series of studies in which they informed Black participants about said stereotypes in various ways and watched their scores in subsequent tests come out lower relative to Whites. Let’s take a look.

In the figure below, marked “A”, you can see a re-rendering of Steele and Aronson’s Figure 2 which illustrates what happened to the scores of Blacks and Whites who took cognitive tests in and outside of the “Threat” condition where they were or were not made aware of the stereotype that Blacks are less intelligent than Whites.

Figure A seemingly makes it clear that Steele and Aronson found that Blacks performed worse than Whites due solely to the impacts of stereotype threat on their ability to perform well in tests. But notice the y-axis label: the scores are the mean numbers of items solved, _adjusted for each person’s earlier SAT score_. If we take the figure as it is, then we might end up thinking that the theory works as in this figure, marked “B”, and the SAT scores were just as low for the sample as the “Threat” condition score deficit implies.

To put “B” in other words, [Sackett, Hardison and Cullen](https://psycnet.apa.org/record/2004-10043-001) described it as the belief that “There is a large score gap on commonly used tests; this mirrors the gap found in the threat condition in Steele and Aronson’s work. But when threat is eliminated, the gap disappears.” Because the original chart featured adjustment for prior scores, this cannot be right. The correct interpretation is thus provided by this figure, marked “C”:

Figure C illustrates the reality of Steele and Aronson’s result: “In the sample studied, there are no differences between groups in prior SAT scores, as a result of the statistical adjustment. Creating stereotype threat produces a difference in scores; eliminating threat returns to the baseline condition of no difference.” In other words, stereotype threat _cannot_ explain the Black-White gap in the general population, because it _adds_ to the gap that’s already there.

But there’s another catch! Though this seems to be true, the method used to show it is not sufficient to tell us that. The nature of this issue was explained [by Jelte Wicherts in a commentary on Sackett, Hardison and Cullen’s work](https://psycnet.apa.org/record/2005-03019-016). Wicherts remarked: Sackett, Hardison and Cullen remarked on analysis of covariance (ANCOVA)-adjusted means, and the assumptions of ANCOVA are not likely to hold up if stereotype threat operates how Steele and Aronson have proposed. These assumptions are that:

1. The relationship of the dependent variable and the covariate is linear;
    
2. The regression weights of the dependent variable on the covariate are equal for all design cells;
    
3. The variance of residuals is equal over cells, and;
    
4. The covariate is measured without error and is independent of the experimental manipulation.
    

To make it clear why these do not apply in analyses of stereotype threat, consider what stereotype threat implies:

> Stereotype threat theory states that stereotype threat effects particularly influence test scores of people for whom the ability of interest is important or self-relevant. It is likely that within each cell there are individual differences in domain identification. Therefore, the manipulation triggering stereotype threat would result not only in mean effects (i.e., stereotype threat effects identical for each subject) but also in (co)variance effects (i.e., stereotype threat effects differing for subjects) on the dependent variable. Furthermore, if one supposes the presence of a positive correlation between (latent) ability and domain identification, this would result in an interaction between the covariate (i.e., ability as measured by the SAT) and the experimental manipulation (i.e., stereotype threat effects on the dependent variable). Higher SAT scores would imply higher domain identification and therefore stronger stereotype threat effects. This would result not only in a curvilinear relationship between covariate and dependent variable in the affected cell (i.e., stereotype threat condition) but also in differences in regression weights over the cells.

There are also other reasons to expect ANCOVA is inappropriate and the homogeneity of regression weights is violated. For example:

> If mediators such as heightened anxiety or lowered motivation are the causes of lowered test scores within stereotype threat conditions, it is likely that these mediators will also affect the regression of the dependent variable on the covariate…. In addition, added mediator variance (e.g., anxiety variance) could result in differences in error variances between design cells, which would violate the homogeneity of variance assumption.

And to make matters worse, _if_ the SAT scores that the other scores were adjusted for were previously affected by stereotype threat, “the covariate and the manipulation are not independent, which may obscure the effects of the manipulation or even produce effects that are spurious.”

What Wicherts argued was that stereotype threat _explicitly_ predicts violations of the assumptions underlying ANCOVA, potentially invalidating not just Sackett, Hardison and Cullen’s methods, but also those used by Steele and Aronson’s and most other authors who had by then published on the topic (and most who have published since, too). The solution, however, was not to uncritically accept Steele and Aronson’s work—after all, nothing Wicherts argued meant they were right or that Sackett, Hardison and Cullen were wrong—, it was to use structural equation modeling to test for measurement invariance. In the same issue of the journal Sackett, Hardison and Cullen’s work and Wicherts’ reply were published, he did just that, and he laid out the rationale for all other work on anxiety.

[Wicherts, Dolan and Hessen](https://psycnet.apa.org/doiLanding?doi=10.1037%2F0022-3514.89.5.696) provided a thorough and clear explanation of how, ultimately, the key claims of stereotype threat research are a question of measurement invariance. They showed that, unless stereotype threat exactly mimics latent ability, then it should be detectable if you only model latent ability in a multi-group model, because it should only affect _some_ model parameters, and not to the same degree latent ability does. If it impacts one test score, the model would look like this:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F607d9a95-11f6-49e8-9d6d-e68568fabfed_1367x1020.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F607d9a95-11f6-49e8-9d6d-e68568fabfed_1367x1020.png)

Wicherts, Dolan and Hessen 2005, Figure 2

If stereotype threat affects multiple subtests, it would look like this, and at a size large enough to explain the Black-White gap, it would certainly produce a covariance between affected subtests:

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffbf9962a-86f3-4088-8af8-2d252c3ccdf2_993x864.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffbf9962a-86f3-4088-8af8-2d252c3ccdf2_993x864.png)

Wicherts, Dolan and Hessen 2005, Figure 3

If stereotype threat had a nonlinear effect, then its impacts would be expressed as an interaction between individuals’ latent ability and stereotype threat, and those impacts would still be detectable, with predictable consequences on measurements (e.g., subtest Y_4’s loading would decline and the intercept would be downwardly biased).

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F09c49508-c751-4f3f-ba26-e4be159ba648_1041x855.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F09c49508-c751-4f3f-ba26-e4be159ba648_1041x855.png)

Wicherts, Dolan and Hessen 2005, Figure 4

As it just so happens, Wicherts, Dolan and Hessen were able to test measurement invariance in some real data. The first dataset they used was a sample including 295 minorities in the Netherlands who took the Differential Aptitude Test. Stereotype threat was induced, and apparently there was a nonlinear impact, because the bias wasn’t uniform.[1](https://www.cremieux.xyz/p/maybe-youre-just-not-smart?utm_source=post-email-title&publication_id=1163860&post_id=146330117&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email#footnote-1-146330117) The induced bias led lower-performing minorities to perform _better_ and higher-performing minorities to do worse. In fact, in the stereotype threat condition, one of their tests—of numerical ability—became utterly worthless, with 0.1% of the variance in performance explained by intelligence versus 30% for the majority group in the experimental setting and the majority and minority groups in the nonexperimental setting.

Wicherts, Dolan and Hessen replicated that result by showing that there was a biasing effect in two sets of comparisons of men and women. They also noted something already said that should be reiterated:

> Suppose that these data would have been nonexperimental data, stemming from a real-life, or even a high-stakes, test setting. Even then, a test for strict factorial invariance would have pointed toward the measurement bias…. The reanalysis of these data illustrates our point that because of their nature, stereotype threat effects are detectable in principle by means of tests for measurement invariance.

Therefore, the fact that [there is generally](https://www.aporiamagazine.com/p/bias-is-often-unpredictable) _[not](https://www.aporiamagazine.com/p/bias-is-often-unpredictable)_ [measurement bias](https://www.aporiamagazine.com/p/bias-is-often-unpredictable) means stereotype threat is probably not at play in real-world settings.

To bring this back to the top, Wicherts (and crew) clarified a few things about stereotype threat. Firstly, it has to be an influence that biases tests. Secondly, we can detect this influence. Third, Sackett, Hardison and Cullen were right even if they didn’t necessarily use the right methods to show it. For clarity, they were right that stereotype threat is an influence added _on top of_ preexisting group differences, if it’s a thing at all.

These papers strongly demonstrated a key problem with how stereotype threat is interpreted, but the problem apparently went unacknowledged. In a later review, [Tomeh and Sackett](https://scholarworks.bgsu.edu/cgi/viewcontent.cgi?article=1183&context=pad) documented that in the fifteen years since the issue the Sackett and Wicherts papers appeared in, the proportion of journal articles that misinterpreted stereotype threat as an explanation for the Black-White gap declined from 90.9% to a still-high 62.8%, while the proportion of textbooks making the same error fell from 55.6% to an also-high 41.18%. During that period in which psychology evidently failed to update on the matter, the evidence for stereotype threat evaporated, with [effect sizes massively declining](https://psycnet.apa.org/record/2019-26581-001)[2](https://www.cremieux.xyz/p/maybe-youre-just-not-smart?utm_source=post-email-title&publication_id=1163860&post_id=146330117&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email#footnote-2-146330117) to the point of irrelevance in both low- and high-stakes settings, and the evidence for specific effects on [Blacks](https://web.archive.org/web/20210118042515/https://emilkirkegaard.dk/en/2018/11/jelte-wicherts-lost-stereotype-threat-study-for-african-americans/) or [between](https://journals.sagepub.com/doi/abs/10.1177/1932202X211061517)[the](https://www.sciencedirect.com/science/article/pii/S0022440514000831)[sexes](https://www.tandfonline.com/doi/full/10.1080/23743603.2018.1559647).[3](https://www.cremieux.xyz/p/maybe-youre-just-not-smart?utm_source=post-email-title&publication_id=1163860&post_id=146330117&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email#footnote-3-146330117)

### OK, But What About Anxiety?

I’m getting to that.

Anxiety is like stereotype threat. Stereotype threat has to do with anxiety over stereotypes, but anxiety more generally has to do with something that should bias test performance. This leads us to two models:

- Deficit Theory
    
- Interference Theory
    

We can put both theories on the same plot, like so:

Look familiar? “External Variable” was stereotype threat before, but now it’s anxiety. Or it’s language experience, or it’s hot temperatures, or it’s education, or it’s a loud siren outside the testing room window, or it’s… anything that biases tests! The dashed lines represent its impacts in the theory _with bias_, and the black line heading to latent ability represents its impacts in the theory _without bias_. The thing to remember though, is that the black line there could be a covariance; to test directedness, we really need longitudinal data, but either way, the meanings of the theories wouldn’t change:

- **Deficit Theory:** Posits that individuals with test anxiety perform worse because they are lower on the latent ability underlying test performance. For an IQ test, this would thus mean that they’re less intelligent.
    
- **Interference Theory:** Posits that individuals with test anxiety perform worse because anxiety makes it harder for people to show the performance of someone with their level of latent ability.
    

Let’s look at some results.

### Deficits or Interference?

**[Reeve and Bonaccio 2008](https://www.sciencedirect.com/science/article/pii/S016028960700133X):** These authors found that the deficit model fit much better than the interference model. Test anxiety had correlations of -0.20, -0.37, -0.31, -0.33, and -0.09 with tests of verbal comprehension, numerical ability, space visualization, symbolic reasoning, and cognitive speededness in their sample of 185 undergraduate students enrolled in an introductory psychology course at a mid-sized southeastern university.

**[Wicherts and Zand Scholten 2010](https://www.sciencedirect.com/science/article/pii/S0160289609001263):** These authors argued that, if anxiety and low test performance are independently correlated with subsequent performances, then anxiety could make test scores _more_ valid for predicting things. For example, if test scores relate to speaking, anxiety is related to lower test scores, and anxiety makes it harder for people to speak, then we might see test scores being more predictive of speaking than they would be if anxiety weren’t in the picture. This theory held up in a few tests (including some showing that stereotype threat ought to be biasing), so “the effects of test anxiety on cognitive test performance may actually _enhance_ the validity of tests.”

**[Sommer and Arendasy 2014](https://www.sciencedirect.com/science/article/abs/pii/S0160289613001694):** These authors found that the deficit model fit much better than the interference model. State and trait anxiety correlated negatively with psychometric _g_ in their sample of 411 Bachelor and Master’s degree psychology students.

**[Sommer and Arendasy 2015](https://www.sciencedirect.com/science/article/abs/pii/S0160289615001075):** These authors found that the deficit model fit much better than the interference model. Trait test anxiety correlated negatively with psychometric _g_ in their sample of 1,768 applicants to a medical university.

**[Sommer and Arendasy 2016](https://www.sciencedirect.com/science/article/abs/pii/S1041608016301121):** These authors found that the deficit model fit much better than the interference model. Wait a second—this is the same sample as Sommer and Arendasy’s 2015 study! It’s not surprising this was a replication. What you might be wondering is… why was it republished? Simple: The 2015 study used cognitive tests, and the 2016 study affirmed the result with high-stakes achievement tests. I guess using different variables with substantively different meanings is a good enough reason to do two highly similar papers with the same sample.

**[Sommer and Arendasy 2019](https://www.sciencedirect.com/science/article/abs/pii/S0160289618302125):** These authors found that the deficit model fit much better than the interference model. This result was interesting because they split their sample of 1,628 medical school applicants into four groups with different levels of test anxiety and appraisals of the fairness of admissions testing, and there was no bias across the groups, so neither anxiety nor thinking testing is unfair actually compromised test fairness.

**[Jendryczko, Scharfen and Holling 2019:](https://www.mdpi.com/2079-3200/7/4/22)** These authors found that interference was present and it produced bias, but they also had longitudinal data and were able to show that this bias only persisted for the first two testing sessions, and thereafter, disappeared. This sample included 297 students at the University of Münster, who completed every testing session (original sample: 326), but another 21 also had to be removed because they took more than three hours to take the tests, indicating something might have been off about their scores. Ultimately, the sample ended up being 225 students because 51 got perfect scores for three or more sessions in a row and they had to have their data dropped.[4](https://www.cremieux.xyz/p/maybe-youre-just-not-smart?utm_source=post-email-title&publication_id=1163860&post_id=146330117&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email#footnote-4-146330117)

There are not many more studies that do proper tests, so I’ll cut myself off here and provide a wrap-up.

### Maybe You’re Just Not Smart

The anxious tend to do worse on tests not because anxiety interferes with test performance, but because they tend to have lower levels of ability. A possible explanation for the association is, therefore, that living the life of someone with low ability gives people a life of learning experiences that rightly promote anxiety about test performance, even if that anxiety doesn’t play a role in how well people test.

Now there are some gaps in the literature, but thanks to the size of the stereotype threat literature, I think it’s safe to argue those gaps are small.

The biggest gap has to do with the representativeness of sampling and the presence of anxiety as an interfering versus deficit-representing variable in high-stakes settings. Since high-stakes setting tend to see reduced stereotype threat—an anxiety-based hypothesis—I’m going to say ‘anxiety probably has reduced impacts in testing environments that matter.’ One down.

Since we see invariance most of the time in representatively sampled comparisons of demographic groups proposed to be differentially impacted by stereotype threat, I’m going to argue even further that the deficit account is probably right if there’s any truth whatever to groups varying in their anxiety levels. Since invariance generally applies to male-female comparisons and women _definitely_ tend to be more anxious, I’ll wager the support is strong.

Or in other words, it’s not that you’re bad at taking tests[5](https://www.cremieux.xyz/p/maybe-youre-just-not-smart?utm_source=post-email-title&publication_id=1163860&post_id=146330117&utm_campaign=email-post-title&isFreemail=false&r=7br8e&triedRedirect=true&utm_medium=email#footnote-5-146330117), it’s that you’re just not that smart.

![](chrome-extension://eppedlbobmdflmhleafebmahnbphgipb/assets/icons/icon-128.png)