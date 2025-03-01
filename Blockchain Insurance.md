---
title: Blockchain Insurance
source: https://www.cubegeek.com/2017/07/blockchain-insurance.html
author:
  - "[[Cubegeek]]"
published: 07/18/2017
created: 2025-02-19
description: It turns out that Vinay Gupta is smarter than I thought he was, which is pretty goddamned smart. He points out something that excites me in a way I haven't been in a while. So let me tell you a...
tags:
  - clippings
---
It turns out that Vinay Gupta is smarter than I thought he was, which is pretty goddamned smart. He points out something that excites me in a way I haven't been in a while. So let me tell you a little story.

Once upon a time in Atlanta when Essbase was young, I had a sit down with some actuaries at a company of extraordinary repute. They wanted me to get some of their data into Essbase so they could refine their model. It turned out that they needed 11 dimensions. We could not provide. Oh snap. I always wanted to work with actuaries and there went my chance. My old college roommate did actuarial work, and I can recall being fascinated by the story (was it Gladwell who told it?) of the invention of insurance from the minds and records of some priests in Edinburgh. 

I have another insurance story or three but that's for another time. I only mention this story to help you understand how exciting it is to know that some of the stuff I've always wanted to do I may do in the future. Death panels! Gupta makes the following observation in his talk about identity provision in the future world of 'perfected security'. 

> Insurers are already people that know a ton about you. They know what you’re worth, they know anything special that you own, they know where you live, and they’ve often got these data sets for years and years and years. Most people probably haven’t thought about their insurer in years: they send you a bill, you pay the bill, and it goes on. There could be somebody in this room with a 15–20-year relationship with their insurer, and you’ve almost certainly thought about it less than you think about your bank. The insurers are probably in a position where a lot of people already trust them, they’re in a position where they’re relatively good at keeping secrets, they’re in a position where they don’t really talk very much to other institutions, which is quite nice, because it means they don’t have a bunch of unfair advantage to draw from insider knowledge. They’ve got a bunch of really good attributes for doing the kind of stuff that we want them to do.

Brilliant. I've been thinking about the problem of real world validation of blockchain information. I might have eventually stumbled onto this idea, but I'm glad I heard [Vinay's presentation](https://medium.com/humanizing-the-singularity/a-blockchain-solution-for-identity-51fbcae94caa), because I've been thinking certain things about identity that almost made sense. For example, in my book 'Borky's Beach', I have this global entity called 'The Wizards' and they are a consortium of marketing boffins who have perfected their craft. Based upon my own personal experience with a certain credit card company in Arkansas, I know that companies with enough data can impute a great deal of information by eyeballing patterns. After all, they explained to me that they kept track of about 12 genders, all given various certainties based on imputations vs explicitly validated data. But I didn't think about the fact that insurance companies would also have fat data stacks that could more definitively resolve questions of identity. 

So now I'm thinking about various new kinds of insurance and the newer AIs and models that will keep their scrying digital eyes on our metadata for all kinds of things. While I'm on this slight tangent, I'd like to bring up the notion of 'continuous transaction states'. They are not continuous but rather they are formally discrete but with a great deal more granularity than what all sorts of transactions have heretofore been. Part of this is '[Triple Entry Accounting](https://www.evernote.com/l/AAYhxe0eYZZHT7KlKtiBBJ8SCUo2MBU6X_k)', but that's not the whole of it. So this paragraph also serves as a placeholder for that idea of tracking an interim set of states before a transaction is fully executed and verified by all parties. And that alludes to an answer I gave today:

Q. How can businesses accept Bitcoin if it takes hours or days to process a transaction?

> A.  There is at least one search engine that is available that will poll the top mining pools for the existence of a transaction being worked on in the current block. Using historical data, a service can predict based on the number of miners working on the transaction, how likely that transaction is to be contained within the next mined block. When that likelihood reaches a certain threshold, but before it’s actually confirmed, this service can make a guarantee and the seller can approve the sale.
>
> Basically it is a short-term insurance policy which could be paid for by the seller to the service provider, the downside risk is held by the service provider.
>
> This is different from counterparty risk, it is basically a bet that the entire bitcoin system will inevitably accept the transaction. There may be some double-spend risk, but no more than that of the entire bitcoin system.

"I attest."  is the key word. Such an attestation will bridge the gap between the impossibility of perfect information and those digital systems which are subject to human error.