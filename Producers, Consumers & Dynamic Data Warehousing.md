---
title: Producers, Consumers & Dynamic Data Warehousing
source: https://web.archive.org/web/20250211220313/http://www.cubegeek.com/2014/01/producers-consumers-dynamic-data-warehousing.html
author:
  - "[[Cubegeek - AWS 1]]"
published:
created: 2025-10-12
description: So we have a bunch of big ideas around here at Full360 and it seems that I have been doing them rather than talking about them. That's what I like about work. Here's what we're doing now. If you're going...
tags:
  - clippings
---
The Wayback Machine - https://web.archive.org/web/20250211220313/https://www.cubegeek.com/2014/01/producers-consumers-dynamic-data-warehousing.html

||

### Producers, Consumers & Dynamic Data Warehousing

So we have a bunch of big ideas around here at [Full360](https://web.archive.org/web/20250211220313/http://www.full360.com/) and it seems that I have been doing them rather than talking about them. That's what I like about work. Here's what we're doing now.

If you're going to handle big data, sooner or later you're going to get massive amounts that really are too bothersome to keep on your database server in any other form than IN the database. The cheapest place in the world to keep your data is at the NSA, they'll scrape it and store it for you free, indefinitely if you encrypt it. But the cheapest *accessible* place to keep your data is in Amazon S3. So our theory of DW says, keep your permanent record on S3, and build dynamic data warehouses as needed. What? Dynamic data warehouses? Yes, we shall explain but we're not there just yet.

The massive amounts of data on permanent record generally comes in a stream or in multiple streams. In fact, we have abstracted all of our dataflows essentially to streams and have build standard operations around those streams. There is some precise language that I have around here but the purpose of this blog is to just give an overview. Suffice it to say that there are timing and chunking issues between the way data is produced at the source and the way it is consumed into the data warehouse. Therefore, producers and consumers.

A Producer is a chunk of code that aims itself at a source of a datastream, periodically scrapes off a chunk and then stores an {compressed, encrypted, UTF-8'd, versioned} file set onto a time-hierarchally organized S3 bucket. Let's say that your stream was POS transactions from McDonalds. Every hour, you would make a smart query of the transactions based on a time window (which may or may not be redundant) and then send your results to S3. At the end of the day, you'll have 24 flatfiles in the path mickeyd-bucket-name/POS/2014/2014-01/2014-01-09\_0100\_MickeyDPOS.txt or some such. Easy to get, can handle millions of files, no problem. But the point of the producer is that it is synchronized to the actual production of data, whatever the source and chunks it appropriate to the most efficient manner of database ingestion.

Producers have smart sub-features. For example, it is the responsibility of the producer to translate XML or JSON to CSV. We like vertical bars (since we are a Vertica shop, nyuk nyuk) but we call it text file or a flat file anyway. Basically all of the cleansing REGEX, bogus character detection, and internal record consistency stuff takes place in the producer. The producer can be made smarter with regard to time (to avoid redundancy) by tying its query to the DW control table. Most importantly, the producer process itself can be scaled horizontally for scalability and/or redundancy.

The producers create a text-based data warehouse in S3 which is rationalized to the largest set of data any data warehouse can handle. It is all history, all fields, all streams. The consumers determine what goes live and queryable at what rate.

The Consumer is a chunk of code which generates smart efficient updates and merges to the data warehouse in synch with the way that data is consumed by the DW users. So it is the more conventional driver of database operations. In fact, you can think of the actual database production lifecycle in terms of the consumer. As my old good habits dictate, each of these are discrete operations that are verbs.

- Capture
- Ingest
- Cleanse
- Stage
- Merge
- Calc
- Errorfy
- Report
- Distribute

Errorfication is something we've done before but it is a concept that needs a bit of explaining. I'll do that in another post. The rest are basically self-explanatory. Notice that from Ingestion through Merging, we increase the complexity of the operations but reduce the volume of records we ultimately work on. Since we're using columnar shardable database tech, this scales rather well, even though merging will always be a CS nightmare.

Note that the producers and consumers work together in real-time but you can choke them up or down. This is determined by the commit stamps on your control table. So let me talk about that a little bit.

Each file processed into the S3 buckets is going to be registered into a control table. This control table will let us trace all of our records back to S3. IE it is a key into the DW that gives us the provenance of the ETL process. You might be producing on the daily but consuming over the weekend in a 4 hour batch window. Nothing exists to the DW until it is registered which is done immdiately after a bulk copy of a file is loaded to the appropriate source table. Assuming the source table lives until the next step of ETL, the control table will know everything it needs to know about the content of the file loaded into the system. This control table's information is used to throttle the size of consumption chunks. I could go back 2 days, 30 days or two years on my consumer depending upon how much I want to burden my merge process. I could measure those two days by transaction stamps in the datafiles themselves or by the days they were produced to S3. Or I could just rebuild the entire warehouse from scratch or stream by stream.

These are the fundamentals of the dynamic data warehouse. Its great efficiency is that database servers are not burdened with local data - transfers from S3 to the VPC being cheap. It allows near-realtime data loads from disparate external sources, sometimes halfway around the world, and it allows for the exciting possibilities of adding open data into corporate DWs with relative ease. Naturally, dumped DWs can be published elsewhere. It's very cool, sez me.

## Categories

- [AWS (24)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/aws/)
- [Best Practices (46)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/best_practices/)
- [BI Basics (10)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/bi_basics/)
- [Big Data (16)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/big-data/)
- [Blockchain (10)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/blockchain/)
- [Case Stories (11)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/case_stories/)
- [Cloud (13)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/cloud/)
- [Current Affairs (10)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/current_affairs/)
- [DB Tech (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/db-tech/)
- [DevOps (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/devops/)
- [DW (5)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/dw/)
- [eCRM History (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/ecrm_history/)
- [Essbase (19)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/essbase/)
- [Everyday Geekery (73)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/everyday_geekery/)
- [Fast Data (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/fast-data/)
- [Games (5)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/games/)
- [Gear & Gadgets (11)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/gear_gadgets/)
- [golang (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/golang/)
- [Hadoop (2)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/hadoop/)
- [Industry Opinion (70)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/industry_opinion/)
- [Information Theory (14)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/information_theory/)
- [Interesting & Cool (43)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/interesting_cool/)
- [Logos Project (6)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/logos-project/)
- [MDBMS (4)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/mdbms/)
- [Models (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/models/)
- [Multitouch (10)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/multitouch/)
- [Music (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/music/)
- [Odds & Ends (18)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/odds_ends/)
- [Redshift (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/redshift/)
- [Science (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/science/)
- [Security & Identity (10)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/security_identity/)
- [Serverless (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/serverless/)
- [SQL Server (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/sql_server/)
- [Television (2)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/television/)
- [Theory (4)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/theory/)
- [Thinking Machines (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/thinking-machines/)
- [Training Notes (3)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/training-notes/)
- [Transparency (4)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/transparency/)
- [Vertica (5)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/vertica/)
- [Web/Tech (1)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/webtech/)
- [Xerox History (6)](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/xerox_history/)

[Blog](https://web.archive.org/web/20250211220313/https://www.typepad.com/ "Blog") powered by [Typepad](https://web.archive.org/web/20250211220313/https://www.typepad.com/ "TypePad")

## Search

## May 2023

| Sun | Mon | Tue | Wed | Thu | Fri | Sat |
| --- | --- | --- | --- | --- | --- | --- |
|  | 1 | 2 | 3 | [4](https://web.archive.org/web/20250211220313/https://www.cubegeek.com/2023/05/it-begins-again.html) | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 |  |  |  |