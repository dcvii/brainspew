---
title: motherduckdb/DuckDB-NSQL-7B-v0.1-GGUF · Hugging Face
source: https://huggingface.co/motherduckdb/DuckDB-NSQL-7B-v0.1-GGUF
author: 
published: 
created: 2025-03-05
description: We’re on a journey to advance and democratize artificial intelligence through open source and open science.
tags:
  - clippings
  - duckdb
  - llm
---
The repository includes model files in the GGUF format for [DuckDB-NSQL-7B-v0.1](https://huggingface.co/motherduckdb/DuckDB-NSQL-7B-v0.1), featuring both the f16 and Q8\_0 versions.

## Provided model files

## Model Description

NSQL is a family of autoregressive open-source large foundation models (FMs) designed specifically for SQL generation tasks.

In this repository we are introducing a new member of NSQL, DuckDB-NSQL. It's based on Meta's original [Llama-2 7B model](https://huggingface.co/meta-llama/Llama-2-7b) and further pre-trained on a dataset of general SQL queries and then fine-tuned on a dataset composed of DuckDB text-to-SQL pairs.

## Training Data

200k DuckDB text-to-SQL pairs, synthetically generated using [Mixtral-8x7B-Instruct-v0.1](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1), guided by the DuckDB v0.9.2 documentation. And text-to-SQL pairs from [NSText2SQL](https://huggingface.co/datasets/NumbersStation/NSText2SQL) that were transpiled to DuckDB SQL using [sqlglot](https://github.com/tobymao/sqlglot).

## Evaluation Data

We evaluate our models on a DuckDB-specific benchmark that contains 75 text-to-SQL pairs. The benchmark is available [here](https://github.com/NumbersStationAI/DuckDB-NSQL/).

## Training Procedure

DuckDB-NSQL was trained using cross-entropy loss to maximize the likelihood of sequential inputs. For finetuning on text-to-SQL pairs, we only compute the loss over the SQL portion of the pair. The model is trained using 80GB A100s, leveraging data and model parallelism. We fine-tuned for 10 epochs.

## Intended Use and Limitations

The model was designed for text-to-SQL generation tasks from given table schema and natural language prompts. The model works best with the prompt format defined below and outputs. In contrast to existing text-to-SQL models, the SQL generation is not contrained to `SELECT` statements, but can generate any valid DuckDB SQL statement, including statements for official DuckDB extensions.

## How to Use

Setup llama.cpp:

```shell
CMAKE_ARGS="-DLLAMA_METAL=on" pip install llama-cpp-python
huggingface-cli download motherduckdb/DuckDB-NSQL-7B-v0.1-GGUF DuckDB-NSQL-7B-v0.1-q8_0.gguf --local-dir . --local-dir-use-symlinks False
pip install wurlitzer
```

Example 1:

```python
## Setup - Llama.cpp
from llama_cpp import Llama
with pipes() as (out, err):
    llama = Llama(
        model_path="DuckDB-NSQL-7B-v0.1-q8_0.gguf",
        n_ctx=2048,
    )

text = """### Instruction:
Your task is to generate valid duckdb SQL to answer the following question.

### Input:

### Question:
create a new table called tmp from test.csv

### Response (use duckdb shorthand if possible):
"""

with pipes() as (out, err):
    pred = llama(text, temperature=0.1, max_tokens=500)
print(pred["choices"][0]["text"])
```

Example 2:

```python
from llama_cpp import Llama
with pipes() as (out, err):
    llama = Llama(
        model_path="DuckDB-NSQL-7B-v0.1-q8_0.gguf",
        n_ctx=2048,
    )
    
text = """### Instruction:
Your task is to generate valid duckdb SQL to answer the following question, given a duckdb database schema.

### Input:
Here is the database schema that the SQL query will run on:
CREATE TABLE taxi (
    VendorID bigint,
    tpep_pickup_datetime timestamp,
    tpep_dropoff_datetime timestamp,
    passenger_count double,
    trip_distance double,
    fare_amount double,
    extra double,
    tip_amount double,
    tolls_amount double,
    improvement_surcharge double,
    total_amount double,
);

### Question:
get all columns ending with _amount from taxi table

### Response (use duckdb shorthand if possible):"""

with pipes() as (out, err):
    pred = llama(text, temperature=0.1, max_tokens=500)
print(pred["choices"][0]["text"])
```

Example 3:

```python
from llama_cpp import Llama
with pipes() as (out, err):
    llama = Llama(
        model_path="DuckDB-NSQL-7B-v0.1-q8_0.gguf",
        n_ctx=2048,
    )
    
text = """### Instruction:
Your task is to generate valid duckdb SQL to answer the following question, given a duckdb database schema.

### Input:
Here is the database schema that the SQL query will run on:
CREATE TABLE rideshare (
    hvfhs_license_num varchar,
    dispatching_base_num varchar,
    originating_base_num varchar,
    request_datetime timestamp,
    on_scene_datetime timestamp,
    pickup_datetime timestamp,
    dropoff_datetime timestamp,
    trip_miles double,
    trip_time bigint,

);

### Question:
get longest trip in december 2022

### Response (use duckdb shorthand if possible):
"""

with pipes() as (out, err):
    pred = llama(text, temperature=0.1, max_tokens=500)
print(pred["choices"][0]["text"])
```

For more information (e.g., run with your local database), please find examples in [this repository](https://github.com/NumbersStationAI/DuckDB-NSQL).