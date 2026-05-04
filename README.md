# 🛒 E-Commerce Data Preprocessing — Python Data Cleaning Pipeline

> A structured, end-to-end data preprocessing pipeline built in Python that transforms a raw, messy e-commerce dataset into a clean, analysis-ready format — ready for machine learning and business insight generation.

## 📌 Short Description & Purpose

This project transforms raw e-commerce transactional data containing 2,010 records into a clean, feature-rich dataset through a 10-step preprocessing pipeline built entirely in Python. It was designed to train students in handling real-world data quality challenges — including missing values, outliers, skewed distributions, and inconsistent categorical formatting. The goal is to produce a machine-learning-ready dataset that enables an e-commerce business to analyze customer behavior, optimize pricing, predict product returns, and improve delivery efficiency.

## 🛠️ Tech Stack

| Tool / Library | Purpose |
|---|---|
| **Python 3.x** | Core programming language |
| **Pandas** | Data loading, exploration, transformation, and export |
| **NumPy** | Numerical operations, outlier capping (IQR), log/sqrt transformations |
| **Matplotlib** | Distribution histograms and boxplot visualizations |
| **Seaborn** | Statistical visualizations (histplots, boxplots, countplots) |
| **Scikit-learn** | `LabelEncoder` for categorical variable encoding |
| **Jupyter Notebook** | Interactive step-by-step execution environment |
| **Microsoft Excel (.xlsx)** | Output format for the cleaned dataset |


## 📂 Data Source

- **Dataset Name:** E-Commerce Transactions Dataset
- **Format:** CSV (raw input) → Excel `.xlsx` (cleaned output)
- **Records:** 2,010 rows (raw) → 2,000 rows (after duplicate removal)
- **Features:** 14 original columns → 25 columns after feature engineering

**Original Columns:**

| Column | Type | Description | Known Issues |
|---|---|---|---|
| OrderID | Integer | Unique order identifier | None |
| ProductPrice | Float | Product price in USD | Missing values, Outliers |
| Quantity | Integer | Units purchased | Missing values, Outliers |
| CustomerAge | Integer | Customer age in years | Missing values, Outliers |
| ProductReviews | Integer | Number of product reviews | Missing values |
| ProductRating | Float | Customer rating (1–5) | None |
| DiscountPercentage | Float | Discount offered (0–50%) | None |
| CustomerTenure | Float | Months as a customer | Skewed distribution |
| ProductCategory | Categorical | Clothing, Sports, Home, Electronics, Books | Inconsistent casing |
| DeliveryType | Categorical | Standard, Express, Overnight | Extra whitespace |
| PaymentMethod | Categorical | PayPal, Debit Card, UPI, Credit Card | None |
| CustomerLocation | Categorical | Central, North, South, East, West | None |
| ReturnStatus | Categorical | Whether product was returned (Yes/No) | None |
| BrowsingTime | Float | Time spent on website (seconds) | Outliers, Skewed |

**Data Quality Issues Resolved:**
- 200 missing values across 4 columns (~5% of data) — imputed using median per column
- 145 outliers capped using IQR method (ProductPrice: 56, Quantity: 40, CustomerAge: 37, ProductReviews: 12)
- 10 duplicate records removed
- 15 inconsistent categorical values standardized (mixed case, extra spaces, spelling variants)
- 3 skewed columns normalized — `CustomerTenure` (log transform), `BrowsingTime` (sqrt transform)

## ✨ Features & Highlights

The pipeline follows a **10-step structured workflow:**

**Step 1 — Import & Explore Data**
Load dataset using Pandas, inspect shape (2010 × 14), check dtypes, and visualize distributions of all numeric columns using Seaborn histplots with KDE curves.

**Step 2 — Remove Duplicates**
Identify and drop 10 exact duplicate rows → cleaned shape: (2000, 14).

**Step 3 — Handle Missing Values**
Detect 395 missing values across ProductPrice (97), Quantity (99), CustomerAge (99), and ProductReviews (100). Impute all using column median.

**Step 4 — Detect & Treat Outliers**
Apply IQR-based outlier capping function across 4 numeric columns. Visualize before/after boxplots to confirm treatment.

**Step 5 — Standardize Categorical Data**
Strip whitespace, apply Title Case normalization, and fix spelling errors across ProductCategory, DeliveryType, and PaymentMethod. Final unique values verified.

**Step 6 — Apply Transformations**
Apply log1p transformation to `CustomerTenure` (skew: 1.78 → -0.45) and sqrt transformation to `BrowsingTime` (skew: 1.68 → 0.52).

**Step 7 — Binning**
Create 3 new segmentation columns using `pd.cut()`:
- `AgeGroup` — Teen (222), Young Adult (695), Adult (760), Senior (309)
- `PriceSegment` — Very Low / Low / Medium / High / Very High
- `TenureCategory` — New (115), Regular (302), Loyal (1,583)

**Step 8 — Encode Categorical Variables**
One-hot encode 4 nominal columns (DeliveryType, PaymentMethod, CustomerLocation, ReturnStatus). DataFrame expands from 17 → 27 columns.

**Step 9 — Feature Engineering**
Create 7 new analytical features:
- `price_rating_interaction` = ProductPrice × ProductRating
- `quantity_reviews_interaction` = Quantity × ProductReviews
- `discounted_price` = ProductPrice × (1 - DiscountPercentage)
- `price_per_review` = ProductPrice / (ProductReviews + 1)
- `TotalSpend` = ProductPrice × Quantity
- `high_value_order` — binary flag (TotalSpend > $700)
- `frequent_buyer` — binary flag (CustomerTenure > 36 months)

**Step 10 — Save & Validate**
Export cleaned dataset to Excel. Generate full numeric and categorical summary reports. Final shape: (2000, 25) with zero missing values.


## ❓ Key Business Questions This Enables

1. Which product categories have the highest average spend per order?
2. How does discount percentage affect total order value and return rates?
3. Are loyal customers (high tenure) spending more than new customers?
4. Which delivery type is most associated with product returns?
5. What is the price sensitivity across different customer age groups?
6. How does browsing time correlate with purchase quantity and product rating?


## 📸 Notebook Screenshot

![Ecommerce_Dataset_Project](https://github.com/vaibhavichavan/E-commerce-Data-Pre-processing/blob/main/Ecommerce-Pdf.pdf)


