# 🍕 Pizza Sales Analytics Dashboard

> An end-to-end sales analytics project built with **SQL + Power BI** and **SQL + Tableau**, transforming raw pizza order data into two fully interactive Business Intelligence dashboards with deep insights on revenue, orders, product performance, and customer behavior.

---

## 📊 Project Overview

This project analyzes **Pizza Sales data (Jan 2015 – Dec 2015)** across **two separate dashboard implementations**:

| Dashboard | Tool | Focus |
|---|---|---|
| Dashboard 1 | **SQL + Power BI** | KPIs, category/size breakdown, best & worst sellers |
| Dashboard 2 | **SQL + Tableau** | KPIs, hourly/weekly trends, multi-page drill-down views |

All visualizations are backed by structured **SQL queries** for data extraction, aggregation, and KPI calculation.

---

## 🗂️ Repository Structure

```
Pizza-Sales-Analytics-Dashboard-SQL-Tableau/
│
├── data/
│   └── pizza_sales.csv                    # Raw dataset
│
├── sql/
│   ├── kpi_queries.sql                    # Revenue, orders, avg value KPIs
│   ├── trend_analysis.sql                 # Daily, hourly, weekly trends
│   ├── category_size_analysis.sql         # Sales by category and size
│   └── best_worst_sellers.sql             # Top 5 & Bottom 5 pizza analysis
│
├── powerbi/
│   └── Pizza_Sales_Dashboard.pbix         # Power BI dashboard file
│
├── tableau/
│   └── Pizza_Sales_Dashboard.twbx         # Packaged Tableau workbook
│
├── assets/
│   ├── sql-powerbi-dashboard.png
│   ├── tableau-dashboard-home.png
│   └── tableau-dashboard-sellers.png
│
└── README.md
```

---

## 🖥️ Dashboard 1 — SQL + Power BI

### KPIs
| Metric | Value |
|---|---|
| 💰 Total Revenue | $68,737 |
| 🛒 Total Orders | 1,799 |
| 🍕 Total Pizzas Sold | 4,151 |
| 💵 Avg Order Value | $38.21 |
| 📦 Avg Pizzas Per Order | 2.31 |

### Features
- **Daily Order Trends** — bar chart across all 7 days (peak: Wednesday with 306 orders)
- **Hourly Order Trends** — line chart showing peak at 12–1 PM and 4–8 PM
- **% of Sales by Pizza Category** — donut chart (Classic: 27.38%, Supreme: 25.67%, Veggie: 22.99%, Chicken: 23.97%)
- **% of Sales by Pizza Size** — pie chart (Large dominates at 44.55%)
- **Total Pizzas Sold by Category** — horizontal bar (Classic: 1253, Supreme: 1013, Veggie: 961, Chicken: 924)
- **Top 5 Best Sellers** — Hawaiian (219), Classic Deluxe (216), Barbecue Chicken (214)
- **Bottom 5 Worst Sellers** — Brie Carre at the bottom (32 units)
- **Date Slicer** — filter by order date (2015–2016)

### Screenshot
![SQL Power BI Dashboard]<img width="1155" height="660" alt="Screenshot 2026-04-09 023835" src="https://github.com/user-attachments/assets/930fe93a-ceb2-4ec9-a33a-b1342bc79353" />


---

## 📊 Dashboard 2 — SQL + Tableau

### KPIs
| Metric | Value |
|---|---|
| 💰 Total Revenue | $817.9K |
| 🛒 Total Orders | 21.4K |
| 🍕 Total Pizzas Sold | 49.6K |
| 💵 Avg Order Value | $38.31 |
| 📦 Avg Pizzas Per Order | 2.32 |

### Page 1 — Home (Sales Overview)
- **Hourly Trends** — stacked bar by category (peak: 12–1 PM & 4–7 PM)
- **Weekly Order Trends** — line chart with Avg 402.8 orders/week (peak: Week 48, December)
- **% Sales by Pizza Category** — donut chart (Classic: $220.05K / 26.91%)
- **% Sales by Pizza Size** — horizontal bar (Large: 45.9%, Medium: 30.5%, Regular: 21.8%)
- **Total Orders & Pizzas Sold by Category** — grouped bar chart
- **Pizza Category & Date Filters** — interactive slicers

### Page 2 — Best & Worst Sellers
- **Top 5 by Revenue** — Thai Chicken Pizza leads ($43.43K)
- **Top 5 by Quantity** — Classic Deluxe most ordered (2.45K units)
- **Top 5 by Orders** — Classic Deluxe with 2,329 orders
- **Bottom 5 by Revenue** — Brie Carre Pizza ($11.59K)
- **Bottom 5 by Quantity** — Brie Carre Pizza (490 units)
- **Bottom 5 by Orders** — Brie Carre Pizza (480 orders)

### Screenshots
![Tableau Home Dashboard] <img width="1548" height="866" alt="Screenshot 2026-04-09 025208" src="https://github.com/user-attachments/assets/4b1166d9-0e60-4447-8108-c513593b6bf1" />

![Tableau Sellers Dashboard]<img width="1541" height="867" alt="Screenshot 2026-04-09 025230" src="https://github.com/user-attachments/assets/5b77d0bc-756b-44d7-a9aa-d646994305ba" />


---

## 💡 Key Business Insights

- 📅 **Busiest Days:** Friday and Saturday evenings record the highest order volumes
- ⏰ **Peak Hours:** 12–1 PM and 4–7 PM are the highest demand windows
- 📆 **Busiest Week:** Week 48 (December) — single highest weekly order spike
- 🏆 **Top Category:** Classic pizzas lead in revenue, quantity sold, and total orders
- 📏 **Top Size:** Large pizzas account for ~45–46% of total sales across both dashboards
- ⭐ **Best Seller (Revenue):** Thai Chicken Pizza | **Best Seller (Volume):** Classic Deluxe Pizza
- ❌ **Worst Seller:** Brie Carre Pizza — consistently lowest across revenue, quantity, and orders

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **SQL (MySQL / PostgreSQL)** | Data extraction, KPI queries, trend & category analysis |
| **Power BI Desktop** | Dashboard 1 — interactive visuals with slicers |
| **Tableau Desktop / Public** | Dashboard 2 — multi-page drill-down analytics |
| **Excel / CSV** | Raw data source |

---

## 📐 SQL Queries

### Total Revenue & All KPIs
```sql
SELECT 
    ROUND(SUM(total_price), 2)                                    AS Total_Revenue,
    ROUND(SUM(total_price) / COUNT(DISTINCT order_id), 2)         AS Avg_Order_Value,
    SUM(quantity)                                                  AS Total_Pizzas_Sold,
    COUNT(DISTINCT order_id)                                       AS Total_Orders,
    ROUND(SUM(quantity) / COUNT(DISTINCT order_id), 2)            AS Avg_Pizzas_Per_Order
FROM pizza_sales;
```

### Hourly Trend for Total Orders
```sql
SELECT HOUR(order_time) AS Order_Hour,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY HOUR(order_time)
ORDER BY Order_Hour;
```

### Daily Trend for Total Orders
```sql
SELECT DAYNAME(order_date) AS Day_Name,
       COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DAYNAME(order_date)
ORDER BY FIELD(Day_Name,'Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday');
```

### % Sales by Pizza Category
```sql
SELECT pizza_category,
       ROUND(SUM(total_price), 2) AS Total_Revenue,
       ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS Pct_Sales
FROM pizza_sales
GROUP BY pizza_category;
```

### Top 5 Best Sellers by Revenue
```sql
SELECT pizza_name,
       ROUND(SUM(total_price), 2) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;
```

### Bottom 5 Worst Sellers by Quantity
```sql
SELECT pizza_name,
       SUM(quantity) AS Total_Quantity
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity ASC
LIMIT 5;
```

---

## 🧠 Learnings & Skills Demonstrated

- ✅ Wrote optimized SQL queries for KPI extraction, trend analysis, and aggregations
- ✅ Built an interactive **Power BI dashboard** with slicers, donut/pie charts, and bar charts
- ✅ Built a multi-page **Tableau dashboard** with filters, tooltips, and drill-down navigation
- ✅ Compared two BI tools on the same dataset — understanding strengths of each
- ✅ Performed comparative analysis across categories, sizes, and time dimensions
- ✅ Practiced data storytelling — presenting raw data as actionable business insights
- ✅ Identified revenue drivers and underperforming products for business decision-making

---

## 📬 Connect

**Swapnil Ware**  
Final Year IT Student | Data Science & AI Enthusiast

- 🔗 [LinkedIn](https://www.linkedin.com/in/swapnilware)
- 💻 [GitHub](https://github.com/wareswapnil)
- 📧 swapnil.ware@email.com

---

> ⭐ *If you found this project useful, consider giving it a star!*
