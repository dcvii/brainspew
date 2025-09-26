---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Ten"
source: "https://www.spinroot.com/p10/rule10.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Ten |  | Compile with all warnings enabled, in pedantic mode, and use one or more modern static source code analyzers.  All code must be compiled, from the first day of development, with all compiler warnings enabled at the compiler's most pedantic setting. All code must compile with these setting without warnings. All code must be checked on each build with at least one, but preferably more than one, state-of-the-art static source code analyzer and should pass the analyses with zero warnings. |
| --- | --- | --- |

---

| #### Rationale |  | There are several very effective static source code analyzers on the market today, and quite a few freeware tools as well. There is no excuse for any serious software development effort not to make use of this technology. It should be considered routine practice, especially for critical software development. The rule of zero warnings applies even in cases where the compiler or the static analyzer gives an erroneous warning: if the compiler or the static analyzer gets confused, the code causing the confusion should be rewritten so that it becomes more trivially valid. Many have been caught in the assumption that a warning was likely invalid, only to realize much later that the report was in fact valid for less obvious reasons.   Static analyzers originally had a bad reputation due to the limited capabilities of early versions (e.g., the early Unix tool lint). The early tools produced mostly invalid messages, but this is not the case for the current generation of commercial tools. The best static analyzers today are fast, and they produce selective and accurate messages.  For an overview of static source code analyzers for C, see [here](http://spinroot.com/static/).   Recommended tools include [codesonar](http://www.grammatech.com/), [coverity](http://www.coverity.com/), [klocwork](http://www.klocwork.com/), and [uno](http://spinroot.com/uno) (roughly in that order). |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule9.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule1.html) |
| --- | --- | --- |