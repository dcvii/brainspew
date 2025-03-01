---
title: Expensive Disk in the 80s
source: https://www.cubegeek.com/2017/06/expensive-disk-in-the-80s.html
author:
  - "[[Cubegeek]]"
published:
created: 2025-02-19
description: (Q) Why was RDBMS invented? I know that RDBMS is all about normalization and relationships. This maintains a strongly connected dataset. Today, I read that originally RDBMS was invented to reduce the footprint of data on disk. Apparently, disk was...
tags:
  - clippings
  - Xerox
---
(Q)
Why was RDBMS invented?
I know that RDBMS is all about normalization and relationships. This maintains a strongly connected dataset. Today, I read that originally RDBMS was invented to reduce the footprint of data on disk. Apparently, disk was more expensive then cpu at that time. Is that true?

(A)

I don’t know how expensive CPU was at the time but disk was very expensive. I was working an internship at Xerox around 1984 and one of my jobs was to build a data dictionary. That was because the division was in the process of moving from hierarchical databases to relational. They chose Focus.
The idea was to put this data dictionary online, but it turned out that it would cost 2 cylinders of DASD. I had no idea how much space that was except I was told to pound sand if I expected to get that much. Well, I said, that’s the size of the old data dictionary. And by the way I needed to get a copy of the old data dictionary to the West Coast from NY. This required something called ‘bulk data transfer’ and again, it was like asking for a free ski trip to Switzerland.
I ended up writing the data dictionary on the newish Xerox Star 8010 Workstation. It had a 40MB hard drive. This was considered a cutting edge thing to do, and I was very sick of dealing with the mainframe guys who refused to debug or run my JCL, but were not above making snarky comments. (So my pal hacked their RACF)
So it turns out that the mighty IBM mainframe DASD 3380 storage worked out to something like this:

Here’s the information in a table format:

| **Model** | **Cylinders** | **Bytes/Track** | **Bytes/Cylinder** | **Capacity (Bytes/Volume)** | **Capacity (MB/GB)** |
| --------- | ------------- | --------------- | ------------------ | --------------------------- | -------------------- |
| 3380-J    | 885           | 47,476          | 712,140            | 630MB                       |                      |
| 3380-E    | 1,770         | 47,476          | 712,140            | 1.26GB                      |                      |
| 3380-K    | 2,655         | 47,476          | 712,140            | 1.89GB                      |                      |

This provides a structured view of the IBM 3380 disk drive models and their specifications. Let me know if you need additional details!

I was literally begging for weeks for what turned out to be 1.4 MB. The mighty mainframe could not afford that much, basically the capacity of a 3.5 inch floppy. (Which were new at the time).
—
I ended up working full time for Xerox in ’87 in a much more interesting division in which we had a stunning 900MB of file service. Not attached to a mainframe mind you, but three massive 300MB file servers I named Cherokee, Apache and Iroquois. Each was the size of a washing machine., and I’d have to venture a guess that each machine, called a Trident, cost about $30,000 each. That’s $100 per MB. Check out this page and that memory squares with prices at the time .
—
I can’t comment on the relative storage space required by relational databases vs hierarchical, but I can testify that standard SQL was an order of magnitude more simple and powerful than the query languages of other databases I had used. Considering that IBM itself moved from ISAM and VSAM to DB2 was all the proof most of the world needed and that Oracle made its fortune over the dead bodies of ADABAS and other stuff that used to dominate the data space in the 80s. I’m sure it had some internal efficiencies working for it.
Disk was monstrously expensive in the 80s. Way back then, I dreamed that someday in the future I would have a Trident in my garage and own 300MB of data. I finally came close to that when I bought a PowerMac 7100 in 1994.