---
title: "DeepSeek brings disruption to AI-optimized parallel file systems, releases powerful new open-source Fire-Flyer File System"
source: "https://www.tomshardware.com/pc-components/storage/deepseek-releases-powerful-new-parallel-file-system-fire-flyer-fire-system-made-open-source"
author:
  - "[[Tom's Hardware]]"
published: 2025-03-01
created: 2025-03-11
description: "DeepSeek's 3FS file system is now open-source and is a no-brainer for AI-HPC model training, boosting efficiency and training more data-driven models."
tags:
  - "clippings"
---
![Google](https://cdn.mos.cms.futurecdn.net/tRgspGN4ycFeiFrnRn3dbA-1200-80.jpg)

(Image credit: Google)

DeepSeek AI has made its Fire-Flyer Fire System (3FS) parallel file system [fully open-source this week](https://x.com/deepseek_ai/status/1895279409185390655), as part of its Open Source Week event. The [disruptive AI company](https://www.tomshardware.com/tech-industry/artificial-intelligence/nvidia-loses-usd589-billion-in-market-cap-broad-stock-plunge-triggered-by-deepseek-ai-release) from China brags that 3FS can hit 7.3 TB/s aggregate read throughput in its own server data clusters, where DeepSeek has been using 3FS to organize its servers since at least 2019.

3FS is a Linux-based parallel file system designed for use in AI-HPC operations, where many data storage servers are being constantly accessed by GPU nodes for training LLMs. 3FS is unique from other file systems thanks largely to its almost singular prioritization of random read speeds above all else, and almost completely ignoring read caching.

When training AI models, compute units need to access random training data constantly, and reading this data is a one-time-only process. Therefore, a read cache is nearly useless and is largely done away with by 3FS. In fact, using the read cache when training LLMs may be potentially harmful; as LLMs are basically just super-tuned inference machines, reading the same data in the same order repeatedly has the potential to link completely different data as a set to the language model.

The team responsible for operating one of DeepSeek's deep learning clusters, Fire-Flyer 2, published [this paper](https://arxiv.org/html/2408.14158v2) last August outlining using 3FS in the custom-built system. In Fire-Flyer 2, DeepSeek utilized 180 storage nodes, each loaded with 16 16TB SSDs and two 200Gbps NUCs. These nodes served 10,000 PCIe Nvidia A100 GPUs, built out in much cheaper servers than Nvidia's proprietary [DGX-A100](https://www.tomshardware.com/news/amd-unveils-nvidia-dgx-a100-specs) products.

Across the whole array, DeepSeek claims it benchmarked 3FS's performance at 6.6 TB/s, while also running training tasks in the background that added an additional 1.4TB/s of read throughput. In comparison, competitor file system Ceph only reached speeds of 1.1 TB/s read throughput (on a server with 68 nodes, loaded with 10 16TB SSDs and 2 x 100 Gbps networking) for the first time [in early 2024](https://ceph.io/en/news/blog/2024/ceph-a-journey-to-1tibps/).

3FS was credited as a crucial part of DeepSeek's software stack for training DeepSeek AI in the above paper, as tested on the Fire-Flyer 2 HPC solution that achieved 80% of the performance of Nvidia's DGX-A100 server solution for 50% of the price and 60% of the power draw.

Those curious about trying out the Fire-Flyer File System and its random-read-forward style for AI-HPC solutions can find the full download on DeepSeek's [Github page](https://github.com/deepseek-ai/3FS). We'd be surprised if this new open-source system does not become a hit for enthusiasts and enterprise AI-HPC users alike, though it may have to overcome some level of anti-Chinese tech fear to hit blockbuster status.

## Stay On the Cutting Edge: Get the Tom's Hardware Newsletter

Get Tom's Hardware's best news and in-depth reviews, straight to your inbox.

TOPICS

More about storage

 [![Seagate Exos X20 20TB hard drive](https://cdn.mos.cms.futurecdn.net/RTud8WtjKvRL3cX9pdXmMi-840-80.jpg)

Seagate hard drive controversy persists as scammers discover methods to alter reliability metrics](https://www.tomshardware.com/pc-components/hdds/seagate-hard-drive-controversy-persists-as-scammers-discover-methods-to-alter-reliability-metrics) [![Astera Labs testbench holding Micron&#039;s PCIe 6.0 SSDs.](https://cdn.mos.cms.futurecdn.net/P3QmEr3sF2BF4YwywcCNDD-840-80.png)

Micron shows off world's fastest PCIe 6.0 SSD, hitting 27 GB/s speeds — Astera Labs PCIe 6.0 switch enables impressive sequential reads](https://www.tomshardware.com/pc-components/ssds/micron-shows-off-worlds-fastest-pcie-6-0-ssd-hitting-27-gb-s-speeds-astera-labs-pcie-6-0-switch-enables-impressive-sequential-reads)

 [![Fake Ryzen 7 9800X3D bought new, direct from Amazon Germany.](https://cdn.mos.cms.futurecdn.net/jjEYWfgEAxxFT4hhVGLrUj-840-80.jpg)

Fake Ryzen 7 9800X3D bought from Amazon was actually an old AMD FX chip disguised by IHS sticker](https://www.tomshardware.com/pc-components/cpus/fake-ryzen-7-9800x3d-bought-from-amazon-was-actually-an-old-amd-fx-chip-disguised-by-ihs-sticker)

[See more latest](https://www.tomshardware.com/news)