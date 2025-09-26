---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Seven"
source: "https://www.spinroot.com/p10/rule7.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Seven |  | Check the return value of all non-void functions, and check the validity of all function parameters.  The return value of non-void functions must be checked by each calling function, and the validity of parameters must be checked inside each function. |
| --- | --- | --- |

---

| #### Rationale |  | This is possibly the most frequently violated rule, and therefore somewhat more suspect as a general principle. In the strictest interpretation, this rule means that even the return value of printf statements and file close statements must be checked.   A case can be made, though, that if the response to an error would rightfully be no different than the response to success, there is no point in checking a return value. This is often the case with calls to printf and close. In cases like these, it can be acceptable to explicitly cast the function return value to (void) -- thereby indicating that the programmer explicitly and not accidentally decides to ignore a return value. The rule is then only violated if the cast is missing.   In more dubious cases, a comment should be present to explain why a return value is irrelevant.  In most cases, though, the return value of a function should not be ignored, especially if error return values must be propagated up the function call chain. Standard libraries famously violate this rule with potentially grave consequences.  See, for instance, what happens if you accidentally execute strlen(0), or strcat(s1, s2, -1) with the standard C string library. For this reason, most coding guidelines for safety critical software also forbid the use of all ansi standard headers like string.h, stdlib.h, stdio.h etc. If the function are needed, they should be written separately, and made compliant with safety critical use.  The enforcement of this rule makes sure that exceptions are always explicitly justified (and justifiable), with mechanical checkers flagging violations.   Often, it will be easier to comply with the rule than to explain why non-compliance is acceptable. |
| --- | --- | --- |

---

| #### Notes |  | **Parameter checking** Function parameters should normall be verified for validity before being used. This rule especially applies to pointers: before dereferencing a pointer that is passed as a parameter the pointer must be checked for null. Similarly, if an integer parameter value is used to index an array, a bounds check should be present to make sure that the index cannot exceed the array bounds.   In some cases it may be acceptable to omit the checks, if, for instance, it can be shown that it is impossible to pass a null-pointer to the function. Static analyzers can help verify that such assumptions are justified. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule6.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule8.html) |
| --- | --- | --- |