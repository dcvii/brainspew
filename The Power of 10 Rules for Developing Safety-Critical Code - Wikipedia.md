---
title: "The Power of 10: Rules for Developing Safety-Critical Code - Wikipedia"
source: "https://en.wikipedia.org/wiki/The_Power_of_10:_Rules_for_Developing_Safety-Critical_Code"
author:
  - "[[Contributors to Wikimedia projects]]"
published: 2012-09-13
created: 2025-12-04
description:
tags:
  - "clippings"
---
**The Power of 10 Rules** were created in 2006 by [Gerard J. Holzmann](https://en.wikipedia.org/wiki/Gerard_J._Holzmann "Gerard J. Holzmann") of the [NASA/JPL](https://en.wikipedia.org/wiki/JPL "JPL") Laboratory for Reliable Software.[^1] The rules are intended to eliminate certain [C](https://en.wikipedia.org/wiki/C_\(programming_language\) "C (programming language)") coding practices that make code difficult to review or statically analyze. These rules are a complement to the [MISRA C](https://en.wikipedia.org/wiki/MISRA_C "MISRA C") guidelines and have been incorporated into the greater set of JPL [coding standards](https://en.wikipedia.org/wiki/Coding_conventions "Coding conventions").[^2]

## Rules

The ten rules are:[^1]

1. Restrict all code to very simple control flow constructs—do not use [goto](https://en.wikipedia.org/wiki/Goto "Goto") statements, setjmp or longjmp constructs, or [direct or indirect recursion](https://en.wikipedia.org/wiki/Recursion_\(computer_science\) "Recursion (computer science)").
2. Give all loops a fixed upper bound. It must be trivially possible for a checking tool to prove statically that the loop cannot exceed a preset upper bound on the number of iterations. If a tool cannot prove the loop bound statically, the rule is considered violated.
3. Do not use [dynamic memory allocation](https://en.wikipedia.org/wiki/Memory_management#DYNAMIC "Memory management") after initialization.
4. No function should be longer than what can be printed on a single sheet of paper in a standard format with one line per statement and one line per declaration. Typically, this means no more than about 60 lines of code per function.
5. The code's [assertions](https://en.wikipedia.org/wiki/Assertion_\(software_development\)#Assertions_for_run-time_checking "Assertion (software development)") density should average to minimally two assertions per function. Assertions must be used to check for anomalous conditions that should never happen in real-life executions. Assertions must be side-effect free and should be defined as Boolean tests. When an assertion fails, an explicit recovery action must be taken such as returning an error condition to the caller of the function that executes the failing assertion. Any assertion for which a static checking tool can prove that it can never fail or never hold violates this rule.
6. Declare all data objects at the smallest possible level of scope.
7. Each calling function must check the return value of nonvoid functions, and each called function must check the validity of all parameters provided by the caller.
8. The use of the [preprocessor](https://en.wikipedia.org/wiki/Preprocessor "Preprocessor") must be limited to the inclusion of [header files](https://en.wikipedia.org/wiki/Include_directive "Include directive") and simple [macros](https://en.wikipedia.org/wiki/Macro_\(computer_science\)#Text-substitution_macros "Macro (computer science)") definitions. Token pasting, variable argument lists (ellipses), and recursive macro calls are not allowed. All macros must expand into complete syntactic units. The use of conditional compilation directives must be kept to a minimum.
9. The use of pointers must be restricted. Specifically, no more than one level of [dereference](https://en.wikipedia.org/wiki/Dereference_operator "Dereference operator") should be used. Pointer dereference operations may not be hidden in macro definitions or inside typedef declarations. [Function pointers](https://en.wikipedia.org/wiki/Function_pointer "Function pointer") are not permitted.
10. All code must be compiled, from the first day of development, with all compiler warnings enabled at the most pedantic setting available. All code must compile without warnings. All code must also be checked daily with at least one, but preferably more than one, strong static source code analyzer and should pass all analyses with zero warnings.

## Uses

The NASA study of the [Toyota electronic throttle control firmware](https://en.wikipedia.org/wiki/2009%E2%80%932011_Toyota_vehicle_recalls "2009–2011 Toyota vehicle recalls") found at least 243 violations of these rules.[^3] [^4]

## See also

- [Life critical system](https://en.wikipedia.org/wiki/Life-critical_system "Life-critical system")
- [Coding conventions](https://en.wikipedia.org/wiki/Coding_conventions "Coding conventions")
- [Software quality](https://en.wikipedia.org/wiki/Software_quality "Software quality")
- [Software assurance](https://en.wikipedia.org/wiki/Software_assurance "Software assurance")

## Further reading

- [G.J. Holzmann](https://en.wikipedia.org/wiki/Gerard_J._Holzmann "Gerard J. Holzmann") (2006-06-19). "The Power of 10: Rules for Developing Safety-Critical Code". *[IEEE Computer](https://en.wikipedia.org/wiki/IEEE_Computer "IEEE Computer")*. **39** (6): 95–99. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1109/MC.2006.212](https://doi.org/10.1109%2FMC.2006.212).

## References

## External links

- [NASA Technical Standards System](https://standards.nasa.gov/standard/NASA/NASA-STD-87398) *Software Assurance and Software Safety Standard*
- [Open Source Satellite: How do you make software that is reliable enough for space missions?](https://opensourcesatellite.org/how-do-you-make-software-reliable-enough-space-travel/)

[^1]: [The Power of 10: Rules for Developing Safety-Critical Code](http://web.eecs.umich.edu/~imarkov/10rules.pdf)

[^2]: [JPL C Coding Standard - JPL Laboratory for Reliable Software](https://web.archive.org/web/20111015064908/http://lars-lab.jpl.nasa.gov/JPL_Coding_Standard_C.pdf)

[^3]: Barr, Michael (2011-03-01). ["Unintended Acceleration And Other Embedded Software Bugs"](https://web.archive.org/web/20240226080759/https://embeddedgurus.com/barr-code/2011/03/unintended-acceleration-and-other-embedded-software-bugs/). *Embedded Gurus*. Archived from [the original](https://embeddedgurus.com/barr-code/2011/03/unintended-acceleration-and-other-embedded-software-bugs/) on 2024-02-26. Retrieved 2025-03-03.

[^4]: ["NASA Engineering and Safety Center Technical Assessment Report, National Highway Traffic Safety Administration Toyota Unintended Acceleration Investigation, Appendix A"](https://web.archive.org/web/20220625035237/https://one.nhtsa.gov/staticfiles/nvs/pdf/NASA_FR_Appendix_A_Software.pdf) (PDF). 2011-01-18. Archived from [the original](https://one.nhtsa.gov/staticfiles/nvs/pdf/NASA_FR_Appendix_A_Software.pdf) (PDF) on 2022-06-25. Retrieved 2025-03-03.