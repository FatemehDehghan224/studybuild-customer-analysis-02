# StudyBuild Project 02
# Customer Behavior Analysis

## Project Overview

In this project, I worked as a Junior Data Analyst on an e-commerce customer dataset.

The main goal was not only to summarize the data, but to answer practical business questions related to customer profiling, marketing opportunities, loyalty, retention risk, discount behavior, device usage, payment methods, and executive decision-making.

The analysis was performed using Python with Pandas, NumPy, and Matplotlib.

The final project includes:

- Customer profile analysis
- Geographic marketing analysis
- Loyalty scoring
- High-value customer risk detection
- Discount, device, and payment analysis
- Executive KPI summary
- Three prioritized business recommendations
- Excel output tables
- One-page executive report

---

# Dataset

The cleaned dataset contains customer-level information.

Main variables include:

- `customer_id`
- `first_name`
- `gender`
- `age`
- `city`
- `province`
- `signup_date`
- `membership_tier`
- `purchase_count`
- `avg_order_value`
- `total_spending`
- `last_purchase_days`
- `payment_method`
- `device`
- `discount_used`
- `returned_items`
- `satisfaction_score`

The cleaned dataset used in this project is:

`cleaned_dataset.xlsx`

---

# Data Validation

Before beginning the analysis, several basic checks were performed.

These included:

- Checking required columns
- Reviewing missing values
- Reviewing duplicate records
- Converting `signup_date` to datetime
- Confirming numerical columns were suitable for analysis

Missing values were handled separately for each analysis rather than deleting all incomplete rows globally.

This approach avoids unnecessarily reducing the available sample.

---

## Important Note About Returned Items

A true return rate was not calculated.

The dataset contains:

- `returned_items`: number of returned items
- `purchase_count`: number of purchases/orders

These variables have different units.

Therefore:

`returned_items / purchase_count`

cannot be interpreted as a true item return rate.

Instead, this project reports:

**Average Returned Items**

when comparing customer groups.

A true return rate would require information about the total number of items purchased.

---

# Question 1
# Who Are the Main Customers?

The first analysis focused on understanding the current customer profile.

The following dimensions were examined:

- Age group
- Gender
- Membership tier
- Device
- Payment method

Age was divided into the following groups:

- Under 25
- 25–34
- 35–44
- 45–54
- 55–64
- 65+

A summary table was created containing:

- Total number of customers
- Average age
- Median age
- Dominant age group
- Dominant gender
- Dominant membership tier
- Dominant device
- Dominant payment method

Four main visualizations were produced:

1. Customer count by age group
2. Membership tier distribution
3. Device distribution
4. Payment method distribution

---

## Dominant Customer Persona

The dominant customer persona was created using the most common characteristics in the dataset.

Example structure:

**Typical Customer = Dominant Age Group + Dominant Gender + Dominant Membership + Dominant Device + Dominant Payment Method**

This persona represents the most frequently observed customer profile in the current dataset.

It should not be interpreted as representing every customer.

---

## Marketing Implication

The dominant persona can help guide:

- Campaign targeting
- Communication channels
- Device optimization
- Payment experience
- Loyalty messaging

However, other segments should still be tested separately.

The company should avoid assuming that one dominant customer profile represents the entire market.

---

# Question 2
# Which City Is the Best Candidate for Marketing Investment?

Customer performance was analyzed at:

**Province + City**

level.

For each location, the following metrics were calculated:

- Customer count
- Total revenue
- Average customer spending
- Average purchase count
- Average order value
- Average satisfaction

---

## Primary Marketing City

The primary recommended city was selected based mainly on current observed total revenue, while the other metrics were used to understand the trade-offs.

The city with the highest observed revenue was selected as the primary candidate for a marketing pilot.

---

## Alternative City

A second city was also identified as an alternative opportunity.

The alternative city was evaluated using:

- Average customer spending
- Average satisfaction
- Customer base size

This is important because a city with lower total revenue may still have high-value customers and strong customer satisfaction.

---

## Marketing Decision

The recommendation should therefore not be interpreted as:

> This city will definitely produce the highest advertising ROI.

The dataset does not include:

- Advertising cost
- Customer acquisition cost
- Campaign exposure
- Conversion rate
- Marketing channel
- Incremental campaign revenue

Therefore, the analysis identifies promising cities based on existing customer behavior, not actual advertising ROI.

---

## Required Visualizations

Two key charts were created:

1. **Top Cities by Total Revenue**
2. **Total Revenue vs Average Satisfaction**

In the second chart:

- X-axis = Total Revenue
- Y-axis = Average Satisfaction
- Bubble Size = Customer Count

This allows management to compare market size, customer value, and satisfaction simultaneously.

---

# Question 3
# Which Customers Should Be Prioritized for a Loyalty Program?

A multi-factor Loyalty Score was created.

The score uses four customer behavior variables:

- Total Spending
- Purchase Frequency
- Recency
- Satisfaction

All variables were normalized using Min-Max normalization before weighting.

---

## Loyalty Score Weights

The final weights were:

- 35% Total Spending
- 30% Purchase Frequency
- 20% Recency
- 15% Satisfaction

Recency was reversed before scoring.

This means:

**fewer days since the last purchase = higher loyalty contribution**

---

## Why Membership Tier Was Not Included in the Score

Membership tier was not used to calculate the Loyalty Score.

This is intentional.

The objective is to measure customer loyalty based on actual behavior.

If VIP or Gold membership were included directly in the score, existing membership status could artificially increase a customer's ranking.

Instead, membership tier was compared after the Top 10 customers were selected.

This allows the analysis to evaluate whether current membership status is aligned with actual customer behavior.

---

# Top 10 Loyalty Customers

The ten customers with the highest Loyalty Scores were selected.

The final table includes:

- Rank
- Customer ID
- Customer Name
- Membership Tier
- Total Spending
- Purchase Count
- Days Since Last Purchase
- Satisfaction
- Loyalty Score
- Individual Selection Reason

---

## Individual Selection Reasons

Each selected customer receives a reason based on their actual behavior.

Examples include:

- High spending
- High purchase frequency
- Recent activity
- Good satisfaction

This makes the loyalty ranking more explainable and useful for business decision-making.

---

## Loyalty Visualization

The main Loyalty chart shows:

**Purchase Count vs Total Spending**

where:

- X-axis = Purchase Count
- Y-axis = Total Spending
- Point size/color = Recency
- Top 10 Loyalty Customers = highlighted

This visualization helps identify customers who combine strong financial value, frequency, and recent activity.

---

# Question 4
# Which Valuable Customers Are at Risk?

The goal of this analysis was not to label all inactive customers as churned.

Instead, the focus was specifically on customers who were:

- Historically valuable
- Frequent purchasers
- Inactive for a relatively long period

---

## At-Risk Definition

Three conditions were required simultaneously:

### High Spending

`Total Spending >= 75th percentile`

### High Purchase Frequency

`Purchase Count >= Median`

### Long Inactivity

`Last Purchase Days >= 75th percentile`

Only customers satisfying all three conditions were classified as:

**High-Value Customers at Risk**

---

## Important Interpretation

These customers are not confirmed churners.

The dataset does not contain a future observed churn outcome.

Therefore, the correct interpretation is:

**Inactivity Risk**

or:

**Potential Churn Risk**

rather than confirmed churn.

---

# Satisfaction-Based Retention Actions

After identifying At-Risk customers, satisfaction was used to determine the recommended retention strategy.

### Low Satisfaction + Inactivity

Recommended action:

- Service recovery
- Customer feedback
- Identify dissatisfaction causes
- Resolve experience issues before offering incentives

### Good Satisfaction + Inactivity

Recommended action:

- Personalized reminder
- Win-back campaign
- Relevant incentive
- Loyalty offer

This creates a more targeted retention strategy than sending the same promotion to every inactive customer.

---

## At-Risk Visualization

The main chart shows:

**Days Since Last Purchase vs Total Spending**

At-Risk customers are highlighted separately.

The chart also includes:

- Spending threshold
- Inactivity threshold

This makes the business rule visually interpretable.

---

# Question 5
# How Are Discounts, Devices, and Payment Methods Related to Customer Behavior?

This section contains three different analyses.

---

# Discount Analysis

Customers were separated into:

- Discount Users
- Non-Discount Users

The following metrics were compared:

- Average Total Spending
- Average Purchase Count
- Average Order Value
- Average Returned Items
- Average Satisfaction

---

## Interpretation

The results are descriptive.

They show observed differences between groups.

They do not prove that discounts caused:

- Higher spending
- Higher satisfaction
- More purchases
- More returns

The dataset is observational.

Customers were not randomly assigned to discount and non-discount groups.

Therefore, causal conclusions should not be made.

---

## Recommended Next Step

If management wants to estimate the actual effect of discounting, a controlled experiment such as an:

**A/B Test**

would be more appropriate.

---

# Device Analysis

Average customer spending was compared across devices.

The analysis includes:

- Customer count by device
- Average spending by device

This helps identify whether customers using different devices show different observed spending behavior.

---

# Payment Method Analysis

Average customer spending was also compared across payment methods.

The analysis includes:

- Customer count
- Average spending

This can help management identify customer behavior differences across payment options.

However, observed differences should not automatically be interpreted as being caused by the payment method itself.

---

# Required Question 5 Visualizations

Four charts were created:

1. Average Spending by Discount Usage
2. Average Returned Items by Discount Usage
3. Average Spending by Device
4. Average Spending by Payment Method

---

# Question 6
# Five-Minute Executive Report

The final management report was designed to be short enough for executive review.

The report contains exactly:

- 6 KPIs
- 3 charts
- 3 prioritized recommendations

---

# Six Executive KPIs

The final KPI summary contains:

1. Total Customers
2. Total Revenue
3. Average Customer Spending
4. Average Purchase Count
5. Average Satisfaction
6. Number of High-Value At-Risk Customers

These KPIs provide a concise view of:

- Customer scale
- Financial value
- Purchasing behavior
- Experience
- Retention risk

---

# Three Executive Charts

Only three charts were selected for the CEO report:

### 1. Top Cities by Revenue

Purpose:

Identify current high-value geographical markets.

### 2. High-Value Customers at Risk

Purpose:

Show valuable customers who may require immediate retention action.

### 3. Average Spending by Discount Usage

Purpose:

Provide a simple management-level comparison of observed discount behavior.

Detailed visualizations remain available in the technical analysis but are excluded from the executive report to keep it concise.

---

# Three Business Recommendations

## Recommendation 1
### Regional Marketing Pilot

**KPI:** Revenue from Target Region

**Evidence:**  
The primary selected city currently generates the highest observed revenue among the analyzed cities.

**Action:**  
Run a controlled regional marketing pilot in the selected city.

Use the alternative city as a secondary test market or comparison region.

The result should be evaluated using incremental revenue or campaign conversion metrics if campaign data becomes available.

---

## Recommendation 2
### High-Value Customer Reactivation

**KPI:** Reactivation Rate

**Evidence:**  
A group of high-value, frequent customers has not purchased for a relatively long period.

**Action:**  
Launch a segmented win-back campaign.

For dissatisfied customers:

- Gather feedback
- Resolve service issues

For satisfied inactive customers:

- Use personalized reminders
- Offer relevant incentives

---

## Recommendation 3
### Optimize Discount Strategy

**KPI:** Average Customer Spending and Average Returned Items

**Evidence:**  
Discount and non-discount customers show different observed spending and return behavior.

**Action:**  
Do not distribute discounts broadly without testing.

Use targeted discount experiments and evaluate:

- Spending
- Purchase frequency
- Average order value
- Returned items
- Satisfaction

A controlled A/B test is recommended before making causal conclusions.

---

# Project Limitations

This analysis has several limitations.

## 1. Customer-Level Aggregated Data

Each row represents a customer summary rather than an individual transaction.

Therefore, the dataset does not provide complete order-level history.

---

## 2. No True Churn Outcome

The dataset does not indicate whether a customer actually churned in the future.

`last_purchase_days` is only used as an inactivity proxy.

---

## 3. No True Return Rate

The dataset does not provide the total number of items purchased.

Therefore, a true item return rate cannot be calculated.

---

## 4. Observational Discount Data

Discount usage was not randomly assigned.

Therefore, the analysis cannot establish causal discount effects.

---

## 5. No Marketing Cost Data

The dataset does not contain:

- Customer acquisition cost
- Advertising spend
- Campaign conversion
- ROAS
- Incremental campaign revenue

Therefore, the analysis cannot directly determine which city would generate the highest advertising ROI.

---

## 6. No Profit or Margin Data

The dataset contains spending/revenue information but not:

- Product cost
- Gross margin
- Net profit

Therefore, the analysis does not make profitability claims.

---

## 7. Threshold-Based Risk Definition

At-Risk classification depends on statistical thresholds.

Different thresholds may identify different customers.

The selected thresholds are business rules and should be reviewed when more historical customer data becomes available.

---

