# Customer Analytics Project

## Project Overview

This project analyzes customer-level data to identify key customer segments, geographic investment opportunities, loyalty program priorities, customer retention risks, and behavioral differences associated with discounts, devices, and payment methods.

The main objective is to transform customer data into actionable business insights that can support marketing, customer retention, and management decision-making.

The analysis focuses on six business questions requested by management.

---

## Dataset Description

The dataset contains one row per customer, representing a summary of each customer's observed behavior and characteristics.

The dataset includes information related to:

- Customer demographics
- Location
- Membership tier
- Purchase frequency
- Customer spending
- Recency of the last purchase
- Payment method
- Device
- Discount usage
- Returned items
- Customer satisfaction

---

## Data Quality Checks

Before analysis, the dataset was cleaned and validated to improve consistency and reliability.

The main data quality checks included:

- Checking for missing values
- Identifying and correcting invalid age values
- Converting data types appropriately
- Standardizing text-based categorical variables
- Checking duplicate customer IDs
- Validating date fields
- Checking inconsistencies in total spending
- Reviewing outliers in age and total spending
- Standardizing gender information using the available reference data
- Validating the final dataset structure and column types

The detailed data-cleaning process, including the identified issues, decisions made, and resulting changes to the dataset, is documented in [data-cleaning project](https://github.com/StudyBuildCommunity/studybuild-data-cleaning-01/tree/main/submissions/Mahya-Jabbari).
The cleaned dataset was then used consistently across all six business questions.

---

## Business Questions

### Question 1: Customer Profile

The first analysis identifies the main characteristics of the store's current customer base using age group, gender, membership tier, device, and payment method.

The largest age group is 55-64, representing 16 customers (26.67%). Male customers represent 35 customers (58.33%). Gold is the most common membership tier with 19 customers (31.67%). Android is the most commonly used device with 22 customers (36.67%), while Online Wallet is the most common payment method with 23 customers (38.33%).

Based on these observed characteristics, the dominant customer characteristics in this dataset, considered individually, are male gender, age 55-64, Gold membership, Android device usage, and Online Wallet as the payment method.

However, this dominant profile is based on customer distribution rather than financial value. Therefore, it should not automatically become the sole target of future campaigns. Smaller customer segments may generate higher financial value or show stronger loyalty and should also be evaluated.

---

### Question 2: Geographic Investment Opportunities

Customer metrics were aggregated at both city and province levels to identify locations with stronger advertising potential.

The analysis considered customer count, total customer spending, average customer spending, purchase frequency, average order value, and satisfaction.

Mashhad has the highest total customer spending among the analyzed cities at 43,197.58, with 11 customers. Its average customer spending is 3,927.05 and its average purchase count is 22.64.

Isfahan has a smaller customer base of 5 customers but has the highest average customer spending at 4,395.06 and the highest average satisfaction score at 4.40.

Mashhad's satisfaction score is 2.91, which indicates that customer experience should be monitored before significantly increasing acquisition activity.

Therefore, Mashhad is the primary market recommended for targeted advertising because of its combination of customer volume, total spending, and purchase frequency. Isfahan can be considered an alternative or test market because its smaller customer base shows higher average customer spending and satisfaction.

A high-revenue market with relatively lower satisfaction should not automatically receive substantially more advertising investment, because additional acquisition may increase exposure to an experience that requires improvement.

---

### Question 3: Loyalty Program Prioritization

The loyalty analysis identifies the 10 customers who should receive priority when the loyalty program has limited capacity.

Customers were ranked using a composite loyalty score based on four dimensions:

* Total Spending: 35%
* Purchase Frequency: 30%
* Recency: 20%
* Satisfaction: 15%

The weighting scheme was designed based on the business objective of prioritizing financially valuable and frequently purchasing customers, while also considering recent activity and satisfaction. Total spending received the highest weight because financial value is the primary consideration when allocating a limited number of loyalty benefits. Purchase frequency represents repeated engagement, while recency prevents highly inactive customers from being prioritized solely because of historical value. Satisfaction provides an additional indicator of customer relationship quality.

A sensitivity analysis was performed to assess whether the Top 10 ranking was sensitive to moderate changes in the selected weights. The Top 10 customers remained unchanged in three of the four alternative scenarios, while 9 out of 10 customers remained in the Top 10 under the fourth scenario. This indicates that the customer ranking is relatively robust to moderate changes in the weighting scheme.

The top 10 customers were selected using the calculated loyalty score rather than membership tier alone.

Maryam, a Bronze member, ranked first with a loyalty score of 0.865. She has 31 purchases, total spending of 13,532.74, only 82 days since her last purchase, and a satisfaction score of 4.

The results also demonstrate that membership tier does not always correspond to behavioral loyalty. Some Bronze or Silver customers rank above VIP customers because their observed spending, purchase frequency, recency, and satisfaction produce a higher overall score.

For example, Mina is a Gold member with the highest spending among the selected customers (14,354.34) and 33 purchases, but her satisfaction score is 2 and 165 days have passed since her last purchase. Ali, another Gold customer, has 31 purchases and a satisfaction score of 5 but has not purchased for 224 days. Neda is a VIP customer but ranks seventh because her overall behavioral score is lower than several customers with lower membership tiers.

The loyalty program should therefore prioritize observed customer behavior rather than membership tier alone.

The weighting scheme is an analytical decision for customer prioritization and should not be interpreted as a statistically validated prediction model of future loyalty.

---

### Question 4: Valuable Customers at Risk

A customer was classified as valuable and potentially at risk when all three conditions were met:

- Total spending was at or above the 75th percentile.
- Purchase count was at or above the median.
- Days since the last purchase were at or above the 75th percentile.

Using these criteria, three valuable customers were identified for a potential win-back campaign:

- Customer 1010: 7,241.47 total spending, 19 purchases, 276 days since last purchase, satisfaction score of 1.
- Customer 1035: 5,918.21 total spending, 17 purchases, 365 days since last purchase, satisfaction score of 3.
- Customer 1053: 5,805.54 total spending, 18 purchases, 320 days since last purchase, satisfaction score of 1.

All three customers fall into the high-value, high-inactivity region of the analysis.

Customers 1010 and 1053 have low satisfaction and should therefore receive a personalized service-recovery or feedback-oriented approach rather than a generic discount.

Customer 1035 has a long inactivity period without a low satisfaction score and can be targeted with a personalized re-engagement offer.

These customers should receive priority attention because they combine financial value, purchasing history, and extended inactivity.

However, the analysis does not establish confirmed customer churn. The dataset contains only the number of days since the last purchase and does not provide a complete historical order timeline.

---

### Question 5: Discount, Device, and Payment Behavior

A descriptive comparison was performed to examine customer behavior across discount usage, device, and payment method.

Customers who used discounts had lower average total spending and lower average order value than customers who did not use discounts. Their average purchase count was slightly higher, while their average returned items were slightly lower and their average satisfaction was higher.

The discount comparison was based on 26 discount users and 34 non-discount users.

The observed differences were:

- Average total spending: 2,882.17 with discount vs. 3,736.74 without discount
- Average purchase count: 17.50 with discount vs. 17.29 without discount
- Average order value: 203.29 with discount vs. 220.70 without discount
- Average returned items: 4.08 with discount vs. 4.26 without discount
- Average satisfaction: 3.27 with discount vs. 2.76 without discount

Therefore, discount users did not show higher average spending or higher average returns in this dataset.

Among devices, iPhone customers had the highest average total spending at 3,773.95, based on 18 customers.

Among payment methods, Card users had the highest average total spending at 3,929.01, based on 18 customers.

These findings are descriptive and should not be interpreted as evidence of causal relationships. In particular, the analysis does not prove that using a discount causes spending, purchase frequency, satisfaction, or returns to increase or decrease.

In addition, `returned_items` represents the number of returned items rather than a return rate. Since the total number of purchased items is unavailable, the actual return rate cannot be calculated from this dataset.

---

### Question 6: Executive Five-Minute Report

The final executive dashboard was designed to provide management with a concise overview of the business that can be reviewed within five minutes.

#### Key Performance Indicators

The dashboard includes six KPIs:

- Unique Customers: 60
- Total Customer Spending: 201,985.73
- Average Customer Spending: 3,366.43
- Average Purchase Count: 17.38
- Average Satisfaction: 2.98
- Total Returned Items: 251

#### Selected Visualizations

Three visualizations were selected from the previous analyses:

1. Top 10 Cities by Total Customer Spending
2. Valuable Customers at Risk of Inactivity
3. Average Customer Spending by Discount Usage

These visualizations were selected to highlight the most important geographic opportunity, customer retention risk, and promotional behavior pattern.

#### Evidence → Action → KPI

**1. Geographic Investment**

Evidence: Mashhad has the highest total customer spending among the analyzed cities and also has high customer volume and purchase frequency.

Action: Prioritize targeted advertising in Mashhad while monitoring customer satisfaction. Consider Isfahan as a smaller test market because of its higher average spending and satisfaction.

KPI: Revenue growth and new customer acquisition in target markets.

**2. Customer Retention**

Evidence: Three valuable customers are located in the high-value, high-inactivity region.

Action: Launch personalized win-back campaigns, with service recovery for low-satisfaction customers and re-engagement offers for inactive customers without low satisfaction.

KPI: Customer reactivation rate and repeat purchase rate.

**3. Discount Strategy**

Evidence: Discount users show lower average spending but higher average satisfaction and slightly fewer returned items.

Action: Use customer segmentation to target discounts selectively instead of applying them broadly.

KPI: Average customer spending and average returned items per customer among targeted customers.

---

## Key Findings

The analysis produces several major business insights:

1. The largest customer segment consists of customers aged 55-64, with males, Gold members, Android users, and Online Wallet users representing the dominant categories across the analyzed characteristics.

2. Customer volume alone should not determine marketing investment. Mashhad has the highest total spending and strong purchase frequency, while Isfahan has a smaller customer base but higher average customer spending and satisfaction.

3. Membership tier alone is not sufficient for loyalty program selection. Behavioral scoring can identify lower-tier customers with stronger observed loyalty characteristics than some VIP customers.

4. Three customers combine relatively high financial value, repeated purchases, and long inactivity periods and should be considered for immediate win-back actions.

5. Discount users have lower average spending but higher average satisfaction than non-discount users. They do not show higher average returned items in this dataset.

6. iPhone users and Card users have the highest average customer spending among the analyzed device and payment groups, respectively.

7. The overall customer base consists of 60 unique customers, with total customer spending of 201,985.73 and an average satisfaction score of 2.98.

---

## Business Recommendations

### 1. Protect and Reactivate High-Value Customers

Prioritize high-value customers who have become inactive and use personalized win-back strategies. Low-satisfaction customers should receive service recovery or feedback-oriented communication, while inactive customers with acceptable satisfaction can receive personalized re-engagement offers.

### 2. Use Behavioral Segmentation for Loyalty and Promotion

Do not rely solely on membership tier when allocating loyalty benefits. Similarly, avoid broad discount campaigns. Use observed spending, purchase frequency, recency, and satisfaction to identify customers who are most likely to benefit from targeted loyalty or promotional actions.

### 3. Optimize Geographic Advertising Investment

Use Mashhad as the primary market for targeted advertising because of its combination of customer volume, total spending, and purchase frequency. However, monitor and investigate customer satisfaction before significantly increasing acquisition activity.

Isfahan can be considered as an alternative or test market because, despite its smaller customer base, it has the highest average customer spending and satisfaction among the analyzed cities.


---

## Limitations

Several limitations should be considered when interpreting the results:

- Each row represents a summary of one customer's status rather than individual orders. Therefore, detailed order-level analysis is not possible.
- `last_purchase_days` only indicates the number of days since the customer's last purchase. It does not provide a complete history of purchase timing or customer behavior over time.
- The discount analysis is based only on observed customer groups. Therefore, causal relationships between discount usage and customer behavior cannot be established.
- When the number of customers in a city, group, device, or payment category is small, averages and other statistical measures may be unstable and should be interpreted cautiously.
- The loyalty score weighting scheme was designed for this project and has not been statistically validated as a prediction of future loyalty.
- The at-risk customer definition is a segmentation rule based on percentile thresholds and should not be interpreted as a confirmed churn model.
- The results are based on the available customer-level data and should be interpreted together with the limitations above.

Therefore, the findings should be considered decision-support insights rather than definitive causal or predictive conclusions.
