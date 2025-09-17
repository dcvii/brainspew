---
title: "I'm Still Here! Let's Catch Up."
source: "https://materializedview.io/p/im-still-here-lets-catch-up?publication_id=2070040&post_id=171754493&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Chris]]"
published: 2025-08-27
created: 2025-08-27
description: "The latest on Designing Data-Intensive Applications, SlateDB, AI, Materialized View Capital, and forthcoming newsletter posts."
tags:
  - "clippings"
---
### The latest on Designing Data-Intensive Applications, SlateDB, AI, Materialized View Capital, and forthcoming newsletter posts.

My apologies for the lack of posts recently. I’ve been hard at work on a few things over the summer, which has left little time for this newsletter. I’m getting my bearings now. More posts are back on the docket. My first post—this one—will be a quick catch-up.

[Martin](https://martin.kleppmann.com/) and I have been working on [Designing Data-Intensive Applications](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/) ’s batch and streaming chapters for its second edition. The batch chapter has been published to Safari Online as an early release; it required a full rewrite. The streaming chapter is still a work-in-progress. [Kafka: The End of the Beginning](https://materializedview.io/p/kafka-end-of-beginning), my previous post on this newsletter, reflected on how stagnant the streaming ecosystem has been over the past 10-15 years. The updates to the streaming chapter reflect this; they’ll be more minimal. I do plan to add a section on [incremental view maintenance (IVM)](https://wiki.postgresql.org/wiki/Incremental_View_Maintenance), which I’ll base off of my IVM newsletter post.

Meanwhile, [SlateDB](https://slatedb.io/) work continues apace. [Li Yazhou](https://flaneur2020.github.io/) has [added](https://github.com/slatedb/slatedb/issues/489) [serializable snapshot isolation (SSI)](https://wiki.postgresql.org/wiki/SSI) support. He’s in the process of [adding transactions](https://github.com/slatedb/slatedb/issues/816). The RFC is [here](https://github.com/slatedb/slatedb/blob/main/rfcs/0011-transaction.md) if you’d like to learn more. We also have both [Python](https://github.com/slatedb/slatedb/tree/main/slatedb-py) and [Go](https://github.com/slatedb/slatedb/tree/main/slatedb-go) bindings now. I have been focusing on refactoring and stability; I added a basic [deterministic simulation tester](https://github.com/slatedb/slatedb/tree/main/slatedb-dst) recently. [Sujeet Sawala](https://www.linkedin.com/in/sujeet-sawala-8b70a9144) is [working on an RFC](https://github.com/slatedb/slatedb/pull/695) to persist compaction progress. We’re starting to see some [real adoption](https://github.com/slatedb/slatedb?tab=readme-ov-file#adopters). More projects are launching in the near future, too.

The biggest news with SlateDB, though, is [Pierre Barre](https://github.com/Barre) ’s [ZeroFS](https://www.zerofs.net/) project. ZeroFS provides [network filesystem (NFS)](https://www.zerofs.net/nfs-access), [network block device (NBD)](https://www.zerofs.net/nbd-devices), and [Plan 9 Filesystem Protocol (9P)](https://www.zerofs.net/9p-access) implementations on top of SlateDB. The filesystem is also [POSIX compliant](https://github.com/Barre/ZeroFS/actions/workflows/pjdfstest.yml) —no small feat. On the performance front, check out Pierre’s [AWS EFS](https://www.zerofs.net/zerofs-vs-aws-efs), [AWS Mountpoint-S3](https://www.zerofs.net/zerofs-vs-mountpoint-s3), [JuiceFS](https://www.zerofs.net/zerofs-vs-juicefs), and [Azure Files](https://www.zerofs.net/zerofs-vs-azure-files) benchmarks.

ZeroFS is a young project, but I’m very excited about it. SlateDB’s [branching and forking](https://github.com/slatedb/slatedb/blob/main/rfcs/0004-checkpoints.md) features mean ZeroFS will be able to provide zero-copy filesystem forking—an important feature for AI and many other use cases.

Speaking of AI, I’m still getting my bearings with it. I’ve been reluctant to post about the topic because I don’t feel I’m an expert in the subject. (Then again, it’s so new that very few are.) I use coding agents constantly, though. As a user, I’ve begun to form some opinions around [model context protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro), agent adoption in the enterprise, and its impact on developer tooling and infrastructure. I plan to write more on AI in the near future.

I’ve continued to invest in startups throughout the summer. [Materialized View Capital](https://materializedview.capital/) is now 75% deployed and will be fully deployed ~18 months from its inception. One usually targets a 3 year deployment. An 18 month deployment for a smaller fund like MVC is not unheard of. I’m quite pleased with our portfolio, which includes [Bauplan](https://bauplanlabs.com/), [Dosu](https://dosu.dev/), [Fiveonefour](https://www.fiveonefour.com/), [Gauge](https://withgauge.com/), [Loophole Labs](https://loopholelabs.io/), [ParadeDB](https://paradedb.com/), [Reboot](https://reboot.dev/), [Signadot](https://signadot.com/), [Spiral](https://spiraldb.com/), [Tigris](https://tigrisdata.com/), [Tensorlake](https://tensorlake.ai/), and [many more](https://materializedview.capital/).

Starting a fund has been rewarding. I plan to take a few months off after the fund is deployed. I’d like to evaluate what’s next for my startup investing adventure.

And that pretty much sums it up! I’m sure I’ve missed a few things. Let me know if there’s something specific that’s worth noting. In the meantime, expect an interview next week with [Xorq](https://xorq.dev/) ’s﹩ CEO, [Hussain Sultan](https://www.linkedin.com/in/hussainsultan/).

---

#### Book

Support this newsletter by purchasing [The Missing README: A Guide for the New Software Engineer](https://www.amazon.com/Missing-README-Guide-Software-Engineer/dp/1718501838) for yourself or gifting it to someone.

![](https://substackcdn.com/image/fetch/$s_!CI0B!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fde442631-41a6-4119-a99a-62957cd53edb_870x978.png)

---

#### Disclaimer

I occasionally invest in infrastructure startups. Companies that I’ve invested in are marked with a ﹩ in this newsletter. See my [LinkedIn profile](https://www.linkedin.com/in/riccomini/) and [Materialized View Capital](https://materializedview.capital/) for a complete list.