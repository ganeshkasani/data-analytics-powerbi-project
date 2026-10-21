# KPI Definitions --- Amazon Products Sales Analysis

## Purpose

This document records the intended meaning, calculation approach, and
validation checks for the KPI cards and supporting measures in the Power
BI dashboard.

**Important:** These are recommended definitions, not confirmation of
the formulas currently implemented in the `.pbix` file. Inspect the
existing DAX measures and compare their results with the source data
before treating the definitions as final.

## 1. Source Fields and Known Constraints

The source workbook includes:

-   `Product Category`
-   `Product Description`
-   `Price(Dollar)`
-   `Number of reviews`
-   `Shipment`
-   `Order Date`

The listed columns do not include an explicit transaction revenue,
quantity sold, order identifier, or star-rating field. Confirm the
dataset's grain and source documentation before deciding what each
measure represents.

## 2. Date and Filter Conventions

Before validating time-based KPIs, document:

-   **Reporting year:** The year selected for YTD analysis.
-   **Calendar or fiscal year:** State which convention the report uses.
-   **Date table:** Confirm whether the model has a dedicated date table
    with a continuous date range.
-   **Date relationship:** Confirm that the date table is related to the
    source table through the intended date field.
-   **Quarter logic:** Confirm whether the quarter slicer selects
    quarters within a specific year or across multiple years.
-   **Filter behavior:** Decide which report filters should affect each
    KPI and test the result.

For conventional calendar-year calculations, use a proper date table
marked as a date table where appropriate, and use its date column for
time-intelligence calculations.

## 3. KPI 1 --- YTD Sales

**Dashboard label:** YTD Sales

**Business meaning:** The cumulative value of the project's defined
sales measure from the start of the selected reporting year through the
current date context.

### Calculation approach

First define a base measure that reflects what the source data actually
supports. For example, if the existing project intentionally sums the
`Price(Dollar)` field, it may be represented as:

``` dax
Sum of Listed Prices =
SUM ( 'Amazon_Data'[Price(Dollar)] )
```

This measure is a sum of listed prices. It must not be called actual
sales revenue unless the source documentation establishes that
interpretation.

With a suitable date table named `Date` and a valid relationship, a
year-to-date version could be:

``` dax
YTD Sum of Listed Prices =
TOTALYTD (
    [Sum of Listed Prices],
    'Date'[Date]
)
```

Use a revenue-based name only if the data truly represents transaction
revenue. Adapt the table and column names to the actual model.

### Validation checklist

-   Confirm the base measure's business meaning.
-   Confirm the date table and active relationship.
-   Select a reporting year and reconcile the YTD result to the
    underlying records.
-   Test behavior at month, quarter, and year boundaries.
-   Confirm whether the quarter slicer should affect this KPI.

## 4. KPI 2 --- QTD Sales

**Dashboard label:** QTD Sales

**Business meaning:** The cumulative value of the defined sales measure
from the start of the selected quarter through the current date context.

### Calculation approach

Using the same valid base measure and date table:

``` dax
QTD Sum of Listed Prices =
TOTALQTD (
    [Sum of Listed Prices],
    'Date'[Date]
)
```

This example calculates quarter-to-date listed prices, not necessarily
actual sales revenue. Rename it according to the verified meaning of the
base measure.

### Validation checklist

-   Confirm quarter start and end dates.
-   Test dates in Q1, Q2, Q3, and Q4.
-   Confirm the selected year is handled correctly.
-   Reconcile the result with source records for the quarter-to-date
    period.
-   Check the interaction between the quarter slicer and the QTD date
    calculation.

## 5. KPI 3 --- YTD Products Sold

**Dashboard label:** YTD Products Sold --- use only if supported by the
source.

**Business meaning:** The number of product units sold during the
year-to-date period. The currently listed source columns do not
establish a quantity sold, so the dashboard's current calculation must
be inspected.

### Choose the measure that matches the data

**If every row represents one verified unit sold**, a row count over the
intended YTD period could represent units sold:

``` dax
YTD Units Sold =
CALCULATE (
    COUNTROWS ( 'Amazon_Data' ),
    DATESYTD ( 'Date'[Date] )
)
```

Do not use this formula unless each row represents one sold unit and the
date field is a valid transaction date.

**If rows represent product listings or product observations**, a row
count is not units sold. Use a truthful label, such as `YTD Records`, if
that is what the measure actually counts.

**If each row represents a product and products can occur multiple
times**, a distinct product count may be appropriate for the question
being asked, but it measures unique products, not units sold:

``` dax
Distinct Products =
DISTINCTCOUNT ( 'Amazon_Data'[Product Description] )
```

This example counts distinct product descriptions in the current filter
context; it is not inherently a YTD units-sold measure.

### Validation checklist

-   Establish what one row represents.
-   Check whether duplicate product descriptions are distinct products
    or repeated observations.
-   Confirm the date field represents the event being measured.
-   Align the KPI label with the verified calculation.
-   Do not infer unit sales from price or review count.

## 6. KPI 4 --- YTD Reviews

**Dashboard label:** YTD Reviews --- only if the source supports a
time-based review measure.

**Business meaning:** Review activity during the year-to-date period, if
the source contains dated review observations.

The field `Number of reviews` may represent a product-level cumulative
total rather than reviews received on the row's `Order Date`. If it is a
cumulative product attribute, applying a YTD date filter to that field
does not necessarily calculate reviews received during the year.

### Calculation approach

If each row records review activity for a particular date and the value
is a valid count of reviews for that date, a measure could be:

``` dax
Total Reviews =
SUM ( 'Amazon_Data'[Number of reviews] )
```

Then, with a valid date table and relationship:

``` dax
YTD Reviews =
TOTALYTD (
    [Total Reviews],
    'Date'[Date]
)
```

Use these examples only if the data semantics support summing dated
review activity. If the source instead contains a cumulative review
count for each product, do not sum repeated product totals across dates
without a defensible methodology. Consider showing a product-level
review count or ranking products by their recorded review count instead.

### Validation checklist

-   Verify what `Number of reviews` means in the original source.
-   Check whether each value is a dated increment or a cumulative
    product total.
-   Check for repeated product-level counts across multiple records.
-   Confirm that the YTD filter measures the intended period.
-   Never describe review volume as a rating or positive sentiment.

## 7. Supporting Measure --- % YTD Sales

The category table in the dashboard displays `% YTD Sales`. Define its
denominator clearly.

A common approach is to divide a category's YTD value by the total YTD
value across all categories, while preserving relevant report filters
and removing only the category filter for the denominator. The exact DAX
depends on the model relationships and desired slicer behavior.

Example pattern:

``` dax
% YTD Sales =
DIVIDE (
    [YTD Sales],
    CALCULATE (
        [YTD Sales],
        REMOVEFILTERS ( 'Amazon_Data'[Product Category] )
    )
)
```

This is a starting pattern, not a verified drop-in formula. Test that
category shares sum to approximately 100% for the intended filter
context and that the quarter slicer behaves correctly.

## 8. Currency and Display Formatting

-   Use the correct currency symbol and units for the source values.
-   Keep number formats consistent across KPI cards and charts.
-   Use compact labels such as `$2.18M` only when the underlying measure
    and currency are verified.
-   Document rounding behavior and ensure rounded category values do not
    appear to contradict totals.
-   Avoid calling the measure revenue until its business meaning is
    confirmed.

## 9. KPI Validation Log

Complete this table after inspecting the actual Power BI model.

  -----------------------------------------------------------------------
  KPI               Formula checked?  Source meaning    Result
                                      verified?         reconciled?
  ----------------- ----------------- ----------------- -----------------
  YTD Sales         Pending           Pending           Pending

  QTD Sales         Pending           Pending           Pending

  YTD Products Sold Pending           Pending           Pending
  / alternative                                         
  label                                                 

  YTD Reviews       Pending           Pending           Pending

  \% YTD Sales      Pending           Pending           Pending
  -----------------------------------------------------------------------

## 10. Finalization Rule

The final dashboard labels, README, and business findings must agree
with the actual DAX formulas and the source data. If a measure cannot be
validated, rename it to a precise description of what it calculates or
document it as an assumption rather than presenting it as a confirmed
business KPI.
