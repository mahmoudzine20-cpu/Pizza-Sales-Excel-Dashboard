🍕 Pizza Sales Dashboard 
An end-to-end Excel analytics project: raw pizza sales data is cleaned with Power Query, modeled with Power Pivot (star schema), analyzed with Pivot Tables, and presented in an interactive dashboard with KPIs, charts and slicers.
<img width="655" height="293" alt="لقطة شاشة 2026-11-20 180128" src="https://github.com/user-attachments/assets/ce2dcb27-4cb4-4f13-8e76-65399db56bbe" />

---
📌 Table of Contents
Project Overview
Business Questions
Tools & Skills
Project Workflow
Stage 1: Data Cleaning (Power Query)
Stage 2: Data Modeling (Power Pivot – Star Schema)
Stage 3: Analysis (Pivot Tables)
Stage 4: Dashboard (Source Code Layer)
Key Insights
Repository Structure
How to Use
---
📖 Project Overview
The goal of this project is to turn raw pizza order data into a clear, interactive dashboard that helps a business owner monitor sales performance, understand customer ordering behavior, and identify best- and worst-selling products.
Headline KPIs
KPI	Value
Total Sales	$8,436
Total Quantity	511
Total Orders	499
Total Customers	499
---
❓ Business Questions
How much revenue is generated, and from which pizza categories (Classic, Veggie, Supreme, Chicken)?
Which pizza sizes (S, M, L, XL) drive the most sales?
Which months and weekdays have the highest order volume?
What are the Top 5 and Bottom 5 best-selling pizzas?
---
🛠 Tools & Skills
Microsoft Excel
Power Query: ETL / data cleaning
Power Pivot (Data Model): relationships, star schema
DAX / Measures: Sum of Sales, Count of Orders, Count of Customers
Pivot Tables & Pivot Charts
Slicers & Timeline: interactive filtering
Dashboard design: KPI cards, layout, formatting
---
🔄 Project Workflow
```
Raw Data → Power Query (Clean) → Power Pivot (Star Schema) → Pivot Tables → Dashboard
```
Stage 1: Data Cleaning (Power Query)
The raw data was loaded into Power Query and prepared before modeling:
Import the source data into Power Query.
Inspect each column's profile (errors, empty values, distribution).
Fix data types: dates as `Date`, quantities and prices as numbers, IDs as text/whole numbers.
Handle nulls and duplicates: remove duplicate rows and treat missing values.
Standardize text: trim spaces and fix inconsistent casing in names, categories and sizes.
Split the data into logical tables (see star schema below) by separating customer, product and order attributes.
Derive date attributes from the order date: Month (with numeric prefix such as `01-January` so months sort correctly), Weekday, Quarter.
Calculate Sales per row (quantity × price) where needed.
Rename columns to clear, consistent names (`order_id`, `pizza_category`, `pizza_size`, `order_date`, ...).
Load to the Data Model (connection only) instead of to worksheets for better performance.
> ✏️ _Adjust the steps above to match exactly what you applied in your query._
Stage 2: Data Modeling (Power Pivot – Star Schema)
The cleaned tables were loaded into the Excel Data Model and connected as a star schema:
Fact table: order/sales transactions (order ID, quantity, sales, and foreign keys).
Dimension tables: Customers, Products (name, category, size), Dates.
Relationships: one-to-many from each dimension to the fact table (single-direction filtering).
Why a star schema? It gives faster pivot performance, simpler measures, and clean filtering from slicers across all visuals.
Measures created
`Sum of Sales`
`Count of order_id` (total orders)
`Count of Customer Name` (total customers)
Total Quantity
Stage 3: Analysis (Pivot Tables)
Pivot tables were built from the Data Model, each feeding one dashboard visual:
Pivot Table	Fields	Used For
Sales by Category	Category → Sum of Sales	Donut chart
Sales by Size	Size → Sum of Sales	Pie chart
Orders by Month	Month → Count of order_id	Line chart (monthly peaks)
Orders by Weekday	Weekday → Count of order_id	Column chart
Top 5 Pizzas	Pizza Name → Sum of Sales (Top 5 filter)	Bar chart
Bottom 5 Pizzas	Pizza Name → Sum of Sales (Bottom 5 filter)	Bar chart
KPI cards	Total sales, quantity, orders, customers	Header KPIs
<img width="365" height="299" alt="لقطة شاشة 2026-11-20 180202" src="https://github.com/user-attachments/assets/a0e62253-1b99-4fb9-8d21-72ddc579a28a" />

Stage 4: Dashboard (Source Code Layer)
The dashboard sheet is built entirely from the pivot tables above, with no hard-coded values:
KPI header linked to the pivot results (Total Sales, Quantity, Orders, Customers).
Pivot charts created from each pivot table:
Donut: Total Sales per Category
Pie: Sales Distribution by Pizza Size
Line: Monthly Order Volume
Column: Weekly Order Distribution
Bar: Top 5 / Bottom 5 Best-Selling Pizzas
Slicers (`pizza_category`, `pizza_size`) and a Timeline (`order_date`) connected to all pivot tables via Report Connections, so one click filters the whole dashboard.
Formatting: gridlines hidden, consistent color palette (red/orange), data labels, rounded card-style panels, and a clean layout.
---
💡 Key Insights
Veggie (28%) and Classic (27%) lead sales by category, followed by Supreme (24%) and Chicken (21%).
Large pizzas generate 48% of sales; XL contributes only 3%.
Order volume peaks in June (54 orders) and is lowest in March (30).
Friday is the busiest day (91 orders); Wednesday is the slowest (48).
Every order in the dataset maps to a unique customer (499 orders / 499 customers).
---
📁 Repository Structure
```
Pizza-Sales-Excel-Dashboard/
├── Pizza_Sales_Dashboard.xlsx   # Final workbook (data model, pivots, dashboard)
├── data/                        # Raw source data
├── images/
│   ├── dashboard.png
│   ├── pivot_tables.png
│   └── star_schema.png
└── README.md
```
