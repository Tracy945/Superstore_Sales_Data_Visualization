# Superstore_Sales_Data_Visualization
A retail company sells a wide range of products to customers across different regions, states, and cities in the United States. Create visualization using PowerBI to understand sales performance and identify patterns that can support better business and sales decisions.

## Dataset

The dataset contains retail transaction records covering a four-year period from **2015 to 2018**. Each record includes information about orders, customers, geographic location, products, product categories, shipping methods, and sales, allowing performance to be analyzed from multiple perspectives.

## Project Objective

The objective of this project is to transform raw sales data into an interactive dashboard that provides clear and actionable insights into business performance. The analysis focuses on identifying sales trends, high-performing products and markets, and differences across customer segments.

## Key Questions

- How do sales change over time, and are there any noticeable trends or patterns?
- Which product categories, sub-categories, and products perform best?
- Which regions, states, and cities generate the highest sales?
- How do sales differ across customer segments and shipping methods?

## Tools & Technologies

**Power BI** is used for data cleaning and transformation, data modeling, DAX calculations, and interactive dashboard development. The project also uses **Power Query** for data preparation and **DAX** for creating analytical measures and KPIs.

## Data Preparation & Processing - Key Steps

1. **Remove duplicates**. Use command in Power Query to remove duplicate rows.
2. **Modify data types.** Change data type of column “Postal Code” from Number into Text.
3. **Create columns.** In Power Query, create a column “Processing Days” to indicate days taken to process each order, which helps to analysis the performance of processing time. 

!image.png

1. **Create New Measures & DAX.** In Power Query, create new measures to calculate Sales Growth Year-over-Year, Average Sales per Order, Total Sales under certain criteria. 
> [!INFO]
> 
```sql
Sales SPLY = 
	CALCULATE(
		[Total Sales], 
		SAMEPERIODLASTYEAR(superstore_sales_dataset[Order Date].[Date])
		)
```
