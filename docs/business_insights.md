# Business Insights — Amazon Products Sales Analysis

## Executive Summary

This project explores Amazon product records across categories and dates using Microsoft Power BI. It examines the supplied price and review-count fields to identify category-level patterns and changes over time.

The `Amazon_Data` worksheet contains **89,082 records**, dated from **January 3, 2019, to December 31, 2022**, across **8 product categories** and **67,942 distinct product descriptions**. Across the full dataset, the sum of `Price(Dollar)` is **$8,420,708**.

The dashboard screenshot displays **$2,177,738**, matching the sum of `Price(Dollar)` for 2022 in the workbook. This is consistent with a 2022 reporting context, but the dashboard's filter settings have not been independently confirmed.

**Metric interpretation:** The available data does not establish that each row represents a completed transaction or that summing `Price(Dollar)` measures verified revenue. This document therefore uses *price sum* rather than *revenue*. Record counts should not be interpreted as units sold without further evidence.

## Key Findings

### 1. Camera and Men Shoes have the largest full-period price sums

| Product Category | Sum of Price ($) | Share of Full-Period Price Sum |
|---|---:|---:|
| Camera | 2,476,922 | 29.41% |
| Men Shoes | 2,232,016 | 26.51% |
| Men Clothes | 1,168,165 | 13.87% |
| Laptop | 1,086,045 | 12.90% |
| Car Accessories | 628,656 | 7.47% |
| Toys | 354,229 | 4.21% |
| Mobile & Accessories | 333,042 | 3.96% |
| Audio Video | 141,633 | 1.68% |
| **Total** | **8,420,708** | **100.00%** |

Camera and Men Shoes together account for approximately **55.9%** of the full-period price sum.

**Business implication:** These categories are useful candidates for deeper product-level analysis. Comparing their record counts, price distributions, and trends over time may help explain their contribution to the total.

*Scope note: These figures cover 2019–2022 and should not be compared directly with category values from a dashboard view filtered to a single year.*

### 2. The annual price sum and record count follow different patterns

| Order Year | Sum of Price ($) | Number of Records |
|---|---:|---:|
| 2019 | 1,516,086 | 18,459 |
| 2020 | 3,095,892 | 19,170 |
| 2021 | 1,630,992 | 23,706 |
| 2022 | 2,177,738 | 27,747 |

The highest annual price sum occurs in **2020**, while **2022 has the highest record count**.

**Business implication:** Reviewing record counts alongside price sums can help investigate whether differences relate to record volume, product mix, price levels, or the structure of the source data. These descriptive figures do not, by themselves, establish revenue growth or decline.

### 3. Product categories have different price profiles

Across the full dataset:

- **Camera:** Average price of approximately **$211.23** and median price of **$66**.
- **Laptop:** Average price of approximately **$1,000.96** and median price of **$784**.

The Laptop category has a higher typical price level than most categories. For Camera, the average is substantially higher than the median, suggesting that some higher-priced records may influence the average.

**Business implication:** Medians and price-distribution charts can complement averages and totals, helping show typical price levels and the influence of high-price records.

Price data alone does not establish profitability; cost and margin data are not available.

### 4. Review-count totals are concentrated in a few categories

The sum of `Number of reviews` across the workbook is **58,540,289**. The largest category totals include:

- **Men Clothes:** 18,922,701
- **Men Shoes:** 11,001,863
- **Mobile & Accessories:** 9,835,939

These figures are sums of the supplied review-count field, not verified counts of new reviews received during the period.

**Business implication:** Review counts may help explore product engagement after the field's meaning is confirmed. Verified ratings or review text would be needed to assess customer sentiment more directly.

A high review count does not, by itself, demonstrate positive sentiment, product quality, or customer satisfaction.

### 5. The dashboard shows month-to-month variation

The supplied dashboard screenshot shows the monthly price-sum line rising sharply around September and remaining relatively high in November and December. The full-workbook analysis also shows high monthly price sums in November and December 2020; these observations refer to different reporting contexts.

**Business implication:** Comparing equivalent months across years and examining record counts alongside price sums could help investigate recurring patterns and distinguish changes in record volume from changes in price or product mix.

The available evidence does not establish the causes of the observed spikes. Seasonality, promotions, and holiday demand should not be presented as causes without supporting evidence.

### 6. Repeated product descriptions need careful interpretation

The workbook contains **67,942 distinct product descriptions across 89,082 records**. Repeated descriptions do not automatically indicate duplicate records because a description may occur in multiple valid observations.

**Business implication:** Establishing what each row represents and identifying a reliable product key are important before counting unique products or removing records.

## Business Recommendations

Based on the observed patterns, the following actions merit further investigation:

1. **Investigate leading categories:** Examine Camera and Men Shoes at product level to understand their contribution to the overall price sum.
2. **Compare periods consistently:** Compare equivalent months across years and consider record counts alongside price sums.
3. **Understand price distributions:** Use medians and price-distribution analysis to investigate differences between typical prices and averages.
4. **Validate review metrics:** Confirm the meaning of the review-count field before using it to assess product engagement or customer sentiment.

These are suggested areas for investigation, not proven strategies for increasing revenue or profit.

## Method and Limitations

The findings were calculated from the supplied `amazon_products_raw_data.xlsx` workbook, worksheet `Amazon_Data`; dashboard-specific observations were taken from the supplied Power BI screenshots. The dashboard's $2,177,738 total matches the workbook's 2022 price sum, suggesting a 2022 reporting context, but the filter configuration has not been independently confirmed.

The dataset does not establish whether each record represents a transaction, product listing, dated product observation, or another unit of analysis. The sum of `Price(Dollar)` is not confirmed transaction revenue, and record counts do not necessarily represent units sold. The `Number of reviews` field may contain cumulative product-level counts, so its sum cannot automatically be interpreted as new reviews received during the period.

The findings are descriptive. The available data does not establish causation, profitability, customer sentiment, or future performance.
