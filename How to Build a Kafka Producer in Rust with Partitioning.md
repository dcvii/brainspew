---
title: "How to Build a Kafka Producer in Rust with Partitioning"
source: "https://dev.to/ciscoemerge/how-to-build-a-kafka-producer-in-rust-with-partitioning-3168"
author:
  - "[[Jan Schulte]]"
published: 2023-03-03
created: 2025-02-17
description: "Hero Image by Askhat Gilyakhov  In this blog post we build an Apache Kafka producer in... Tagged with rust, kafka, tracing."
tags:
  - "clippings"
---
*Hero Image by [Askhat Gilyakhov](https://enterprise.shutterstock.com/g/Askhat_Gilyakhov)*

**In this blog post we build an Apache Kafka producer in Rust,  
showcasing how you partition data for a specific topic.**

When it comes to writing producers for Kafka, writing a [simple  
producer](https://dev.to/ciscoemerge/how-to-build-a-simple-kafka-producerconsumer-application-in-rust-3pl4)  
is straightforward. With a growing amount of data, however, it becomes  
necessary to publish data in a way that allows consumers to work with it efficiently.

To showcase how to produce Kafka events, we will leverage Tokio's [tracing crate](https://github.com/tokio-rs/tracing) to generate log data.

## Setup a new Project

In this tutorial, our dev setup consists of VSCode, Rust, and Docker to build a Kafka Producer.

Let's get started with a new Rust project. In your terminal, run:  

```shell
$ cargo new tracing_publisher
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

As mentioned above, we want to use VSCode's  
[DevContainer](https://code.visualstudio.com/docs/devcontainers/containers) feature to run our Rust code, but also to run Kafka and Zookeeper.

Dev Containers require a config file in a separate directory:  

```shell
$ cd tracing_publisher
$ mkdir .devcontainer
$ cat > .devcontainer/devcontainer.json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/rust
{
  "name": "Rust",
  "service": "rust-log-processing",
  "dockerComposeFile": "../docker-compose.yml",
  "features": {
   "ghcr.io/devcontainers/features/rust:1": {}
  },
  "workspaceFolder": "/workspaces/${localWorkspaceFolderBasename}",
  "shutdownAction": "stopCompose"
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Additionally, we also need a `docker-compose.yml` file to orchestrate all Docker containers:  

```yaml
#docker-compose.yml
version: '3.8'
services:
rust-log-processing:
image: mcr.microsoft.com/devcontainers/rust:0-1-bullseye
volumes:
- ..:/workspaces:cached
  cap_add:
  - SYS_PTRACE
    security_opt:
    - seccomp:unconfined
      command: /bin/sh -c "while sleep 1000; do :; done"
zookeeper:
image: confluentinc/cp-zookeeper:7.3.0
container_name: zookeeper
environment:
ZOOKEEPER_CLIENT_PORT: 2181
ZOOKEEPER_TICK_TIME: 2000
broker:
image: confluentinc/cp-kafka:7.3.0
container_name: broker
ports:
# To learn about configuring Kafka for access across networks see
     # https://www.confluent.io/blog/kafka-client-cannot-connect-to-broker-on-aws-on-docker-etc/
     - "9092:9092"
       depends_on:
       - zookeeper
         environment:
KAFKA_BROKER_ID: 1
KAFKA_ZOOKEEPER_CONNECT: 'zookeeper:2181'
KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_INTERNAL:PLAINTEXT
KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://broker:9092,PLAINTEXT_INTERNAL://broker:29092
KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 1
KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 1
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

With these configuration files in place, let's open the project in VSCode:  

```shell
$ code .
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

\****Please Note: Once VSCode has loaded the project, it should present  
you with a message in the bottom right corner, asking if you'd like to `Open this Project in a container`:***\*

[![VSCode prompt to open project in Dev<br>
Container](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fbh2w844uamu5252r0ec1.png "open-in-container")](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fbh2w844uamu5252r0ec1.png)

Click on **Reopen in Container**. This step will take a few moments to complete, as it downloads all Docker images and installs several components into our development container.

Once VSCode finished loading, click **View > Terminal** to open the integrated Terminal. We will use this terminal session to execute all commands inside the dev container unless noted otherwise.

Before we add the first few lines of code, let's install some  
dependencies we will need (**You need to run these commands in the VSCode Terminal**):  

```shell
$ cargo add anyhow
$ cargo add kafka
$ cargo add serde_json
$ cargo add tracing
$ cargo add tracing_subscriber
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

## Collecting Telemetry Data from a Rust Program

We will build a custom tracing subscriber layer to gather telemetry data produced by the `tracing` crate. We will then send that telemetry data to Kafka.

We won't cover the actual collection mechanism in detail. This aspect is based on the work of Bryan Burgers excellent blog post on ["Custom  
Logging in Rust Using tracing and  
tracing-subscriber"](https://burgers.io/custom-logging-in-rust-using-tracing).

Before we add code, in the terminal, run:  

```shell
$ cargo run 
Hello, World!
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

to ensure everything works perfectly. Next, let's add the following code  
to `main.rs`:  

```rust
use tracing::info;
use tracing_subscriber::prelude::*;

mod custom_layer;
use custom_layer::CustomLayer;

fn main() {
    // Set up how \`tracing-subscriber\` will deal with tracing data.
    tracing_subscriber::registry().with(CustomLayer).init();

    // Log something simple. In \`tracing\` parlance, this creates an "event".
    info!(a_bool = true, answer = 42, message = "first example");
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Then, create a new module called `custom_layer.rs`:  

```rust
// Credit: https://github.com/bryanburgers/tracing-blog-post/blob/main/examples/figure_3/custom_layer.rs
use std::collections::BTreeMap;
use tracing_subscriber::Layer;

pub struct CustomLayer;

impl<S> Layer<S> for CustomLayer
where
    S: tracing::Subscriber,
{
    fn on_event(
        &self,
        event: &tracing::Event<'_>,
        _ctx: tracing_subscriber::layer::Context<'_, S>,
    ) {
        // Covert the values into a JSON object
        let mut fields = BTreeMap::new();
        let mut visitor = JsonVisitor(&mut fields);
        event.record(&mut visitor);

        // Output the event in JSON
        let output = serde_json::json!({
            "target": event.metadata().target(),
            "name": event.metadata().name(),
            "level": format!("{:?}", event.metadata().level()),
            "fields": fields,
        });
        println!("{}", serde_json::to_string_pretty(&output).unwrap());
    }
}

struct JsonVisitor<'a>(&'a mut BTreeMap<String, serde_json::Value>);

impl<'a> tracing::field::Visit for JsonVisitor<'a> {
    fn record_f64(&mut self, field: &tracing::field::Field, value: f64) {
        self.0
            .insert(field.name().to_string(), serde_json::json!(value));
    }

    fn record_i64(&mut self, field: &tracing::field::Field, value: i64) {
        self.0
            .insert(field.name().to_string(), serde_json::json!(value));
    }

    fn record_u64(&mut self, field: &tracing::field::Field, value: u64) {
        self.0
            .insert(field.name().to_string(), serde_json::json!(value));
    }

    fn record_bool(&mut self, field: &tracing::field::Field, value: bool) {
        self.0
            .insert(field.name().to_string(), serde_json::json!(value));
    }

    fn record_str(&mut self, field: &tracing::field::Field, value: &str) {
        self.0
            .insert(field.name().to_string(), serde_json::json!(value));
    }

    fn record_error(
        &mut self,
        field: &tracing::field::Field,
        value: &(dyn std::error::Error + 'static),
    ) {
        self.0.insert(
            field.name().to_string(),
            serde_json::json!(value.to_string()),
        );
    }

    fn record_debug(&mut self, field: &tracing::field::Field, value: &dyn std::fmt::Debug) {
        self.0.insert(
            field.name().to_string(),
            serde_json::json!(format!("{:?}", value)),
        );
    }
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

With this code in place, let's run it:  

```shell
$ cargo run 
{
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Info)",
   "name": "event src/main.rs:12",
   "target": "tracing_publisher"
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Now, every time we use `info!`, `warn!`, `trace!`, or `error!`, our new extension turns this event into json.

In the next step, we will use the generated JSON and produce Kafka messages from it.

## Implement a Kafka Publisher with a Partitioning Strategy

We will implement the publishing capability in a separate `impl` block `custom_layer.rs`. Before we get started with that, let's enhance the `CustomLayer` struct. Change this:  

```rust
//src/custom_layer.rs
pub struct CustomLayer;
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

to:  

```rust
//src/custom_layer.rs
use std::collections::BTreeMap;
use tracing::Level;
use tracing_subscriber::Layer;

pub struct CustomLayer {
   kafka_broker: String,
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Next, in `src/custom_layer.rs`, create a new `impl` in which we will add a `new` method, as well as our Kafka functionality:  

```rust
impl CustomLayer {
    pub fn new(kafka_broker: &str) -> Self {
         Self {
             kafka_broker: kafka_broker.into(),
         }
    }
} 
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

The initializer accepts a Kafka broker address (e.g. `broker:9092`).  
Since we're using Docker Compose, we can refer to the broker by its container name (`broker`).

`send_event` contains the most important functionality:  

```rust
use std::{collections::BTreeMap, time::Duration};
use kafka::producer::{Record, Producer, RequiredAcks};

impl CustomLayer {
   //...
   fn send_event(&self, topic: &str, log_level: &Level, serialized_event: &str) {
       let mut producer = self.create_producer();
       let partition_key = log_level.as_str();

       let record = Record {
           topic: &self.to_kafka_topic_name(topic),
           key: partition_key.to_lowercase(),
           partition: -1,
           value: serialized_event.as_bytes()
       };

       producer
           .send(&record)
           .unwrap();
   }
}

 fn to_kafka_topic_name(&self, input: &str) -> String {
     input.replace('_', "").replace("::", "-")
 }

 fn create_producer(&self) -> Producer {
     Producer::from_hosts(vec![self.kafka_broker.to_owned()])
         .with_ack_timeout(Duration::from_secs(1))
         .with_required_acks(RequiredAcks::One)
         .create()
         .unwrap()
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

`send_event` accepts a Kafka topic, the event's log level (which we will use to determine the partition) and a payload (`serialized_event`).

It creates a `Record`, a Kafka data structure, and sends it off to the broker.

## A Primer on Kafka Partitions

Kafka organizes different types of messages in **topics**. A topic is a logical separation between different types of messages. It contains a certain type of event, for instance log messages, while another might hold customer events.

Often, with a high amount of data, it makes sense to split a topic into several partitions. We do this for several reasons:

- It's easier to replicate a partition across different Kafka brokers
- It's easier to distribute the load on the consumer side

If you're curious to learn more about the details, check out [this Post](https://dev.to/ciscoemerge/what-is-kafka-event-streaming-in-a-nutshell-c4b).  
In our case, we're distributing log messages into separate partitions based on their severity.

Let's examine `send_event` in a bit more detail:  

```rust
 fn send_event(&self, topic: &str, log_level: &Level, serialized_event: &str) {
       let mut producer = self.create_producer();
       let partition_key = log_level.as_str();

       let record = Record {
           topic: &self.to_kafka_topic_name(topic),
           key: partition_key.to_lowercase(),
           partition: -1,
           value: serialized_event.as_bytes()
       };
       //...
   }
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

When we construct a new `Record`, besides providing the topic and the payload (`value`), we also specify a `key`, as well as `partition`.

Both, `key` and `partition` allow us to influence in which partition this record should end up in.

`partition: -1` tells the Kafka broker to determine the partition on its own. Since we provided a `key`, it will use the `key` to decide. `key` is an optional value. If not provided, Kafka will use a round-Robbin approach to distribute events into partitions. If we choose to provide a  
`key`, it should be related to the application's domain, such as a user id, or, in our case, the application's name.

## Publish Log Events

With all Kafka-related code in place, let's start publishing events.  
Find the `on_event` method in the `Layer` `impl` block and add a call to `send_event`:  

```rust
fn on_event(
     &self,
     event: &tracing::Event<'_>,
     _ctx: tracing_subscriber::layer::Context<'_, S>,
 ) {
     let mut fields = BTreeMap::new();
     let mut visitor = JsonVisitor(&mut fields);
     event.record(&mut visitor);

     // Output the event in JSON
     let output = serde_json::json!({
         "target": event.metadata().target(),
         "name": event.metadata().name(),
         "level": format!("{:?}", event.metadata().level()),
         "fields": fields,
         "timestamp": SystemTime::now().duration_since(UNIX_EPOCH).unwrap().as_secs()
     });
     //add this line
     let serialized_event = serde_json::to_string_pretty(&output).unwrap();
     println!("{}", serialized_event);
     //add this line
     self.send_event(event.metadata().target(), event.metadata().level(), &serialized_event);
 }
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

From now on, every time we intercept a `tracing` event, it will get sent to Kafka.

Before we can start running the program, we need a little bit of configuration in `main.rs`:  

```rust
use tracing::info;
use tracing_subscriber::prelude::*;

mod custom_layer;
use custom_layer::CustomLayer;

fn main() {
    // Set up how \`tracing-subscriber\` will deal with tracing data.
    //change this line
    tracing_subscriber::registry().with(CustomLayer::new("broker:9092")).init();

    // Log something simple. In \`tracing\` parlance, this creates an "event".
    info!(a_bool = true, answer = 42, message = "first example");
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

If we run our code now, we will see the following output:  

```shell
$ cargo run
{
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Info)",
   "name": "event src/main.rs:12",
   "target": "tracing_publisher"
 }
 thread 'main' panicked at 'called \`Result::unwrap()\` on an \`Err\` value: Kafka(UnknownTopicOrPartition)', src/custom_layer.rs:35:32
 note: run with \`RUST_BACKTRACE=1\` environment variable to display a backtrace
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Our program fails because we haven't created the Kafka topic yet. While Kafka can be configured to create topics on an ad-hoc basis, we will create the topic manually.

## Configure Kafka

Before we create the topic, let's quickly discuss how our code determines topic names.  

```rust
fn on_event(
    &self,
    event: &tracing::Event<'_>,
    _ctx: tracing_subscriber::layer::Context<'_, S>,
) {
    // Covert the values into a JSON object
    let mut fields = BTreeMap::new();
    let mut visitor = JsonVisitor(&mut fields);
    event.record(&mut visitor);

    // Output the event in JSON
    let output = serde_json::json!({
        "target": event.metadata().target(),
        "name": event.metadata().name(),
        "level": format!("{:?}", event.metadata().level()),
        "fields": fields,
    });
    let serialized_event = serde_json::to_string_pretty(&output).unwrap();
    println!("{}", serialized_event);
    self.send_event(
        event.metadata().target(), //This is our topic name
        event.metadata().level(),
        &serialized_event,
    );
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

The `send_event` method accepts a topic name as argument. In `on_event`, we provide `event.metadata().target()` as our topic name. `target` contains the application's name: `tracing_publisher`. After processing the name via `to_kafka_topic`, our topic name will be `tracingpublisher`.

If we had more applications sending log data, we would want to separate data per application, therefore we create a topic dedicated to a single application.

Let's create the topic. **In a terminal on your host machine**, run the following command to create a topic and two partitions:  

```shell
$ docker exec broker \
   kafka-topics --bootstrap-server broker:9092 \
             --create \
             --topic tracingpublisher --partitions 2
 Created topic tracingpublisher.
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

With that out of the way, let's try running the code again (**Run this command in the VSCode terminal**):  

```shell
$ cargo run
{
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Info)",
   "name": "event src/main.rs:12",
   "target": "tracing_publisher"
 }
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Now we don't see any additional output. To verify it worked, let's use [`kafkacat`](https://github.com/edenhill/kcat) to consume the topic's events. (We install `kafkacat` in the Dev Container. Please run the following command in VSCode's terminal)  

```shell
$ sudo apt-get update && sudo apt-get install -y kafkacat
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

(Note: `kafkacat` got renamed to `kcat`. We refer to the old name because the dev container's package sources haven't updated to the new name yet).

Let's run `kafkacat` in Consumer mode and listen to the  
`tracingpublisher` topic:  

```shell
$ kafkacat -C -b broker:9092 -t tracingpublisher 
 {
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Info)",
   "name": "event src/main.rs:12",
   "target": "tracing_publisher"
 }
 % Reached end of topic tracingpublisher [0] at offset 1
 % Reached end of topic tracingpublisher [1] at offset 0   
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Now we see our event. But what about the partitions? When we created the topic, we created two partitions.

Let's update our main function and re-run everything again.  

```rust
use tracing::{info, warn}; //update imports
use tracing_subscriber::prelude::*;

mod custom_layer;
use custom_layer::CustomLayer;

fn main() {
    // Set up how \`tracing-subscriber\` will deal with tracing data.
    tracing_subscriber::registry().with(CustomLayer::new("broker:9092")).init();

    // Log something simple. In \`tracing\` parlance, this creates an "event".
    info!(a_bool = true, answer = 42, message = "first example");
    //add this line 
    warn!(a_bool = true, answer = 42, message = "first example"); 
}
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Let's run the program again:  

```shell
$ cargo run
 {
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Info)",
   "name": "event src/main.rs:12",
   "target": "tracing_publisher"
 }
 {
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Warn)",
   "name": "event src/main.rs:13",
   "target": "tracing_publisher"
 }
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Now, we get two log outputs, one for `info!` and one for `warning!`. Let's run `kafkacat` again to verify the output:  

```shell
$ kafkacat -C -b broker:9092 -t tracingpublisher 
{
  "fields": {
    "a_bool": true,
    "answer": 42,
    "message": "first example"
  },
  "level": "Level(Info)",
  "name": "event src/main.rs:12",
  "target": "tracing_publisher"
}
{
  "fields": {
    "a_bool": true,
    "answer": 42,
    "message": "first example"
  },
  "level": "Level(Info)",
  "name": "event src/main.rs:12",
  "target": "tracing_publisher"
}
% Reached end of topic tracingpublisher [0] at offset 2
{
  "fields": {
    "a_bool": true,
    "answer": 42,
    "message": "first example"
  },
  "level": "Level(Warn)",
  "name": "event src/main.rs:13",
  "target": "tracing_publisher"
}
% Reached end of topic tracingpublisher [1] at offset 1
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Without additional parameters, we consume both partitions at the same  
time. But if we're only interested in, let's say warnings, we could do the following:  

```shell
$ kafkacat -C -b broker:9092 -t tracingpublisher -p 1
 {
   "fields": {
     "a_bool": true,
     "answer": 42,
     "message": "first example"
   },
   "level": "Level(Warn)",
   "name": "event src/main.rs:13",
   "target": "tracing_publisher"
 }
 % Reached end of topic tracingpublisher [1] at offset 1
```

<svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-on"><title>Enter fullscreen mode</title> <path d="M16 3h6v6h-2V5h-4V3zM2 3h6v2H4v4H2V3zm18 16v-4h2v6h-6v-2h4zM4 19h4v2H2v-6h2v4z"></path></svg> <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" class="highlight-action crayons-icon highlight-action--fullscreen-off"><title>Exit fullscreen mode</title><path d="M18 7h4v2h-6V3h2v4zM8 9H2V7h4V3h2v6zm10 8v4h-2v-6h6v2h-4zM8 15v6H6v-4H2v-2h6z"></path></svg>

Partitions don't have a name, but are identified by an index. In our case, index 1 contains all warnings.

## Summary

In this tutorial, we used `tracing` and a custom [`tracing_subscriber` Layer](https://docs.rs/tracing-subscriber/latest/tracing_subscriber/layer/)  
to capture telemetry data and sent it to Apache Kafka for further processing.

Instead of sending all data into a single partition, we divide the telemetry events based on severity. A consumer can choose to selectively work with certain subsets of data, based on event severity.

Running Apache Kafka on a local machine as part of your development setup is straightforward. Deploying Kafka into a production environment, however, is a different story. We know sometimes deadlines are approaching quickly and it's challenging to deliver all features and also become a Kafka operations expert at the same time. With Calisti,  
you can run Apache Kafka and Zookeeper as a Kubernetes workload without having to become an expert first. Calisti takes care of deployment and configuration, so you can focus on running your application.

Ready to deploy? Check out [Calisti.app](https://calisti.app/?utm_source=website&utm_campaign=devto_kafka_partition_producer&utm_medium=organic) to get started with our free  
tier.

Find the project's [source code on GitHub.](https://github.com/schultyy/rust-kafka-producer-partitioner-example)