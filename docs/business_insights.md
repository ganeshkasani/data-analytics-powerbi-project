# Business Insights --- Amazon Products Analysis

## Executive Summary

The Power BI dashboard summarizes the cumulative sum of the
`Price(Dollar)` field, counts nonblank product-category records, and
sums `Number of reviews` over the selected date context. These are the
calculations implemented by the supplied DAX formulas; they should not
automatically be interpreted as actual revenue, units sold, or new
reviews received.

In the all-category screenshot, the dashboard shows: - **YTD Sales
measure:** approximately **\$2.18M** - **QTD Sales measure:**
approximately **\$811.09K** - **YTD Products Sold measure:**
approximately **27.75K** - **YTD Reviews measure:** approximately
**19.42M**

The category table total is **\$2,177,738** for the YTD sales measure.
The findings below are based on the supplied dashboard screenshots and
formulas, not on an independent re-analysis of every source row.

## Key Findings

### 1. The displayed measure is concentrated in Men Shoes and Camera

  Product category         YTD sales measure         Share
  ---------------------- ------------------- -------------
  Men Shoes                        \$940,266        43.18%
  Camera                           \$492,521        22.62%
  Men Clothes                      \$357,644        16.42%
  Car Accessories                  \$237,290        10.90%
  Toys                             \$110,839         5.09%
  Mobile & Accessories              \$39,178         1.80%
  **Total**                  **\$2,177,738**   **100.00%**

Men Shoes and Camera together account for approximately **65.8%** of the
displayed YTD measure. Men Shoes is the largest category in this view.

**Business implication:** These categories dominate the current measure
and are good candidates for deeper analysis. First verify that the
measure is appropriate for commercial decisions: the DAX sums product
prices, and the source fields shown do not establish transaction
revenue.

### 2. Monthly values are uneven across the year

In the all-category annual view, the line chart shows lower values early
in the year, a relatively steady period through the middle months, a
sharp rise in September, a decline in October, and high values again in
November and December.

**Business implication:** Annual totals can hide meaningful changes over
time. Investigate these periods using reliable promotion, inventory,
pricing, or marketing data if available. The chart alone does not prove
seasonality or explain the causes.

### 3. Weekly values vary noticeably

The weekly column chart shows considerable week-to-week variation,
including several higher-value weeks later in the displayed period.

**Business implication:** Weekly monitoring can help identify periods
that deserve investigation. Since `WEEKNUM` is used, confirm the
week-number convention and ensure weeks are not accidentally combined
across different years.

### 4. Product rankings change with the metric and filters

The dashboard's top-five lists differ between the YTD sales measure and
YTD review measure, and the displayed products change when quarter or
category filters are selected.

**Business implication:** A high review count does not necessarily mean
a product has the highest sales measure, the best rating, or the most
positive customer sentiment. Compare products using aligned time periods
and verified metric definitions.

### 5. Category and quarter slicers support focused exploration

The supplied screenshots show KPI cards and charts changing under
different quarter and category selections.

**Business implication:** These filters help users investigate specific
slices of the data. Validate that all intended visuals respond correctly
and that the reporting period remains clear to the reader.

## Measure Definitions and Important Interpretation

The following definitions come directly from the supplied DAX formulas:

-   **YTD Sales:**
    `TOTALYTD(SUM(Amazon_Data[Price(Dollar)]), 'Date Table'[Date])` ---
    cumulative sum of the `Price(Dollar)` field in the year-to-date date
    context. This is not proven transaction revenue.
-   **QTD Sales:**
    `TOTALQTD(SUM(Amazon_Data[Price(Dollar)]), 'Date Table'[Date])` ---
    quarter-to-date sum of the same price field.
-   **YTD Products Sold:**
    `TOTALYTD(COUNT(Amazon_Data[Product Category]), 'Date Table'[Date])`
    --- year-to-date count of nonblank `Product Category` values. Unless
    each row is known to represent one unit sold, label this as a
    record/category count rather than units sold.
-   **YTD Reviews:**
    `TOTALYTD(SUM(Amazon_Data[Number of reviews]), 'Date Table'[Date])`
    --- year-to-date sum of the review-count field. If that field stores
    cumulative product-level totals rather than dated review activity,
    this calculation may not represent reviews received during the year
    and may double-count repeated totals.

The date table is generated from the minimum and maximum `Order Date`
values and is related to `Amazon_Data`. Confirm that the relationship is
active, the date column is suitable for time intelligence, and the date
table is marked as a date table in Power BI.

## Recommendations

1.  **Use accurate KPI labels.** Consider renaming "YTD Sales" to "YTD
    Sum of Listed Prices" unless the dataset source confirms these rows
    represent sales transactions and the sum is valid revenue.
2.  **Rename or redefine "YTD Products Sold."** The current formula
    counts nonblank category entries; use "YTD Records" unless each row
    is confirmed to represent one sold unit.
3.  **Validate the review metric.** Confirm whether `Number of reviews`
    is a dated increment or a cumulative product attribute before
    interpreting it as YTD review activity.
4.  **Validate date logic.** Check YTD/QTD calculations, quarter
    filtering, week numbering, and the reporting year.
5.  **Improve product readability.** Show full product names in tooltips
    and keep rankings sorted by the intended measure.
6.  **Investigate patterns, don't assume causes.** Use additional
    promotion, inventory, transaction, cost, or sentiment data before
    making causal or profitability claims.

## Limitations

-   Findings are based on the supplied screenshots and DAX formulas, not
    a fresh calculation over the full dataset.
-   The visible dataset fields do not establish transaction revenue or
    quantity sold.
-   The current products-sold formula counts nonblank category values.
-   Review counts do not indicate star ratings or positive/negative
    sentiment.
-   Different screenshots show different filter states and must not be
    added together as separate periods.

## Conclusion

The dashboard's clearest visible finding is that Men Shoes and Camera
account for approximately **65.8% of the displayed YTD sum-of-price
measure**. Monthly and weekly values also vary noticeably. Before
treating these patterns as commercial sales insights, validate the
source data's grain and use labels that accurately describe what the DAX
measures calculate.
