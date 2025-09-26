---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Nine"
source: "https://www.spinroot.com/p10/rule9.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Nine |  | Limit the use of pointers. Use no more than N levels of dereferencing (star operators) per expression. A strict value for N=1, but in some cases using N=2 can be justified.  Pointer dereference operations may not be hidden in macro definitions or inside typedef declarations. The use of function pointers should be restricted to simple cases. |
| --- | --- | --- |

---

| #### Rationale |  | Pointers are easily misused, even by experienced programmers. They can make it hard to follow or analyze the flow of data in a program, especially by tool-based static analyzers. Function pointers, similarly, can seriously restrict the types of checks that can be performed by static analyzers and should only be used if there is a strong justification for their use, and ideally alternate means are provided to assist tool-based checkers determine flow of control and function call hierarchies. For instance, if function pointers are used, it can become impossible for a tool to prove absence of recursion, so alternate guarantees would have to be provided to make up for this loss in analytical capabilities. |
| --- | --- | --- |

---

| #### Notes |  | **Derefence operations** The limit of two derefence operations per expression means that there should be no more than two star operators to the left or to the right of an assignment operator, or in any single conditional expression.  **Function pointers** It should be possible for a static analyzer to determine in all cases which function is being called, if the call is made through a function pointer. It may be acceptable to allow cases where the number of possible functions that may be called is larger than one, provided it does not affect the precision of the code analysis itself. This means that it can depend on the capabilities of a specific static analyzer what liberties can be taken with the use of function pointers.   Additionally, though, it is wise to keep function pointer use to a minimum, and to restrict to simple cases, to make sure that also humans can determine accurately and with modest effort which functions may be evoked. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule8.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule10.html) |
| --- | --- | --- |