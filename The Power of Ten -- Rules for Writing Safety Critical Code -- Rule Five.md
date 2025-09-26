---
title: The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Five
source: https://www.spinroot.com/p10/rule5.html
author: 
published: 
created: 2025-03-10
description: 
tags:
  - coding
---
---

| #### Rule Five |  | Use minimally N assertions for every function of more than M lines.  Assertions are used to check for anomalous conditions that should never happen in an execution. Assertions must be *side-effect free* and are best defined as Boolean tests. When an assertion fails, an explicit recovery action should be taken, e.g., by returning an error condition to the caller of the function that executes the failing assertion. Assertions for which a static checking tool can prove that it can never fail or never hold should be removed and replaced with comments. (This means that it is not possible to satisfy the rule by adding unhelpful assert(true) statements throughout the code.)  For safety critical code, typical values for N and M are N=2 and M=20. For less critical applications, the value of M could be increased but to be meaningful it should always be smaller than the maximum function length (See Rule 4). |
| --- | --- | --- |

---

| #### Rationale |  | Statistics for industrial coding efforts indicate that unit tests often find at least one defect per 10 to 100 lines of code written. The odds of intercepting defects increase with assertion density. Use of assertions is often also recommended as part of a strong defensive coding strategy. Assertions can be used to verify pre- and post-conditions of functions, parameter values, return values of functions, and loop-invariants. A typical use of an assertion would be as follows: ``` 	if (!c_assert(p >= 0)) { 		return ERROR; 	} ``` with the assertion defined as follows: ``` 	#define c_assert(e)	((e) ? (true) : \ 		(tst_debugging("%s,%d: assertion '%s' failed\n", \ 		__FILE__, __LINE__, #e), false)) ``` In this definition, \_\_FILE\_\_ and \_\_LINE\_\_ are predefined by the macro preprocessor to produce the filename and line-number of the failing assertion. The syntax #e turns the assertion condition e into a string that is printed as part of the error message. In code destined for an embedded processor there is of course no place to print the error message itself -- in that case, the call to tst\_debugging is turned into a no-op, and the assertion turns into a pure Boolean test that enables error recovery from anomolous behavior.  Assertions should never be disabled. (E.g., they do not just serve to improve the effectiveness of software testing -- they also serve an important role at runtime to catch misbehaving code at the earliest possible moment.) |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule4.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule6.html) |
| --- | --- | --- |