---
title: The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Six
source: https://www.spinroot.com/p10/rule6.html
author: 
published: 
created: 2025-03-10
description: 
tags:
  - coding
---
---

| #### Rule Six |  | Declare data objects at the smallest possible level of scope. |
| --- | --- | --- |

---

| #### Rationale |     | This rule supports a basic principle of data-hiding. Clearly if an object is not in scope, its value cannot be referenced or corrupted. Similarly, if an erroneous value of an object has to be diagnosed, the fewer the number of statements where the value could have been assigned; the easier it is to diagnose the problem. The rule discourages the re-use of variables for multiple, incompatible purposes, which can complicate fault diagnosis. |
| -------------- | --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

---

| #### Notes |  | Data should always be declared at the start of the scope in which it is used: for file scope, the declarations go at the top of the source file (never in a header file); for function scope, the declaration goes at the top of the function body; for block scope, at the start of the block. This means that declarations should not be placed at random places in the code, e.g., that the point of first use.   Data objects only used in one file should be declared file *static*. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule5.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule7.html) |
| --- | --- | --- |