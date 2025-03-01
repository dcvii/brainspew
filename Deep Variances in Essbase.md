---
title: Deep Variances in Essbase
source: https://www.cubegeek.com/2019/01/deep-variances-in-essbase.html
author:
  - "[[MPP Database Update]]"
  - "[[Michael Bowen]]"
published: 1996-09-14
created: 2025-02-08
description: (from the archives - Fall 1996) In my travels, I have just come upon a neat trick. I've never seen it posted anywhere and it solves a problem I remember being unable to solve a few years ago. Consider a...
tags:
  - clippings
---
(from the archives - Fall 1996)

In my travels, I have just come upon a neat trick. I've never seen it posted anywhere and it solves a problem I remember being unable to solve a few years ago.

Consider a simple model with a geographic dimension 5 levels deep, a measures dimension of sales, and a scenario dimension with actual, plan and variance. How can I get the model to indicate 'deep variances' without having to drill down to them if my high level variances are within spec?

Create 'red flag' and '%red flags' in the scenario dimension.

Let's say that I have a 10% absolute value variance tolerance set.

The member formula for redflag would be

```
if (@abs(variance%>=10)
    redflag = 1;
else
    redflag = 0;
endif
```

Create a 'neutral flag' member in the variance dimension and hardcode the member formula to be 1;

```
redflag% = redflag % neutralflag; (two pass)
```

| geo | actual | plan | variance | variance% | redflag | redflag% |
| --- | --- | --- | --- | --- | --- | --- |
| NY | 100 | 115 | (15) | (15%) | 1 | 100% |
| NJ | 100 | 97 | 3 | 3% | 0 | 0% |
| CT | 100 | 85 | 15 | 15% | 1 | 100% |
| East | 300 | 297 | 3 | 1% | 2 | 67% |

Notice that even though your high level variance is only 1%, 67% of your lower level forecasts are out of bounds with two red flags.

simple, neat.

The comments to this entry are closed.