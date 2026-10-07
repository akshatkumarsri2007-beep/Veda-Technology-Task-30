# Veda-Technology-Task-30
# Regional Growth Analysis: Superstore Sales (2023-2025)
--

## Objective

Compare how each region's sales grew over time and practice **period-over-period comparisons**: year-over-year (YoY), quarter-over-quarter (QoQ) and compound annual growth rate (CAGR).

## Deliverables

| Deliverable | Where to find it |
|---|---|
| Growth table | `Task30_Regional_Growth_Analysis.xlsx` (sheet: *Growth Table*) |
| Chart | `Task30_Regional_Growth_Analysis.xlsx` (sheet: *Charts*) and `images/` |
| 5 insights | `Task30_Regional_Growth_Analysis.xlsx` (sheet: *Insights*) and the PDF report |
| SQL queries | `task30_regional_growth.sql` |
| Full written report | `Task30_Regional_Growth_Report.pdf` |

## Dataset

`superstore.csv` / `superstore.xlsx` contain **5,000 orders** from **1 Jan 2023 to 31 Dec 2025**.

> **Note:** This is a **synthetic dataset** that follows the structure of the well-known Superstore dataset. The numbers illustrate the method and are not real company results. The same SQL and Excel logic works on the original Superstore data, since the column names are the same.

**Columns:** Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, Country, City, State, Postal Code, Region, Product ID, Category, Sub-Category, Product Name, Sales, Quantity, Discount, Profit

**Regions:** West, East, Central, South

## Approach

1. Loaded the order data and added `Year` and `Quarter` helper columns.
2. Aggregated sales and profit by region and period (`SUMIFS` in Excel, `GROUP BY` in SQL).
3. Calculated growth with `LAG()` window functions in SQL and equivalent formulas in Excel.
4. Used consistent calendar periods for every region, and checked the 2024 base for small-base effects.
5. Compared same quarters across years to remove seasonality.

## Results

### Yearly sales and growth by region

| Region | 2023 | 2024 | 2025 | YoY 2024 | YoY 2025 | CAGR |
|---|---:|---:|---:|---:|---:|---:|
| West | $395,364 | $565,164 | $655,039 | 42.9% | 15.9% | 28.7% |
| East | $518,726 | $441,844 | $631,415 | -14.8% | 42.9% | 10.3% |
| Central | $374,220 | $388,178 | $382,880 | 3.7% | -1.4% | 1.2% |
| South | $269,257 | $375,577 | $509,146 | 39.5% | 35.6% | 37.5% |
| **Total** | **$1,557,567** | **$1,770,763** | **$2,178,480** | **13.7%** | **23.0%** | **18.3%** |

### Charts

![Yearly sales by region](images/yearly_sales_by_region.png)
![YoY growth by region](images/yoy_growth_by_region.png)
![Quarterly sales by region](images/quarterly_sales_by_region.png)

### Key insights

1. **South is the growth leader.** Sales rose from $269K to $509K (CAGR 37.5%), with strong growth in both 2024 and 2025.
2. **Central is stagnating.** CAGR is only 1.2%, and 2025 sales are slightly below 2024.
3. **East's rebound is partly a small-base effect.** It fell 14.8% in 2024 and then grew 42.9% in 2025. Because 2024 is a low base, the 2025 jump looks bigger than the underlying trend (CAGR 10.3%).
4. **The regional mix is shifting.** South's share of total sales rose from 17.3% to 23.4%, while Central's fell from 24.0% to 17.6%.
5. **Seasonality is strong.** Q4 delivers 30.5% to 35.8% of annual sales depending on region, so same-quarter YoY is a fairer comparison than QoQ.

## Skills demonstrated

- Period-over-period analysis (YoY, QoQ, CAGR)
- SQL window functions (`LAG`, `SUM() OVER`)
- Excel formulas (`SUMIFS`, `IFERROR`), charts and reporting
- Handling seasonality and small-base effects
- Turning data into clear, written insights

## Limitations

- The dataset is synthetic, so conclusions apply to this dataset only.
- Only three years of data are available, so CAGR is sensitive to the starting year and should be read together with the YoY figures.
