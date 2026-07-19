# 🛍️ Customer Shopping Behavior Analysis

## 📌 Project Overview

This project analyzes customer shopping behavior using SQL and Python to identify purchasing patterns, customer preferences, product performance, and category-level insights.

The analysis focuses on transforming raw customer shopping data into meaningful business insights using data cleaning, exploratory data analysis, and advanced SQL techniques.

---

## 🎯 Objectives

- Analyze customer purchasing behavior
- Identify the most popular products in each category
- Find the top 3 most ordered items by category
- Understand customer preferences and shopping patterns
- Analyze customer demographics and purchase behavior
- Use SQL window functions and CTEs for advanced analysis
- Generate actionable insights for business decision-making

---

## 🛠️ Tools & Technologies

- **SQL Server** – Data analysis and querying
- **Python** – Data cleaning and exploratory data analysis
- **Pandas** – Data manipulation
- **Jupyter Notebook** – Analysis environment
- **SQL Window Functions** – Ranking and advanced analysis
- **CTEs (Common Table Expressions)** – Query organization

---

## 📊 Dataset

The dataset contains customer shopping behavior information, including:

- Customer ID
- Age
- Gender
- Item Purchased
- Category
- Purchase Amount (USD)
- Location
- Size
- Color
- Season
- Review Rating
- Subscription Status
- Shipping Type
- Discount Applied
- Promo Code Used
- Previous Purchases
- Payment Method
- Frequency of Purchases

---

## 🔍 Key SQL Analysis

### 🥇 Top 3 Most Ordered Items by Category

A Common Table Expression (CTE) and `ROW_NUMBER()` window function were used to rank products within each category.

```sql
WITH item_count AS (
    SELECT 
        category,
        item_purchased,
        COUNT(customer_id) AS total_orders,
        ROW_NUMBER() OVER (
            PARTITION BY category 
            ORDER BY COUNT(customer_id) DESC
        ) AS item_rank
    FROM customer_shopping_behavior
    GROUP BY category, item_purchased
)
SELECT 
    item_rank,
    category,
    item_purchased,
    total_orders
FROM item_count
WHERE item_rank <= 3;
