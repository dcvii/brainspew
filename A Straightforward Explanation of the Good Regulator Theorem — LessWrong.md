---
title: "A Straightforward Explanation of the Good Regulator Theorem — LessWrong"
source: "https://www.lesswrong.com/posts/JQefBJDHG6Wgffw6T/a-straightforward-explanation-of-the-good-regulator-theorem"
author:
  - "[[Alfred Harwood]]"
published: 2024-11-18
created: 2025-06-14
description: "This post was written during the agent foundations fellowship with Alex Altair funded by the LTFF. Thanks to Alex, Jose, Daniel, Cole, and Einar for…"
tags:
  - "clippings"
---
*This post was written during the* [*agent foundations fellowship*](https://www.lesswrong.com/posts/WiMnhMXu9CM5ytu3t/work-with-me-on-agent-foundations-independent-fellowship) *with* [*Alex Altair*](https://www.lesswrong.com/users/alex_altair) *funded by the* [*LTFF*](https://funds.effectivealtruism.org/funds/far-future)*. Thanks to* [*Alex*](https://www.lesswrong.com/users/alex_altair)*,* [*Jose*](https://www.lesswrong.com/users/josefaustino)*,* [*Daniel*](https://www.lesswrong.com/users/daniel-c)*,* [*Cole*](https://www.lesswrong.com/users/cole-wyeth)*, and* [*Einar*](https://www.lesswrong.com/users/einar-urdshals) *for reading and commenting on a draft.*

The [Good Regulator Theorem](https://en.wikipedia.org/wiki/Good_regulator), as published by Conant and Ashby in their [1970 paper](http://pespmc1.vub.ac.be/books/Conant_Ashby.pdf) (cited over 1700 times!) claims to show that 'every good regulator of a system must be a model of that system', though it is a subject of debate as to whether this is actually what the paper shows. It is a fairly simple mathematical result which is worth knowing about for people who care about agent foundations and [selection theorems](https://www.lesswrong.com/posts/G2Lne2Fi7Qra5Lbuf/selection-theorems-a-program-for-understanding-agents). You might have heard about the Good Regulator Theorem in the context of John Wentworth's ['Gooder Regulator' theorem](https://www.lesswrong.com/posts/Dx9LoqsEh3gHNJMDk/fixing-the-good-regulator-theorem) and his other improvements on the result.

Unfortunately, the original 1970 paper is notoriously unfriendly to readers. It makes misleading claims, doesn't clearly state what exactly it shows and uses strange non-standard notation and cybernetics jargon ('coenetic variables' anyone?). If you want to understand the theorem without reading the paper, there are a few options. John Wentworth's [post](https://www.lesswrong.com/posts/Dx9LoqsEh3gHNJMDk/fixing-the-good-regulator-theorem) has a nice high-level summary but refers to the original paper for the proof. [John Baez's blogpost](https://johncarlosbaez.wordpress.com/2016/01/27/the-good-regulator-theorem/) is quite good but is very much written in the spirit of trying to work out what the paper is saying, rather than explaining it intuitively. I couldn't find an explanation in any control theory textbooks (admittedly my search was not exhaustive). A five year-old [stackexchange](https://mathoverflow.net/questions/327012/rigorous-proof-of-the-good-regulator-theorem) question, asking for a rigorous proof, goes unanswered. The best explainer I could find was Daniel L. Scholten's ['A Primer for Conant and Ashby's Good-Regulator Theorem'](http://cadia.ru.is/wiki/_media/public:t-720-atai:a_primer_for_conant_and_ashby_s_good-regulator_theorem.pdf) from the mysterious, now-defunct 'GoodRegulatorProject.org' ([link](http://web.archive.org/web/20180803204113/http://goodregulatorproject.org/) to archived website). This primer is nice, but really verbose (44 pages!). It is also aimed at approximately high-school (?) level, spending the first 15 pages explaining the concept of 'mappings' and conditional probability.

Partly to test my understanding of the theorem and partly to attempt to fill this gap in the market for a medium-length, entry-level explainer of the original Good Regulator Theorem, I decided to write this post.

Despite all the criticism, the actual result is pretty neat and the math is not complicated. If you have a very basic familiarity with Shannon entropy and conditional probability, you should be able to understand the Good Regulator Theorem.

This post will just discuss the original Good Regulator Theorem, not any of John Wentworth's additions. I'll also leave aside discussion of how to interpret the theorem (questions such as 'what counts as a model?' etc.) and just focus on what is (as far as I can tell) the main mathematical result in the paper.

Let's begin!

## The Setup

Conant and Ashby's paper studies a setup which can be visualised using the following causal Bayes net:

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/JQefBJDHG6Wgffw6T/qkatnzn7q8uka3gzdoa8)

If you are not familiar with Bayes nets you can just think of the arrows as meaning 'affects'. So means 'variable affects the outcome of variable '. This way of thinking isn't perfect or rigorous, but it does the job.

Just to be confusing, the paper discusses a couple of different setups and draws a few different diagrams, but you can ignore them. This is the setup they study and prove things about. This is the only setup we will use in this post.

The broad idea of a setup like this is that the outcome is affected by a system variable and a regulator variable . The system variable is random. The regulator variable might be random and independent of but most of the time we are interested in cases where it depends on the value of . By changing the way that depends on , the distribution over outcomes can be changed. As control theorists who wish to impose our will on the uncooperative universe, we are interested in the problem of 'how do we design a regulator which can steer towards an outcome we desire, in spite of the randomness introduced by ?'

The archetypal example for this is something like a thermostat. The variable represents random external temperature fluctuations. The regulator is the thermostat, which measures these fluctuations and takes an action (such as putting on heating or air conditioning) based on the information it takes in. The outcome is the resulting temperature of the room, which depends both on the action taken by the regulator, and the external temperature.

Each node in the Bayes net is a random variable. The 'system' is represented by a random variable , which can take values from the set . It takes these values with probabilities etc. Think of the system as an 'environment' which contains randomness.

The variable represents a 'regulator'- a random variable which can take values from the set . As the diagram above shows, the regulator can be affected by the system state and is therefore described by a conditional probability distribution . Conditional probabilities tell you what the probability of is, given that has taken a particular value. For example, the equation tells us that *if* takes the value , *then* the probability that takes the value is . When we discuss making a good regulator, we are primarily concerned with choosing the right conditional probability distribution which helps us achieve our goals (more on exactly what constitutes 'goals' in the next section). One important assumption made in the paper is that the regulator has perfect information about the system, so can 'see' exactly what value takes. This is one of the assumptions which is relaxed by John Wentworth, but since we are discussing the original proof, we will keep this assumption for now.

Finally, the variable represents the 'outcome' - a random variable which can take values from the set . The variable is entirely determined by the values of and so we can write it as a deterministic function of the regulator state and the system state. Following Conant and Ashby, we use to represent this function, allowing us to write . Note that it is possible to imagine cases where is related to and in a non-deterministic way but Conant and Ashby do not consider cases like this so we will ignore them here (this is another one of the extensions proved by John Wentworth - I hope to write about these at a later date!).

## What makes a regulator 'good'?

Conant and Ashby are interested in the question: 'what properties should have in order for a regulator to be good?' In particular, we are interested in what properties the conditional probability distribution should have, so that is effective at steering towards states that we want.

One way that a regulator can be good is if the Shannon entropy of the random variable is low. The Shannon entropy is given by

The Shannon entropy tells us how 'spread out' the distribution on is. A good regulator will make as small as possible, steering towards a low-uncertainty probability distribution. Often, in practice, a producing a low entropy outcome is not on its own sufficient for a regulator to be useful. Scholten gives the evocative example of a thermostat which steers the temperature of a room to 350°F with a probability close to certainty. The entropy of the final distribution over room temperatures would be very low, so in this sense the regulator is still 'good', even though the temperature it achieves is too high for it to be useful as a domestic thermostat. Going forward, we will use low outcome entropy as a criterion for a good regulator, but its better to think of this as a necessary and/or desirable condition rather than sufficient condition for a good regulator.

The second criterion for a good regulator, according to Conant and Ashby, is that the regulator is not 'unnecessarily complex'. What they mean by this is that if two regulators achieve the same output entropy, but one of the regulators uses a policy involving some randomness and the other policy is deterministic, the policy that uses randomness is unnecessarily complex, so is less 'good' than the deterministic policy.

For example, imagine we have a setup where . Then, when the regulator is presented with system state , it could choose from between the following policies:

- Pick with probability 1 whenever . So and
- Pick with probability 1 whenever . So and
- Toss a coin an pick if it lands heads and pick if it lands tails. So and .

All three of these policies achieve the same result (the outcome will always be whenever ), and the same output entropy, but the third option is 'unnecessarily complex', so is not a good regulator. Argue amongst yourselves about whether you find this criterion convincing. Nonetheless, it is the criterion Conant and Ashby use, so we will use it as well.

To recap: a good regulator is one which satisfies the following criteria:

1. It minimizes the entropy of the outcome variable .
2. It is not unnecessarily complex, in the sense described above.

## The Theorem Statement

The theorem statement can be written as follows:

**If a regulator is 'good' (in the sense described by the two criteria in the previous section), then the variable R can be described as a deterministic function of S.**

Another way of saying that ' can be described as a deterministic function of ' is to say that for every and , then either equals 0 or 1. This means that can be written as for some mapping .

We are now almost ready the prove the theorem. But first, it is worth introducing a basic concept about entropy, from which the rest of the Good Regulator Theorem flows straightforwardly.

## Concavity of Entropy

Conant and Ashby write:

> One of the useful and fundamental properties of the entropy function is that any such increase in imbalance in necessarily decreases .

This is probably pretty intuitive if you are familiar with Shannon Entropy. Here is what it means. Suppose we have a probability distribution which assigns probabilities and for two different outcomes with (and other probabilities to other -values). Now suppose we increase the probability of outcome (which was already as likely or more likely than ) and decrease the same amount while keeping the rest of the distribution the same. The resulting distribution will end up with a lower entropy than the original distribution. If you are happy with this claim you can skip the rest of this section and move on to the next section. If you are unsure, this section will provide a little more clarification of this idea.

One way to prove this property is to explicitly calculate the entropy of a general distribution where one of the probabilities is and another is (where and ). Then, you can differentiate the expression for entropy with respect to and show that ie. is a decreasing function of . This is fine and do-able if you don't mind doing a little calculus. Scholten has a nice walk-through of this approach in the section of his primer titled 'A Useful and Fundamental Property of the Entropy Function'.

Here is another way to think about it. Consider a random variable with only two outcomes and . Outcome occurs with probability and occurs with probability The entropy of this variable is

This is a [concave function](https://en.wikipedia.org/wiki/Concave_function) of . When plotted (using base 2 logarithms) it looks like this:

![](https://res.cloudinary.com/lesswrong-2-0/image/upload/f_auto,q_auto/v1/mirroredImages/JQefBJDHG6Wgffw6T/uv3bbbn1dftzjcrkcols)

If , decreasing decreases the entropy and if , increasing decreases the entropy. So 'increasing the imbalance' of a 2-outcome probability distribution will always decrease entropy. Is this still true if we increase the imbalance between two outcomes within a larger probabilities distribution with more outcomes? The answer is yes.

Suppose our outcomes and are situated within a larger probability distribution. We can view this larger probability distribution as a mixture of our 2-outcome variable and another variable which we can call which captures all other outcomes. We can write (which we can think of as the 'total' random variable) as

With probability , the variable takes a value determined by and with probability , the value of is determined by random variable .

It turns out the entropy of such variable, generated by mixing non-overlapping random variables, can be expressed as follows:

where is the [binary entropy](https://en.wikipedia.org/wiki/Binary_entropy_function) (see eg. [this Stackexchange answer](https://math.stackexchange.com/questions/4271669/proving-the-decomposibility-of-entropy/4273155#4273155) for a derivation). Increasing the relative 'imbalance' of and ) while keeping their sum constant does not change or but does reduce , thus reducing the total entropy .

This is a fairly basic property of entropy but understanding it is one of the only conceptual pre-requisites for understanding the good regulator theorem. Hopefully it is clear now if it wasn't before.

On to the main event!

## The Main Lemma

Conant and Ashby's proof consists of one lemma and one theorem. In this section we will discuss the lemma. I'm going to state the lemma in a way that makes sense to me and is (I'm pretty sure) equivalent to the lemma in the paper.

**Lemma:**

**Suppose a regulator is 'good' in the sense that it leads to Z having the lowest possible entropy. Then P(R|S) must have been chosen so that Z is a deterministic function of S ie. H(Z|S)=0.**

Here is an alternative phrasing, closer to what Conant and Ashby write:

Suppose a regulator is 'good' in the sense that it leads to having the lowest possible entropy. Suppose also that, for a system state , this regulator has a non-zero probability of producing states and , ie. and . Then, it must be the case that , otherwise, the regulator would not be producing the lowest possible output entropy.

Here is *another* alternative phrasing:

Suppose a regulator is 'good' in the sense that it leads to having the lowest possible entropy. If, for a given system state, multiple regulator states have non-zero probability, then all of these regulator states lead to the same output state when combined with that system state through . If this was not the case, we could find another regulator which lead to having a lower entropy.

This is one of those claims which is kind of awkward to state in words but is pretty intuitive once you understand what it's getting at.

Imagine there is a regulator which, when presented with a system state , produces state with probability and produces state with probability . Furthermore, suppose that is such that and . This means that, when presented with system state , the regulator sometimes acts such that it produces an outcome state and other times acts so as to produce an outcome state . This means is not a deterministic function of . Is it possible that this regulator produces the lowest possible output entropy? From considering the previous section, you might already be able to see that the answer is no, but I'll spell it out a bit more.

The total probability that will be given by the sum of the probability that , when is not and the probability that is when equals :

Similarly the probably that is given by:

Suppose , then, as we saw in the previous section, we can reduce the entropy of by increasing and decreasing by the same amount. This can be achieved by changing the regulator so that is increased and is decreased by the same amount. Therefore, a regulator which with nonzero probability produces two different values when presented with the same -value cannot be optimal if those two -values lead to different -values. We can always find a regulator which consistently picks 100% of the time which leads to a lower output entropy. (A symmetric argument can be made if we instead assume .)

However, if was such that , then it would not matter whether the regulator picked or or tossed a coin to decide between them when presented with , because both choices would lead to the same -value. In such a case, even though contains randomness, the overall effect would be that is still a deterministic function of .

## The Theorem

90% of the meat of the theorem is contained in the above lemma, we just need to tie up a couple of loose ends. To recap: we have showed that a regulator which achieves the lowest possible output entropy must use a conditional distribution which leads to being a deterministic function of . For each system state , the regulator must only choose -values which lead to a single -value. This still leaves open the possibility that the regulator can pick a random -value from some set of candidates, provided that all of those candidates result in the same -value. In our example from the previous section, this would mean that the regulator could toss a coin to choose between and when presented with system state and this regulator could still achieve the minimum possible entropy.

This is where the 'unnecessary complexity' requirement comes in. Conant and Ashby argue that one of the requirements for a 'good' regulator is that it does not contain any unnecessary complexity. A regulator which randomises its value would be considered unnecessarily complex compared to a regulator which produced the same output state distribution without using randomness. Therefore, for a regulator to be 'good' in the Conant and Ashby sense, it can only pick a single -value with 100% probability when presented with each -value. And the main lemma tells us that this condition does not prevent us from minimizing the output entropy.

This means that in the conditional probability distribution , for each -value, the probability of any one -value is either zero or one. To put it another way, can be described as a deterministic function of . In a good regulator, knowing allows you to predict exactly what value will take. Also, since is a deterministic function of and , this means that , when being regulated by a good regulator, will be a deterministic function of .

Thus, we have proved that a good regulator must be a deterministic function of the system state .

Note that the argument makes no assumptions about the probability distribution over . Though changing the probability distribution over will change the final output entropy, it will not change the properties of a good regulator.

## Example

Consider the following example, where , , and have three possible states and the 'dynamics' function is characterised by the following table:

|  |  |  |  |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

First, consider a regulator which violates the main condition of the main lemma, by randomizing between and when presented with , even though they lead to different -values. Here is the conditional probability table for such a regulator:

|  |  |  |  |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

If has a maximum entropy distribution so , then this regulator will produce outcome with probability . Outcome will have probability and outcome will have . This output distribution will therefore have entropy

(using base 2 logarithms). According to the lemma, we can achieve a better (lower) output entropy by ensuring that is such that the regulator chooses whichever -value corresponds to the -value which already has a higher probability. In this case, has a higher probability than , so 'increasing the imbalance' means increasing the probability of , at the expense of as much as we can. This can be done by increasing to 1 and decreasing to zero (while keeping the rest of the distribution the same).

This results in a -distribution with an entropy of zero, since, regardless of the -value, always ends up in state . Since this entropy cannot be improved upon and the regulator does not have any unnecessary noise/complexity, the Good Regulator Theorem predicts that this regulator should be a deterministic function of . Lo and behold, it is! Each -value gets mapped to exactly one -value:

|  |  |  |  |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

Consider another regulator for the same system, as characterised by the following conditional probability table:

|  |  |  |  |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

Referring back to the table for , we can see that this regulator also achieves an output entropy of zero, even though it randomizes between and when presented with . Since , this isn't a problem from the point of view of minimizing entropy, but it is 'unnecessarily complex', so doesn't meet the criteria of a good regulator as Conant and Ashby define it. There are two ways to make this regulator 'good'. We could either make and , making the regulator the same as our previous example, or we could set and .

Both possibilities would be 'good regulators' in the sense that they achieve the minimum possible entropy and are not unnecessarily complex. They are also both regulators where is a deterministic function of , validating the prediction of the theorem.

## Conclusion

One thing that Conant and Ashby claim about this theorem is that it shows that a good regulator must be 'modelling' the system. This is a bit misleading. As I hope I have shown, the Good Regulator Theorem shows that a good regulator (for a certain definition of 'good') must depend on the system in a particular way. But the way in which a good regulator must depend on the system does not correspond to what we might normally think of as a 'model'. The regulator must have a policy where its state deterministically depends on the system state. That's it! If we were being very generous, we might want to say something like: 'this is a necessary but not sufficient condition for a regulator that does model its environment (when the word model is use in a more normal sense)'. When Conant and Ashby say that a good regulator 'is a model of the system', they might mean that looking at tells you information about and in that sense, is a model of . When is a deterministic function of , this is sometimes true (for example when is a bijective or injective function of ). However, in some setups, the 'good' regulator might be a deterministic function of which takes the same value, regardless of the value of . I don't think its sensible to interpret such a regulator as being a model of .

Personally, I don't think that it is useful to think about the Good Regulator Theorem as a result about models. It's a pretty neat theorem about random variables and entropy (and that's ok!), but on its own, it doesn't say much about models. As with most things in this post, John Wentworth has [discussed](https://www.lesswrong.com/posts/Dx9LoqsEh3gHNJMDk/fixing-the-good-regulator-theorem) how you could modify the theorem to say something about models.

After writing this piece, the good regulator theorem is a lot clearer to me. I hope it is clearer to you as well. Notable by its absence in this post is any discussion of John Wentworth's improvements to the theorem. Time permitting, I hope to cover these at a later date.