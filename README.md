# Amazon Products Sales Analysis Dashboard

## Project Overview

An interactive Power BI dashboard for exploring Amazon product records
by date, category, product description, price-like values, and review
counts. The project demonstrates Power BI dashboard design, DAX
time-intelligence measures, a dedicated date table, data relationships,
and slicer-driven analysis.

> **Important metric note:** The source workbook does not contain a
> dedicated order ID, transaction revenue, or quantity-sold column. The
> current measures sum `Price(Dollar)`, count nonblank
> `Product Category` values, and sum `Number of  reviews`. Therefore,
> the dashboard's "Sales" and "Products Sold" labels should not be
> interpreted as confirmed revenue or units sold without additional
> source evidence.

## Dashboard Preview

![Amazon Products Sales Analysis
Dashboard](images/amazon_sales_dashboard.png)

Open `dashboard/amazon_sales_analysis_dashboard.pbix` in Power BI
Desktop to explore the report interactively.

## Business Questions

-   How does the sum of the price field vary by month and week?
-   Which product categories contribute the largest share of the
    selected price-sum measure?
-   Which product descriptions rank highest by the selected YTD
    price-sum measure?
-   Which product descriptions have the largest summed review counts?
-   How do the displayed metrics change when quarter and
    product-category filters are applied?

These are exploratory questions. The results depend on the source data's
meaning and the report's filter context.

## Dashboard Components

### KPI cards

-   **YTD Sales** --- currently calculated as a year-to-date sum of
    `Price(Dollar)`.
-   **QTD Sales** --- currently calculated as a quarter-to-date sum of
    `Price(Dollar)`.
-   **YTD Products Sold** --- currently calculated as a year-to-date
    count of nonblank `Product Category` values.
-   **YTD Reviews** --- currently calculated as a year-to-date sum of
    `Number of  reviews`.

### Visualizations

-   **Sales by Month:** line chart of the price-sum measure by month.
-   **Sales by Week:** column chart of the price-sum measure by week
    number.
-   **Sales by Product Category:** category comparison table with
    YTD/QTD measures and share of the displayed YTD total.
-   **Top 5 Products by YTD Reviews:** product-description ranking by
    the review-count measure.
-   **Top 5 Products by YTD Sales:** product-description ranking by the
    price-sum measure.

### Filters

-   Quarter slicer
-   Product Category slicer

## Dataset

**Workbook:** `data/amazon_products_raw_data.xlsx`\
**Worksheet:** `Amazon_Data`

The uploaded workbook contains **89,082 rows**, **6 columns**, and dates
from **January 3, 2019 through December 31, 2022**. In the supplied
workbook, the six columns have no blank values according to a basic null
check; this does not replace broader data-quality validation.

  -----------------------------------------------------------------------
  Column                              Meaning / interpretation
  ----------------------------------- -----------------------------------
  `Product Category`                  Category label for the record

  `Product Description`               Product description/name; not
                                      guaranteed to be a unique product
                                      identifier

  `Price(Dollar)`                     Price-like value in dollars; not
                                      verified as transaction revenue

  `Number of  reviews`                Review-count field; confirm whether
                                      it is cumulative or period-specific

  `Shipment`                          Shipment-related text field;
                                      confirm the exact source meaning

  `Order Date`                        Date used for the report's
                                      time-based calculations
  -----------------------------------------------------------------------

**Source and license:** Add the verified original dataset URL and
license before publishing. Public availability alone does not mean a
dataset may be redistributed. Do not imply that this is official Amazon
transaction data unless the source supports that claim.

## Power BI Model and DAX

A date table is created from the minimum and maximum `Order Date`
values:

``` dax
Date Table =
CALENDAR (
    MIN ( Amazon_Data[Order Date] ),
    MAX ( Amazon_Data[Order Date] )
)
```

Additional date columns in the supplied model include month name, month
number, quarter label, quarter number, and week number. The date table
is related to `Amazon_Data`.

Current measures supplied for the report:

``` dax
QTD Sales =
TOTALQTD (
    SUM ( Amazon_Data[Price(Dollar)] ),
    'Date Table'[Date]
)
```

``` dax
YTD Products Sold =
TOTALYTD (
    COUNT ( Amazon_Data[Product Category] ),
    'Date Table'[Date]
)
```

``` dax
YTD Reviews =
TOTALYTD (
    SUM ( Amazon_Data[Number of  reviews] ),
    'Date Table'[Date]
)
```

``` dax
YTD Sales =
TOTALYTD (
    SUM ( Amazon_Data[Price(Dollar)] ),
    'Date Table'[Date]
)
```

The supplied date-column formulas are:

``` dax
Month Name = FORMAT ( 'Date Table'[Date], "MMM" )
Month Number = MONTH ( 'Date Table'[Date] )
Quarters Number = QUARTER ( 'Date Table'[Date] )
Quarter = CONCATENATE ( "Qtr ", 'Date Table'[Quarters Number] )
Week = WEEKNUM ( 'Date Table'[Date] )
```

### Measure interpretation and validation

-   `YTD Sales` and `QTD Sales` are sums of the price field. Rename them
    to reflect that calculation unless the dataset source confirms that
    summing these rows produces valid sales revenue.
-   `YTD Products Sold` counts nonblank category entries. Unless each
    row represents one sold unit, consider a label such as `YTD Records`
    or redefine the measure using a valid quantity/order field.
-   `YTD Reviews` sums review counts by date. If each row contains a
    cumulative product-level review total, this may not measure reviews
    newly received during the year and could double-count totals.
-   `WEEKNUM` returns week numbers that repeat each year. If the dataset
    spans multiple years, week-only charts can combine different years
    unless year is included in the grouping or a unique year-week field
    is used.
-   Confirm that the date relationship is active and that the date table
    is marked as a date table before relying on time-intelligence
    results.

## Observations from the Dashboard

In the supplied all-category screenshot, the displayed YTD price-sum
measure is approximately **\$2.18M**. The category table shows:

  Product category         Displayed YTD measure         Share
  ---------------------- ----------------------- -------------
  Men Shoes                            \$940,266        43.18%
  Camera                               \$492,521        22.62%
  Men Clothes                          \$357,644        16.42%
  Car Accessories                      \$237,290        10.90%
  Toys                                 \$110,839         5.09%
  Mobile & Accessories                  \$39,178         1.80%
  **Total**                      **\$2,177,738**   **100.00%**

Men Shoes and Camera account for approximately **65.8%** of the
displayed total. The monthly visual shows uneven values, with a visible
rise around September and high values again near year-end. These are
descriptive observations from the screenshot; they do not establish why
the values changed.

See [`docs/business_insights.md`](docs/business_insights.md) for
findings, recommendations, and limitations.

## Tools and Techniques

-   Microsoft Power BI Desktop
-   DAX
-   Date-table creation and relationship modeling
-   Interactive slicers and visual interactions
-   Microsoft Excel for source-data inspection

List Power Query or other techniques only if they were actually used in
this project.

## Repository Structure

``` text
amazon-sales-analysis-powerbi/
├── .gitignore
├── README.md
├── data/
│   ├── amazon_products_raw_data.xlsx
│   └── data_dictionary.md
├── dashboard/
│   └── amazon_sales_analysis_dashboard.pbix
├── docs/
│   ├── problem_statement.md
│   ├── kpi_definitions.md
│   ├── data_cleaning_notes.md
│   └── business_insights.md
└── images/
    └── amazon_sales_dashboard.png
```

## How to Open

1.  Clone or download the repository.
2.  Open `dashboard/amazon_sales_analysis_dashboard.pbix` in Power BI
    Desktop.
3.  If prompted, reconnect the source to
    `data/amazon_products_raw_data.xlsx`.
4.  Refresh the report and test the quarter and product-category
    slicers.
5.  Check the KPI definitions and limitations before interpreting the
    displayed values.

## Limitations

-   The sales measure is a sum of prices, not verified transaction
    revenue.
-   The products-sold measure counts nonblank category values, not
    confirmed units.
-   Review-count semantics need source verification.
-   Week numbers can repeat across years.
-   The dataset's source, provenance, and redistribution permissions
    must be confirmed.
-   Findings are descriptive and do not prove causes or future outcomes.
