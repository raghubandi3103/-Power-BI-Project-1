🚀 Power BI Project: Retail Performance Dashboard – Maven Market
Interactive Retail Analytics | Goal Tracking | Profit Optimization
🧠 Project Overview

This Power BI dashboard provides a comprehensive view of Maven Market's retail KPIs. It enables users to:

Monitor monthly sales and performance goals

Identify top-performing product brands

Understand return rates and profit trends

Visualize country-level cost vs. profit comparisons

📊 Key Metrics & Insights

📓 Current Month Transactions: 18,325 (Goal: 17,339, +5.69%)

💰 Current Month Profit: $71.68K (Goal: $67.87K, +5.61%)

🔁 Current Month Returns: 496 (Goal: 482, +2.9%)

📌 Dashboard Highlights

✅ Top 30 Product Brands by:

Total Transactions

Total Profit

Return Rate

🌎 Country Filter: USA, Canada, Mexico

📈 Weekly Revenue Trend (Time Series)

📉 Profit vs. Cost Area Chart by Country

🔢 Revenue vs. Target Gauge

💼 Tools & Technologies Used

Power BI Desktop
Custom Slicers and Interactive Filters

DAX Measures (Profit, Returns, Goal Comparison, etc.)

Data Modeling (Fact & Dimension Tables)


----------------------
✅ Power BI DAX Snippets – Real-World Business Metrics & Data Modeling

📌 Use Cases: Sales Analysis | Customer Segmentation | Profitability | Returns Management

🧩 Data Preparation Steps
Replacing null values with zeros

Renaming columns as per business requirements

Assigning correct data types for all fields

Formatting revenue and currency columns

Adding calculated columns for business logic

📊 DAX Calculated Columns

End of Month = TRIM(EOYMONTH('Calendar'[Date], 0))

Weekend = IF('Calendar'[Name of Day] IN {"Saturday", "Sunday"}, "Y", "N")

Current Age = DATEDIFF(Customers[Birthdate], TODAY(), YEAR)

House Number = IF(T(Customers[customer_address]), SEARCH(" ", Customers[customer_address]))

Priority = IF(Customers[homeowner] = "Y" && Customers[member_card] = "Y", "High", "Standard")

Short_Country = UPPER(LEFT(Customers[Country/Region], 3))

Price_Tier = SWITCH(TRUE(), 
                   Products[product_retail_price] > 1000, "High", 
                   Products[product_retail_price] > 500, "Mid", 
                   "Low")
📐 DAX Measures

Unique Products = DISTINCTCOUNT(Products[product_name])

60 Day Revenue = CALCULATE(Total Revenue, 
    DATEINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -60, DAY))

Return Rate = 1 - DIVIDE([Quantity Returned], [Quantity Sold])

% Total Returns = COUNT(Returns[product_id]) * 1.0 / COUNT(Sales[product_id])

% Weekend Transactions = ([Weekend Transactions] / [Total Transactions]) * 100

Last Month Profit = CALCULATE([Total Profit], 
    DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -1, MONTH))

Last Month Returns = CALCULATE([Total Returns], 
    DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -1, MONTH))

Profit Margin = [Total Profit] / [Total Revenue]

Quantity Returned = SUM(Returns[quantity])

Quantity Sold = SUM(Transaction_Data[quantity])

Total Cost = SUMX(Transaction_Data, Transaction_Data[quantity] * Products[product_cost])

Total Revenue = SUM(Transaction_Data[sales_price])

Total Profit = [Total Revenue] - [Total Cost]

Weekend Transactions = CALCULATE([Transaction Count], 
    'Calendar'[Weekend] = "Y")

YTD Revenue = CALCULATE([Total Revenue], 
    DATESYTD('Calendar'[Date]))
💡 Key Business Insights Derived
Customer segmentation by priority and age

Product categorization by price tiers

Sales analysis over weekends, YTD, and rolling 60 days

Tracking returns, profit margins, and monthly changes

