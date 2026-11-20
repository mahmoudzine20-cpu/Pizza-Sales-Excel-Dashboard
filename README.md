🍕 Pizza Sales Dashboard                   
An end-to-end Excel analytics project: raw pizza order data is cleaned with Power Query, modeled as a star schema in Power Pivot, summarized with Pivot Tables, and presented in an interactive dashboard with KPI cards, charts, and slicers.
---
📌 Project Overview
Item	Detail
Tool	Microsoft Excel (Power Query, Power Pivot, Pivot Tables, Slicers, Timeline)
Period	2015 (monthly / weekly analysis)
Goal	Understand sales performance by category, size, product, month and weekday
Output	Single-page interactive dashboard
Headline KPIs
KPI	Value
Total Sales	$8,436
Total Quantity	511
Total Orders	499
Total Customers	499
---
🔄 Workflow
```
Raw Data → Power Query (Cleaning) → Power Pivot (Star Schema + DAX) → Pivot Tables → Dashboard
```
---
1️⃣ Data Cleaning (Power Query)
The raw data was loaded into Power Query and prepared before modeling:
Import the source tables (orders, order details, pizzas, customers) into the Power Query Editor.
Promote headers and make sure column names are clear and consistent (e.g., `order_id`, `order_date`, `pizza_category`, `pizza_size`).
Fix data types: dates as `Date`, quantities as `Whole Number`, prices and sales as `Decimal Number`, text fields as `Text`.
Remove duplicates and empty rows, and handle `null` / missing values.
Trim and clean text (extra spaces, inconsistent casing) in pizza names, categories, and sizes.
Split / derive columns from the order date: `Month` (numbered, e.g. `01-January` so months sort correctly) and `Weekday`.
Create calculated columns such as `Sales = Quantity × Price`.
Merge / join queries where needed to build clean dimension tables (pizza details, customers, dates).
Load to the Data Model (connection only / Data Model) instead of loading to worksheets, to keep the file light.
---
2️⃣ Data Modeling (Power Pivot)
The cleaned tables were loaded into the Excel Data Model and organized as a star schema:
Fact table: order details (order_id, pizza_id, quantity, sales, order_date)
Dimension tables:
Pizza (name, category, size, price)
Customers (customer name)
Date / Calendar (date, month, weekday, quarter, year)
Relationships were created in Diagram View as one-to-many (dimension → fact) with single-direction filtering.
Measures (DAX) used across the pivot tables and dashboard:
```DAX
Total Sales      = SUM ( FactOrders[Sales] )
Total Quantity   = SUM ( FactOrders[Quantity] )
Total Orders     = DISTINCTCOUNT ( FactOrders[order_id] )
Total Customers  = DISTINCTCOUNT ( Customers[Customer Name] )
```
3️⃣ Pivot Tables
All pivot tables are built from the Data Model, so one set of slicers controls everything:
Pivot Table	Fields	Purpose
KPI cards	Sales, Quantity, Orders, Customers	Headline numbers
Sales by Category	`pizza_category` → Sum of Sales	Category contribution
Sales by Size	`pizza_size` → Sum of Sales	Size distribution
Monthly Orders	`Month` → Count of `order_id`	Seasonality / peak months
Weekly Orders	`Weekday` → Count of `order_id`	Busiest days
Top 5 Pizzas	`pizza_name` → Sum of Sales (Value Filter: Top 5)	Best sellers
Bottom 5 Pizzas	`pizza_name` → Sum of Sales (Value Filter: Bottom 5)	Weakest sellers
<img width="365" height="299" alt="لقطة شاشة 2026-11-20 180202" src="https://github.com/user-attachments/assets/627e0692-2cf1-4dda-9271-6af2d928a834" />

---
4️⃣ Dashboard
The dashboard sheet is built from PivotCharts linked to the pivot tables above, with a clean layout: title banner, KPI cards, chart cards, and a filter panel.
Visuals
KPI cards: Total Sales, Total Quantity, Total Orders, Total Customers
Total Sales per Category (doughnut)
Sales Distribution by Pizza Size (pie)
Monthly Order Volume (line chart with markers and data labels)
Weekly Order Distribution (column chart)
Top 5 / Bottom 5 Best-Selling Pizzas (bar charts)
Interactivity
Slicers: `pizza_category`, `pizza_size`
Timeline: `order_date` (by quarters)
All slicers and the timeline are connected to every pivot table via Report Connections.
<img width="655" height="293" alt="لقطة شاشة 2026-11-20 180128" src="https://github.com/user-attachments/assets/9c099541-6362-48e9-ba18-059a61ec7e6d" />

---
🔍 Key Insights
Category mix is balanced: Veggie (28%) and Classic (27%) lead, followed by Supreme (24%) and Chicken (21%).
Large pizzas dominate: Size L generates 48% of sales, M 27%, S 22%, and XL only 3%.
Peak month is June with 54 orders, while March is the slowest with 30 orders; orders rise from April and stay high through summer.
Friday is the busiest day (91 orders) and Wednesday the slowest (48 orders).
Best seller: The Classic Deluxe Pizza, followed by The Four Cheese Pizza and The Thai Chicken Pizza.
Weakest seller: The Brie Carre Pizza, followed by The Spinach Supreme Pizza and The Chicken Alfredo Pizza.
Each order maps to a unique customer (499 orders = 499 customers), so there is no repeat-customer behavior in this dataset.
---
💡 Recommendations
Promote mid-week offers (especially Wednesday) to lift the slowest day.
Add combo deals pairing weak sellers with best sellers.
Review the XL size pricing / positioning given its low share.
Prepare extra stock and staff for Fridays and the May–September peak.
---
📁 Repository Structure
```
├── Pizza_Sales_Dashboard.xlsx   # Source file (Power Query, Data Model, Pivots, Dashboard)
├── images/
│   ├── star-schema.png
│   ├── pivot-tables.png
│   └── dashboard.png
└── README.md
```
