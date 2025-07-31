---
title: "How did early software developers manage to create efficient programs with such limited computing resources?"
source: "https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?ch=10&oid=1477743853178229&share=78739106&srid=tIPY&target_type=answer"
author:
  - "[[Quora]]"
published:
created: 2025-04-03
description: "Alan Kay's answer: Basically: “every which way” they could think of — and this was actually “highly motivated” by the limitations of computing resources.For example, I have often showed movies of the amazing 1968 Engelbart “Mother of all demos” with its subsecond response times, pointed out tha..."
tags:
  - "clippings"
---


Basically: “every which way” they could think of — and this was actually “highly motivated” by the limitations of computing resources.

For example, I have often showed movies of the amazing 1968 Engelbart “Mother of all demos” with its subsecond response times, pointed out that it was done on a half MIP, 24bit, 192KB time-shared computer with multiple users, and asked “how was this possible?”. Only once in years of asking this question have I ever gotten an accurate answer (interestingly from a student in an audience of undergrads): “Because they \*wanted\* subsecond response?”

Yep. That was one of their principal goals, and they kept it, no matter what.

Another way to look at this is that the instruction times of even really slow computers, even slow computers running interpreters (and losing another factor of 10 or so), are much faster than human nervous systems, so even for interactive systems in the early days — such as “George” on Whirlwind in 1954 — one could get quite good real-time response.

And — in general, whether real-time or batch — many of the earliest programmers were also mathematicians, and so had a feeling for both “abstraction” and “deeper meta”.

Also — a bit of apples and oranges here — the most stringent limitation most of the time was “amount of available RAM”. This tended to dominate how programming needed to be done (basically, if you have to swap/overlay from secondary storage, you have killed your average cycle time). One of the most amazing examples of this was done by Hal Laning (the original creator of “George”) for the extremely slow and limited Apollo Guidance Computer for the moon shot project. The basic computer had a memory cycle time of ~16 bits in 12 microseconds with a RAM of 4KB, however many operations were actually done by an interpreter whose pseudocode ran about 50IPS (!)

One of my favorite “bang for the buck” systems from ca 60 years ago was the Meta II compiler-compiler done on an 8K 6-bit byte IBM 1401 computer by Val Schorre at UCLA. This worked because he had really thought through the problem space and had come up with a tiny meta-characterization that had enough range to deal with a wide range of higher level languages (this is basically the “Math Wins!” idea). He was also able to apply the meta-idea to itself to get the pseudo-code for the system that a simple interpreter on the 1401 could run.

He wrote a classic small paper that was able to give explicit implementable examples of the meta system, a teaching example, and two sample “Algol-level” languages. The system in itself is fun to contemplate:

[This is the link to the entire paper](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=http%3A%2F%2Fwww.chiltoncomputing.org.uk%2Facl%2Fpdfs%2Fschorre.pdf&ved=2ahUKEwih_9m2yruMAxXcSkEAHYfaISgQFnoECBcQAQ&usg=AOvVaw3yw60lbP8ogacYZDA_uiVa "www.google.com")

Basic idea here is that there is often — even “usually” — some “meta math” under most problems. Spending some time trying to articulate and represent this will often result in much tinier, easier to understand and debug systems.

2.5K views · View 69 upvotes · Answer requested by [Miguel Paraz](https://www.quora.com/profile/Miguel-Paraz) [1 of 3answers](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources) Comments [Karl Snowsill](https://www.quora.com/profile/Karl-Snowsill) · [4h](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?comment_id=465075585&comment_type=2)

Being interesting in programming languages and compilers, you must have met Gary Kildall at least once.

[Alan Kay](https://www.quora.com/profile/Alan-Kay-11) · [1h](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?comment_id=465101314&comment_type=2)

I did talk to him a few times in the very early 80s while I was at Atari.

Karl Snowsill Must have been a very interesting time. Did situation like this ever occur? For comedic purposes, any likeness to real people/events is purely coincidental\* [JWC](https://www.quora.com/profile/JWC-23) · [3h](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?comment_id=465081906&comment_type=2)

What do you mean by “Math Wins idea”? Or “applied the meta-idea to itself?”

[Alan Kay](https://www.quora.com/profile/Alan-Kay-11) · [1h](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?comment_id=465099845&comment_type=2) “Math wins!” means that “really using what ‘math’ is all about” will often wind up with much more compact, understandable, powerful, etc. representations of the intrinsic relationships of a situation (it doesn’t mean that some existing math is going to help (sometimes it does), but means that “math… (more) JWC Isn’t the syntactic definition of a programming language just that, a language problem? Where does math come into play here?[Sanjay Kumar](https://www.quora.com/profile/Sanjay-Kumar-27705) · [1h](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources/answer/Alan-Kay-11?comment_id=465104689&comment_type=2)

Sir I want to learn programming how to do it I just cram codes don't have understanding skills.any suggestions

[View 2 other answers to this question](https://www.quora.com/How-did-early-software-developers-manage-to-create-efficient-programs-with-such-limited-computing-resources) About the Author [Alan Kay](https://www.quora.com/profile/Alan-Kay-11) 27followers you know [Jay Wacker](https://www.quora.com/profile/Jay-Wacker), [Tom Musgrove](https://www.quora.com/profile/Tom-Musgrove), [Mills Baker](https://www.quora.com/profile/Mills-Baker), [Joseph Boyle](https://www.quora.com/profile/Joseph-Boyle) and 23others you follow Curious Studied at University of Colorado Boulder 8.2M content views 58.2K this month Top Writer 2018 and 2017 Active in 4Spaces More answers from Alan Kay [View more](https://www.quora.com/profile/Alan-Kay-11)