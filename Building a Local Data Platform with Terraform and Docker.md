---
title: "Building a Local Data Platform with Terraform and Docker"
source: "https://p-munhoz.github.io/blog/data-engineering/building-local-data-platform-terraform-docker?utm_source=tldrdata"
author:
  - "[[Pierre Munhoz]]"
published: 2025-05-21
created: 2025-05-26
description: "A step-by-step guide to building a fully local, cloud-like data platform using Terraform, Docker, Airflow, and more."
tags:
  - "clippings"
---
## Introduction

Ever wanted to experiment with a modern data stack but didn’t want to spend money on cloud resources? In this article, I’ll walk through my recent project: a **local data platform** built entirely with Terraform and Docker that replicates cloud architecture patterns for free.

## Why I Built This

As a data engineer, I regularly work with cloud-based data platforms that can cost hundreds or thousands of dollars per month. These platforms are great for production, but for learning, experimentation, and even some development work, they’re overkill.

What if we could replicate the core architecture patterns locally?

That’s exactly what this project does. I wanted a playground to experiment with infrastructure as code (IaC) patterns for data platforms. The goal was to create something that:

1. **Costs nothing** to run (leveraging local resources)
2. **Mirrors real-world architecture** found in cloud environments
3. **Integrates popular open-source tools** for data engineering
4. **Demonstrates IaC principles** with Terraform
5. **Provides hands-on experience** with event-driven architectures

The beauty of this approach is that it creates a realistic environment for developing data pipelines without the cloud costs. It’s perfect for:

- **Learning data engineering concepts** in a practical setting
- **Prototyping pipelines** before deploying to production
- **Teaching others** about modern data stack components
- **Testing infrastructure changes** safely

Let’s dive into how this works!

## 🔍 Key Technologies Explained

Here’s a quick rundown of the core tools used in this project:

- [Docker](https://www.docker.com/): A containerization platform that packages code and dependencies together so applications run consistently in any environment.
- [Terraform](https://developer.hashicorp.com/terraform): An infrastructure-as-code (IaC) tool that lets you define and provision infrastructure (like networks, containers, and volumes) using declarative configuration files.
- [Airflow](https://airflow.apache.org/): A workflow orchestration tool that lets you define, schedule, and monitor data pipelines using Python code (called DAGs).
- [Minio](https://min.io/): An open-source object storage server that’s API-compatible with Amazon S3. It’s great for storing files like raw and processed data locally.
- [LocalStack](https://www.localstack.cloud/): A fully functional local AWS cloud emulator. In this project, it simulates SQS (Simple Queue Service) to support event-driven workflows without needing an AWS account.
- [DuckDB](https://duckdb.org/): A lightweight analytical SQL database optimized for OLAP workloads. Think of it as SQLite for analytics — perfect for local data warehousing and fast queries.
- [Pandas](https://pandas.pydata.org/): A popular Python library for data manipulation and analysis. Used here in the ETL step to transform CSV data.
- [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html): The official AWS SDK for Python. It interacts with Minio and LocalStack just like it would with AWS S3 or SQS, using the same API.

## The Architecture: Deep Dive

Here’s what the architecture looks like:

```
User / DAG Trigger
   |
   v
Airflow DAG
   |
   |--> Upload CSV to Minio (S3 alternative)
   |--> Load raw CSV to DuckDB
   |--> [Triggered via SQS] Run Docker ETL
   |--> Load transformed data to DuckDB
```

The beauty of this setup is that each component mimics a cloud service, creating a fully functional data pipeline:

| What I Needed | Cloud Service | Local Alternative | Why This Works |
| --- | --- | --- | --- |
| Object Storage | AWS S3 | Minio | API-compatible S3 alternative |
| Event-Driven Compute | AWS Lambda | Docker Containers | Containerized functions with similar lifecycle |
| Workflow Orchestration | MWAA / Airflow | Dockerized Airflow | Same tool, just running locally |
| Message Queue | SQS/SNS | LocalStack | Emulates AWS services API locally |
| Analytical Database | Redshift / BigQuery | DuckDB | Columnar storage with SQL interface |

Let’s break down each component:

### 1\. Minio: S3-Compatible Object Storage

Minio is an open-source object storage server that implements the Amazon S3 API. In my setup, Minio stores:

- Raw CSV files uploaded through the Airflow DAG
- Transformed data processed by our ETL container

The beauty of using Minio is that it works with the exact same boto3 S3 client code you’d use with real AWS S3. This means our code remains cloud-compatible with minimal changes.

You can read the [Minio documentation here](https://min.io/docs/minio/linux/operations/installation.html).

### 2\. Airflow: Workflow Orchestration

Airflow serves as the brain of our operation, coordinating when and how data flows through the system. I’ve configured it with two primary DAGs:

- A data upload pipeline that moves CSVs to Minio and loads them into DuckDB
- An event-listener that polls SQS for messages and triggers ETL jobs

The Docker-based setup includes volume mounts for both DAGs and data, allowing for easy code changes without rebuilding containers.

You can read the [Airflow documentation here](https://airflow.apache.org/docs/).

### 3\. LocalStack: Emulating AWS Services

LocalStack provides a local emulation of AWS services. In this project, I’m using it to create a functional SQS queue that:

- Accepts messages that trigger ETL processes
- Maintains the queue state between runs
- Supports standard AWS CLI and SDK interactions

This component is crucial for demonstrating event-driven architectures without actual AWS costs.

You can read the [LocalStack documentation here](https://docs.localstack.cloud/overview/).

### 4\. Docker Containers: Pseudo-Lambda Functions

Instead of using AWS Lambda for compute, I’m using Docker containers that:

- Run a specific task (our Python ETL code)
- Execute quickly and terminate when complete
- Can be triggered by events (SQS messages)
- Accept environment variables for configuration

This approach mimics serverless functions while giving us complete control over the runtime environment.

You can read the [Docker documentation here](https://docs.docker.com/).

### 5\. DuckDB: Analytical Database

For our data warehouse, I chose DuckDB because:

- It’s lightweight yet powerful for analytical queries
- Stores data in columnar format similar to cloud data warehouses
- Requires no server setup (perfect for local development)
- Has native Python integration

You can read the [DuckDB documentation here](https://duckdb.org/docs/stable/).

## Infrastructure as Code with Terraform: Explained

The entire platform is defined using Terraform, making it reproducible and version-controlled. Let’s dive deeper into how this works.

But why Terraform is that such a big deal in Data Engineering and DevOps?

In the past, infrastructure was manually configured — spinning up EC2s, setting up S3 buckets, clicking around in cloud consoles. That works for a quick test… but it quickly becomes unmanageable, especially when teams grow or systems evolve.

With Terraform, your infrastructure is:

- Declarative: You describe what you want, and Terraform figures out how to make it real.
- Versioned: Infra changes live in git, just like code. You can review them, roll them back, and collaborate safely.- Reproducible: A single terraform apply can spin up your entire stack from scratch — dev, staging, or demo environments.
- Cloud-agnostic: You can use the same tool to provision AWS, GCP, Azure… or in this case, Docker containers on your machine.

For data engineers, this matters a lot. Our workflows depend on storage, compute, and orchestration tools being correctly wired together. With Terraform, we avoid config drift, manual mistakes, and “it works on my machine” syndrome.

### Modular Project Structure

I’ve organized the Terraform configuration into logical modules:

```
terraform/
├── main.tf               # Main configuration that ties everything together
├── modules/
│   ├── airflow/          # Airflow orchestrator setup
│   │   ├── main.tf       # Container, image, and volume configuration
│   │   ├── terraform.tf  # Provider requirements
│   │   └── variables.tf  # Configurable inputs
│   ├── localstack/       # LocalStack for SQS
│   │   ├── main.tf       # Container configuration
│   │   ├── terraform.tf  # Provider requirements
│   │   └── variables.tf  # Configurable inputs
│   └── minio/            # Object storage
│       ├── main.tf       # Container configuration
│       ├── terraform.tf  # Provider requirements
│       └── variables.tf  # Configurable inputs
```

This modularity offers several advantages:

- **Separation of concerns**: Each component is self-contained
- **Reusability**: Modules can be shared across projects
- **Maintainability**: Easier to understand and modify specific parts
- **Isolation**: Changes to one component don’t affect others

### The Docker Network: Connecting Components

First, we need to create a dedicated Docker network that allows all our containers to communicate with each other. This is crucial because it enables containers to reach each other using predictable hostnames instead of dynamic IP addresses:

```hcl
# Create a custom Docker network for inter-container communication

# This allows containers to communicate using service names (e.g., "minio", "airflow")

# instead of having to discover and use dynamic IP addresses

 

resource "docker_network" "data_platform" {

  name = "data_platform_net"

}
```

This network enables our containers to communicate with each other using container names as hostnames (like `http://minio:9000`), which simplifies configuration. Without this network, each service would need to know the others’ IP addresses, which change each time containers restart.

### Building Custom Images

For Airflow, I use Terraform to build a custom Docker image:

```hcl
resource "docker_image" "airflow" {

  name = var.image_name

 

  build {

    context    = var.context

    dockerfile = var.dockerfile

  }

}
```

This allows me to include necessary Python dependencies like `boto3` and `duckdb` directly in the image.

### Container Configuration

Each container is configured with appropriate environment variables, ports, and volume mounts.

The Minio configuration demonstrates several key container orchestration patterns:

```hcl
resource "docker_container" "minio" {

  image = docker_image.minio.name

  name  = var.container_name

 

  # Connect to our custom network and set hostname alias

  # This allows other containers to reach Minio at "http://minio:9000"

  networks_advanced {

    name    = "data_platform_net"

    aliases = ["minio"]

  }

 

  # Port 9000: S3-compatible API (used by boto3 and applications)

  ports {

    internal = 9000

    external = 9000

  }

 

  # Port 9001: Web console UI (accessible at http://localhost:9001)

  ports {

    internal = 9001

    external = 9001

  }

 

  # Set admin credentials for accessing Minio

  env = [

    "MINIO_ROOT_USER=${var.minio_user}",

    "MINIO_ROOT_PASSWORD=${var.minio_password}"

  ]

 

  # Start Minio server with data directory and console on port 9001

  command = ["server", "/data", "--console-address", ":9001"]

 

  # Mount host directory for data persistence

  # Data survives container restarts and can be inspected from host

  volumes {

    container_path = "/data"

    host_path      = var.host_data_path

  }

}
```

This is particularly powerful because:

1. It exposes the same ports you’d use in a cloud environment
2. It mounts volumes from the host for persistence
3. It connects to our shared network for inter-container communication

## Event-Driven ETL Workflow

The real magic happens in the Airflow DAGs. I’ve built two primary workflows:

1. **Data Upload & Processing Pipeline** (`dags/upload_to_minio.py`): Upload CSV → DuckDB → ETL → Load transformed data
2. **Event-Driven ETL** (`dags/trigger_etl_from_sqs.py`): Listen to SQS queue and trigger ETL jobs based on messages

Here’s a snippet from the SQS-triggered DAG:

```python
def check_and_trigger_etl():

    # Create SQS client pointing to LocalStack instead of real AWS

    # Using the same boto3 interface ensures cloud compatibility

    sqs = boto3.client(

        "sqs",

        endpoint_url="http://localstack:4566",  # LocalStack SQS endpoint

        aws_access_key_id="test",               # Dummy credentials for LocalStack

        aws_secret_access_key="test",

        region_name="us-east-1"

    )

 

    # Get the queue URL - required for all SQS operations

    queue_url = sqs.get_queue_url(QueueName="my-etl-queue")["QueueUrl"]

    

    # Poll for messages (non-blocking check for new work)

    # MaxNumberOfMessages=1 ensures we process one job at a time

    messages = sqs.receive_message(QueueUrl=queue_url, MaxNumberOfMessages=1)

 

    # If we found a message, trigger the ETL process

    if "Messages" in messages:

        print("Message received! Triggering ETL.")

        

        # Launch ETL container (simulates AWS Lambda function)

        # Key elements:

        # --rm: Delete container when done (like Lambda's ephemeral nature)

        # -e: Pass environment variables for Minio connection

        # --network: Connect to our data platform network

        subprocess.run([

            "docker", "run", "--rm",

            "-e", "MINIO_ENDPOINT=http://minio:9000",    # Internal network address

            "-e", "AWS_ACCESS_KEY_ID=admin",             # Minio credentials

            "-e", "AWS_SECRET_ACCESS_KEY=password",

            "--network", "data_platform_net",           # Same network as other services

            "etl-transform"                             # Our custom ETL image

        ])

        

        # Clean up: delete processed messages from queue

        # This prevents reprocessing and is standard SQS pattern

        for msg in messages["Messages"]:

            sqs.delete_message(

                QueueUrl=queue_url, 

                ReceiptHandle=msg["ReceiptHandle"]  # Unique handle for this message

            )
```

This code polls an SQS queue and runs a Docker container when it receives a message - just like how AWS Lambda functions can be triggered by SQS events.

## The ETL Process: Under the Hood

Let’s examine the actual transformation logic running in our Docker container. This is where the data processing happens:

```python
import os

import boto3

import pandas as pd

 

s3 = boto3.client(

    's3',

    endpoint_url=os.environ.get("MINIO_ENDPOINT", "http://minio:9000"),

    aws_access_key_id=os.environ.get("AWS_ACCESS_KEY_ID", "admin"),

    aws_secret_access_key=os.environ.get("AWS_SECRET_ACCESS_KEY", "password"),

    region_name="us-east-1"

)

 

# Download file from Minio

s3.download_file("demo-bucket", "sample.csv", "downloaded.csv")

 

# Transform with pandas

df = pd.read_csv("downloaded.csv")

df["age_plus_10"] = df["age"] + 10

 

# Save transformed file

df.to_csv("transformed.csv", index=False)

 

# Upload back to Minio

s3.upload_file("transformed.csv", "demo-bucket", "transformed.csv")
```

While this transformation is simple (adding 10 to the age column), the pattern demonstrates several important concepts:

1. **Environment Configuration**: The script reads connection details from environment variables, allowing the same code to work in different environments
2. **S3-Compatible Operations**: We’re using boto3 just like we would with AWS, making this code cloud-ready
3. **ETL Pattern**:
	- **Extract**: Downloading the CSV from object storage
	- **Transform**: Manipulating the data with pandas
	- **Load**: Saving the result back to object storage
4. **Containerization**: By packaging this in a Docker container, we ensure consistent execution regardless of the environment

The Dockerfile for this transformation is equally important:

```dockerfile
FROM python:3.10-slim

 

WORKDIR /app

 

COPY scripts/transform.py .

 

RUN pip install pandas boto3

 

ENTRYPOINT ["python", "transform.py"]
```

This creates a lightweight image that:

- Uses a minimal Python base
- Installs only the required dependencies
- Sets the transform script as the entrypoint

The beauty of this approach is that our ETL code is:

- **Portable**: It can run anywhere Docker is available
- **Consistent**: The environment is identical every time
- **Isolated**: It doesn’t interfere with other processes
- **Scalable**: Multiple containers can run in parallel
- **Cloud-Ready**: The same container could be deployed to ECS, Kubernetes, or adapted for Lambda

## Running the Platform: Detailed Steps

Let me walk through exactly how to get this platform up and running on your local machine. The beauty of infrastructure as code is that it should “just work” on any system with the prerequisites installed.

### Prerequisites

- **Docker**: To run the containers
- **Terraform**: For deploying the infrastructure
- **AWS CLI**: For interacting with LocalStack

### Step 1: Clone the Repository

```bash
git clone https://github.com/p-munhoz/iac-data-platform.git

cd iac-data-platform
```

### Step 2: Apply Terraform Infrastructure

```bash
cd terraform

terraform init

terraform apply
```

During the `terraform apply` step, Terraform will:

1. Create a Docker network
2. Pull or build necessary Docker images
3. Start containers for Minio, Airflow, and LocalStack
4. Configure the containers with appropriate environment variables
5. Mount volumes for data persistence

This is where the magic of IaC happens - with one command we’ve created our entire data platform!

### Step 3: Access Airflow UI

Once the infrastructure is running, you can access the Airflow web interface:

- **URL**: [http://localhost:8080](http://localhost:8080/)
- **Username**: admin
- **Password**: admin

From here, you can view and trigger the DAGs we’ve created.

### Step 4: Create the SQS Queue (One-Time Setup)

This command creates our message queue in LocalStack, demonstrating how we can use standard AWS CLI commands with local services:

```bash
# Set dummy AWS credentials (required by AWS CLI but not validated by LocalStack)

AWS_ACCESS_KEY_ID=test \

AWS_SECRET_ACCESS_KEY=test \

# Use AWS CLI with LocalStack endpoint instead of real AWS

aws --endpoint-url=http://localhost:4566 \

    sqs create-queue \

    --queue-name my-etl-queue \    # Name used by our Airflow DAG

    --region us-east-1              # Required by AWS CLI
```

Notice how we’re specifying the LocalStack endpoint while using standard AWS CLI commands - this is what makes LocalStack so powerful for development.

### Step 5: Triggering Workflows

You have two options for triggering the data processing:

#### Option A: Direct DAG Execution

From the Airflow UI, simply click on the “upload\_and\_duckdb” DAG and trigger it manually. This will:

1. Upload the sample CSV to Minio
2. Load it into DuckDB
3. Run the ETL transformation
4. Load the transformed data into DuckDB

#### Option B: Send a Message to SQS

To demonstrate event-driven processing, send a message to the SQS queue:

```bash
AWS_ACCESS_KEY_ID=test \

AWS_SECRET_ACCESS_KEY=test \

aws --endpoint-url=http://localhost:4566 \

     sqs send-message \

     --queue-url http://localhost:4566/000000000000/my-etl-queue \

     --message-body "trigger"
```

The Airflow DAG that polls SQS will detect this message and trigger the ETL process.

### Step 6: Verify the Results

You can verify that everything worked by:

1. **Checking Minio**: Navigate to [http://localhost:9001](http://localhost:9001/) and login with admin/password
2. **Inspecting DuckDB**: You can connect to the DuckDB file at `data/warehouse.duckdb` using DuckDB CLI or a SQL client
3. **Viewing Airflow logs**: Check the Airflow UI for execution logs

### Step 7: Tear Down (When Finished)

When you’re done experimenting, you can destroy all resources:

```bash
cd terraform

terraform destroy
```

This will remove all containers and networks, though any data in the mounted volumes will remain on your local filesystem.

## Key Takeaways

Building this project can teach you several valuable lessons about modern data architecture and IaC:

### 1\. Infrastructure as Code is Transformative

With traditional infrastructure management, recreating a development environment across different machines is error-prone and time-consuming. With this Terraform setup:

- **Reproducibility** is guaranteed - the exact same environment every time
- **Version control** applies to infrastructure, not just application code
- **Documentation** is built into the code itself
- **Collaboration** becomes easier when infrastructure is defined as code

Module-based Terraform are particularly powerful, as it allowed you to encapsulate specific components and reuse them across different projects.

### 2\. Container Networking is Crucial for Data Platforms

One of the subtle but important aspects of this project was configuring the Docker network properly:

```hcl
resource "docker_network" "data_platform" {

  name = "data_platform_net"

}
```

This dedicated network allows containers to communicate using predictable hostnames. Without this, each component would need to know the dynamic IP addresses of other services.

### 3\. Event-Driven Architecture Requires Different Thinking

Working with the SQS-triggered workflow highlighted the differences between traditional batch processing and event-driven approaches:

- **Loose coupling**: Components communicate through events, not direct calls
- **Scalability**: Easy to add new consumers without modifying producers
- **Resilience**: Messages persist even if consumers are temporarily unavailable
- **Complexity**: Need to handle idempotency, ordering, and failure scenarios

This local setup provides a perfect sandbox for experimenting with these patterns before implementing them in production.

### 4\. Emulating Cloud Services Locally Has Limitations

While the local stack works well for development, there are some limitations:

- **Performance**: Local resources are constrained compared to cloud services
- **Features**: Some advanced cloud features aren’t available in the local alternatives
- **Scale**: Can’t truly test large-scale data scenarios locally

However, these limitations are acceptable for most development and learning scenarios.

### 5\. Docker Makes ETL Consistent

Using Docker for the ETL process ensures consistent execution environments, which is critical for reproducible data transformations. The container approach offers:

- **Dependency isolation**: Each transformation has its own environment
- **Portability**: Works the same on any machine with Docker
- **Version control**: Container images can be tagged and versioned
- **Resource control**: Can limit CPU/memory allocation

This pattern is particularly useful when scaling to multiple ETL processes with different dependencies.

## Ideas for Extending the Project

There’s plenty of room to grow this platform:

- Add Prometheus + Grafana for monitoring
- Implement streaming with Kafka (via another container)
- Add proper CI/CD pipelines with GitHub Actions
- Build a simple UI to visualize the data flow
- Add dbt for transformation instead of raw Python

## Conclusion

This project demonstrates how to build a complete data platform using infrastructure as code principles - all running locally and for free. It’s a great way to learn about modern data engineering patterns without worrying about cloud costs.

The complete code is available on my [GitHub repository](https://github.com/p-munhoz/iac-data-platform.git). Feel free to clone it, extend it, and use it as a starting point for your own data engineering experiments!

---