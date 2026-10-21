# Business Insights --- Amazon Products Sales Analysis

## Key Findings

### 1. Sales measure is concentrated in two categories

The dashboard reports total YTD sales of **\$2,177,738**. Men Shoes
contributes **\$940,266 (43.18%)**, while Camera contributes **\$492,521
(22.62%)**. Together, they represent approximately **65.8%** of the
displayed total.

**Business implication:** These categories dominate the reported sales
measure. Validate their performance and data coverage before
prioritizing resources based on this result.

### 2. Monthly performance is uneven

The all-category monthly chart shows lower values early in the year, a
relatively steady middle period, a sharp rise in September, a decline in
October, and high values again in November and December.

**Business implication:** Annual totals may hide important monthly
changes. Investigate the peak months using promotion, inventory,
pricing, or marketing data if available.

### 3. Weekly values fluctuate

The weekly chart shows noticeable week-to-week variation, including
several high-value weeks later in the displayed period.

**Business implication:** Weekly monitoring may help identify periods
that need investigation. Confirm the year and week-number logic before
comparing weeks across years.

### 4. Top products depend on the selected measure

The top-five products by the dashboard's sales measure are not always
the same as the top-five products by review count. Rankings also change
with the selected quarter and category.

**Business implication:** Review volume should not be treated as a
substitute for sales performance, star rating, or customer sentiment.
Compare product-level metrics only after their definitions and time
periods are aligned.

### 5. Filters support category-level investigation

Quarter and product-category filters change the KPI cards and charts,
allowing users to explore the report at different levels.

**Business implication:** This is useful for investigating
category-specific patterns. Validate that all visuals respond as
intended and that totals and percentages use the expected filter
context.

## Recommended Actions

1.  **Validate the sales measure:** Confirm whether it represents
    transaction revenue or a sum of listed product prices.
2.  **Validate the products-sold KPI:** Confirm whether it counts units,
    rows, or distinct products; rename it if necessary.
3.  **Validate review calculations:** Determine whether review counts
    are time-based or cumulative product-level totals.
4.  **Check time logic:** Verify the reporting year, date relationship,
    YTD/QTD calculations, and week-number convention.
5.  **Improve readability:** Show the reporting year and make full
    product names available in tooltips.
6.  **Add evidence before making causal claims:** Use promotion,
    inventory, cost, order, or sentiment data only if available and
    reliable.

## Important Limitations

-   Findings are based on dashboard screenshots, not an independent
    recalculation of the workbook or DAX measures.
-   The displayed sales measure has not been verified as actual revenue.
-   The meaning of `YTD Products Sold` and `YTD Reviews` requires
    confirmation.
-   Review count does not indicate whether reviews are positive or
    negative.
-   Different screenshots show different filter states; their values
    should not be combined as if they were separate periods.

## Summary

The clearest visible finding is that **Men Shoes and Camera account for
approximately 65.8% of the dashboard's displayed YTD sales measure**.
Monthly and weekly values also vary considerably. Before making business
decisions, verify the measure definitions, date logic, and source-data
meaning.
