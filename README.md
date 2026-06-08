# 🛒 Olist E-Commerce Case Study — Product & Business Analytics

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?logo=kaggle&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

> A product-oriented analysis of the Brazilian Olist e-commerce platform using the public Kaggle dataset. This case study is designed with a **Product Manager's lens** — uncovering actionable insights around customer experience, seller performance, logistics, and growth opportunities.

---

## 📌 Table of Contents

- [About the Project](#about-the-project)
- [Dataset Overview](#dataset-overview)
- [Key Business Questions Explored](#key-business-questions-explored)
- [Analysis Highlights](#analysis-highlights)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Key Insights & Recommendations](#key-insights--recommendations)
- [Dataset Source](#dataset-source)

---

## About the Project

This case study analyzes **~100,000 orders** placed on [Olist](https://olist.com/), Brazil's largest multi-vendor e-commerce marketplace, between **2016 and 2018**. The analysis is framed around product and business decisions — treating data as a tool to inform strategy rather than just statistics.

The notebook (`Olist_case_study_for_PM.ipynb`) walks through end-to-end analysis from data cleaning to business recommendations, making it suitable for Product Managers, Business Analysts, and Data professionals.

---

## Dataset Overview

The Olist dataset is a relational dataset with **9 CSV files** that can be joined to form a comprehensive view of every order:

| File | Description |
|---|---|
| `olist_orders_dataset.csv` | Core order information and status |
| `olist_customers_dataset.csv` | Customer ID and location data |
| `olist_order_items_dataset.csv` | Items per order with price and freight |
| `olist_order_payments_dataset.csv` | Payment types and installments |
| `olist_order_reviews_dataset.csv` | Customer review scores and comments |
| `olist_products_dataset.csv` | Product attributes and categories |
| `olist_sellers_dataset.csv` | Seller location data |
| `olist_geolocation_dataset.csv` | Zip code to lat/lng mapping |
| `product_category_name_translation.csv` | Category names in English |

**Schema overview:**

```
customers ──── orders ──── order_items ──── products
                  │              │
              payments       sellers
                  │
              reviews
```

---

## Key Business Questions Explored

1. **Customer Experience** — What drives review scores? What causes dissatisfaction?
2. **Delivery Performance** — How does delivery delay correlate with customer ratings?
3. **Seller Health** — Which seller segments perform best? What defines a top seller?
4. **Payment Behaviour** — How do customers prefer to pay? What are installment patterns?
5. **Category Performance** — Which product categories drive revenue vs. volume?
6. **Geographic Insights** — Where are orders concentrated? Are there underserved regions?
7. **Repeat Purchase Rate** — How loyal are Olist customers?

---

## Analysis Highlights

- **Delivery delay is the #1 driver of poor review scores** — orders delivered even 1 day late see a significant drop in ratings
- **São Paulo dominates** order volume (~40%), but states like Minas Gerais and Rio de Janeiro show strong growth potential
- **Credit card installments** are the most popular payment method, with customers opting for 1–3 installments most frequently
- **Top product categories** by revenue include bed/bath/table, health & beauty, and watches/gifts
- **Customer retention is low** (~3% repeat purchase rate), indicating a significant opportunity to invest in loyalty programs

---

## Tech Stack

- **Python 3.8+**
- **Pandas** — data manipulation and merging
- **NumPy** — numerical operations
- **Matplotlib & Seaborn** — data visualisation
- **Plotly** *(if used)* — interactive charts
- **Jupyter Notebook** — analysis environment

---

## Project Structure

```
Olist_Ecommerce_Kaggle_casestudy/
│
├── Olist_case_study_for_PM.ipynb   # Main analysis notebook
├── README.md                        # Project documentation
│
└── data/                            # Dataset CSVs (not tracked in git)
    ├── olist_orders_dataset.csv
    ├── olist_customers_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_order_payments_dataset.csv
    ├── olist_order_reviews_dataset.csv
    ├── olist_products_dataset.csv
    ├── olist_sellers_dataset.csv
    ├── olist_geolocation_dataset.csv
    └── product_category_name_translation.csv
```

> **Note:** The dataset files are not included in this repository. Download them from Kaggle (see below).

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/shashi247/Olist_Ecommerce_Kaggle_casestudy.git
cd Olist_Ecommerce_Kaggle_casestudy
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn plotly jupyter
```

### 3. Download the dataset
Download the Olist dataset from Kaggle:
👉 [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

Place all CSV files in a `data/` folder inside the project directory.

### 4. Launch the notebook
```bash
jupyter notebook Olist_case_study_for_PM.ipynb
```

---

## Key Insights & Recommendations

| Area | Insight | PM Recommendation |
|---|---|---|
| Delivery | Late deliveries strongly reduce review scores | Build a predictive delivery ETA system; alert customers proactively |
| Reviews | ~60% orders receive 5-star ratings; 1-star orders cluster around delays | Introduce a post-delivery follow-up for at-risk orders |
| Sellers | Top 20% sellers account for majority of revenue | Create a seller tiering program with perks and performance SLAs |
| Payments | Installments are widely used | Offer more flexible financing options to increase AOV |
| Categories | Health & beauty and bed/bath show strong demand | Prioritise seller acquisition in these categories |
| Geography | Southern Brazil is underserved relative to population | Regional logistics partnerships and marketing campaigns |
| Retention | Very low repeat purchase rate | Launch a loyalty/rewards program to improve LTV |

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
