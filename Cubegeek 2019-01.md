---
title: "Cubegeek"
source: "https://web.archive.org/web/20240526124923/https://www.cubegeek.com/2019/01/index.html"
author:
  - "[[Cubegeek]]"
published:
created: 2025-10-12
description: "Big Data Analytics, perspectives from a 25 year practitioner."
tags:
  - "clippings"
---
The Wayback Machine - https://web.archive.org/web/20240526124923/https://www.cubegeek.com/2019/01/index.html

[« October 2018](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/2018/10/index.html) | [Main](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/) | [August 2019 »](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/2019/08/index.html)

### Deep Variances in Essbase

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

## Categories

- [AWS (24)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20240526124923/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20240526124923/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20240526124923/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |