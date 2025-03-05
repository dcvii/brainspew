---
title: Postgres | dlt Docs
source: https://dlthub.com/docs/dlt-ecosystem/destinations/postgres
author: 
published: 
created: 2025-02-11
description: Postgres `dlt` destination
tags:
  - clippings
  - postgres
---
## Install dlt with PostgreSQL​

**To install the dlt library with PostgreSQL dependencies, run:**

```prism
pip install "dlt[postgres]"
```

## Setup guide​

**1\. Initialize a project with a pipeline that loads to Postgres by running:**

**2\. Install the necessary dependencies for Postgres by running:**

```prism
pip install -r requirements.txt
```

This will install dlt with the `postgres` extra, which contains the `psycopg2` client.

**3\. After setting up a Postgres instance and `psql` or a query editor, create a new database by running:**

```prism
CREATE DATABASE dlt_data;
```

Add the `dlt_data` database to `.dlt/secrets.toml`.

**4\. Create a new user by running:**

```prism
CREATE USER loader WITH PASSWORD '<password>';
```

Add the `loader` user and `<password>` password to `.dlt/secrets.toml`.

**5\. Give the `loader` user owner permissions by running:**

```prism
ALTER DATABASE dlt_data OWNER TO loader;
```

You can set more restrictive permissions (e.g., give user access to a specific schema).

**6\. Enter your credentials into `.dlt/secrets.toml`.** It should now look like this:

```prism
[destination.postgres.credentials]

database = "dlt_data"
username = "loader"
password = "<password>" # replace with your password
host = "localhost" # or the IP address location of your database
port = 5432
connect_timeout = 15
```

You can also pass a database connection string similar to the one used by the `psycopg2` library or [SQLAlchemy](https://docs.sqlalchemy.org/en/20/core/engines.html#postgresql). The credentials above will look like this:

```prism
# Keep it at the top of your TOML file, before any section starts
destination.postgres.credentials="postgresql://loader:<password>@localhost/dlt_data?connect_timeout=15"
```

To pass credentials directly, use the [explicit instance of the destination](https://dlthub.com/docs/general-usage/destination#pass-explicit-credentials)

```prism
pipeline = dlt.pipeline(
  pipeline_name='chess',
  destination=dlt.destinations.postgres("postgresql://loader:<password>@localhost/dlt_data"),
  dataset_name='chess_data'
)
```

## Write disposition​

All write dispositions are supported.

If you set the [`replace` strategy](https://dlthub.com/docs/general-usage/full-loading) to `staging-optimized`, the destination tables will be dropped and replaced by the staging tables.

## Data loading​

`dlt` will load data using large INSERT VALUES statements by default. Loading is multithreaded (20 threads by default).

### Data types​

`postgres` supports various timestamp types, which can be configured using the column flags `timezone` and `precision` in the `dlt.resource` decorator or the `pipeline.run` method.

- **Precision**: allows you to specify the number of decimal places for fractional seconds, ranging from 0 to 6. It can be used in combination with the `timezone` flag.
- **Timezone**:
- Setting `timezone=False` maps to `TIMESTAMP WITHOUT TIME ZONE`.
- Setting `timezone=True` (or omitting the flag, which defaults to `True`) maps to `TIMESTAMP WITH TIME ZONE`.

#### Example precision and timezone: TIMESTAMP (3) WITHOUT TIME ZONE​

```prism
@dlt.resource(
    columns={"event_tstamp": {"data_type": "timestamp", "precision": 3, "timezone": False}},
    primary_key="event_id",
)
def events():
    yield [{"event_id": 1, "event_tstamp": "2024-07-30T10:00:00.123"}]

pipeline = dlt.pipeline(destination="postgres")
pipeline.run(events())
```

### Fast loading with Arrow tables and CSV​

You can use [Arrow tables](https://dlthub.com/docs/dlt-ecosystem/verified-sources/arrow-pandas) and [CSV](https://dlthub.com/docs/dlt-ecosystem/file-formats/csv) to quickly load tabular data. Pick the CSV loader file format like below:

```prism
info = pipeline.run(arrow_table, loader_file_format="csv")
```

In the example above, `arrow_table` will be converted to CSV with **pyarrow** and then streamed into **postgres** with the COPY command. This method skips the regular `dlt` normalizer used for Python objects and is several times faster.

## Supported file formats​

- [insert-values](https://dlthub.com/docs/dlt-ecosystem/file-formats/insert-format) is used by default.
- [CSV](https://dlthub.com/docs/dlt-ecosystem/file-formats/csv) is supported.

## Supported column hints​

`postgres` will create unique indexes for all columns with `unique` hints. This behavior **may be disabled**.

### Spatial Types​

To enable GIS capabilities in your Postgres destination, use the `x-postgres-geometry` and `x-postgres-srid` hints for columns containing geometric data. The `postgres_adapter` facilitates applying these hints conveniently, with a default SRID of `4326`.

**Supported Geometry Types:**

- WKT (Well-Known Text)
- Hex Representation

If you have geometry data in binary format, you will need to convert it to hexadecimal representation before loading.

**Example:** Using `postgres_adapter` with Different Geometry Types

```prism
from dlt.destinations.impl.postgres.postgres_adapter import postgres_adapter

# Sample data with various geometry types
data_wkt = [
  {"type": "Point_wkt", "geom": "POINT (1 1)"},
  {"type": "Point_wkt", "geom": "Polygon([(0, 0), (1, 0), (1, 1), (0, 1), (0, 0)])"},
  ]

data_wkb_hex = [
  {"type": "Point_wkb_hex", "geom": "0101000000000000000000F03F000000000000F03F"},
  {"type": "Point_wkb_hex", "geom": "01020000000300000000000000000000000000000000000000000000000000F03F000000000000F03F00000000000000400000000000000040"},
]

# Apply postgres_adapter to the 'geom' column with default SRID 4326
resource_wkt = postgres_adapter(data_wkt, geometry="geom")
resource_wkb_hex = postgres_adapter(data_wkb_hex, geometry="geom")

# If you need a different SRID
resource_wkt = postgres_adapter(data_wkt, geometry="geom", srid=3242)
```

Ensure that the PostGIS extension is enabled in your Postgres database:

```prism
CREATE EXTENSION postgis;
```

This configuration allows `dlt` to map the `geom` column to the PostGIS `geometry` type for spatial queries and analyses.

danger

`LinearRing` geometry type isn't supported.

## Table and column identifiers​

Postgres supports both case-sensitive and case-insensitive identifiers. All unquoted and lowercase identifiers resolve case-insensitively in SQL statements. Case insensitive [naming conventions](https://dlthub.com/docs/general-usage/naming-convention#case-sensitive-and-insensitive-destinations) like the default **snake\_case** will generate case-insensitive identifiers. Case sensitive (like **sql\_cs\_v1**) will generate case-sensitive identifiers that must be quoted in SQL statements.

## Additional destination options​

The Postgres destination creates UNIQUE indexes by default on columns with the `unique` hint (i.e., `_dlt_id`). To disable this behavior:

```prism
[destination.postgres]
create_indexes=false
```

### Setting up CSV format​

You can provide [non-default](https://dlthub.com/docs/dlt-ecosystem/file-formats/csv#default-settings) CSV settings via a configuration file or explicitly.

```prism
[destination.postgres.csv_format]
delimiter="|"
include_header=false
```

or

```prism
from dlt.destinations import postgres
from dlt.common.data_writers.configuration import CsvFormatConfiguration

csv_format = CsvFormatConfiguration(delimiter="|", include_header=False)

dest_ = postgres(csv_format=csv_format)
```

Above, we set the `CSV` file without a header, with **|** as a separator.

### dbt support​

This destination [integrates with dbt](https://dlthub.com/docs/dlt-ecosystem/transformations/dbt/) via dbt-postgres.

### Syncing of dlt state​

This destination fully supports [dlt state sync](https://dlthub.com/docs/general-usage/state#syncing-state-with-destination).

## Additional Setup guides​

- [Load data from Stripe to PostgreSQL in python with dlt](https://dlthub.com/docs/pipelines/stripe_analytics/load-data-with-python-from-stripe_analytics-to-postgres)
- [Load data from Salesforce to Azure Cosmos DB in python with dlt](https://dlthub.com/docs/pipelines/salesforce/load-data-with-python-from-salesforce-to-cosmosdb)
- [Load data from DigitalOcean to Timescale in python with dlt](https://dlthub.com/docs/pipelines/digitalocean/load-data-with-python-from-digitalocean-to-timescale)
- [Load data from Keap to EDB BigAnimal in python with dlt](https://dlthub.com/docs/pipelines/keap/load-data-with-python-from-keap-to-biganimal)
- [Load data from Adobe Commerce (Magento) to AlloyDB in python with dlt](https://dlthub.com/docs/pipelines/magento/load-data-with-python-from-magento-to-alloydb)
- [Load data from Adobe Commerce (Magento) to CockroachDB in python with dlt](https://dlthub.com/docs/pipelines/magento/load-data-with-python-from-magento-to-cockroachdb)
- [Load data from Klarna to PostgreSQL in python with dlt](https://dlthub.com/docs/pipelines/klarna/load-data-with-python-from-klarna-to-postgres)
- [Load data from Adobe Commerce (Magento) to Supabase in python with dlt](https://dlthub.com/docs/pipelines/magento/load-data-with-python-from-magento-to-supabase)
- [Load data from Imgur to Supabase in python with dlt](https://dlthub.com/docs/pipelines/imgur/load-data-with-python-from-imgur-to-supabase)
- [Load data from Soundcloud to EDB BigAnimal in python with dlt](https://dlthub.com/docs/pipelines/soundcloud/load-data-with-python-from-soundcloud-to-biganimal)