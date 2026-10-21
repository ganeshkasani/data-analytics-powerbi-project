# Amazon Products Sales Analysis --- Problem Statement

## 1. Background

The project uses an Amazon product dataset to build an interactive Power
BI dashboard for exploring sales-related measures, product categories,
product review counts, and trends over time.

The dashboard is intended for portfolio demonstration and exploratory
analysis. Interpretations must remain consistent with the actual dataset
fields and the definitions implemented in Power BI.

## 2. Business Objective

Create an interactive dashboard that helps users:

-   Track year-to-date (YTD) and quarter-to-date (QTD) sales-related
    measures.
-   Explore monthly and weekly changes in the selected sales measure.
-   Compare sales-related values across product categories.
-   Identify products with the highest values under the report's YTD
    sales measure.
-   Identify products with the largest YTD review counts.
-   Filter the analysis by quarter and product category.

## 3. Dataset Overview

The source workbook is `data/amazon_products_raw_data.xlsx`. Its fields
include:

-   `Product Category`
-   `Product Description`
-   `Price(Dollar)`
-   `Number of reviews`
-   `Shipment`
-   `Order Date`

The dataset should be accompanied by its original source URL and license
or redistribution terms. Confirm the meaning of each field from the
original source before publishing or making business claims.

### Important data limitation

The listed fields do not visibly include a dedicated quantity-sold
field, order ID, or transaction-revenue field. The dashboard's sales
measure must therefore be inspected and documented. If it is calculated
by summing product prices, it should not automatically be described as
actual sales revenue. Likewise, a count of records should not be called
units sold unless each record represents a verified unit sold.

## 4. KPI Requirements

### 4.1 Year-to-Date Sales (YTD Sales)

**Purpose:** Show the cumulative value of the report's defined sales
measure from the start of the applicable year through the selected date
context.

**Requirement:** Display YTD Sales in a KPI card. Confirm the reporting
year, date relationship, filter context, and underlying measure.

**Validation:** Check the value against the underlying records for the
relevant period. Document whether the measure represents transaction
revenue, a sum of listed prices, or another metric.

### 4.2 Quarter-to-Date Sales (QTD Sales)

**Purpose:** Show the cumulative value of the defined sales measure from
the start of the applicable quarter through the selected date context.

**Requirement:** Display QTD Sales in a KPI card and ensure the quarter
slicer behaves as intended.

**Validation:** Confirm quarter boundaries and ensure the result changes
correctly with the selected year and date context.

### 4.3 Year-to-Date Products Sold

**Purpose:** Summarize product movement over the applicable year-to-date
period.

**Requirement:** Display a KPI card for the year-to-date product-count
measure.

**Validation:** Inspect the DAX and dataset grain. Determine whether the
measure counts rows, distinct products, orders, or units. Use the label
**Units Sold** only if the data supports that interpretation; otherwise,
rename the KPI to reflect the actual calculation.

### 4.4 Year-to-Date Reviews (YTD Reviews)

**Purpose:** Summarize the review-count measure over the applicable
year-to-date period.

**Requirement:** Display a KPI card for YTD Reviews.

**Validation:** Confirm whether review counts are associated with dated
observations or product-level totals. Avoid summing repeated
product-level review totals across multiple rows unless that aggregation
is meaningful.

## 5. Chart Requirements

### 5.1 YTD Sales by Month --- Line Chart

**Purpose:** Show the monthly pattern of the defined sales measure.

**Expected use:** Compare months, identify visible increases or
decreases, and explore possible seasonal patterns.

**Validation:** Use a correctly sorted month field and a clearly defined
reporting year. Do not claim seasonality from a single incomplete year.

### 5.2 YTD Sales by Week --- Column Chart

**Purpose:** Show variation in the defined sales measure at a weekly
level.

**Expected use:** Compare weekly performance and investigate short-term
changes.

**Validation:** Define the week-start convention and year/week handling.
Ensure week numbers from different years are not combined
unintentionally.

### 5.3 Sales by Product Category --- Table or Heat Map

**Purpose:** Compare the defined sales measure across product
categories.

**Expected use:** Identify categories with relatively higher or lower
values and display relevant totals or shares.

**Suggested fields:** Product Category, YTD Sales, QTD Sales, and % YTD
Sales, provided each measure is correctly defined.

**Validation:** Check category totals, percentage calculations, sorting,
and the total row. Percentages should use a clearly defined denominator.

### 5.4 Top 5 Products by YTD Sales --- Bar Chart

**Purpose:** Rank the five products with the highest values under the
report's YTD sales measure.

**Expected use:** Highlight the products contributing the largest values
to the selected measure.

**Validation:** Confirm the Top N filter, product-name grouping, tie
handling, and reporting-period context. Describe the ranking as
revenue-based only if the measure represents actual revenue.

### 5.5 Top 5 Products by YTD Reviews --- Bar Chart

**Purpose:** Rank the five products with the highest review-count values
under the report's defined YTD logic.

**Expected use:** Highlight products with comparatively high review
counts.

**Validation:** Confirm how review counts relate to dates and whether
they are cumulative product-level values or dated observations. Review
volume does not establish positive sentiment, customer satisfaction, or
star rating.

## 6. Interactivity Requirements

-   Provide a quarter slicer with the available quarter selections.
-   Provide a product category filter.
-   Verify that slicers filter the intended KPIs, charts, tables, and
    rankings.
-   Ensure the selected reporting period is understandable to users.
-   Keep chart titles, axis labels, currency units, and abbreviations
    readable.
-   Provide sensible behavior when a filter produces no records.

## 7. Data Preparation and Quality Checks

Before publishing the report:

1.  Check missing values and data types.
2.  Trim unnecessary leading and trailing whitespace in text fields.
3.  Investigate duplicate rows before removing them.
4.  Inspect price values for zeros, negative values, and unusual
    outliers.
5.  Validate date parsing and the expected date range.
6.  Establish the grain of the data and what each row represents.
7.  Document Power Query transformations and DAX measures.
8.  Reconcile KPI and category totals against the source data.

Retain an untouched copy of the source workbook and document all
changes.

## 8. Expected Deliverables

-   Interactive Power BI report (`.pbix`).
-   Dashboard preview image (`.png`).
-   Source dataset or a link to obtain it, subject to licensing.
-   Dataset dictionary.
-   KPI definitions and assumptions.
-   Data-cleaning and validation notes.
-   README with project overview, usage instructions, verified findings,
    and limitations.

## 9. Success Criteria

The project is ready for portfolio publication when:

-   All requested KPIs and five visualizations are present.
-   The sales and product-count measures have documented definitions.
-   Date and quarter logic has been validated.
-   Slicers behave correctly across intended visuals.
-   Category totals and KPI calculations reconcile with the source data.
-   The report and screenshot reflect the same final version.
-   Dataset provenance, redistribution permissions, assumptions, and
    limitations are documented.

## 10. Scope and Limitations

This project is a descriptive dashboard, not a causal analysis or a
forecast. It can summarize the measures represented in the data, but it
cannot reliably establish actual revenue, units sold, profitability,
review sentiment, or customer satisfaction unless the source data
contains the necessary fields and the measures are appropriately
defined.

Business insights and recommendations should be added only after the
underlying data and calculations have been validated.
