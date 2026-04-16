---
title: "A Guide to Relational Database Design"
source: "https://blog.bytebytego.com/p/a-guide-to-relational-database-design?publication_id=817132&post_id=194403053&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2026-04-16
created: 2026-04-16
description: "In this article, we cover the core concepts that inform those decisions. We’ll look at tables, keys, relationships, normalization, and joins, with each concept building on the last."
tags:
  - "brain_spew"
---
The hardest part of relational database design is not using SQL. The syntax for creating tables, defining keys, and writing joins can be learnt and mastered over time. The difficult part is to develop the thinking that comes before any code gets written, and answering questions about the design of the database.

- Which pieces of information deserve their own table?
- How should tables reference each other?
- How much redundancy is too much?

These are design decisions, and getting them right means our data stays consistent, our queries stay fast, and changes are painless. Getting them wrong means spending months patching problems that were baked into the structure from day one.

In this article, we cover the core concepts that inform those decisions. We’ll look at tables, keys, relationships, normalization, and joins, with each concept building on the last.

![](https://substackcdn.com/image/fetch/$s_!bl9u!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc11ad2cf-e9f9-46f0-b662-f0fc2d2a95f0_2250x2624.png)