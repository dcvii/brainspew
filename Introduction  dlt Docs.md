---
title: Introduction | dlt Docs
source: https://dlthub.com/docs/intro
author: 
published: 
created: 2025-03-13
description: Introduction to dlt
tags:
  - pyDLT
---
Version: 1.8.1 (latest)

![dlt pacman](https://dlthub.com/docs/assets/images/dlt-pacman-b67f01290996fde3a5a12edbde2186bc.gif)

dlt is an open-source Python library that loads data from various, often messy data sources into well-structured, live datasets. It offers a lightweight interface for extracting data from [REST APIs](https://dlthub.com/docs/tutorial/rest-api), [SQL databases](https://dlthub.com/docs/tutorial/sql-database), [cloud storage](https://dlthub.com/docs/tutorial/filesystem), [Python data structures](https://dlthub.com/docs/tutorial/load-data-from-an-api), and [many more](https://dlthub.com/docs/dlt-ecosystem/verified-sources).

dlt is designed to be easy to use, flexible, and scalable:

- dlt infers [schemas](https://dlthub.com/docs/general-usage/schema) and [data types](https://dlthub.com/docs/general-usage/schema/#data-types), [normalizes the data](https://dlthub.com/docs/general-usage/schema/#data-normalizer), and handles nested data structures.
- dlt supports a variety of [popular destinations](https://dlthub.com/docs/dlt-ecosystem/destinations/) and has an interface to add [custom destinations](https://dlthub.com/docs/dlt-ecosystem/destinations/destination) to create reverse ETL pipelines.
- dlt can be deployed anywhere Python runs, be it on [Airflow](https://dlthub.com/docs/walkthroughs/deploy-a-pipeline/deploy-with-airflow-composer), [serverless functions](https://dlthub.com/docs/walkthroughs/deploy-a-pipeline/deploy-with-google-cloud-functions), or any other cloud deployment of your choice.
- dlt automates pipeline maintenance with [schema evolution](https://dlthub.com/docs/general-usage/schema-evolution) and [schema and data contracts](https://dlthub.com/docs/general-usage/schema-contracts).

To get started with dlt, install the library using pip:

```prism
pip install dlt
```

tip

We recommend using a clean virtual environment for your experiments! Read the [detailed instructions](https://dlthub.com/docs/reference/installation) on how to set up one.

tip

If you'd like to try out dlt without installing it on your machine, check out the [Google Colab demo](https://colab.research.google.com/drive/1NfSB1DpwbbHX9_t5vlalBTf13utwpMGx?usp=sharing).

1. Give the library a ⭐ and check out the code on [GitHub](https://github.com/dlt-hub/dlt).
2. Ask questions and share how you use the library on [Slack](https://dlthub.com/community).
3. Report problems and make feature requests [here](https://github.com/dlt-hub/dlt/issues/new/choose).