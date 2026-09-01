# E-Commerce Customer Analytics & Executive Dashboard

This repository contains a hands-on data analytics project focused on e-commerce customer behavior, segmentation, and retention strategies using Python.

---

##  Project Summary

The main goal of this analysis is to convert raw customer transaction data into strategic business decisions. The project covers data cleaning, RFM-style custom scoring, churn risk identification for VIP customers, behavioral deep-dives (discount behavior, channel usage, and payment preferences), and ends with an executive decision dashboard.

---

##  Key Analysis Steps

1. **Data Cleaning & AOV Metrics:** Cleaned missing values, standardized numeric features, and computed metrics such as Average Order Value (AOV = Spending / Orders).
2. **Multi-Criteria Scoring:** Created a normalized composite value score based on total spending, transaction frequency, and satisfaction scores to classify customers into Low, Medium, and High Value tiers.
3. **At-Risk VIP Identification:** Filtered high-value customers whose inactivity days exceeded the median threshold, isolating churn-risk accounts that need immediate win-back campaigns.
4. **Behavioral Insights:**
   - **Discounts:** Evaluated satisfaction and return rates between discount users and full-price shoppers.
   - **Device Monetization:** Analyzed the gap between Android (high user volume, lower AOV) and iPhone (lower volume, highest spend per user at ~$3,774).
5. **Pareto Distribution:** Verified revenue concentration to check the 80/20 rule across customer segments.

---

##  Executive Dashboard & Recommendations

The final notebook section generates a 3-chart dashboard alongside 6 core metrics:

* **Regional Performance:** Mapping customer count vs total revenue by city to spot untapped growth areas.
* **At-Risk Matrix:** Isolating VIP accounts exceeding both median spend and median inactivity.
* **Device Spend Breakdown:** Comparing per-user purchasing power across iOS and Android platforms.

### Strategic Action Items

* **City Expansion:** Shift 35% of local advertising toward high-converting hubs (e.g., Tehran, Mashhad) while running free-shipping promotions in lower-tier cities.
* **VIP Churn Prevention:** Automatically route low-satisfaction (<3.0) dormant accounts to support teams, and offer exclusive discount vouchers to dormant, high-satisfaction VIPs.
* **Device Targeting:** Focus high-margin and premium product campaigns on iOS users, while using Android for volume-driven promotions.

---


├── executive_dashboard.png
└── README.md
