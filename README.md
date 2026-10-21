# Amazon Products Sales Analysis Dashboard

## Project Overview

This project presents an interactive Power BI dashboard for exploring
Amazon product data, sales-related measures, product categories, and
product review counts. It was developed as a portfolio project to
demonstrate dashboard design, data preparation, KPI reporting, and
interactive data visualization using Microsoft Power BI.

> **Data interpretation note:** The source workbook contains product
> category, product description, price, number of reviews, shipment, and
> order date fields. It does not visibly contain a dedicated
> quantity-sold, order-ID, or transaction-revenue column. Therefore,
> sales and products-sold measures must be validated against the actual
> Power BI calculations and dataset meaning before being interpreted as
> confirmed revenue or units sold.

## Dashboard Preview

![Amazon Products Sales Analysis
Dashboard](images/amazon_sales_dashboard.png)

Open the Power BI report in
`dashboard/amazon_sales_analysis_dashboard.pbix` to explore the report
interactively. The PNG above is a static preview.

## Business Objective

The objective is to summarize product performance over time and across
product categories, highlight products with high sales-related values or
review counts, and provide interactive filters to support exploratory
analysis.

The dashboard is intended to help users investigate questions such as:

-   How do the selected sales measures change by month and week?
-   Which product categories contribute the largest share of the
    selected sales measure?
-   Which products rank highest by the selected year-to-date sales
    measure?
-   Which products have the largest year-to-date review counts?
-   How do the displayed metrics change when a quarter or product
    category is selected?

These questions are exploratory. Any business conclusion should be
supported by verified measure definitions and the underlying data.

## Dashboard Features

### KPI cards

-   **YTD Sales** --- year-to-date value calculated by the report's
    sales measure.
-   **QTD Sales** --- quarter-to-date value calculated by the report's
    sales measure.
-   **YTD Products Sold** --- the report's year-to-date product-count
    measure; its definition should be checked to confirm whether it
    represents units sold, rows, or another count.
-   **YTD Reviews** --- year-to-date review count based on the report's
    measure.

### Visualizations

-   **Sales by Month:** line chart for monthly trends.
-   **Sales by Week:** column chart for week-level variation.
-   **Sales by Product Category:** category-level comparison using a
    formatted table.
-   **Top 5 Products by YTD Reviews:** bar chart ranking products by
    review count.
-   **Top 5 Products by YTD Sales:** bar chart ranking products by the
    report's sales measure.

### Interactivity

-   Quarter slicer.
-   Product category filter.
-   Cross-filtering and visual interactions, subject to verification in
    the final PBIX report.

## Dataset

The source workbook is stored at:

`data/amazon_products_raw_data.xlsx`

The workbook contains a worksheet named `Amazon_Data` with these fields:

  -----------------------------------------------------------------------
  Field                               Description
  ----------------------------------- -----------------------------------
  `Product Category`                  Product category associated with
                                      the record.

  `Product Description`               Product description or product
                                      name.

  `Price(Dollar)`                     Price value expressed in dollars in
                                      the source data. Confirm its
                                      meaning and data type before using
                                      it as revenue.

  `Number of reviews`                 Number of reviews recorded for the
                                      product.

  `Shipment`                          Shipment-related field; its precise
                                      meaning should be documented from
                                      the source.

  `Order Date`                        Date field used for time-based
                                      analysis.
  -----------------------------------------------------------------------

The workbook was reported to contain 89,082 data rows and dates spanning
January 2019 through December 2022. Reconfirm these details if the
workbook is refreshed or replaced.

### Data source and licensing

Document the original dataset URL, creator, and applicable license here
before publishing:

-   **Source:** Add the original dataset URL.
-   **License/permission:** Verify that redistribution of the dataset is
    permitted.

Do not assume that a dataset is free to redistribute merely because it
is publicly accessible.

## Tools and Techniques

-   **Microsoft Power BI** --- dashboard creation and interactive
    reporting.
-   **Power Query** --- data import and preparation, where used.
-   **DAX** --- KPI and time-based calculations, where used.
-   **Microsoft Excel** --- source workbook inspection.

Only list a tool or technique as used after confirming that it was part
of the actual project workflow.

## Data Preparation and Validation

Before final publication, review and document the following:

1.  Standardize text fields by trimming unnecessary leading and trailing
    whitespace.
2.  Inspect duplicate rows and determine whether they are genuine
    duplicates or valid repeated observations before removing anything.
3.  Validate data types, date values, missing values, and unusual price
    values.
4.  Confirm how `Price(Dollar)` is used in the sales measure.
5.  Confirm whether the data represents product listings, orders, or
    individual transactions.
6.  Validate the definitions of YTD, QTD, products sold, and reviews.
7.  Check that the quarter and category filters produce expected results
    across all visuals.

See `docs/data_cleaning_notes.md` for the detailed validation log and
`docs/kpi_definitions.md` for measure definitions.

## Key Findings and Business Recommendations

Add findings here only after validating the calculations against the
source data. For each finding, include the metric, time period, relevant
category or product, and the business implication.

Suggested structure:

-   **Finding:** State a verified pattern or comparison.
-   **Evidence:** Include the relevant value, period, and visual.
-   **Recommendation:** Suggest a practical action supported by the
    evidence.
-   **Limitation:** Note any data-quality or interpretation constraint.

Do not interpret review count as customer satisfaction or product
rating; review volume alone does not indicate whether reviews are
positive or negative.

## Repository Structure

``` text
amazon-sales-analysis-powerbi/
├── data/
│   ├── amazon_products_raw_data.xlsx
│   └── data_dictionary.md
├── dashboard/
│   └── amazon_sales_analysis_dashboard.pbix
├── docs/
│   ├── problem_statement.md
│   ├── kpi_definitions.md
│   └── data_cleaning_notes.md
├── images/
│   ├── amazon_sales_dashboard.png
│   ├── problem_statement_kpi_requirements.png
│   └── problem_statement_chart_requirements.png
└── README.md
```

If the source data cannot be redistributed, replace the workbook in the
public repository with a source link and instructions for obtaining it
legally.

## How to Use

1.  Download or clone this repository.
2.  Open `dashboard/amazon_sales_analysis_dashboard.pbix` in Microsoft
    Power BI Desktop.
3.  If Power BI prompts for a data-source path, point it to
    `data/amazon_products_raw_data.xlsx` and verify the query steps.
4.  Refresh the report, then validate the KPI values and slicer
    interactions.
5.  Review the documentation in `docs/` before interpreting the metrics.

## Limitations

-   The meaning of the sales measure must be verified; a sum of listed
    prices is not necessarily sales revenue.
-   Product counts should not be described as units sold unless the data
    supports that interpretation.
-   Review counts do not reveal review sentiment or product ratings.
-   Results depend on the source data, reporting-period logic, data
    cleaning, and DAX definitions.
-   Dataset provenance and redistribution permission must be confirmed
    before public sharing.

## Project Status

Portfolio project --- Power BI dashboard and supporting documentation
are being reviewed and refined. Update this status once data validation
and documentation are complete.
