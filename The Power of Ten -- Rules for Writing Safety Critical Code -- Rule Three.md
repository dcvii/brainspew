---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Three"
source: "https://www.spinroot.com/p10/rule3.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Three |  | Do not use dynamic memory allocation after initialization.  This excludes the use of malloc, sbrk, alloca, and all variants, after thread or process initialization. |
| --- | --- | --- |

---

| #### Rationale |  | This rule is common for safety critical software and appears in most coding guidelines. The reason is simple: memory allocators, such as malloc, and garbage collectors often have unpredictable behavior that can significantly impact performance. A notable class of coding errors also stems from mishandling of memory allocation and free routines: forgetting to free memory or continuing to use memory after it was freed, attempting to allocate more memory than physically available, overstepping boundaries on allocated memory, etc. Forcing all applications to live within a fixed, pre-allocated, area of memory can eliminate many of these problems and make it easier to verify memory use. Note that the only way to dynamically claim memory in the absence of memory allocation from the heap is to use stack memory. In the absence of recursion ([Rule One](https://www.spinroot.com/p10/rule1.html)), an upper-bound on the use of stack memory can derived statically, thus making it possible to prove that an application will always live within its pre-allocated memory means. |
| --- | --- | --- |

---

| #### Notes |  | A common way to implement this check is to allow for memory allocation calls in only function calls with names ending in the suffix "\_init". Typically, there is only one such function per process, and it is executed only once after a system reset or reboot. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule2.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule4.html) |
| --- | --- | --- |