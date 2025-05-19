---
title: "The Power of Ten -- Rules for Writing Safety Critical Code -- Rule Eight"
source: "https://www.spinroot.com/p10/rule8.html"
author:
published:
created: 2025-03-10
description:
tags:
  - "coding"
---
---

| #### Rule Eight |  | Limit the use of the preprocessor to file inclusion and simple macros.  The use of the preprocessor must be limited to the inclusion of header files and simple macro definitions. Token pasting, variable argument lists (ellipses), and recursive macro calls are not permitted.   All macros must expand into complete syntactic units.   The use of conditional compilation directives should be restricted to the prevention of duplicate file inclusion in header files. |
| --- | --- | --- |

---

| #### Rationale |  | The C preprocessor is a powerful obfuscation tool that can destroy code clarity and befuddle many text based checkers. The effect of constructs in unrestricted preprocessor code can be extremely hard to decipher, even with a formal language definition in hand. In a new implementation of the C preprocessor, developers often have to resort to using earlier implementations as the referee for interpreting complex defining language in the C standard. The rationale for the caution against conditional compilation is equally important. Note that with just ten conditional compilation directives, there could be up to 2^10 (i.e., 1024) possible versions of the code, each of which would have to be tested -- causing a significant increase in the required test effort. |
| --- | --- | --- |

---

| #### Notes |  | **Macros** Macros should only appear in headerfiles, never in the source code itself. The #undef directive should not be used. Macros should never hide declarations, and they should not hide pointer dereference operations from the code. Macros should also never be used to redefine the language.  The restriction of macro definitions to the definition of complete syntactic units means that *all* macro bodies must be enclosed in either round or curly braces.  **Compiler directives** There should not be more #ifdef directives in a code base than there are headerfiles. Each use of compilation directives (other than the duplicate file inclusion prevention use) should be flagged by a tool-based checker and justified with a comment in the code. |
| --- | --- | --- |

---

| [last rule](https://www.spinroot.com/p10/rule7.html) | [index](https://www.spinroot.com/p10/index.html) | [next rule](https://www.spinroot.com/p10/rule9.html) |
| --- | --- | --- |