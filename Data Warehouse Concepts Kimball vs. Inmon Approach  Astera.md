---
title: "Data Warehouse Concepts: Kimball vs. Inmon Approach | Astera"
source: "https://www.astera.com/type/blog/data-warehouse-concepts/"
author:
  - "[[Tehreem Naeem]]"
published: 2020-02-03
created: 2025-02-24
description: "Inmon vs Kimball: Which data warehouse concept should you use to design a data warehouse. Find out in this blog."
tags:
  - "clippings"
---
When it comes to [data warehouse](https://www.astera.com/type/blog/data-warehouse-definition/) (DWH) designing, two of the most widely discussed and explained data warehouse approaches are the Inmon and the Kimball methodology. For years, people have debated over which data warehouse approach is better and more effective for businesses. However, there’s still no definite answer as both methods have their benefits and drawbacks.

In this blog, we will discuss the basics of a data warehouse, it’s characteristics, and compare the two popular data warehouse approaches – Kimball vs. Inmon.

- [Characteristics of a Data Warehouse](https://www.astera.com/type/blog/data-warehouse-concepts/#Characteristics-of-a-Data-Warehouse)
- [Functions of a Data Warehouse](https://www.astera.com/type/blog/data-warehouse-concepts/#Functions-of-a-Data-Warehouse)
- [Normalization vs. Denormalization Approach](https://www.astera.com/type/blog/data-warehouse-concepts/#Normalization-Vs-Denormalization-Approach)
- [Data Warehouse vs. Database](https://www.astera.com/type/blog/data-warehouse-concepts/#Data-Warehouse-Vs-Database)
- [The Two Data Warehouse Concepts: Kimball vs. Inmon](https://www.astera.com/type/blog/data-warehouse-concepts/#What-Are-the-Two-Data-Warehouse-Concepts-Kimball-vs-Inmon-Explained)
- [Which Data Warehouse Approach to Choose?](https://www.astera.com/type/blog/data-warehouse-concepts/#Which-Data-Warehouse-Approach-to-Choose)
- [An Automated Data Warehousing Tool](https://www.astera.com/type/blog/data-warehouse-concepts/#An-Automated-Data-Warehousing-Tool)
- [Bottom-line](https://www.astera.com/type/blog/data-warehouse-concepts/#Bottom-line)

The key data warehouse concept allows users to access a unified version of truth for timely business decision-making, reporting, and forecasting. DWH functions like an information system with all the past and commutative data stored from one or more sources.

## **Data Warehouse Models**

**Data Warehouse Models** refer to the *architectural designs and structures used to organize and manage data within a data warehousing environment*. These models dictate how data is stored, accessed, and utilized for analytical purposes. Major sections include:

- **Virtual Warehouse:** Comprising separate databases that can be queried collectively, allowing users to access data as if it were stored in a single warehouse.
- **Data Mart:** Focused on specific business functions or departments, containing subsets of data tailored for analysis.
- **Enterprise Data Warehouse:** Comprehensive repository integrating data from various sources across an organization, supporting enterprise-wide analytics and reporting.

## Characteristics of a Data Warehouse

The following are the four characteristics of a Data Warehouse:

- **Subject-Oriented:** A data warehouse uses a theme, and delivers information about a specific subject instead of a company’s current operations. In other words, the data warehousing process is more equipped to handle a specific theme. Examples of themes or subjects include sales, distributions, marketing, etc.
- **Integrated:** Integration is defined as establishing a connection between large amount of data from multiple databases or sources. However, it is also essential for the data to be stored in the data warehouse in a unified manner. The process of data warehousing integrates data from multiple sources, such as a mainframe, relational databases, flat files, etc. Furthermore, it helps maintain consistent codes, attribute measures, naming conventions, and, formats.
- **Time-variant:** Time-variant in a DW is more extensive as compared to other operating systems. Data stored in a data warehouse is recalled with a specific time period and provides information from a historical perspective.
- **Non-volatile:** In the non-volatile data warehouse, data is permanent i.e. when new data is inserted, previous data is not replaced, omitted, or deleted. In this data warehouse, data is read-only and only refreshes at certain intervals.  The two data operations performed in the data warehouse are data access and data loading.

![Approaches of data warehouse ](https://cdn-ajfbi.nitrocdn.com/GuYcnotRkcKfJXshTEEKnCZTOtUwxDnm/assets/images/optimized/rev-07863b0/media.geeksforgeeks.org/wp-content/uploads/Untitled-drawing-9-1.png "Characteristics and Functions of Data Warehouse: Subject Oriented, Integrated, Time-Variant, Non-Volatile")

Characteristics and Functions of Data Warehouse (Source: GeeksforGeeks)

## Functions of a Data Warehouse

Data warehouse functions as a repository. It helps organizations avoid the cost of storage systems and backup data at an enterprise level. The prominent functions of the data warehouse are:

- [Data Cleaning](https://www.astera.com/type/blog/data-cleansing/)
- [Data Integration](https://www.astera.com/type/blog/data-integration/)
- [Data Mapping](https://www.astera.com/type/blog/understanding-data-mapping-and-its-techniques/)
- [Data Extraction](https://www.astera.com/type/blog/what-is-data-extraction-a-brief-guide/)
- [Data Transformation](https://www.astera.com/type/blog/data-transformation/)
- Data Loading
- Refreshing

## Normalization vs. Denormalization Approach

Normalization is defined as a way of data re-organization. This helps meet two main requirements in an [enterprise data warehouse](https://www.astera.com/type/blog/enterprise-data-warehouse/) i.e. eliminating data redundancy and protecting data dependency. On the other hand, denormalization increases the functionality of the database system’s infrastructure.

## Data Warehouse vs. Database

The main differences between data warehouse and database are summarized in the table below:

| **Database** | **Data Warehouse** |
| --- | --- |
| A database is an amalgamation of related data. | Data warehouse serves as an information system that contains historical and commutative data from one or several sources. |
| A database is used for recording data. | A data warehouse is used for analyzing data. |
| A database is an application-oriented collection of data. | Data warehouse is the subject-oriented collection of data. |
| A database uses Online Transactional Processing (OLTP). | Data warehouse uses Online Analytical Processing (OLAP). |
| Database tables and joins are normalized, therefore, more complicated. | Data warehouse tables and joins are denormalized, hence simpler. |
| ER modeling techniques are used for designing. | Data modeling techniques are used for designing. |

## The Two Data Warehouse Concepts: Kimball vs. Inmon

Both data warehouse design methodologies have their own pros and cons. Let’s go through them in detail to figure out which one is better.

### The Kimball Methodology

Initiated by Ralph Kimball, the Kimball data model follows a bottom-up approach to [data warehouse architecture design](https://www.astera.com/knowledge-center/data-warehouse-architecture/) in which data marts are first formed based on the business requirements.

The primary data sources are then evaluated, and an [Extract, Transform and Load (ETL) tool](https://www.astera.com/knowledge-center/what-is-etl-tool/) is used to fetch data from several sources and load it into a staging area of the relational database server. Once data is uploaded in the  data warehouse staging area, the next phase includes loading data into a dimensional data warehouse model that’s denormalized by nature. This model partitions data into the fact table, which is numeric transactional data or dimension table, which is the reference information that supports facts.

Star schema is the fundamental element of the dimensional data warehouse model. The combination of a fact table with several dimensional tables is often called the star schema. Kimball dimensional modeling allows users to construct several star schemas to fulfill various reporting needs. The advantage of star schema is that small dimensional-table queries run instantaneously.

To integrate data, Kimball approach to Data Warehouse lifecycle suggests the idea of conformed data dimensions. It exists as a basic dimension table shared across different fact tables (such as customer and product) within a data warehouse or as the same dimension tables in various Kimball data marts. This guarantees that a single data item is used in a similar manner across all the facts.

An important design tool in Ralph Kimball’s data warehouse methodology is the enterprise bus matrix or Kimball bus architecture that vertically records the facts and horizontally records the conformed dimensions. The Kimball matrix, which is a part of bus architecture, displays how star schemas are constructed. It is used by business management teams as an input to prioritize which row of the Kimball matrix should be implemented first.

The Kimball approach to data warehouse lifecycle is also based on conformed facts, i.e. data marts that are separately implemented together with a robust architecture.

![Kimball method data warehouse architecture ](https://www.astera.com/type/blog/data-warehouse-concepts/ "Basic Kimball Data Warehouse architecture explained")

Figure 2. Basic Kimball Data Warehouse  architecture explained (Source: Zentut)

#### Advantages of the Kimball Methodology

Some of the main benefits of the Kimball Data Warehousing Concept include:

- Kimball dimensional modeling is fast to construct as no normalization is involved, which means swift execution of the initial phase of the [data warehousing](https://www.astera.com/type/blog/what-is-a-data-warehouse-definition-benefits/) design process.
- An advantage of star schema is that most data operators can easily comprehend it because of its denormalized structure, which simplifies querying and analysis.
- Data warehouse system footprint is trivial because it focuses on individual business areas and processes rather than the whole enterprise. So, it takes less space in the database, simplifying system management.
- It enables fast data retrieval from the data warehouse, as data is segregated into fact tables and dimensions. For example, the fact and dimension table for the insurance industry would include policy transactions and claims transactions.
- A smaller team of designers and planners is sufficient for data warehouse management because data source systems are stable, and the data warehouse is process-oriented. Also, query optimization is straightforward, predictable, and controllable.
- Conformed dimensional structure for [data quality](https://www.astera.com/type/blog/data-quality/) framework. The Kimball approach to data warehouse lifecycle is also referred to as the business dimensional lifestyle approach because it allows business intelligence tools to deeper across several star schemas and generates reliable insights.

![Kimball DW/BI Lifecycle Methodology - Kimball Group](https://cdn-ajfbi.nitrocdn.com/GuYcnotRkcKfJXshTEEKnCZTOtUwxDnm/assets/images/source/rev-07863b0/www.kimballgroup.com/wp-content/uploads/2012/06/kimball-core-concepts-021.png "Shows Kimball's Approach to Data Warehouse Lifecycle")

Kimball Approach to Data Warehouse Lifecycle (Source: Kimball Group)

#### Disadvantages of the Kimball Methodology

Some of the drawbacks of the Kimball [Data Warehousing](https://www.astera.com/type/blog/what-is-data-warehousing/) design concept include:

- Data isn’t entirely integrated before reporting; the idea of a ‘single source of truth is lost.’
- Irregularities can occur when data is updated in Kimball DW architecture. This is because in denormalization technique, redundant data is added to database tables.
- In the Kimball DW architecture, performance issues may occur due to the addition of columns in the fact table, as these tables are quite in-depth. The addition of new columns can expand the fact table dimensions, affecting its performance. Also, the dimensional data warehouse model becomes difficult to alter with any change in the business needs.
- As the Kimball model is business process-oriented, instead of focusing on the enterprise as a whole,  it cannot handle all the BI reporting requirements.
- The process of incorporating large amounts of legacy data into the data warehouse is complex.

### The Inmon Method

Bill Inmon, the father of data warehousing, came up with the concept to develop a data warehouse which identifies the main subject areas and entities the enterprise works with, such as customers, product, vendor, and so on. Bill Inmon’s definition of a data warehouse is that it is a “subject-oriented, nonvolatile, integrated, time-variant collection of data in support of management’s decisions.”

The model then creates a thorough, logical model for every primary entity. For instance, a logical model is constructed for products with all the attributes associated with that entity. This logical model could include ten diverse entities under product, including all the details, such as business drivers, aspects, relationships, dependencies, and affiliations.

The [Bill Inmon design approach](https://www.astera.com/type/blog/consolidation-software/) uses the normalized form for building entity structure, avoiding data redundancy as much as possible. This results in clearly identifying business requirements and preventing any data update irregularities. Moreover, the advantage of this top-down approach in [database design](https://www.astera.com/type/blog/all-you-need-to-know-about-database-design/) is that it is robust to business changes and contains a dimensional perspective of data across data mart.

Next, the physical model is constructed, which follows the normalized structure. This Bill Inmon model creates a single source of truth for the whole business. Data loading becomes less complex due to the normalized structure of the model. However, using this arrangement for querying is challenging as it includes numerous tables and links.

This Inmon data warehouse methodology proposes constructing data marts separately for each division, such as finance, marketing sales, etc. All the data entering the data warehouse is integrated. The data warehouse acts as a single data source for various data marts to ensure integrity and consistency across the enterprise.

![Data Warehouse Concepts: Kimball vs. Inmon Approach 2](https://www.astera.com/type/blog/data-warehouse-concepts/ "Basic Bill Inmon data warehousing architecture explained")

Figure 3. Basic Bill Inmon data warehousing architecture explained (Source: Stanford University)

#### Advantages of the Inmon Method

The Bill Inmon design approach offers the following benefits :

- Data warehouse acts as a unified source of truth for the entire business, where all data is integrated.
- This approach has very low data redundancy. So, there’s less possibility of data update irregularities, making the ETL-concept based data warehouse process more straightforward and less susceptible to failure.
- It simplifies business processes, as the logical model represents detailed business objects.
- This approach offers greater flexibility, as it’s easier to update the data warehouse in case there’s any change in the business requirements or source data.
- It can handle diverse enterprise-wide reporting requirements.

#### Disadvantages of the Inmon Method

The possible drawbacks of this approach are as follows:

- Complexity increases as multiple tables are added to the data model with time.
- Resources skilled in data warehouse data modeling are required, which can be expensive and challenging to find.
- The preliminary setup and delivery are time-consuming.
- Additional ETL process operation is required since data marts are created after the creation of the data warehouse.
- This approach requires experts to manage a data warehouse effectively.

## Which Data Warehouse Approach to Choose?

Now that we’ve evaluated the Kimball vs. Inmon approach and seen the advantages and drawbacks of both these methods, the question arises: *Which one of these data warehouse concepts would best serve your business?*

Both these approaches consider [data warehouse](https://discover.astera.com/implementing-virtual-databases-in-your-enterprise-data-warehouse-edw) as a central repository that supports business reporting. Also, both types of approaches use ETL concepts for data loading. However, the main difference lies in modeling data and loading it in the data warehouse.

The approach used for data warehouse construction influences the preliminary delivery time of the warehousing project and the capacity to put up with prospective variations in the ETL design.

Still not sure about the conclusion to Kimball vs. Inmon dilemma?  We can help you decide which one of these data warehouse approaches would help improve your [data quality management](https://www.astera.com/type/blog/data-quality-management/) framework in the best way?

We’ve narrowed down a few aspects that can help you decide between the two approaches.

- **Reporting Needs**: If you need organization-wide and integrated reporting, then the Bill Inmon approach is more suitable. But if you require reporting focused on the business process or team, then opt for the Kimball method.
- **Project Deadline:** Designing a normalized data model is comparatively more complex than designing a denormalized model. This makes the Inmon approach a time-intensive process. Therefore, if you have less time for delivery, then opt for the Kimball method.
- **Prospective Recruitment Plan:** The higher complexity of data model creation in the Inmon data warehouse approach requires a larger team of professionals for data warehouse management. Therefore, choose accordingly.
- **Frequent Changes:** If your reporting needs are likely to change more quickly and you are dealing with volatile source systems, then opt for the Inmon method as it offers more flexibility. However, if reporting needs and source systems are comparatively stable, it’s better to use the Kimball method.
- **Organizational Principles:** If your organization’s stakeholders and corporate directors recognize the need for data warehousing and are ready to bear the expenses, then the Bill Inmon data warehouse method would be a safer bet. On the other hand, if the decision-makers aren’t concerned about the nitty-gritty of the approach, and are only looking for a solution to improve reporting, then it’s sufficient to opt for the Kimball data warehouse method.

## Bottom-line

Both Kimball vs. Inmon data warehouse concepts can be used to design data warehouse models successfully. In fact, several enterprises use a blend of both these approaches (called hybrid data model).

In the hybrid data model, the Inmon method creates a dimensional data warehouse model of a data warehouse. In contrast, the Kimball method is followed to develop data marts using the star schema.

It’s impossible to claim which approach is better as both methods have their benefits and drawbacks, working well in different situations. A data warehouse designer has to choose a method, depending on the various factors discussed in this article.

Lastly, for any method to be effective, it has to be well-thought-out, explored in-depth, and developed to gratify your company’s [business intelligence](https://www.astera.com/type/infographic/self-service-bi/) reporting requirements.

## Astera Data Warehouse Builder – An Automated Data Warehousing Solution

Astera Data Warehouse Builder offers an integrated platform to design, deploy and test large-volume data warehouses and automate the processes to reach meaningful insights quickly, without the hassle of writing ETL codes.

Organizations are moving toward [data warehouse automation](https://www.astera.com/type/blog/data-warehouse-automation-series-introduction/) to save costs, maximize productivity, and get actionable insights quicker. Data Warehousing Automation allows you to quickly build high-quality data marts, build self-regulating data pipelines, and deliver relevant insights to decision-makers via BI and analytics tools.

Data Warehousing Automation eliminates the most time-consuming part in populating a data warehouse: writing ETL/ELT code. As no SQL hand coding is required, developers can focus their energy on working at a logical level (design level) to create more efficient integration flows.

In addition, automation helps you design an [agile data warehouse infrastructure](https://www.astera.com/type/blog/agile-data-warehouse-design/). The result is a more adaptable, responsive data repository that can be queried efficiently, producing valuable insights in seconds and allow you to extract valuable insights.

In a nutshell, removing manual intervention in the planning, modeling, and deployment steps allows you to [build a better quality data warehouse](https://www.astera.com/type/blog/game-changing-benefits-of-data-warehouse-automation/) with success — that too, in a matter of weeks or even days.

### Authors:

- ![](https://www.astera.com/type/blog/data-warehouse-concepts/) Tehreem Naeem