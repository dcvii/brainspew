---
title: "Real-time Data Replication with Debezium and Python"
source: "https://debezium.io/blog/2025/02/01/real-time-data-replication-with-debezium-and-python/"
author:
  - "[[Debezium]]"
published:
created: 2025-02-11
description: "Debezium is an open source distributed platform for change data capture. Start it up, point it at your databases, and your apps can start responding to all of the inserts, updates, and deletes that other apps commit to your databases. Debezium is durable and fast, so your apps can respond quickly and never miss an event, even when things go wrong."
tags:
  - "clippings"
---
We configure Debezium by creating a Java `Properties` object. This object holds the [configuration settings](https://debezium.io/documentation/reference/stable/connectors/postgresql.html) for the Debezium engine. It includes database connection details, the connector class (PostgresConnector), offset storage, and transformations. The `transforms` property is used to unwrap the Debezium message, simplifying downstream processing.

```python
def debezium_engine_props(sourcedb: DbPostgresql):
    props = Properties()
    props.setProperty("name", "engine")
    props.setProperty("snapshot.mode", "initial_only")
    props.setProperty("database.hostname", sourcedb.CONTAINER.get_container_host_ip())
    props.setProperty("database.port",
                      sourcedb.CONTAINER.get_exposed_port(sourcedb.POSTGRES_PORT_DEFAULT))
    props.setProperty("database.user", sourcedb.POSTGRES_USER)
    props.setProperty("database.password", sourcedb.POSTGRES_PASSWORD)
    props.setProperty("database.dbname", sourcedb.POSTGRES_DBNAME)
    props.setProperty("connector.class", "io.debezium.connector.postgresql.PostgresConnector")
    props.setProperty("offset.storage", "org.apache.kafka.connect.storage.FileOffsetBackingStore")
    props.setProperty("offset.storage.file.filename", OFFSET_FILE.as_posix())
    props.setProperty("max.batch.size", "5")
    props.setProperty("poll.interval.ms", "10000")
    props.setProperty("converter.schemas.enable", "false")
    props.setProperty("offset.flush.interval.ms", "1000")
    props.setProperty("database.server.name", "testc")
    props.setProperty("database.server.id", "1234")
    props.setProperty("topic.prefix", "testc")
    props.setProperty("schema.whitelist", "inventory")
    props.setProperty("database.whitelist", "inventory")
    props.setProperty("table.whitelist", "inventory.*")
    props.setProperty("replica.identity.autoset.values", "inventory.*:FULL")
    # // debezium unwrap message
    props.setProperty("transforms", "unwrap")
    props.setProperty("transforms.unwrap.type", "io.debezium.transforms.ExtractNewRecordState")
    props.setProperty("transforms.unwrap.add.fields", "op,table,source.ts_ms,sourcedb,ts_ms")
    props.setProperty("transforms.unwrap.delete.handling.mode", "rewrite")
    # props.setProperty("debezium.transforms.unwrap.drop.tombstones", "true")
    return props
```