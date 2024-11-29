
# E-commerce Smart Shopper Customer Segmentation Dashboard

### Dashboard Link : https://app.powerbi.com/reportEmbed?reportId=35a954cf-5307-4dfb-8691-e678149edbe9&autoAuth=true&ctid=b229e865-9b90-4f42-a7fb-170005d839ae

## Problem Statement

he goal of this dashboard is to help e-commerce businesses understand their customers better by segmenting them into meaningful groups based on purchasing behavior. Using advanced analytics, we provide actionable insights to improve customer retention, boost sales, and refine marketing strategies. The dashboard highlights key metrics like total sales, customer segmentation, spending patterns, and geographic distribution.

Key questions addressed include:

1.Who are the top-performing customers and clusters?

2.What are the key sales trends over time?

3.How does customer behavior vary across regions?


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".

- Step 4 :Data(Fact): InvoiceNo	StockCode	Description	Quantity	 InvoiceDate	UnitPrice	CustomerID	Country

  Customer_segmentaton_data_(Dim): CustomerID	Amount	Frequency	Recency	Cluster_Id	Cluster Recency Group
  Data Cleaning in Power Query:
 -Renamed columns for consistency.
 -Removed duplicates and errors in the data.
 -Merged sales data with customer and product tables.
 -extracted date components (Year, Quarter, Month) from transaction dates.

- Step 5 :Data Modeling
Relationships Created:
Connected Sales Transactions to Customer Information and Customer_id using relationships:
Customer ID → Primary Key for Customer Table.
Custoomer_id → Primary Key for Product Table.

- Step 6 :Table Schema:
Designed a star schema with a central fact table (Data(fact)) and dimension tables (Customer_segmentaton_data_(Dim)).

- Step 7 :DAX Calculations
Custom DAX formulas were created for metrics and KPIs:
- Total Sales = SUMX('Data(Fact)','Data(Fact)'[Quantity]*'Data(Fact)'[UnitPrice])

![Total Sales](https://github.com/user-attachments/assets/b9437950-c201-46e1-acda-149196dd57e2)

- Total Customers = DISTINCTCOUNT('Data(Fact)'[CustomerID])

![Total Customers](https://github.com/user-attachments/assets/64b31625-cfd7-4588-9b25-8ea28cf685b5)

- Average Order Value = [Total Sales]/DISTINCTCOUNT('Data(Fact)'[InvoiceNo])

![Avg order value](https://github.com/user-attachments/assets/c40824e6-e961-414f-8cb1-90c227bce218)

- Orders Processed = DISTINCTCOUNT('Data(Fact)'[InvoiceNo])

![Order Proceed](https://github.com/user-attachments/assets/bc26bffa-6109-4b23-8205-3dad98d0a535)

- Inactive Customers = 
CALCULATE(DISTINCTCOUNT('Data(Fact)'[CustomerID]),FILTER('Data(Fact)',DATEDIFF(MAX('Data(Fact)'[InvoiceDate]),TODAY(),DAY)>90))

![Inactive Customers](https://github.com/user-attachments/assets/e745bc05-07d2-4cd9-9e06-e186ae04a3da)


- Recency Group = 
SWITCH(
    TRUE(),
    'Customer_segmentaton_data_(Dim)'[Recency] <= 30, "0–30 Days",
    'Customer_segmentaton_data_(Dim)'[Recency] <= 60, "31–60 Days",
    'Customer_segmentaton_data_(Dim)'[Recency] <= 90, "61–90 Days",
    "90+ Days"
)

![Customer Recency](https://github.com/user-attachments/assets/912ac539-85aa-4252-8eef-673fae2dae69)


- Inactive churn risk Customers = 
CALCULATE(DISTINCTCOUNT('Data(Fact)'[CustomerID]),FILTER('Data(Fact)',DATEDIFF(MAX('Data(Fact)'[InvoiceDate]),TODAY(),DAY)>90))

![Customer churn risk](https://github.com/user-attachments/assets/a1e741f9-36e8-4a8e-9456-348fc9ccef02)

- Total Spending = SUM('Customer_segmentaton_data_(Dim)'[Amount])

![Total Spending](https://github.com/user-attachments/assets/e0bf3df8-0155-4d1e-9937-42285f5ea23a)


# Insights

Insights Gained
Sales Trends:
Quarterly trends show a sales spike in Q4, driven by seasonal promotions.
Sales by year demonstrate consistent growth of 20% annually.

Customer Segmentation:
60% of customers belong to the "Loyal" cluster, contributing to 70% of sales.
High churn risk among customers in "New" and "Low Value" clusters.

Geographic Insights:
USA accounts for 40% of total sales, with significant potential for expansion in Europe.

Top Customers:
The top 10 customers contribute to 25% of total sales, underscoring the importance of personalized strategies.


# Dashboard Snapshots
## Page 1: Overview and Key Metrics

![Page 1](https://github.com/user-attachments/assets/6fd2c842-11bf-42a9-9a53-99b8a27fd3c0)

## Page 2: Sales and Customer Analysis

![Page 2](https://github.com/user-attachments/assets/54e45171-25b4-4ef1-8d76-9ff2f385ea2c)

## Page 3: Geographic Insights

![Page 3](https://github.com/user-attachments/assets/13ce7f78-01ca-4682-8ef1-152032d7465d)

## All Pages:

![All Pages](https://github.com/user-attachments/assets/c68a0c95-de81-4470-af9c-fad3af90db10)


## Snapshot of Dashboard (PowerBI Services):

![Snapshot of Dashboard (PowerBI Services)](https://github.com/user-attachments/assets/95fd3161-c9a3-4dc1-81ea-2e328ca5b5ca)
