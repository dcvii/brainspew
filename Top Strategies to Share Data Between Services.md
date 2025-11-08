---
title: "Top Strategies to Share Data Between Services"
source: "https://blog.bytebytego.com/p/top-strategies-to-share-data-between?publication_id=817132&post_id=178169954&isFreemail=false&r=7br8e&triedRedirect=true"
author:
  - "[[ByteByteGo]]"
published: 2025-11-06
created: 2025-11-06
description: "In this article, we explore these questions in depth. We investigate the difference between sharing a data source and sharing data, and examine the main strategies used to share data between services."
tags:
  - "clippings"
---
Modern software systems have grown more complex, and many organizations have moved from building large monolithic applications to using services. This shift offers several benefits, such as faster development, easier deployment, and better scalability. However, it also introduces new challenges, especially in how services handle and share data.

In a monolithic system, all components share the same database. Any part of the application can read or update data from a common source. This makes coordination simple but also creates tight coupling between different parts of the system. A small change in one area can affect the entire application.

In contrast, service-oriented architectures divide the system into smaller, independent services. Each service is responsible for a specific business function and should manage its own data. This principle is often referred to as service data ownership. It ensures that services can be developed, tested, and deployed independently without depending on the internal workings of other services.

However, even though services own their data, they still need to exchange information with each other. For example, an order service may need customer details from a customer service, or a payment service may need transaction information from an order service. Sharing data between services becomes essential for the system to work as a whole.

The main challenge, then, is how to share data without losing the independence that microservices aim to achieve.

- Should multiple services connect to the same database?
- Or should they communicate through APIs or messages?
- How do we ensure consistency, performance, and fault tolerance while keeping services loosely coupled?

In this article, we explore these questions in depth. We investigate the difference between sharing a data source and sharing data, and examine the main strategies used to share data between services.

![](https://substackcdn.com/image/fetch/$s_!9vpY!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff5f41f86-4bf2-4b21-85aa-69659c039111_2250x2624.png)

## Data Ownership and Isolation

One of the core principles of service-oriented architecture is that each service should own its data. This means a service is fully responsible for how its data is stored, updated, and accessed. It also means that no other service should directly read or write to that service’s database. This rule may seem restrictive at first, but it exists to protect independence and stability within the system.

When multiple services share the same physical database, they become tightly coupled.

A change in one service’s schema or query can accidentally break another service that depends on the same tables. This leads to cross-service schema dependencies, where teams must coordinate every schema change. Over time, this slows down development and makes deployments risky. Shared databases can also cause versioning deadlocks, where one team cannot release new features because another team’s code still depends on the old structure.

Owning data allows each service to evolve independently. Teams can choose the most suitable database technology for their needs. For example, a relational database for transactions, a document store for product catalogs, or a time-series database for metrics. This freedom, known as polyglot persistence, improves scalability and performance.

It is important to understand that data ownership does not mean isolation from the rest of the system. Services still need to share information, but they should do so through controlled interfaces such as APIs or events. The distinction lies not in whether data is shared, but how it is shared.

## Sharing a Data Source vs Sharing Data

A common source of confusion in service-based systems is the difference between sharing a data source and sharing data. Although the two sound similar, they represent very different approaches with very different consequences.

Sharing a data source means that multiple services directly connect to and use the same database.

For example, both an Order service and a Product service might read and write to the same tables in a shared database. While this setup may seem convenient, it creates hidden dependencies between services. Any change in the database schema or queries used by one service can unintentionally break another.

Over time, this leads to tight coupling, fragile deployments, and coordination overhead between teams. The independence that microservices promise is effectively lost because all services are tied to a single shared source of truth.

See the diagram below:

![](https://substackcdn.com/image/fetch/$s_!NkAG!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fce171013-be83-489a-a84c-8fd2fc5b1b08_2508x1606.png)

Sharing data, on the other hand, is about controlled communication. Each service owns its own database and exposes only the information others need through well-defined interfaces. This could be anything, such as REST APIs or gRPC APIs, message queues, or replication streams.

In this model, services don’t directly touch each other’s data stores but exchange data in a structured and predictable way. For example, in a monolithic system, showing order details along with product names might simply involve a SQL join between the orders and products tables. In a microservices setup, the Order service would instead call the Product service’s API to retrieve product information or consume an event containing product updates.

## Synchronous Data Sharing

Synchronous data sharing happens when one service calls another service and waits for a response before continuing its own operation.

This approach feels very similar to how functions call each other within a monolithic application. The caller pauses until it receives the data it needs. Because of this, synchronous communication provides strong consistency. The data received is always the most up-to-date at that moment.

However, it also introduces dependencies between services, which can reduce overall reliability and independence. If one service is slow or unavailable, the delay or failure can quickly spread across the system.

Despite these drawbacks, synchronous data sharing is still common, especially when real-time data accuracy is critical. Let’s look at some common patterns.

### Request-Response Model

The most common synchronous pattern is the request-response model, usually implemented using REST or gRPC APIs. In this model, Service A sends a request to Service B asking for specific information, such as product details, and then waits for the reply before continuing.

![](https://substackcdn.com/image/fetch/$s_!J-D2!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F48b874b6-a6cf-4dcf-ae49-16b302a3b291_1674x960.png)

This pattern is easy to understand and implement. It guarantees immediate consistency because Service A always retrieves the latest data directly from the source. It’s also simple to debug, as requests and responses can be traced easily in logs.

However, this model can also cause several issues. Each network call adds latency to the overall response time. If one service goes down or becomes slow, every other service that depends on it can also be affected. This problem is known as cascading failure. To prevent this, developers often use timeouts, retries with exponential backoff, and circuit breakers to stop a failing service from overwhelming the rest of the system.

While the request-response model works well for small systems, it can become fragile when hundreds of services depend on each other.

### Gateway or Orchestrator Pattern

In more complex systems, synchronous data sharing can be coordinated using a gateway or orchestrator service. This gateway acts as a central controller that handles requests involving multiple services.

For example, if a product update requires changes in both the Product and Order services, the gateway sends update requests to each of them and waits for their confirmation. Only when all services report success does the gateway confirm that the operation is complete. If any service fails, the gateway can roll back the changes to maintain consistency.

![](https://substackcdn.com/image/fetch/$s_!JJkp!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Faf460506-bb46-4482-a942-ae0e447e765a_2508x1604.png)

This pattern simplifies coordination for clients and keeps business logic centralized. However, it also introduces new challenges.

- The gateway can become a bottleneck or single point of failure if it handles too many operations.
- It can also struggle to maintain performance in high-latency environments, where waiting for multiple services to respond increases total response time.

In many ways, it resembles a lightweight version of a two-phase commit, which provides consistency at the cost of scalability and fault tolerance.

### Synchronous Caching and Duplication

To reduce the delays caused by synchronous calls, some systems use local caching or data duplication. A service stores copies of frequently accessed data (such as product names or user profiles) so it does not need to make repeated network calls.

While this improves performance and reduces dependency on other services, it introduces a new problem: data consistency.

If the original data changes, the cached copy can become outdated, leading to incorrect results. This trade-off highlights the limits of purely synchronous models and sets the stage for asynchronous data sharing, where updates propagate automatically without blocking requests.

## Asynchronous Data Sharing

Asynchronous data sharing has become the preferred approach for large, distributed systems.

In this model, services exchange information without waiting for immediate responses. Instead of making blocking calls, a service publishes messages or events that other services can consume whenever they are ready. This style of communication promotes independence, scalability, and fault tolerance.

Since services do not rely on one another’s availability to function, temporary failures or slowdowns do not cause a system-wide outage. Each service can continue working and process messages later when it recovers. However, this flexibility comes at a cost. Asynchronous systems introduce eventual consistency, meaning that data may take a short time to become fully synchronized across all services. They can also be harder to debug since data flow happens across multiple queues and logs rather than direct API calls.

Still, for most high-scale systems, the benefits of resilience and scalability make asynchronous communication an essential design choice.

Let us look at some key building blocks of this approach.

### Event-Driven Architecture

In an event-driven architecture, services communicate through events that represent meaningful changes in the system. When a service performs an operation or its state changes, it publishes an event such as OrderCreated, UserRegistered, or ProductUpdated to a central message broker or event bus.

Other services can subscribe to these events and react accordingly. For example, when the Order service publishes an OrderCreated event, the Inventory service might decrease stock levels, and the Notification service might send a confirmation email. Each subscriber maintains its own local data based on the events it receives.

![](https://substackcdn.com/image/fetch/$s_!vdDT!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8974f2d1-7eba-4142-b70e-54bbaf8fb917_2508x1546.png)

This approach allows services to evolve independently. A new service can start listening to existing events without changing the services that produce them. It also makes the system more extensible since producers do not need to know who is consuming their events. The trade-off is that data synchronization becomes eventually consistent, as updates propagate asynchronously through the system.

### Message Brokers

At the heart of asynchronous data sharing lies the message broker, a system that routes events between producers and consumers. Popular examples include RabbitMQ and AWS SNS/SQS.

Message brokers organize communication using concepts like topics and queues. Producers send messages to a topic, and consumers subscribe to one or more topics to receive relevant messages.

Different brokers offer varying delivery guarantees. Some aim for at-most-once delivery, where each message is delivered zero or one time. Others use at-least-once, which ensures every message is delivered but may result in duplicates. More advanced systems implement exactly-once semantics, ensuring a message is processed only once, even in the presence of retries.

To handle real-world challenges like failures or retries, systems use dead-letter queues to store unprocessed messages and retry queues to reattempt processing later. Consumers must be designed to be idempotent, meaning they can safely process the same message multiple times without corrupting data. These techniques make asynchronous pipelines reliable and self-healing.

### Event Sourcing and Change Data Capture (CDC)

Asynchronous communication can be extended through architectural patterns like event sourcing and change data capture (CDC).

In event sourcing, every change in application state is recorded as a series of immutable events rather than as direct updates to a database record. For example, instead of simply changing an order’s status to “Shipped,” the system would record an OrderShipped event. The current state of an entity can then be reconstructed at any time by replaying its event history. This provides an auditable and consistent record of all state changes.

See the diagram below for an example of event sourcing pattern:

![](https://substackcdn.com/image/fetch/$s_!9Ud4!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5ed21d95-a6c8-4dcf-a707-ae72186b2086_2276x1606.png)

Change Data Capture (CDC) takes a more practical approach for existing systems. It tracks changes directly from a database’s transaction logs and converts them into event streams. For instance, when a product name is updated in the Product database, a CDC tool such as Debezium or AWS Database Migration Service (DMS) can detect the change and publish a ProductUpdated event. Other services, such as the Order service, can then consume this event to update their local copies.

These patterns help achieve near real-time synchronization without breaking the rule of data ownership. They allow services to remain isolated yet stay up-to-date with changes across the ecosystem.

### Eventual Consistency and Data Synchronization

In asynchronous systems, eventual consistency is not a weakness but a deliberate design choice. It means that while data across services may not be instantly synchronized, it will become consistent once all events are processed.

Each service maintains its own local copy of the data it depends on. When the original data changes, the owning service publishes an event, and the consuming services update their local versions accordingly. For instance, when a product’s price is updated, the Product service emits a ProductUpdated event, and the Order service adjusts its local record of the product.

![](https://substackcdn.com/image/fetch/$s_!Azh_!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2f7d48ec-75f3-4e18-b3e9-3afbe198a7b6_2508x1604.png)

There may be short delays before all services reflect the latest state. To manage this, systems often use techniques such as versioning (to track which data version is current), tombstoning (to mark deletions explicitly), and compensating transactions (to reverse actions when out-of-date data causes inconsistencies).

While debugging asynchronous systems can be complex, the model offers enormous advantages in scalability and fault tolerance. Services remain independent, communication is decoupled, and the entire system can handle high loads without being limited by synchronous dependencies.

## Hybrid Data Sharing Models

In practice, most systems do not rely entirely on either synchronous or asynchronous communication. Instead, they combine both approaches to create a hybrid data sharing model.

This model aims to balance the strengths of each strategy while minimizing their weaknesses. Services use synchronous communication when they need the latest data or must confirm an operation in real time, and rely on asynchronous updates for background synchronization or less critical information.

Consider the example of a ride-sharing application.

The Ride service needs information about the driver. To operate efficiently, it might store a local copy of basic driver details such as the driver’s ID, name, and contact information. However, if the service needs additional data, such as the driver’s live rating, vehicle details, or current location, it makes a synchronous API call to the Driver service to retrieve the most recent information. This approach allows the Ride service to respond quickly to most requests while still maintaining access to up-to-date data when needed.

See the diagram below:

![](https://substackcdn.com/image/fetch/$s_!TgP3!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4b1e5df7-a99d-414f-af9e-fe9aeb80843a_2508x1604.png)

Hybrid models are powerful because they provide both speed and accuracy. Frequently used data is available locally, which improves performance and reduces dependency on other services. At the same time, asynchronous updates keep local copies from becoming too outdated. Services can refresh their data periodically or listen for update events from other services.

However, this approach also introduces complexity. Teams must decide which data to cache locally, how long to retain it, and when to refresh or invalidate it. Common strategies include caching layers, data snapshots, and event-triggered updates. Each choice affects system behavior in terms of freshness, performance, and storage cost.

When implemented carefully, hybrid data sharing models provide a practical middle ground. They allow systems to achieve low latency and resilience while ensuring that data across services remains reasonably consistent and up to date.

## Design Considerations and Trade-Offs

Choosing the right data-sharing strategy is not about finding a single perfect solution but about balancing trade-offs. Here are a few trade-offs to consider:

- **Consistency Models:** Synchronous communication supports strong consistency, where all services always see the most recent data. This is essential for critical operations such as payments or inventory updates. Asynchronous communication relies on eventual consistency, where services may temporarily hold slightly outdated data that becomes accurate after a short delay. This model is suitable for user-facing or analytical features such as product recommendations or dashboards. Between these two extremes are models like quorum-based consistency and causal consistency, which provide partial guarantees that balance accuracy and availability.
- **Performance and Latency:** Synchronous systems are easier to reason about but introduce blocking latency, especially as the number of inter-service calls grows. Asynchronous systems avoid this by decoupling communication, often using batching or caching to improve throughput. However, they require careful handling of delayed or duplicate messages.
- **Scalability and Fault Tolerance:** Asynchronous systems scale more easily since they buffer work and operate independently. Synchronous systems can struggle under heavy load due to coordination bottlenecks. Techniques like circuit breakers, retry policies, sagas, and dead-letter queues help improve resilience regardless of the model chosen.

## Summary

In this article, we look at data sharing in microservices in great detail. Here are the key learning points in brief:

- Modern systems use service-oriented or microservices architectures where each service manages its own data but still needs to share information to support business workflows.
- Data ownership ensures independence and flexibility, preventing cross-service schema dependencies and deployment coupling caused by shared databases.
- Sharing a data source tightly couples services and risks failures, while sharing data through APIs or events maintains autonomy and clear communication boundaries.
- Synchronous data sharing uses direct, blocking calls between services, offering immediate consistency but introducing latency and dependency on network reliability.
- The request-response model is simple and consistent but vulnerable to cascading failures, while gateway orchestration coordinates updates across services at the cost of scalability.
- Local caching or duplication can reduce synchronous latency but creates consistency challenges that often require asynchronous solutions.
- Asynchronous data sharing lets services communicate through events and message brokers, improving scalability and resilience while accepting temporary inconsistencies.
- Event-driven architectures, message brokers, event sourcing, and change data capture enable independent evolution and near real-time synchronization across services.
- Hybrid models combine synchronous and asynchronous patterns, using local caching and event-driven updates to balance data freshness and performance.
- The best data-sharing strategy depends on trade-offs between consistency, performance, and scalability, chosen to match the system’s goals and reliability requirements.