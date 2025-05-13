---
title: The Power of Ten -- Rules for Writing Safety Critical Code
source: https://www.spinroot.com/p10/
author:
  - "[[Gerard Holzmann]]"
published: 
created: 2025-03-10
description: Ten rules for writing safety critical code, to facilitate analysis and increase software reliability
tags:
  - coding
---
---

| 1 |  | Restrict to simple control flow constructs. | [(details)](https://www.spinroot.com/p10/rule1.html) |
| --- | --- | --- | --- |
| 2 |  | Give all loops a fixed upper-bound. | [(details)](https://www.spinroot.com/p10/rule2.html) |
| 3 |  | Do not use dynamic memory allocation after initialization. | [(details)](https://www.spinroot.com/p10/rule3.html) |
| 4 |  | Limit functions to no more than 60 lines of text. | [(details)](https://www.spinroot.com/p10/rule4.html) |
| 5 |  | Use minimally two assertions per function on average. | [(details)](https://www.spinroot.com/p10/rule5.html) |
| 6 |  | Declare data objects at the smallest possible level of scope. | [(details)](https://www.spinroot.com/p10/rule6.html) |
| 7 |  | Check the return value of non-void functions, and check the validity of function parameters. | [(details)](https://www.spinroot.com/p10/rule7.html) |
| 8 |  | Limit the use of the preprocessor to file inclusion and simple macros. | [(details)](https://www.spinroot.com/p10/rule8.html) |
| 9 |  | Limit the use of pointers. Use no more than two levels of dereferencing per expression. | [(details)](https://www.spinroot.com/p10/rule9.html) |
| 10 |  | Compile with all warnings enabled, and use one or more source code analyzers. | [(details)](https://www.spinroot.com/p10/rule10.html) |

---

Based on: ''The Power of Ten -- Rules for Developing Safety Critical Code,'' *IEEE Computer*, June 2006, pp. 93-95 [(PDF)](http://spinroot.com/gerard/pdf/P10.pdf).

---