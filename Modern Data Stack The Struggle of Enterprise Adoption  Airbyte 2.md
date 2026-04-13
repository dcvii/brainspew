---
title: "Modern Data Stack: The Struggle of Enterprise Adoption | Airbyte"
source: "https://airbyte.com/blog/modern-data-stack-struggle-of-enterprise-adoption"
author:
  - "[[Simon Späti]]"
  - "[[Henry Mattingly]]"
  - "[[Brian Leonard]]"
  - "[[Jim Kutz]]"
published:
created: 2026-02-26
description: "The Modern Data Stack has powerful tools for building enterprise data stacks, yet mid- to large-sized enterprises haven't adopted them. Exploring the enterprise data landscape and tools enterprises use today, what the opportunities are for using the open-source, free-of-charge data stack, and its downsides."
---
[![Modern Data Stack: The Struggle of Enterprise Adoption](https://cdn.prod.website-files.com/687b2d16145b3601a227c560/68ce828e7a6cbec1fed4358b_63bbe8be15cbc74fd1a4ec7f_mds-enterprise-struggle-feature.webp)](https://airbyte.com/blog/#)

## Opportunities for Enterprises with the MDS Stack

Now let's discuss opportunities that the MDS stack delivers for enterprises.

- **Getting started**: Think about all the gains you can realize from existing solutions that could allow non-data engineers to start getting insight in a few hours or days.
- **Data privacy & legal**: MDS lowers the legal risks, giving more flexibility on where to run with open code. This means it’s easier to comply with changing data regulations.
- **Modularity & extensibility**: You can choose dedicated specialized tools for each use case without cost.
- **Technological advantage**: You are using the latest technology and gaining benefits over competitors who remain less data-driven.

It is strongly recommended to have highly technical people who use [DevOps](https://glossary.airbyte.com/term/dev-ops/) to set up the Modern Data Stack, especially on a scale or in an enterprise where many use it with something like [Kubernetes](https://glossary.airbyte.com/term/kubernetes/).

#### Modularity: Supporting the Data Engineering Lifecycle

Whether you choose an enterprise data platform or the open-source route with the Modern Data Stack, your selection must solve the [Data Engineering Lifecycle](https://glossary.airbyte.com/term/data-engineering-lifecycle). Each of these blocks needs to be implemented in one way or another to output insights valuable to the data consumers.

![The data engineering lifecycle, inspired by Fundamentals of Data Engineering](https://cdn.prod.website-files.com/687b2d16145b3601a227c560/68ce828e7a6cbec1fed43586_63bbe94a9d70bb1070efa434_data-integration-ELT.webp)

The data engineering lifecycle, inspired by Fundamentals of Data Engineering

### When not to use an MDS Stack

The advantage of modularity is undoubtedly also a disadvantage to the point that failures can pop up at each integration of another tool. Always keep in mind this quote from [Data Platforms: The Past](https://medium.com/alexandre-beauvois/modern-data-stack-as-a-service-1-3-1a1813c38633):

> Integrating good tools doesn't mean you'll get a good stack and expected results. It's still a complex thing.

On the other hand, if you choose wisely, you can end up much better than a custom monolith that lost its maintainer.

**Costs** are another consideration, but can be hard to predict. As you run many independent tools, it's harder to forecast the costs and to balance than to have one tool solution that does it for you.

The core of each MDS tool needs to be built for **enterprise scale** and is added as an afterthought. You need to prove the solution first before you scale. I'm confident that the scale can't be fixed, but that is something to keep in mind when testing the MDS tool.

**Adopting** MDS is slower than just plugging a credit card into an enterprise data platform and getting started. With such platforms, you do not need to consider deploying, upgrading, security, or other concerns. These things are hard. Therefore, you will need a dedicated data team and DevOps people.

In the end, it's always a **tradeoff** between fully on-premise and hosting all your tools yourself vs. everything managed on SaaS:

![](https://cdn.prod.website-files.com/687b2d16145b3601a227c560/68ce828e7a6cbec1fed43582_63bbe99f2801840993377fe0_mdsaas.webp)

From Data Platforms: The Past - The Evolution of Data Platforms

## The Core Open (Modern) Data Stack

There are always more tools you can add to your Modern Data Stack! You can use the data engineering lifecycle as a reference for the building blocks to add. But in general, the core four you need are data ingestion, transformation, orchestration, and analytics.

Unfortunately, the fast phase will continue for a while. Sure, there are thousands of tools, and it's impossible to keep updated with them, but you only need a few. Take Airbyte, dbt, a visualization tool, and Dagster, and you’ll be up and running within hours—with a battle-tested, open-source high-impact tool at your fingertips. I illustrated these tools and how to set them up in Part I: [The Open Data Stack Distilled into Four Core Tools](https://airbyte.com/blog/modern-open-data-stack-four-core-tools). Check it out to get started with the analytics journey today.

Another consideration is naming. Even though the term Modern Data Stack hasn't spread much, there is already the dislike of "modern," which has no tangible value. Alternative names for "Modern Data Stack" that I saw are [new generation open-source data stack](https://blog.devgenius.io/modern-data-stack-demo-5d75dcdfba50) (ngods), DataStack 2.0, and the Boring Data Stack. While starting an open-source [Project](https://github.com/airbytehq/open-data-stack/), I found [Open Data Stack](https://glossary.airbyte.com/term/open-data-stack/) to be the perfect nomenclature, emphasizing the **value open-source** tools provide. “Open” also speaks to **open standards** —desperately needed in data engineering.

No matter the name, the essence of open source, extensible, and free-to-use will not change.

📏 **GitHub Project**: Check out the [open-data-stack](https://github.com/airbytehq/open-data-stack/) example project we just started (we’ll be adding to it as part of this [series](https://airbyte.com/blog/building-airbytes-data-stack)).