---
title: "Types of Data Engineering Architecture"
source: "https://medium.com/@ckekula/types-of-data-engineering-architecture-8e28a8e7519f"
author:
  - "[[Chamuditha Kekulawala]]"
published: 2024-12-16
created: 2025-03-02
description: "Here, I’ll outline prominent examples and types of data architecture that are popular today. Though this list is not exhaustive, the purpose is to present some of the most common data architecture…"
tags:
  - "clippings"
---
[

![Chamuditha Kekulawala](https://miro.medium.com/v2/resize:fill:88:88/1*58K4QrIMSGIQfhdoIrcdeQ.jpeg)

](https://medium.com/@ckekula?source=post_page---byline--8e28a8e7519f---------------------------------------)

Looking to hide highlights? You can now hide them from the “•••” menu.

Here, I’ll outline prominent examples and types of data architecture that are popular today. Though this list is not exhaustive, the purpose is to present some of the most common data architecture patterns and to get you thinking about the required flexibility and trade-offs when designing a good architecture for your use case.

## Data Warehouse

A data warehouse is **a central data hub used for reporting and analysis**. Data in a data warehouse is typically **highly formatted and structured** for analytics use cases. It’s among the oldest and most well-established data  
architectures.

> In 1990, Bill Inmon introduced the data warehouse, which he described as “a subject-oriented, integrated, nonvolatile, and time-variant collection of data in support of management’s decisions.”

At present, the scalable, pay-as-you-go model has made cloud data warehouses accessible even to small companies. There are 2 types of data warehouse architecture:

1. **Organizational**: Organizes data associated with certain business team structures and processes
2. **Technical**: Reflects the technical nature of the data warehouse, such as MPP (Massively Parallel Processing) databases

A company can have a data warehouse without an MPP system or run an MPP system that is not organized as a data warehouse. However, the technical and organizational architectures have existed in a virtuous cycle and are frequently identified with each other.

The organizational data warehouse architecture has 2 main characteristics:

1. **Separates analytics processes (OLAP) from production databases (OLTP)**. This separation is critical as businesses grow. Moving data into a separate physical system directs load away from production systems and improves analytics performance.
2. **Centralizes and organizes data**: Traditionally, a data warehouse pulls data from application systems using **ETL**.

The *extract* phase pulls data from source systems. The *transform* phase cleans and standardizes data, organizing and imposing business logic in a highly modeled form.

The *load* phase pushes data into the data warehouse target database system. Data is loaded into multiple **data marts** that serve the analytical needs for specific lines or business and departments:

![](https://miro.medium.com/v2/resize:fit:700/1*jpYJA2F2W-Hq3dSh9BANTg.png)

One variation on ETL is **ELT**. With this, data gets moved more or less **directly from production systems into a staging area** in the data warehouse. (Staging in this setting indicates that the data is in a raw form.)

Rather than using an external system, transformations are handled directly in the data warehouse. The intention is to take advantage of the massive computational power of cloud data warehouses and data processing tools. Data is processed in batches, and transformed output is written into tables and views for analytics:

![](https://miro.medium.com/v2/resize:fit:700/1*y2WpiNZ4u88tgFTHffmexw.png)

ELT is also popular in a streaming arrangement, as events are streamed from a CDC (Change Data Capture) process, stored in a staging area, and then subsequently transformed within the data warehouse.

## Cloud Data Warehouses

**Google BigQuery**, **Snowflake**, and other competitors popularized the idea of separating compute from storage. In this architecture, data is housed in object storage, allowing virtually limitless storage. This also gives users the option to spin up computing power on demand, providing ad hoc big data capabilities without the long-term cost of thousands of nodes.

Cloud data warehouses expand the capabilities of MPP systems to cover many big data use cases that required a Hadoop cluster in the very recent past. They can readily process petabytes of data in a single query. They typically support data structures that allow the storage of tens of megabytes of raw text data per row or extremely rich and complex JSON documents.

## Data Mart

A data mart is a more **refined subset of a warehouse** designed to serve analytics and reporting, focused on a single suborganization, department, or line of business; every department has its own data mart, specific to its needs. This is in contrast to the full data warehouse that serves the broader organization or business.

**Data marts exist for 2 reasons**:

1. A data mart makes data more easily accessible to analysts and report developers.
2. Data marts provide an additional stage of transformation beyond that provided by the initial ETL or ELT pipelines.

This can significantly improve performance if reports or analytics queries require complex joins and aggregations of data, especially when the raw data is large. Transform processes can populate the data mart with joined and aggregated data to improve performance for live queries:

![](https://miro.medium.com/v2/resize:fit:700/1*Jf2BMfs55wSphFrg1mk3Bw.png)

## Data Lakes

Among the most popular architectures that appeared during the big data era is the data lake. Instead of imposing tight structural limitations on data, why not simply dump all of your data — structured and unstructured — into a central location?

As the cloud grew in popularity, these data lakes moved to cloud-based object storage, with extremely cheap storage costs and virtually limitless storage capacity. Instead of relying on a monolithic data warehouse where storage and compute are tightly coupled, the data lake allows an immense amount of data of any size and type to be stored.

When this data needs to be queried or transformed, you have access to nearly unlimited computing power by spinning up a cluster on demand, and you can pick your favorite data-processing technology for the task at hand — **MapReduce**, **Spark**, **Ray**, **Presto**, **Hive**, etc.

## First generation Data Lakes

Despite the promise and hype when it first came out, the first-generation data lake had serious shortcomings. The data lake became a dumping ground; giving birth to terms such as **data swamp**, **dark data**.

Data grew to unmanageable sizes, with little in the way of schema management, data cataloging, and discovery tools. In addition, the original data lake concept was essentially write-only, creating huge headaches with the arrival of regulations such as GDPR that required targeted deletion of user records.

## Data Lakehouse

In response to the limitations of first-generation data lakes, **Databricks** introduced the **data lakehouse**. The lakehouse incorporates the controls, data management, and data structures found in a data warehouse while still housing data in object storage and supporting a variety of query and transformation engines.

In particular, the data lakehouse supports **ACID transactions**, a big departure from the original data lake, where you simply pour in data and never update or delete it. The term data lakehouse suggests a convergence between data lakes and data warehouses.

> As cloud data warehouses mature, the line between the data warehouse and the data lake will continue to blur. Cloud data warehouse capabilities are so significant the term data warehouse might be dropped altogether.

Cloud data warehouses separate compute from storage, support petabyte-scale queries, store unstructured text and semi-structured objects, and integrate with advanced processing technologies such as **Spark** or **Beam**.

We can see several vendors offering data platforms that combine data lake and data warehouse such as AWS, Azure, Google Cloud, Snowflake,  
and Databricks.

Thanks for reading 🎉 In [part 2](https://medium.com/@ckekula/types-of-data-engineering-architecture-part-2-ffed1a017b09) I introduce the Data Mesh and IoT architecture!