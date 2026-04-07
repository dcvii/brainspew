---
title: "The Evolution of Data Warehousing in the AWS Cloud"
source: "https://medium.com/full360/the-evolution-of-data-warehousing-in-the-aws-cloud-cd31638c26e0"
author:
  - "[[Michael David Cobb Bowen]]"
published: 2020-02-04
created: 2026-04-07
description: "The Evolution of Data Warehousing in the AWS Cloud Our company has been designing cloud architectures for BI and Data Warehousing for a decade in the Amazon cloud. There are several new features we …"
tags:
  - "brain_spew"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

## [Full 360 (A Micro Focus Company)](https://medium.com/full360?source=post_page---publication_nav-3fd6096b9b05-cd31638c26e0---------------------------------------)

[![Full 360 (A Micro Focus Company)](https://miro.medium.com/v2/resize:fill:38:38/1*DevO0On9e8FSzyB2R9y55A.png)](https://medium.com/full360?source=post_page---post_publication_sidebar-3fd6096b9b05-cd31638c26e0---------------------------------------)

Full 360 is now part of Micro Focus. [https://www.vertica.com/resources/eon-accelerator-early-access-program-full360-acquisition/](https://www.vertica.com/resources/eon-accelerator-early-access-program-full360-acquisition/)

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*kqtRg-Ie8EWMdShj9uJcEA.jpeg)

Our company has been designing cloud architectures for BI and Data Warehousing for a decade in the Amazon cloud. There are several new features we have been implementing over the past several years at my firm as we evolve our own expertise in satisfying our customers. Allow me to share them with you.

**Cloud Implementation of Big / Fast / Wide**  
The first thing we did back in 2012 was get our hands on **Vertica**, the commercialization of Michael Stonebraker’s [C-Store](http://db.lcs.mit.edu/projects/cstore/) project at MIT. At the time, Vertica was on version 4 or 5, I forget which. What I do remember was that when we got the multi-node clusters working up on AWS it was a breakthrough. This was before Snowflake. This was before Redshift. So we were learning denormalized models. At the time people were asking what is ‘big data’ and our definition has roughly centered around the idea that big data means that you regularly make sets of transforms or transactions that you cannot really test before hand, and tend to be expensive if you have to do them a second time.

But more important to us and to our customers was Wide. This means you can integrate multiple DW applications and have more than 256 columns of data — no more horizontal partitioning of fact tables and data models. (Vertica can handily do 4500 columns wide). This was the basis of a lot of new integrations we did.

Fast was important as well. Most financial DWs were only refreshing MTD data on a nightly basis. We got workloads that were continuous and updated the DW continuously. All under nice control.

**Producer Ingestor Transformer  
T** he next thing we did, learning from the Fast innovations, was that we could have continual idempotent processes running against the DW from any number of streams. Breaking up these processes by leveraging AWS S3 allowed us to optimize each input stream by building its own **Producer**. For us, a Producer is a task that takes data from a source, does a small bit of cleansing and dumps that data into a standardized format.

An **Ingestor** is a process that moves data from the data store (S3) into the database as smartly and as efficiently as the DW can handle it. Since our Producers created a [structured data lake](https://insight.full360.com/what-is-the-role-of-a-structured-data-lake-in-dw-cbc8682cc815) in the first place, the Ingestor can do restatements, incremental loads, or any special kind of update, merge or replacement we choose. Again, every different application will have different requirements.

A **Transformer** uses the power of a sharded multi-node database engine on giant AWS EC2 instances to use easily understandable SQL statements and make set transformations on data. Essentially any stored procedure is done in this manner, thus making the strategy of ELT rather than ETL.

**Containers & Scale Out**  
The next thing we did was to containerize our producers, ingestors and transformers. With this we added a great deal of monitoring of these processes through **Cloudwatch** and ultimately streamlined the process of development and deployment of these containers. We added service discovery with **Consul** for the database engine nodes. We invented [SneaQL](https://www.youtube.com/watch?v=FWVI93hUtGM) to create the conditional executions in ANSI standard SQL. We stored this SQL separate from the database as we iterated over best practices. It made working with containers less cumbersome in our CI/CD process.

Launching our producers, consumers and ingestors in Amazon’s Elastic Container Service (ECS) paved the way for us to scale out horizontally and provide high availability for all of the data streams we manage.

**Multitier Database Architecture**  
One of the things we quickly learned, especially in dealing with website backends, is that a lot of data is provided via APIs and NoSQL sources like **Hadoop**. Also, there are a large number of transactional data that is best handled in-memory with tech like **Redis** or **VoltDB**. Our work with online gaming companies showed that our DW architecture was flexible enough to orchestrate data workloads for complex applications. So once we mastered Producers and Consumers (a consumer is an ingestor & transformer in one) we discovered we could publish and subscribe to everything our customers wanted. This paved the way for our latest innovative practices.

## Get Michael David Cobb Bowen’s stories in your inbox

Join Medium for free to get updates from this writer.

**Plug & Play Data Engineering**  
One of the things we have been able to learn in our history of building on our **PITbull Framework** (Producer Ingestor Transformer) is what languages work best. Our engineers have had the opportunity to learn the AKKA framework in **Scala**. We build a DSL (domain specific language) in Ruby for our first producers, then went to **JRuby** to run faster. We have worked in **Python** for our Lambdas. We are now closing ranks around **Go.**

Let me say something about Lambdas, although it wasn’t automatic, using ECS prepared us for serverless **Fargate**. We don’t necessarily build for serverless just to say that we do, we go about it on a case by case basis. Some more complex tasks simply don’t make sense and the economics of serverless processing can vary widely depending on how you code and how smartly you benchmark performance.

New technologies are evolving all of the time. That includes Redshift and technologies like Athena and Redshift Spectrum. **Apache Spark** has a big role to play. Recently we have mastered the art of horizontal scale out for **Tableau** servers running on AWS. But the fundamental architectural discipline we have makes the applications we build very close to future-proof. We started off being vendor agnostic and it has served our customers well, in addition to making our staff more well-rounded.

**On the Horizon**  
We are very proud of an **AI** (using TensorFlow) application we have developed for the airline industry. We will be publishing more about that in 2020. What makes me particularly excited are two big things that I think are going to revolutionize the industry.

The first is **Apache Beam**. After all I have learned in the past 25 years in this industry, this is probably the most revolutionary framework to come about. Ever time I take an hour or two to study up, I come away more impressed. If you haven’t heard about it, check it out. Basically it sets in theory what we learned in practice — batch processing is just another form of stream processing and all data applications are about managing streams. Streams with different temporalities for different purposes.

That is why I am convinced that **Kafka** is a large part of the future of Data Warehousing. I believe we will be replacing the databases in certain applications with streaming services like Kafka and Kinesis. The kind of data objects we serve in those streams will be very interesting indeed. So bone up message buses and KSQL. It’s the future.

**In Summary & Predictions**  
We have learned a great deal about what DW can do when it is architected in the cloud and subjected to the disciplines of DevOps. Our applications are more highly available, easier to maintain and expand, more interoperable and vendor independent, more secure and capable of handling more diverse loads and types of data. Infrastructure as code had demonstrated to us that we can quickly standup DWs. VLDB has become a great deal more inexpensive and approachable.

So I’ll predict, after the discontinuation of Netezza by IBM (we do migrations), that Teradata is not long for this earth. Also the popularity of Postgres combined with the logic of SneaQL and the reliability of RDS is going to gut Oracle in the DW space. MySQL is officially a toy. Says me.

I’ve heard rumors that GCP is under threat from Google to rapidly gain market share. I think that’s something of an impossible task and I hope they don’t go away. Amazon and Microsoft are not a good duopoly — we need Google in this cloud space. I don’t believe that hybrid clouds are a really safe place to be long-term.

I expect a shakeout in the data science boom, and I reiterate what I’ve always said. The tools will make data science easier and easier. It’s not about the tools; the real value is in knowing an industry in depth.

The future is bright. The frameworks are evolving. The tools will get easier to use. Custom data applications that are industry specific is the way to go. Multi-tier streaming, storage and querying is the future. Never forget [Gall’s Law](http://www.principles-wiki.net/principles:gall_s_law).

One more observation tangential to DW. That is decentralization of data and blockchain. My rule of thumb with regard to organizations is clear. “Decentralize until it hurts, then centralize until it works.” But there’s going to be a lot of work involved with rearchitecting all data collection to be GDPR and CCPA compliant. So I would focus more on making centralized PII data more manageable and guarantee such compliance before pushing data out into the boonies. The secret message is to think about what kind of data objects you can stream in a Kafkaesque data environment.

We continue to innovate for our customers. We are fortunate in our position as a managed service provider to keep our platform up to date. We are especially lucky that our customers and partners keep challenging us to do more. Stay tuned.

[![Full 360 (A Micro Focus Company)](https://miro.medium.com/v2/resize:fill:48:48/1*DevO0On9e8FSzyB2R9y55A.png)](https://medium.com/full360?source=post_page---post_publication_info--cd31638c26e0---------------------------------------)

[![Full 360 (A Micro Focus Company)](https://miro.medium.com/v2/resize:fill:64:64/1*DevO0On9e8FSzyB2R9y55A.png)](https://medium.com/full360?source=post_page---post_publication_info--cd31638c26e0---------------------------------------)

[Last published Mar 26, 2021](https://medium.com/full360/how-to-fine-tune-iam-policies-used-by-terraform-a88fc3f68ed5?source=post_page---post_publication_info--cd31638c26e0---------------------------------------)

Full 360 is now part of Micro Focus. [https://www.vertica.com/resources/eon-accelerator-early-access-program-full360-acquisition/](https://www.vertica.com/resources/eon-accelerator-early-access-program-full360-acquisition/)

[![Michael David Cobb Bowen](https://miro.medium.com/v2/resize:fill:48:48/1*fY3JkK0Pr32KHnbZ8QpV-w.png)](https://medium.com/@mdcbowen?source=post_page---post_author_info--cd31638c26e0---------------------------------------)

[![Michael David Cobb Bowen](https://miro.medium.com/v2/resize:fill:64:64/1*fY3JkK0Pr32KHnbZ8QpV-w.png)](https://medium.com/@mdcbowen?source=post_page---post_author_info--cd31638c26e0---------------------------------------)

[157 following](https://medium.com/@mdcbowen/following?source=post_page---post_author_info--cd31638c26e0---------------------------------------)

dad. architect. writer. entrepreneur. stoic. gearhead. hacker.