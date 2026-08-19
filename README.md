# 🎯 E-Commerce Customer Segmentation: RFM & K-Means Clustering

## 📌 Business Overview
In the e-commerce industry, a "one-size-fits-all" marketing strategy leads to inefficient ad spend, low customer retention, and missed upsell opportunities. 

This project delivers an **end-to-end Machine Learning pipeline** that segments over **4,200 retail customers** into actionable behavioral profiles based on their **Recency, Frequency, and Monetary (RFM)** patterns. By isolating high-volume extreme outliers from core clustering models, this solution enables targeted retention, win-back, and VIP marketing campaigns.

---

## 💡 Key Results & Impact
* **Identified High-Value Whales:** Discovered top VIP buyer segments generating significant revenue spikes (up to $350k+).
* **Automated Outlier Categorization:** Built custom negative-cluster logic (`-1`, `-2`, `-3`) to separate operational B2B bulk buyers from core consumer models.
* **Data-Driven Personas:** Created 7 distinct business personas (`DELIGHT`, `PAMPER`, `REWARD`, `RETAIN`, `UPSELL`, `NURTURE`, `RE-ENGAGE`) tied directly to tailored marketing strategies.

---

## 📊 Segment Breakdown & Strategy Matrix

| Segment Label | Cluster ID | Customer Profile | Strategic Action |
| :--- | :---: | :--- | :--- |
| **DELIGHT** | `-3` | Extreme Spend + High Frequency | White-glove enterprise account management |
| **PAMPER** | `-1` | Extreme One-Off Spenders | VIP luxury perks & personalized cross-selling |
| **UPSELL** | `-2` | High Frequency, Low Ticket | Order-minimum incentives & volume bundling |
| **REWARD** | `3` | High-Value K-Means Champions | Early product access & loyalty reward tiers |
| **RETAIN** | `0` | Active Mid-Tier Core Buyers | Preferred customer discounts & engagement perks |
| **NURTURE** | `2` | Active Low-Value / Casual Buyers | Automated second-purchase triggers |
| **RE-ENGAGE** | `1` | High Recency (Dormant / At-Risk) | Win-back email sequences & reactivation offers |

---

## 🛠️ Tech Stack & Methodology
* **Language:** Python 3.12
* **Data Manipulation:** `pandas`, `numpy`
* **Visualization:** `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn` (StandardScaler, K-Means Clustering, Silhouette Analysis)
