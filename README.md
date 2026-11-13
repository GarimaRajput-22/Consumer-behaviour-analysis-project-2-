# 🛍️ Customer Behavior Dashboard

An end-to-end analytics project that explores customer purchasing behavior, using **Python** for data cleaning and preparation, **SQL** for analysis, and **Power BI** for interactive visualization.

## 📖 Project Overview

This project analyzes customer shopping data to understand **who is buying, what they are buying, and how much they are spending**. The goal is to turn raw transaction data into clear, actionable insights that can help a retail business improve marketing, product strategy, and customer retention.

The dashboard summarizes customer demographics, subscription behavior, category performance, and age-group trends in one interactive view.

---

## ❓ Business Questions

- How many customers do we have, and how much does the average customer spend?
- What share of customers are subscribed vs. not subscribed?
- Which product categories generate the most revenue and sales?
- Which age groups contribute the most to revenue and sales?
- How do gender, category, and shipping type affect purchasing behavior?
- How satisfied are customers (average review rating)?

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Python** (Pandas, NumPy) | Data cleaning, preprocessing, feature engineering (e.g., age groups) |
| **SQL** | Data storage, querying, and aggregation for business analysis |
| **Power BI** | Interactive dashboard and data visualization |
| **GitHub** | Version control and project documentation |

---

## 📂 Dataset

- **Source:** *( Kaggle )*
- **Records:** *(100000+)*
- **Key fields:** Customer ID, Age, Gender, Item Purchased, Category, Purchase Amount (USD), Review Rating, Subscription Status, Shipping Type etc.

---

## 🔄 Project Workflow

### 1. Data Cleaning & Preparation (Python)
- Loaded the dataset with Pandas and inspected structure, data types, and summary statistics
- Handled missing values (e.g., imputed missing review ratings)
- Standardized column names and formats
- Created a new **Age Group** column (Young Adult, Adult, Middle-aged, Senior)
- Exported the cleaned data / loaded it into a SQL database

```python
# Example: creating age groups
df['age_group'] = pd.qcut(df['age'], q=4, labels=['Young Adult', 'Adult', 'Middle-aged', 'Senior'])
```

> 📓 See [`notebooks/data_cleaning.ipynb`](notebooks/data_cleaning.ipynb) for the full process.

### 2. Data Analysis (SQL)
Ran queries to answer key business questions, for example:

```sql
-- Revenue by category
SELECT category,
       SUM(purchase_amount) AS total_revenue,
       COUNT(*)             AS total_sales
FROM customer
GROUP BY category
ORDER BY total_revenue DESC;

-- Subscription split
SELECT subscription_status,
       COUNT(customer_id) AS customers,
       ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 1) AS pct
FROM customer
GROUP BY subscription_status;
```

> 🗄️ See [`sql/analysis_queries.sql`](sql/analysis_queries.sql) for all queries.

### 3. Visualization (Power BI)
- Connected Power BI to the cleaned data
- Built KPI cards, charts, and slicers
- Designed a clean, consistent layout with a pink/purple/navy theme

---

## 📊 Dashboard Features

**KPI Cards**
- 👥 Number of Customers
- 💵 Average Purchase Amount
- ⭐ Average Review Rating

**Visuals**
- 🍩 % of Customers by Subscription Status (donut chart)
- 📊 Revenue by Category (column chart)
- 📊 Sales by Category (column chart)
- 📊 Revenue by Age Group (bar chart)
- 📊 Sales by Age Group (bar chart)

**Interactive Filters (Slicers)**
- Subscription Status
- Gender
- Category
- Shipping Type

---

## 💡 Key Insights

> Figures below reflect the dashboard's current view (filtered to **2-Day Shipping**).

- **627 customers** with an **average purchase of $60.73** and an **average review rating of 3.77**.
- **Only 24.4% of customers are subscribed**, while **75.6% are not**, which shows a large opportunity to grow subscriptions.
- **Clothing** is the top category for both revenue and sales, followed by **Accessories**. Together they drive the majority of the business.
- **Footwear** and **Outerwear** contribute significantly less in both revenue and sales.
- **Young Adults** lead in both revenue and sales, followed by **Seniors**.
- **Adult** and **Middle-aged** groups contribute the least and are fairly close to each other.

---

## ✅ Recommendations

1. **Grow subscriptions:** Target the 75.6% non-subscribers with promotions, free shipping, or loyalty perks.
2. **Double down on Clothing and Accessories:** Keep inventory, marketing, and bundles focused on these top performers.
3. **Revive underperforming categories:** Test seasonal campaigns or cross-selling for Footwear and Outerwear.
4. **Engage mid-range age groups:** Create targeted campaigns for Adult and Middle-aged customers to close the gap with Young Adults and Seniors.
5. **Improve satisfaction:** A 3.77 average rating leaves room for improvement. Investigate low-rated products and shipping experiences.

---

## 📁 Repository Structure

```
├── data/
│   ├── raw_data.csv
│   └── cleaned_data.csv
├── notebooks/
│   └── data_cleaning.ipynb
├── sql/
│   └── analysis_queries.sql
├── powerbi/
│   └── Customer_Behavior_Dashboard.pbix
├── images/
│   └── dashboard.png
└── README.md
```

---

## 🚀 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```
2. **Install Python dependencies**
   ```bash
   pip install pandas numpy jupyter
   ```
3. **Run the notebook** in `notebooks/` to clean the data.
4. **Load the cleaned data** into your SQL database and run the queries in `sql/`.
5. **Open the dashboard:** open `powerbi/Customer_Behavior_Dashboard.pbix` and refresh the data source if prompted.



