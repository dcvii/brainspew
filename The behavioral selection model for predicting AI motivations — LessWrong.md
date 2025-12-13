---
title: "The behavioral selection model for predicting AI motivations — LessWrong"
source: "https://www.lesswrong.com/posts/FeaJcWkC6fuRAMsfp/the-behavioral-selection-model-for-predicting-ai-motivations-1"
author:
  - "[[Alex Mallen]]"
published: 2025-12-04
created: 2025-12-11
description: "Highly capable AI systems might end up deciding the future. Understanding what will drive those decisions is therefore one of the most important ques…"
tags:
  - "clippings"
---
![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/FeaJcWkC6fuRAMsfp/hv67tflwzwxwspxlgf44)

Illustrative depiction of different cognitive patterns encoded in the weights changing in influence via selection.

x

[^1]: In this post, I’ll use “AI” to mean a set of model weights.

[^2]: You can try to define the “influence of a cognitive pattern” precisely in the context of particular ML systems. One approach is to define a cognitive pattern by what you would do to a model to remove it (e.g. setting some weights to zero, or ablating a direction in activation space; note that these approaches don't clearly correspond to something meaningful, they should be considered as illustrative examples). Then that cognitive pattern’s influence could be defined as the divergence (e.g., KL) between intervened and default action probabilities. E.g.: Influence(intervention; context) = KL(intervention(model)(context) || model(context)). Then to say that a cognitive pattern gains influence would mean that ablating that cognitive pattern now has a larger effect (in terms of KL) on the model’s actions.

[^3]: This requires modeling beliefs, and it can be ambiguous to distinguish this from motivations. One approach is to model AI beliefs as a causal graph that the AI it uses to determine which actions would produce higher X. You could also use a more general model of beliefs. To the extent the AI is capable and situationally aware, then it's a reasonable approximation to just use the same causal model for the AI's beliefs as you use to predict the consequences of the AI's actions.

[^4]: Motivations can vary in how hard they optimize for X. Some might try to maximize X, while others merely tend to choose actions that lead to higher-than-typical X across a wide variety of circumstances.

[^5]: In fact, this definition of a motivation is expressive enough to model arbitrary AI behavior. For any AI that maps contexts to actions, we can model it as a collection of context-dependent X-seekers, where X is the action the AI in fact outputs in that context. (This is similar to how [any agent](https://www.lesswrong.com/posts/NxF5G6CJiof6cemTw/coherence-arguments-do-not-entail-goal-directed-behavior) can be described as a utility maximizer with a utility function of 1 for the exact action trajectory it takes and 0 otherwise.) I think this expressivity is actually helpful in that it lets us model goal-directed and non-goal-directed cognitive patterns in the same framework, as we’ll see in the section on kludges.

[^6]: By “deployment”, I mean the times in which the AI is generally empowered to do useful things, internal and external to the AI lab. When the AI is empowered to do useful things is likely also when it carries the most risk. But you could substitute out “deployment” for any time at which you want to predict the AI’s motivations.

[^7]: In particular, this assumes an idealized policy-gradient reinforcement learning setup where having influence through deployment can be explained by reward alone. In practice, other selection pressures likely shape AI motivations— [cognitive patterns might propagate](https://www.lesswrong.com/posts/qjCk73Hu4wv9ocmRF/the-case-for-countermeasures-to-memetic-spread-of-misaligned) through persistent memory banks or shared context in a process akin to human cultural evolution, there might be quirks in RL algorithms, and developers might iterate against held out signals about their AI, like their impression of how useful the AI is when they work with it. You could modify the causal graph to include whatever other selection pressures and proceed with the analysis in this post.

[^8]: How does “I get higher reward on this training episode” cause “I have influence through deployment”? This happens because RL can identify when the cognitive pattern was responsible for the higher reward. The RL algorithm reinforces actions proportional to reward on the episode, which in turn increases the influence (via SGD) of the cognitive patterns within the AI that voted for those actions (this is true in simple policy-gradient RL; in more standard policy-gradient implementations there’s more complexity that doesn’t change the picture).

[^9]: These motivations are the “blood relatives” of “influence through deployment”.

[^10]: Unless X is a (combination of) actions.

[^11]: When you define a motivation’s fitness this way you have to be careful about exactly what you mean by the correlation between it and selection. Most importantly, the correlation must be *robust to the AI’s optimization*, such that intervening on (causes of) the motivation actually improves selection. Also note that I’m using correlation loosely, not in the strict statistical sense of linear correlation. Though we can define the fitness of a motivation as the linear correlation between that variable and reward (with caveats about the distribution over which to compute the correlation) in the (current) case where all of selection happens via idealized reinforcement learning.

[^12]: One general approach to approximately predicting generalization behavior is: drawing a new causal graph depicting the AI’s beliefs about the new situation (which can often reasonably be assumed fairly accurate), and inferring what the AI might be motivated to do to achieve its terminal motivation(s) in the new causal graph.

[^13]: More precisely, the “reward” variable *screens off* the “influence in deployment” variable from the AI’s actions.

[^14]: When I say that something is causally “close” to selection, I mean that it explains a lot of the variance in selection via a mechanism that doesn't involve many nodes.

[^15]: People often express confusion about how reward-seekers will behave in deployment. Supposing the AI solely seeks “reward on the episode”, what does it do when “reward on the episode” doesn’t appear in its model of the world? I think there is genuine ambiguity about how reward-seekers (and fitness-seekers more broadly) behave in deployment, but we can make some predictions.

For one, developers will quite plausibly train fitness-seekers throughout deployment (“online training”). In this case, there is no ambiguity about what it means to pursue most fitness-seeking motivations. But even absent online training, fitness-seekers seem reasonably likely to follow local selection pressures. For example: A reward-seeker seems likely to [condition on the possibility that it is in training](https://www.lesswrong.com/posts/FuGfR3jL3sw6r8kB4/richard-ngo-s-shortform?commentId=GYuWN7jHYsfhDCGNK); An influence-in-deployment-seeker seems likely to condition on the possibility of training too, or else ensure its behavior looks desirable enough to remain deployed; Slightly further-causally-upstream proxies like “code passes test cases” are likely to generalize straightforwardly to deployment too.

[^16]: One case is what I call the “wireheader,” which cares about *activation patterns correlated with* causes of deployment influence. This is neither a cause nor a consequence of selection. Instead, the wireheader’s internal proxies were tied to selection by training (analogous to the role of valenced emotions like happiness in humans), so it therefore behaves similarly to fitness-seekers overall, but has some different behaviors (e.g. it would choose to enter  [the experience machine](https://en.wikipedia.org/wiki/Experience_machine)).  
Another case is [instrumentally-convergent](https://en.wikipedia.org/wiki/Instrumental_convergence) [goals](https://ai-2027.com/research/ai-goals-forecast), like power-seeking. The causal graph clarifies a distinction between two kinds of instrumentally-convergent goals: ones that are causally downstream of selection (e.g., “long-term power”) and ones that are causally upstream of selection (e.g., you could imagine a “gather resources in coding environments” node which eventually causes reward). Instrumentally convergent goals that are causally  *upstream* of selection aren’t maximally fit on their own—they need to be combined with some other motivations.

[^17]: In theory, developers could intend for the AI to seek a consequence of selection (e.g., making sure the AI’s deployment behavior is desirable), which could make intended motivations maximally fit for the same reasons as a schemer.

[^18]: Which, to be clear, it isn’t exactly: some “implicit priors” eventually drown out with greater behavioral selection (e.g., pretraining priors) while others don’t (e.g., “the instrumental becomes the terminal”).

[^19]: Other notions of simplicity are discussed in Carlsmith.

[^20]: I list some more (still not exhaustive) possibilities for held-out oversight signals here: Developers might honeypot models and use [alignment auditing agents](https://alignment.anthropic.com/2025/automated-auditing/); they might look at [chains of thought](https://arxiv.org/abs/2507.11473); they might use monitors in production usage; they might improve the quality of their oversight during the course of training, so that they are able to notice new reward-hacks as training goes on; they might be able to make inferences based on training dynamics or by extrapolating from smaller-scale experiments; they might use “honest tests”, which I’ll mention later.

[^21]: I also think it’s quite plausible that selection pressures produce powerful AIs that nonetheless have out-of-touch models of the consequences of their actions. E.g., when an aligned AI gets a suboptimal reward for not hardcoding an answer to an erroneous test case, SGD might *not* update it to want to hardcode answers to test cases, but instead to believe that hardcoding answers to test cases is what the developers wanted. These two hypotheses make different predictions about generalization behavior, e.g., in cases where developers convince the AI that they don’t want hardcoded outputs.

[^22]: People often express confusion about how reward-seekers will behave in deployment. Supposing the AI solely seeks “reward on the episode”, what does it do when “reward on the episode” doesn’t appear in its model of the world? I think there is genuine ambiguity about how reward-seekers (and fitness-seekers more broadly) behave in deployment, but we can make some predictions.

[^23]: One case is what I call the “wireheader,” which cares about *activation patterns correlated with* causes of deployment influence. This is neither a cause nor a consequence of selection. Instead, the wireheader’s internal proxies were tied to selection by training (analogous to the role of valenced emotions like happiness in humans), so it therefore behaves similarly to other fitness-seekers overall, but has some different behaviors (e.g. it would choose to enter [the experience machine](https://en.wikipedia.org/wiki/Experience_machine)).