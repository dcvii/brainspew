---
title: "Essbase - Wikipedia"
source: "https://en.wikipedia.org/wiki/Essbase"
author:
  - "[[Contributors to Wikimedia projects]]"
published: 2005-03-21
created: 2026-04-07
description:
tags:
  - "brain_spew"
---
**Essbase** is a multidimensional [database management system](https://en.wikipedia.org/wiki/Database_management_system "Database management system") (MDBMS). The platform provides tools to build data analytic applications.

[Arbor Software](https://en.wikipedia.org/wiki/Arbor_Software "Arbor Software") developed Essbase first releasing it in 1992. Arbor merged with Hyperion Software in 1998. [Oracle Corporation](https://en.wikipedia.org/wiki/Oracle_Corporation "Oracle Corporation") acquired [Hyperion Solutions Corporation](https://en.wikipedia.org/wiki/Hyperion_Solutions "Hyperion Solutions") in 2007. Until late 2005 [IBM](https://en.wikipedia.org/wiki/IBM "IBM") also marketed an OEM version of Essbase as [DB2](https://en.wikipedia.org/wiki/IBM_DB2 "IBM DB2") OLAP Server.[^1]

The database researcher [E. F. Codd](https://en.wikipedia.org/wiki/E._F._Codd "E. F. Codd") coined the term " [on-line analytical processing](https://en.wikipedia.org/wiki/Online_analytical_processing "Online analytical processing") " ([OLAP](https://en.wikipedia.org/wiki/OLAP "OLAP")) in a [whitepaper](https://en.wikipedia.org/wiki/White_paper "White paper") [^2] that set out twelve rules for analytic systems (an allusion to his earlier famous set of [twelve rules](https://en.wikipedia.org/wiki/Codd%27s_12_rules "Codd's 12 rules") defining the [relational model](https://en.wikipedia.org/wiki/Relational_model "Relational model")). This whitepaper, published by [Computerworld](https://en.wikipedia.org/wiki/Computerworld "Computerworld"), was somewhat explicit in its reference to Essbase features, and when it was later discovered that Codd had been sponsored by Arbor Software, Computerworld withdrew the paper.[^3]

In contrast to "on-line transaction processing" ([OLTP](https://en.wikipedia.org/wiki/OLTP "OLTP")), OLAP defines a database technology optimized for processing human queries rather than transactions. The results of this orientation were that [multidimensional databases](https://en.wikipedia.org/wiki/Multidimensional_database "Multidimensional database") oriented their performance requirements around a different set of [benchmarks](https://en.wikipedia.org/wiki/Benchmark_\(computing\) "Benchmark (computing)") (Analytic Performance Benchmark, APB-1) than that of [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system "Relational database management system") ([Transaction Processing Performance Council](https://en.wikipedia.org/wiki/Transaction_Processing_Performance_Council "Transaction Processing Performance Council") \[TPC\]).

Hyperion renamed many of its products in 2005, giving Essbase an official name of **Hyperion System 9 BI+ Analytic Services**, but the new name was largely ignored by practitioners. The Essbase brand was later returned to the official product name for marketing purposes, but the server software still carried the "Analytic Services" title until it was incorporated into Oracle's Business Intelligence Foundation Suite (BIFS) product.[^4]

In August 2005, *[Information Age](https://en.wikipedia.org/wiki/Information_Age "Information Age")* magazine named Essbase as one of the 10 most influential technology innovations of the previous 10 years,[^5] along with [Netscape](https://en.wikipedia.org/wiki/Netscape "Netscape"), the [BlackBerry](https://en.wikipedia.org/wiki/BlackBerry "BlackBerry"), [Google](https://en.wikipedia.org/wiki/Google "Google"), [virtualization](https://en.wikipedia.org/wiki/Platform_virtualization "Platform virtualization"), Voice Over IP ([VOIP](https://en.wikipedia.org/wiki/VOIP "VOIP")), [Linux](https://en.wikipedia.org/wiki/Linux "Linux"), [XML](https://en.wikipedia.org/wiki/XML "XML"), the [Pentium](https://en.wikipedia.org/wiki/Pentium_\(brand\) "Pentium (brand)") processor, and [ADSL](https://en.wikipedia.org/wiki/ADSL "ADSL"). Editor Kenny MacIver said: "Hyperion Essbase was the multi-dimensional database technology that put online analytical processing on the [business intelligence](https://en.wikipedia.org/wiki/Business_intelligence "Business intelligence") map. It has spurred the creation of scores of rival OLAP products – and billions of OLAP cubes".[^6]

## History and motivation

Shortly before commercializing its Essbase product, Arbor Software filed a patent for a *[Method and apparatus for storing and retrieving multi-dimensional data in computer memory](https://patents.google.com/patent/US5359724A)* in 1992, which was granted in 1994 (expired 2012)*.* Essbase was originally developed to address the [scalability](https://en.wikipedia.org/wiki/Scalability "Scalability") issues associated with using [spreadsheets](https://en.wikipedia.org/wiki/Spreadsheets "Spreadsheets") such as [Lotus 1-2-3](https://en.wikipedia.org/wiki/Lotus_1-2-3 "Lotus 1-2-3") and [Microsoft Excel](https://en.wikipedia.org/wiki/Microsoft_Excel "Microsoft Excel") to model and analyze complex data relationships. Indeed, the Essbase patent application uses spreadsheets as a motivating example to illustrate the need for such a system.[^7]

In this context, "multi-dimensional" refers to the representation of financial data in spreadsheet format. A typical spreadsheet may display time intervals along column headings, and account names on row headings. For example:

|  | Jan | Feb | Mar | Total |
| --- | --- | --- | --- | --- |
| Quantity | 1000 | 2000 | 3000 | **6000** |
| Sales | $100 | $200 | $300 | **$600** |
| Expenses | $80 | $160 | $240 | **$480** |
| Profit | $20 | $40 | $60 | **$120** |

If a user wants to break down these values by region, for example, this typically involves the duplication of this table on multiple spreadsheets:

| \|  \| Jan \| Feb \| Mar \| Total \| \| --- \| --- \| --- \| --- \| --- \| \| Quantity \| 240 \| 1890 \| 50 \| **2180** \| \| Sales \| $24 \| $189 \| $5 \| **$218** \| \| Expenses \| $20 \| $150 \| $3 \| **$173** \| \| Profit \| $4 \| $39 \| $2 \| **$45** \| | \|  \| Jan \| Feb \| Mar \| Total \| \| --- \| --- \| --- \| --- \| --- \| \| Quantity \| 760 \| 110 \| 2950 \| **3820** \| \| Sales \| $76 \| $11 \| $295 \| **$382** \| \| Expenses \| $60 \| $10 \| $237 \| **$307** \| \| Profit \| $16 \| $1 \| $58 \| **$75** \| | \|  \| Jan \| Feb \| Mar \| Total \| \| --- \| --- \| --- \| --- \| --- \| \| Quantity \| 1000 \| 2000 \| 3000 \| **6000** \| \| Sales \| $100 \| $200 \| $300 \| **$600** \| \| Expenses \| $80 \| $160 \| $240 \| **$480** \| \| Profit \| $20 \| $40 \| $60 \| **$120** \| |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

An alternative representation of this structure would require a three-dimensional spreadsheet grid, giving rise to the idea that "Time", "Account", and "Region" are [dimensions](https://en.wikipedia.org/wiki/Dimensions "Dimensions"). As further dimensions are added to the system, it becomes very difficult to maintain spreadsheets that correctly represent the multi-dimensional values. Multidimensional databases such as Essbase provide a data store for values that exist, at least conceptually, in a multi-dimensional " [hypercube](https://en.wikipedia.org/wiki/OLAP_cube "OLAP cube") ".

### Sparsity

As the number and size of dimensions increases, developers of multidimensional databases increasingly face technical problems in the physical representation of data. Say the above example was extended to add a "Customer" and "Product" dimension:

| Dimension | Number of dimension values |
| --- | --- |
| Accounts | 4 |
| Time | 4 |
| Region | 3 |
| Customer | 10,000 |
| Product | 5,000 |

If the [multidimensional database](https://en.wikipedia.org/wiki/Multidimensional_database "Multidimensional database") reserved storage space for every possible value, it would need to store 2,400,000,000 (4 × 4 × 3 × 10,000 × 5,000) cells. If the software maps each cell as a [64-bit floating point](https://en.wikipedia.org/wiki/Double-precision_floating-point_format "Double-precision floating-point format") value, this equates to a memory requirement of about 17.9 [GiB](https://en.wikipedia.org/wiki/Gibibytes "Gibibytes") (exactly 19.2 [GB](https://en.wikipedia.org/wiki/Gigabytes "Gigabytes")). In practice, of course, the number of combinations of "Customer" and "Product" that contain meaningful values will be a tiny subset of the total space. This property of multi-dimensional spaces is referred to as [sparsity](https://en.wikipedia.org/wiki/Sparsity "Sparsity").

### Aggregation

[OLAP](https://en.wikipedia.org/wiki/OLAP "OLAP") systems generally provide for multiple levels of detail within each dimension by arranging the members of each dimension into one or more [hierarchies](https://en.wikipedia.org/wiki/Hierarchies "Hierarchies"). A time dimension, for example, may be represented as a hierarchy starting with "Total Time", and breaking down into multiple years, then quarters, then months. An Accounts dimension may start with "Profit", which breaks down into "Revenue" and "Expenses", and so on.

In the example above, if "Product" represents individual product [SKUs](https://en.wikipedia.org/wiki/Stock_Keeping_Unit "Stock Keeping Unit"), analysts may also want to report using aggregations such as "Product Group", "Product Family", "Product Line", etc. Similarly, for "Customer", natural aggregations may arrange customers according to geographic location or industry.

The number of aggregate values implied by a set of input data can become surprisingly large. If the Customer and Product dimensions are each in fact six "generations" deep, then 36 (6 × 6) aggregate values are affected by a single data point. It follows that if all these aggregate values are to be stored, the amount of space required is proportional to the [product](https://en.wikipedia.org/wiki/Product_\(mathematics\) "Product (mathematics)") of the depth of all aggregating dimensions. For large databases, this can cause the effective storage requirements to be many hundred times the size of the data being aggregated.

## Block storage (Essbase Analytics)

Since version 7, Essbase has supported two "storage options" which take advantage of sparsity to minimize the amount of physical memory and disk space required to represent large multidimensional spaces. The Essbase patent [^7] describes the original method, which aimed to reduce the amount of physical memory required without increasing the time required to look up closely related values. With the introduction of alternative storage options, marketing materials called this the **Block Storage Option** (**Essbase BSO**), later referred to as **Essbase Analytics**.

Put briefly, Essbase requires the developer to tag dimensions as "dense" or "sparse". The system then arranges data to represent the hypercube into "blocks", where each block comprises a multi-dimensional array made up of "dense" dimensions, and space is allocated for every potential cell in that block. Sparsity is exploited because the system only creates blocks when required. In the example above, say the developer has tagged "Accounts" and "Time" as "dense", and "Region", "Customer", and "Product" as "sparse". If there are, say, 12,000 combinations of Region, Customer and Product that contain data, then only 12,000 blocks will be created, each block large enough to store every possible combination of Accounts and Time. The number of cells stored is therefore 192000 (4 × 4 × 12000), requiring under 2 [GiB](https://en.wikipedia.org/wiki/Gibibytes "Gibibytes") of memory (exact 1,536 [MB](https://en.wikipedia.org/wiki/Megabytes "Megabytes")), plus the size of the index used to look up the appropriate blocks.

Because the database hides this implementation from front-end tools (i.e., a report that attempts to retrieve data from non-existent cells merely sees "null" values), the full hypercube can be navigated naturally, and it is possible to load values into any cell interactively.

### Calculation engine

Users can specify calculations in Essbase BSO as:

- The aggregation of values through dimensional hierarchies;
- Stored calculations on dimension members;
- "Dynamically calculated" dimension members; or
- Procedural "calculation scripts" that act on values stored in the database.

The first method (dimension aggregation) takes place implicitly through addition, or by selectively tagging branches of the hierarchy to be subtracted, multiplied, divided or ignored. Also, the result of this aggregation can be stored in the database, or calculated dynamically on demand—members must be tagged as "Stored" or "Dynamic Calc." to specify which method is to be used.

The second method (stored calculations) uses a [formula](https://en.wikipedia.org/wiki/Formula "Formula") against each calculated dimension member – when Essbase calculates that member, the result is stored against that member just like a data value.

The third method (dynamic calculation) is specified in exactly the same format as stored calculations, but calculates a result when a user accesses a value addressed by that member; the system does not store such calculated values.

The fourth method (calculation scripts) uses a [procedural](https://en.wikipedia.org/wiki/Procedural_programming "Procedural programming") [programming language](https://en.wikipedia.org/wiki/Programming_language "Programming language") specific to the Essbase calculation engine. This type of calculation may act upon any data value in the hypercube, and can therefore perform calculations that cannot be expressed as a simple formula.

A calculation script must also be executed to trigger the calculation of aggregated values or stored calculations as described above—a built-in calculation script (called the "default calculation") can be used to execute this type of calculation.

## Aggregate storage (Enterprise Analytics)

Although block storage effectively minimizes storage requirements without impacting retrieval time, it has limitations in its treatment of aggregate data in large applications, motivating the introduction of a second storage engine, named **Aggregate Storage Option** (**Essbase ASO**) or more recently, **Enterprise Analytics**. This storage option makes the database behave much more like an OLAP database, such as [SQL Server Analysis Services](https://en.wikipedia.org/wiki/SQL_Server_Analysis_Services "SQL Server Analysis Services").

Following a data load, Essbase ASO does not store any aggregate values, but instead calculates them on demand. For large databases, where the time required to generate these values may become inconvenient, the database can materialize one or more aggregate "views", made up of one aggregate level from each dimension (for example, the database may calculate all combinations of the fifth generation of Product with the third generation of Customer), and these views are then used to generate other aggregate values where possible. This process can be partially automated, where the administrator specifies the amount of disk space that may be used, and the database generates views according to actual usage.

This approach has a major drawback in that the cube cannot be treated for calculation purposes as a single large hypercube, because aggregate values cannot be directly controlled, so write-back from front-end tools is limited, and complex calculations that cannot be expressed as [MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions "MultiDimensional eXpressions") expressions are not possible.

### Calculation engine

Essbase ASO can specify calculations as:

- The aggregation of values through dimensional hierarchies; or
- Dynamically calculated dimension members.

The first method (dimension aggregation) basically duplicates the algorithm used by Essbase BSO.

The second method (dynamic calculations) evaluates [MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions "MultiDimensional eXpressions") expressions against dimension members.

## User interface

The majority of Essbase users work with Essbase data via an [add-in](https://en.wikipedia.org/wiki/Add-in "Add-in") for [Microsoft Excel](https://en.wikipedia.org/wiki/Microsoft_Excel "Microsoft Excel") (previously also [Lotus 1-2-3](https://en.wikipedia.org/wiki/Lotus_1-2-3 "Lotus 1-2-3")) known as Smart View. The Essbase Add-In is a standard plugin to Microsoft Excel and creates an additional menu that can be used to connect to Essbase databases, retrieve or write data, and navigate the cube's dimensions ("Zoom in", "Pivot", etc.).[^8]

In 2005, Hyperion began to offer a [visualization](https://en.wikipedia.org/wiki/Visualization_\(computer_graphics\) "Visualization (computer graphics)") tool called Hyperion Visual Explorer (HVE) which was an OEM from [Tableau Software](https://en.wikipedia.org/wiki/Tableau_Software "Tableau Software"). [Tableau Software](https://en.wikipedia.org/wiki/Tableau_Software "Tableau Software") originated at [Stanford University](https://en.wikipedia.org/wiki/Stanford_University "Stanford University") as a government-sponsored research project to investigate new ways for users to interact with [relational](https://en.wikipedia.org/wiki/Relational_database "Relational database") and [OLAP](https://en.wikipedia.org/wiki/OLAP "OLAP") databases. Hyperion and Tableau together built fundamentally the first versions of [Tableau Software](https://en.wikipedia.org/wiki/Tableau_Software "Tableau Software") which was designed specifically for multidimensional (OLAP) databases. Oracle quickly terminated the OEM arrangement with [Tableau Software](https://en.wikipedia.org/wiki/Tableau_Software "Tableau Software") soon after the acquisition of Hyperion in 2007.

Most other well known analytics vendors provide user-facing applications with support for Essbase and include;

- [Hyperion Analyzer](https://en.wikipedia.org/w/index.php?title=Hyperion_Analyzer&action=edit&redlink=1 "Hyperion Analyzer (page does not exist)") (aka Hyperion System 9 BI+ Web Analysis)
- [Hyperion Reports](https://en.wikipedia.org/w/index.php?title=Hyperion_Reports&action=edit&redlink=1 "Hyperion Reports (page does not exist)") (aka Hyperion System 9 BI+ Financial Reporting)
- [Hyperion Enterprise Reporting](https://en.wikipedia.org/w/index.php?title=Hyperion_Enterprise_Reporting&action=edit&redlink=1 "Hyperion Enterprise Reporting (page does not exist)")
- [Hyperion Business Intelligence](https://en.wikipedia.org/w/index.php?title=Hyperion_Business_Intelligence&action=edit&redlink=1 "Hyperion Business Intelligence (page does not exist)") (aka Hyperion System 9 BI+ Interactive Reporting, and Brio Interactive Reporting)
- [Hyperion SQR](https://en.wikipedia.org/w/index.php?title=Hyperion_SQR&action=edit&redlink=1 "Hyperion SQR (page does not exist)") (aka Hyperion System 9 BI+ Production Reporting)
- [Alphablox](https://en.wikipedia.org/w/index.php?title=Alphablox&action=edit&redlink=1 "Alphablox (page does not exist)")
- [Arcplan dynaSight](https://en.wikipedia.org/w/index.php?title=Arcplan_dynaSight&action=edit&redlink=1 "Arcplan dynaSight (page does not exist)") (aka Arcplan Enterprise)
- [Oracle Business Intelligence Suite Enterprise Edition](https://en.wikipedia.org/wiki/Oracle_Business_Intelligence_Suite_Enterprise_Edition "Oracle Business Intelligence Suite Enterprise Edition") (aka OBIEE, Siebel Analytics)
- Dodeca Spreadsheet Management System [^9]
- Dodeca Excel Add-In for Essbase [^10]
- Reporting Suite [^11]
- EV Analytics [^12]

The previous offerings from Hyperion acquired new names as given below:

| Hyperion's previous offerings | Hyperion System 9 BI+ offerings |
| --- | --- |
| Hyperion Essbase ASO | Enterprise Analytics |
| Hyperion Essbase BSO | Essbase Analytics |
| Hyperion Analyzer | Web Analysis |
| Hyperion Reports | Financial Reporting |
| Hyperion Intelligence | Interactive Reporting |
| Hyperion SQR | Production Reporting |
| Hyperion Metrics Builder | Enterprise Metrics |

[APIs](https://en.wikipedia.org/wiki/API "API") are available for [C](https://en.wikipedia.org/wiki/C_\(programming_language\) "C (programming language)"), [Visual Basic](https://en.wikipedia.org/wiki/Visual_Basic "Visual Basic") and [Java](https://en.wikipedia.org/wiki/Java_\(programming_language\) "Java (programming language)"), and embedded scripting support is available for [Perl](https://en.wikipedia.org/wiki/Perl "Perl"). The standardised [XML for Analysis](https://en.wikipedia.org/wiki/XML_for_Analysis "XML for Analysis") protocol can query Essbase data sources using the [MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions "MultiDimensional eXpressions") language.

In 2007, Oracle Corporation began bundling Hyperion BI tools into Oracle Business Intelligence Enterprise Edition Plus.

## Administrative interface

A number of standard interfaces can administer Essbase applications:

- *ESSCMD*, the original [command line interface](https://en.wikipedia.org/wiki/Command_line_interface "Command line interface") for administration commands;
- *MaxL*, a "multi-dimensional database access language" which provides both a superset of ESSCMD commands, but with a syntax more akin to [SQL](https://en.wikipedia.org/wiki/SQL "SQL"), as well as support for [MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions "MultiDimensional eXpressions") queries;
- *Essbase Application Manager*, the original [Microsoft Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "Microsoft Windows") [GUI](https://en.wikipedia.org/wiki/GUI "GUI") administration client, compatible with versions of Essbase before 7.0;
- *Essbase Administration Services*, later renamed *Analytic Administration Services*, and then back to 'Essbase Administration Services' in v. 9.3.1, the currently supported [GUI](https://en.wikipedia.org/wiki/GUI "GUI") administration client; and
- *Essbase Integration Server* for maintaining the structure and content of Essbase databases based on data models derived from relational or file-based data sources.

## Cloud offerings

Since 2017, Essbase Cloud has been available as part of the Oracle Analytics Cloud (OAC), a suite of analytics that include reports and dashboards, data visualization, inline data preparation and mobile.[^13]

## Competitors

There are several significant competitors among the OLAP, analytics products to that of Essbase (HOLAP/MOLAP) on the market, among them SAP BPC, Microsoft SQL Server [Microsoft Analysis Services](https://en.wikipedia.org/wiki/Microsoft_Analysis_Services "Microsoft Analysis Services"), (MOLAP, HOLAP, ROLAP), IBM [Cognos](https://en.wikipedia.org/wiki/Cognos "Cognos") (ROLAP), IBM/Cognos/Applix [TM1](https://en.wikipedia.org/wiki/TM1 "TM1") (MOLAP), [Oracle OLAP](https://en.wikipedia.org/wiki/Oracle_OLAP "Oracle OLAP") (ROLAP/MOLAP), [MicroStrategy](https://en.wikipedia.org/wiki/MicroStrategy "MicroStrategy") (ROLAP), and [EXASolution](https://en.wikipedia.org/wiki/EXASOL "EXASOL") (ROLAP).

Also note that of the above competitors, including Essbase, all use heterogenous relational ([Microsoft SQL Server](https://en.wikipedia.org/wiki/Microsoft_SQL_Server "Microsoft SQL Server"), Oracle, IBM DB/2, TeraData, Access, etc.) or non-relational data sourcing (Excel, text Files, CSV Files, etc.) to feed the cubes (facts and dimensional data), except for Oracle OLAP which may only use Oracle relational sourcing.

## Export and/or product migration of Essbase

As of 2009 two options can export Essbase cubes into other formats:

1. [CubePort](https://en.wikipedia.org/wiki/CubePort "CubePort"), a commercial conversion application, converts Essbase cubes to the Microsoft SQL Server Analysis Services product. This product performs an object-to-object translation that make up an Essbase cube, including: outline, member formulas, calc scripts, data loading (load rules), report scripts to MDX queries, substitution variables, and security model. It can extract from any platform version of Essbase, including Oracle/Hyperion Essbase on Windows, Unix, AIX, HP UX, Solaris, IBM DB/2 OLAP, or AS/400 Showcase Essbase.
2. OlapUnderground Outline Extractor performs a pure, rudimentary, export of the outline, though it does not directly create any new objects. The output is a simple text file that can be pulled indirectly into other OLAP products, among other uses, such as synchronizing outlines.

[^1]: ["DB2 OLAP Server"](https://web.archive.org/web/20061205020530/http://www-306.ibm.com/software/data/db2/db2olap). Archived from [the original](http://www-306.ibm.com/software/data/db2/db2olap/) on 2006-12-05. IBM DB2 OLAP Server goes out of support January 31, 2007.

[^2]: [Codd, E. F.](https://en.wikipedia.org/wiki/Edgar_F._Codd "Edgar F. Codd"); S B Codd; C T Salley (1993-07-26). ["Providing OLAP to User-Analysts: An IT Mandate"](https://web.archive.org/web/20170808214004/https://www.minet.uni-jena.de/dbis/lehre/ss2005/sem_dwh/lit/Cod93.pdf) (PDF). *[Computerworld](https://en.wikipedia.org/wiki/Computerworld "Computerworld")*. Archived from [the original](https://www.minet.uni-jena.de/dbis/lehre/ss2005/sem_dwh/lit/Cod93.pdf) (PDF) on 2017-08-08.

[^3]: Whitehorn, Mark (26 Jan 2007). ["OLAP and the need for SPEED: In another dimension"](https://www.theregister.co.uk/2007/01/26/olap_speed/). *The Register*.

[^4]: ["Essbase | Business Intelligence"](https://www.oracle.com/technetwork/middleware/essbase/overview/index.html). Oracle.

[^5]: Rossi, Ben (2006-02-25). ["Ten-year top tens"](https://www.information-age.com/ten-year-top-tens-21771/). *Information Age*. Retrieved 2024-01-27.

[^6]: ["News Release - Hyperion"](https://web.archive.org/web/20070927190115/http://www.hyperion.com/company/news/news_releases/press_release_2005_000512.cfm) (Press release). 16 August 2005. Archived from [the original](https://www.hyperion.com/company/news/news_releases/press_release_2005_000512.cfm) on 2007-09-27.

[^7]: Earle, Robert J. (1992) ["Method and apparatus for storing and retrieving multi-dimensional data in computer memory"](http://patft.uspto.gov/netacgi/nph-Parser?u=%2Fnetahtml%2Fsrchnum.htm&Sect1=PTO1&Sect2=HITOFF&p=1&r=1&l=50&f=G&d=PALL&s1=5359724.PN.&OS=PN/5359724&RS=PN/5359724) [Archived](https://web.archive.org/web/20180201075154/http://patft.uspto.gov/netacgi/nph-Parser?u=%2Fnetahtml%2Fsrchnum.htm&Sect1=PTO1&Sect2=HITOFF&p=1&r=1&l=50&f=G&d=PALL&s1=5359724.PN.&OS=PN/5359724&RS=PN/5359724) 2018-02-01 at the [Wayback Machine](https://en.wikipedia.org/wiki/Wayback_Machine "Wayback Machine"). United States Patent 5,359,724 assigned to [Arbor Software Corporation](https://en.wikipedia.org/wiki/Arbor_Software_Corporation "Arbor Software Corporation").

[^8]: Hyperion Solutions Corporation (2006). [Essbase Database Administrator's Guide](http://dev.hyperion.com/techdocs/essbase/essbase_712/Docs/dbag/dba_html.htm). [Archived](https://web.archive.org/web/20060204085022/http://dev.hyperion.com/techdocs/essbase/essbase_712/Docs/dbag/dba_html.htm) 2006-02-04 at the [Wayback Machine](https://en.wikipedia.org/wiki/Wayback_Machine "Wayback Machine")

[^9]: ["Applied OLAP: Dodeca Spreadsheet Management System Software"](https://www.appliedolap.com/products/dodeca-spreadsheet-management/). *DodecaSpreadsheet Management System*. Applied OLAP, Inc.

[^10]: ["Dodeca Excel Add-In for Essbase"](https://www.appliedolap.com/products/dodeca-excel-addin-for-essbase).

[^11]: ["Homepage -"](https://web.archive.org/web/20130422094749/http://essbase.cxo-cockpit.com/). Archived from [the original](http://essbase.cxo-cockpit.com/) on 2013-04-22. Retrieved 2018-09-06.

[^12]: ["Self-service data analysis with cubus EV"](https://www.cubus-ev.com/).

[^13]: Todd Rebner (April 19, 2017). ["Oracle Essbase Cloud is Here"](https://www.datavail.com/blog/oracle-essbase-cloud-is-here/). Datavail Corporation.