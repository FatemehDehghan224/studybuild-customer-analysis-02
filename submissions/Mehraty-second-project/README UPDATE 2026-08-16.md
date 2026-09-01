# Project 02 | Customer Behavior Analysis
**Author / GitHub:** Mehraty

Revised version, addressing reviewer feedback. Changes from the first submission are called out inline as **[Fixed]**.

## What's in this project
- `Mehraty_project_02_REVISED.ipynb` — full analysis notebook, now organized strictly Question 1 → Question 6, with extra analyses (RFM, Pareto, Segmentation) kept at the end.
- `customer_data_clean_var2.csv` — cleaned dataset (60 customers, 17 columns).
- Loads via a **relative path** now — runs on any machine. **[Fixed: was an absolute `F:\...` path]**

## Data notes
- Sample size: 60 customers. Small enough that percentages and rankings should be read as directional, not precise estimates.
- `satisfaction_score` is on a **1–5 scale**. **[Fixed: previously reported out of 10 in charts and text]**

## Question 1 — Who is our main customer?
Built from Age Group, Gender, Membership Tier, Device, and Payment Method, each with its own chart.

- **Dominant profile:** 56–65 age group, Male, Gold tier, Android device, pays via Online Wallet.
- Average satisfaction is **2.98 / 5** — below the scale's midpoint. **[Fixed: Device was missing entirely; Age was a raw histogram, not Age Groups; no persona was previously stated]**

## Question 2 — Which city should we advertise in?
Grouped by Province + City, with Customer Count, Revenue, Average Spending, Purchase Count, AOV, and Satisfaction together, plus a Revenue-vs-Satisfaction scatter.

- **Mashhad (Khorasan)** leads on revenue (~$64.1K from 11 customers).
- **Isfahan** stands out on satisfaction (4.40/5) despite lower volume — a lower-risk secondary market worth piloting.
- **[Fixed]** The "Tehran = 1% market share" claim is removed — this dataset has no data on total market size or competitors, so market share isn't calculable from it.
- **[Fixed]** The "Forecasted Revenue" chart is renamed **Expected Customer Value** (`avg_order_value × purchase_count`) — it's an observed-behavior proxy, not a time-series forecast, since we have no monthly/temporal purchase data.

## Question 3 — Top 10 Loyalty Program customers
Selected using a combined **Loyalty Score**: Spending (35%) + Purchase Frequency (25%) + Recency (20%) + Satisfaction (20%), each normalized 0–1. Weights are a stated judgment call, not a data-derived optimum.

**[Fixed]** Previously ranked by `total_spending` alone. Now includes the required scatter (Purchase Count vs Total Spending, point size = recency) and a one-line reason for each of the 10 selected customers.

## Question 4 — Valuable customers at risk
**[Fixed]** Reframed from "churn" to **inactivity risk** — `last_purchase_days` only shows a customer hasn't bought recently; it cannot confirm they won't return.

- Threshold: >90 days inactive **and** in the top 40% by spending (both conditions required, not inactivity alone). This flags **21 of 60** customers — a more targeted list than the previous 50/60. **[Fixed: previous version flagged 50/60 using inactivity alone]**
- Added the required scatter (last purchase days vs. total spending, at-risk customers highlighted) and split the group into **dissatisfied** (service-recovery outreach) vs. **satisfied-but-inactive** (light re-engagement) with different recommended actions.

## Question 5 — Discount, Device, Payment Method
Four charts as specified: Avg Spending by Discount, Avg Returned Items by Discount, Avg Spending by Device, Avg Spending by Payment Method.

- A two-sample t-test on spending and purchase count by discount usage confirms both differences are **not statistically significant** (p ≈ 0.94–0.97). **[Fixed: previously called "statistically insignificant" without running a test]**
- **[Fixed]** Removed unsupported causal claims — "discount lowers profit margin" (no cost data exists in this dataset) and "satisfaction is because of discount, not product quality" (this is observational data; it can't establish causation).

## Question 6 — Executive Report
**[Fixed]** Rebuilt to match the brief exactly: **6 KPIs, 3 charts, 3 recommendations**, each structured as **KPI → Evidence → Action**. The detailed technical notebook above remains available as the supporting technical report.

**6 KPIs:** Total Revenue ($222,907) · Total Customers (60) · Avg Order Value ($212.10) · Avg Satisfaction (2.98/5) · Inactivity Rate >90d (83.3%) · High-Value At-Risk Customers (21)

## Extra analyses (kept from the original)
RFM segmentation, Pareto analysis, and Value×Inactivity segmentation are kept — these were solid additions. Naming was cleaned up (see LTV/Forecast note below) but the logic is unchanged.

- Pareto: the top 20% of customers generate **~54.9%** of revenue — not a classic 80/20 split, and the writeup says so directly rather than forcing the label.

## Naming fixes
- **[Fixed]** "LTV" → **Observed Customer Value** everywhere (`avg_order_value × purchase_count`). It isn't a true Lifetime Value estimate since there's no retention rate or customer lifespan data.
- **[Fixed]** "Monthly Sales Forecast" → renamed or removed. Without time-series/monthly purchase data, this can't be a real forecast.

## Limitations of this dataset
- **Small sample:** 60 customers — rankings and percentages are directional, not statistically robust.
- **No time-series data:** only aggregated totals per customer, so nothing here is a true sales forecast or seasonality read.
- **No cost/margin data:** all figures are revenue, not profit — discount and campaign ROI can't be assessed.
- **No market/competitor data:** market share and penetration claims aren't possible from this data alone.
- **`last_purchase_days` measures inactivity, not confirmed churn** — we can't tell if a customer switched elsewhere or just hasn't needed to buy recently.
- **No reason codes:** returns and low satisfaction scores tell us *that* something happened, not *why*.
- **No acquisition-channel or ad-spend data:** the city recommendation reflects where value already exists, not acquisition cost/efficiency.
- **Satisfaction is a single, undated score per customer** — not tied to a specific purchase or moment.

## Interpretation guardrails
Statements that went beyond what the data can support have been removed or rephrased as open questions rather than conclusions, e.g. "Bronze customers expect less," "Mashhad is saturated," "customers forgot the brand," "the premium strategy isn't working." Where a claim needs more data than this dataset provides, the report says so instead of asserting it.
