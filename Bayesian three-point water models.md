---
title: "Bayesian three-point water models"
source: "https://journalclub.io/episodes/bayesian-three-point-water-models"
author:
published:
created: 2026-01-12
description:
tags:
  - "clippings"
---
---

In computational modeling, a surprising number of problems revolve around the same thing: water. Are you simulating how proteins fold? If so, you'll need a good model for water. Modeling how drug molecules bind? Start with water. Calculating how materials interact with biological systems? Well, those living systems are probably made largely of water.

Given its ubiquity you might assume that we'd have sophisticated nuanced representations of water. Ones that can accommodate the subtlety and complexity of the hydrogen-bonding network. But you'd be wrong. After decades of work on this problem, we're still using remarkably simplistic representations, and we know that they don't get everything right.

But just how bad are they? Just how much information are they missing? In this paper, the authors are trying to figure that out. They're not trying to create the perfect water model, they're just trying to understand the limits of the existing ones. On today's episode, we'll walk through their analysis. We'll talk about how synthetic likelihood inference works, how the posterior landscape (in this case) changes depending on which experimental properties you use, how the authors quantified different sources of error, and what the results tell us. Let's dive in.

First, let's talk more about why this problem matters and what makes it so tricky.

Three-point water models like TIP3P have been around since the 1980s. They represent each water molecule with three points, and I'm sure you can guess what those are. One oxygen atom and two hydrogen atoms. The oxygen has a negative charge, the hydrogens have positive charges. The interactions between molecules follow the Lennard-Jones potential for Van der Waals forces plus Coulomb interactions for electrostatics. That's it. No polarization, no flexibility in the molecular geometry, no quantum effects. Just three rigid points in space.

This simplicity is a feature, not a bug. These models are computationally cheap, which matters when you're simulating millions of molecules. And they're compatible with most existing biomolecular force fields, which means you don't have to rebuild your entire simulation stack to use them. The problem is that they struggle to reproduce multiple experimental properties at once. You can tune the parameters to match density and enthalpy of vaporization pretty well, but then the diffusion coefficient might be way off. Or it's the dielectric constant. Or the hydrogen bonding patterns.

Traditional approaches to force field parameterization typically involve picking a handful of target properties, running simulations across a parameter grid, and selecting the set that best matches the experiment. But this approach has a few problems.

- First, it gives you a single point estimate with no sense of uncertainty.
- Second, it doesn't tell you whether the mismatch with the experiment is because you chose bad parameters or because the model itself is fundamentally limited.
- Third, it doesn't generalize well. Parameters optimized at one temperature might fail at another.

The authors wanted to do better. Instead of finding one optimal parameter set, they wanted to find the entire posterior distribution over plausible parameters. This tells you not just which parameters are likely, but also how much uncertainty exists and how parameters correlate with each other. It also lets you quantify how much of the prediction error comes from parameter uncertainty versus model limitations.

So what did they do differently?

Well, they used synthetic-likelihood Bayesian inference combined with Metropolis-Hastings sampling. Let's break down how this works. The basic idea is that you want to compute the posterior distribution of parameters given experimental data using Bayes' theorem. The posterior is proportional to the likelihood times the prior. The prior encodes what you knew about the parameters before seeing any data. In this case, parameter proposals were defined in log-transformed space to enforce positivity, which induces a non-uniform prior in the original parameter space even though no specific parameter values were explicitly favored.

Ideally, you'd want to compute the probability of observing your experimental data given a particular parameter set. But molecular dynamics simulations are stochastic. If you run the same simulation twice with the same parameters but different initial conditions, you'll get slightly different results. This means you can't directly compute a likelihood from a single simulation. You need to characterize the distribution of possible outcomes. The synthetic likelihood approach solves this by assuming that the observable quantities from your simulations follow a multivariate normal distribution. For any given parameter set, you run long simulations and estimate the mean and covariance of the observables using block averaging over the trajectory. Then you construct a Gaussian likelihood function using those estimated statistics. This likelihood approximates the true likelihood, and it's computationally tractable because you only need to estimate means and covariances rather than the full distribution.

The assumption of normality is important here. For molecular dynamics simulations, observable quantities averaged over long trajectories typically do converge to normal distributions. That is: the longer you run your simulation and the more you average, the more the distribution of your observables looks like a bell curve.

Once you have the likelihood, you can explore the posterior using Metropolis-Hastings sampling. This is an MCMC algorithm that generates samples from the posterior distribution. At each iteration, you propose a new parameter set by perturbing the current one. You run simulations with the new parameters, compute the synthetic likelihood, and decide whether to accept or reject the proposal based on the likelihood ratio and a random draw. Over many iterations, this generates a chain of samples that, after discarding an initial burn-in period, represent draws from the true posterior.

They first mapped the posterior structure by scanning a two-dimensional grid of oxygen with the charge fixed, showing that different observable subsets induce qualitatively different parameter landscapes. Enthalpy of vaporization and molecular volume alone favored epsilon values far above TIP3P and produced a posterior with a correlation that flips sign across parameter space, while RDF-based observables enforced a consistently negative epsilon-sigma correlation tied to solvation-shell geometry, and hydrogen-bond metrics pushed sigma even lower. When all six observables were combined, the posterior collapsed, penalizing high-epsilon solutions and revealing that no single parameter choice could satisfy all constraints simultaneously. Extending to three dimensions by sampling epsilon, sigma, and charge with Metropolis-Hastings confirmed the tradeoffs. Charge correlated positively with epsilon and negatively with sigma, and the posterior mean stayed near TIP3P. This indicates that TIP3P sits in a reasonable but non-optimal compromise region of parameter space.

Uncertainty analysis showed that for fitted observables, parameter uncertainty dominated prediction error, while simulation noise was negligible, but for unfitted properties like dielectric constant, diffusion, and heat capacity, large systematic biases exposed the kind of model inadequacy that tuning can't fix.

Allowing charge variation did not materially reduce bias, especially for hydrogen bonding, implying that fixed molecular geometry severely limits what charge reparameterization can achieve. To efficiently propagate uncertainty to expensive observables, they validated the unscented transform as an accurate surrogate for full posterior sampling, achieving close agreement with MCMC using only a handful of simulations.

Comparing parameter sets, their posterior mode improved several key properties over TIP3P but slightly degraded others. This reinforces the idea that three-point models encode unavoidable tradeoffs. More flexible models like OPC3 perform better by adding geometric degrees of freedom, but even these cannot overcome the structural limits of the model class. All of this underscores the paper's core takeaway: that Bayesian inference exposes not just better parameters, but where parameter optimization ends and model inadequacy begins.

The authors point out that their framework doesn't just optimize parameters: it reveals where the model class itself is inadequate. The large systematic biases in properties like dielectric constant and diffusion coefficient can't be blamed on parameter choices. They're inherent to the three-point rigid non-polarizable framework. That insight is exactly what Bayesian approaches are good for: separating parameter uncertainty from model inadequacy.

If you want to pore over the synthetic likelihood construction, the validation tests, the Metropolis-Hastings acceptance criteria, the transform sigma point calculations, or the complete simulation protocols, I'd recommend downloading the paper.