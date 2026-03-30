---
title: Fivetran donates its SQLMesh data transformation framework to the Linux Foundation
source: https://thenewstack.io/fivetran-donates-sqlmesh-lf/
author:
  - "[[Frederic Lardinois]]"
published: 2026-03-25
created: 2026-03-30
description: Fivetran, which also own SQLMesh competitor dbt, says it believes the data transformation layer should evolve as a community effort.
tags:
  - brain_spew
  - SQLMesh
---
Fivetran, which also own SQLMesh competitor dbt, says it believes the data transformation layer should evolve as a community effort.

![Featued image for: Fivetran donates its SQLMesh data transformation framework to the Linux Foundation](https://cdn.thenewstack.io/media/2026/03/8b29e7c0-getty-images-lzwee7oe3tm-unsplash-1024x725.jpg)

[Fivetran](https://www.fivetran.com/), the company best known for its data movement platform, on Wednesday announced that it would donate SQLMesh, its open source data transformation framework, to the Linux Foundation. The additional founding members supporting the vendor-neutral governance of the project include ATOMS (Uber founder Travis Kalanick’s CloudKitchens-to-robotics pivot), Benzinga, Harness, Infinite Lambda, Jump AI, and Minerva.

SQLMesh allows data teams to define, test, and deploy their SQL-based data transformations. The project came to Fivetran in September 2025, when the company acquired Tobiko Data, the startup founded by brothers (and former world-record speed-cubers) [Toby](https://en.wikipedia.org/wiki/Toby_Mao) and [Tyson](https://en.wikipedia.org/wiki/Tyson_Mao) Mao, and Iaroslav Zeigerman.

The fact that the company is donating SQLMesh on this date is surely no coincidence, given that the project [launched its SQLMesh-based cloud service into general availability exactly a year ago](https://thenewstack.io/tobiko-launches-its-sqlmesh-based-cloud-service-into-ga/).

## SQLMesh and dbt

The SQLMesh team never shied away from comparing SQLMesh to dbt, dbt Labs’ open source data transformation tool. On its GitHub page, SQLMesh describes itself as “more than just a dbt alternative.”

![](https://cdn.thenewstack.io/media/2026/03/8fca5e60-architecture_diagram-1024x459.png)

The main differentiators for SQLMesh are its use of virtual data environments to run dev, staging, and production without duplicating data, and its compile-time [SQLGlot](https://sqlglot.com/sqlglot.html) parser and optimizer, which enable significant performance gains.

The wrinkle to the story here is that Fivetran announced plans to merge with dbt Labs in October of 2025 (though the transaction hasn’t closed yet).

In mid-2025, dbt Labs had adopted the Elastic License for Fusion, the next-generation engine that powers dbt. This license keeps the source code open and primarily focuses on ensuring that other companies can’t offer a hosted version of Fusion on their platform. At the time, Toby Mao [criticized](https://www.tobikodata.com/blog/dbt-fusion-death-of-dbt-core) this move, arguing that “Analytics Engineers deserve a free, open, and continually evolving transformation platform.”

It’s hard not to see today’s move, in part, as a reaction to this licensing discussion, as Fivetran can now easily argue that it is supporting a fully open-source alternative to dbt and giving it to the community. Dbt core currently has 12,500 stars on GitHub, while SQLMesh has 3,000.

“Data infrastructure works best when its core components are open,” says Anjan Kundavaram, Chief Product Officer of Fivetran. “As analytics and AI workloads become more complex, organizations need the flexibility to choose the best technologies, control their costs, and adapt their architectures over time. SQLMesh reflects our belief that the transformation layer should evolve through open collaboration as part of a broader Open Data Infrastructure approach.”