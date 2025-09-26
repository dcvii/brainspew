---
title: "How AMEX Processes Millions of Daily Transactions With Millisecond Latency"
source: "https://blog.bytebytego.com/p/how-amex-processes-millions-of-daily?publication_id=817132&post_id=160237866&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2023-04-19
created: 2025-04-01
description: "Optimize Kubernetes performance with these essential metrics (Sponsored)"
tags:
  - "clippings"
---
## Optimize Kubernetes performance with these essential metrics (Sponsored)

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F01515b19-0319-471a-b448-2a6f6e983166_2400x1256.png)

Download our comprehensive eBook on optimizing Kubernetes performance. This guide delves into crucial cluster state, resource, and control plane metrics, highlighting 15 of the most essential metrics your DevOps team should be tracking. Learn how to gain complete visibility into your containerized environments and ensure optimal Kubernetes performance with Datadog.

*Disclaimer: The details in this post have been derived from the presentation by the American Express engineering team on the Monster Scale Summit by ScyllaDB. All credit for the technical details goes to the American Express engineering team. Special thanks to ScyllaDB for organizing the event. The links to the original articles are present in the references section at the end of the post. We’ve attempted to analyze the details and provide our input about them. If you find any inaccuracies or omissions, please leave a comment, and we will do our best to fix them.*

American Express processes trillions of dollars worth of transactions every year, which means millions of daily transactions worldwide.

Considering how impatient users can become if a transaction takes too long, these transactions must support low-latency responses in milliseconds. To support this requirement, American Express rebuilt its payment system in 2018 to create a more modern, flexible, and reliable infrastructure.

But what was the problem with the old system?

The older system was a traditional on-premise payment network that relied on legacy infrastructure. It had several limitations that made it less suitable for the future. Also, it was difficult to change and scale based on demand. AMEX wanted to ensure that its payment network could handle increasing transaction volumes while maintaining high speed and security.

The key reasons for the move are as follows:

- **Cloud Readiness**: The previous system was not fully designed for cloud environments. American Express aimed to build a system that could take advantage of cloud computing for better scalability and resilience.
- **Flexibility and Adaptability**: The financial industry evolves rapidly, with new payment technologies and regulations emerging frequently. A redesigned system would allow for quicker updates and integrations with partners.
- **Security and Reliability**: As a major payment provider, American Express needed a network that could process millions of transactions securely and without failure. The updated system was designed to be more resilient against disruptions.
- **Low Latency Processing**: Payments must be processed in milliseconds. The older system faced challenges in meeting modern performance expectations. By upgrading the network, American Express ensured faster transaction approvals and smoother customer experiences.
- **Handling More Transactions** – The volume of digital payments continues to grow. The new system was built to handle a significantly larger number of transactions per second, reducing the risk of slowdowns or failures.

In this article, we’ll look at the architectural and design decisions AMEX engineers made when building the new payment system.

## Make 2025 your Best Year With This $399 FREE AI Masterclass

If you don’t become an AI-enabled professional in 2025, you will:

- Get replaced by a person who uses AI.
- Face slow career growth and income.
- Spend hours on tasks that can be done in 10 minutes.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2a735f2c-8251-427d-8e1e-2da9f1b49351_1600x805.png)

This 3 hour power packed workshop that will teach you 25+ AI Tools, make you a master of prompting & talk about hacks, strategies & secrets that only the top 1% know of. **[Save your seat now](https://bit.ly/Growthschool_040125Save)** (Offer valid for 24 hours only ⏰)

**Here’s why you can’t miss this:**

✅ Learn 30+ cutting-edge AI tools to completely transform the way you work, market, and lead.

✅ Automate your workflows and reclaim **20+ hours a week** (imagine no more burnout).

✅ Create an **AI-powered version of YOU** —a digital clone that handles the tedious work while you focus on what truly matters.

So don’t think twice, you have NOTHING to lose. Consider it a $0 investment that will yield value worth millions. ⏲️ Time: 10 AM EST (Tomorrow)

(First 100 people get it for free + $500 bonus) 🎁

## Global Transaction Router

The centerpiece of the new payment system is the Global Transaction Router (GTR). The AMEX payment system has to interact with different entities involved in handling payment transactions.

- **Acquirers (Merchant Banks):** These are financial institutions or banks that process card transactions on behalf of a merchant. When a customer uses their AMEX card at a store or online, the acquirer is responsible for sending the transaction request to a payment network like AMEX.
- **Processors (Payment Service Providers):** These are companies that manage the technical infrastructure required to handle payment transactions between merchants, acquiring banks, and card networks. Processors ensure that the payment data is securely transmitted and correctly formatted for authorization.
- **Issuers (Card-Issuing Banks):** An issuer is a bank or financial institution that provides the payment card to the customer. The issuer is responsible for verifying whether the cardholder has sufficient funds of credit available to approve the transaction.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2279ce73-d468-4b04-a409-d65628fee72d_1600x952.png)

The GTR sits at the edge of the AMEX network, meaning it is the first system that interacts with these different entities. Here’s how the various entities work with the GTR:

- A merchant (through an acquirer) submits a payment request when a customer uses their AMEX card.
- The request reaches GTR, which determines the best route to process the transaction.
- GTR forwards the request to the processor, which verifies transaction details and forwards it to the issuer.
- The issuer checks if the cardholder has sufficient funds or credit and sends an approve/decline response back through GTR.
- The merchant receives the final approval, and the payment is completed.
- Settlement occurs later when the issuer transfers funds to the acquirer, who then pays the merchant.

### Unique Challenges for the GTR

There were several unique challenges when it came to building the GTR:

- **Managing Long-Lived TCP Sessions:** Unlike modern web services that use short-lived HTTP-based APIs, payment systems often rely on ISO 8583, an older financial messaging standard that operates over long-lived TCP connections. This meant that persistent connections must be maintained for extended periods.
- **Handling ISO 8583 Messages:** ISO 8583 is a widely used but outdated messaging protocol in financial transactions.
- **Traffic Spikes and Load Surges:** Financial transactions do not occur at a constant rate. The system had to handle sudden spikes such as during Black Friday and holiday shopping seasons.
- **Ensuring Ultra-Low Latency:** Payment systems operate on a millisecond scale. Even a small delay in processing a transaction can result in declined payments due to timeouts and bad customer experience if a transaction takes too long to complete.

## Design Decisions of the GTR

The AMEX engineering team made several technical decisions when designing the GTR to ensure it overcame the challenges. Some of the major decisions are as follows:

### 1 - Language Choice: Go (Golang)

The team selected Go (Golang) as the primary language for developing GTR.

But why Go?

One of the major reasons was Go’s concurrency model. Payment transactions involve thousands of concurrent connections, each requiring processing in real time. Go provides goroutines that can handle thousands of open connections efficiently without excessive CPU or memory overhead.

Second, Go compiles ahead of time (AOT), meaning applications start instantly without the need for runtime optimizations. This is important for low-latency transaction processing.

Go’s garbage collector is also optimized for low-latency applications, ensuring that memory cleanup does not interrupt transactional processing. Compared to languages like Java, where garbage collection can cause random pauses (GC spikes), Go’s GC is designed to minimize transaction delays.

### 2 - gRPC over HTTP/2

AMEX opted for gRPC over HTTP/2 to improve internal communication within the payment system.

gRPC uses Protocol Buffers (protobuf) instead of JSON, which results in smaller message sizes and faster serialization and deserialization. When routing payments, GTR converts ISO 8583 messages into gRPC messages using protobuf, making internal processing faster.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F47324ff6-0ff4-4ed8-a49e-7f5df56767fb_1600x1027.png)

Moreover, gRPC over HTTP/2 allows multiplexing, meaning multiple requests can be sent and processed simultaneously on a single TCP connection. This is critical for handling thousands of real-time transactions without delays.

See the diagram below that shows HTTP/2 multiplexing in action.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1f829db0-dff8-46db-b48c-4ab0433d288d_1600x917.png)

### 3 - Asynchronous Logging for Performance Optimization

In traditional systems, logging is synchronous, meaning every time the application writes a log message, it pauses execution until the log is written to a file or database. This slows down transaction processing, especially when dealing with millions of log entries per second.

GTR uses asynchronous logging. Log messages are written to an in-memory buffer instead of being processed immediately. A separate goroutine reads from the buffer and writes logs in batches, reducing contention. This way transactions continue processing while logs are written in the background.

See the diagram below:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7d001ace-b2a1-4494-aa1e-c0f2f798105b_1600x962.png)

Also, AMEX built custom logging handlers using Go’s standard “slog” library. The library helps buffer logs in memory and structure them for easy debugging. AMEX also optimized logging by using log sampling, where only a subset of logs is recorded under heavy load conditions.

## Optimization Strategies

To ensure that the Global Transaction Router could handle millions of transactions per second while maintaining low latency and high reliability, the American Express (AMEX) engineering team implemented several key optimization strategies.

Let’s look at the three major areas of optimization.

### 1 - Profiling and Benchmarking

Profiling is the process of analyzing a program while it is running to identify performance bottlenecks (for example, slow functions, high CPU usage, or memory inefficiencies).

On the other hand, benchmarking involves running a set of tests to measure how well the system performs under different conditions, such as high transaction volumes.

The team used Go’s built-in profiling tools (pprof) to analyze the system’s performance. They measured CPU usage, memory consumption, and execution time for different functions in the codebase. This helped them identify which functions were taking too long to execute and needed optimization.

Next, the team ran benchmark tests by simulating high-traffic scenarios to test how GTR performs under stress. They ran tests to measure parameters such as latency, throughput, and failure recovery.

### 2 - Using Reader-Writer Mutexes

A mutex (mutual exclusion lock) is a mechanism used to control access to shared resources in a concurrent system. If multiple Go routines (threads) try to read and write the same data at the same time, data corruption can occur. A mutex prevents this by allowing only one thread to access the resource at a time.

Instead of using a standard mutex, the AMEX team implemented a Reader-Writer Mutex. This is because a standard mutex locks a resource completely, meaning no other thread can access it until the lock is released. Such an approach is inefficient when multiple threads only need to read the data and creates unnecessary delays by blocking all access.

The Reader-Writer Mutex works differently. It allows multiple read operations to happen at the same time. Write operations still require exclusive access.

See the diagram below that shows the difference between a standard mutex and reader-writer mutex.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffe8c7a05-084c-4f0c-b736-5a3d094b76de_1562x1600.png)

### 3 - Avoiding Excessive Use of Go Channels

Go channels are a way for Go routines to communicate with each other by passing data between them. They are often used to coordinate asynchronous tasks.

Initially, AMEX used Go channels to process transaction data, but they found that this approach was slower than direct socket communication.

Channels introduce extra overhead because:

- Messages need to be queued and synchronized before they are processed.
- Each transaction had to wait for a channel to be read before moving forward.
- This added unnecessary complexity in high-speed financial transactions.

Instead of reading from a TCP socket, sending data through a Go channel, and then writing to a gRPC socket, the team removed the intermediate channel step. Transactions were processed directly from TCP to gRPC, eliminating unnecessary delays.

See the diagram below:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5b91af6f-b8b6-4386-a467-6462fa2e9962_1564x1600.png)

## Operational Best Practices

Lastly, the AMEX engineering team also follows some operational best practices to ensure that the Global Transaction Router works efficiently under all conditions.

### 1 - Continuous Performance Testing For Every Release

Even a small change in the codebase could affect performance, scalability, or transaction speed. A minor update that seems harmless could introduce unexpected bottlenecks in high-traffic scenarios.

Therefore, every release undergoes performance testing, regardless of how small the update is. Benchmark tests are run to measure transaction processing speed, response time, and system resource usage. Load testing tools simulate real-world transaction volumes to ensure the system can handle peak loads.

### 2 - Chaos Testing

Payment networks must remain operational 24/7, even during sudden traffic surges, network outages, or system crashes.

To ensure this, AMEX performs regular chaos testing.

Chaos testing involves intentionally introducing failures or extreme conditions to observe how the system responds. It helps ensure that GTR can recover quickly from unexpected issues without service disruption.

### 3 - Iterative Development Process

Instead of making large, infrequent updates, the AMEX team continuously improves GTR through small, incremental enhancements.

Developers analyze profiling data to find areas where performance can be improved. Instead of deploying large, risky changes, small updates are made frequently.

This approach ensures that performance, security, and scalability are always improving.

## Conclusion

The development of the Global Transaction Router at American Express showcases how a well-architected payment system can achieve high scalability, low latency, and fault tolerance.

By making strategic technical decisions such as using Go for concurrency, gRPC for efficient communication, and asynchronous logging to reduce bottlenecks, the engineering team ensured that GTR could handle millions of transactions per second without performance degradation.

Optimization strategies like profiling and benchmarking, reader-writer mutexes, and direct socket writes further improved transaction processing speed. This has enabled American Express to build a cutting-edge financial transaction system capable of meeting the ever-growing demands of the digital economy.

**References:**

- [Scaling Payments Routing at American Express - Monster Scale Summit 2025](https://www.youtube.com/watch?v=5q0BBfiF-Ic&t=124s)
- [ScyllaDB Tech Talk](https://www.scylladb.com/tech-talk/route-it-like-its-hot-scaling-payments-routing-at-american-express/)
- [Route It Like It’s Hot: Scaling Payments Routing at American Express](https://www.slideshare.net/slideshow/route-it-like-it-s-hot-scaling-payments-routing-at-american-express-by-benjamin-cane)

## SPONSOR US

Get your product in front of more than 1,000,000 tech professionals.

Our newsletter puts your products and services directly in front of an audience that matters - hundreds of thousands of engineering leaders and senior engineers - who have influence over significant tech decisions and big purchases.

Space Fills Up Fast - Reserve Today

Ad spots typically sell out about 4 weeks in advance. To ensure your ad reaches this influential audience, reserve your space now by emailing **[sponsorship@bytebytego.com](https://blog.bytebytego.com/p/)**.