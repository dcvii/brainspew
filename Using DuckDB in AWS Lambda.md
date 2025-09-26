---
title: "Using DuckDB in AWS Lambda"
source: "https://tobilg.com/using-duckdb-in-aws-lambda"
author:
  - "[[Tobias Müller]]"
published: 2023-02-12
created: 2025-08-25
description: "How to run DuckDB in a serverless way on AWS Lambda, with a custom layer."
tags:
  - "clippings"
---
![Using DuckDB in AWS Lambda](https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/VTvnoNBowZs/upload/e930e7fd571fb4bae4510f6986b305f6.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp)

Using DuckDB in AWS Lambda

Photo by [Jason Richard](https://unsplash.com/es/@jasonthedesigner?utm_source=Hashnode&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=Hashnode&utm_medium=referral)![Tobias Müller's photo](https://cdn.hashnode.com/res/hashnode/image/upload/v1673393236830/3QTaMXr-U.jpeg?w=200&h=200&fit=crop&crop=faces&auto=compress,format&format=webp)

Tobias Müller's photo

[Tobias Müller](https://hashnode.com/@TobiLG)

·

6 min read

## Prelude

DuckDB is an open-source in-process SQL OLAP database management system that has recently gained significant public interest due to its unique architecture and impressive performance benchmarks.

Unlike traditional databases that are designed to handle a wide variety of use cases, DuckDB is built specifically for analytical queries and is optimized to perform extremely well in these scenarios. This focus on analytics has allowed DuckDB to outperform traditional databases by several orders of magnitude, making it a popular choice for data scientists and analysts who need to process large datasets quickly and efficiently.

As DuckDB is designed to be a highly efficient and scalable database system, which makes it a perfect fit for serverless architectures that allow developers to build and run applications and services without having to manage infrastructure.

DuckDB's ability to handle large datasets in a memory-efficient manner makes it an ideal choice for serverless environments. Being able to read columnar storage formats like Parquet or Apache Arrow tables from local, S3 or HTTP sources, DuckDB can quickly scan and aggregate large amounts of data without having to load it all into memory, reducing the amount of memory required to perform complex analytical queries. This allows for cost savings, as serverless environments typically charge for both compute and memory resources.

Existing AWS services, such as Athena or RDS, don't provide the same functionalities, and also have different scaling and pricing models. That's why it makes sense to explore ways to run DuckDB as an analytical service on AWS.

## How to run DuckDB in AWS Lambda?

The goal of this article is to use DuckDB on Node.js runtimes (12, 14, 16 and 18), thus it is necessary to find a way to make DuckDB usable with Lambda. The first idea was to simply use the existing [DuckDB npm package](https://www.npmjs.com/package/duckdb) and use the default packaging mechanisms when deploying Lambda functions. Unfortunately, this idea proved impossible due to [downstream package problems](https://github.com/mapbox/node-pre-gyp/issues/661#issuecomment-1347186316) and different build Operating Systems (Lambda needs statically linked binaries built on Amazon Linux).

Generally, there are several ways to package dependencies in AWS Lambda functions with Node.js runtimes. Using bundlers like WebPack or ESbuild is probably the most used option at the moment.

Another one is using AWS Lambda layers for distributing dependencies to Lambda functions, allowing developers to manage common components and libraries across multiple functions in a centralized manner. By creating a layer for the dependencies, developers can avoid having to include them in each function’s deployment package. This helps reduce the size of the deployment package and makes it easier to manage updates to the dependencies. Moreover, using a Lambda layer can also improve the performance of Lambda functions.

## Building DuckDB for AWS Lambda

So, how can we achieve to build a DuckDB version that can be used with Node.js runtimes on AWS Lambda?

- We have to use a compatible environment when compiling the DuckDB binary, to avoid GLIBC incompatibilities etc. This means that we have to use an Amazon Linux distribution to build DuckDB, and enable static linking.
- We have to solve the downstream package problems stated above, which make it impossible to use the default package.
- On a side note, we want to enable the current features like COPY TO PARTITIONED BY and improved Parquet file reading, thus requiring a build from the master branch of DuckDB.

I created [https://github.com/tobilg/duckdb-nodejs-layer](https://github.com/tobilg/duckdb-nodejs-layer) to achieve this. It uses GitHub Actions to automatically trigger a build of DuckDB from the current master, package it as AWS Lambda layer and automatically upload it to all AWS regions. Feel free to have a look at the source code, and open a GitHub issue in case you find some errors or ideas for improvement.

## Using the DuckDB Lambda layer

Depending on your preferred framework, the methods to use a Lambda layer are different. You can find the respective docs of the most common frameworks below:

- [Serverless Framework](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml/#functions)
- [SAM](https://aws.amazon.com/blogs/compute/working-with-aws-lambda-and-lambda-layers-in-aws-sam/)
- [CDK](https://docs.aws.amazon.com/cdk/api/v1/docs/aws-lambda-readme.html#layers)
- [CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html#cfn-lambda-function-layers)

The ARNs follow the following logic:

```bash
arn:aws:lambda:$REGION:041475135427:layer:duckdb-nodejs-layer:$VERSION
```

You can find the list of ARNs for all regions at [https://github.com/tobilg/duckdb-nodejs-layer#usage](https://github.com/tobilg/duckdb-nodejs-layer#usage).

I created an example repository with the Serverless Framework at [https://github.com/tobilg/serverless-duckdb](https://github.com/tobilg/serverless-duckdb) that uses API Gateway and Lambda to provide an endpoint to which SQL queries can be issued, which the built-in DuckDB then executes. Let's walk through it!

### Requirements

You'll need a current v3 version installation of the [Serverless Framework](https://serverless.com/) on the machine you're planning to deploy the application from.

Also, you'll have to set up your AWS credentials according to the [Serverless docs](https://www.serverless.com/framework/docs/providers/aws/guide/credentials/).

### Configuration

DuckDB is automatically configured to use the [HTTPFS extension](https://duckdb.org/docs/extensions/httpfs) and uses the AWS credentials that are given to your Lambda function by its execution role. This means you can potentially query data that is available via HTTP(S) or in AWS S3 buckets.

If you want to also query data (e.g. Parquet files) that resides in one or more S3 buckets, you'll have to adjust the `iamRoleStatements` part of the function configuration in the [serverless.yml](https://github.com/tobilg/serverless-duckdb/blob/main/serverless.yml#L45) file. Just replace the `YOUR-S3-BUCKET-NAME` with your actual S3 bucket name.

```yaml
query:
    handler: src/functions/query.handler
    memorySize: 10240
    timeout: 30
    iamRoleStatements:
      - Effect: Allow
        Action:
          - s3:GetObject
        Resource: 'arn:aws:s3:::YOUR-S3-BUCKET-NAME/*'
      - Effect: Allow
        Action:
          - s3:ListBucket
        Resource:
          - 'arn:aws:s3:::YOUR-S3-BUCKET-NAME'
    layers:
      - 'arn:aws:lambda:${self:provider.region}:041475135427:layer:duckdb-nodejs-layer:3'
    events:
      - http:
          path: ${self:custom.api.version}/query
          method: post
          cors: true
          private: true
```

### Deployment

After you cloned this repository to your local machine and cd'ed in its directory, the application can be deployed like this (don't forget a `npm i` to install the dependencies):

```bash
$ sls deploy
```

This will deploy the stack to the default AWS region `us-east-1`. In case you want to deploy the stack to a different region, you can specify a `--region` argument:

```bash
$ sls deploy --region eu-central-1
```

The deployment should take 2-3 minutes. Once the deployment is finished, you should find some output in your console that indicates the API Gateway endpoint URL and the API Key:

```yaml
api keys:
  DuckDBKey: REDACTED
endpoint: POST - https://REDACTED.execute-api.us-east-1.amazonaws.com/prd/v1/query
```

### Usage

You can now query your DuckDB endpoint via HTTP requests (don't forget to exchange `REDACTED` with your real URL and API Key), e.g.

The query results will look to this:

```json
[
    {
        "avg(c_acctbal)": 4454.577060000001
    }
]
```

### Example queries

```bash
Remote Parquet Scans:
  SELECT count(*) FROM 'https://shell.duckdb.org/data/tpch/0_01/parquet/lineitem.parquet';
  SELECT count(*) FROM 'https://shell.duckdb.org/data/tpch/0_01/parquet/customer.parquet';
  SELECT avg(c_acctbal) FROM 'https://shell.duckdb.org/data/tpch/0_01/parquet/customer.parquet';
  SELECT * FROM 'https://shell.duckdb.org/data/tpch/0_01/parquet/orders.parquet' LIMIT 10;

Remote Parquet/Parquet Join:
  SELECT n_name, count(*)
  FROM 'https://shell.duckdb.org/data/tpch/0_01/parquet/customer.parquet',
       'https://shell.duckdb.org/data/tpch/0_01/parquet/nation.parquet'
  WHERE c_nationkey = n_nationkey GROUP BY n_name;
```

## Conclusion

We were able to show that it's possible to package and use DuckDB in a Lambda function, as well as to run performant queries on remote data with this setup.

But we need to keep in mind that this is just a showcase. The example application doesn't solve a lot of issues we'd have to solve if we'd want to run this in a distributed manner:

- A query planner and router, that scales DuckDB instances and redistributes the queries to the "query backend" functions, as well as unites the query results before passing them back to the query issuer
- "Query stickiness": The example is stateless, meaning that even if you'd load data into a memory table, you'd not be able to be sure that you'd reach the same function instance with a subsequent query due to Lambda's scaling/execution model
- Running DuckDB "only" in Lambda functions may not be the most performant way when AWS Fargate and very large EC2 instances exist
- The example application uses API Gateway as the event source for the Lambda function, which means the maximum runtime of the queries can be 30 seconds, which is unrealistic for large datasets or complicated queries. In real-world scenarios, the Lambda function would need to be triggered asynchronously, e.g. via SNS or SQS. This also means that the queries probably can't follow a strict request/response model.

## References

- [BoilingData](https://www.boilingdata.com/)
- [STOIC](https://stoic.com/)
- [Ismael Ghalimi's Twitter feed](https://twitter.com/ghalimi)