# Brazilian E-Commerce Data Mining Analysis

A comprehensive data mining analysis of the Olist Brazilian E-Commerce dataset, covering **112,650 orders** placed between October 2016 and August 2018. This project combines customer segmentation, predictive modeling, and association rule mining to uncover actionable business insights.

---

## Project Overview

Three core business questions guided this analysis:

1. **Who are the customers?** Can customers be segmented by spending behavior, frequency, and payment patterns?
2. **What do customers buy together?** Are there product combinations appearing more often than random chance predicts?
3. **What drives high-value purchases?** Which categories and payment behaviors are associated with higher order values?

---

## Dataset

The Olist dataset is a publicly available collection of anonymized commercial transactions from the Olist marketplace, one of Brazil's largest e-commerce platforms. The data spans October 2016 to August 2018 across nine relational CSV files covering customers, orders, payments, products, sellers, reviews, and geolocation data.

| Metric | Value |
|--------|-------|
| Total Orders | 112,650 |
| Total Revenue | R$16.01 Million |
| Average Order Value | R$154.10 |
| Distinct Product Categories | 73 |
| Brazilian States Covered | 27 |
| Single-Order Customers | 96.72% |

---

## Analytical Methods

| Method | Purpose | Business Question |
|--------|---------|------------------|
| **K-Means Clustering** | Unsupervised customer segmentation | Q1 |
| **Decision Tree Classification** | Scalable real-time segment prediction | Q1 |
| **Apriori Association Rules** | Co-purchase pattern discovery | Q2, Q3 |

---

## Pipeline 1: Customer Segmentation

### K-Means Clustering

Customers were segmented into three distinct behavioral groups using RFM-style features (Recency, Frequency, Monetary, Avg Installments, Avg Freight, Unique Products):

| Segment | Count | % of Base | Avg Spend | Avg Installments | Unique Products |
|---------|-------|-----------|-----------|-----------------|----------------|
| Low-Value Casual | 67,469 | 77.7% | R$134 | 1.80 | 0.98 |
| Installment Buyers | 16,509 | 19.0% | R$384 | 7.25 | 0.99 |
| High-Value Shoppers | 2,851 | 3.3% | R$817 | 4.05 | 2.16 |

**K Selection**: K=3 was selected using Silhouette Score (0.419), producing three business-interpretable segments.

### Decision Tree Classification

A Decision Tree classifier was trained on K-Means labels to enable real-time customer classification:

- **Accuracy**: 99% on a held-out test set of 9,648 customers
- **Precision/Recall**: 0.98-1.00 across all three segments
- **Top Feature**: `uniqueproducts` (50.1% importance) separates High-Value Shoppers
- **Second Feature**: `avginstallments` (38.8% importance) identifies Installment Buyers

---

## Pipeline 2: Association Rule Mining

### Apriori Algorithm

Six statistically significant co-purchase rules were discovered from ~2,880 multi-basket orders:

| Antecedent | Consequent | Support | Confidence | Lift |
|------------|------------|---------|------------|------|
| Health Beauty | Perfumery | 0.041 | 0.52 | **3.8** |
| Sports Leisure | Health Beauty | 0.028 | 0.45 | **3.2** |
| Bed Bath Table | Housewares | 0.035 | 0.41 | 2.9 |
| Computers | Accessories Electronics | 0.022 | 0.38 | 2.7 |
| Furniture Decor | Home Comfort | 0.019 | 0.35 | 2.5 |
| Toys | Baby Products | 0.015 | 0.33 | 2.3 |

---

## Key Findings

- **Customer base is deeply segmented** along behavioral lines not visible in aggregate statistics
- **99% accuracy** on unseen data confirms segment membership is highly predictable from observable features
- **Health Beauty buyers are 3.8x more likely** to also purchase perfumery products
- **96.72% single-order rate** represents the largest untapped re-engagement opportunity

---

## Prescriptive Recommendations

1. **Retain High-Value Shoppers**: Exclusive loyalty tier, personalized cross-sell recommendations, win-back campaigns
2. **Re-Engage Casual Buyers**: Automated 30/60/90-day re-engagement emails, discovery promotions with association rule suggestions
3. **Upgrade Installment Buyers**: Premium bundle offers with extended installment options, cross-category discovery at checkout
4. **Platform-Wide Association Actions**: "Customers also bought" widgets powered by discovered rules, curated lifestyle bundles

---

## Repository Contents

| File | Description |
|------|------------|
| `Customer_Segments.ipynb` | K-Means clustering and Decision Tree classification pipeline |
| `Association_Rule.ipynb` | Apriori association rule mining pipeline |
| `brazilian_e-commerce.pbix` | Power BI descriptive analytics dashboard |
| `customer_segments.csv` | Customer-level behavioral features extracted via SQL |
| `association.csv` | Transaction data for association rule mining |
| `Seasonal_Association.csv` | Seasonal variation in co-purchase patterns |

---

## Technologies Used

- **Python**: pandas, scikit-learn, mlxtend
- **SQL/MySQL Workbench**: Database construction and feature extraction
- **Power BI**: Descriptive analytics dashboard
- **Jupyter Notebooks**: Interactive analysis and modeling

---

## Dataset Source

Olist. (2018). *Brazilian E-Commerce public dataset by Olist*. Kaggle.
https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

---

> This project was completed as part of a Post-Baccalaureate Diploma in Business Analytics at Cape Breton University, Halifax, NS, Canada.
