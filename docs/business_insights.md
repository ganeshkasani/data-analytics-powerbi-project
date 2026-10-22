# Business Insights — Amazon Products Sales Analysis

## Executive Summary

The dashboard explores product records across categories and dates, using the sum of `Price(Dollar)` as its sales-related measure and the sum of `Number of  reviews` as its review-related measure.

A fresh descriptive check of the uploaded `Amazon_Data` worksheet found **89,082 rows**, covering **January 3, 2019 to December 31, 2022**, with **8 product categories** and **67,942 distinct product descriptions**. Across the full workbook, the sum of `Price(Dollar)` is **$8,420,708**. The all-category dashboard screenshot shows **$2,177,738**, which matches the sum of the price field for **2022** in the workbook. This suggests the screenshot is displaying a 2022 reporting context; confirm the report's page filters and date logic in Power BI before treating that interpretation as definitive.

> **Interpretation warning:** The workbook does not contain a dedicated transaction/order ID, quantity-sold field, or confirmed transaction-revenue field. Consequently, this document calls `SUM(Price(Dollar))` the **price-sum measure** where accuracy matters. It should not be described as verified revenue unless the dataset's provenance and row-level meaning confirm that interpretation. Similarly, counting nonblank category entries measures records, not necessarily units sold.

## Key Findings

### 1. The 2022 dashboard total is consistent with the source workbook

- **Evidence:** The all-category screenshot displays YTD Sales of approximately **$2.18M** and a category-table total of **$2,177,738**. The uploaded workbook's sum of `Price(Dollar)` for 2022 is also **$2,177,738**.
- **Interpretation:** The displayed total is consistent with a 2022 sum of the price field.
- **Business implication:** A year-specific reporting context makes the dashboard easier to interpret and compare. Make the reporting year visible in the report title, a year slicer, or a subtitle.
- **Validation:** Confirm that the page/report filter is actually set to 2022 and that all visuals use the same date context. Do not rely on a matching total alone to prove the model's filter configuration.

### 2. Camera and Men Shoes have the largest price sums across the full dataset

| Category | Sum of `Price(Dollar)` | Share of full-workbook sum |
|---|---:|---:|
| Camera | $2,476,922 | 29.41% |
| Men Shoes | $2,232,016 | 26.51% |
| Men Clothes | $1,168,165 | 13.87% |
| Laptop | $1,086,045 | 12.90% |
| Car Accessories | $628,656 | 7.47% |
| Toys | $354,229 | 4.21% |
| Mobile & Accessories | $333,042 | 3.96% |
| Audio Video | $141,633 | 1.68% |
| **Total** | **$8,420,708** | **100.00%** |

- **Evidence:** These values are calculated directly from all 89,082 workbook rows, across 2019–2022. They are not the same as the screenshot's 2022-only category shares.
- **Interpretation:** Camera and Men Shoes together account for approximately **55.9%** of the full-workbook price sum.
- **Business implication:** These categories are useful priorities for deeper product-level investigation. Compare record counts, price distributions, and time trends before making inventory or marketing decisions.
- **Caution:** A large price sum does not by itself prove high profit, high demand, or high sales volume.

### 3. The price-sum measure varies substantially by year

| Order year | Sum of `Price(Dollar)` | Number of records |
|---|---:|---:|
| 2019 | $1,516,086 | 18,459 |
| 2020 | $3,095,892 | 19,170 |
| 2021 | $1,630,992 | 23,706 |
| 2022 | $2,177,738 | 27,747 |

- **Evidence:** The annual sums and record counts were calculated from `Order Date` and `Price(Dollar)` in the uploaded workbook.
- **Interpretation:** The price sum is highest in 2020, while 2022 has the highest record count. The two measures therefore do not move in lockstep.
- **Business implication:** Track both record counts and price-related measures. A change in a summed price metric may reflect changes in the number of records, product mix, prices, or source-data structure.
- **Caution:** These are descriptive comparisons, not evidence of revenue growth or decline. Confirm the dataset's meaning and completeness before using them as commercial performance indicators.

### 4. Category totals reflect different product-price profiles

- **Evidence:** Across the full workbook, Camera has a mean `Price(Dollar)` of about **$211.23** and a median of **$66**. Laptop has a mean of about **$1,000.96** and a median of **$784**, based on the supplied price field.
- **Interpretation:** The Laptop category has a much higher typical listed-price level than most categories, while Camera's mean is notably above its median, suggesting a right-skewed price distribution or some high-price records.
- **Business implication:** Use median, quartiles, and price-distribution charts alongside sums and averages. This can help identify whether category totals are influenced by a small number of expensive items.
- **Caution:** Price distribution is not a profitability analysis; cost and margin data are not available in the workbook.

### 5. Review counts are concentrated in a few categories, but do not measure sentiment

- **Evidence:** The full-workbook sum of `Number of  reviews` is **58,540,289**. Men Clothes contributes **18,922,701** summed review counts, Men Shoes **11,001,863**, and Mobile & Accessories **9,835,939**.
- **Interpretation:** These categories have the largest sums of the review-count field in the workbook. However, the field may represent a product-level cumulative count repeated across dated records.
- **Business implication:** Use review counts as an engagement or popularity proxy only after confirming their semantics. For customer satisfaction, add verified star ratings, review sentiment, or review text.
- **Caution:** A high review count does not establish positive sentiment, product quality, or customer satisfaction. Do not call this measure “new reviews during the year” unless the source field records review events by date.

### 6. Repeated product descriptions need careful interpretation

- **Evidence:** The workbook has **67,942 distinct product descriptions** across **89,082 rows**. Product descriptions repeat; the number of repeated description occurrences is not evidence of duplicate transactions by itself.
- **Interpretation:** A description is not necessarily a unique product key, and repeated rows may represent repeated dated records or other source-specific observations.
- **Business implication:** Before deduplicating or counting products, establish a stable product identifier and document what one row represents. Preserve valid repeated records.
- **Caution:** Do not remove repeated descriptions or duplicate-looking rows without inspecting the source semantics.

### 7. The monthly screenshot shows visible spikes, but the cause is unknown

- **Evidence:** In the supplied all-category dashboard screenshot, the monthly line rises sharply around September and remains high in November and December. The workbook's full-period monthly totals show high price sums in November and December 2020; these are different reporting contexts and should not be conflated.
- **Interpretation:** The chart indicates month-to-month variation, but the screenshot alone cannot explain whether this is caused by seasonality, product mix, pricing, promotions, record volume, or filter context.
- **Business implication:** Add a year selector and compare the same month across years. Include record counts alongside the price-sum measure to help separate volume effects from price/mix effects.
- **Caution:** Do not attribute spikes to holiday shopping or promotions without supporting evidence.

## Recommendations

### Priority 1 — Correct metric naming and definitions

1. **Rename “YTD Sales” and “QTD Sales”** to something like `YTD Price Sum` and `QTD Price Sum` unless the dataset owner confirms that summing `Price(Dollar)` represents transaction revenue.
2. **Rename “YTD Products Sold”** to `YTD Records` unless each row is verified to represent one sold unit. The current measure counts nonblank `Product Category` values.
3. **Validate “YTD Reviews.”** Determine whether `Number of  reviews` is a cumulative product-level count or a count of reviews created on each order date. If it is cumulative, summing it across rows and dates can overstate review activity.
4. **Define the reporting year explicitly.** The all-category screenshot's $2,177,738 total matches the workbook's 2022 price sum. Display the selected year and verify the page-level filter, date relationship, and slicer interactions.

### Priority 2 — Improve time intelligence

5. **Use a complete date table.** Mark `Date Table` as the model's date table and maintain an active one-to-many relationship from `Date Table[Date]` to `Amazon_Data[Order Date]`.
6. **Sort month names by month number.** Set `Month Name` to sort by `Month Number` so visuals retain January–December order.
7. **Avoid combining week numbers across years.** `WEEKNUM` repeats from year to year. Use a Year-Week label or a week-start date, and decide whether to use standard or ISO week numbering.
8. **Test YTD/QTD calculations under filters.** Confirm that selecting Qtr 1–Qtr 4 returns the expected period and that QTD values reset at quarter boundaries. Check whether “YTD” means calendar-year-to-date or another business year.

### Priority 3 — Improve the dashboard for decision-making

9. **Show the reporting year and metric definitions** near the dashboard title or in a small information tooltip.
10. **Add record count as a separate KPI or companion visual** so viewers can distinguish changes in the number of records from changes in the price sum.
11. **Improve product-name readability.** Use full names in tooltips, provide a product-detail table, and ensure the top-five charts are sorted descending by the intended measure.
12. **Use category-level drill-through.** Allow users to select a category and inspect its top products, price distribution, record count, and monthly pattern.
13. **Use consistent units and precision.** Format dollar values consistently and avoid misleading precision when values are rounded to K/M.
14. **Check visual filter interactions.** Confirm that quarter and category slicers affect every intended KPI and chart consistently.

### Priority 4 — Strengthen data quality and business context

15. **Investigate the 135 exact duplicate rows** found by a basic full-row duplicate check. Determine whether they are legitimate repeated observations before removing any.
16. **Investigate 33 rows with a zero price value.** Confirm whether these represent valid free items, missing/placeholder values, or data errors. No negative price values were found in the basic numeric check.
17. **Document the source and license.** Add the original dataset URL, creator, and redistribution terms before making the workbook public on GitHub.
18. **Avoid causal or profitability claims.** To assess profit, demand, campaign impact, inventory performance, or customer satisfaction, obtain relevant cost, quantity/order, promotion, stock, rating, or sentiment fields.

## Recommended Follow-up Analysis

Once the source semantics are confirmed, useful next analyses include:

- Year-over-year comparisons by category using the same reporting periods.
- Monthly category trends with record counts and price-sum measures shown together.
- Product price distributions by category (median and quartiles).
- Top products by a verified sales or revenue metric, using a stable product identifier.
- Review engagement and sentiment analysis, if review dates, ratings, or review text are available.
- Profitability analysis, if cost and margin data become available.

## Method and Limitations

- **Source-derived evidence:** The dataset totals, dates, category summaries, and basic quality checks in this file were calculated from the uploaded `amazon_products_raw_data.xlsx`, worksheet `Amazon_Data`.
- **Screenshot-derived evidence:** The displayed 2022 category table, dashboard KPI values, and visible monthly pattern were read from the supplied Power BI screenshots.
- **Inference:** The match between the screenshot's $2,177,738 total and the workbook's 2022 price sum suggests a 2022 reporting context; it does not independently prove the report's filter setup.
- The workbook does not establish whether each row represents a transaction, a product listing, a dated product observation, or another unit of analysis.
- The price field is not confirmed transaction revenue, review totals may be cumulative, and no quantity-sold field is present.
- Findings are descriptive and should not be used as causal claims or forecasts.
