# 🛒 Olist E-Commerce Case Study — Product & Business Analytics

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?logo=kaggle&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-F9AB00?logo=googlecolab&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

> A product-oriented analysis of the Brazilian Olist e-commerce platform using the public Kaggle dataset. This case study is designed with a **Product Manager's lens** — uncovering actionable insights around supply dynamics, customer segmentation, category performance, seasonality, and growth opportunities.

---

## 📌 Table of Contents

- [About the Project](#about-the-project)
- [Dataset Overview](#dataset-overview)
- [Analysis Structure](#analysis-structure)
- [Key Analyses & Findings](#key-analyses--findings)
  - [1. Supply Details & Category Performance](#1-supply-details--category-performance)
  - [2. Deep Dive: watches\_gifts Category](#2-deep-dive-watches_gifts-category)
  - [3. Deep Dive: party\_supplies Seasonality](#3-deep-dive-party_supplies-seasonality)
  - [4. RFM Customer Segmentation](#4-rfm-customer-segmentation)
  - [5. Customer Segmentation by Product Category](#5-customer-segmentation-by-product-category)
  - [6. Cross-Sell Opportunity Analysis](#6-cross-sell-opportunity-analysis)
- [PM Recommendations](#pm-recommendations)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Dataset Source](#dataset-source)

---

## About the Project

This case study analyzes **~100,000 orders** placed on [Olist](https://olist.com/), Brazil's largest multi-vendor e-commerce marketplace, between **2016 and 2018**. The analysis is framed around product and business decisions — treating data as a tool to inform strategy rather than just statistics.

The notebook (`Olist_case_study_for_PM.ipynb`) walks through end-to-end analysis from data loading and business understanding, through supply analytics, deep-dive category analysis, RFM modelling, and customer segmentation — making it suitable for Product Managers, Business Analysts, and Data professionals.

---

## Dataset Overview

The analysis uses **11 CSV files** — the full Olist transactional dataset plus the Marketing Funnel extension:

| File | Rows | Description |
|---|---|---|
| `olist_orders_dataset.csv` | 99,441 | Core order info: status, purchase & delivery timestamps |
| `olist_customers_dataset.csv` | 99,441 | Customer ID and location (zip, city, state) |
| `olist_order_items_dataset.csv` | 112,650 | Items per order: product, seller, price, freight |
| `olist_order_payments_dataset.csv` | 103,886 | Payment type, installments, value |
| `olist_order_reviews_dataset.csv` | 99,224 | Review score, title, comment, timestamps |
| `olist_products_dataset.csv` | 32,951 | Product category, dimensions, description length |
| `olist_sellers_dataset.csv` | 3,095 | Seller location data |
| `olist_geolocation_dataset.csv` | 1,000,163 | Zip code to lat/lng mapping |
| `product_category_name_translation.csv` | 71 | Portuguese → English category names |
| `olist_marketing_qualified_leads_dataset.csv` | 8,000 | MQLs from landing page form submissions |
| `olist_closed_deals_dataset.csv` | 842 | Confirmed sellers: segment, lead type, profile |

**Order Flow:**
```
Purchase → Payment Approval → Carrier Handover → Customer Delivery → Review Request
```

**Data Schema:**
```
customers ──── orders ──── order_items ──── products ──── sellers
                  │              │
              payments       geolocation
                  │
              reviews
                  │
        MQL leads ──── closed_deals
```

---

## Analysis Structure

```
1. Environment Setup & Data Loading
2. Dataset Understanding (Business Context + Data Flow)
3. Supply Details Table Construction
   └── seller count, ASP, price range, revenue, revenue/seller, orders, MoM growth, avg monthly metrics
4. Critical Business Indicators (Category Performance Matrix)
5. Deep Dive: watches_gifts (Top Revenue Category)
   ├── Order value distribution
   ├── Top products & top sellers by revenue
   ├── Seasonality (monthly orders vs revenue)
   ├── Payment method breakdown
   └── Delivery time vs review score analysis
6. Deep Dive: party_supplies (High-Growth, Low-Supply Category)
   └── Monthly seasonality trends
7. RFM Customer Segmentation
   ├── Recency, Frequency, Monetary scoring (1–5)
   ├── Segment classification (6 segments)
   └── Recency vs Monetary scatter plot
8. Customer Segmentation by Product Category
   ├── Customer–category spend matrix (94,088 × 71)
   ├── Threshold-based major buyer identification
   ├── Primary category assignment per customer
   └── Cross-sell opportunity analysis (bed_bath_table)
```

---

## Key Analyses & Findings

### 1. Supply Details & Category Performance

A `supply_details` table was constructed per product category (72 categories) containing:

| Metric | Description |
|---|---|
| `seller_count` | Number of unique sellers in the category |
| `average_sales_price` | Mean item price |
| `highest_price` / `lowest_price` | Price range |
| `total_revenue` | Total revenue generated |
| `total_revenue_per_seller` | Revenue efficiency per seller |
| `total_orders` | Unique orders placed |
| `2017_growth%` / `2018_growth%` | Avg month-on-month revenue growth by year |
| `month_average_orders` | Avg monthly order volume |
| `month_average_revenue` | Avg monthly revenue |

**Top Revenue Categories:** `health_beauty`, `watches_gifts`, `bed_bath_table`, `sports_leisure`, `computers_accessories`

**Key Findings:**
- **Cash Cows:** `watches_gifts`, `health_beauty`, and `bed_bath_table` lead in total revenue. `watches_gifts` has the highest Revenue per Seller, indicating a highly profitable, concentrated segment.
- **2017 Surge vs 2018 Consolidation:** Many categories showed triple-digit MoM growth in 2017. By 2018, growth rates normalized, indicating a maturing market.
- **Surging Categories (High Growth, Low Supply):** `party_supplies`, `drinks`, `fashion_female_clothing`, `signaling_and_security`, `arts_and_craftmanship` — prime targets for seller acquisition.
- **Dipping Categories:** `security_and_services` and `consoles_games` show negative or stagnant growth — candidates for a "Fix or Exit" review.

---

### 2. Deep Dive: `watches_gifts` Category

**Why investigated:** Highest Revenue per Seller across all categories.

| Metric | Value |
|---|---|
| Total orders | 5,991 |
| Mean order value | R$ 201.14 |
| Median order value | R$ 129.00 |
| Max order value | R$ 3,999.90 |
| Unique sellers | 101 |
| Average review score | 4.02 / 5 |
| Average delivery time | 12.19 days |
| Days delivered ahead of estimate | 10.92 days |

**Payment breakdown (by value):**
- Credit Card: **86.1%** (R$ 1,169,481)
- Boleto: 10.8%
- Voucher: 2.0%
- Debit Card: 1.1%

**Seasonality:** Strong growth in 2017–2018 with a massive revenue and order peak in **November 2017 (Black Friday)**.

**Top seller concentration:** The top 3 sellers alone account for a disproportionate share of category revenue (seller revenues of R$ 201K, R$ 192K, R$ 169K respectively out of 101 total sellers).

---

### 3. Deep Dive: `party_supplies` Seasonality

Investigated as a high MoM growth category with low seller supply. Monthly order and revenue data confirmed demand spikes, providing evidence for targeted seller acquisition ahead of seasonal peaks.

---

### 4. RFM Customer Segmentation

Customers were scored on **Recency**, **Frequency**, and **Monetary** value (each scored 1–5) and classified into 6 segments:

| Segment | Count | % of Base | Description |
|---|---|---|---|
| At Risk / Hibernating | 38,429 | ~40% | Haven't purchased in a long time |
| Potential Loyalists | 19,238 | ~20% | Moderate recency & frequency |
| Others | 15,255 | ~16% | Mixed profile |
| Loyal Customers | 14,396 | ~15% | High recency + high frequency |
| New Customers | 7,720 | ~8% | Recently acquired, low frequency |
| Champions | 1,057 | ~1% | Best RFM score (555) |

**Key Findings:**
- The **At Risk / Hibernating** segment is the largest — over 38,000 customers need re-engagement campaigns.
- **Champions + Loyal Customers** (~15,453 combined) are the highest-value group and should receive retention-priority treatment.
- **New Customers** (7,720) are prime targets for onboarding and welcome sequences to build loyalty before they lapse.

---

### 5. Customer Segmentation by Product Category

A **94,088 × 71 customer–category spend matrix** was built to profile each customer's purchasing behaviour across all product categories.

**Threshold-based Major Buyer identification** (75th percentile of active spenders per category):

| Category | Major Buyers (≥75th pct) | Spend Threshold | Non-Buyers |
|---|---|---|---|
| `health_beauty` | 2,170 | R$ 151.39 | 85,410 |
| `watches_gifts` | 1,393 | R$ 223.00 | 88,541 |
| `bed_bath_table` | 2,295 | R$ 139.80 | 84,943 |
| `sports_leisure` | 1,887 | R$ 149.00 | 86,573 |
| `computers_accessories` | 1,831 | R$ 149.90 | 87,531 |

**Primary Category Distribution** (category of highest spend per customer — Top 10):

| Rank | Category | Customers |
|---|---|---|
| 1 | bed_bath_table | 8,922 |
| 2 | health_beauty | 8,530 |
| 3 | sports_leisure | 7,384 |
| 4 | computers_accessories | 6,459 |
| 5 | furniture_decor | 6,022 |
| 6 | housewares | 5,623 |
| 7 | watches_gifts | 5,472 |
| 8 | telephony | 4,051 |
| 9 | auto | 3,785 |
| 10 | toys | 3,779 |

---

### 6. Cross-Sell Opportunity Analysis

For customers whose **primary spend category is `bed_bath_table`**, the top cross-sell categories by average spend are:

| Rank | Category | Avg Spend |
|---|---|---|
| 1 | furniture_decor | R$ 0.85 |
| 2 | home_confort | R$ 0.44 |
| 3 | housewares | R$ 0.32 |
| 4 | health_beauty | R$ 0.11 |
| 5 | baby | R$ 0.10 |

This reveals a natural **home & lifestyle cluster** that can be used to build product recommendation and bundling strategies.

---

## PM Recommendations

| Area | Finding | Recommendation |
|---|---|---|
| **Category Strategy** | `watches_gifts` has the highest revenue/seller with just 101 sellers | Protect top sellers from churn; audit seller concentration risk |
| **Seller Acquisition** | `party_supplies`, `drinks`, `fashion_female_clothing` are high-growth with low supply | Run targeted seller acquisition campaigns for these categories before seasonal peaks |
| **Fix or Exit** | `security_and_services`, `consoles_games` show negative/zero growth | Investigate root cause (price, selection, demand decline) and decide on investment level |
| **Re-engagement** | 38,429 customers (~40%) are At Risk / Hibernating | Launch re-engagement email/push campaign with personalized offers based on past category spend |
| **New Customer Activation** | 7,720 new customers with low frequency | Build a welcome sequence (first 30/60/90 days) with category recommendations to drive second purchase |
| **Loyalty** | Only 1,057 Champions in a 96K+ base | Introduce a tiered loyalty or rewards program to grow this segment |
| **Cross-Sell** | `bed_bath_table` buyers also spend in `furniture_decor` and `housewares` | Implement "Customers also bought" recommendations and home lifestyle bundles |
| **Seasonality** | `watches_gifts` spikes on Black Friday (Nov) | Plan inventory, marketing spend, and seller capacity ahead of November each year |
| **Payments** | 86% of `watches_gifts` revenue is credit card, often high-value | Consider expanding installment options to capture higher AOV orders |
| **Delivery** | `watches_gifts` averages 10.9 days ahead of estimated delivery | Use this as a marketing message to improve perceived service quality for the category |

---

## Tech Stack

- **Python 3.8+** on **Google Colab**
- **Pandas** — data wrangling, merging, aggregation
- **NumPy** — numerical operations
- **Matplotlib & Seaborn** — visualisations (histograms, bar charts, box plots, pie charts, scatter plots)

---

## Project Structure

```
Olist_Ecommerce_Kaggle_casestudy/
│
├── Olist_case_study_for_PM.ipynb   # Main analysis notebook (Google Colab)
├── README.md                        # Project documentation
│
└── data/                            # Dataset CSVs (stored in Google Drive)
    ├── olist_orders_dataset.csv
    ├── olist_customers_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_order_payments_dataset.csv
    ├── olist_order_reviews_dataset.csv
    ├── olist_products_dataset.csv
    ├── olist_sellers_dataset.csv
    ├── olist_geolocation_dataset.csv
    ├── product_category_name_translation.csv
    ├── olist_marketing_qualified_leads_dataset.csv
    └── olist_closed_deals_dataset.csv
```

> **Note:** The dataset files are stored in Google Drive and loaded via the Colab mount path. Download them from Kaggle (see below) and place them in your Drive folder.

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/shashi247/Olist_Ecommerce_Kaggle_casestudy.git
```

### 2. Download the dataset
Download the Olist dataset from Kaggle:
👉 [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

Upload all CSV files to a folder in your **Google Drive** (e.g., `My Drive/Colab Notebooks/Olist Study`).

### 3. Open in Google Colab
Upload `Olist_case_study_for_PM.ipynb` to Colab or open directly from GitHub.

### 4. Update the folder path
In the notebook, update this line to match your Drive folder path:
```python
csv_folder_path = '/content/drive/MyDrive/Colab Notebooks/Olist Study'
```

### 5. Run all cells
Mount your Drive when prompted, then run all cells top to bottom.

---

## Dataset Source

**Brazilian E-Commerce Public Dataset by Olist**
- Kaggle: [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- License: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
- Original data provided by [Olist](https://olist.com/) and published by André Sionek

---

## 👤 Author

**Shashi** — [@shashi247](https://github.com/shashi247)

---

*If you found this useful, consider ⭐ starring the repository!*
