---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Four"
source: "https://www.spinroot.com/p10/rule4.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Four |  | Limit functions to no more than N lines of text.  A function should not be longer than what can be printed on a single sheet of paper in a standard reference format with one line per statement and one line per declaration. Typically, this means no more than about N=60 lines of code per function.   N can be set to any reasonable value in the range 50..100 lines. |
| --- | --- | --- |

---

| #### Rationale |  | Each function should be a logical unit in the code that is understandable and verifiable as a unit. It is much harder to understand a logical unit that spans multiple screens on a computer display or multiple pages when printed. Excessively long functions are often a sign of poorly structured code. |
| --- | --- | --- |

---

| #### Notes |  | Since we do not want to discourage comments in the code, we normally interpret this rule in the following very specific way:  - Before counting function length, we make a copy of each file, and format it in a standard way (e.g., K&R style). This is to avoid dependencies on specific ways that different developers format their code, and it is to prevent 'cheating' (e.g., by merging multiple statements or declarations into one line).   The normalization of the code layout can be done with the Linux tool indent, e.g. with the call "indent -kr file.c". - Next, we strip all comments and blank lines from the normalized code.   This can be done with the tool ncsl, e.g. with the call "ncsl -s file.c > output" - Next we measure the function length, counting from the function name to the closing curly brace. (That is, every line that contains text is counted, including declarations, curly braces, etc.)  A variation of this rule that is sometimes used is to limit not the full function length, but only the length of each compound statement (if/then/else, and for-, while-, and until-loop bodies). In those cases, a slightly tighter bound would be recommended, using e.g. N=30. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule3.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule5.html) |
| --- | --- | --- |