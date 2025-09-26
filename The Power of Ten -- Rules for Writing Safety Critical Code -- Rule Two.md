---
title: The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Two
source: https://www.spinroot.com/p10/rule2.html
author: 
published: 
created: 2025-03-10
description: 
tags:
  - coding
---
---

| #### Rule Two |  | Give all loops a fixed upper-bound.  It must be possible for a checking tool to prove statically that a preset upper-bound on the number of iterations of a loop cannot be exceeded. If the loop-bound cannot be proven statically, the rule is considered violated. |
| --- | --- | --- |

---

| #### Rationale |  | The absence of recursion and the presence of loop bounds helps to prevent runaway code. This rule does not, of course, apply to iterations that are meant to be non-terminating (e.g., in a process or task scheduler), but those cases are relatively rare.  A simple way to comply with this rule is to add an explicit upper-bound to all loops that have a variable number of iterations (e.g., code that traverses a linked list). When the upper-bound is exceeded an assertion failure is triggered, and the function containing the failing iteration returns an error. The upper-bound serves to prevent infinite looping, so in that sense the absolute value of that bound is less important. Tight bounds are still preferred to prevent that a runaway loop does much damage before the bound is reached, and the error detected. Assertions can be used fruitfully in these cases to claim that the loop bound is never exceeded (see [Rule Five](https://www.spinroot.com/p10/rule5.html)).  A nice illustration of what can happen when this rule is violated is the Zune bug from December 31st, 2008: the last day of the first leap year since the Zune-30 model was introduced.  In a simple "day of the year" computation, the devices ended up in an infinite loop, freezing all functionality of the player. The recommended remedy was to let the players drain their batteries, and to start recharging and rebooting them on January 1, 2009. Uncounted numbers of users thus lost the use of this device for at least one day. Had loop bounds been used, the bug could not have happened.  More information (including the source code) can be found on [Wikipedia](https://en.wikipedia.org/wiki/Zune_30), or on [this website](http://www.zuneboards.com/forums/zune-news/38143-cause-zune-30-leapyear-problem-isolated.html). |
| --- | --- | --- |

---

| #### Notes |  | To help a static analyzer determine that a loop necessarily always terminates, it is sometimes necessary to rewrite the code a little to make it more obvious. Note, for instance, that it could require the use of full-blown theorem provers to figure out whether certain computations converge to a specific value. One rule that an analyzer can check for more easily is, for instance, that the loop index from a for-loop in a C program is not modified anywhere inside the loop body. Compliance with this sub-rule is often enforced in safety critical code. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule1.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule3.html) |
| --- | --- | --- |