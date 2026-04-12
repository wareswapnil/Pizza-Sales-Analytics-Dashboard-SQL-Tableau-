# 🍕 Pizza Sales Analytics Dashboard

> **End-to-End Sales Analytics Project** using SQL, Python (Jupyter Notebook), Excel, Power BI & Tableau

---

## 📊 Project Overview

This project performs a comprehensive analysis of pizza sales data spanning **January 2015 to December 2015**. It covers the full analytics pipeline — from raw data cleaning and SQL querying to interactive dashboards in Power BI and Tableau.

**Key Business Questions Answered:**
- Which pizzas generate the most revenue, orders, and quantity sold?
- What are the busiest days, times, and months for orders?
- Which pizza categories and sizes dominate sales?
- Who are the best and worst performers in the menu?

---

## 🗂️ Project Structure

```
Pizza-Sales-Analytics-Dashboard/
│
├── data/
│   └── pizza_sales.csv                  # Raw sales dataset
│
├── sql/
│   └── pizza_sales_queries.sql          # All SQL queries used for KPIs & analysis
│
├── notebooks/
│   └── Pizza_Sales_EDA.ipynb            # Jupyter Notebook - EDA & Visualizations
│
├── excel/
│   └── Pizza_Sales_Excel.xlsx           # Excel Dashboard
│
├── powerbi/
│   └── Pizza_Sales_PowerBI.pbix         # Power BI Dashboard (2 pages)
│
├── tableau/
│   └── Pizza_Sales_Tableau.twbx         # Tableau Dashboard (2 pages)
│
├── screenshots/
│   ├── excel_dashboard.png
│   ├── tableau_page1.png
│   ├── tableau_page2.png
│   ├── powerbi_page1.png
│   └── powerbi_page2.png
│
└── README.md
```

---

## 📈 Key KPIs (Jan 2015 – Dec 2015)

| Metric | Value |
|---|---|
| 💰 Total Revenue | **$817.86K** |
| 🧾 Average Order Value | **$38.31** |
| 🍕 Total Pizzas Sold | **49,574** |
| 📦 Total Orders | **21,350** |
| 🔢 Avg Pizzas Per Order | **2.32** |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **SQL (MySQL / SQL Server)** | Data extraction, KPI calculation, aggregations |
| **Python (Jupyter Notebook)** | EDA, data cleaning, visualizations (Matplotlib, Seaborn, Pandas) |
| **Microsoft Excel** | Pivot tables, charts, Excel dashboard |
| **Power BI** | Interactive dashboard with slicers and drill-down |
| **Tableau** | Advanced visual analytics and storytelling |

---

## 📸 Dashboard Screenshots

### 📊 Excel Dashboard

![Excel Dashboard] <img width="1155" height="660" alt="Screenshot 2026-04-09 023835" src="https://github.com/user-attachments/assets/8e51997e-64d2-4847-a87f-b20a5ae3d898" />


> Single-page Excel dashboard showing KPIs, daily/hourly trends, best/worst sellers, and sales by category & size with a dark pizza-themed background.

---

### 📊 Tableau Dashboard

**Page 1 — Best / Worst Sellers**

![Tableau Best Worst Sellers] <img width="1541" height="867" alt="Screenshot 2026-04-09 025230" src="https://github.com/user-attachments/assets/30f3974e-7dd9-47b8-ba13-173ea8ee69c6" />


**Page 2 — Home (Trends & Category Performance)**

![Tableau Home Dashboard] <img width="1548" height="866" alt="Screenshot 2026-04-09 025208" src="https://github.com/user-attachments/assets/3585c95e-6078-4efe-b694-d91816cb9bc6" />


> Tableau dashboards feature interactive filters for Pizza Category and Order Date range, with hourly/weekly trend charts and category breakdown.

---

### 📊 Power BI Dashboard

**Page 1 — Best / Worst Sellers**

![Power BI Best Worst Sellers] <img width="1347" height="737" alt="Screenshot 2026-04-12 133649" src="https://github.com/user-attachments/assets/9d979af6-cfc4-4816-992b-4cd13fceb38c" />


**Page 2 — Home (Trends & Performance)**

![Power BI Home Dashboard] <img width="1347" height="738" alt="Screenshot 2026-04-12 133624" src="https://github.com/user-attachments/assets/62766b8c-1c52-4149-9ac6-31cacd057d5a" />


> Power BI dashboards include slicer filters, KPI cards, Top 5 / Bottom 5 pizza charts, and monthly/daily trend analysis.

---

## 🔍 Key Insights

### 🏆 Best Sellers
- **Revenue:** The Thai Chicken Pizza (~$43K)
- **Quantity & Orders:** The Classic Deluxe Pizza (~2.5K units, ~2.3K orders)

### 📉 Worst Sellers
- **Revenue, Quantity & Orders:** The Brie Carre Pizza (lowest across all metrics)

### 📅 Busiest Days & Times
- **Peak Days:** Friday and Saturday evenings
- **Peak Hours:** 12:00 PM – 1:00 PM and 4:00 PM – 7:00 PM
- **Peak Months:** July and January
- **Peak Week:** 48th week (December)

### 🍕 Category & Size Performance
- **Top Category:** Classic (26.91% of sales, $220.05K)
- **Top Size:** Large (45.89% of sales)

---

## 🧪 SQL Queries Used

```sql
-- Total Revenue
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

-- Average Order Value
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Avg_Order_Value FROM pizza_sales;

-- Total Pizzas Sold
SELECT SUM(quantity) AS Total_Pizzas_Sold FROM pizza_sales;

-- Total Orders
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;

-- Top 5 Pizzas by Revenue
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;

-- Daily Trend for Orders
SELECT DAYNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY DAYNAME(order_date);

-- % Sales by Pizza Category
SELECT pizza_category,
       ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales
GROUP BY pizza_category;

-- Hourly Trend for Orders
SELECT HOUR(order_time) AS order_hour, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY HOUR(order_time)
ORDER BY order_hour;
```

---

## 📉 Python EDA Highlights (Jupyter Notebook)

- Data loading and null-value checks using **Pandas**
- Distribution plots for pizza sizes and categories using **Seaborn**
- Monthly and hourly revenue trends using **Matplotlib**
- Top/bottom pizza visualizations using horizontal bar charts
- Correlation analysis between order quantity, price, and revenue

---

## 🚀 How to Run

### SQL
1. Import `pizza_sales.csv` into MySQL or SQL Server
2. Run queries from `sql/pizza_sales_queries.sql`

### Python
```bash
pip install pandas matplotlib seaborn jupyter
jupyter notebook notebooks/Pizza_Sales_EDA.ipynb
```

### Excel
1. Open `excel/Pizza_Sales_Excel.xlsx`
2. Refresh pivot tables if prompted

### Power BI
1. Open `powerbi/Pizza_Sales_PowerBI.pbix` in Power BI Desktop
2. Refresh data source if needed

### Tableau
1. Open `tableau/Pizza_Sales_Tableau.twbx` in Tableau Desktop or Tableau Public

---

## 👨‍💻 Author

**Swapnil Ware**  
Final Year B.E. – Information Technology  
JSPM Bhivrabai Sawant Institute of Technology and Research (SPPU), Pune  

[![GitHub](https://img.shields.io/badge/GitHub-wareswapnil-black?logo=github)](https://github.com/wareswapnil)  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/swapnil-ware)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
