---
title: "Solving a \"Fill Forward\" NULL problem with Polars - Confessions of a Data Guy"
source: "https://www.confessionsofadataguy.com/solving-a-fill-forward-null-problem-with-polars/"
author:
  - "[[By Daniel]]"
published:
created: 2025-07-29
description:
tags:
  - "clippings"
---
---

---

I recently used Polars … inside an AWS Lambda … to fill a novel and somewhat obtuse CSV formatting issue.

We were receiving CSV files that contained rows with specific columns that were empty because the following values matched the first one, until a different value finally appeared.

Let me show you.

```
+-----------+-----------+---------+
| City      | Event      | Attends |
+-----------+-----------+---------+
| Chicago   | Marathon   | 5000    |
|           | Parade     | 8000    |
|           | Concert    | 12000   |
| Austin    | Festival   | 10000   |
|           | Rodeo      | 7000    |
+-----------+-----------+---------+
```

… and what it needs to look like is this …

```
+-----------+-----------+---------+
| City      | Event      | Attends |
+-----------+-----------+---------+
| Chicago   | Marathon   | 5000    |
| Chicago   | Parade     | 8000    |
| Chicago   | Concert    | 12000   |
| Austin    | Festival   | 10000   |
| Austin    | Rodeo      | 7000    |
+-----------+-----------+---------+
```

Imagine this strange formatting problem over multiple columns, how annoying uh? This problem, and solution, is usually refered to as the “Fill Forward” … for obvious reasons, you need to carry forward empty rows with the last previous valid vaule.

Can we solve this problem with Polars?

![](https://www.confessionsofadataguy.com/wp-content/uploads/2025/07/polars-1030x702.webp)

Easy enough with Polars.

A simple solution that shows the power of new tools like Polars, after doing some pre-filtering to ensure empty columns have actual NULL for a value, then simply ***FILL\_NULL(strategy=”forward”)*** is all you need to do.

Strange such a weird problem as a solved solution is it not? Goes to show you should do your research on the problem you’re working on, it’s very likely someone has come up with a solution for you.