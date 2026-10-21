# Data Cleaning and Validation Notes --- Amazon Products Sales Analysis

## 1. Purpose

This document records data-quality checks and preparation steps for the
Amazon Products Sales Analysis Power BI dashboard. It is designed to be
completed with the actual results from the workbook and Power BI
queries.

**Important:** Do not mark a check as completed until it has been
performed and its result recorded. Keep the original source workbook
unchanged and apply transformations in a separate working copy or Power
Query.

## 2. Source Workbook

-   **Workbook:** `data/amazon_products_raw_data.xlsx`
-   **Worksheet:** `Amazon_Data`
-   **Known fields:**
    -   `Product Category`
    -   `Product Description`
    -   `Price(Dollar)`
    -   `Number of reviews`
    -   `Shipment`
    -   `Order Date`
-   **Reported size:** 89,082 data rows. Reconfirm after loading the
    current workbook.
-   **Reported date range:** January 2019 through December 2022.
    Reconfirm after parsing dates.
-   **Original source URL:** Add the verified source link.
-   **License/redistribution terms:** Verify and record before
    publishing the workbook publicly.

## 3. Data Grain and Meaning

Before cleaning, establish what one row represents. It may represent a
product listing, a dated product observation, a shipment record, or a
transaction; these are not interchangeable.

The visible fields do not include a dedicated order ID, quantity sold,
or transaction-revenue field. Therefore:

-   Do not assume each row represents one unit sold.
-   Do not assume `Price(Dollar)` is transaction revenue.
-   Do not assume `Number of reviews` represents reviews received on
    `Order Date`.
-   Verify the meaning of `Shipment` from the source documentation.

Record the confirmed grain here:

-   **One row represents:** Pending source verification.
-   **Price field meaning:** Pending source verification.
-   **Review-count meaning:** Pending source verification.
-   **Shipment field meaning:** Pending source verification.

## 4. Recommended Checks and Decisions

### 4.1 Column names and data types

**Checks** - Confirm all expected columns are present. - Set
`Product Category` and `Product Description` to text. - Set
`Price(Dollar)` to a numeric type with the correct decimal handling. -
Set `Number of reviews` to a suitable numeric whole-number type if
appropriate. - Parse `Order Date` as a valid date. - Inspect the
`Shipment` type and values before changing its type.

**Decision/log:** Pending.

### 4.2 Missing and blank values

**Checks** - Count null and blank values in each column. - Determine
whether missing values are valid, unknown, or data-entry issues. -
Decide whether to retain, correct, or exclude affected rows based on the
analysis. - Do not replace missing prices or review counts with zero
unless zero is the correct business meaning.

**Decision/log:** Pending.

### 4.3 Text whitespace and category consistency

**Checks** - Trim leading and trailing whitespace in category and
description fields. - Review category labels for inconsistent spelling,
capitalization, and near-duplicates. - Check whether visually identical
descriptions differ only by spaces or formatting.

**Recommended action:** Use Power Query's Trim and Clean transformations
where appropriate, then inspect distinct values before consolidating
categories.

**Decision/log:** Pending. Do not claim that category cleanup is
complete until verified.

### 4.4 Duplicate records

The initial inspection reported 135 duplicate full rows, but this must
be reconfirmed against the current workbook.

**Checks** - Count exact duplicate rows across all fields. - Inspect a
sample of duplicates. - Determine whether duplicates are accidental
copies or legitimate repeated observations. - If a unique record key
exists in the original source, use it to assess duplication. - Remove
rows only when there is a defensible reason to treat them as duplicates.

**Decision/log:** Pending.

**Caution:** Repeated product descriptions or repeated prices alone do
not prove that rows are duplicates.

### 4.5 Price validation

**Checks** - Count null, zero, and negative price values. - Inspect
unusually high and low values. - Confirm decimal and currency
conventions. - Compare suspicious values with the original source if
available.

Do not automatically delete outliers: they may be valid products or may
reflect a different meaning of the field.

**Decision/log:** Pending.

### 4.6 Review-count validation

**Checks** - Identify null, negative, fractional, or unusually high
review counts. - Confirm whether the field is a cumulative product-level
count or a count of reviews in a particular period. - Check for repeated
product-level totals across multiple records.

Do not sum repeated cumulative totals over time and describe the result
as new reviews received without a valid methodology.

**Decision/log:** Pending.

### 4.7 Date validation

**Checks** - Confirm all nonblank `Order Date` values parse
successfully. - Check the minimum and maximum dates. - Inspect records
outside the expected date range. - Check for future dates or implausible
values, if relevant. - Confirm that Power BI uses the intended date
column and date-table relationship.

**Reported range to verify:** January 2019 to December 2022.

**Decision/log:** Pending.

### 4.8 Shipment validation

**Checks** - Inspect distinct values and missing values. - Confirm
whether `Shipment` describes a status, method, date, or another
attribute. - Standardize values only after the field meaning is known.

**Decision/log:** Pending.

## 5. Power Query Preparation Workflow

Use this workflow only for steps that are applicable to the source data:

1.  Connect Power BI to the source workbook.
2.  Verify the worksheet and expected columns.
3.  Assign appropriate data types.
4.  Inspect missing values and errors.
5.  Trim and clean text fields.
6.  Review category inconsistencies.
7.  Investigate duplicate rows.
8.  Validate price, review-count, shipment, and date fields.
9.  Apply only justified corrections.
10. Rename queries and steps clearly.
11. Load the prepared data and validate the report measures.

Keep the raw source unchanged so that cleaning decisions can be
reproduced.

## 6. Post-Cleaning Validation

After preparing the data, compare the original and cleaned versions.

  Validation item                                        Status    Result / notes
  ------------------------------------------------------ --------- ----------------
  Row count before and after cleaning recorded           Pending   
  Missing values reviewed                                Pending   
  Data types verified                                    Pending   
  Category whitespace and inconsistent labels reviewed   Pending   
  Duplicate rows investigated                            Pending   
  Price anomalies investigated                           Pending   
  Review-count semantics verified                        Pending   
  Date range verified                                    Pending   
  Shipment values understood                             Pending   
  KPI totals reconciled with source records              Pending   
  Quarter and category slicers tested                    Pending   

Record actual counts, decisions, and reasons in the notes column rather
than simply marking each item complete.

## 7. Impact on Dashboard Measures

Before publishing the dashboard, verify that:

-   The sales measure matches the confirmed meaning of the price or
    transaction data.
-   The products-sold KPI is supported by a genuine quantity or
    appropriate record grain.
-   YTD and QTD calculations use the intended date field and reporting
    convention.
-   YTD Reviews is based on valid time-based review data, if presented
    as a time-based metric.
-   `% YTD Sales` uses the correct denominator.
-   Category totals and KPI values reconcile under the intended filter
    context.
-   Slicer interactions are consistent and do not produce misleading
    comparisons.

Refer to `docs/kpi_definitions.md` for measure definitions and
validation rules.

## 8. Data Privacy and Publication

Before committing the workbook to a public repository:

-   Confirm the source license permits redistribution.
-   Check for personal, confidential, or otherwise restricted data.
-   If redistribution is not permitted, omit the workbook and provide a
    legitimate source link and download instructions instead.
-   Do not describe the data as official Amazon sales data unless its
    provenance establishes that claim.

## 9. Cleaning Summary

Complete this section after the checks are performed.

-   **Rows in source:** Pending verification.
-   **Rows retained:** Pending.
-   **Rows removed:** Pending; explain the reason.
-   **Columns transformed:** Pending.
-   **Key quality issues found:** Pending.
-   **Key assumptions:** Pending.
-   **Remaining limitations:** Pending.
-   **Validation date:** Add date after review.

## 10. Completion Standard

This document is complete when the data grain and field meanings are
supported by source evidence, cleaning actions are reproducible,
row-count changes are explained, and the final dashboard measures have
been reconciled with the prepared data.
