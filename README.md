# Retail Sales & Operations Analytics | Power BI

An end-to-end Business Intelligence project that transforms a poorly structured data model into an integrated analytical solution using Power Query, dimensional modeling, a Galaxy Schema, DAX, interactive dashboards, and security-oriented modeling.

## Project Overview

This project focuses on transforming raw operational data into a structured analytical model that supports business decision-making across sales, marketing campaigns, and order fulfillment.

Starting with a poorly organized source data model, I redesigned the data structure by extracting dimension tables, preparing data using Power Query, implementing a Galaxy Schema with multiple fact tables, developing reusable DAX measures, and building four interactive Power BI dashboard pages.

The final solution enables stakeholders to monitor business performance, investigate sales drivers, evaluate marketing engagement and budget utilization, and identify potential bottlenecks in the order lifecycle.

## Business Problem

The original data model was not adequately structured for reliable, scalable business analysis. Descriptive attributes and business processes required a more organized analytical structure to support consistent reporting across multiple business functions.

This created several analytical challenges:

- Limited ability to analyze sales across customers, products, regions, and time.
- Difficulty comparing actual sales performance against targets.
- Limited visibility into campaign expenditure, budget utilization, and click-through rates.
- Insufficient insight into regional delivery performance and order-processing bottlenecks.
- Risk of inconsistent aggregations when combining data from different business processes.
- Need for reusable KPIs and a more maintainable semantic model.
- Need to incorporate security concepts into the analytical model.

### The Solution

I redesigned the analytical foundation rather than simply creating visuals on top of the original tables.

The solution includes:

- Data preparation and transformation using Power Query.
- Extraction of descriptive attributes into dimension tables.
- A Galaxy Schema with multiple fact tables and shared dimensions.
- A centralized DAX measure layer.
- Four interactive dashboards designed around specific business questions.
- Security-oriented modeling using a dedicated security table.
- Interactive filtering, decomposition analysis, drill-through, and page navigation.

The result is a business-focused analytical solution that connects sales performance, campaign effectiveness, and operational efficiency in one Power BI report.

## Technical Architecture

### 1. Data Preparation — Power Query

Power Query was used to prepare the source data for analytical modeling.

The preparation and modeling workflow focused on:

- Inspecting source tables and identifying their analytical roles.
- Preparing tables for dimensional modeling.
- Separating descriptive attributes from transactional and process-related data.
- Maintaining keys required to establish relationships.
- Preparing dates, geographic attributes, and categorical fields for analysis.
- Organizing the data into fact and dimension tables.
- Supporting consistent data types and a refreshable transformation workflow.

### 2. Data Modeling — Galaxy Schema

Instead of relying on a single flat table, I implemented a Galaxy Schema, also known as a Fact Constellation Schema.

This approach supports multiple business processes through separate fact tables connected to shared dimensions where the relationships and data grain allow valid analysis.

The model separates business events from descriptive entities, making the semantic layer more organized, reusable, and maintainable.

#### Fact Tables

The model diagram contains the following fact tables:

| Fact Table | Business Purpose |
|---|---|
| `fact_sales` | Sales performance and profitability analysis |
| `fact_campaign_spend` | Marketing expenditure and campaign engagement |
| `fact_inventory` | Inventory-related analysis |
| `fact_promotion_coverege` | Promotion coverage analysis |
| `fact_order_process` | Order lifecycle and process-duration analysis |
| `fact_sales_targets` | Actual-versus-target performance analysis |

**Modeling note:** The supplied model diagram visibly contains six fact tables, including `fact_sales_targets`. If targets are treated separately from the five operational fact tables in the project's intended documentation, that distinction should be made explicit.

#### Dimension and Supporting Tables

| Table | Purpose |
|---|---|
| `dim_customer` | Customer attributes and customer-level analysis |
| `dim_proudect` | Product attributes and product-level analysis |
| `dim_geo` | Geographic analysis by city and region |
| `dim_campaign` | Campaign attributes |
| `dim_date` | Date-based filtering and time analysis |
| `order_flags` | Order-related classifications and flags |
| `security` | Security-oriented access-control modeling |
| `_measures` | Centralized home for DAX measures |

The names `dim_proudect` and `fact_promotion_coverege` are preserved as they appear in the model. They can be renamed to `dim_product` and `fact_promotion_coverage` in a future cleanup.

#### Modeling Strategy

The modeling approach emphasizes:

- Separating business processes into fact tables with clearly defined grains.
- Extracting descriptive attributes into dimension tables.
- Reusing shared dimensions where appropriate.
- Avoiding unnecessary fact-to-fact joins.
- Maintaining appropriate relationship cardinality and filter propagation.
- Centralizing DAX measures for maintainability.
- Validating totals to avoid duplicated values and incorrect aggregations.
- Supporting time-based analysis through a dedicated date dimension.

This structure provides a foundation for consistent analysis across multiple business processes.

## DAX Measures and KPIs

The report uses DAX measures to support business performance monitoring and interactive analysis.

Key metrics include:

- Total Sales
- Total Profit
- Profit Margin
- Total Active Customers
- Sales vs Target
- Month-over-Month (MoM) Sales Change
- MoM Growth Rate
- Total Campaign Spend
- Budget Usage
- Total Clicks
- Click-Through Rate (CTR)
- Average Days for Delivery
- Average Total Process Duration
- Order-process stage durations

The measures support KPI cards, time-series analysis, campaign comparisons, geographic analysis, and actual-versus-target monitoring.

## Dashboard 1 — Executive Overview

### Business Questions

- What are the overall sales and profitability levels?
- How many active customers are represented?
- Which regions contribute the most sales?
- How close is the business to its sales target?
- How does sales performance change over time?
- Which customers contribute the most revenue?

### Key Performance Indicators

| KPI | Reported Value |
|---|---:|
| Total Sales | 525,956.41 |
| Total Profit | Approximately 194.19K |
| Profit Margin | 37% |
| Active Customers | 47 |
| Sales Target Marker | Approximately 552K |

### Sales Performance

The report shows total sales of **525,956.41**, with a reported profit margin of **37%**.

The sales gauge displays a target marker of approximately 552K.

Based on the rounded visual values:

- Estimated target attainment: **95.3%**
- Estimated gap to target: **26.04K**

These target calculations are estimates based on the screenshot labels and should be validated against the exact DAX target measure before being treated as final financial reporting figures.

### Sales by Region

| Region | Total Sales | Share of Sales |
|---|---:|---:|
| Europe | 166,695.89 | 31.7% |
| Middle East | 117,005.39 | 22.2% |
| Asia Pacific | 103,846.54 | 19.7% |
| North America | 97,436.25 | 18.5% |
| Latin America | 40,972.34 | 7.8% |
| **Total** | **525,956.41** | **100% approximately** |

Percentages are calculated from the displayed regional values and rounded to one decimal place.

### Key Insights

**1. Europe is the largest sales contributor.**

Europe generates 166.70K in sales, representing approximately 31.7% of total revenue.

**2. Latin America has the lowest reported sales contribution.**

Latin America generates approximately 40.97K, or 7.8% of sales.

Europe's reported sales are approximately **4.1 times** Latin America's.

This indicates a substantial difference in regional sales contribution, but it does not by itself establish underperformance. Market size, customer coverage, product mix, and operating costs must also be considered.

**3. Sales are slightly below the displayed target.**

The gauge suggests approximately 95.3% target attainment, leaving an estimated gap of 26.04K against the displayed target marker.

### Business Recommendations

- Investigate the drivers behind Europe's leading contribution and identify practices that may be transferable to other regions.
- Examine Latin America's customer coverage, order volume, average order value, and product mix before deciding whether expansion is justified.
- Break down the sales-target gap by month, region, customer, and product to identify the largest contributors.
- Evaluate revenue and profit together rather than prioritizing sales volume alone.

## Dashboard 2 — Sales Analysis

### Business Questions

- How does sales performance change from month to month?
- Which customers, products, cities, and regions contribute to total sales?
- Which periods show the largest increases or decreases?
- What areas should be investigated to understand sales performance?

### Monthly Sales Analysis

The MoM Analysis visual shows the following values:

| Month | Total Sales | MoM Change | MoM Growth Rate |
|---|---:|---:|---:|
| February 2025 | 30,035.25 | 30,035.25 | Initial displayed period |
| March 2025 | 38,840.06 | +8,804.81 | +29% |
| April 2025 | 47,073.49 | +8,233.43 | +21% |
| May 2025 | 18,705.31 | -28,368.18 | -60% |
| June 2025 | 12,716.23 | -5,989.08 | -32% |
| July 2025 | 22,915.12 | +10,198.89 | +80% |
| September 2025 | 7,556.28 | -15,358.84 | -67% |
| October 2025 | 16,036.80 | +8,480.52 | +112% |
| November 2025 | 29,060.04 | +13,023.24 | +81% |
| December 2025 | 43,332.68 | +14,272.64 | +49% |
| January 2026 | 17,664.33 | -25,668.35 | -59% |
| February 2026 | 36,068.44 | +18,404.11 | +104% |
| March 2026 | 6,742.08 | -29,326.38 | -81% |
| April 2026 | 28,074.88 | +21,332.82 | +316% |
| May 2026 | 32,734.04 | +4,659.16 | +17% |
| June 2026 | 6,132.94 | -26,601.10 | -81% |
| July 2026 | 44,633.82 | +38,500.88 | +628% |
| August 2026 | 21,200.92 | -23,432.90 | -53% |
| September 2026 | 27,977.27 | +6,776.35 | +32% |
| October 2026 | 38,456.45 | +10,479.18 | +37% |

*Values are transcribed from the report screenshot. The displayed timeline omits August 2025, so the missing period and the date-table behavior should be checked before interpreting every change as a consecutive-month comparison. Growth rates are rounded.*

### Key Insights

**1. Sales fluctuate significantly across the displayed periods.**

The highest displayed month is July 2026, with sales of **44,633.82**.

The lowest displayed month is June 2026, with sales of **6,132.94**.

The difference is approximately **38,500.88**, showing substantial variation in monthly sales.

**2. July 2026 shows a sharp recovery.**

Sales increased from 6,132.94 in June 2026 to 44,633.82 in July 2026, corresponding to a displayed growth rate of approximately **628%**.

**3. March 2026 shows a significant decline.**

Sales fell from 36,068.44 in February 2026 to 6,742.08 in March 2026, a displayed decline of approximately **81%**.

**4. The business experienced both strong recoveries and substantial declines.**

April 2026 shows approximately 316% growth, while June 2026 shows approximately 81% negative growth. These patterns warrant further investigation rather than assuming stable growth.

### Decomposition Analysis

The decomposition tree provides a breakdown of sales by region, city, customer, and product.

The displayed tree highlights:

- Europe: 166,695.89
- Amsterdam: 54,808.73
- Cascade Commerce: 22,256.78
- Audio M002: 5,838.12

These values belong to a selected decomposition path and should not be interpreted as the overall contribution of those entities without confirming the tree's filter context.

### Business Recommendations

- Investigate the causes of the sharp monthly changes, including promotions, seasonality, unusual transactions, and data completeness.
- Validate the missing August 2025 period and ensure MoM calculations compare the intended months.
- Use the decomposition tree to identify important customer-product-region combinations for further analysis.
- Develop a more reliable forecasting approach only after investigating the underlying sources of volatility.

## Dashboard 3 — Campaign Analysis

### Business Questions

- How much has been spent on marketing campaigns?
- How much of the allocated budget has been used?
- Which campaigns generate stronger click engagement?
- How does CTR change over time?
- Which campaigns require a budget review?

### Key Performance Indicators

| KPI | Reported Value |
|---|---:|
| Total Clicks | Approximately 224K |
| Total Spend | Approximately 78.84K |
| Budget Usage | 97% |
| Overall CTR | 3% |

### Campaign CTR Comparison

| Campaign | CTR |
|---|---:|
| Back to School | 4.2% |
| Black Friday | 4.2% |
| Spring Launch 2026 | 3.1% |
| Spring Launch | 2.9% |
| New Year Clearance | 2.9% |
| Summer Sale | 2.9% |

### Key Insights

**1. Back to School and Black Friday have the highest displayed CTR.**

Both campaigns report a CTR of **4.2%**, compared with approximately 2.9% for Spring Launch, New Year Clearance, and Summer Sale.

Their displayed CTR is approximately **1.45 times** that of the 2.9% campaigns.

This indicates stronger click engagement, but not necessarily stronger conversion or profitability.

**2. CTR varies over time.**

The displayed trend ranges from approximately **2.5% in July 2025** to a peak of around **4.4% later in 2025**.

Later visible points include approximately 2.9% and 3.1%, suggesting that campaign engagement changes over time.

**3. Overall budget utilization is close to the allocated budget.**

The dashboard reports **97% budget usage**, indicating that expenditure is close to the total budget according to the measure's definition.

However, individual campaign variances must be reviewed separately.

### Spend vs. Budget

The chart displays the following approximate values:

| Campaign | Spend | Budget | Approximate Variance |
|---|---:|---:|---:|
| Black Friday | 28.1K | 30.0K | -1.9K |
| Summer Sale | 14.6K | 15.0K | -0.4K |
| Spring Launch | 12.1K | 12.0K | +0.1K |
| Back to School | 9.2K | 9.0K | +0.2K |
| Spring Launch 2026 | 7.6K | 8.0K | -0.4K |
| New Year Clearance | 7.2K | 7.0K | +0.2K |

*Campaign values are rounded from the screenshot, so the variances are approximate.*

### Business Recommendations

- Investigate why Back to School and Black Friday have higher CTRs and determine whether the performance is consistent across audiences and periods.
- Compare CTR with conversion rates, attributed revenue, cost per conversion, and profit before reallocating budgets.
- Review Spring Launch, Back to School, and New Year Clearance for the small budget overruns visible in the chart.
- Investigate campaign performance over time to distinguish sustained engagement improvements from short-term fluctuations.
- Establish budget alerts and campaign-level variance monitoring.

CTR should be treated as an engagement metric, not a complete measure of marketing ROI.

## Dashboard 4 — Order Process Analysis

### Business Questions

- How long does the order process take?
- What is the average delivery duration?
- Which regions experience longer delivery times?
- Which cities appear among the highest-delay locations?
- Which process stages require further investigation?

### Key Performance Indicators

| KPI | Reported Value |
|---|---:|
| Average Total Process Duration | 31 days |
| Average Days for Delivery | 9 days |

### Delivery Performance by Region

The report visually ranks average delivery duration from highest to lowest as:

1. Latin America
2. North America
3. Europe
4. Asia Pacific
5. Middle East

The exact regional values are not legible in the screenshot, so the ranking is reported without inventing durations.

### Top 5 Cities in Delay

The displayed chart identifies the following cities:

1. Buenos Aires
2. Amsterdam
3. Berlin
4. Sydney
5. Istanbul

The chart does not provide readable numerical labels for the city-level delays in the supplied screenshot.

### Order Process Stage Analysis

The process table displays the following aggregate stage durations:

| Process Stage | Displayed Total Duration |
|---|---:|
| Order to Shipment | 116 days |
| Shipment to Delivery | 213 days |
| Delivery to Invoice | 80 days |
| Invoice to Payment | 752 days |

These are **sums of stage durations**, not averages per order.

### Key Insights

**1. Average total process duration is substantially longer than average delivery duration.**

The dashboard reports 31 days for the total process and 9 days for delivery.

This indicates that the overall lifecycle includes substantial time beyond the delivery-duration KPI, although the precise comparison depends on how each measure is defined.

**2. Latin America appears to have the highest average delivery duration.**

This region should be investigated alongside order volumes, delivery routes, carrier performance, and potential outliers.

**3. Buenos Aires is the leading city in the displayed delay ranking.**

It is followed by Amsterdam and Berlin. These cities are candidates for operational investigation, but order counts and exact delay values should be checked before prioritizing interventions.

**4. Invoice-to-payment has the largest displayed aggregate stage duration.**

The visible total is 752 days, compared with 213 days for shipment-to-delivery.

Because these figures are sums across the displayed order population, they do not establish that invoice-to-payment is the slowest stage for a typical order. Average or median stage duration and the number of orders in each calculation should be validated first.

### Business Recommendations

- Investigate the top-delay cities and regional delivery differences using order counts, carrier data, and route-level performance.
- Compare average and median durations for each process stage.
- If invoice-to-payment delays are confirmed on a per-order basis, investigate payment terms, invoice accuracy, outstanding balances, and collection workflows.
- Establish delivery service-level targets and monitor the percentage of orders meeting those targets.
- Add order counts and on-time-delivery rates alongside average duration KPIs to provide more reliable operational context.

## Security and Access Control

The model includes a dedicated `security` table, reflecting a security-oriented modeling approach.

Power BI Row-Level Security (RLS) can be used to restrict the rows available to different users or roles.

Before deployment, the following should be validated:

- Role definitions and DAX security filters.
- User-to-business-key mappings in the security table.
- Filter propagation to all relevant fact tables.
- Access behavior for users without a matching security mapping.
- Results using Power BI's **View as** functionality.
- Workspace permissions and report-sharing settings.

The presence of the security table is visible in the model, but the supplied screenshots do not independently prove that all RLS rules have been configured and tested successfully. End-to-end security should only be claimed as verified after testing.

## Business Impact

The report provides a unified analytical view across sales, marketing, and operations.

The numerical results identify several areas for further investigation:

- Europe contributes approximately 31.7% of sales, while Latin America contributes approximately 7.8%.
- The sales gauge suggests approximately 95.3% target attainment.
- Monthly sales vary considerably, including a displayed 628% increase in July 2026 and an approximately 81% decline in March 2026.
- Back to School and Black Friday have the highest displayed campaign CTR at 4.2%.
- Overall campaign budget usage is 97%.
- Average total process duration is 31 days, while average delivery duration is 9 days.
- Buenos Aires, Amsterdam, and Berlin appear among the highest-delay cities.
- Invoice-to-payment has the largest visible aggregate stage-duration total and warrants further investigation using per-order statistics.

These findings help prioritize deeper analysis, budget reviews, sales investigations, and operational improvement efforts.

## Tools and Technologies

- **Power BI Desktop** — data modeling, DAX, report development, and interactive analytics.
- **Power Query** — data preparation and transformation.
- **DAX** — KPI development, time-based analysis, and reusable business measures.
- **Dimensional Modeling** — fact and dimension separation.
- **Galaxy Schema** — multi-process analytical modeling using shared dimensions.
- **Power BI Security Concepts** — security table and RLS-oriented design.

## Validation and Limitations

The numerical findings in this README were transcribed from the supplied dashboard screenshots. Some values are rounded or abbreviated, and the report may show different values when filters change.

Before treating the findings as final business conclusions:

- Validate sales, profit, target, and budget measures against their underlying data.
- Confirm the date coverage and missing-period behavior in MoM analysis.
- Reconcile regional sales percentages against total sales.
- Verify campaign-level budget variances using unrounded values.
- Validate city-level delivery delays using exact durations and order counts.
- Compare process-stage averages and medians using a consistent order population.
- Test all RLS roles before describing security as fully implemented.

The report provides descriptive analytics. It does not independently establish the causes of sales fluctuations, the profitability of campaigns, or the causes of delivery delays.

## Conclusion

This project demonstrates the process of turning a poorly structured data model into a business-focused Power BI solution.

By preparing data in Power Query, extracting dimensions, designing a Galaxy Schema, developing reusable DAX measures, incorporating security-oriented modeling, and building four interactive dashboards, I created an analytical framework for investigating sales performance, campaign engagement, and operational efficiency.

The project demonstrates practical skills in **data preparation, dimensional modeling, semantic-layer design, DAX, interactive dashboard development, business analysis, and BI governance**.

---

*Built with Power BI Desktop.*
