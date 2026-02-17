---
title: Slowly changing dimension - Wikipedia
source: https://en.wikipedia.org/wiki/Slowly_changing_dimension
author:
published:
created: 2025-04-04
description:
tags:
  - clippings
  - SCD2
---
In [data management](https://en.wikipedia.org/wiki/Data_management "Data management") and [data warehousing](https://en.wikipedia.org/wiki/Data_warehousing "Data warehousing"), a **slowly changing dimension** (SCD) is a [dimension](https://en.wikipedia.org/wiki/Dimension_\(data_warehouse\) "Dimension (data warehouse)") that stores [data](https://en.wikipedia.org/wiki/Data "Data") which, while generally stable, may change over time, often in an unpredictable manner.[^1] This contrasts with a **rapidly changing dimension**, such as transactional parameters like customer ID, product ID, quantity, and price, which undergo frequent updates. Common examples of SCDs include [geographical locations](https://en.wikipedia.org/wiki/Market_area "Market area"), [customer details](https://en.wikipedia.org/wiki/Customer_data "Customer data"), or [product attributes](https://en.wikipedia.org/wiki/Product_analysis "Product analysis").

Various methodologies address the complexities of SCD management. The Kimball Toolkit has popularized a categorization of techniques for handling SCD attributes as Types 1 through 6.[^1] These range from simple overwrites (Type 1), to creating new rows for each change (Type 2), adding new attributes (Type 3), maintaining separate history tables (Type 4), or employing hybrid approaches (Type 6 and 7). Type 0 is available to model an attribute as not really changing at all. Each type offers a trade-off between historical accuracy, data complexity, and system performance, catering to different [analytical](https://en.wikipedia.org/wiki/Business_analytics "Business analytics") and [reporting](https://en.wikipedia.org/wiki/Business_intelligence "Business intelligence") needs.

The challenge with SCDs lies in preserving historical accuracy while maintaining [data integrity](https://en.wikipedia.org/wiki/Data_integrity "Data integrity") and [referential integrity](https://en.wikipedia.org/wiki/Referential_integrity "Referential integrity"). For instance, a [fact table](https://en.wikipedia.org/wiki/Fact_table "Fact table") tracking sales might be linked to a dimension table containing information about salespeople and their assigned regional offices. If a salesperson is transferred to a new office, historical sales reports need to reflect their previous assignment without breaking the relationships between the fact and dimension tables. SCDs provide mechanisms to manage such changes effectively.

## Type 0: retain original

The Type 0 dimension attributes never change and are assigned to attributes that have durable values or are described as 'Original'. Examples: *Date of Birth*, *Original Credit Score*. Type 0 applies to most date dimension attributes.[^2]

## Type 1: overwrite

This method overwrites old with new data, and therefore does not track historical data.

Example of a supplier table:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State |
| --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA |

In the above example, Supplier\_Code is the [natural key](https://en.wikipedia.org/wiki/Natural_key "Natural key") and Supplier\_Key is a [surrogate key](https://en.wikipedia.org/wiki/Surrogate_key "Surrogate key"). Technically, the surrogate key is not necessary, since the row will be unique by the natural key (Supplier\_Code).

If the supplier relocates the headquarters to Illinois the record would be overwritten:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State |
| --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | IL |

The disadvantage of the Type 1 method is that there is no history in the data warehouse. It has the advantage however that it's easy to maintain.

If one has calculated an aggregate table summarizing facts by supplier state, it will need to be recalculated when the Supplier\_State is changed.[^1]

## Type 2: add new row

This method tracks historical data by creating multiple records for a given [natural key](https://en.wikipedia.org/wiki/Natural_key "Natural key") in the dimensional tables with separate [surrogate keys](https://en.wikipedia.org/wiki/Surrogate_key "Surrogate key") and/or different version numbers. Unlimited history is preserved for each insert. The natural key in these examples is the "Supplier\_Code" of "ABC".

For example, if the supplier relocates to Illinois the version numbers will be incremented sequentially:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Version |
| --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 0 |
| 124 | ABC | Acme Supply Co | IL | 1 |
| 125 | ABC | Acme Supply Co | NY | 2 |

Another method is to add 'effective date' columns.

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Start\_Date | End\_Date |
| --- | --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 |
| 124 | ABC | Acme Supply Co | IL | 2004-12-22T00:00:00 | `NULL` |

The Start date/time of the second row is equal to the End date/time (or next) of the previous row. The null End\_Date in row two indicates the current tuple version. A standardized surrogate high date (e.g. 9999-12-31) may instead be used as an end date so that null-value substitution is not required when querying. In some database software, using an artificial high date value could cause performance issues, that using a null value would prevent.

And a third method uses an effective date and a current flag.

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Effective\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 2000-01-01T00:00:00 | N |
| 124 | ABC | Acme Supply Co | IL | 2004-12-22T00:00:00 | Y |

The Current\_Flag value of 'Y' indicates the current tuple version.

Transactions that reference a particular [surrogate key](https://en.wikipedia.org/wiki/Surrogate_key "Surrogate key") (Supplier\_Key) are then permanently bound to the time slices defined by that row of the slowly changing dimension table. An aggregate table summarizing facts by supplier state continues to reflect the historical state, i.e. the state the supplier was in at the time of the transaction; no update is needed. To reference the entity via the natural key, it is necessary to remove the unique constraint making [referential integrity](https://en.wikipedia.org/wiki/Referential_integrity "Referential integrity") by DBMS (DataBase Management System) impossible.

If there are retroactive changes made to the contents of the dimension, or if new attributes are added to the dimension (for example a Sales\_Rep column) which have different effective dates from those already defined, then this can result in the existing transactions needing to be updated to reflect the new situation. This can be an expensive database operation, so Type 2 SCDs are not a good choice if the dimensional model is subject to frequent change.[^1]

## Type 3: add new attribute

This method tracks changes using separate columns and preserves limited history. The Type 3 preserves limited history as it is limited to the number of columns designated for storing historical data. The original table structure in Type 1 and Type 2 is the same but Type 3 adds additional columns. In the following example, an additional column has been added to the table to record the supplier's original state - only the previous history is stored.

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Original\_Supplier\_State | Effective\_Date | Current\_Supplier\_State |
| --- | --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 2004-12-22T00:00:00 | IL |

This record contains a column for the original state and current state—cannot track the changes if the supplier relocates a second time.

One variation of this is to create the field Previous\_Supplier\_State instead of Original\_Supplier\_State which would track only the most recent historical change.[^1]

## Type 4: add history table

The Type 4 method is usually referred to as using "history tables", where one table keeps the current data, and an additional table is used to keep a record of some or all changes. Both the surrogate keys are referenced in the fact table to enhance query performance.

For the example below, the original table name is Supplier and the history table is Supplier\_History:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State |
| --- | --- | --- | --- |
| 124 | ABC | Acme & Johnson Supply Co | IL |

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Create\_Date |
| --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 2003-06-14T00:00:00 |
| 124 | ABC | Acme & Johnson Supply Co | IL | 2004-12-22T00:00:00 |

This method resembles how database audit tables and [change data capture](https://en.wikipedia.org/wiki/Change_data_capture "Change data capture") techniques function.

## Type 5

The type 5 technique builds on the type 4 mini-dimension by embedding a “current profile” mini-dimension key in the base dimension that's overwritten as a type 1 attribute. This approach is called type 5 because 4 + 1 equals 5. The type 5 slowly changing dimension allows the currently-assigned mini-dimension attribute values to be accessed along with the base dimension's others without linking through a fact table. Logically, we typically represent the base dimension and current mini-dimension profile outrigger as a single table in the presentation layer. The outrigger attributes should have distinct column names, like “Current Income Level,” to differentiate them from attributes in the mini-dimension linked to the fact table. The ETL team must update/overwrite the type 1 mini-dimension reference whenever the current mini-dimension changes over time. If the outrigger approach does not deliver satisfactory query performance, then the mini-dimension attributes could be physically embedded (and updated) in the base dimension.[^3]

## Type 6: combined approach

The Type 6 method combines the approaches of types 1, 2 and 3 (1 + 2 + 3 = 6). One possible explanation of the origin of the term was that it was coined by [Ralph Kimball](https://en.wikipedia.org/wiki/Ralph_Kimball "Ralph Kimball") during a conversation with Stephen Pace from Kalido. [Ralph Kimball](https://en.wikipedia.org/wiki/Ralph_Kimball "Ralph Kimball") calls this method "Unpredictable Changes with Single-Version Overlay" in *The Data Warehouse Toolkit*.[^1]

The Supplier table starts out with one record for our example supplier:

| Supplier\_Key | Row\_Key | Supplier\_Code | Supplier\_Name | Current\_State | Historical\_State | Start\_Date | End\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 123 | 1 | ABC | Acme Supply Co | CA | CA | 2000-01-01T00:00:00 | 9999-12-31T23:59:59 | Y |

The Current\_State and the Historical\_State are the same. The optional Current\_Flag attribute indicates that this is the current or most recent record for this supplier.

When Acme Supply Company moves to Illinois, we add a new record, as in Type 2 processing, however a row key is included to ensure we have a unique key for each row:

| Supplier\_Key | Row\_Key | Supplier\_Code | Supplier\_Name | Current\_State | Historical\_State | Start\_Date | End\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 123 | 1 | ABC | Acme Supply Co | IL | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 | N |
| 123 | 2 | ABC | Acme Supply Co | IL | IL | 2004-12-22T00:00:00 | 9999-12-31T23:59:59 | Y |

We overwrite the Current\_State information in the first record (Row\_Key = 1) with the new information, as in Type 1 processing. We create a new record to track the changes, as in Type 2 processing. And we store the history in a second State column (Historical\_State), which incorporates Type 3 processing.

For example, if the supplier were to relocate again, we would add another record to the Supplier dimension, and we would overwrite the contents of the Current\_State column:

| Supplier\_Key | Row\_Key | Supplier\_Code | Supplier\_Name | Current\_State | Historical\_State | Start\_Date | End\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 123 | 1 | ABC | Acme Supply Co | NY | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 | N |
| 123 | 2 | ABC | Acme Supply Co | NY | IL | 2004-12-22T00:00:00 | 2008-02-04T00:00:00 | N |
| 123 | 3 | ABC | Acme Supply Co | NY | NY | 2008-02-04T00:00:00 | 9999-12-31T23:59:59 | Y |

## Type 2 / type 6 fact implementation

### Type 2 surrogate key with type 3 attribute

In many Type 2 and Type 6 SCD implementations, the [surrogate key](https://en.wikipedia.org/wiki/Surrogate_key "Surrogate key") from the dimension is put into the fact table in place of the [natural key](https://en.wikipedia.org/wiki/Natural_key "Natural key") when the fact data is loaded into the data repository.[^1] The surrogate key is selected for a given fact record based on its effective date and the Start\_Date and End\_Date from the dimension table. This allows the fact data to be easily joined to the correct dimension data for the corresponding effective date.

Here is the Supplier table as we created it above using Type 6 Hybrid methodology:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Current\_State | Historical\_State | Start\_Date | End\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | NY | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 | N |
| 124 | ABC | Acme Supply Co | NY | IL | 2004-12-22T00:00:00 | 2008-02-04T00:00:00 | N |
| 125 | ABC | Acme Supply Co | NY | NY | 2008-02-04T00:00:00 | 9999-12-31T23:59:59 | Y |

Once the Delivery table contains the correct Supplier\_Key, it can easily be joined to the Supplier table using that key. The following SQL retrieves, for each fact record, the current supplier state and the state the supplier was located in at the time of the delivery:

```
SELECT
  delivery.delivery_cost,
  supplier.supplier_name,
  supplier.historical_state,
  supplier.current_state
FROM delivery
INNER JOIN supplier
  ON delivery.supplier_key = supplier.supplier_key;
```

### Pure type 6 implementation

Having a Type 2 surrogate key for each time slice can cause problems if the dimension is subject to change.[^1] A pure Type 6 implementation does not use this, but uses a surrogate key for each [master data](https://en.wikipedia.org/wiki/Master_data "Master data") item (e.g. each unique supplier has a single surrogate key). This avoids any changes in the master data having an impact on the existing transaction data. It also allows more options when querying the transactions.

Here is the Supplier table using the pure Type 6 methodology:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Start\_Date | End\_Date |
| --- | --- | --- | --- | --- | --- |
| 456 | ABC | Acme Supply Co | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 |
| 456 | ABC | Acme Supply Co | IL | 2004-12-22T00:00:00 | 2008-02-04T00:00:00 |
| 456 | ABC | Acme Supply Co | NY | 2008-02-04T00:00:00 | 9999-12-31T23:59:59 |

The following example shows how the query must be extended to ensure a single supplier record is retrieved for each transaction.

```
SELECT
  supplier.supplier_code,
  supplier.supplier_state
FROM supplier
INNER JOIN delivery
  ON supplier.supplier_key = delivery.supplier_key
 AND delivery.delivery_date >= supplier.start_date AND delivery.delivery_date < supplier.end_date;
```

A fact record with an effective date (Delivery\_Date) of August 9, 2001 will be linked to Supplier\_Code of ABC, with a Supplier\_State of 'CA'. A fact record with an effective date of October 11, 2007 will also be linked to the same Supplier\_Code ABC, but with a Supplier\_State of 'IL'.

While more complex, there are a number of advantages of this approach, including:

1. [Referential integrity](https://en.wikipedia.org/wiki/Referential_integrity "Referential integrity") by DBMS is now possible, but one cannot use Supplier\_Code as [foreign key](https://en.wikipedia.org/wiki/Foreign_key "Foreign key") on Product table and using Supplier\_Key as foreign key each product is tied on specific time slice.
2. If there is more than one date on the fact (e.g. Order\_Date, Delivery\_Date, Invoice\_Payment\_Date) one can choose which date to use for a query.
3. You can do "as at now", "as at transaction time" or "as at a point in time" queries by changing the date filter logic.
4. You don't need to reprocess the fact table if there is a change in the dimension table (e.g. adding additional fields retrospectively which change the time slices, or if one makes a mistake in the dates on the dimension table one can correct them easily).
5. You can introduce [bi-temporal](https://en.wikipedia.org/wiki/Temporal_database#Bitemporal_Relations "Temporal database") dates in the dimension table.
6. You can join the fact to the multiple versions of the dimension table to allow reporting of the same information with different effective dates, in the same query.

The following example shows how a specific date such as '2012-01-01T00:00:00' (which could be the current datetime) can be used.

```
SELECT
  supplier.supplier_code,
  supplier.supplier_state
FROM supplier
INNER JOIN delivery
  ON supplier.supplier_key = delivery.supplier_key
 AND supplier.start_date <= '2012-01-01T00:00:00' AND supplier.end_date > '2012-01-01T00:00:00';
```

## Type 7: Hybrid - Both surrogate and natural key

An alternative implementation is to place *both* the [surrogate key](https://en.wikipedia.org/wiki/Surrogate_key "Surrogate key") and the [natural key](https://en.wikipedia.org/wiki/Natural_key "Natural key") into the fact table.[^5] This allows the user to select the appropriate dimension records based on:

- the primary effective date on the fact record (above),
- the most recent or current information,
- any other date associated with the fact record.

This method allows more flexible links to the dimension, even if one has used the Type 2 approach instead of Type 6.

Here is the Supplier table as we might have created it using Type 2 methodology:

| Supplier\_Key | Supplier\_Code | Supplier\_Name | Supplier\_State | Start\_Date | End\_Date | Current\_Flag |
| --- | --- | --- | --- | --- | --- | --- |
| 123 | ABC | Acme Supply Co | CA | 2000-01-01T00:00:00 | 2004-12-22T00:00:00 | N |
| 124 | ABC | Acme Supply Co | IL | 2004-12-22T00:00:00 | 2008-02-04T00:00:00 | N |
| 125 | ABC | Acme Supply Co | NY | 2008-02-04T00:00:00 | 9999-12-31T23:59:59 | Y |

To get current records:

```
SELECT
  delivery.delivery_cost,
  supplier.supplier_name,
  supplier.supplier_state
FROM delivery
INNER JOIN supplier
  ON delivery.supplier_code = supplier.supplier_code
WHERE supplier.current_flag = 'Y';
```

To get history records:

```
SELECT
  delivery.delivery_cost,
  supplier.supplier_name,
  supplier.supplier_state
FROM delivery
INNER JOIN supplier
  ON delivery.supplier_code = supplier.supplier_code;
```

To get history records based on a specific date (if more than one date exists in the fact table):

```
SELECT
  delivery.delivery_cost,
  supplier.supplier_name,
  supplier.supplier_state
FROM delivery
INNER JOIN supplier
  ON delivery.supplier_code = supplier.supplier_code
  AND delivery.delivery_date BETWEEN supplier.Start_Date AND supplier.End_Date
```

Some cautions:

- [Referential integrity](https://en.wikipedia.org/wiki/Referential_integrity "Referential integrity") by DBMS is not possible since there is not a unique key to create the relationship.
- If relationship is made with surrogate to solve problem above then one ends with entity tied to a specific time slice.
- If the join query is not written correctly, it may return duplicate rows and/or give incorrect answers.
- The date comparison might not perform well.
- Some [business intelligence](https://en.wikipedia.org/wiki/Business_intelligence "Business intelligence") tools do not handle generating complex joins well.
- The [ETL](https://en.wikipedia.org/wiki/Extract,_transform,_load "Extract, transform, load") processes needed to create the dimension table needs to be carefully designed to ensure that there are no overlaps in the time periods for each distinct item of reference data.

## Combining types

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Scd_model.png/220px-Scd_model.png)

Scd model example

Different SCD Types can be applied to different columns of a table. For example, we can apply Type 1 to the Supplier\_Name column and Type 2 to the Supplier\_State column of the same table.

## See also

- [Change data capture](https://en.wikipedia.org/wiki/Change_data_capture "Change data capture")
- [Temporal database](https://en.wikipedia.org/wiki/Temporal_database "Temporal database")
- [Log trigger](https://en.wikipedia.org/wiki/Log_trigger "Log trigger")
- [Entity–attribute–value model](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model "Entity–attribute–value model")
- [Multitenancy](https://en.wikipedia.org/wiki/Multitenancy "Multitenancy")
- [Operational planning](https://en.wikipedia.org/wiki/Operational_planning "Operational planning")
- [Business process management](https://en.wikipedia.org/wiki/Business_process_management "Business process management")
- [Data element](https://en.wikipedia.org/wiki/Data_element "Data element")

## Notes

## References

- Bruce Ottmann, Chris Angus: *Data processing system*, US Patent Office, Patent Number [7,003,504](http://patft.uspto.gov/netacgi/nph-Parser?u=%2Fnetahtml%2Fsrchnum.htm&Sect1=PTO1&Sect2=HITOFF&p=1&r=1&l=50&f=G&d=PALL&s1=7003504.PN.&OS=PN/7003504&RS=PN/7003504). February 21, 2006
- [Ralph Kimball](https://en.wikipedia.org/wiki/Ralph_Kimball "Ralph Kimball"):*Kimball University: Handling Arbitrary Restatements of History* [\[1\]](http://www.kimballgroup.com/2005/03/slowly-changing-dimensions-are-not-always-as-easy-as-1-2-3/). December 9, 2007

[^1]: Kimball, Ralph; Ross, Margy. *The Data Warehouse Toolkit: The Complete Guide to Dimensional Modeling*.

[^2]: ["Design Tip #152 Slowly Changing Dimension Types 0, 4, 5, 6 and 7"](https://www.kimballgroup.com/2013/02/design-tip-152-slowly-changing-dimension-types-0-4-5-6-7/). 5 February 2013.

[^3]: ["Design Tip #152 Slowly Changing Dimension Types 0, 4, 5, 6 and 7"](https://www.kimballgroup.com/2013/02/design-tip-152-slowly-changing-dimension-types-0-4-5-6-7/). 5 February 2013.

[^4]: Kimball, Ralph; Ross, Margy (July 1, 2013). *The Data Warehouse Toolkit: The Definitive Guide to Dimensional Modeling, 3rd Edition*. John Wiley & Sons, Inc. p. 122. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-1-118-53080-1](https://en.wikipedia.org/wiki/Special:BookSources/978-1-118-53080-1 "Special:BookSources/978-1-118-53080-1").

[^5]: Ross, Margy; Kimball, Ralph (March 1, 2005). ["Slowly Changing Dimensions Are Not Always as Easy as 1, 2, 3"](https://www.kimballgroup.com/2005/03/slowly-changing-dimensions-are-not-always-as-easy-as-1-2-3/). *Intelligent Enterprise*.