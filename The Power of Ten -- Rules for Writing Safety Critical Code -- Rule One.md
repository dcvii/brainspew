---
title: The Power of Ten -- Rules for Writing Safety Critical Code -- Rule One
source: https://www.spinroot.com/p10/rule1.html
author: 
published: 
created: 2025-03-10
description: 
tags:
  - coding
---
---

| #### Rule One |  | Restrict to simple control flow constructs.  Do not use goto statements, setjmp or longjmp constructs, and do not use direct or indirect recursion. |
| --- | --- | --- |

---

| #### Rationale |  | Simpler control flow translates into stronger capabilities for verification and often results in improved code clarity. The banishment of recursion is perhaps the biggest surprise here. Without recursion, though, we are guaranteed to have an acyclic function call graph, which can be exploited by code analyzers, and can directly help to prove that all executions that should be bounded are in fact bounded (see also [Rule Two](https://www.spinroot.com/p10/rule2.html)).   Note that this rule does not require that all functions have a single point of return -- although this often also simplifies control flow. There are enough cases, though, where an early error return is the simpler solution. |
| --- | --- | --- |

---

| #### Notes |  | Of course, poorly written code does not suddenly become reliable if you just omit these language constructs from it. But, it is true that reliable code is almost always written without them.  **Gotos** first got a bad name when Edsger Dijkstra published his letter in the Communications of the ACM in 1968 ["Goto statement considered harmful"](http://www.acm.org/classics/oct95/). This letter sparked what may well be one of the most heated debates in software engineering in the last few decades. Today, there is very little one could say that could sway someone to change his or her coding style. There is little or no empirical evidence that could tell objectively whether Dijkstra was right or not.  There is a lot of solid code around that contains goto statements. Of course, most of that code is not written to control safety critical systems. Should we feel differently if someones *life* depends on a particular software package doing the right thing -- not just once, but always?  If this does make a difference, then what should we do differently if we had to write that code? Would we not be just a little more paranoid about making the code as transparent and as readable as we possibly can? Think about the last bug you found in your own code. How many times did you have to look at the piece of code that contained the bug before you could spot it? Bugs are adept at hiding and they appreciate all the help we can offer them to do so by making the control flow just a little more complex than necessary.  If someones life is at stake, you should do anything you can to make sure you stay far from any potential danger zone, real or imagined. If gotos can make your code structure a little more complex than it has to be, then the wise thing to do is to find another way to structure it.  If (for critical applications) it takes longer than a few seconds to figure out what the possible *control flow* is through a function, then it should be rewritten.  **Setjmp, longjmp** Very much the same reasoning applies to the abolishment of setjmp and longjump constructs. Fortunately, they are very rarely used already, so it is not a grave restriction to rule them out alltogether.  **Recursion** Avoiding recursion has a different justification. Safety critical software typically runs as embedded software on resource-constrained systems, with little opportunity for user intervention if something goes wrong. Recursion is an elegant programming paradigm based on the mathematical notion of induction. One of the most frequently made mistakes in the programming of safety critical systems is to use the assumption that mathematical concepts can be used unmodified on a physical computer system. The integers we use in software, for instance, are really different from natural numbers: they have limited precision, and strange things can happen if we accidentily cross these limits. Similarly, the use of recursion is convenient if we can assume the availability of an unbounded stack. But, stacks are never unbounded, they have a bound and if we cross that bound accidentily bad things can happen. Often embedded systems are also not very strong in offering standard protections such as memory protection or stack protection that would prevent a runaway program from overshooting its stack, or writing in forbidden memory locations. It can be difficult to reason convincingly that the maximum recursion depth will always respect a given stack limit. Furtunately, recursion can always be replaced with basic iteration. The stack issue now disappears, and all we now need to worry about is that the iteration is bounded (see Rule 2). |  |
| --- | --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule10.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule2.html) |
| --- | --- | --- |