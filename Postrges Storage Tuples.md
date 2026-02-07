---
title: "Thread by @arpit_bhayani"
source: "https://x.com/arpit_bhayani/status/2018306637938020484"
author:
  - "[[@arpit_bhayani]]"
published: 2026-02-02
created: 2026-02-02
description: "Rusty guy in a blue neighborhood of a red county of a blue state.  Live in gratitude, not a bubble."
tags:
  - "clippings"
---
**Arpit Bhayani** @arpit\_bhayani [2026-02-02](https://x.com/arpit_bhayani/status/2018306637938020484)

Rows in PostgreSQL are immutable and stored on the 'heap'. Every row has a hidden identifier called CTID that points to its physical location on disk.

CTID is a tuple identifier with two parts: the page number and the index within that page. You can see it with a simple query:

\`\`\`

SELECT ctid, \* FROM your\_table;

\`\`\`

The output looks like (0,1), (0,2), (1,1), where the first number is the page and the second is the position.

Here's what makes CTID interesting: when you create a primary key index, the index doesn't store the entire row. It stores the value and the CTID, which points to the actual row location on the heap.

This is why lookups are fast. The index gives you the CTID, and PostgreSQL jumps directly to that physical location on the heap to fetch the row.

But here's the catch: CTID changes when a row is updated. PostgreSQL uses MVCC (Multi-Version Concurrency Control), so updates create new row versions at different physical locations. The old CTID becomes invalid, and the row gets a new one.

This is why indexes need to be updated on every row update. The key value might stay the same, but the CTID it points to changes.

Interesting design choices. PostgreSQL saved one indirection by saving CTID, but now the index needs to be updated even if non-indexed columns are modified.

This is why I absolutely love going through the internals of databases :) It is filled with interesting design choices and trade-offs.

---

**Jagdish Parihar** @jatin6972 [2026-02-02](https://x.com/jatin6972/status/2018432286514200711)

@grok what is the reason behind this design choice ? pros and cons ?

---

**Akash Ranjan** @akashbitm787 [2026-02-02](https://x.com/akashbitm787/status/2018331887559958605)

Mind-blown by PostgreSQL internals like this!

That CTID → heap pointer design explains so much about why updates are heavier than we think, even changing a non-indexed column forces index updates.

I remember debugging a slow UPDATE and realizing it was due to index

---

**Sevik** @sevikkk13 [2026-02-02](https://x.com/sevikkk13/status/2018423563909550285)

Because of MVCC, updating a row does not remove the old one, as it can still be visible to other transactions. So a new row is inserted into the index, and the old row stays there as well until vacuum removes the physical row when it’s no longer visible to any active transaction.

---

**The Daft Knight** @the\_daftknight [2026-02-02](https://x.com/the_daftknight/status/2018339104753430638)

Can you also share the sources you looked up for your research regarding this. Were they official docs or did you directly have a look at the source code or something else. How does one start if we want to have a closer look at such things.

---

**Manthan Indane** @manthanindane [2026-02-02](https://x.com/manthanindane/status/2018332228116447618)

this is such a clean tradeoff. faster reads by jumping straight to the heap, but you pay for it on updates. database design is just choosing where you want the pain.

---

**avrl** @techdevdaily [2026-02-02](https://x.com/techdevdaily/status/2018312381705888057)

Nice design choice. Really puts in the perspective how detailed these things are when we open the hood on them, every design decision, every implementation serves a purpose. I don't know in this AI era people are thinking to put thay much thought into building stuff. I think

---

**Albert Sebastian** @albeinstein92 [2026-02-02](https://x.com/albeinstein92/status/2018339182272512490)

if you didnt have auto vacuum for a table and it had millions of entries. it opens up a very specific issue in psql when you try to vacuum it.

---

**Kishor Pawar** @iskishor [2026-02-02](https://x.com/iskishor/status/2018312352241000654)

This CTID approach must have helped PostgreSQL make the indexes lighter, no?

---

**Divs** @divs117 [2026-02-02](https://x.com/divs117/status/2018316384326070614)

Interesting stuff, going deep into PostgreSQL definitely seems like a good time investment.

---

**Jetha** @hariommandloi4 [2026-02-02](https://x.com/hariommandloi4/status/2018312921554846103)

Good read. @grok Why CTID changes on updates? What are the challenges if we keep ctid same?

---

**Sudheer Gajula** @SudheerGajula3 [2026-02-02](https://x.com/SudheerGajula3/status/2018381995198574705)

Another interesting topic is HOT - heap only tuple. This comes into picture when update doesn’t affect indexed columns and page still has space to accommodate new tuple. When both these conditions are met, it creates new tuple and pointers are updated.

---

**chaithanya reddy** @chaithanya\_187 [2026-02-02](https://x.com/chaithanya_187/status/2018319017388413278)

For non indexed columns they introduced this phenomenon called hot updates where the pointer to the row updates within the page (8kb). fill factor plays a crucial role here though we leave some space in these pages for these updates

---

**Rishabh Singh** @rishabh\_1056 [2026-02-02](https://x.com/rishabh_1056/status/2018347756537135489)

Just today itself I was exploring prepared statements and went down a little too deep into the rabbit hole to independently discover this exact mechanism : https://claude.ai/share/c2ab4f90-9184-40d1-a62b-48dee73320de…

---

**allen (love/acc)** @allenkaplan [2026-02-02](https://x.com/allenkaplan/status/2018420554446098531)

this is why understanding HOT updates and index management is key