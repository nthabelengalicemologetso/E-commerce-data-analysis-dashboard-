
# 📊 E-Commerce Sales Analytics Dashboard

An interactive, multi-tab dashboard that analyzes e-commerce performance across **5,000 orders**, covering revenue, product categories, regional sales, payment methods, and customer satisfaction.

**Built with:** Python · Pandas · Plotly · Streamlit

🔗 **[View Live Project](YOUR_LIVE_APP_LINK)**

![Dashboard Preview](images/dashboard-preview.png)

---

## 📌 Table of Contents
1. [Introduction](#-introduction)
2. [Problem Statement](#-problem-statement)
3. [Data Overview](#-data-overview)
4. [Data Cleaning Process](#-data-cleaning-process)
5. [Dashboard Features](#-dashboard-features)
6. [KPIs Explained](#-kpis-explained)
7. [Key Insights](#-key-insights)
8. [Recommendations](#-recommendations)
9. [How to Run Locally](#-how-to-run-locally)
10. [Project Structure](#-project-structure)
11. [Author](#-author)

---

## 🧭 Introduction

E-commerce businesses generate large volumes of transaction data, but raw tables don't tell decision-makers *what is working and what isn't*. This project turns 5,000 order records into an interactive dashboard so that anyone, technical or not, can explore sales performance, spot trends, and understand customer satisfaction in a few clicks.

The dashboard uses tabbed navigation (**Overview, Sales Trends, Product & Region, Customer Insights, Raw Data**) and dynamic filters for **date range, region, category, and payment method**.

---

## ❓ Problem Statement

The business needs clear answers to questions such as:

- How much revenue are we generating, and from which product categories?
- Which regions perform best and which are underperforming?
- Which payment methods do customers prefer?
- How satisfied are customers, and is delivery time affecting their experience?
- How do sales change over time?

Without a central, interactive view, these questions require manual spreadsheet work and are slow to answer. **Goal:** build a self-service analytics dashboard that answers these questions and supports data-driven decisions.

---

## 🗂 Data Overview

| Item | Details |
|---|---|
| **Records** | 5,000 orders |
| **Source** | `[Add source: Kaggle / company export / synthetic]` |
| **Time period** | `[Start date] – [End date]` |
| **Format** | CSV |

**Main columns** *(update to match your dataset)*:

| Column | Description |
|---|---|
| `order_id` | Unique identifier for each order |
| `order_date` | Date the order was placed |
| `region` | Geographic region of the customer |
| `category` | Product category |
| `payment_method` | How the customer paid |
| `revenue` / `total_amount` | Order value |
| `rating` | Customer rating (1–5) |
| `delivery_days` | Days between order and delivery |

---

## 🧹 Data Cleaning Process

> ⚠️ *Adjust this section to match the steps you actually performed in your notebook/script. Below are the standard steps with the reasoning behind each.*

| # | Cleaning Step | Why It Was Done |
|---|---|---|
| 1 | **Inspected the data** (`df.info()`, `df.describe()`, `df.head()`) | To understand structure, data types, and spot obvious problems before changing anything. |
| 2 | **Removed duplicate orders** (`df.drop_duplicates()`) | Duplicate rows double-count revenue and inflate order totals, giving misleading KPIs. |
| 3 | **Handled missing values** (dropped or filled) | Nulls break calculations and charts. Numeric fields (e.g., rating) can be filled with the median; rows missing critical fields (e.g., order ID, revenue) are removed. |
| 4 | **Converted data types** (`pd.to_datetime` for dates, numeric for amounts) | Dates stored as text can't be used for time-series analysis, and text-based numbers can't be summed or averaged. |
| 5 | **Standardized text values** (trim whitespace, consistent casing for region, category, payment method) | `"north"`, `"North "` and `"NORTH"` would otherwise appear as three different groups in charts and filters. |
| 6 | **Validated ranges** (ratings between 1–5, no negative revenue or delivery days) | Impossible values are data-entry errors that would distort averages. |
| 7 | **Checked for outliers** (IQR / boxplots on revenue and delivery days) | Extreme values can skew averages. They were reviewed and kept if genuine, removed if errors. |
| 8 | **Created new features** (`month`, `year`, `day_of_week` from order date) | Enables the Sales Trends tab and time-based filtering. |
| 9 | **Saved the cleaned dataset** (`data/cleaned_data.csv`) | Keeps the dashboard fast and separates cleaning logic from visualization. |

---

## 🖥 Dashboard Features

| Tab | What It Shows |
|---|---|
| **Overview** | Headline KPIs, revenue share by category, revenue by region, revenue by payment method, rating distribution |
| **Sales Trends** | Revenue and order volume over time |
| **Product & Region** | Category and regional performance breakdowns |
| **Customer Insights** | Ratings, delivery times, and satisfaction analysis |
| **Raw Data** | Filterable table of the underlying orders |

**Sidebar filters:** Date range · Region · Category · Payment method. All charts and KPIs update instantly.

---

## 📈 KPIs Explained

| KPI | Value | What It Means | Why It Matters |
|---|---|---|---|
| **Total Revenue** | **$5,109,776** | Sum of all order values | Shows overall business size and is the baseline for measuring growth. |
| **Total Orders** | **5,000** | Number of orders placed | Measures demand and sales volume. |
| **Avg Order Value (AOV)** | **$1,021.96** | Total revenue ÷ total orders | Indicates how much customers spend per purchase. Raising AOV grows revenue without needing more customers. |
| **Avg Rating** | **2.97 ⭐** | Mean customer rating (out of 5) | A direct measure of customer satisfaction and a leading indicator of repeat purchases and reviews. |
| **Avg Delivery Days** | **6.1 days** | Mean time from order to delivery | Delivery speed strongly influences satisfaction and repeat buying. |

---

## 💡 Key Insights

> *Verify each point against your final charts and update the numbers or names where marked.*

1. **High order value:** With an AOV of about $1,022, customers are buying relatively high-ticket items, so each order carries significant revenue weight.
2. **Revenue is concentrated in a few categories:** The category donut chart shows that `[top category]` contributes the largest share (`[X%]`), meaning performance depends heavily on a handful of product lines.
3. **Regional gap:** `[Top region]` generates the most revenue, while `[lowest region]` lags behind, which suggests untapped potential or weaker market presence there.
4. **Payment preferences:** `[Top payment method]` leads in revenue, while `[lowest payment method]` is used far less.
5. **Customer satisfaction is a concern:** The average rating of **2.97/5** is below the "satisfied" level, and the rating distribution is spread across the scale rather than clustered at 4–5. Many customers are having a mediocre or poor experience.
6. **Delivery may be a driver:** An average of 6.1 days is relatively slow for e-commerce standards, and it likely contributes to lower ratings. *(Check this by comparing ratings against delivery days in the Customer Insights tab.)*

---

## ✅ Recommendations

1. **Improve customer satisfaction first.** Investigate low-rated orders (1–2 stars) by category, region, and delivery time to find the root causes, such as product quality, late delivery, or poor packaging. Set a target to raise the average rating above 4.0.
2. **Reduce delivery time.** Work with logistics partners, use regional fulfillment centers, or offer express shipping. Aim to bring the 6.1-day average down to 3–4 days.
3. **Double down on top categories, and diversify.** Invest marketing and inventory in the best-performing categories, while testing promotions for weaker ones to reduce dependence on a few lines.
4. **Grow underperforming regions.** Run region-specific campaigns, local partnerships, or shipping discounts in the lowest-revenue region.
5. **Optimize payment options.** Promote the most-used payment method with incentives (e.g., cashback), and investigate whether friction is limiting the less-used methods.
6. **Increase AOV further.** Introduce bundles, free-shipping thresholds, and cross-sell recommendations.
7. **Track these KPIs monthly.** Use the dashboard's date filter to measure whether the changes above are improving revenue, ratings, and delivery times.
