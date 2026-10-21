# Business Insights --- Amazon Products Sales Analysis

## 1. Purpose and Interpretation

This document summarizes observations visible in the supplied Power BI
dashboard screenshots. It is intended as a portfolio-ready
interpretation of the displayed visuals, not as an independent audit of
the source data or DAX measures.

**Important limitations** - The screenshots show different filter
states, including different quarters and product categories. Values from
different screenshots must not be added together or compared as if they
represented separate periods. - The report's sales measure and the
meaning of `YTD Products Sold` and `YTD Reviews` have not been
independently verified. In particular, the source fields shown for this
project do not clearly establish transaction revenue, units sold, review
sentiment, or star ratings. - Findings below are descriptive
observations. They do not establish causation or prove that the same
patterns will continue.

## 2. Executive Summary

The dashboard provides an interactive view of sales-related values by
month and week, category-level contribution, and product rankings by the
report's sales and review measures.

In the unfiltered dashboard screenshot, the KPI cards display
approximately: - **YTD Sales:** \$2.18M - **QTD Sales:** \$811.09K -
**YTD Products Sold:** 27.75K - **YTD Reviews:** 19.42M

The category table displays a total YTD sales measure of **\$2,177,738**
and a QTD sales measure of **\$811,090**. These totals are broadly
consistent with the rounded KPI cards. The dashboard's current
calculations should still be verified before describing these values as
actual revenue or confirmed units sold.

## 3. Key Observations

### 3.1 Sales-related values are uneven across months

In the unfiltered annual view, the monthly line chart shows relatively
lower values early in the year, a fairly stable middle stretch, and a
marked increase in September. October drops from September, followed by
another increase in November and a high value in December.

**Business interpretation:** Performance appears concentrated in a few
stronger months rather than evenly distributed throughout the year.

**Potential action:** Compare these peaks with promotions, product
availability, pricing changes, and marketing activity if those data
become available. Check the reporting year and completeness of the final
months before drawing a seasonal conclusion.

### 3.2 Weekly performance varies considerably

The weekly column chart shows substantial week-to-week variation, with
several later weeks reaching higher values than many earlier weeks.

**Business interpretation:** Monthly totals may hide short-term spikes
and dips. Weekly monitoring can help identify periods that warrant
investigation.

**Potential action:** Review the underlying dates and validate
week-number logic, particularly if the dataset spans multiple years.
Investigate unusually high weeks against promotions, inventory, or other
explanatory data rather than assuming a cause.

### 3.3 Men Shoes is the largest category by the displayed YTD sales measure

In the all-category table, the displayed values are:

  Product category         YTD sales measure   Share of displayed total
  ---------------------- ------------------- --------------------------
  Men Shoes                        \$940,266                     43.18%
  Camera                           \$492,521                     22.62%
  Men Clothes                      \$357,644                     16.42%
  Car Accessories                  \$237,290                     10.90%
  Toys                             \$110,839                      5.09%
  Mobile & Accessories              \$39,178                      1.80%
  **Total**                  **\$2,177,738**                **100.00%**

**Business interpretation:** Men Shoes represents the largest share of
the displayed measure, at approximately 43%, followed by Camera at
approximately 23%. Together, these two categories account for about
65.8% of the displayed total, indicating that the measure is
concentrated in these categories.

**Potential action:** Investigate whether this concentration reflects
genuine commercial performance, differences in product coverage, or how
the source data and measure are constructed. If the metric is validated
as revenue, category managers could use this view to prioritize deeper
analysis of the largest contributors while monitoring smaller categories
for opportunities.

### 3.4 Product rankings differ by category and filter context

The Top 5 Products by YTD Sales and Top 5 Products by YTD Reviews charts
show different product names, and the rankings change when a product
category or quarter is selected.

**Business interpretation:** A product's position depends on the metric
and the selected slice of the data. High review volume does not
necessarily imply the highest sales-related value.

**Potential action:** Compare the two rankings side by side using
verified product identifiers and consistent time periods. If the
business goal is to understand whether review activity relates to sales,
analyze the relationship at product level with correctly aligned
measures and avoid treating correlation as causation.

### 3.5 Category filters make the report useful for focused investigation

The screenshots show category selections such as Camera, Car
Accessories, Men Clothes, Men Shoes, Mobile & Accessories, and Toys. The
KPI cards and time-series visuals update to reflect different
selections.

**Business interpretation:** The category slicer allows users to move
from an overall view to a category-specific view and examine differences
in monthly and weekly patterns.

**Potential action:** Use the slicer to investigate category-specific
spikes, but verify that all visuals respond correctly and that the
category table's totals and percentages are intended to remain
category-wide or change with the selected filter.

## 4. Filtered-View Observations

The screenshots include multiple quarter selections. They show that the
displayed KPI values, monthly trends, weekly patterns, and top-product
rankings vary with the selected quarter. Examples visible in the
screenshots include:

-   One view displays YTD Sales of approximately **\$347.01K** and QTD
    Sales of approximately **\$347.01K**.
-   Another displays YTD Sales of approximately **\$795.35K** and QTD
    Sales of approximately **\$448.34K**.
-   Another displays YTD Sales of approximately **\$1.37M** and QTD
    Sales of approximately **\$571.30K**.

These values should be treated as snapshots of the dashboard's current
filter states, not as a validated quarterly time series. The equal YTD
and QTD values in one view may be correct for the selected period, but
they should be checked against the intended date logic.

For category-specific screenshots, KPI values change with the selected
category. Do not compare a category-filtered KPI directly with the
all-category KPI without making the filter context explicit.

## 5. Recommended Business Questions for Further Analysis

The current dashboard supports descriptive exploration. The following
questions could deepen the analysis if the required fields are
available:

1.  What events or business activities coincide with the strongest
    monthly and weekly periods?
2.  Are the largest category contributors also the most stable across
    the year?
3.  Do top products by the sales measure also rank highly by review
    count?
4.  Are results affected by missing records, duplicate observations, or
    inconsistent category labels?
5.  How do results change across complete years when the same date logic
    and metric definitions are applied?
6.  Are product-level review counts cumulative totals or reviews
    received during a specific period?

## 6. Recommendations

### Immediate --- validate the measures

-   Confirm whether the sales measure is actual transaction revenue or
    simply the sum of listed product prices.
-   Confirm whether `YTD Products Sold` measures units, rows, distinct
    products, or another count.
-   Confirm whether review counts are time-based or cumulative product
    attributes.
-   Validate the calendar, date relationships, quarter slicer, and
    YTD/QTD logic.
-   Reconcile KPI values with the underlying dataset.

### Next --- improve the analysis

-   Add a clear reporting-year indicator.
-   Ensure week numbers are tied to the correct year and week-start
    convention.
-   Improve truncated product labels, or provide full names in tooltips.
-   Add a documented source and data dictionary.
-   Add margin, quantity, order, or sentiment analysis only if the
    required fields are available and valid.

### Later --- develop stronger commercial insights

If reliable order, quantity, revenue, cost, promotion, inventory, or
review-sentiment data becomes available, extend the analysis to
profitability, units sold, promotional impact, inventory availability,
and customer feedback sentiment.

## 7. Limitations

-   The observations are based on screenshots, not a fresh recalculation
    from the workbook or inspection of the Power BI model.
-   The exact DAX definitions and filter behavior have not been
    independently verified.
-   The data's grain and original source meaning need confirmation.
-   Review count is not equivalent to a product rating or positive
    customer sentiment.
-   A sum of listed prices is not necessarily actual sales revenue.
-   The screenshots do not provide enough evidence to attribute spikes
    to promotions, seasonality, marketing, or other causes.

## 8. Conclusion

The dashboard provides a useful starting point for exploring category
contribution, time-based variation, and product rankings. The clearest
visible pattern is the concentration of the displayed YTD sales measure
in Men Shoes and Camera, alongside uneven monthly and weekly values. The
next priority is to validate the metric definitions and date logic so
that future recommendations are based on defensible business measures
rather than visual patterns alone.
