

Relative risk (RR) is a preferred measure for investigating associations in clinical and epidemiological studies with dichotomous outcomes.
14 min. read
[View original](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email)

---

## 1. Introduction

In both observational and experimental studies, the relative risk (RR) is one of the preferred measures for reporting associations between dichotomous exposures/risk factors and a dichotomous outcome. For clinicians, the RR is often easier to interpret than an odds ratio (OR) [[1](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B1-ijerph-18-05527)]. The RR is defined as the ratio between outcome probabilities obtained in two groups and thus has a very direct probabilistic interpretation compared to the more abstract definition of the OR. Hence, while translating an RR of two to the statement “The risk in the intervention group is twice as high as in the control group”, a similar interpretation would be incorrect for an OR.

When estimating an RR, researchers may encounter a challenge if one of the comparison groups does not experience any event (or if everyone in a group experiences an event), as this would result in an RR of zero or ∞, respectively. In these cases, confidence intervals (CIs) for the RR cannot easily be reported, and in the resulting research papers, it is often concluded that the sample was not large enough to obtain sufficient inference about the RR. However, as the RR is a measure of an association, this is not reasonable. For example, in the case of a randomized clinical trial (RCT) where the outcome is a rare adverse event, a result of no adverse event in the intervention group, but of a moderate number of adverse events in the control group, would give clear evidence of a protective effect of the intervention [[2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B2-ijerph-18-05527),[3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B3-ijerph-18-05527)]. Similarly, in an epidemiological study investigating the efficacy of a vaccine, a result with no observed infections in the group of vaccinated persons, but with some infected persons among the non-vaccinated, could give clear evidence of a positive effect of the vaccine [[4](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B4-ijerph-18-05527)].

In general, it seems erroneous that a study reporting decreasing incidence of an adverse outcome from 10%10% to 1%1% can (possibly) provide strong evidence of a protective effect, while a similar sized study reporting decreasing incidence of the adverse outcome from 10%10% to 0%0% is not considered to provide strong evidence, although the effect size is larger. Hence, it is obvious that the problem with an RR estimate of zero does not indicate an epidemiological weakness of the study but rather a limitation of the statistical procedures used to obtain the estimate and corresponding CI.

This problem has been discussed by Fagerland et al. as a special case without much detail [[5](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B5-ijerph-18-05527)] and in a note on how to approach the problem in R [[6](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B6-ijerph-18-05527)]. Moreover, research [[7](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B7-ijerph-18-05527),[8](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B8-ijerph-18-05527)] has suggested an approximate rule proposing that an upper limit for a CI could be calculated as three divided by the total number of observations. However, these suggestions were made before the development of modern computational possibilities, and they are later discussed in a more current setting [[9](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B9-ijerph-18-05527)].

The aim of this paper is to present, compare, and discuss different statistical approaches to obtain frequentist CIs as well as Bayesian credibility intervals (CrIs) in cases where an RR is estimated to be zero due to no outcome events in one of the comparison groups.

## 2. Materials and Methods

#### 2.1. Motivating Examples

To demonstrate the different approaches, we will present three examples, each of which corresponds to the setting of an RCT with two groups of equal size and an observed incidence of an (adverse) outcome of 0%0% in the intervention group and 10%10% in the control group. These three examples correspond to total sample sizes of 40, 200, and 400, respectively ([Table 1](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t001)). They are chosen as their ranges correspond to most of the study sizes used in clinical practice. Furthermore, we include three additional examples (Examples D, E, and F), corresponding to large (N = 20,000) epidemiological studies with differing incidences of 10%10%, 1%1%, and 0.1%0.1%, respectively, in the reference group. We decided not to include examples in which the group with 0 events is the reference (control) group, as these result in RR estimates of ∞ and, hence, are best handled by presenting the inverse RR using the other group as the reference.

**Table 1.** Examples.

![Table](https://www.mdpi.com/img/table.png)[](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t001)

For clarity, we will denote the group experiencing 0 events as the intervention group, and the group experiencing more than 0 events as the control group, even if this nomenclature may be considered inappropriate in epidemiological studies. Moreover, we will denote positive outcomes as events and negative outcomes as non-events.

First, we will present the investigated approaches. We will start with frequentist approaches to determine CIs for the RR, continue with frequentist approaches utilizing the OR as an approximation of the RR, and end with Bayesian approaches to obtain CrI for the RRs. Subsequently, we will demonstrate the results of applying these approaches to the examples from [Table 1](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t001). All computations are performed in Stata version 16.1. Stata codes are available in [Supplementary File S1](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#app1-ijerph-18-05527).

#### 2.2. Frequentist Approaches

#### 2.2.1. Normal Approximation Formula for the RR

The classical formula for a CI of the RR using the normal approximation is given by

$𝐶𝐼RRN−appr=(𝑅𝑅̂·exp(−1.96·𝑆𝐸RRN−appr);𝑅𝑅̂·exp(1.96·𝑆𝐸RRN−appr))𝐶𝐼RRN-appr=𝑅𝑅^·exp−1.96·𝑆𝐸RRN-appr;𝑅𝑅^·exp1.96·𝑆𝐸RRN-appr$

with

and

where 𝑑1𝑑1 and 𝑑0𝑑0 are the number of events in the intervention group and the control group, respectively, and 𝑛1𝑛1 and 𝑛0𝑛0 are the corresponding total number of observations in each group. Here, 1.961.96 is the 0.9750.975 quantile of the normal distribution, corresponding to a 95%95% confidence interval. This will fail in the case of 𝑑1=0𝑑1=0, as it would imply division by 0 in the standard error (SE). In principle, one could try to determine limits for these expressions for 𝑑1→0𝑑1→0, handling the counts as if they were continuous. For the lower confidence limit, this will result in a limit of 0, while the (more interesting) upper limit can be shown to diverge to ∞ by use of l’Hospital’s rule. Furthermore, as the normal approximation for the CI generally requires counts of at least 5 (or 10) in each cell, this method is discouraged in case of 0 events observed in the intervention group [[10](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B10-ijerph-18-05527)]. Hence, we will not investigate modifications to the normal-based CI for the RR further.

#### 2.2.2. Adding One to Each Cell or Moving One Non-Event to Event in the Intervention Group

A simple ad-hoc approach to avoid these challenges is adding 1 to each cell in the cross table. This will result in an RR estimate slightly higher than 0 and create the possibility of applying standard methods to obtain a CI. However, because the resulting cross table will include 1 as the number of events in the intervention group, normal approximation methods are generally discouraged [[10](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B10-ijerph-18-05527)]. Furthermore, this approach will artificially increase the total sample size by 4, thus suggesting more information than what is obtained in reality, resulting in too narrow confidence intervals. In large studies, this effect will be minimal, but in small studies, the effect should be considered (Approach I in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002) and [Table 3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003)).

**Table 2.** Results: reported intervals are 95%95% CIs for frequentist methods and 95%95% CrI for Bayesian methods. (Note: 0 indicates an estimate formally forced to be 0, while 0.0000.000 indicates an estimate numerically within 0.00050.0005 of 0.)

![Table](https://www.mdpi.com/img/table.png)[](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002)

**Table 3.** Results: reported intervals are 95%95% CIs for frequentist methods and 95%95% CrI for Bayesian methods. (Note: 0 indicates an estimate formally forced to be 0, while 0.0000.000 indicates an estimate numerically within 0.00050.0005 of 0.)

![Table](https://www.mdpi.com/img/table.png)[](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003)

In 1966, Gart [[11](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B11-ijerph-18-05527)] suggested adding 1/21/2 instead of 1 to each cell in the table. This naturally decreases the distortion of the sample size. However, it has been shown [[6](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B6-ijerph-18-05527)] that the resulting CI is quite sensitive to the magnitude of the added term. Furthermore, due to the resulting counts not being integers, this solution has no clear probabilistic interpretation, while approximate methods will still be discouraged due to the low count (0.50.5) in one cell. Again, a one-sided CI can be considered to increase both power and interpretability. Because of the unclear probabilistic interpretation and infeasibility of applying many estimation methods due to non-integer counts, in this paper, we decided not to investigate the approach of adding 1/21/2 further.

A less distorting but similar strategy is to move one observation in the intervention group from no event to event. This results in an event-count of 1 and a non-event-count decreased by 1, without modifying results in the control group. This method preserves the total sample size (and the sample size in each group) as well as the integrity of all counts. One can think of this method as a counterfactual setting, investigating a similar study, where one of the intervention participants did counterfactually experience the outcome event, corresponding to an outcome with (slightly) weaker evidence for a protective effect. However, it should be noted that this will always lead to a more conservative estimate of the RR in the sense that it will indicate a weaker association than is actually present (Approach I in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002) and [Table 3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003)).

Moreover, as the true RR is 0, estimating a lower limit of the CI above 0 does not seem reasonable. Hence, one can obtain additional power and avoid unintuitive results by instead reporting a one-sided upper CI.

#### 2.2.3. Using the OR as Substitute for the RR

It is well known that the OR can be used as an approximation for the RR when the outcome is rare [[12](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B12-ijerph-18-05527)]. In our examples, this implies that the OR often could be a feasible approximation, as the 0 event in the intervention group indicates a low probability, while the probability in most, but not necessarily all studies, will be low in the control group as well. If necessary, the literature suggests approaches to adjust the resulting OR and its CI to achieve a closer approximation to the RR [[12](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B12-ijerph-18-05527),[13](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B13-ijerph-18-05527)].

The classical normal approximation formula for a CI for the OR, as suggested by [[14](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B14-ijerph-18-05527)] is

𝐶𝐼ORN−appr=(𝑂𝑅̂·exp(−1.96·𝑆𝐸ORN−appr);𝑂𝑅̂·exp(1.96·𝑆𝐸ORN−appr))𝐶𝐼ORN-appr=𝑂𝑅^·exp−1.96·𝑆𝐸ORN-appr;𝑂𝑅^·exp1.96·𝑆𝐸ORN-appr

with

and

where ℎ1ℎ1 and ℎ0ℎ0 are the number of non-events in the intervention and the control group, respectively.

Similarly, as in the case of the approximate formula for RR, if we let 𝑑1→0𝑑1→0 (and ℎ1→𝑛1ℎ1→𝑛1), the lower CI limit will converge to 0, while the upper limit will diverge to ∞. Instead, one can apply methods for combinatorically determined CIs for the OR, which typically will be able to handle counts of 0. For instance, the Cornfield approximate CI for the OR [[15](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B15-ijerph-18-05527)] can be estimated in the case of 0 events in the intervention group and will, in this case, always result in a lower CI limit of 0 (Approach II in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002) and [Table 3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003)).

This approach has been improved further by Baptista and Pike [[16](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B16-ijerph-18-05527)] and Fagerland [[17](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B17-ijerph-18-05527)] with exact CIs for the OR including an implementation of the exact CI suggested by Cornfield [[15](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B15-ijerph-18-05527)]. Furthermore, Fagerland [[17](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B17-ijerph-18-05527)] also provided a Stata implementation (merci), which we used to apply these methods. This implementation offers both exact CIs as well as mid-p intervals obtained by approximating a correction term [[17](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B17-ijerph-18-05527)]. As these extensions are currently computationally infeasible for large samples, we only apply these for Examples A, B, and C, with sample sizes of 40–400 and not for examples D, E, and F with a sample size of 20,000 (Approach II in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002)).

#### 2.2.4. Frequentist Regression Models

In general, inference for the RR is possible by binomial regression (a general linear model with logarithmic link function) determining maximum likelihood estimates (MLE). In our examples, this approach will obtain an MLE at a coefficient of −∞−∞ corresponding to an RR of 0. Hence, binomial regression will not result in meaningful estimates and CIs. As with the case of binomial regression, logistic regression is infeasible in the case of an estimated OR of 0, as the MLE will correspond to a coefficient of −∞−∞.

#### 2.2.5. Bootstrapping

As no individuals in the intervention group experienced the outcome event, any bootstrapping sample will result in RR estimates of 0 (or possibly in non-estimability of the RR, if no events in the control group are included in the sample). Hence, a bootstrapped CI will consist of only 0 and thus be inappropriate, although it has, in some cases, been reported in recent literature [[3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B3-ijerph-18-05527)].

#### 2.3. Bayesian Approaches

#### 2.3.1. Priors for the Proportions

The most natural approach for modeling a dichotomous outcome in two groups is to assume priors for the proportion of events in both groups. The posterior of these proportions can then be estimated, and from these, the posterior of the RR can be determined.

The most natural choice of priors is a beta distribution, as this is the conjugate prior for a Bernoulli likelihood [[18](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B18-ijerph-18-05527)]. In this case, with a 𝐵(𝛼,𝛽)𝐵(𝛼,𝛽) prior for a proportion, the posterior will be 𝐵(𝛼+𝑑,𝛽+ℎ)𝐵(𝛼+𝑑,𝛽+ℎ) if d positive and h negative outcomes have been observed. Applying this to our examples, we have an intervention group prior of 𝐵(𝛼1,𝛽1)𝐵(𝛼1,𝛽1), observing 𝑑1𝑑1 positive and ℎ1ℎ1 negative outcomes, and a control group prior of 𝐵(𝛼0,𝛽0)𝐵(𝛼0,𝛽0), observing 𝑑0𝑑0 positive and ℎ0ℎ0 negative outcomes. In this case, the posterior for the RR will be given by

𝑃(𝑅𝑅=𝑟)=∫𝑝/𝑞=𝑟𝑓𝐵(𝛼0,𝛽0)(𝑝)𝑓𝐵(𝛼1,𝛽1)(𝑞)𝑑𝑝𝑑𝑞𝑃(𝑅𝑅=𝑟)=∫𝑝/𝑞=𝑟𝑓𝐵(𝛼0,𝛽0)(𝑝)𝑓𝐵(𝛼1,𝛽1)(𝑞)𝑑𝑝𝑑𝑞

where 𝑓𝐵(𝛼,𝛽)𝑓𝐵(𝛼,𝛽) is the density of a beta distribution with parameters 𝛼𝛼 and 𝛽𝛽.

While this is challenging to evaluate algebraically, it can easily be estimated numerically, e.g., by Markov Chain Monte Carlo (MCMC) simulation. The two most natural choices for hyperparameters 𝛼𝛼 and 𝛽𝛽 are either 𝐵(1,1)𝐵(1,1), corresponding to the uniform distribution on (0,1)(0,1), or 𝐵(0.5,0.5)𝐵(0.5,0.5), which is the non-informative Jeffrey’s prior for the Bernoulli model (Approach III in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002) and [Table 3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003)).

Furthermore, one could consider priors with a point mass (an atom) at 0, hence with a non-zero prior probability of the proportion being precisely 0. We decided not to employ these priors, as the mass placed at 0 necessarily would be a subjective choice and would strongly influence the estimated CrIs.

#### 2.3.2. Bayesian Binomial Regression

A different approach is to assume a prior for the RR itself together with a prior for the proportion in the control (reference) group, and from these two, obtain a posterior for the RR. In this case, estimation by Bayesian binomial regression is the most relevant method to apply, as binomial regression generally is the preferred strategy to obtain RR estimates from regression models [[19](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B19-ijerph-18-05527)]. An important practical point in this approach is that the Bayesian estimation cannot be initialized by MLE, as we have described above, since the MLE does not exist in our case.

If it is desired to use weakly informative normal priors, it might be necessary to use smaller standard deviations than otherwise common to enable fitting of the model in these circumstances.

## 3. Results

Results for examples A, B, and C are given in [Table 2](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t002). When comparing the approaches of moving and adding one observation, respectively, we find that adding one observation generally results in narrower CIs than moving one, especially in Example A, which has the smallest sample size. As expected, the one-sided approaches result in lower upper bounds for the CI.

Comparing the approaches regarding the ORs, all CIs will automatically have zero as their lower bound. The approximate Cornfield interval generally obtains the lowest upper bound, especially for small sample sizes, but as the approximate Cornfield interval is constructed by using a large sample asymptotic theory, this interval should be interpreted carefully in small samples [[15](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B15-ijerph-18-05527)]. Among the exact approaches for OR-based CIs, the midpoint Baptista–Pike method generally results in the narrower CI, while the exact Cornfield method results in the widest intervals. For moderate sample sizes, the OR-based approaches result mainly in narrower CIs than moving or adding one.

The Bayesian proportion-based approach results in CrIs of similar magnitude compared to the frequentist OR-based CIs, with highest posterior density (HPD) intervals being generally narrower than equal-tailed (EqT) CrIs. While these CrIs have a non-zero lower limit, this estimate is extremely close to zero in all examples. On the other hand, the Bayesian approach, based on binomial regression, results in much narrower CrIs than is the case for all the other methods investigated.

Results from examples D, E, and F corresponding to larger epidemiological cohort studies are presented in [Table 3](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#table_body_display_ijerph-18-05527-t003). In general, these results behave similarly to those obtained from the smaller examples. Furthermore, the proportion-based Bayesian approaches result in CrIs, which are similar in magnitude to the CIs obtained by frequentist approaches. On the other hand, the Bayesian binomial regression obtains extremely narrow CrIs with almost all mass concentrated close to zero.

## 4. Discussion

In this study, results showed that several different methods are feasible for obtaining CIs or CrIs even in studies with zero observed events in the intervention group. Overall, the different frequentist approaches result in comparable CIs as long as the sample size is moderate or large, and Bayesian methods are able to obtain CrI of similar magnitude, although Bayesian binomial regression generally results in very narrow CrIs concentrating much of the mass around zero. This phenomenon is caused by the parametrization implied by binomial regression, in which an RR of zero corresponds to a regression coefficient of −∞−∞, hence driving the posterior distribution of the coefficient downwards. Therefore, the results from Bayesian binomial regression should be interpreted cautiously and the proportion-based Bayesian approach should be considered the preferred method. Moreover, while Bayesian approaches have an explicit probabilistic interpretation, as a 95%95% CrI indicates an interval, which with 95%95% probability contains the true population parameter, conditional on the chosen prior distributions, Bayesian approaches are still not widespread in epidemiological literature [[20](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B20-ijerph-18-05527)], which limits dissemination of their results.

#### 4.1. Strengths and Limitations

The main strength of this study is that both the frequentist and the Bayesian approaches, commonly suggested in the literature, are compared in a set of examples representing many practical applications, thus enabling a direct comparison of the approaches and their results.

A weakness of this study is that it had to be limited to the most well-known approaches. Thus, we were not able to compare all the approaches suggested in the literature, such as the exact approaches to the CI [[21](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B21-ijerph-18-05527)] and exact Bayesian inference [[22](https://www.mdpi.com/1660-4601/18/11/5527?utm_source=substack&utm_medium=email#B22-ijerph-18-05527)]. Another limitation is that due to the observation of zero events laying at the border of the parameter space for all frequentist methods, no formal evaluation of coverage for the obtained CIs was feasible.

#### 4.2. Possible Future Research

This paper focused on the inference for unadjusted RRs, for instance, those typically estimated in randomized clinical trials. In observational studies, one would most often have a desire to adjust for possible confounders, which would not be easily achievable with most of the discussed methods. Hence, future research should investigate how inference for RR estimates with 0 events can be obtained in models with covariate adjustment.

Furthermore, problems as those seen in the case of an RR estimate of 0 can occur in time-to-event studies, in which no events are observed in the intervention group. Similarly to the RR, this challenges the inference obtainable from, for instance, the hazard ratio from a survival analysis. This issue should be investigated in future studies.

## 5. Conclusions

This investigation demonstrates that it is possible to obtain CIs and CrIs for the RR in studies with no observed events in the intervention group. Hence, researchers should also report CIs or CrIs in these circumstances and refrain from concluding that inference was impossible due to no observed events, as this often will result in understating the evidence obtainable from a study. On the other hand, researchers should be aware that the obtained intervals are sensitive to the method applied for smaller samples while quite robust in large samples.