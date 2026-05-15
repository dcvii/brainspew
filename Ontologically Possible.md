---
title: "Post by @jessi_cata on X"
source: "https://x.com/jessi_cata/status/2055117156300603730"
author:
  - "[[@jessi_cata]]"
published: 2026-05-13
created: 2026-05-15
description: "OP infers \"metaphysically possible\" from \"logically consistent\". In this case we don't need modal logic to interpret the argument. We could"
tags:
  - "brain_spew"
---
OP infers "metaphysically possible" from "logically consistent". In this case we don't need modal logic to interpret the argument. We could instead use first-order model theory as giving the set of possible worlds, and translate "metaphysically possible" to "logically possible".

Let T be the background first-order theory, whose set of models are the logically conceivable worlds. Assume T has recursively enumerable axioms, and is an extension of Peano Arithmetic (PA).

The ontological argument uses a "maximal greatness" predicate. The main relevant property is that anything that is "maximally great" is real.

To avoid getting confused between first-order existence and philosophical existence, treat "Real" as a predicate which means something exists in reality. Let "MaxGreat" be some predicate which provably implies Real: T proves "for all x, if MaxGreat(x), then Real(x)".

The main assumption of the ontological argument is that a maximally great entity is logically conceivable. Here we formalize this with model theory: there is some model of T in which "there exists x, MaxGreat(x)". By Godel's completeness theorem, this is equivalent to: T does not prove "there does not exists x, MaxGreat(x)".

There is no obvious way to prove, from here, that "there exists x, MaxGreat(x)". Indeed, it is possible to imagine theories T and definitions of MaxGreat and Real, for which T does not prove "there does not exist x, MaxGreat(x)", and yet, T neither proves "there exists x, MaxGreat(x)".

So it looks like the ontological argument doesn't work in provability logic. It might work in modal logic, but that would distinguish metaphysical possibility from logical possibility, questioning the inference from conceivability of a maximally great being to metaphysical possibility.

I do, however, want to discuss inferences from existence to necessary existence in provability logic, because these are sometimes possible.

Let a natural number be NEven if it is even, and also PA proves it is NEven. (A convenient property of natural numbers, unlike maximally great beings, is that they can be written literally into PA sentences, like "S(S(S(0)))" for 3. So when I say "PA proves n is NEven" I mean PA proves "NEven(S(S(...(0)))".)

If a NEven number exists, then PA proves it is NEven. Therefore, by Godel's completeness theorem, this number is NEven in all models of PA.

Does a NEven number exist? Yes, 0 is NEven by Lob's theorem. PA proves that, if PA proves 0 is NEven, then 0 is NEven. Therefore, by Lob's theorem, PA proves that 0 is NEven.

Let us contrastively consider a predicate CounterFermat of natural numbers, true of n when n encodes a quadruple of numbers which is a counterexample to Fermat's last theorem. We can, as before, define a predicate NCounterFermat to be true of a number when it is CounterFermat, and also PA proves it is NCounterFermat. As before, by Godel's completeness theorem, if a number is NCounterFermat, then it is NCounterFermat in all models of PA.

Of course, we have reason to believe that no CounterFermat, and therefore no NCounterFermat, numbers exist. The point of this exercise is to show that there are non-trivial predicates whose satisfaction by some number implies their satisfaction by that number in all models of PA. This has some of the flavor of the ontological argument, but is not sufficient to reconstruct it.

To summarize, if generally allowing inferences from "logically consistent" to "metaphysically possible", then first-order model theory and provability logic are more appropriate tools than modal logic; but the ontological argument fails when formulated in these terms. Modal logics will distinguish logical consistency from metaphysical possibility, and thereby permit only restricted inferences from consistency to possibility.

> **An Undistinguished Professor @2Philosophical\_** · 2026-05-13
> 
> An Ontological Argument
> 
> 1\. If the idea of God is internally consistent, then God is metaphysically possible.
> 
> 2\. If God is metaphysically possible, then God exists.
> 
> 3\. The idea of God is internally consistent.
> 
> So,
> 
> 4\. God exists.
> 
> ![Image](https://pbs.twimg.com/media/HIOaC3-WoAEoXAA?format=jpg&name=large)

---

## Comments

> **Arthur Wakefield @JerichoLeylines** · [2026-05-15](https://x.com/JerichoLeylines/status/2055313472057905167)
> 
> Pretty clever, kid. Here's a general version:
> 
> Let T be the proposition "X is exactly empty"
> 
> Let all facts about X be indexed by X.
> 
> Therefore, if T is true then X is not exactly empty. It contains the truth value of T, which is real-valued in any model that admits truth
> 
> > **jessicat @jessi\_cata** · [2026-05-15](https://x.com/jessi_cata/status/2055347938436747459)
> > 
> > "Let all facts about X be indexed by X."
> > 
> > Unjustified assumption. False in set theory. Every subset of some set S corresponds to a fact about S: that it is a superset of that subset. But there are more subsets of S than elements of S. (Cardinality of power set; Cantor's theorem)