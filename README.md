# DataCo Smart Supply Chain – Delivery Performance Analysis


## Overview

This project analyzes the **DataCo Smart Supply Chain** dataset, a supply chain and e-commerce dataset covering orders, customers, products, sales, and shipping activity across multiple markets, countries, regions, and cities. The analysis focuses on **shipping performance and delivery delays**, aiming to identify supply chain issues, poor-performing areas, and opportunities to improve the overall delivery process.

The project combines:
- **Python (Pandas)** for data cleaning and transformation
- **Power BI** for interactive dashboarding and visualization
- A written report summarizing methodology, findings, and recommendations

## Repository Contents

| File | Description |
|---|---|
| `DataCo_project.ipynb` | Jupyter notebook with the full data cleaning and feature engineering pipeline |
| `DataCO.pbix` | Power BI dashboard file with all visuals and KPIs |
| `DataCoSupplyChainDataset.csv` | Source dataset (not included — see Data Source below) |

## Data Source

The original dataset contains **180,519 rows and 53 columns**, with each row representing an order item record (order/shipping dates, actual vs. scheduled shipping days, delivery status, shipping mode, order/customer locations, sales, quantity, product details, and delivery risk indicators).

> The raw CSV (`DataCoSupplyChainDataset.csv`) is not included in this repo. To reproduce the notebook, place the dataset in the project root before running the cells.

## Data Cleaning & Transformation

Performed in `DataCo_project.ipynb` using Pandas:

1. **Column selection** – reduced the 53 original columns to 24 relevant to supply chain, shipping, delivery, and geography (e.g. shipping days, delivery status, market, region, sales, shipping mode).
2. **Renaming** – converted all selected columns to a consistent `snake_case` naming convention (e.g. `Days for shipping (real)` → `actual_shipping_days`, `Late_delivery_risk` → `is_late`).
3. **Data quality checks** – inspected missing values and dropped duplicate records.
4. **Type conversion** – converted `order_date` and `shipping_date` to proper `datetime` types.
5. **Feature engineering**:
   - `delivery_delay_days` = `actual_shipping_days` − `scheduled_shipping_days`
   - `order_year`, `order_month` extracted from `order_date`
   - `delay_category` — orders classified as `On Time`, `Slightly Late`, or `Highly Delayed` based on delay days

The result is a clean, analysis-ready dataset used to build the Power BI dashboard.

## Business Questions Explored

1. Which shipping modes have the highest late delivery rates?
2. How does delivery performance vary across markets and regions?
3. What is the overall delivery performance of the supply chain?
4. How has the late delivery rate changed over time (2015–2018)?
5. What is the relationship between shipping performance and overall business activity?
6. Which areas of the supply chain require further investigation?

## Dashboard (`DataCO.pbix`)

Built in Power BI, the dashboard includes:
- Late delivery rate by shipping mode
- Total orders & late delivery rate by country (map)
- Actual vs. scheduled shipping days by market
- Top 5 regions with the highest late delivery rate
- Late delivery rate trend over time (2015–2018)
- Delivery status distribution (on time / late / advance / canceled)
- KPI cards: total sales, average shipping delay, overall late delivery rate, total orders

## Key Findings

- **Overall late delivery rate: ~55%** — more than half of all deliveries were late.
- **Shipping mode matters a lot**: First Class has the highest late rate (95.3%), followed by Second Class (76.6%), while Standard Class has the lowest (38.1%).
- **Actual shipping consistently exceeds scheduled shipping** (~3.5 days actual vs. ~2.9–3.0 days scheduled across markets).
- **Regional variation**: the top 5 regions show late delivery rates between ~56% and 58%.
- **No clear trend over time**: the late delivery rate fluctuates around 0.54–0.56 from 2015–2018, with occasional peaks/dips.
- **Delivery status breakdown**: 54.83% late, 23.04% advance shipped, 17.83% on time, 4.29% canceled.
- Total sales across the dataset: **$36.78M**.

## Recommendations

- Review First and Second Class shipping processes (scheduling, carriers, handling times).
- Improve delivery-time planning using historical performance to set more realistic schedules.
- Investigate the highest-delay regions for carrier, route, or operational causes.
- Set up continuous KPI monitoring (late delivery rate, average delay, on-time rate).
- Analyze root causes behind cancellations alongside late deliveries.

## How to Reproduce

1. Place `DataCoSupplyChainDataset.csv` in the project directory.
2. Install dependencies:
   ```bash
   pip install pandas numpy
   ```
3. Run `DataCo_project.ipynb` end to end to regenerate the cleaned dataset.
4. Open `DataCO.pbix` in Power BI Desktop to explore/refresh the dashboard (point it to the cleaned data if refreshing).

## Conclusion

The analysis shows that late delivery is a significant, persistent supply chain issue — driven largely by shipping mode choice and a consistent gap between scheduled and actual shipping times. These findings give decision-makers a data-driven basis for prioritizing shipping-mode reviews, delivery-time re-planning, and closer monitoring of high-delay regions.
