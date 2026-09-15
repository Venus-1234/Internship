# E-Commerce Exploratory Data Analysis & Data Cleaning

An exploratory data analysis (EDA) and data validation project on an e-commerce transaction dataset containing 1,200 order records across 14 attributes. 

This project covers the full initial analytics workflow: data hygiene verification, statistical distribution analysis, outlier diagnosis, and correlation testing using Python.

---

## 📌 Project Objectives
* **Data Validation & Cleaning:** Verify data types, identify missing values, test for pipeline duplications, and validate transaction calculation integrity.
* **Descriptive Statistics:** Analyze central tendency and dispersion metrics (`mean`, `median`, `IQR`, standard deviation, and skewness).
* **Outlier Diagnosis:** Detect statistical anomalies using the 1.5× Interquartile Range (IQR) method and determine whether they represent errors or valid business activity.
* **Bivariate & Correlation Analysis:** Test relationships between cart sizes, order quantities, unit prices, and overall order revenues.

---

## 🛠️ Tech Stack & Tools
* **Language:** Python
* **Environment:** Jupyter Notebook
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn

---

## 🔍 Key Findings & Workflow

### 1. Data Cleaning & Integrity Checks
* **Missing Value Imputation:** Addressed 309 missing values in `CouponCode` via mode imputation without altering transaction financials.
* **Row Uniqueness:** Confirmed 1,189 unique customer IDs across 1,200 orders, verifying legitimate repeat purchasing behavior rather than pipeline duplicate records.
* **Mathematical Integrity:** Verified that `TotalPrice == Quantity * UnitPrice` across all 1,200 records with zero calculation discrepancies.

### 2. Distribution & Descriptive Statistics
* **Right-Skewed Revenue Distribution:** Order values (`TotalPrice`) exhibit a positive skew (+0.89).
  * **Mean:** $1,053.97
  * **Median:** $823.62
  * The median sits significantly lower than the mean, showing that over 57% of orders are under $1,000, while a long tail of larger orders pulls up the average.

### 3. Outlier Evaluation (1.5× IQR Rule)
* **Threshold:** Q1 ($410.52) and Q3 ($1,578.48) establish an IQR of $1,167.96, placing the upper statistical boundary at **$3,330.41**.
* **Finding:** 8 orders exceeded this threshold.
* **Analytical Decision:** Rather than dropping these rows as dirty data, investigation revealed that all 8 transactions involved customers purchasing maximum units (`Quantity = 5`) of high-cost items (`UnitPrice > $666`). They represent valid high-margin bulk sales and were preserved in the primary dataset.

### 4. Correlation & Feature Relationships
* **Deterministic Scaling:** `UnitPrice` ($r \approx 0.72$) and `Quantity` ($r \approx 0.62$) show moderate-to-strong positive correlations with `TotalPrice`, as expected from the revenue formula.
* **Cart Independence:** `ItemsInCart` shows virtually zero statistical correlation ($r \approx -0.01$ to $-0.03$) with `Quantity` or `UnitPrice`. A fuller cart does not predict higher checkout values in this sample.

  # Combined data cleaning & EDA notebook
└── README.md                          # Project overview and insights
