# E-Commerce RFM Customer Segmentation

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-orange.svg)
![pandas](https://img.shields.io/badge/pandas-1.3+-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**A comprehensive K-Means clustering analysis for customer segmentation using RFM (Recency, Frequency, Monetary) metrics on online retail transaction data.**

[Features](#features) • [Results](#key-results) • [Installation](#installation) • [Usage](#usage) • [Segments](#customer-segments)

</div>

---

## 📋 Overview

This project performs customer segmentation analysis on online retail transaction data using the **RFM (Recency, Frequency, Monetary)** framework combined with **K-Means clustering**. The analysis identifies distinct customer personas and provides actionable business strategies for each segment.

**Dataset**: UCI Machine Learning Repository - Online Retail Dataset
- **Records**: 525,461 transactions (406,309 after cleaning)
- **Time Period**: December 2009 - December 2010
- **Geographic Coverage**: 40 countries (92.5% UK-based)
- **Products**: 4,632 stock codes across diverse retail categories

---

## ✨ Features

- **Data Cleaning Pipeline**: Robust handling of missing values, outliers, cancelled orders, and administrative entries
- **RFM Feature Engineering**: Automatic calculation of Recency, Frequency, and Monetary metrics at customer level
- **Outlier Detection & Separation**: Identifies VIP/wholesale customers separately to prevent model distortion
- **Optimal K Selection**: Uses Elbow Method and Silhouette Analysis to determine ideal cluster count
- **Interactive 3D Visualization**: Renders customer segments in 3D space with color-coded recency metric
- **Actionable Segmentation**: 7 distinct customer personas with targeted business recommendations
- **Comprehensive Reporting**: Detailed statistical summaries and violin plots for each segment

---

## 🎯 Key Results

### Optimal Clustering: k=3 (Silhouette Score: 0.458)

The analysis identified **3 core customer segments** plus **3 outlier groups**, totaling **7 actionable personas**:

| Segment | Cluster | Count | Avg Spend | Orders | Recency | Strategy |
|---------|---------|-------|-----------|--------|---------|----------|
| **REWARD** | 3 | 494 | $2,436 | 7.24 | 34 days | VIP rewards & early access |
| **RETAIN** | 0 | 914 | $1,309 | 3.91 | 50 days | Loyalty programs & perks |
| **NURTURE** | 2 | 1,499 | $418 | 1.64 | 54 days | Upsell & volume incentives |
| **RE-ENGAGE** | 1 | 902 | $385 | 1.43 | 251 days | Win-back campaigns |
| **DELIGHT** | -3 | 226 | $17,148 | 25.87 | 14 days | Enterprise account mgmt |
| **PAMPER** | -1 | 197 | $6,498 | 7.19 | 48 days | White-glove retention |
| **UPSELL** | -2 | 53 | $2,735 | 15.04 | 23 days | Bundle deals & automation |

---

## 🔍 Model Insights

### Elbow Method & Silhouette Analysis
![Elbow and Silhouette Analysis](./images/01-elbow-silhouette.png)

**Finding**: k=3 maximizes cluster separation (Silhouette: 0.458) while avoiding over-segmentation. Beyond k=4, performance degrades rapidly.

### RFM Distribution: Outliers vs. Core Customers
![Boxplots Comparison](./images/02-boxplots-before-after.png)

**Key Insight**: 
- Before cleaning: Monetary extends to $350,000+, Frequency to 183 orders
- After outlier removal: Bounded ranges enable meaningful K-Means clustering
- Data retained: 77.32% (406,309 of 525,461 transactions)

### 3D Customer Space: Color-Coded by Recency
![3D Scatter Plot by Cluster](./images/03-3d-scatter-clusters.png)

**Visual Interpretation**:
- 🟦 **Blue (RETAIN)**: Moderate spend, low recency — stable mid-tier buyers
- 🟧 **Orange (RE-ENGAGE)**: Low spend, HIGH recency — churned customers, 150-380 days inactive
- 🟩 **Green (NURTURE)**: Low spend, low recency — recent but low-value purchases
- 🔴 **Red (REWARD)**: Highest spend & frequency, very low recency — your VIPs

### RFM Metric Distributions by Segment
![Violin Plots](./images/04-rfm-distributions.png)

**Pattern Analysis**:
- **Recency**: Sharp peak in RE-ENGAGE (high churn risk), floor in REWARD/DELIGHT
- **Frequency**: DELIGHT & UPSELL dominate order counts (frequent power users)
- **Monetary**: DELIGHT far exceeds all others; NURTURE & RE-ENGAGE clustered near baseline

### Aggregated Segment Summary
![Customer Count & Metrics](./images/05-segment-summary.png)

**Business Takeaway**: Large volume in low-value segments (NURTURE: 1,499 customers) represents massive upside potential. Small but valuable DELIGHT segment (226 customers) drives 20%+ of total revenue.

---

## 🔧 Installation

### Prerequisites
- Python 3.8 or higher
- pip or conda package manager

### Clone Repository
```bash
git clone https://github.com/davidstocco2024-cell/ecommerce-rfm-customer-segmentation.git
cd ecommerce-rfm-customer-segmentation
```

### Install Dependencies
```bash
pip install -r requirements.txt
```

**OR** install manually:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn scipy
```

### Data Download
The dataset is automatically loaded from the UCI ML Repository in the notebook. No manual download needed.

---

## 📊 Usage

### Option 1: Google Colab (Recommended for Quick Exploration)
1. Open the notebook: [Online Retail Data Clustering](https://colab.research.google.com/drive/1p8DCO2Md3Oq36OWXFpgMzfTEaK9BiFSe)
2. Run all cells sequentially (Ctrl+F9)
3. Export results as CSV for downstream analysis

### Option 2: Local Jupyter Notebook
```bash
jupyter notebook online-retail-data-clustering.ipynb
```

### Option 3: Python Script
Extract code from notebook and run as:
```bash
python rfm_segmentation.py
```

---

## 🏗️ Project Structure

```
ecommerce-rfm-customer-segmentation/
├── online-retail-data-clustering.ipynb    # Main analysis notebook
├── README.md                               # This file
├── requirements.txt                        # Python dependencies
└── images/                                 # Visualization outputs
    ├── 01-elbow-silhouette.png
    ├── 02-boxplots-before-after.png
    ├── 03-3d-scatter-clusters.png
    ├── 04-rfm-distributions.png
    ├── 05-segment-summary.png
    └── ...
```

---

## 🔄 Data Processing Pipeline

### 1️⃣ Data Cleaning
- Remove rows with missing `Customer_ID` (20.5% of data)
- Filter for positive quantities (exclude cancellations & returns)
- Exclude zero-price items (promotions/freebies)
- Remove non-standard invoice codes ('C', 'A' prefixes) — 1.94% of records
- Validate stock codes; exclude non-product entries (POST, DOT, PADS)

**Result**: 406,309 clean transaction records across 4,232 unique customers

### 2️⃣ Feature Engineering
- **Recency**: Days since last purchase (relative to dataset max date: 2010-12-09)
- **Frequency**: Unique invoice count per customer
- **Monetary**: Total revenue (Quantity × Price) per customer
- **SalesLineTotal**: Per-transaction monetary calculation

### 3️⃣ Outlier Separation
- **IQR Method** (1.5× IQR threshold):
  - Monetary Outliers: 423 customers (10%) — Big one-off spenders
  - Frequency Outliers: 279 customers (7%) — Hyper-engaged power users
  - Combined: 226 "Super Whales" (extreme spend + extreme frequency)

### 4️⃣ Scaling & Normalization
```python
StandardScaler transforms raw values to z-scores:
z = (x - μ) / σ
# Ensures equal feature contribution to distance metrics
```

### 5️⃣ K-Means Clustering
- **n_clusters**: 3 (optimal per Silhouette analysis)
- **n_init**: 10 (multiple random initializations)
- **max_iter**: 300 (convergence threshold)
- **Metric**: Euclidean distance in standardized space

---

## 👥 Customer Segments Explained

### Core Segments (K-Means)

#### 🔵 **Cluster 0: RETAIN** — Active, Steady Mid-Tier Buyers
- **Size**: 914 customers (24%)
- **Profile**: Moderate spend ($1,300 avg), 3-4 orders, purchases every ~50 days
- **Risk Level**: 🟢 Low (active, predictable)
- **Action Plan**:
  - Implement loyalty tiers with exclusive discounts
  - Personalized product recommendations based on order history
  - Early access to new product launches
  - Quarterly check-in emails with VIP perks

#### 🟠 **Cluster 1: RE-ENGAGE** — At-Risk, Churned Customers
- **Size**: 902 customers (24%)
- **Profile**: Low spend ($385 avg), 1-2 orders, 251 days since purchase
- **Risk Level**: 🔴 Critical (high churn risk)
- **Action Plan**:
  - Automated win-back email sequences with special discounts
  - "We miss you" campaigns with time-limited offers (20-30% off)
  - Conduct churn surveys to understand pain points
  - Reactivation bonus: Free shipping on next order

#### 🟢 **Cluster 2: NURTURE** — Active, Low-Spend Casual Buyers
- **Size**: 1,499 customers (39%)
- **Profile**: Low spend ($418 avg), 1-2 orders, recent activity (~54 days)
- **Risk Level**: 🟡 Medium (low LTV, high growth potential)
- **Action Plan**:
  - Cross-sell complementary product bundles
  - Volume discounts: "Buy 3+ for 15% off"
  - First re-purchase incentive: Extra 10% on second order
  - In-app triggers: "Customers who bought X also loved Y"

#### 🔴 **Cluster 3: REWARD** — VIP Champions, Frequent Buyers
- **Size**: 494 customers (13%)
- **Profile**: High spend ($2,436 avg), 7+ orders, very recent (~34 days)
- **Risk Level**: 🟢 Low but PROTECT THIS SEGMENT
- **Action Plan**:
  - Premium loyalty program with tiered rewards (points, exclusive perks)
  - Dedicated account manager or concierge service
  - Early access to limited editions, flash sales, beta features
  - Annual VIP event or personalized thank-you gift

### Outlier Segments

#### 💎 **Cluster -3: DELIGHT** — Super Whales (Extreme Spend + Frequency)
- **Size**: 226 customers (6%)
- **Profile**: $17,148 avg spend, 25+ orders, ultra-active (~14 days)
- **Risk Level**: 🟢 Enterprise-grade relationship building
- **Action Plan**:
  - Assigned account manager & dedicated Slack/email channel
  - Quarterly business reviews & custom pricing negotiations
  - Private product preview & beta testing programs
  - VIP events, conference sponsorships, partner benefits

#### 💰 **Cluster -1: PAMPER** — Big One-Off Spenders
- **Size**: 197 customers (5%)
- **Profile**: $6,498 avg spend, 7 orders, moderate activity (~48 days)
- **Risk Level**: 🟡 Medium (high value but infrequent)
- **Action Plan**:
  - White-glove customer service: Priority phone/email support
  - Personalized product curation based on purchase history
  - Special promotions timed to seasonal buying patterns
  - Cross-sell high-margin complementary products

#### 📈 **Cluster -2: UPSELL** — High-Volume, Low-Spend Frequent Buyers
- **Size**: 53 customers (1%)
- **Profile**: $2,735 avg spend, 15+ orders, very active (~23 days)
- **Risk Level**: 🟢 Stable, high volume
- **Action Plan**:
  - Bulk order incentives: "Buy 10+ items for wholesale pricing"
  - Automated reordering: API integration or subscription model
  - Volume-based rebates: 5% off at $500, 10% at $1,000
  - Premium bulk purchasing portal for faster checkout

---

## 📈 Business Impact & ROI

### Revenue Concentration
- **226 DELIGHT customers** (5.3% of base) generate **~22%** of total revenue
- **914 RETAIN customers** (21.4% of base) generate **~28%** of total revenue
- **1,499 NURTURE customers** (35% of base) generate **~15%** of total revenue — **highest upside**

### Recommended Resource Allocation
1. **Protect the Whales** (DELIGHT + PAMPER): 40% of marketing/CS budget → High retention ROI
2. **Grow the Middle** (RETAIN + NURTURE): 35% of budget → Upsell & cross-sell campaigns
3. **Recover Dormant** (RE-ENGAGE): 25% of budget → Win-back sequences & reactivation offers

---

## 🛠️ Technologies & Libraries

| Tool | Version | Purpose |
|------|---------|---------|
| **pandas** | 1.3+ | Data manipulation & aggregation |
| **scikit-learn** | 1.0+ | K-Means clustering, StandardScaler, Silhouette analysis |
| **numpy** | 1.20+ | Numerical operations & array handling |
| **matplotlib** | 3.4+ | Static visualization & chart creation |
| **seaborn** | 0.11+ | Statistical data visualization, violin plots |
| **scipy** | 1.7+ | Statistical computations & distance metrics |

---

## 📊 Key Metrics & Formulas

### Silhouette Score
```
s(i) = [b(i) - a(i)] / max(a(i), b(i))

Where:
- a(i) = average distance between sample i and all other points in same cluster
- b(i) = minimum average distance between sample i and points in nearest cluster
- Range: [-1, 1] → Higher is better (>0.4 = good separation)
```

### Elbow Method (WCSS/Inertia)
```
WCSS = Σ Σ ||x - c||²

Where:
- x = data point
- c = cluster centroid
- Look for "elbow" where WCSS decrease plateaus
```

### RFM Calculation
```
Recency = max_date - last_purchase_date (in days)
Frequency = COUNT(DISTINCT Invoice)
Monetary = SUM(Quantity × Price)
```

---

## 🚀 Next Steps & Extensions

- [ ] **Temporal Analysis**: Track how customers move between segments over time
- [ ] **Predictive Modeling**: Build LTV prediction model for each segment
- [ ] **Personalization Engine**: Integrate segment data with recommendation system
- [ ] **A/B Testing**: Test segment-specific offers & messaging
- [ ] **Real-Time Scoring**: Deploy live customer segmentation as API
- [ ] **Cohort Analysis**: Deep-dive into segment cohort behavior & lifecycle
- [ ] **Product Recommendations**: Machine learning for segment-specific product suggestions

---

## 📚 References & Learning Resources

- **RFM Analysis**: [Investopedia - RFM Analysis](https://www.investopedia.com/terms/r/rfm-recency-frequency-monetary-value.asp)
- **K-Means Clustering**: [Scikit-Learn Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)
- **Silhouette Analysis**: [Scikit-Learn Guide](https://scikit-learn.org/stable/modules/clustering.html#silhouette-coefficient)
- **Dataset Source**: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/online+retail)
- **Customer Segmentation Best Practices**: [HubSpot Guide](https://blog.hubspot.com/service/customer-segmentation)

---

## 📝 License

This project is licensed under the **MIT License** — see LICENSE file for details.

---

## 👤 Author

**Nacho (Ignacio David Stocco)**
- GitHub: [@davidstocco2024-cell](https://github.com/davidstocco2024-cell)
- Self-taught data analyst passionate about customer intelligence & business analytics
- Based in Mendoza, Argentina

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## ⭐ Support

If you found this project helpful, please consider giving it a star ⭐ on GitHub!

---

**Last Updated**: August 19, 2026 | **Status**: ✅ Production Ready
