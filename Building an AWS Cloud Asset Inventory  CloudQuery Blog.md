---
title: "Building an AWS Cloud Asset Inventory | CloudQuery Blog"
source: "https://www.cloudquery.io/blog/building-cloud-asset-inventory-with-aws"
author:
  - "[[CloudQuery]]"
published: 2024-11-24
created: 2025-03-09
description: "Learn how to build a cloud asset inventory in AWS using CloudQuery, PostgreSQL, and Grafana. This guide covers setting up CloudQuery, transforming data with dbt, and visualizing cloud assets for improved security and compliance."
tags:
  - "clippings"
---
AWS

Cloud Asset Inventory

Tutorials

[Joe Karlsson](https://www.cloudquery.io/authors/joe-karlsson)

•

November 24, 2024

Are you experiencing challenges in managing your AWS infrastructure? Do you need help keeping track of all your cloud assets, ensuring compliance, and maintaining security? If these issues sound familiar, then it's time to consider implementing a cloud asset inventory.

Managing assets in cloud environments like AWS is becoming increasingly complex. As organizations scale their cloud infrastructure, keeping track of all resources, ensuring compliance, and maintaining robust security measures become more challenging. The dynamic nature of cloud environments, with frequent changes and additions, further complicates asset management. This is where a comprehensive cloud asset inventory becomes indispensable, providing a clear and organized view of all cloud resources, helping to streamline operations and mitigate potential risks.

In this tutorial, you will build a cloud asset manager for AWS using [CloudQuery](https://www.cloudquery.io/). You’ll connect to your AWS account, collect data on all your cloud assets, and store it in a PostgreSQL database for analysis and reporting. However, with CloudQuery, you can extract data from [ANY data source](https://hub.cloudquery.io/plugins/source) ([Azure](https://hub.cloudquery.io/plugins/source/cloudquery/azure/latest/docs), [GCP](https://hub.cloudquery.io/plugins/source/cloudquery/gcp/latest/docs), [etc](https://hub.cloudquery.io/plugins/source).) and load it into [ANY data destination](https://hub.cloudquery.io/plugins/destination) ([Snowflake](https://hub.cloudquery.io/plugins/destination/cloudquery/snowflake/latest/docs), [BigQuery](https://hub.cloudquery.io/plugins/destination/cloudquery/bigquery/latest/docs), [Databricks](https://hub.cloudquery.io/plugins/destination/cloudquery/databricks/latest/docs), [DuckDB](https://hub.cloudquery.io/plugins/destination/cloudquery/duckdb/latest/docs), [Clickhouse](https://hub.cloudquery.io/plugins/destination/cloudquery/clickhouse/latest/docs), etc.).

### What is a Cloud Asset Inventory? #

The core of any Cloud Asset Management solution is a Cloud Asset Inventory. Fundamentally, a Cloud Asset Inventory is a centralized database of all the cloud assets you’re paying for.

A Cloud Asset Inventory is constructed by collecting information from the various Cloud Platform APIs (e.g. AWS, Google Cloud, Azure, etc.) and storing it in an accessible format, such as a SQL database. You can learn more about Cloud Asset Inventories here: [https://www.cloudquery.io/blog/what-is-a-cloud-asset-inventory](https://www.cloudquery.io/blog/what-is-a-cloud-asset-inventory)

#### Why Do You Need a Cloud Asset Inventory? #

A Cloud Asset Inventory enables engineers to identify, preempt, and mitigate a wide array of issues while simultaneously allowing them to perform risk and impact assessments quickly. They also enable otherwise complicated and expensive requests, such as identifying the source of a cost spike (in both simple single-cloud/single-account and complicated multi-cloud/multi-account platforms). Cloud Asset Inventories can help deliver:

- Improved Security: By maintaining a comprehensive inventory of cloud assets, organizations can quickly identify and address security vulnerabilities. This proactive approach helps in mitigating potential threats before they escalate.
- Compliance: Ensuring that all cloud resources comply with regulatory and internal policies is crucial. A cloud asset inventory helps in tracking compliance status and generating audit-ready reports.
- Cost Management: Understanding where and how resources are being utilized allows for better cost management. Organizations can identify underutilized assets, optimize resource allocation, and reduce unnecessary expenditures.
- Operational Efficiency: Streamlining the management of cloud resources enhances operational efficiency. Automated tracking and reporting reduce the manual effort required for asset management, allowing engineers to focus on more strategic tasks.

### Building an AWS Cloud Asset Inventory #

Let’s break down the tech stack and architecture of this project, and I’ll explain why we’re using each component.

If you want to follow along with a video version of this post, you can check that out here:

[

![Live Coding: Building a Multi-Cloud Asset Inventory with AWS & GCP using CloudQuery and Postgres YouTube Video](https://www.cloudquery.io/_next/image?url=https%3A%2F%2Fwww.cloudquery.io%2Fimages%2Fblog%2Fcomplete-guide-building-multi-cloud-asset-inventory%2Fvideo-thumbnail.png%3FomitLightbox%3Dtrue&w=3840&q=75)

](https://www.youtube.com/embed/nFA2C5JgjPw)

### Step 0: Prerequisites #

Before jumping into the demo, you’ll need a few prerequisites to ensure everything runs smoothly. These setup steps will prepare your environment to sync cloud data from AWS and GCP into PostgreSQL.

#### 1. AWS Access #

You will need AWS credentials to pull cloud asset data from AWS. You can check out all the ways to authenticate with AWS [here](https://hub.cloudquery.io/plugins/source/cloudquery/aws/latest/docs#authentication).

#### 3. Docker #

We’ll be using [Docker](https://www.docker.com/) to run a PostgreSQL container where cloud assets from AWS will be stored. Make sure Docker is installed and running on your local machine before proceeding with the demo.

#### Step 1: Installing CloudQuery #

The first step is to install CloudQuery, which will act as the engine for pulling in cloud asset data. CloudQuery is open-source, which means it’s free to use and easy to extend if needed. It supports a wide range of cloud providers, and in our case, we'll focus on AWS.

To get started, install CloudQuery using Homebrew:

```
brew install cloudquery/tap/cloudquery
```

After the installation, you’ll need to log in using your CloudQuery credentials:

```
cloudquery login
```

This login gives CloudQuery access to your cloud accounts and allows it to pull in asset data. Once logged in, you’re ready to start pulling in cloud data.

Note: If you have any questions or encounter an issue when following along with this post, the best place to get help is to join the [CloudQuery Community](https://community.cloudquery.io/).

#### Setting Up PostgreSQL as the Data Store for AWS Cloud Asset Data #

Now, we need a place to store all this data. We’ll use PostgreSQL, a powerful (and popular) open-source database that works great for storing structured data like cloud assets.

If you don’t already have a PostgreSQL database set up, you can easily run one in a Docker container. This is a fast way to get things running without much setup. Here’s the command to start PostgreSQL in Docker:

```
docker run --name postgres_container \--restart unless-stopped \--env POSTGRES_USER=postgres \--env POSTGRES_PASSWORD=postgres \--env POSTGRES_HOST=db \--env POSTGRES_DB=asset_inventory \--publish 5432:5432 \--volume pgdata:/var/lib/postgresql/data \postgres
```

This command will launch a PostgreSQL pre-configured container to store your cloud assets. The credentials are set to Postgres for both the username and password, but you can adjust this as needed.

Note: While PostgreSQL is used in this example, any compatible database can be used as the data store for your AWS Cloud Asset data. PostgreSQL is chosen for its robustness and widespread adoption, but you can configure your setup to use another database system if preferred.

### Step 3: Configuring CloudQuery for AWS #

Next, we’ll configure CloudQuery to pull data from AWS and sync it to PostgreSQL. CloudQuery works by defining sources (like AWS) and destinations (like PostgreSQL). It then automates the process of syncing data between them.

Start by initializing a CloudQuery project for AWS:

```
cloudquery init --source=aws --destination=postgresql
```

This command sets up the necessary configurations for pulling data from AWS and storing it in PostgreSQL. The configurations are defined in a YAML file that CloudQuery generates for you. In our case, we’re targeting AWS S3 buckets, but CloudQuery supports many other AWS resources like EC2 instances, security groups, and more.

Now, let’s take a quick look at how we can define this process. Here’s a basic example of what the configuration file looks like (`aws_to_postgresql.yaml`):

```
kind: source
spec:# Source spec sectionname: aws
path: cloudquery/aws
registry: cloudquery
version:'v28.1.0'tables:['aws_s3_buckets']destinations:['postgresql']---kind: destination
spec:name:'postgresql'path:'cloudquery/postgresql'registry:'cloudquery'version:'v8.6.4'write_mode:'overwrite-delete-stale'
```

This file tells CloudQuery to pull in AWS S3 buckets and store them in the PostgreSQL database running on localhost.

Note: If you are interested in building a multi-cloud asset inventory, you can pull assets from [any cloud provider](https://hub.cloudquery.io/plugins/source), including [Azure](https://hub.cloudquery.io/plugins/source/cloudquery/azure/latest/docs) and [GCP](https://hub.cloudquery.io/plugins/source/cloudquery/gcp/latest/docs), using CloudQuery.

### Step 4: Syncing Data from AWS #

With our configuration in place, we’re ready to start syncing data.

To sync AWS data into PostgreSQL, run the following command:

```
cloudquery sync aws_to_postgresql.yaml
```

This will kick off the process of pulling S3 bucket data from AWS and storing it in your PostgreSQL database.

Now that we have data in PostgreSQL, let’s run a simple query to list the first 10 EC2 instances in the database:

```
dockerexec -it postgres_container psql -U postgres -d asset_inventory -c 'SELECT name, region FROM aws_ec2_instances LIMIT 10;'
```

#### How to Use dbt to Transform AWS Data into a Cloud Asset Inventory #

dbt (Data Build Tool) is used here to transform your raw AWS data into structured tables. These tables are then ready to be consumed by visualization tools for easier data interpretation and analysis. This process is fully customizable, allowing you to tailor the transformations to fit your specific AWS configuration and requirements.

To simplify data transformations, CloudQuery provides several pre-built dbt projects, including security and compliance frameworks like PCI\_DSS, CIS, and Foundational Security Best Practices. But for this tutorial, you will be using our prebuilt [AWS Asset Inventory](https://hub.cloudquery.io/addons/transformation/cloudquery/aws-asset-inventory/latest/docs) transformation. Here’s how you set up your dbt Transformations:

Go to the [AWS Asset Inventory pack](https://hub.cloudquery.io/addons/transformation/cloudquery/aws-asset-inventory/latest/docs), and download and extract the contents into your project folder.

Finally, you need to define the `dbt-profiles.yml` file itself in your project directory:

```
config:send_anonymous_usage_stats:Falseuse_colors:True
aws_asset_inventory:target: postgres
outputs:postgres:type: postgres
host:"{{ env_var('POSTGRES_HOST') }}"user:"{{ env_var('POSTGRES_USER') }}"pass:"{{ env_var('POSTGRES_PASSWORD') }}"port:5432dbname:"{{ env_var('POSTGRES_DB') }}"schema: public
threads:1
```

To run dbt with Docker, you can use this Docker CLI command to set up the environment and execute dbt commands.

```
docker run --platform linux/amd64 --name dbt_container \  --env POSTGRES_USER=postgres \  --env POSTGRES_PASSWORD=postgres \  --env POSTGRES_HOST=db \  --env POSTGRES_DB=asset_inventory \  --volume $(pwd)/cloudquery_transformation_aws-asset-inventory_vX.X.X:/usr/app \  --volume $(pwd)/dbt-profiles.yml:/root/.dbt/profiles.yml \  ghcr.io/dbt-labs/dbt-postgres:1.8.1 run
```

Note: If you’re copying this sample directly into your Docker Compose file, make sure you set the version number to match the one you’ve downloaded.

What Happens When You Run This Command?

•    Docker pulls the specified dbt image from GitHub Container Registry. •    A new container starts, named dbt\_container, with the specified environment variables. •    Local directories and files are mapped to directories and files inside the container, making your dbt project and configuration available to dbt. •    dbt runs the dbt run command inside the container, which processes your data models and executes them against the connected PostgreSQL database.

#### Running Grafana to visualize your AWS Cloud Asset Data #

Grafana is used to visualize and monitor the transformed AWS data stored in the PostgreSQL database. It allows you to create interactive and customizable dashboards to make sense of your data, providing insights through charts, graphs, and alerts.

Note: While Grafana is used here, you can use any visualization platform that suits your needs, such as Tableau, Power BI, or Kibana, depending on your specific requirements and preferences.

You can set up your Grafana instance by running the following command:

```
docker run --name grafana_container \  --restart unless-stopped \  --platform linux/amd64 \  --volume grafana:/var/lib/grafana \  --publish 3000:3000 \  grafana/grafana
```

### Feeding your AWS Cloud Asset Inventory Data into Grafana for Visualization #

Using Grafana to visualize your cloud asset inventory data not only makes it easier to monitor compliance and security but also enhances your ability to present critical information in a clear and actionable manner. This setup ensures that you can maintain a high level of oversight and continually improve your cloud asset inventory.

Now, let’s set up a dynamic dashboard in Grafana that pulls information from our PostgreSQL database.

1. Select and Download Pre-Built Dashboards

1. Visit the [CloudQuery Hub](https://hub.cloudquery.io/addons/visualization/) and browse through the range of pre-built dashboards.
2. Since you are working with AWS in this tutorial, select the [AWS Asset Inventory](https://hub.cloudquery.io/addons/visualization/cloudquery/aws-asset-inventory/latest/docs) visualization pack.
3. Click “Download Now” and extract the zip file to your project folder.
2. Access Grafana

1. The Grafana instance launched by our Docker Compose setup should be accessible at [http://localhost:3000](http://localhost:3000/).
2. If you haven’t done so already, you may need to set a password for the admin account before proceeding.

1. Note: The default Grafana username is admin and the default password is admin.
3. Import the Dashboard

1. In Grafana, open the hamburger menu (three horizontal lines) in the top left corner and select “Dashboards”.
2. Click the blue “New” button on the top right, then select “Import”.
3. Navigate to the extracted zip file directory and locate `aws_asset_inventory/grafana/asset_inventory.json`.
4. Drag this file into the “Upload dashboard JSON file” area and click “Import”.
5. This will load your dashboard.
6. Note: You might need to add the data source in Grafana to connect to your PostgreSQL database.

Using a pre-built dashboard is a great start, but one of the key benefits of Grafana is its flexibility to create custom visualizations that meet your specific needs.

### Conclusion #

In this tutorial, you walked through the process of building a cloud asset inventory for AWS using CloudQuery. Here’s a quick recap of what you achieved:

- Setting up CloudQuery: You configured CloudQuery to connect to your AWS account and gather detailed asset data.
- Storing Data in PostgreSQL: You set up a PostgreSQL database to store the collected asset data, enabling efficient querying and analysis.
- Transforming Data with dbt: You utilized dbt to apply data transformations, enhancing the quality and usability of your cloud asset inventory.
- Visualizing Data in Grafana: You imported pre-built dashboards into Grafana, allowing you to visualize and monitor your AWS assets dynamically.

By using CloudQuery, you can ensure that your asset inventory is comprehensive, adaptable, and integrated with your broader data strategy. This empowers your team to gain better insights and make informed decisions, ultimately driving more value from your cloud infrastructure.

Ready to dive deeper? You can try out CloudQuery locally with our [quick start guide](https://docs.cloudquery.io/docs/quickstart/macOS) or explore [the CloudQuery Platform](https://cloud.cloudquery.io/) (currently in beta) for a more scalable solution.

Want help getting started? Join the [CloudQuery community](https://community.cloudquery.io/) to connect with other users and experts, or message our team directly [here](https://www.cloudquery.io/contact-us) if you have any questions.

Thank you for following along, and we hope this guide helps you effectively manage your AWS cloud assets!

### Additional Resources #

- [Google Cloud Asset Inventory 101](https://www.youtube.com/embed/c0LVkrTLmVY)
- [What is a Cloud Asset Inventory?](https://www.cloudquery.io/blog/what-is-a-cloud-asset-inventory)
- [Cloud Asset Inventory with AWS Quicksight](https://www.cloudquery.io/blog/cloud-asset-inventory-cloudquery-aws-quicksight)
- [Build an AWS Cloud Asset Inventory](https://www.youtube.com/embed/H5RpX5z4H40)

### FAQs #

Q: What is a Cloud Asset Inventory?

A: A Cloud Asset Inventory is a centralized database that tracks all cloud resources and assets within an organization’s cloud environment, such as AWS. It helps in monitoring, managing, and securing these assets effectively.

Q: Why do I need a Cloud Asset Inventory for my AWS environment?

A: An asset inventory helps improve security, ensure compliance, manage costs, and enhance operational efficiency by providing a comprehensive view of all cloud resources.

Q: What is CloudQuery and how does it help with Cloud Asset Inventory?

A: CloudQuery is a tool that collects and normalizes cloud infrastructure data from AWS and other cloud providers. It helps in building a cloud asset inventory by gathering detailed information about cloud resources.

Q: How do I set up CloudQuery to gather AWS asset data?

A: You need to configure CloudQuery with your AWS credentials and specify the resources you want to inventory. This setup involves creating a configuration file and running CloudQuery to sync data from AWS.

Q: What are the prerequisites for setting up a Cloud Asset Inventory with CloudQuery?

A: Basic knowledge of AWS, SQL, and command-line interface is required. You also need an AWS account with the necessary permissions and PostgreSQL installed locally.

Q: How do I store collected asset data in PostgreSQL?

A: CloudQuery can be configured to export collected data directly into a PostgreSQL database. This involves setting up PostgreSQL credentials and specifying the target database schema.

Q: How do I use dbt to transform AWS asset data into a Cloud Asset Inventory?

A: You can use pre-built dbt projects provided by CloudQuery to apply data transformations. This involves downloading the transformation pack, updating the Docker Compose file, and running dbt commands.

Q: How does CloudQuery address the limitations of traditional asset inventory solutions?

A: CloudQuery provides a highly customizable solution that allows organizations to build their own asset inventories using their existing data warehouses and BI tools. This flexibility enables deeper insights, better integration with existing data, and reduces costs.

Q: Can CloudQuery work with existing data warehouse and BI tools?

A: Yes, CloudQuery can integrate seamlessly with your current stack of data warehouse and BI tools. This allows you to drive more insights by combining infrastructure data with other business data and leveraging the expertise of your existing tech team.

Q: What is an infrastructure data lake and how does it relate to CloudQuery?

A: [An infrastructure data lake](https://docs.cloudquery.io/docs/glossary/what-is-infrastructure-data-lake) is a concept where all infrastructure-related data is collected and stored in a centralized repository for analysis. CloudQuery supports this idea by enabling organizations to gather and analyze comprehensive infrastructure data within their data warehouses.

### Code #
#### CloudQuery #

`config.yml`

```
kind: source
spec:# Source spec sectionname: aws
path: cloudquery/aws
registry: cloudquery
version:'v26.9.0'tables:['aws_apigateway_rest_api_stages','aws_apigatewayv2_api_stages','aws_apigatewayv2_api_routes','aws_autoscaling_groups','aws_codebuild_projects','aws_config_configuration_recorders','aws_cloudwatch_alarms','aws_cloudtrail_trail_event_selectors','aws_cloudwatchlogs_metric_filters','aws_cloudfront_distributions','aws_iam_accounts','aws_iam_credential_reports','aws_iam_password_policies','aws_iam_users','aws_ec2_network_acls','aws_ec2_security_groups','aws_efs_access_points','aws_elasticbeanstalk_environments','aws_elbv1_load_balancers','aws_elbv2_load_balancers','aws_rds_clusters','aws_sns_subscriptions','aws_s3_accounts',]destinations:['postgresql']spec:---kind: destination
spec:name:'postgresql'path:'cloudquery/postgresql'registry:'cloudquery'version:'v8.0.8'spec:connection_string:'postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:5432/${POSTGRES_DB}?sslmode=disable'
```

#### dbt #

dbt-profiles.yml

```
config:send_anonymous_usage_stats:Falseuse_colors:True
aws_asset_inventory:target: postgres
outputs:postgres:type: postgres
host:"{{ env_var('POSTGRES_HOST') }}"user:"{{ env_var('POSTGRES_USER') }}"pass:"{{ env_var('POSTGRES_PASSWORD') }}"port:5432dbname:"{{ env_var('POSTGRES_DB') }}"schema: public
threads:1
```

[![Joe Karlsson](https://www.cloudquery.io/_next/image?url=%2Fimages%2Fpeople%2Fjoekarlsson.jpg&w=256&q=75)](https://www.cloudquery.io/authors/joe-karlsson)

## Written by [Joe Karlsson](https://www.cloudquery.io/authors/joe-karlsson)

Joe Karlsson (He/They) is an Engineer turned Developer Advocate (and massive nerd). Joe empowers developers to think creatively when building applications, through demos, blogs, videos, or whatever else developers need.