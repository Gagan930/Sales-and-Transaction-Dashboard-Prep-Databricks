# 🛍️ Transaction Dashboard — Sales Analytics on Databricks

[![Platform](https://img.shields.io/badge/Platform-Databricks-FF3621?style=flat-square)](https://www.databricks.com/)
[![Built with](https://img.shields.io/badge/Built%20with-AI%2FBI%20Dashboards-blue?style=flat-square)](https://www.databricks.com/product/ai-bi)
[![Data](https://img.shields.io/badge/Source-Unity%20Catalog%20Samples-green?style=flat-square)](https://docs.databricks.com/en/discover-databricks/sample-datasets.html)
[![SQL](https://img.shields.io/badge/Language-SQL-lightgrey?style=flat-square)]()

> An interactive, production-ready **Databricks AI/BI Dashboard (Lakeview)** that transforms raw bakery sales transactions into actionable revenue, product, payment, and volume insights — built entirely with SQL and dashboard-as-code (`.lvdash.json`), no external BI tools required.

---

## 📖 Overview

**Transaction Dashboard** analyzes 3,300+ sales transactions from the *Bakehouse* sample dataset (`samples.bakehouse.sales_transactions` in Unity Catalog), covering **May 1–17, 2024** across six bakery products and three payment methods.

The dashboard answers four core business questions:

1. **Which products drive the most revenue?** → Revenue ranking across all products
2. **How do customers pay?** → Payment-method transaction mix
3. **How is sales volume trending over time?** → Daily units sold
4. **How do these metrics interact?** → Global filters for interactive slicing

---

## 🎯 Key Insights at a Glance

| Insight | Detail |
| --- | --- |
| 🥇 Top product | **Golden Gate Ginger** — **$11,595** revenue, the highest seller 8 years in a row |
| 💰 Total revenue | **$66,471** across all 6 products |
| 💳 Payments | **Mastercard** leads with 1,144 transactions (Amex 1,106 · Visa 1,083) — an even ~⅓ split |
| 📈 Sales volume | **22,157 units** sold over 17 days (~1,300/day average) |
| 🔝 Peak day | **May 6, 2024** — 1,500 units in a single day |

### Revenue by Product

| Rank | Product | Total Revenue |
| --- | --- | --- |
| 1 | Golden Gate Ginger | $11,595 |
| 2 | Outback Oatmeal | $11,199 |
| 3 | Austin Almond Biscotti | $11,148 |
| 4 | Tokyo Tidbits | $10,986 |
| 5 | Pearly Pies | $10,785 |
| 6 | Orchard Oasis | $10,758 |

---

## 📊 Dashboard Pages & Widgets

### Page 1 — `Dashboard` (main canvas)

| Widget | Type | Description |
| --- | --- | --- |
| Total Price By Product | **Bar** | Revenue per product, ranked descending — Golden Gate Ginger at #1 |
| Total Price By Product (raw) | **Bar** | Revenue per product served directly from the base dataset |
| Payment Method Breakdown | **Pie** | Transaction share by payment method |
| Total Transactions by Payment Method | **Pie** | Transaction counts derived using payment method |
| Quantity of Sales Over Time | **Line** | Daily units sold across the full May 1–17 window |
| Narrative text | **Text** | Context/callout widget for headline findings |

### Page 2 — `Global Filters`

| Widget | Type | Description |
| --- | --- | --- |
| Range slider | **Slider** | Interactive value-range filter that slices all connected widgets on the main page |

---

## 🗃️ Data Source

**Table:** `samples.bakehouse.sales_transactions` (Databricks sample Bakehouse dataset — synthetic bakery franchise transactions, shared via Delta Sharing)

### Schema

| Column | Type | Description |
| --- | --- | --- |
| `transactionID` | BIGINT | Unique transaction identifier |
| `customerID` | BIGINT | Customer reference |
| `franchiseID` | BIGINT | Store/franchise reference |
| `dateTime` | TIMESTAMP | Transaction timestamp |
| `product` | STRING | Product name |
| `quantity` | BIGINT | Units sold |
| `unitPrice` | BIGINT | Price per unit |
| `totalPrice` | BIGINT | Total transaction price |
| `paymentMethod` | STRING | `amex`, `mastercard`, or `visa` |
| `cardNumber` | BIGINT | Card reference |

### Dataset Queries Behind the Widgets

**Product revenue ranking (Product_Sales_Desc):**

```sql
SELECT product, SUM(totalPrice)
FROM samples.bakehouse.sales_transactions
GROUP BY product
ORDER BY SUM(totalPrice) DESC;
```

**Full transaction feed (From Notebook):**

```sql
SELECT * FROM samples.bakehouse.sales_transactions;
```

---

## 🧰 Tech Stack

* **Databricks AI/BI Dashboards (Lakeview)** — dashboards stored as version-controlled JSON (`.lvdash.json`)
* **Databricks SQL** — serverless warehouse powering all dataset queries
* **Unity Catalog** — governed access to the `samples` catalog
* **Git** — dashboard-as-code, source-controlled on GitHub

---

## 🚀 Getting Started

### Prerequisites

* A Databricks workspace (Free Edition works)
* Access to the `samples.bakehouse.sales_transactions` table (available by default in most workspaces)

### Steps

1. **Clone the repo**

   ```bash
   git clone https://github.com/Gagan930/Sales-and-Transaction-Dashboard-Prep-Databricks.git
   ```

2. **Import the dashboard** — In your Databricks workspace, use **Workspace → Import** (or drag-and-drop) to upload `Transaction Dashboard.lvdash.json` into your workspace.
3. **Open it** in the AI/BI dashboard editor; queries run against `samples.bakehouse.sales_transactions` automatically.
4. **Publish** with **Publish** in the top-right, then share with stakeholders using the **Share** button (use *shared data permission* so viewers don't need direct table access).

---

## 📁 Repository Structure

```text
Sales-and-Transaction-Dashboard-Prep-Databricks/
├── Transaction Dashboard.lvdash.json   # AI/BI dashboard definition (pages, widgets, datasets)
└── README.md                           # This file
```

---

## 🔮 Possible Enhancements

* Add franchise-level and customer-level breakdowns (`franchiseID`, `customerID`)
* Revenue-over-time line chart alongside quantity trends
* Currency formatting and KPI headline tiles (total revenue, transactions, avg order value)
* Scheduled refresh / alerting on volume anomalies

---

## 🙌 Author

**Gagan930** — [GitHub](https://github.com/Gagan930)

Built as a capstone sales-analytics showcase on Databricks AI/BI Dashboards.
