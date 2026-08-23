# 📊 StudyBuild – Project 02: Customer Analytics & Segmentation

> **Role:** Junior Data Analyst  
> **Project:** StudyBuild – Project 02  
> **Date:** August 2026

---

## 📌 Executive Summary

The goal of this project was to analyze a cleaned e-commerce customer dataset and extract meaningful business insights related to customer behavior, spending, loyalty, retention risk, discount usage, customer segmentation, and revenue concentration.

Using **Python, Pandas, NumPy, Matplotlib, and Jupyter Notebook**, I performed:

- Dataset validation and consistency checks
- Business summary and key customer metrics
- City-level revenue and customer analysis
- Customer loyalty scoring and Top 10 customer identification
- At-risk customer identification
- Discount usage analysis
- Rule-based customer segmentation
- Pareto analysis of revenue concentration
- Business recommendations
- Data visualization
- Export of analysis results to Excel

---

## 🗂️ Repository Structure

```text
project-02-customer-analytics/

├── data/
│   └── cleaned_dataset.xlsx
│
├── charts/
│   ├── revenue_by_city.png
│   ├── discount_vs_spending.png
│   └── customer_segmentation.png
│
├── notebook/
│   └── customer_analytics.ipynb
│
├── analysis_results.xlsx
│
└── README.md
```

---

## 📊 Dataset

The project uses a cleaned customer dataset containing:

- **60 customers**
- **17 original features**

The original dataset includes:

- Customer ID
- First Name
- Gender
- Age
- City
- Province
- Signup Date
- Membership Tier
- Purchase Count
- Average Order Value
- Total Spending
- Last Purchase Days
- Payment Method
- Device
- Discount Used
- Returned Items
- Satisfaction Score

The dataset was loaded using Pandas:

```python
df = pd.read_excel("cleaned_dataset.xlsx")
```

The original dataset shape was:

```text
(60, 17)
```

During the analysis, additional calculated columns were added, including:

- `calculated_spending`
- `spending_difference`
- `customer_segment`

Therefore, the final DataFrame contains **20 columns**.

---

## 🔎 Data Validation

Before performing the business analysis, several data quality checks were performed.

The following checks were included:

- Dataset structure and data types
- Dataset dimensions
- Missing values
- Duplicate rows
- Duplicate customer IDs
- Spending consistency

### Validation Results

```text
Rows: 60
Original Columns: 17
Missing Values: 0
Duplicate Rows: 0
Duplicate Customer IDs: 0
```

The `signup_date` column is stored as:

```text
datetime64[ns]
```

All customer IDs are unique and no missing values were detected.

---

## 💰 Spending Consistency Check

The consistency between the following variables was validated:

- `purchase_count`
- `avg_order_value`
- `total_spending`

Calculated spending was created using:

```python
df["calculated_spending"] = (
    df["purchase_count"] *
    df["avg_order_value"]
)
```

The difference between recorded and calculated spending was then calculated:

```python
df["spending_difference"] = (
    df["total_spending"] -
    df["calculated_spending"]
)
```

Rows with an absolute difference greater than `0.01` were considered mismatches.

### Result

```text
Rows with spending mismatch: 0
```

Therefore, all recorded `total_spending` values are consistent with:

```text
purchase_count × avg_order_value
```

Small floating-point differences such as `-4.5e-13` were treated as numerical precision effects because they are far below the `0.01` threshold.

---

## 📈 Business Summary

The following key business metrics were calculated:

- Total customers
- Total purchases
- Total revenue
- Average customer spending
- Average order value
- Average satisfaction
- Average returned items

### Results

| Metric | Value |
| :--- | ---: |
| Total Customers | 60 |
| Total Purchases | 1,043 |
| Total Revenue | 201,985.73 |
| Average Customer Spending | 3,366.43 |
| Average Order Value | 213.16 |
| Average Satisfaction | 2.98 |
| Average Returned Items | 4.18 |

The summary was stored in a separate DataFrame and exported to the final Excel workbook.

---

## 🏙️ City Analysis

Customer performance was analyzed by city using:

- Number of customers
- Total purchases
- Total revenue
- Average spending
- Average satisfaction
- Total returned items

The analysis was performed using Pandas `groupby()` and `agg()`.

The resulting table was sorted by total revenue in descending order.

### Key Findings

**Mashhad** generated the highest total revenue:

```text
43,197.58
```

**Tabriz** had the largest number of customers:

```text
12 customers
```

### City Revenue Ranking

| City | Customers | Purchases | Revenue | Avg. Spending | Satisfaction | Returned Items |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| Mashhad | 11 | 249 | 43,197.58 | 3,927.05 | 2.91 | 29 |
| Tabriz | 12 | 189 | 36,192.49 | 3,016.04 | 3.00 | 55 |
| Karaj | 7 | 112 | 26,189.81 | 3,741.40 | 2.86 | 34 |
| Ahvaz | 8 | 111 | 23,384.78 | 2,923.10 | 3.50 | 39 |
| Isfahan | 5 | 99 | 21,975.32 | 4,395.06 | 4.40 | 22 |
| Shiraz | 6 | 98 | 20,715.92 | 3,452.65 | 2.00 | 29 |
| Rasht | 5 | 82 | 15,168.54 | 3,033.71 | 2.60 | 22 |
| Tehran | 6 | 103 | 15,161.29 | 2,526.88 | 2.67 | 21 |

A bar chart was created to visualize total revenue by city.

---

## 🏆 Customer Loyalty Analysis

A custom loyalty score was created to rank customers based on four factors:

| Factor | Weight |
| :--- | ---: |
| Spending | 40% |
| Purchase Frequency | 30% |
| Satisfaction | 20% |
| Recency | 10% |

Each factor was normalized using the maximum value of the corresponding feature.

### Loyalty Score

```text
Loyalty Score =
    Spending Score × 0.40
  + Purchase Score × 0.30
  + Satisfaction Score × 0.20
  + Recency Score × 0.10
```

The customers were then sorted by the resulting loyalty score and the top 10 customers were selected.

### Top 10 Loyalty Customers

| Customer ID | Name | City | Membership | Purchases | Total Spending | Last Purchase Days | Satisfaction |
| :--- | :--- | :--- | :--- | ---: | ---: | ---: | ---: |
| 1057 | Maryam | Ahvaz | Bronze | 31 | 13,532.74 | 82 | 4 |
| 1044 | Mina | Shiraz | Gold | 33 | 14,354.34 | 165 | 2 |
| 1059 | Ali | Isfahan | Gold | 31 | 8,898.55 | 224 | 5 |
| 1009 | Kimia | Karaj | Silver | 34 | 11,615.42 | 232 | 2 |
| 1012 | Arash | Mashhad | Gold | 27 | 11,731.50 | 224 | 2 |
| 1033 | Neda | Tabriz | VIP | 24 | 5,521.20 | 112 | 5 |
| 1004 | Sina | Mashhad | Gold | 23 | 6,121.45 | 40 | 4 |
| 1014 | Reza | Tabriz | VIP | 31 | 3,353.89 | 97 | 4 |
| 1023 | Ali | Mashhad | Bronze | 31 | 3,851.44 | 170 | 4 |
| 1017 | Parsa | Ahvaz | VIP | 30 | 3,239.40 | 135 | 4 |

> Note: The loyalty ranking is based on the custom weighted score, not simply total spending.

---

## 🚨 At-Risk Customer Analysis

At-risk customers were identified using two business rules:

```text
Total Spending >= Median Spending

AND

Last Purchase Days > 180
```

The median `total_spending` was used as the threshold for identifying relatively high-value customers.

The analysis identified:

```text
18 at-risk customers
```

These customers have relatively high spending but have not made a purchase for more than 180 days.

The resulting customer list was sorted by `total_spending` in descending order.

---

## 🎟️ Discount Analysis

Discount usage was first examined using:

```python
df["discount_used"].value_counts()
```

### Discount Usage Distribution

| Discount Used | Customers |
| :--- | ---: |
| No | 34 |
| Yes | 26 |

Customer behavior was then compared between discount users and non-discount users.

The following metrics were analyzed:

- Average spending
- Average purchases
- Average satisfaction
- Average returned items

### Results

| Discount Used | Customers | Avg. Spending | Avg. Purchases | Avg. Satisfaction | Avg. Returned Items |
| :--- | ---: | ---: | ---: | ---: | ---: |
| No | 34 | 3,736.74 | 17.29 | 2.76 | 4.26 |
| Yes | 26 | 2,882.17 | 17.50 | 3.27 | 4.08 |

Customers who used discounts had:

- Higher average satisfaction: **3.27**
- Slightly higher average purchases: **17.50**
- Lower average spending: **2,882.17**

Customers who did not use discounts had higher average spending:

**3,736.74**

A bar chart was created to compare average customer spending based on discount usage.

> These results describe an observed difference between the two groups and do not establish that discounts caused higher satisfaction or lower spending.

---

## 👥 Customer Segmentation

Customers were segmented using predefined business rules based on:

- Total spending
- Purchase count
- Last purchase days

The median values of `total_spending` and `purchase_count` were used as thresholds.

Four customer segments were created:

| Segment | Description |
| :--- | :--- |
| Champions | High spending, high purchase frequency, and recent purchase |
| At Risk | High spending but more than 180 days since last purchase |
| Loyal Customers | High spending and high purchase frequency |
| Needs Attention | Customers who do not meet the conditions above |

### Segment Distribution

| Segment | Customers |
| :--- | ---: |
| Needs Attention | 33 |
| At Risk | 18 |
| Loyal Customers | 7 |
| Champions | 2 |

The segment analysis also calculated:

- Average spending
- Average purchases
- Average last purchase days
- Average satisfaction

### Segment Performance

| Segment | Customers | Avg. Spending | Avg. Purchases | Avg. Last Purchase Days | Avg. Satisfaction |
| :--- | ---: | ---: | ---: | ---: | ---: |
| At Risk | 18 | 5,493.62 | 22.22 | 265.72 | 2.72 |
| Champions | 2 | 9,827.09 | 27.00 | 61.00 | 4.00 |
| Loyal Customers | 7 | 5,610.31 | 28.00 | 141.57 | 3.29 |
| Needs Attention | 33 | 1,338.61 | 11.91 | 182.42 | 3.00 |

A bar chart was created to visualize the number of customers in each segment.

---

## 📊 Pareto Analysis

A Pareto-style analysis was performed to measure revenue concentration among the highest-spending customers.

Customers were sorted by `total_spending` in descending order.

The top 20% of customers were calculated using:

```python
top_20_count = int(np.ceil(len(pareto) * 0.20))
```

For 60 customers:

```text
Top 20% customer count: 12
```

The 12 highest-spending customers generated approximately:

**51.00% of total revenue**

The cumulative revenue percentage was also calculated to create a cumulative revenue curve.

This analysis shows that a relatively small group of customers contributes a significant share of total revenue.

---

## 📊 Visualizations

The project generated and saved the following visualizations.

### 1. Total Revenue by City

Shows total revenue generated by each city.

```text
charts/revenue_by_city.png
```

### 2. Average Spending by Discount Usage

Compares average customer spending between customers who used discounts and those who did not.

```text
charts/discount_vs_spending.png
```

### 3. Customer Segmentation

Shows the number of customers in each customer segment.

```text
charts/customer_segmentation.png
```

The notebook also contains the Pareto cumulative revenue visualization.

---

## 💡 Key Findings

Based on the analysis:

- The dataset contains **60 unique customers**.
- Total purchases equal **1,043**.
- Total revenue is **201,985.73**.
- Average customer spending is **3,366.43**.
- Average order value is **213.16**.
- Average satisfaction score is **2.98**.
- Mashhad generated the highest total revenue.
- Tabriz has the largest number of customers.
- **18 customers** were identified as at risk.
- Customers using discounts have higher average satisfaction but lower average spending.
- **33 customers** were classified as Needs Attention.
- The top **20% of customers (12 customers)** generate approximately **51% of total revenue**.
- Champions have the highest average spending among the defined customer segments.

---

## 💼 Managerial Recommendations

### 1. Focus on High-Value Customers

The top 20% of customers generate approximately 51% of total revenue.

The company should prioritize retaining these customers through:

- Personalized loyalty benefits
- Targeted offers
- Exclusive promotions
- Retention campaigns

The goal is to protect the customer group responsible for a significant portion of revenue.

---

### 2. Reactivate At-Risk Customers

The analysis identified **18 at-risk customers** who have relatively high spending but have not purchased for more than 180 days.

Recommended actions include:

- Personalized reactivation campaigns
- Purchase reminders
- Targeted offers
- Customer-specific incentives

The objective is to encourage these customers to make another purchase.

---

### 3. Use Discounts Strategically

Discount users have higher average satisfaction but lower average spending than customers who did not use discounts.

Therefore, discounts should be used selectively rather than applied broadly.

The company can evaluate discount campaigns based on whether they improve customer engagement, repeat purchases, and retention without unnecessarily reducing customer value.

---

### 4. Prioritize Customer Segments

Different customer segments should receive different strategies:

- **Champions:** Focus on retention and loyalty benefits.
- **Loyal Customers:** Encourage repeat purchases and continued engagement.
- **At Risk:** Focus on reactivation.
- **Needs Attention:** Focus on engagement and understanding customer needs.

---

## 📤 Output

The analysis results were exported to:

```text
analysis_results.xlsx
```

The Excel workbook contains the following sheets:

| Sheet | Content |
| :--- | :--- |
| Summary | Overall business metrics |
| City Analysis | City-level customer and revenue analysis |
| Top 10 Loyalty | Top 10 customers based on loyalty score |
| At Risk | Customers identified as at risk |
| Discount Analysis | Discount usage comparison |
| Segments | Customer segmentation analysis |
| Pareto | Revenue concentration analysis |

The workbook was created using Pandas:

```python
with pd.ExcelWriter("analysis_results.xlsx") as writer:
```

---

## ⚠️ Dataset Limitations

- The dataset contains only **60 customers**, so the results may not represent a larger customer population.
- The data is customer-level data and does not contain detailed transaction-level information.
- The analysis is primarily descriptive and does not establish causal relationships.
- The loyalty score uses manually selected weights.
- Customer segmentation is based on predefined business rules and median thresholds rather than machine learning clustering.
- The dataset does not contain detailed product-level information.
- The analysis does not include profit or operational cost information.
- The discount analysis compares observed groups and should not be interpreted as a causal analysis.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
| :--- | :--- |
| **Python** | Core programming and analysis |
| **Pandas** | Data loading, validation, aggregation, analysis, and Excel export |
| **NumPy** | Numerical calculations |
| **Matplotlib** | Data visualization |
| **Jupyter Notebook** | Interactive analysis and documentation |
| **Microsoft Excel** | Dataset and analysis result storage |

---

## 📁 Files Included

| File | Description |
| :--- | :--- |
| `cleaned_dataset.xlsx` | Cleaned customer dataset |
| `customer_analytics.ipynb` | Jupyter Notebook containing the complete analysis |
| `analysis_results.xlsx` | Exported analysis results |
| `charts/revenue_by_city.png` | Revenue by city visualization |
| `charts/discount_vs_spending.png` | Discount and spending visualization |
| `charts/customer_segmentation.png` | Customer segmentation visualization |
| `README.md` | Project documentation |

---

## 🏁 Result

The cleaned customer dataset was analyzed from multiple business perspectives, including:

- Customer value
- City performance
- Loyalty
- Retention risk
- Discount behavior
- Customer segmentation
- Revenue concentration

The analysis identified high-value customers, at-risk customers, customer segments, discount-related differences, and the contribution of the highest-spending customers to total revenue.

The final analysis tables were exported to Excel, and key visualizations were saved as PNG files for reporting and further use.

---

## 👤 Author

**Melika Khandan**

**Project:** StudyBuild – Project 02  
**Topic:** Customer Analytics & Segmentation  
**Date:** August 2026