# pizza_analysis_dashboard
🍕 Pizza Sales Analysis — Power BI Dashboard

An interactive Power BI dashboard built to analyze pizza sales performance — revenue, order volume, product mix, and best/worst sellers — for a fictional pizza business, based on a year of transactional order data.

📌 Overview

This project explores a pizza restaurant's sales data to uncover trends in revenue, order behavior, and product performance. The dashboard is built as a Power BI Template (.pbit) with two report pages: a Home overview page and a Best/Worst Sellers page, both fully interactive with slicers for filtering by pizza category and date.

🎯 Objectives
Track overall business KPIs: total revenue, total orders, average order value, total pizzas sold, and average pizzas per order
Identify daily and monthly sales trends
Understand product mix by pizza category and pizza size
Identify the best-performing and worst-performing pizzas by revenue, quantity sold, and number of orders
🗂️ Data Source
Source system: PostgreSQL database (pizzaDb, public.pizza_sales table)
Grain: One row per pizza line item within an order
Key columns
Column	Description
pizza_id	Unique ID for the pizza line item
order_id	Order identifier
pizza_name_id	Pizza SKU/variant identifier
pizza_name	Pizza name
pizza_category	Category (Classic, Veggie, Supreme, Chicken, etc.)
pizza_size	Size — cleaned to Regular, Medium, Large, X-Large
pizza_ingredients	Ingredients list
quantity	Quantity ordered
unit_price / total_price	Price per unit and line total
order_date / order_time	Date and time of the order
🔧 Data Preparation (Power Query / M)

Cleaning and transformation steps applied before loading into the model:

Standardized pizza_size values (S → Regular, M → Medium, L → Large, XLarge → X-Large)
Derived new columns from order_date:
Day Name and Day number (Sunday = 1 → Saturday = 7, for correct weekday sort order)
Month Name and Month number
Removed unused intermediate columns after transformation
🧮 Data Model & Measures

Single fact table (public pizza_sales) plus auto-generated date hierarchy tables. Core DAX measures:

Measure	Formula	Purpose
Total Revenue	SUM(total_price)	Total sales value
TOTAL_ORDERS	DISTINCTCOUNT(order_id)	Total number of unique orders
Average order value	[Total Revenue] / [TOTAL_ORDERS]	Avg. revenue per order
Total pizzas sold	SUM(quantity)	Total units sold
Avg pizzas per order	[Total pizzas sold] / [TOTAL_ORDERS]	Avg. basket size
📊 Dashboard Pages
1. Home
KPI cards: Total Revenue, Average Order Value, Total Orders, Total Pizzas Sold, Avg Pizzas per Order
Column chart — Daily Trend for Total Orders
Area chart — Monthly Trend for Total Orders
Donut chart — % of Sales by Pizza Category
Donut chart — % of Sales by Pizza Size
Funnel chart — Total Pizzas Sold by Pizza Category
Slicers — Pizza Category, Order Date
2. Best/Worst Sellers
Same KPI cards for context
Bar charts comparing Top 5 vs Bottom 5 pizzas across three metrics:
By Revenue
By Quantity Sold
By Number of Orders
Slicers — Pizza Category, Order Date
Page navigation buttons between Home and Best/Worst Sellers
🛠️ Tools Used
Power BI Desktop — data modeling, DAX, report design
Power Query (M) — data cleaning and transformation
PostgreSQL — source database
🚀 How to Use
Download proj.pbit from this repository.
Open it in Power BI Desktop.
When prompted, connect it to your own PostgreSQL instance containing a pizza_sales table (or point it to a CSV/database with a matching schema).
Explore the Home and Best/Worst Sellers pages; use the slicers to filter by category and date range.

Screenshots : https://github.com/harshPai1906/pizza_analysis_dashboard/blob/main/Screenshot%202026-09-12%20102933.png
https://github.com/harshPai1906/pizza_analysis_dashboard/blob/main/Screenshot%202026-09-12%20103107.png
