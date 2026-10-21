# Data Dictionary --- Amazon Products Sales Analysis

## Purpose

This document describes the fields present in the source workbook used
by the Amazon Products Sales Analysis Power BI dashboard. Field meanings
below are provisional where the original dataset documentation has not
yet been verified.

**Source workbook:** `data/amazon_products_raw_data.xlsx`\
**Worksheet:** `Amazon_Data`

## Dataset Overview

  -----------------------------------------------------------------------
  Attribute                           Details
  ----------------------------------- -----------------------------------
  Reported row count                  89,082 data rows; verify against
                                      the current workbook

  Reported date range                 January 2019--December 2022; verify
                                      after parsing dates

  Dataset grain                       Not yet confirmed; determine what
                                      one row represents

  Original source                     Add verified URL

  License                             Verify source license and
                                      redistribution permission
  -----------------------------------------------------------------------

## Column Definitions

  ------------------------------------------------------------------------------
  Source column           Recommended data  Provisional        Validation notes
                          type              meaning            
  ----------------------- ----------------- ------------------ -----------------
  `Product Category`      Text              Category assigned  Trim whitespace;
                                            to the product or  inspect spelling
                                            record             and category
                                                               consistency

  `Product Description`   Text              Product            Check blanks,
                                            description or     inconsistent
                                            product name       text, and whether
                                                               descriptions
                                                               uniquely identify
                                                               products

  `Price(Dollar)`         Decimal number    Price-like value   Verify whether
                                            expressed in       this is a listing
                                            dollars            price, unit
                                                               price, or
                                                               transaction
                                                               price; do not
                                                               assume it is
                                                               revenue

  `Number of reviews`     Whole number, if  Review count       Confirm whether
                          confirmed         associated with a  the value is
                                            product or record  cumulative or
                                                               represents review
                                                               activity in a
                                                               specific period

  `Shipment`              Depends on source Shipment-related   Inspect distinct
                          definition        attribute          values and verify
                                                               whether it
                                                               represents a
                                                               status, method,
                                                               date, or another
                                                               field

  `Order Date`            Date              Date associated    Verify date
                                            with the record    parsing and
                                                               confirm that it
                                                               is the correct
                                                               date for
                                                               time-based
                                                               calculations
  ------------------------------------------------------------------------------

## Field-Level Notes

### `Product Category`

-   **Role:** Category grouping for comparisons and filtering.
-   **Recommended handling:** Trim leading/trailing whitespace and
    inspect inconsistent labels.
-   **Caution:** Similar labels should not be merged until their
    equivalence is confirmed.

### `Product Description`

-   **Role:** Product label for charts and product rankings.
-   **Recommended handling:** Check for blanks, extra whitespace, and
    inconsistent descriptions.
-   **Caution:** A description is not necessarily a unique product
    identifier. If the dataset has no product ID, document this
    limitation when ranking products.

### `Price(Dollar)`

-   **Role:** Numeric price-like field.
-   **Recommended handling:** Parse as a numeric value and inspect
    missing, zero, negative, and unusual values.
-   **Caution:** Summing prices does not automatically produce actual
    sales revenue. Revenue normally requires a meaningful transaction
    value or a valid price-times-quantity calculation.

### `Number of reviews`

-   **Role:** Review-count field.
-   **Recommended handling:** Check for missing, negative, fractional,
    and unusually large values.
-   **Caution:** Review count is not the same as a star rating or
    sentiment. If the count is a cumulative product attribute, summing
    it across repeated observations may double-count the same reviews.

### `Shipment`

-   **Role:** Shipment-related field whose exact meaning needs
    confirmation.
-   **Recommended handling:** Inspect unique values, missing values, and
    the original source description.
-   **Caution:** Do not assign a business meaning based on the column
    name alone.

### `Order Date`

-   **Role:** Date field used for time-based analysis, subject to source
    verification.
-   **Recommended handling:** Convert to a valid date, inspect errors,
    and establish the minimum and maximum dates.
-   **Caution:** Confirm that this is a transaction or event date before
    using it to calculate YTD/QTD sales or reviews.

## Suggested Power BI Model

For conventional time-intelligence calculations, consider a dedicated
calendar table with a continuous date range and a one-to-many
relationship from the date table to the source table, provided the
source date semantics support it.

Document the actual model here:

-   **Fact/source table name:** Pending verification.
-   **Date table name:** Pending verification.
-   **Date relationship:** Pending verification.
-   **Reporting calendar:** Calendar year or fiscal year --- pending.
-   **Dataset grain:** Pending source verification.

Do not create a relationship or apply time-intelligence logic merely
because a date-like column exists; confirm the meaning and uniqueness of
the relevant dates first.

## Confirmed vs. Unconfirmed Metadata

Update this section after reviewing the original dataset source.

  -----------------------------------------------------------------------
  Item                                Status
  ----------------------------------- -----------------------------------
  Original dataset publisher          Pending

  Original download URL               Pending

  Dataset license                     Pending

  Meaning of each source field        Partially inferred from column
                                      names; source verification required

  One-row definition                  Pending

  Currency convention                 Pending

  Whether data represents             Pending
  transactions, listings, or          
  observations                        
  -----------------------------------------------------------------------

## Use in Analysis

This dictionary should be read alongside:

-   `docs/problem_statement.md`
-   `docs/kpi_definitions.md`
-   `docs/data_cleaning_notes.md`

Keep the dictionary synchronized with the actual workbook and Power BI
model. Update it whenever column names, data types, transformations, or
field meanings change.
