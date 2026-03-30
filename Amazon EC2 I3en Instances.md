---
title: "Amazon EC2 I3en Instances"
source: "https://aws.amazon.com/ec2/instance-types/i3en/"
author:
  - "[[Amazon Web Services]]"
  - "[[Inc.]]"
published:
created: 2026-03-30
description:
tags:
  - "brain_spew"
---
Dense SSD storage instances for data-intensive workloads

## Why Amazon EC2 I3en Instances?

Amazon EC2 I3en instances offer the lowest price per GB of SSD instance storage on x86-based Amazon EC2 instances and are designed for data-intensive workloads such as relational and NoSQL databases, distributed file systems, search engines, and data warehousing. With up to 60 TB of low latency Non-Volatile Memory Express (NVMe) SSD instance storage, I3en instances are optimized for applications requiring high random I/O access to large amounts of data. I3en instances also come with up to 100 Gbps networking bandwidth, 96 vCPUs, and 768 GiB of memory. Customers can enable Elastic Fabric Adapter (EFA) on I3en for low and consistent network latency. I3en instances feature either the 1st or 2nd generation Intel® Xeon® Scalable processor (Skylake or Cascade Lake) with a sustained all core Turbo CPU clock speed of up to 3.1 GHz.

Customers are able to choose from seven different instance sizes to match the price, performance, and storage requirements of their application. I3en instances can deliver up to 2 million random IOPS at 4 KB block sizes and up to 16 GB/s of sequential disk throughput.

## Benefits

## Features

### Built on the aws nitro system

I3en instances are built on the AWS Nitro System, a rich collection of building blocks that offloads many of the traditional virtualization functions to dedicated hardware. By doing so, the AWS Nitro System enables high performance, high availability, and high security while also reducing virtualization overhead.

### Bare metal instances

I3en instances offer bare metal size (i3en.metal) that provide your applications with direct access to the compute and memory resources of the underlying next generation AWS hardware and software infrastructure. Bare metal instances let you run a variety of workloads on AWS, including non-virtualized workloads, workloads that benefit from direct access to physical resources, and workloads that may have licensing restrictions. The i3en.metal instances are powered by 1st or 2nd generation Intel® Xeon® Scalable (Skylake or Cascade Lake) processors with 48 hyper-threaded cores, 768 GiB of memory, and 60 TB of NVMe SSD-backed instance storage. They deliver high networking throughput and lower latency with up to 100 Gbps of aggregate network bandwidth by leveraging the next generation of EC2 networking technology, Enhanced Networking based on Elastic Network Adapter (ENA).

## Product Details

| Model | vCPU | Memory (GiB) | Instance Storage (GB) | Network Bandwidth (Gbps) | EBS Bandwidth (Gbps) |
| --- | --- | --- | --- | --- | --- |
| i3en.large | 2 | 16 | 1 x 1250 NVMe SSD | Up to 25 | Up to 4.75 |
| i3en.xlarge | 4 | 32 | 1 x 2500 NVMe SSD | Up to 25 | Up to 4.75 |
| i3en.2xlarge | 8 | 64 | 2 x 2500 NVMe SSD | Up to 25 Gbps | Up to 4.75 |
| i3en.3xlarge | 12 | 96 | 1 x 7500 NVMe SSD | Up to 25 | Up to 4.75 |
| i3en.6xlarge | 24 | 192 | 2 x 7500 NVMe SSD | 25 | 4.75 |
| i3en.12xlarge | 48 | 384 | 4 x 7500 NVMe SSD | 50 | 9.5 |
| i3en.24xlarge | 96 | 768 | 8 x 7500 NVMe SSD | 100 | 19 |
| i3en.metal | 96 | 768 | 8 x 7500 NVMe SSD | 100 | 19 |

All instances have the following specs:

- 3.1 GHz all core turbo 1st or 2nd generation Intel® Xeon® Scalable (Skylake or Cascade Lake) processors
- Intel AVX†, Intel AVX2†, Intel AVX-512†, Intel Turbo
- EBS Optimized
- Enhanced Networking

## Blog

New – The Next Generation (I3en) of I/O-Optimized EC2 Instances.

Jeff Barr - May 8th, 2019  
  
[Read the Blog](https://aws.amazon.com/blogs/aws/new-the-next-generation-i3en-of-i-o-optimized-ec2-instances/)