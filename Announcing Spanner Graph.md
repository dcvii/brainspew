---
title: "Announcing Spanner Graph"
source: "https://cloud.google.com/blog/products/databases/announcing-spanner-graph"
author:
  - "[[Google Cloud Blog]]"
published:
created: 2025-04-23
description: "With Spanner Graph, you can analyze interconnected data using Google Cloud’s always-on, globally consistent, and virtually unlimited-scale database."
tags:
  - "clippings"
---
Databases

## Introducing Spanner Graph: Graph databases reimagined

August 1, 2024

##### Bei Li

Sr. Staff Software Engineer

##### Chris Taylor

Google Fellow

Enterprises are looking for better ways to extract insights from their connected data, so they can build more intelligent applications, and using a graph database can be a powerful — albeit complex — way to do that. Today, we are thrilled to announce Spanner Graph, a groundbreaking offering that unites purpose-built graph database capabilities with Spanner, our always-on, globally consistent, and virtually unlimited-scale database.

Graphs provide a natural mechanism for representing relationships in data, making them well-suited for analyzing interconnected data, uncovering hidden patterns, and powering applications that rely on understanding connections. Graphs are used for a variety of use-cases such as fraud detection, recommendation engines, network security, knowledge graphs, customer 360, route planning, data cataloging, and data lineage tracing.

![https://storage.googleapis.com/gweb-cloudblog-publish/images/Fig1.max-1000x1000.png](https://storage.googleapis.com/gweb-cloudblog-publish/images/Fig1.max-1000x1000.png)

However, adopting standalone graph databases to address these use cases often presents the following challenges:

- **Data fragmentation and operational overhead:** Maintaining separate graph databases often leads to data silos, increased complexity, and inconsistencies between data copies, which in turn impedes efficient analysis and decision-making.
- **Scalability and availability bottlenecks:** Many standalone graph databases struggle to meet the scalability and availability demands of mission-critical applications, especially as data volumes and complexity grow, hindering business growth.
- **Ecosystem friction and skill gaps:** Organizations have substantial investments in SQL expertise and infrastructure, which can make it harder to adopt a completely new graph paradigm. To do so, they need additional resources and training, which may divert resources away from critical business needs.

Spanner Graph reimagines graph data management, introducing a unified database that seamlessly integrates graph, relational, search, and AI capabilities with virtually unlimited scalability. With Spanner Graph, you get:

- **Native graph experience:** The ISO Graph Query Language (GQL) interface offers an intuitive and concise way to match patterns and traverse relationships, based on open standards.
- **Unified relational and graph models**: Full interoperability between GQL and SQL breaks down data silos, empowering developers to choose the optimal tool for each query. Tight integration of graph and table data helps remove operational overhead and the need for complex and costly data movement.
- **Built-in search capabilities:** Rich vector and full-text search capabilities enable efficient retrieval of graph data using semantic meaning and keywords.
- **Industry-leading scalability, availability, and consistency:** Spanner's renowned scalability, availability, and consistency provide data foundations that you can trust.
- **AI-powered insights:** Deep integration with Vertex AI unlocks a powerful suite of AI models directly within Spanner Graph, accelerating AI workflows.

“At Credit Karma, ensuring the safety of our 130+ million members’ data is our top priority. To combat and eliminate fraud across our systems, we’ve partnered with Google to enhance our fraud mitigation capabilities by implementing Spanner Graph Database. This advanced platform capability allows us to detect potential fraud threats before they happen. With Spanner Graph, we effectively detect and prevent fraudulent transactions, account takeovers, and other fraudulent activities.” - Engineering team, Credit Karma

### Let’s dive deeper into what makes Spanner Graph unique

**Spanner Graph offers a familiar and future-proof graph database experience.** Spanner Graph supports ISO GQL, the new international standard for graph databases. It offers an intuitive and concise way to match patterns, traverse relationships, and filter results in graph data, making it easier to uncover hidden relationships and insights.

The following example uses GQL to implement a simplified collaborative filtering algorithm. This algorithm suggests products by identifying items frequently purchased alongside a specific product, “TrailMaster All-Terrain Boots”, and makes recommendations based on shared user preferences:

```
GRAPH RetailGraph
```

```
MATCH (:Product {name: "TrailMaster All-Terrain Boots"})<-[:Purchase]-
```

```
(:User)-[:Purchase]->(alsoBought:Product)
```

```
RETURN DISTINCT alsoBought.name;
```

**Spanner Graph bridges the relational and graph worlds**. Spanner Graph combines the well-established capabilities from SQL and the expressiveness of graph pattern matching from GQL, so you can leverage the strengths of both paradigms within a single, unified database.

The following code example first leverages a graph query to generate product recommendations, same as the code example above. The example code then seamlessly joins with table data to retrieve corresponding price histories, resulting in a comprehensive view of recommended items and their pricing trends:

```
SELECT priceHistory.*
```

```
FROM GRAPH_TABLE(
```

```
RetailGraph
```

```
MATCH (:Product {name: "TrailMaster All-Terrain Boots"})<-[:Purchase]-
```

```
(:User)-[:Purchase]->(alsoBought:Product)
```

```
RETURN DISTINCT alsoBought.productId
```

```
) AS alsoBought
```

```
LEFT JOIN ProductPriceHistory priceHistory
```

```
ON alsoBought.productId = priceHistory.productId;
```

In addition, tables can be declaratively mapped to graphs without migrating the data, which brings the power of graph to tabular datasets. With this capability, you can late-bind (i.e., postpone) data model choices and use the best query language for each job to be done.

The following code example shows how to map tables `User`, `Product`, and `Purchase` to the graph `RetailGraph` declaratively using the schema. The schema encodes semantic information regarding entities and how they relate to each other. The generated graph is accessible using GQL, which provides a flexible and intuitive way to query your data. Additionally, you retain the ability to directly access the underlying tables using SQL. This dual-access approach lets you choose the optimal data model — graph or tabular — depending on the task or analysis you're performing.

x

```
CREATE OR REPLACE PROPERTY GRAPH RetailGraph
```

```
NODE TABLES (User, Product)
```

```
EDGE TABLES (
```

```
Purchase
```

```
SOURCE KEY (userId) REFERENCES User
```

```
DESTINATION KEY (productId) REFERENCES Product
```

```
);
```

```
​
```

```
-- Now we can query RetailGraph!
```

```
GRAPH RetailGraph MATCH … RETURN …;
```

**Spanner Graph works seamlessly with vector search and full-text search.** The combination lets you traverse relationships within graph structures using GQL, while simultaneously leveraging search to find graph contents. Specifically, you can leverage vector search to discover nodes or edges based on semantic meaning, or use full-text search to pinpoint nodes or edges that contain specific keywords. From these starting points, you can then seamlessly explore the rest of the graph using GQL. By integrating these complementary techniques, this unified capability lets you uncover hidden connections, patterns, and insights that would be difficult to discover using any single method.

The following code example employs a two-step process: first, it utilizes full-text search to efficiently retrieve products related to “waterproof hiking boots”, and then it applies GQL to analyze the search results and generate product recommendations.

```
GRAPH RetailGraph
```

```
MATCH (product)<-[:Purchase]-(otherUser:User)-[:Purchase]->(alsoBought:Product)
```

```
WHERE SEARCH(product.descriptionToken, "waterproof hiking boots")
```

```
RETURN DISTINCT alsoBought.name;
```

**Spanner Graph scales beyond trillions of edges while offering industry-leading availability and consistency.** Spanner Graph inherits virtually unlimited scalability, industry-leading availability, and global consistency from Spanner, making it a great solution for even the most mission-critical graph applications. In particular, Spanner’s transparent sharding can scale elastically to very large data sets and can use massively parallel query processing without any intervention on your part.

**Spanner Graph accelerates your AI workflows through deep integration with Vertex AI.** Spanner Graph is deeply integrated with [Vertex AI](https://cloud.google.com/vertex-ai), Google Cloud’s fully managed, unified AI development platform. You can directly access Vertex AI's extensive suite of predictive and generative models through the Spanner Graph schema and query, streamlining your AI workflow. For example, you can generate text embeddings for graph nodes and edges using LLMs, enriching your graph with the results, and then you can use vector search to retrieve from your graph in the semantic space.

### With Spanner Graph, you can build more intelligent applications

Spanner Graph seamlessly integrates graph, relational, search, and AI capabilities with virtually unlimited scalability, opening up a realm of possibilities:

- **Product recommendations**: Spanner Graph models the complex relationships between users, products, and preferences to build a knowledge graph rich with context. Combining fast graph traversal with full-text search, you can make product recommendations based on user queries, purchase history, and preferences, as well as similarities to other users.
- **Financial fraud detection**: Spanner Graph's natural representation of financial entities like accounts, transactions, and individuals makes it easier to identify suspicious connections. Vector search reveals similar patterns and anomalies in the embedding space. By combining these technologies, financial institutions can quickly and accurately identify potential threats, minimizing financial losses.
- **Social networks**: Spanner Graph intuitively models individuals, groups, interests, and interactions even in the largest social networks. It enables efficient discovery of patterns such as mutual friends, shared interests, or overlapping group memberships for personalized recommendations. The integrated full-text search lets users use natural language queries to easily find people, groups, posts, or specific topics.
- **Gaming**: Game worlds can be naturally represented as entities like players, characters, items, and locations, and the relationships between them. Spanner Graph enables efficient traversal of connections, which is essential for game mechanics like pathfinding, inventory management, and social interactions. Additionally, Spanner Graph's scalability and global consistency guarantees a seamless and equitable experience for all players, even during peak usage.
- **Network security**: Understanding the interdependencies between devices, users, and events across time is essential for identifying patterns and anomalies. With Spanner Graph relational and graph interoperability, security professionals can use graph capabilities to trace the origins of attacks, assess the impact of security breaches, and correlate these findings with temporal trends for proactive threat detection and mitigation.
- **GraphRAG**: Spanner Graph takes Retrieval Augmented Generation (RAG) to the n ext level by grounding foundation models with a knowledge graph. In addition, the fusion of graph and tabular data in Spanner Graph enriches your AI applications with contextual information beyond what either format could represent alone. With unmatched scalability, it can accommodate even the largest knowledge graphs. Built-in vector search and Vertex AI integration streamline your GenAI workflow s.

### Get started with Spanner Graph today

Learn more about Spanner Graph benefits and use cases [here](https://cloud.google.com/products/spanner/graph). Use this [quick setup guide](https://cloud.google.com/spanner/docs/graph/set-up) to get started with [Spanner Graph capabilities](https://cloud.google.com/spanner/docs/graph/overview). If you have questions along the way, tag "google-spanner-graph" in community forums or email [spanner-graph-feedback@google.com](https://cloud.google.com/blog/products/databases/).

##### Related articles

[![https://storage.googleapis.com/gweb-cloudblog-publish/images/10_-_Databases.max-700x700.jpg](https://storage.googleapis.com/gweb-cloudblog-publish/images/10_-_Databases.max-700x700.jpg)](https://cloud.google.com/blog/products/databases/google-cloud-database-and-langchain-integrations-support-go-java-and-javascript)

[Databases](https://cloud.google.com/blog/products/databases/google-cloud-database-and-langchain-integrations-support-go-java-and-javascript)

Google Cloud Database and LangChain integrations now support Go, Java, and JavaScript

By Hamsa Buvaraghan • 7-minute read

[View original](https://cloud.google.com/blog/products/databases/google-cloud-database-and-langchain-integrations-support-go-java-and-javascript)

[![https://storage.googleapis.com/gweb-cloudblog-publish/images/01_-_AI__Machine_Learning_H1ZyZG8.max-700x700.jpg](https://storage.googleapis.com/gweb-cloudblog-publish/images/01_-_AI__Machine_Learning_H1ZyZG8.max-700x700.jpg)](https://cloud.google.com/blog/products/ai-machine-learning/mcp-toolbox-for-databases-now-supports-model-context-protocol)

[AI & Machine Learning](https://cloud.google.com/blog/products/ai-machine-learning/mcp-toolbox-for-databases-now-supports-model-context-protocol)

MCP Toolbox for Databases: Simplify AI Agent Access to Enterprise Data

By Hamsa Buvaraghan • 5-minute read

[View original](https://cloud.google.com/blog/products/ai-machine-learning/mcp-toolbox-for-databases-now-supports-model-context-protocol)

[![https://storage.googleapis.com/gweb-cloudblog-publish/images/10_-_Databases.max-700x700.jpg](https://storage.googleapis.com/gweb-cloudblog-publish/images/10_-_Databases.max-700x700.jpg)](https://cloud.google.com/blog/products/databases/announcing-general-availability-of-memorystore-for-valkey)

[Databases](https://cloud.google.com/blog/products/databases/announcing-general-availability-of-memorystore-for-valkey)

Supercharge your data the open-source way: Memorystore for Valkey is now GA

By Ankit Sud • 6-minute read

[View original](https://cloud.google.com/blog/products/databases/announcing-general-availability-of-memorystore-for-valkey)

[![https://storage.googleapis.com/gweb-cloudblog-publish/images/AlloyDB.max-700x700.jpg](https://storage.googleapis.com/gweb-cloudblog-publish/images/AlloyDB.max-700x700.jpg)](https://cloud.google.com/blog/products/databases/alloydb-ai-drives-innovation-from-the-database)

[Databases](https://cloud.google.com/blog/products/databases/alloydb-ai-drives-innovation-from-the-database)

AlloyDB AI drives innovation for application developers

By Sanjay Mishra • 7-minute read

[View original](https://cloud.google.com/blog/products/databases/alloydb-ai-drives-innovation-from-the-database)