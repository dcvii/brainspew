---
title: "Brave Search"
source: "https://search.brave.com/search?q=is+there+a+databricks+API&source=newtab&summary=1&conversation=08e17484b5802ac338d34cd9c0dfc90dde06"
author:
  - "[[Brave Search]]"
published:
created: 2026-03-23
description: "Search the Web. Privately. Truly useful results, AI-powered answers, & more. All from an independent index. No profiling, no bias, no Big Tech."
tags:
  - "brain_spew"
---
Yes, **Databricks provides a comprehensive REST API** for programmatic access to its platform. This API enables automation of tasks such as job scheduling, cluster management, file operations (via DBFS), secret management, and workspace configuration.

### Key Databricks API Features:

- **REST API**: Officially documented and supported for Azure Databricks and AWS Databricks.
- **Python SDK**: The **Databricks SDK for Python** (`databricks-sdk-py`) is the recommended way to interact with Databricks programmatically. It wraps the REST API with a clean, Pythonic interface and handles retries, authentication, and error handling.
	- GitHub: [github.com/databricks/databricks-sdk-py](https://github.com/databricks/databricks-sdk-py)
- **SQL Execution API**: Allows querying data via SQL using the `/sql/statements` endpoint, ideal for BI tools like Power BI.
	- Supported via Databricks SQL Warehouses and REST API.
- **Use Cases**:
	- Automate job runs and pipeline orchestration.
		- Integrate with CI/CD pipelines, Airflow, or Azure Data Factory.
		- Securely manage secrets and permissions.
		- Build scalable data ingestion and monitoring workflows.

> 🔐 **Authentication**: Use personal access tokens, OAuth, or Azure Active Directory (for Azure Databricks).  
> 📌 **Best Practice**: Use the official **Databricks SDK for Python** instead of third-party wrappers like `databricks-api` (which is deprecated).

[![Generating Access Token in Databricks.](https://imgs.search.brave.com/OKn_mqZL1zZu_NJMslfN1bmnk7fxhFkiNWUf7DLYsOM/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9tZWRp/YS5kYXRhY2FtcC5j/b20vY21zL2FkXzRu/eGQzNHl0dXJiaXJx/bWNqMGQ0ZWxnZmtx/Y2x0YWpnYWgtaDl1/eHA4Mm90N2dkdWZh/eS1kdS1mcHk4eGN5/Z2RkeWEtZV9feS1y/ZWcwcnhnY3FvdHBf/a2d1ZG1namdsbjFy/dmhqdnZzN2dwaHBh/YW92M2JqZHV2Yl9x/eGJxX3ZjeWJycWl2/bWhwanEucG5n)](https://search.brave.com/images?q=is+there+a+databricks+API&context=W3sic3JjIjoiaHR0cHM6Ly9pbWdzLnNlYXJjaC5icmF2ZS5jb20vT0tuX21xWkwxelp1X05KTXNsZk4xYm1uazdmeGhGa2lOV1VmN0RMWXNPTS9yczpmaXQ6NTAwOjA6MDowL2c6Y2UvYUhSMGNITTZMeTl0WldScC9ZUzVrWVhSaFkyRnRjQzVqL2IyMHZZMjF6TDJGa1h6UnUvZUdRek5IbDBkWEppYVhKeC9iV05xTUdRMFpXeG5abXR4L1kyeDBZV3BuWVdndGFEbDEvZUhBNE1tOTBOMmRrZFdaaC9lUzFrZFMxbWNIazRlR041L1oyUmtlV0V0WlY5ZmVTMXkvWldjd2NuaG5ZM0Z2ZEhCZi9hMmQxWkcxbmFtZHNiakZ5L2RtaHFkblp6TjJkd2FIQmgvWVc5Mk0ySnFaSFYyWWw5eC9lR0p4WDNaamVXSnljV2wyL2JXaHdhbkV1Y0c1biIsInRleHQiOiJHZW5lcmF0aW5nIEFjY2VzcyBUb2tlbiBpbiBEYXRhYnJpY2tzLiIsInBhZ2VfdXJsIjoiaHR0cHM6Ly93d3cuZGF0YWNhbXAuY29tL3R1dG9yaWFsL2RhdGFicmlja3MtYXBpIn1d&sig=7e07de212bf9ab5562873208b3640aa058484c390b0dbab50df20d894aa96f3c&nonce=773d31d6defddcdf3458751e4d26253c&source=llmImg)

[![Databricks Workspace.](https://imgs.search.brave.com/16sBATEdVKqDfPb-PwEtGHUiUd-4g6i2WKuXzG6-Kgg/rs:fit:500:0:0:0/g:ce/aHR0cHM6Ly9tZWRp/YS5kYXRhY2FtcC5j/b20vY21zL2FkXzRu/eGV1eHlkZW8xbWts/ZzFkdzJsa2kyaGNt/c3NpeDUzdHp1amQz/eWNldnhrdTgwY3p6/cGFzZXBzZi0tenZt/eXd5amRsNmV5MG43/dnVsdXRqbjN4c3Rw/ZzZ1Y3lhYnpzaG4w/aGp3ZGx0ZHA0dHU4/dmQza3RrMDA2OTlr/OG9ha3hlb3lyaXh0/bWFsLnBuZw)](https://search.brave.com/images?q=is+there+a+databricks+API&context=W3sic3JjIjoiaHR0cHM6Ly9pbWdzLnNlYXJjaC5icmF2ZS5jb20vMTZzQkFURWRWS3FEZlBiLVB3RXRHSFVpVWQtNGc2aTJXS3VYekc2LUtnZy9yczpmaXQ6NTAwOjA6MDowL2c6Y2UvYUhSMGNITTZMeTl0WldScC9ZUzVrWVhSaFkyRnRjQzVqL2IyMHZZMjF6TDJGa1h6UnUvZUdWMWVIbGtaVzh4Yld0cy9aekZrZHpKc2Eya3lhR050L2MzTnBlRFV6ZEhwMWFtUXovZVdObGRuaHJkVGd3WTNwNi9jR0Z6WlhCelppMHRlblp0L2VYZDVhbVJzTm1WNU1HNDMvZG5Wc2RYUnFiak40YzNSdy9aeloxWTNsaFlucHphRzR3L2FHcDNaR3gwWkhBMGRIVTQvZG1RemEzUnJNREEyT1Rsci9PRzloYTNobGIzbHlhWGgwL2JXRnNMbkJ1WnciLCJ0ZXh0IjoiRGF0YWJyaWNrcyBXb3Jrc3BhY2UuIiwicGFnZV91cmwiOiJodHRwczovL3d3dy5kYXRhY2FtcC5jb20vdHV0b3JpYWwvZGF0YWJyaWNrcy1hcGkifV0%3D&sig=8061c3a636ce823d8c686f1d8e41be2b910dd5a770e57c0bb7de725e2498c251&nonce=1d2c49bf8ec3549d1f3cb2b27bddb3a6&source=llmImg)

[

Databricks reference documentation | Databricks on AWS

](https://docs.databricks.com/aws/en/reference/api)

2 weeks ago - Reference documentation for **Databricks APIs**, SQL language, command-line interfaces, and more. Databricks reference docs cover tasks from automation to data queries.

[

Azure Databricks REST APIs | Microsoft Learn

](https://learn.microsoft.com/en-us/rest/api/databricks/)

July 30, 2024 - Azure Databricks is an interactive workspace that integrates effortlessly with a wide variety of data stores and services. **To create and manage Databricks workspaces in the Azure Resource Manager, use the APIs in this section**.

[![](https://imgs.search.brave.com/KxEtqQiadL_R-Mr9_FffhMDYK3gVHrYWjuByaTLSjYg/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9sZWFy/bi5taWNyb3NvZnQu/Y29tL2VuLXVzL21l/ZGlhL29wZW4tZ3Jh/cGgtaW1hZ2UucG5n)](https://learn.microsoft.com/en-us/rest/api/databricks/)

[![](https://imgs.search.brave.com/KxEtqQiadL_R-Mr9_FffhMDYK3gVHrYWjuByaTLSjYg/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9sZWFy/bi5taWNyb3NvZnQu/Y29tL2VuLXVzL21l/ZGlhL29wZW4tZ3Jh/cGgtaW1hZ2UucG5n)](https://learn.microsoft.com/en-us/rest/api/databricks/)

---

How do I call a Web API from Databricks?

Use code in **Databricks** (like Python or Scala) to send HTTP requests to the Web **API** and get data or perform actions.

[

How to integrate & use Databricks API? \[+best practices\]

](https://hevodata.com/learn/databricks-api/)

What does Databricks do?

**Databricks** **is** **a** platform that helps you process data, build machine learning models, and do data analysis, all in one place.

[

How to integrate & use Databricks API? \[+best practices\]

](https://hevodata.com/learn/databricks-api/)

[

Databricks API: Managing Data Pipelines at Scale | DataCamp

](https://www.datacamp.com/tutorial/databricks-api)

January 29, 2025 - By automating repetitive tasks, organizations can improve efficiency and reduce the likelihood of human error, which can lead to costly mistakes or downtime. **The Databricks API** is designed for flexibility, enabling integration with external platforms such as orchestration tools like Apache...

[

Databricks API reference documentation (prototype)

](https://api-docs.databricks.com/index.html)

Note: This is a beta website. This website contains a subset of the **Databricks API** reference documentation.

[

Databricks REST API reference

](https://docs.databricks.com/api/workspace/introduction)

Reference documentation for **Databricks APIs**, SQL language, command-line interfaces, and more. Databricks reference docs cover tasks from automation to data queries.

[

databricks-api

](https://pypi.org/project/databricks-api/)

JavaScript is disabled in your browser. Please enable JavaScript to proceed · A required part of this site couldn’t load. This may be due to a browser extension, network issues, or browser settings. Please check your connection, disable any ad blockers, or try using a different browser

[

How to integrate & use Databricks API? \[+best practices\]

](https://hevodata.com/learn/databricks-api/)

January 12, 2026 - **Databricks is a Data Warehousing, Machine Learning web-based platform that allows users to store data, run analysis, and get insights using Spark SQL. APIs are flexible, reliable methods to communicate between applications and transfer data**.

[![](https://imgs.search.brave.com/0GZdVu6Vjs1moEouMlKR0hcKtjMyKi4J5fOaZlI60ME/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9yZXMu/Y2xvdWRpbmFyeS5j/b20vaGV2by9pbWFn/ZXMvZl93ZWJwLHFf/YXV0bzpiZXN0L3Yx/NzY4MzA5MDExL2hl/dm8tbGVhcm4tMS9C/bG9nLTIyNjIvQmxv/Zy0yMjYyLnBuZz9f/aT1BQSA)](https://hevodata.com/learn/databricks-api/)

[![](https://imgs.search.brave.com/0GZdVu6Vjs1moEouMlKR0hcKtjMyKi4J5fOaZlI60ME/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9yZXMu/Y2xvdWRpbmFyeS5j/b20vaGV2by9pbWFn/ZXMvZl93ZWJwLHFf/YXV0bzpiZXN0L3Yx/NzY4MzA5MDExL2hl/dm8tbGVhcm4tMS9C/bG9nLTIyNjIvQmxv/Zy0yMjYyLnBuZz9f/aT1BQSA)](https://hevodata.com/learn/databricks-api/)

[

Azure Databricks reference documentation - Azure Databricks | Microsoft Learn

](https://learn.microsoft.com/en-us/azure/databricks/reference/api)

October 1, 2022 - Reference documentation for **Azure Databricks APIs**, SQL language, command-line interfaces, and more. Azure Databricks reference docs cover tasks from automation to data queries.

[

Databricks REST API reference

](https://api-reference.cloud.databricks.com/)

We cannot provide a description for this page right now

[

Azure Databricks REST API reference

](https://docs.databricks.com/api/azure/workspace/introduction)

Reference documentation for **Databricks APIs**, SQL language, command-line interfaces, and more. Databricks reference docs cover tasks from automation to data queries.

[

GitHub - crflynn/databricks-api: A simplified, autogenerated API client interface using the databricks-cli package

](https://github.com/crflynn/databricks-api)

June 8, 2023 - **This package provides a simplified interface for the Databricks REST API**. The interface is autogenerated on instantiation using the underlying client library used in the official databricks-cli python package.

[![](https://imgs.search.brave.com/UmoFdF0wWL9WTY1x5BvWWu6Nv8P_vJw85_Kr-aVVb20/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9vcGVu/Z3JhcGguZ2l0aHVi/YXNzZXRzLmNvbS8x/OWJlMzcxMjgwOGEx/ZmRkYmRlMjM0Zjcz/MjdmZWY1ZGUwZTYw/MTRmMmQ4YjMyZWIw/MDNmN2FlZDAxNzA0/MmZkL2NyZmx5bm4v/ZGF0YWJyaWNrcy1h/cGk)](https://github.com/crflynn/databricks-api)

**Starred** by 59 users

**Forked** by 15 users

**Languages** Python 90.9% | Makefile 9.1% | Python 90.9% | Makefile 9.1%

[![](https://imgs.search.brave.com/UmoFdF0wWL9WTY1x5BvWWu6Nv8P_vJw85_Kr-aVVb20/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9vcGVu/Z3JhcGguZ2l0aHVi/YXNzZXRzLmNvbS8x/OWJlMzcxMjgwOGEx/ZmRkYmRlMjM0Zjcz/MjdmZWY1ZGUwZTYw/MTRmMmQ4YjMyZWIw/MDNmN2FlZDAxNzA0/MmZkL2NyZmx5bm4v/ZGF0YWJyaWNrcy1h/cGk)](https://github.com/crflynn/databricks-api)

[

Foundation model REST API reference | Databricks on AWS

](https://docs.databricks.com/aws/en/machine-learning/foundation-model-apis/api-reference)

January 6, 2026 - This article provides general API information for **Databricks Foundation Model APIs** and the models they support. The Foundation Model APIs are designed to be similar to OpenAI's REST API to make migrating existing projects easier.

[

r/databricks on Reddit: Databricks REST API and getting data from an all purpose compute question

](https://www.reddit.com/r/databricks/comments/1c9ujdi/databricks_rest_api_and_getting_data_from_an_all/)

April 21, 2024 - So I was tasked with getting some data from an all purpose compute cluster from Powershell and used the REST APIs to execute an SQL command to select the data and get that data to process. (https://docs.databricks.com/api/workspace/commandexecution/commandstatus) However there is a 1000 row limit of that api call and it doesn’t return any kind of chunk info or next page information like the SQL Warehouse APIs do.

[

r/dataengineering on Reddit: Best way to ingest data from API to databricks

](https://www.reddit.com/r/dataengineering/comments/118cb99/best_way_to_ingest_data_from_api_to_databricks/)February 21, 2023 -

I have a data source that's only accessible through rest API calls and I want to do some light transformation on the data before dumping into databricks table. One way I am thinking is to do this in python notebook and just schedule this notebook as part of the automation pipeline.

Is this reasonable? what downside is there to it? I am asking because I haven't seen any tutorial suggesting loading data this way. All the info I see online is basically loading data from another storage infra like SQL table, kafka, or S3 for example.[You can put the API calls in a table and call them using a Spark UDF in order to make parallel API calls. Pretty convenient because it scales horizontally well. Don't do transformations before ingesting the data, use a medallion architecture (raw, cleaned, aggregated). Then schedule it using a Workflow.](https://www.reddit.com/r/dataengineering/comments/118cb99/best_way_to_ingest_data_from_api_to_databricks/)

[

That’s how I do it

](https://www.reddit.com/r/dataengineering/comments/118cb99/best_way_to_ingest_data_from_api_to_databricks/)[Creating REST api in Databricks which would display delta tables information to the user? - Stack Overflow](https://stackoverflow.com/questions/76047847/creating-rest-api-in-databricks-which-would-display-delta-tables-information-to)[You can just leverage the Databricks SQL Statement Execution API to access data on Azure Databricks. Follow the tutorial that shows how to work with that API using curl](https://stackoverflow.com/questions/76047847/creating-rest-api-in-databricks-which-would-display-delta-tables-information-to)[

In Databricks there is no REST Api to get data in delta table, but we can get data of delta table using Databricks jobs.

Follow below steps,

First, create a notebook in databricks which gets data in delta table and returns the data in Json format. Add below code in your notebook, alter accordingly to your table.

```
df = spark.sql("SELECT  *  FROM test")
j_son = df.toJSON()

res=""
for i in j_son.collect():
    res = res + "," + i

dbutils.notebook.exit("["+res[1:]+"]")
```

Then create a job using this notebook.

In the next page create the task name, select the path to notebook and your cluster on which it needs to be run. Then hit on create.

After creating you will get details as below, copy the job id.

This is the job in databricks provides API's for running job, getting results of that particular job.

For more information follow this documentation.\`

Next create an backed server where the API request raised to databricks job. I've used javascript and expressJs framework.

In visual code open new folder and execute below command in terminal. Make sure you have `nodeJs` installed in your system.

```
npm install express axios cors
```

You will get the project structure as below in your folder.

Next, create.js file, mine it's `btst.js`. After creating, add below code in that file.

```
const  express = require('express');
const  axios = require('axios');
const  cors = require('cors');
const  app = express();

app.use(cors({
origin:'*'
}));

const  port = 5000;

// Set the access token for authentication
const  token = 'your databricks token';

// Set the base URL for the Databricks REST API
const  baseUrl = 'https://your databricks host/api/2.1/';

app.get('/runjob', async  function(req, res) {
try {
const  headers = {
'Authorization':  \`Bearer ${token}\`,
'Content-Type':  'application/json'
}

function  sleep(ms) {
return  new  Promise(resolve  =>  setTimeout(resolve, ms));
}

const  requestBody = {
job_id:  "1121949406005982"
};
const  response = await  axios.post(\`${baseUrl}jobs/run-now/\`, requestBody, { headers });
console.log(\`run id : ${response.data.run_id}\`)
console.log("job is running...")
const  t_res = await  axios.get(\`${baseUrl}jobs/runs/get?run_id=${response.data.run_id}\`,{ headers })
task_id = t_res.data.tasks[0].run_id
console.log(\`task id : ${task_id}\`)
await  sleep(15000)
const  d_res = await  axios.get(\`${baseUrl}jobs/runs/get-output?run_id=${task_id}\`,{ headers })
j_res = JSON.parse(d_res.data.notebook_output.result)
console.log(j_res)
res.send(j_res);
} catch (error) {
console.log(error)
res.status(500).send(\`Error1.......${error}\`);
}
});

app.listen(port, () => {
console.log(\`Server listening at http://localhost:${port}\`);
});
```

Here you paste the job id you copied earlier in databricks.

Then execute below command in terminal.

```
node yourfilename.js
```

In my case it is

```
node btst.js
```

Then your server will be running at `http://localhost:5000`.

You send `GET` request to this url in browser or using postman at endpoint. `http://localhost:5000/runjob`, you will get the data in json format so you can use it anywhere. This is the below result, it takes 15 seconds to display because after sending post request to jobs it needs to run the task, it takes about 10-15 seconds.

and data in databricks table is

](https://stackoverflow.com/questions/76047847/creating-rest-api-in-databricks-which-would-display-delta-tables-information-to)

[

Generate Databricks APIs | Powered by DreamFactory

](https://www.dreamfactory.com/connectors/databricks)

DreamFactory’s Databricks connector enables rapid, secure REST API generation for various databases, complete with documentation. Log in to the DreamFactory Admin Console and navigate to the API Generation & Connections tab.

[

GitHub - databricks/databricks-sdk-py: Databricks SDK for Python (Beta) · GitHub

](https://github.com/databricks/databricks-sdk-py)

Unity Catalog Automated Migration heavily relies on Python SDK for working with Databricks APIs. ip-access-list-analyzer checks & prunes invalid entries from IP Access Lists. If you use Databricks configuration profiles or Databricks-specific environment variables for Databricks authentication, the only code required to start working with a Databricks workspace is the following code snippet, which instructs the Databricks SDK for Python to use its default authentication flow:

[![](https://imgs.search.brave.com/596ajVeh5jU5BJgjOV5SaTVEruR7ZfVHN3WQvY_tKb0/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9hdmF0/YXJzLmdpdGh1YnVz/ZXJjb250ZW50LmNv/bS91LzQ5OTgwNTI_/cz00MDAmYW1wO3Y9/NA)](https://github.com/databricks/databricks-sdk-py)

**Starred** by 532 users

**Forked** by 191 users

**Languages** Python

[![](https://imgs.search.brave.com/596ajVeh5jU5BJgjOV5SaTVEruR7ZfVHN3WQvY_tKb0/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9hdmF0/YXJzLmdpdGh1YnVz/ZXJjb250ZW50LmNv/bS91LzQ5OTgwNTI_/cz00MDAmYW1wO3Y9/NA)](https://github.com/databricks/databricks-sdk-py)[REST API to query Databricks table - Stack Overflow](https://stackoverflow.com/questions/73097372/rest-api-to-query-databricks-table)[Update: April 2023rd. There is a new SQL Execution API for querying Databricks SQL tables via REST API.](https://stackoverflow.com/questions/73097372/rest-api-to-query-databricks-table)

[

It's possible to use Databricks for that, although it heavily dependent on the SLAs - how fast should be response. Answering your questions in order:

1. There is no standalone API for execution of queries and getting back results (**yet**). But you can create a thin wrapper using one of the drivers to work with Databricks: Python, Node.js, Go, or JDBC/ODBC.
2. Response time heavily dependent on the size of the data, and if the data is already cached on the nodes, and other factors (partitioning of the data, data skipping, etc.). Databricks SQL Warehouses are also able to cache results of queries execution so they won't reprocess the data if such query was already executed.
3. Storing data in operational databases is also one of the approaches that often used by different customers. But it heavily dependent on the size of the data, and other factors - if you have huge gold layer, then SQL databases may also not the best solution from cost/performance perspective.
4. For such queries it's recommended to use Databricks SQL that is more cost efficient that having always running interactive cluster. Also, on some of the cloud platforms there is already support for serverless Databricks SQL, where the startup time is very short (seconds instead of minutes), so if your queries to gold layer doesn't happen very often, you may have them configured with auto-termination, and pay only when they are used.
](https://stackoverflow.com/questions/73097372/rest-api-to-query-databricks-table)

[

There is a new release that now makes 1. possible.

Here is the documentation: https://docs.databricks.com/sql/api/sql-execution-tutorial.html

Here is a python example:

```
import os
import requests
import json

db_token = os.environ.get('DATABRICKS_TOKEN')

# set databricks host
db_host = "https://<your databricks host>.databricks.com"

# sql query
warehouse_id = '<your sql warehouse id>'
query = "SELECT * from some_table;"

query_resp = requests.post(db_host + "/api/2.0/sql/statements", headers={"Authorization": "Bearer " + db_token}, data=json.dumps({"statement": query, "warehouse_id": warehouse_id}))
print(query_resp.status_code)
print(query_resp.json()['result']['data_array'][0])
```

](https://stackoverflow.com/questions/73097372/rest-api-to-query-databricks-table)

[

Workspace Client — Databricks SDK for Python beta documentation

](https://databricks-sdk-py.readthedocs.io/en/latest/clients/workspace.html)

**This is an evolving API that facilitates the addition and removal of widgets from existing dashboards within the Databricks Workspace**.... In general, there is little need to modify dashboards using the API.

[

Enabling Data Access with Databricks SQL REST API | Le blog de Cellenza

](https://blog.cellenza.com/en/data/enabling-data-access-with-databricks-sql-rest-api/)

June 16, 2023 - It uses an SQL warehouse, which is a kind of Spark cluster optimized for analytical workloads. **Databricks has released a public preview of REST API access for Databricks SQL** so that data does not have to be duplicated and can be accessed through...

[![](https://imgs.search.brave.com/ILurJCe2wWfic10tsCyeElXdqNZpVVP-fYonUbNuNhk/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9ibG9n/LmNlbGxlbnphLmNv/bS93cC1jb250ZW50/L3VwbG9hZHMvMjAy/My8wNi9WaWduZXR0/ZS1TUUxfRU4uanBn)](https://blog.cellenza.com/en/data/enabling-data-access-with-databricks-sql-rest-api/)

[![](https://imgs.search.brave.com/ILurJCe2wWfic10tsCyeElXdqNZpVVP-fYonUbNuNhk/rs:fit:200:200:1:0/g:ce/aHR0cHM6Ly9ibG9n/LmNlbGxlbnphLmNv/bS93cC1jb250ZW50/L3VwbG9hZHMvMjAy/My8wNi9WaWduZXR0/ZS1TUUxfRU4uanBn)](https://blog.cellenza.com/en/data/enabling-data-access-with-databricks-sql-rest-api/)

[Next](https://search.brave.com/search?q=is%20there%20a%20databricks%20API&offset=1&spellcheck=0)

Save