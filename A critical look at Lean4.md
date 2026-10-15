---
title: "A critical look at Lean4"
source: "https://www.lesswrong.com/posts/zHhGa3iQBQcdSifFL/a-critical-look-at-lean4-1"
author:
  - "[[Milo Moses]]"
published: 2026-10-09
created: 2026-10-15
description: "Lots of the discussion around Lean certificates and trust centers around general philosophical ideas of how much humans should trust formal certifica…"
tags:
  - "brainspew"
---
Lots of the discussion around Lean certificates and trust centers around general philosophical ideas of how much humans should trust formal certificates. It's important to remember, though, that Lean4 is not an ideal formal certificate machine: Lean4 is a software in its infancy and has issues. There are reasonable reasons to specifically not trust Lean4.

If we're going to be putting our society's trust in Lean4, I think that it's good to have an open critical discussion of how warranted that trust is.

**Epistemic status:** Most of this work is a factual description about aspects of Lean4 and set theory. I am 85% sure that at most two of these factual descriptions are incorrect. I am 90% sure that, in the current version of Lean4 on Github, there exists a proof of the statement "True=False" that would be accepted in such a way that the Lean community would call it a bug in need of patching (either by messing with the elaborator, compiler, kernel, or some other part of the Lean). I am 2% certain that we will soon be putting huge amounts of trust into Lean4 certificates produced by misaligned AIs, and that the human work we do as a community thinking about and fixing Lean4 in the next 24 months would fall under Less Wrong's classification of a [pivotal act](https://www.lesswrong.com/w/pivotal-act).

## The current status of things

Here's a quote from a [last April](https://leodemoura.github.io/blog/2026-4-2-why-lean/) be Leo de Moura, the creator of Lean.

![leo-de-moura.png](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1791519691/lexical_client_uploads/f9invokjx7ggtmppvbpb.png)

Here's [another post by Leo de Moura](https://leodemoura.github.io/blog/2026-8-1-postmortem-for-kernel-soundness-bug-14576/), three months later:

![leo-de-moura2.png](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1791765643/lexical_client_uploads/c2sjawhr0sodofdx1iz5.png)

Following this incident, the Lean FRO found [seven more bugs in the kernel](https://leodemoura.github.io/blog/2026-8-24-postmortem-for-the-kernel-soundness-bug-hunt/). The new opinion of Leo de Moura: "\[False statements being accepted by Lean\] is going to keep happening. AIs are really good at exploiting soundness bugs in the kernels".

What was the Lean community's reaction to "soundness bug #14576"? There's a nice thread about it on a Lean developer's forum [here](https://leanprover.zulipchat.com/#narrow/channel/270676-lean4/topic/Counterexample.20to.20the.20Lean.20Conjecture.20.28Soundness.20Bug.29).

![Screenshot 2026-10-08 at 9.33.12 PM.png](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1791520397/lexical_client_uploads/vzplii50m6hbezmdubey.png)

Uh oh! Not only do we expect bugs, but there are possibilities of "sea monsters". This article is a bit about the bugs, a bit about the sea monsters, and a bit about the unsafe ways that Lean4 is currently being used (e.g. the un-sandboxed comparator used in [Anthropic's formalization of Fermat's Last Theorem](https://www.anthropic.com/research/formalizing-fermats-last-theorem)).

## What does it mean for Lean4 to be consistent?

Lean4 lets you write mathematical statements and proofs using the bare low-level primitive notions of mathematics, and checks that the proofs are valid using the fundamental axioms. Which axioms? The most standard mathematical axioms are the "Zermelo-Fraenkel plus Choice" axioms (ZFC). These axioms have been vetted by armies of nerds and we're really quite certain that they are consistent. Lean4 is not based on ZFC. It is based on a special home-brew version of dependent type theory, which was designed by picking and choosing features of various modern type theories, with the governing design principle that it should be fast at compile time.

How do we know that Lean4's type theory is consistent? Ideally we would construct some totally convincing proof that if ZFC (or some standard strengthening of of it via [large cardinal axioms](https://en.wikipedia.org/wiki/Large_cardinal)) is consistent, then Lean4 is consistent. However, we currently don't know how to do this.

**As of writing, there is no publicly available proof that Lean4 is consistent with respect to ZFC + any large cardinal axiom.**

When I originally learned that Lean4 had no known consistency proof, I thought this was some sort of bug or technicality. Surely we understand why Lean4 is *supposed* to be consistent, we just haven't bothered writing out the details? My current read of the situation is that this is not the case. Lean4 is not known to consistent, we don't know why it should be consistent, and there are real obstructions to all known proof strategies for showing that Lean4 is consistent.

## Smart people make fundamentally inconsistent type theories all the time

Lean4 is a "dependent type theory". Dependent type theory as a foundation for mathematics was pioneered in 1971 by [Martin-Löf](https://en.wikipedia.org/wiki/Intuitionistic_type_theory). A year after Martin-Löf came out with his type theory, Girard found a contradiction in Martin-Löf's theory. In his [revised paper](https://archive-pml.github.io/martin-lof/pdfs/An-Intuitionistic-Theory-of-Types-1972.pdf), Martin-Löf concluded that one of the axioms “had to be abandoned” and describes the necessary change as “so drastic” that the theory lost substantial expressive strength. Oops! Constructing good dependent type theories is hard.  
  
Outside the world of dependent type theory there are other famous examples of mathematicians trying to come up with new foundations of mathematics and making deep, subtle, fundamental mistakes: Church's 1932 proposed foundations for mathematics using lambda calculus (which was shown to be inconsistent by [Kleene and Rosser](https://www.cis.upenn.edu/~cis5110/Kleene-InconsistencyCertainFormal-1935.pdf)), and Quine's 1940 proposed reworking of ZFC (which was shown to be inconsistent by [Rosser](https://www.cambridge.org/core/journals/journal-of-symbolic-logic/article/abs/buraliforti-paradox/01B4F184BDBDB8F5C29A2D10ECF83907)).

## The status of Lean4's consistency proof

Coming up with consistent foundations for math is tricky business. The ingredients that make Lean4 fast at compile time are the same ingredients that give it access to an unusually strong amount of recursion. For instance, a common proof strategy for showing that dependent type theories are consistent with respect to ZFC + large cardinals is to use the so called "normalization" property. It was proved in 2019 by Abel and Coquand that this [normalization property fails for type theories like Lean's](https://arxiv.org/pdf/1911.08174v4), which in some precise sense means that Lean4's type theory is wild/poorly behaved.

There was a proof of Lean3's consistency [proposed in 2019](https://github.com/digama0/lean-type-theory/releases/tag/v1.0) by Mario Carneiro. This proof works by embedding the primitive notions of Lean3 into the primitive notions of set theory (sets, functions between them), and then showing that the axioms of Lean3 correspond to true statements about sets. Proving that type theories are consistent with respect to ZFC + large cardinals via embedding into set theory is standard business. Unfortunately it came out in 2024 that [there was a flaw in his proof strategy](https://hottest-seminar.github.io/hottestfiles/Carneiro-2025-02-06-HoTTEST.pdf#page=52) (oops!) and that the correct proof would require a new approach. Even if the Lean3 embedding gets fixed, Lean4 adds new features which require non-trivial extensions of that embedding.

I recently asked my GPT-6 Astra to find an embedding of Lean4 into set theory. It spent ~25h and several thousand dollars on the task, and it did not succeed. It kept trying new embeddings and tricks, but every time it found counterexamples using the strong recursive power of Lean4. So it seems to me like finding this set theory embedding is a genuinely non-trivial task, and we don't have a high-level picture of why Lean4 should be consistent.

## Untamed recursion is bug-prone

One of the main things which makes Lean4 logically complex are its "nested inductive types", a sort of declaration where you can define a type in terms of a higher-order property of its own type. Nested inductive types are a new research area, but our understanding is still in its infancy (we've had some good progress in 2026, [here](https://hal.science/hal-05366368v2/document) and [here](https://arxiv.org/pdf/2306.10124)). Preliminary evidence suggests they might be pretty wild. Here's a quote from the former of those two papers:

> "Considering the importance of nested inductive types, one would expect Rocq and Lean to offer good support for them, yet neither one does. They both fail to generate usable elimination principles, and surprisingly accept a different set of nested inductive types, neither of which is satisfactory...
> 
> \[technical paragraph about a problem with Lean's implementation of nested inductive types\]  
>   
> ... this workaround highlights the need for a more systematic treatment of the problem—one that avoids such leakage of the internal encoding. More problematic, since a straightforward mutual encoding becomes impractical in more complex scenarios, Lean ultimately rejects some nested definitions that are theoretically valid—and often crucial for advanced specifications.  
>   
> **These implementation shortcomings likely stem from an incomplete foundational understanding of nested inductive types.**"

The conclusion from the literature, in my view, is that even if Lean4's type theory is consistent at a high level, the nature of nested inductive types makes Lean4's recursion wild. That behavior could be so wild that it is fundamentally incompatible with logic (i.e. is inconsistent), but even assuming that's not the case, it could easily be wild enough to cause bugs.

This is what Chris Bailey was referring to as the "sea monsters" from before - aspects of nested inductive types which are consistent, but wild and ill-behaved and cause bugs. It's impossible to do a systematic search for this bugs currently, because we don't know at a high level what we're looking for. There's no spec to track because nobody knows how Lean4's type theory is supposed to behave.

## "But doesn't con-leche give a proof?"

There was recently a project announced called [con-leche](https://github.com/leanprover/con-leche), which claims to give a formally-verified Lean4 kernel written in Lean4. This is the second attempt at such a project, the first of which is called [lean4lean](https://arxiv.org/abs/2403.14064) and is still under development.

> "\[Con-leche\] intentionally explores a different point in the design space than [lean4lean](https://github.com/digama0/lean4lean/): We compromise on the checker implementation (annotations, extra checks, generated inductive models) so that we can have a direct model-based proof of consistency that does not need some of the hard-to-prove metatheoretical properties of Lean" - Joachim Breitner, creator of con-leche

- Con-leche does not claim to say anything about whether official Lean4 C++ kernel is consistent. It construct its own kernel, and claims that the kernel it constructs is consistent. Con-leche and the official Lean4 handle nested inductive types differently. There are statements which are accepted by the official Lean4 kernel but rejected by con-leche.
	- I tried using Astra to translate con-leche's proof into a proof of a proof of the consistency of the official Lean4 C++ kernel, and there was a real failure in the proof translation.
		- The changes con-leche makes are specifically to avoid the sea monsters. The fact that this embedding works for con-leche does not resolve the relevant issues that make Lean4 difficult.
- There is really subtle set theory and logic afoot. In principle, for the obvious reason, using con-leche to prove the consistency of con-leche is circular. What you try to do is only use the model of set theory embedded within con-leche to prove that con-leche is consistent. However, you have to be careful that your model of set theory hasn't been corrupted by the inconsistent theory surrounding it.

The con-leche experiment is nice (it's good to have more kernels!), but doesn't solve the "sea monster" questions, and it doesn't rule out bugs in the official kernel.[^1]

## Using Lean4 safely

Here is the breakdown of the compute cost associated to running [Anthropic's Lean4 certificate](https://www.anthropic.com/research/formalizing-fermats-last-theorem) of Fermat's Last Theorem:

![Screenshot 2026-10-07 at 1.19.22 PM.png](https://res.cloudinary.com/lesswrong-2-0/image/upload/v1791527799/lexical_client_uploads/pi9ncg4jqqxwbqhwazhf.png)

What is this "comparator" thing that takes all the runtime? The comparator is an extra tool which is useful for making sure that malicious code in the proof body does not mess up the theorem statement during the elaboration+compilation process. This is something you have to worry about even if you trust the kernel completely. As you can see, it takes a long time to run.

Soon, we expect that the world's critical software infrastructure will be formally verified. This is a huge project, which is quite expensive. The difference between running basic Lean4 and running Lean4 + comparator could be the difference between "expensive but doable" and prohibitive.

The broader point is that there are choices you make when you use Lean4. If you wanted, you could run your code in con-leche and nanoda. You could use the comparator. You could sandbox your cached.olean files. None of these are the default behavior of Lean4; these are choices you have to opt into as a developer. The right choice surely depends on the application, and your level of trust in both in Lean4 and agent swarms.

## How much do we trust the agents?

There's an aspect of Anthropic's FLT certificate I find worrying. When running the comparator, they decided to explicitly disable the sandbox that separates the untrusted proof code from the trusted statement. In their codebase, when justifying their decision, they [make the following comment](https://github.com/anthropics/fermats-last-theorem/blob/main/verification/comparator/run.sh):

> "Comparator's own scripts/fake-landrun.sh is used = no sandbox, which is how the recorded run was made; **the sandbox guards against an untrusted solution, which is moot when you built the tree yourself**."

It seems like Anthropic decided that the agent swarm that wrote the FLT proof is trusted, and that guarding against malicious code (even when it is easy to do) is "moot". Do we as a community think this is okay? FLT was a landmark formalization. I can easily imagine somebody pointing to the FLT certificate and saying "of course you should trust my certificate, it passed the level of rigor that FLT did". I think we should set higher standards.[^2]

## Where do we go from here?

All of the issues I talked about seem temporary or fixable. Assuming that Lean4 is consistent, then a proof should exist and we should be able to find it. We should be able to use that understanding of Lean4's foundations to run a systematic bug-search through the Lean4 kernel. We should be able to change the default "maximum trust" behavior of Lean4 to involve significant sandboxing, with formally-proven specs showing that untrusted proofs aren't able to tamper with trusted theorem statements. We should, we should, we should.

Even though Lean4 is open source, not everybody can participate in this journey. Fixing Lean4's safety issues counts as a cybersecurity task, and as such (in my experience), Astra will refrain from answering questions. Astra is happy to try to prove that Lean4 is consistent, but when I've asked it to take seriously the possibility that Lean4 is not consistent it shuts down the chat as cybersecurity. When I ran Anthropic's FLT certificate on my computer, I asked Astra to take a critical look at the logs to make sure there was no funny business and it classified the chat as cybersecurity.

We're entering a world where frontier labs are major decision-makers in cybersecurity. This essay is in part a letter for them: please take Lean4's correctness seriously.  
  
Lean4 is in its infancy. There are still significant hurdles between where we are now and where it needs to be before we can confidently expect it to hold the weight of the world's critical infrastructure against cyberattacks by sophistical, lazy, reward-hacking AI agents.

[^1]: On a more personal note, related to the con-leche experiment: I hope we don't end up in a future where the most trusted software in the world ends up being in a situation where we are told to trust it because of an AI-generated certificate, especially one that has room for loopholes. Certificates are not replacements for understanding.

[^2]: I ran the comparator with the sandbox on the FLT certificate and it checked out. Kevin Buzzard also independently checked the FLT certificate and ran various due-diligence checks. The real community verification of the FLT certificate was at a higher standard than Anthropic's repo.