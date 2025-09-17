---
title: "Architecture : The cheat sheet"
source: "https://lab.scub.net/architecture-patterns-the-cheat-sheet-e8b5386f4b4b"
author:
  - "[[Pier-Jean Malandrino]]"
published: 2024-01-29
created: 2025-04-08
description: "This paper presents a concise summary of various software architecture patterns, models, philosophies and strategies offering insights into their unique characteristics, applications, and impacts on…"
tags:
  - "clippings"
---
This paper presents a concise summary of various software architecture patterns, models, philosophies and strategies offering insights into their unique characteristics, applications, and impacts on software design. These patterns represent key approaches and strategies in modern software engineering, each addressing specific requirements and challenges. The objective is to provide a high-level understanding and a classification of these patterns, aiding architects and developers in selecting the most suitable approach for their specific needs.

Software architecture patterns are fundamental guidelines used to address complex architectural challenges in software development. They provide structured solutions to recurring problems, ensuring efficiency, scalability, and maintainability.

> ==It is not an exhaustive list, but it will be updated each time I publish new papers concerning architecture patterns.==

## Architecture Patterns

## Backend For Frontend (BFF)

Involves creating specific backend services tailored to the requirements of individual frontend applications, optimizing communication and data delivery.

**Focus:** Creating backend services tailored to specific frontend applications.

**Benefits:** Optimizes communication and data delivery.

**Trade-offs:** Can lead to duplicated logic, requires additional maintenance.

Architecture Patterns: Backend For Frontend (BFF) Pattern

### What is BFF?

lab.scub.net

[View original](https://lab.scub.net/backend-for-frontend-bff-pattern-57de57683264?source=post_page-----e8b5386f4b4b---------------------------------------)

## Publish/Subscribe Pattern

**Focus:** Decoupling producers and consumers in messaging systems.

**Benefits:** Enhances scalability and system flexibility, supports asynchronous communication.

**Trade-offs:** Increases message management complexity, depends on broker reliability.

Architecture Patterns: Publish/Subscribe

### What is Publish/Subscribe?

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-publish-subscribe-1bbd810e52fb?source=post_page-----e8b5386f4b4b---------------------------------------)

## Sidecar Pattern

**Focus:** Enhancing or extending the functionality of a primary application.

**Benefits:** Isolates and modularizes functionalities, easier maintenance.

**Trade-offs:** Can increase system complexity, additional resource consumption.

Architecture Patterns: Sidecar

### What is the Sidecar Pattern?

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-sidecar-041801104b99?source=post_page-----e8b5386f4b4b---------------------------------------)

## Data-Driven Testing

**Focus:** Enhancing testing processes by using data-driven methodologies.

**Benefits:** Increases test coverage, improves efficiency.

**Trade-offs:** Requires thorough data management, potential for data-related errors.

Architecture Patterns: Data Driven Testing

### What is Data Driven Testing?

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-data-driven-testing-95f437cfe2cb?source=post_page-----e8b5386f4b4b---------------------------------------)

## Circuit Breaker

Provides a way to handle failures gracefully, preventing a cascade of failures in distributed systems. It acts like an electrical circuit breaker, stopping the flow of requests to a failing service to allow recovery.

**Focus:** Handling failures in distributed systems.

**Benefits:** Prevents cascading failures, allowing services time to recover.

**Trade-offs:** Requires careful threshold settings to avoid false

Architecture Patterns: The Circuit-Breaker

### What is “Circuit Breaker”?

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-the-circuit-breaker-8f79280771f1?source=post_page-----e8b5386f4b4b---------------------------------------)

## API Gateway

Acts as an intermediary layer that manages and routes requests from clients to various microservices, providing a unified interface, security, and other cross-cutting concerns.

**Focus:** Managing requests to microservices.

**Benefits:** Provides a unified interface, enhances security.

**Trade-offs:** Potential single point of failure, increased complexity.

Architecture Patterns: API Gateway

### What is “API Gateway”

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-api-gateway-4426edb64649?source=post_page-----e8b5386f4b4b---------------------------------------)

## Command Query Responsibility Segregation (CQRS)

Separates read and write operations into distinct models, optimizing performance and scalability, especially in complex and high-demand environments.

**Focus:** Separating read and write operations.

**Benefits:** Optimizes performance and scalability.

**Trade-offs:** Adds complexity, may lead to eventual consistency issues.

Architecture Patterns: Command Query Responsibility Segregation (CQRS)

### What is CQRS?

lab.scub.net

[View original](https://lab.scub.net/command-query-responsibility-segregation-cqrs-93e35d1929ec?source=post_page-----e8b5386f4b4b---------------------------------------)

## Outbox Pattern

Addresses the challenge of ensuring reliable message delivery in distributed systems, particularly in microservices architectures, by temporarily storing messages before forwarding them.

**Focus:** Ensuring reliable message delivery in distributed systems.

**Benefits:** Prevents data loss during transmission failures.

**Trade-offs:** Adds implementation complexity, may introduce latency.

Architecture Patterns: The Outbox Pattern ( Beyond Microservices)

### In the intricate tapestry of distributed systems, particularly within the microservices architecture, the challenges of…

lab.scub.net

[View original](https://lab.scub.net/the-outbox-pattern-beyond-microservices-4ac37a1c3a86?source=post_page-----e8b5386f4b4b---------------------------------------)

## Multi-tenancy

Discusses implementing a multi-tenant system using Keycloak for authentication, and Angular and Springboot for frontend and backend development, respectively.

**Focus:** Implementing a multi-tenant system using specific technologies.

**Benefits:** Efficient authentication management in SaaS applications.

**Trade-offs:** Complex setup, requiring integration of multiple technologies.

Architecture Patterns: Multi-tenancy with Keycloak, Angular and Springboot

### Multi-tenancy is a critical aspect of contemporary software architecture. It assists in overcoming significant…

lab.scub.net

[View original](https://lab.scub.net/multi-tenancy-with-keycloak-angular-and-springboot-487c38943979?source=post_page-----e8b5386f4b4b---------------------------------------)

## Architecture Anti-Patterns

Highlights common pitfalls and ‘anti-patterns’ in software architecture, offering insights into what to avoid for maintaining healthy and efficient software systems.

Architecture Anti-Patterns: The DARK side of the Architect

### Amid the realm of logic and structured thought, architects, much like the mythical creatures of old, harbor a shadowy…

lab.scub.net

[View original](https://lab.scub.net/architecture-anti-patterns-the-dark-side-of-the-architect-d9265b52d997?source=post_page-----e8b5386f4b4b---------------------------------------)

## Architecture tools

This section describes models, philosophies, and strategies used to enhance your practice of architecture. They cannot be considered as patterns but are still very useful for building great systems.

## C4 Model

Focuses on providing a comprehensive visualization of software architecture, breaking it down into four levels: Context, Containers, Components, and Code. It aids in understanding and communicating the software structure at different abstraction levels.

**Focus:** Visualization of software architecture across four levels.

**Benefits:** Enhances understanding and communication of software structure.

**Trade-offs:** May be overly complex for smaller systems.

Architecture Modeling: C4 Model

### What is the C4 Model?

lab.scub.net

[View original](https://lab.scub.net/architecture-modeling-c4-model-bd050c13964c?source=post_page-----e8b5386f4b4b---------------------------------------)

## Domain-Driven Design (DDD)

Centers on aligning software design closely with domain complexities, using a model-driven approach. It emphasizes collaboration between technical and domain experts to create a common language and shared understanding.

**Focus:** Aligning software design with domain complexities.

**Benefits:** Facilitates collaboration and creates a shared language.

**Trade-offs:** Requires deep understanding of the domain, potentially complex.

Architecture Approach: Domain-Driven Design (DDD)

### What is Domain-Driven Design (DDD)?

lab.scub.net

[View original](https://lab.scub.net/architecture-approach-domain-driven-design-ddd-2423fbbea375?source=post_page-----e8b5386f4b4b---------------------------------------)

## Strangler Pattern

Aims at gradually replacing parts of a legacy system, allowing for incremental updates and smooth migration to new technologies without disrupting existing functionalities.

**Focus:** Gradual replacement of legacy systems.

**Benefits:** Allows incremental updates without disrupting existing functionalities.

**Trade-offs:** Can be slow and resource-intensive.

Architecture Patterns: Strangler Pattern

### What is Strangler Pattern?

lab.scub.net

[View original](https://lab.scub.net/architecture-patterns-strangler-pattern-a33927ee8f64?source=post_page-----e8b5386f4b4b---------------------------------------)

*I am the CTO and Head of an architectural unit in a digital company. I participate in the development of technological strategy, design solutions, and lead R&D projects.*

*Thank you for reading! If you enjoyed this article, please feel free to 👏 and help others find it. Please do not hesitate to share your thoughts in the comments section below.*

## Scub Lab

*Thank you for being a part of our community! Before you go:*

- *Be sure to* ***clap*** *and* ***follow*** *the writer! 👏*
- *You can find even more content at* [***lab.scub.net***](https://lab.scub.net/) ***🚀***
- *Sign up for our* [***free weekly newsletter***](https://medium.com/scub-lab/newsletters/scub-lab)*. 🗞️*
- *Follow us on* [***Twitter***](https://twitter.com/scub_france) ***(X*** *),* [***LinkedIn***](https://www.linkedin.com/company/scub/mycompany/)*, and our* [***site web***](https://www.scub.net/)***.***