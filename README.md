
# Executive Sales Performance Dashboard (Power BI)

An end-to-end Power BI business intelligence dashboard designed for executive stakeholders to monitor sales performance, seasonal revenue trends, product demand, and regional market distribution.

---

## 📊 Dashboard Overview

![Sales Performance Dashboard](Screenshot%202026-10-29%20105235.png)

### Key Metrics Monitored
* **Total Revenue:** $18M top-line sales performance
* **Total Orders:** 37K total transactions processed
* **Average Order Value (AOV):** $480 average spend per order
* **Total Units Sold:** 11M units moved across catalog lines

---

## 🏗️ Architecture & Data Modeling

The analytical model follows a classic **Star Schema** architecture to ensure optimized query execution and clean measure evaluation:

* **Fact Table:**
  * `Fact_Sales`: Transactional order records (order ID, line revenue, quantity, keys).
* **Dimension Tables:**
  * `Dim_Date`: Calendar dimension enabling multi-year time intelligence (`Date`, `YearMonth`, `Year`, `MonthName`).
  * `Dim_Product`: Product metadata (`Description`, unit prices, category info).
  * `Dim_Customer`: Geographic and customer attributes (`Country`, `CustomerID`).

### Data Cleaning & Modeling Considerations
* **Timestamp Normalization:** Resolved initial relationship mismatches between fact and dimension tables by standardizing all transactional date/time values to strict `Date` data types.
* **Relationship Cardinality:** Configured 1-to-many (`1:*`) relationships with single-direction cross-filtering from dimensions to the fact table.

---

## 📐 Core DAX Measures

All primary measures are organized in a dedicated `_Measures` table:

```dax
-- Total Top-Line Revenue
Total Revenue = 
SUM(Fact_Sales[Revenue])

-- Total Transactions Count
Total Orders = 
DISTINCTCOUNT(Fact_Sales[InvoiceNo])

-- Total Units Sold
Total Units Sold = 
SUM(Fact_Sales[Quantity])

-- Average Order Value (AOV)
Average Order Value = 
DIVIDE([Total Revenue], [Total Orders], 0)
