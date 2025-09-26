---
title: DuckDB + Delta Lake.
source: https://dataengineeringcentral.substack.com/p/duckdb-delta-lake
author:
  - "[[T50/Daniel Beach]]"
published: 2024-12-11
created: 2025-05-12
description: ... just checking for rough edges.
tags:
  - clippings
---
### ... just checking for rough edges.

![](https://substackcdn.com/image/fetch/w_424)

I’ve done a lot of playing around with Delta Lake in my day, enough to have fallen in and out of love a few different times. I think for those of us who grew up in the land of Kimball and SQL Server, before the demi-gods of Snowflake and Databricks came along, we still can’t believe such a thing as a Lake House exists. What a wonder indeed.

**Anywho, I’ve been meaning to give Delta Lake + DuckDB a try and see what’s cracking.**

I’m not sure I have a particular purpose in doing so, other than that I’ve done similar things with Non-Spark tools like Daft and found great success. We’ve all heard how fast DuckDB is, so it should be interesting to unleash it on Delta Lake and see what happens.

**Thanks to [Delta](http://www.delta.io/) for sponsoring this newsletter!** ***I personally use Delta Lake on a daily basis, and I believe this technology represents the future of Data Engineering*****. Check out their website below.**

![](https://substackcdn.com/image/fetch/w_424)

### DuckDB + Delta Lake (open source / non-Databricks)

I think we should take a dual approach to this little DuckDB experiment. It will be a two-pronged attack.

- *Laptop - DuckDB + local open/source Delta Lake.*
- *Laptop - DuckDB + local open/source Delta Lake (s3 backend).*

I’m not really sure if there will be much, or any difference between these two approaches. I am curious generally if when we move onto testing DuckDB with s3, what happens with credentials and such things, but let’s not get ahead of ourselves.

> ***Let’s just try out a local setup of DuckDB + open-source Delta Lake.***

### Setting up a local environment for DuckDB + Delta Lake.

Let’s start with the easy one, just a local laptop setup for DuckDB and Delta Lake, we will wrap it up with Docker so you can do the same yourself.

As far as I can tell, at the moment, there isn’t any WRITE support with DuckDB + Delta Lake, so we will have to resort to some other package to get that part done (*the creation of the Delta Lake that is*).

Read support for Delta Lake is nice, but it would be even better to have write support … the full deal that is. At this point, the idea would be to use DuckDB as a pure analytics crunching machine on top of Delta Lake.

Let’s use the following basic Dockerfile.

```markup
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

VOLUME ["/app"]

RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && . "$HOME/.cargo/env" \
    && cargo --version

RUN git clone https://github.com/danielbeach/datahobbit.git

ENV PATH="/root/.cargo/bin:${PATH}"

CMD ["python"]
```

Here is our *requirements.txt*

```markup
duckdb
getdaft[deltalake,sql]
deltalake
```

To build the image, simply use …

```markup
docker build . --tag=ducky
```

To drop into the container to mess around you can …

```markup
docker run -it ducky /bin/bash
```

Now let’s make ourselves a dataset with [my wonderful datahobbit tool](https://github.com/danielbeach/datahobbit).

```markup
git clone https://github.com/danielbeach/datahobbit.git
cd datahobbit && cargo run -- schema.json output.csv --records 10000000
```

> *Now that I’m about to convert this 10 million line CSV file over to a Delta Lake table format, with some tool, [I just remembered I recently wrote about a tool called Daft](https://dataengineeringcentral.substack.com/p/daft-vs-spark-databricks-for-delta), using Delta Lake. Let’s use that project/tool to convert our CSV file to a Delta Lake we can read with DuckDB.*

Let’s get that CSV into Delta Lake format.

```markup
import daft

df = daft.read_csv('output.csv')
df.write_deltalake("example_deltalake", mode="overwrite")
```

Well, it worked, that’s something.

```markup
root@dcd6ec0c818d:/app/datahobbit# ls example_deltalake/
0-06d5b7fb-757b-47d0-9061-78f2bbb63b5c-0.parquet  _delta_log
```

We now have a Delta Table with about 10 million records, enough to play around with DuckDB finally!

```markup
>>> df.count().show()
╭──────────╮                                                                                                                                       
│ count    │                                                                                                                                       
│ ---      │
│ UInt64   │
╞══════════╡
│ 10000000 │
╰──────────╯
```

### DuckDB + Delta Lake … locally.

Well, let’s hope this is blissfully boring, shall we? We don’t want any surprises and we want it to be simple and fast.

```markup
import duckdb
df = duckdb.delta_scan('delta_example');

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'duckdb' has no attribute 'delta_scan'
```

Ah yes, I’m a DuckDB padawan, so I forget things easily.

```markup
INSTALL delta;
LOAD delta;
```

So, to back up a bit.

```markup
import duckdb

duckdb.sql("""
INSTALL delta;
LOAD delta;
""")
duckdb.sql("""
SELECT * 
FROM delta_scan('delta_example');
""").show()
```

Ok, so that’s always a great sign when things work out of the box like that, no funny stuff going on, no buttons to push or secret switches to flip.

> *Let’s try running and aggregation query, and writing the results to a CSV file.*

Let’s do some query like this.

```markup
from datetime import datetime
import duckdb

t1 = datetime.now()
duckdb.sql("""
INSTALL delta;
LOAD delta;
""")

duckdb.sql("""
SELECT age, is_active, AVG(age) as avg_age
FROM delta_scan('example_deltalake')
GROUP BY age, is_active
""").write_csv("results.csv");
t2 = datetime.now()
total = t2-t1
print(f"it took {total} to run this query.")
```

Well, I didn’t expect that.

```markup
it took 0:00:00.462964 to run this query.
```

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/e8c34b83-43ef-40cb-9a19-b7586ccd86df_736x440.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:440,%22width%22:736,%22resizeWidth%22:null,%22bytes%22:49795,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

So, DuckDB did the work, very fast, less than half a second for 10 million rows of aggregationon Delta Lake. That’s pretty fast!

##### Should we try it with Daft just to see how fast DuckDB is so we can get an idea??

Of course. Let’s try this same aggregation with Daft and get an idea of just how fast DuckDB is since we really don’t have a baseline.

```markup
import daft
from daft.sql import SQLCatalog
from datetime import datetime

t1 = datetime.now()
df = daft.read_deltalake('example_deltalake')
catalog = SQLCatalog({'data': df})

results = daft.sql("""
SELECT age, is_active, AVG(age) as avg_age
FROM df
GROUP BY age, is_active
""", catalog=catalog)
results.write_csv('daft_results')
t2 = datetime.now()
total = t2-t1
print(f'it took {total} to run the query')
```

Very interesting indeed.

```markup
it took 0:00:01.145941 to run the query
```

**I think we can safely say that DuckDB is VERY fast, compared to Daft at least … and Rust based Daft is very fast at just about everything. Amazing, DuckDB is 3x faster than Daft at running an aggregation on Delta Lake.**

### But what about an AWS s3 based Delta Lake inside + DuckDB.

This will be very interesting won’t it? Will DuckDB be able to handle a remote s3 Delta Lake well, and will it still be fast and easy??

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/b89519fa-b539-4dd6-8e28-312feb118af2_1033x575.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:575,%22width%22:1033,%22resizeWidth%22:null,%22bytes%22:124289,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

There is our same Delta Lake, except up in the cloud.

```markup
from datetime import datetime
import duckdb

t1 = datetime.now()
duckdb.sql("""
INSTALL delta;
LOAD delta;
CREATE SECRET delta_s1 (
    TYPE S3,
    PROVIDER CREDENTIAL_CHAIN
);
""")

duckdb.sql("""
SELECT age, is_active, AVG(age) as avg_age
FROM delta_scan('s3://confessions-of-a-data-guy/duckdbtest/')
GROUP BY age, is_active
""").write_csv("results.csv");
t2 = datetime.now()
total = t2-t1
print(f"it took {total} to run this query.")
```

And the results.

```markup
it took 0:00:07.065167 to run this query.
```

> **I mean it ran, but took way longer for sure, than local, this is not a surprise I would suppose.**

Let’s try Daft to see what happens here.

```markup
import daft
from daft.sql import SQLCatalog
from datetime import datetime

t1 = datetime.now()
df = daft.read_deltalake('s3://confessions-of-a-data-guy/duckdbtest/')
catalog = SQLCatalog({'data': df})

results = daft.sql("""
SELECT age, is_active, AVG(age) as avg_age
FROM df
GROUP BY age, is_active
""", catalog=catalog)
results.write_csv('daft_results')
t2 = datetime.now()
total = t2-t1
print(f'it took {total} to run the query')
```

Interesting indeed! Daft took the lead.

```markup
it took 0:00:03.706798 to run the query
```

> **Daft is more than twice as fast as DuckDB when it comes to remote s3 execution of a Delta Lake query!!**

Strange indeed are the times we live in. But, you know, the real world of data tools never ends up being what we think it will be like. *Who would have saw that coming??*

![](https://dataengineeringcentral.substack.com/p/%7B%22src%22:%22https://substack-post-media.s3.amazonaws.com/public/images/10d40b06-b5c9-4b8e-b562-b353128c0331_626x389.png%22,%22srcNoWatermark%22:null,%22fullscreen%22:null,%22imageSize%22:null,%22height%22:389,%22width%22:626,%22resizeWidth%22:null,%22bytes%22:20885,%22alt%22:null,%22title%22:null,%22type%22:%22image/png%22,%22href%22:null,%22belowTheFold%22:true,%22topImage%22:false,%22internalRedirect%22:null,%22isProcessing%22:false,%22align%22:null%7D)

These results actually make the most sense to me. Rarely is one tool the golden child that does us no ill. Those we love most usually hurt us the most.

> *DuckDB, like our children, went from being the quickest tool and brining us rainbows and unicorns to the slowest of the slow, making us wonder where we went wrong. This is life.*