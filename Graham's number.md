---
title: "Graham's number - Simple English Wikipedia, the free encyclopedia"
source: "https://simple.wikipedia.org/wiki/Graham%27s_number"
author:
  - "[[Contributors to Wikimedia projects]]"
published: 2010-02-11
created: 2025-02-10
description:
tags:
  - "clippings"
---
From Simple English Wikipedia, the free encyclopedia

| [![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Question_book-4.svg/50px-Question_book-4.svg.png)](https://simple.wikipedia.org/wiki/File:Question_book-4.svg) | This article **does not have any [sources](https://simple.wikipedia.org/wiki/Wikipedia:Citing_sources "Wikipedia:Citing sources")**. You can help Wikipedia by finding [good](https://simple.wikipedia.org/wiki/Wikipedia:RELIABLE "Wikipedia:RELIABLE") sources, and adding them. *(June 2020)* |
| --- | --- |

**Graham's number** (*G*) is a large [natural number](https://simple.wikipedia.org/wiki/Natural_number "Natural number") that was defined by a man named [Ronald Graham](https://simple.wikipedia.org/wiki/Ronald_Graham "Ronald Graham"). Graham was solving a problem in an area of [mathematics](https://simple.wikipedia.org/wiki/Mathematics "Mathematics") called [Ramsey theory](https://simple.wikipedia.org/wiki/Ramsey_theory "Ramsey theory"). He proved that the answer to his problem was smaller than Graham's number.

Graham's number is one of the greatest numbers ever used in a [mathematical proof](https://simple.wikipedia.org/wiki/Mathematical_proof "Mathematical proof"). Even if every digit in Graham's number were written in the tiniest writing possible, it would still be too big to fit in the [observable universe](https://simple.wikipedia.org/wiki/Observable_universe "Observable universe").

Ramsey theory is an area of mathematics that asks questions like the following:

> Suppose we draw some number of points, and connect every pair of points by a line. Some lines are blue and some are red. Can we always find 3 points for which the 3 lines connecting them are all the same color?

It turns out that for this simple problem, the answer is "yes" when we have 6 or more points, no matter how the lines are colored. But when we have 5 points or fewer, we can color the lines so that the answer is "no".

> Once again, say we have some points, but now they are the corners of an *n*\-dimensional [hypercube](https://simple.wikipedia.org/wiki/Hypercube "Hypercube"). They are still all connected by blue and red lines. For any 4 points, there are 6 lines connecting them. Can we find 4 points that all lie on one [plane](https://simple.wikipedia.org/wiki/Plane_\(mathematics\) "Plane (mathematics)"), and the 6 lines connecting them are all the same color?

By asking that the 4 points lie on a plane, we have made the problem much harder. We would like to know: for what values of *n* is the answer "no" (for some way of coloring the lines), and for what values of *n* is it "yes" (for all ways of coloring the lines)? But this problem has not been completely solved yet.

In 1971, Ronald Graham and B. L. Rothschild found a partial answer to this problem. They showed that for *n*\=6, the answer is "no". But when *n* is very large, as large as Graham's number or larger, the answer is "yes".

One of the reasons this partial answer is important is that it means that the answer is eventually "yes" for at least some large *n*. Before 1971, we didn't know even that much.

There is a much smaller limit for the same problem called N. It is equal to ${\displaystyle f_{64}(4)}$  , where ${\displaystyle f(n)=3\uparrow ^{n}3}$  . This weaker upper bound for the problem, attributed to an unpublished work of Graham, was eventually published and named by Martin Gardner in [Scientific American](https://simple.wikipedia.org/wiki/Scientific_American "Scientific American") in November 1977.

Graham's number is not only too big to write down all of its digits, it is too big even to write in [scientific notation](https://simple.wikipedia.org/wiki/Scientific_notation "Scientific notation"). In order to be able to write it down, we have to use [Knuth's up-arrow notation](https://simple.wikipedia.org/wiki/Knuth%27s_up-arrow_notation "Knuth's up-arrow notation").

We will write down a [sequence](https://simple.wikipedia.org/wiki/Sequence "Sequence") of numbers that we will call **g1**, **g2**, **g3**, and so on. Each one will be used in an [equation](https://simple.wikipedia.org/wiki/Equation "Equation") to find the next. **g64** is Graham's number.

First, here are some examples of up-arrows:

- ${\displaystyle 3\uparrow 3}$ is 3x3x3 which equals 27. An arrow between two numbers just means the first number multiplied by itself the second number of times.
- One can think of ${\displaystyle 3\uparrow \uparrow 3}$ as ${\displaystyle 3\uparrow (3\uparrow 3)}$ because two arrows between numbers A and B just means A written down a B number of times with an arrow in between each A. Because we know what single arrows are, ${\displaystyle 3\uparrow (3\uparrow 3)}$ is 3 multiplied by itself ${\displaystyle 3\uparrow 3}$ times and we know ${\displaystyle 3\uparrow 3}$ is twenty-seven. So ${\displaystyle 3\uparrow \uparrow 3}$ is 3x3x3x3x....x3x3, in total 27 times. That equals 7,625,597,484,987.
- ${\displaystyle 3\uparrow \uparrow \uparrow 3}$ is ${\displaystyle 3\uparrow \uparrow (3\uparrow \uparrow 3)}$ and we know ${\displaystyle 3\uparrow \uparrow 3}$ is 7,625,597,484,987. So ${\displaystyle 3\uparrow \uparrow (3\uparrow \uparrow 3)}$ is ${\displaystyle 3\uparrow \uparrow 7,625,597,484,987}$  . That can also be written as ${\displaystyle 3\uparrow (3\uparrow (3\uparrow (3\uparrow ...(3\uparrow (3\uparrow (3\uparrow 3)}$ with a total of 7,625,597,484,987 3s. This number is so huge, its digits, even written very small, could fill up the observable universe and beyond.
- Although this number may already be beyond comprehension, this is barely the start of this giant number.
- The next step like this is ${\displaystyle 3\uparrow \uparrow \uparrow \uparrow 3}$ or ${\displaystyle 3\uparrow \uparrow \uparrow (3\uparrow \uparrow \uparrow 3)}$  . This is the number we will call the **grahal** (**g1**).

After that, the **graham grahal** (**g2**) is equal to ${\displaystyle 3\uparrow \uparrow \uparrow \uparrow \ldots \uparrow \uparrow \uparrow \uparrow 3}$  ; the number of arrows in this number is **g1**.

Next, **g3** is equal to ${\displaystyle 3\uparrow \uparrow \uparrow \uparrow \uparrow \ldots \uparrow \uparrow \uparrow \uparrow \uparrow 3}$  , where the number of arrows is **g2**.

We keep going in this way. We stop when we define **g64** to be ${\displaystyle 3\uparrow \uparrow \uparrow \uparrow \uparrow \ldots \uparrow \uparrow \uparrow \uparrow \uparrow 3}$  , where the number of arrows is **g63**.

This is Graham's number.

- [Knuth's up-arrow notation](https://simple.wikipedia.org/wiki/Knuth%27s_up-arrow_notation "Knuth's up-arrow notation")