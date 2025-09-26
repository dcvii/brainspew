---
title: "Why does “data engineering” usually refer to analytics and not transactional and operational systems?"
source: "https://www.quora.com/Why-does-data-engineering-usually-refer-to-analytics-and-not-transactional-and-operational-systems/answer/Michael-David-Cobb-Bowen"
author:
  - "[[Quora]]"
published:
created: 2025-09-22
description: "Michael David Cobb Bowen's answer: Transactional and operational systems have two major components that make them more simple to deal with.1. You have many (but generally fixed and known) sources that generate simple messages that are routed to a central target. It’s mostly one way traffic.2. ..."
tags:
  - "clippings"
---
[Why does “data engineering” usually refer to analytics and not transactional and operational systems?](https://www.quora.com/unanswered/Why-does-data-engineering-usually-refer-to-analytics-and-not-transactional-and-operational-systems)

Transactional and operational systems have two major components that make them more simple to deal with.

1. You have many (but generally fixed and known) sources that generate simple messages that are routed to a central target. It’s mostly one way traffic.
2. The transactions generated are well-known ahead of time. And transaction technology is old and well understood. You could do it all in COBOL.

Data engineers are dealing with greater complexities in analytical architectures because they are

1. Responding to unknown queries. Query spaces are much larger than transaction spaces.
2. Query processing is still evolving, new technologies are still emerging.
3. Data is blended in unique ways that expands the query space even larger.

In short, the analytic data space is much larger and much more complex that the transaction data space. Think of it this way.

Imagine a car. The RPMs of the engine, the speed of the wheels and the GPS location of the car. That can be generated in every half second and messaged out in a compressed packet about 150 bytes per packet. Brain dead simple. A simple RDBMS system can eat billions of these records every day.

Now imagine you are going to build an Uber client for cellphones where you have millions of customers querying for the positions of millions of cars and you have to recalculate distance and estimated time of arrival. That’s a lot more complex math. You have no idea how many people are going to stare at the screen and therefore generate more queries per minute as opposed to people who don’t look. Processing millions of queries is way more difficult than ingesting billions of tiny fixed format transaction messages.

The specs on the telematics data is not going to change much over time. What millions of customers will demand from the app is going to vary widely. What management of the company will want to infer from that data is going to change much more rapidly than the telematic content.

A data engineer has to evaluate all that as well as select the proper technology that will be compatible with additional datastreams (like financial and customer satisfaction data) that is relevant to the business. Then they have to build the pipelines, integrate the data, archive it, secure it, and save the company money doing so.

Now everybody wants AI too? Good luck.

1 view ·[1 of 1answer](https://www.quora.com/unanswered/Why-does-data-engineering-usually-refer-to-analytics-and-not-transactional-and-operational-systems)

[![Profile photo for Michael David Cobb Bowen](https://qph.cf2.quoracdn.net/main-thumb-17296487-100-nuswfmmvsmekbujhoikudktinmtidakz.jpeg)](https://www.quora.com/profile/Michael-David-Cobb-Bowen)

  

[

View question

](https://www.quora.com/unanswered/Why-does-data-engineering-usually-refer-to-analytics-and-not-transactional-and-operational-systems)