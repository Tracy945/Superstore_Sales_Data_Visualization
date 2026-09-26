# Superstore Sales Data Visualization

A retail company called Superstore sells a wide range of products to customers across different regions, states, and cities in the United States. Create **data visualization** using **PowerBI** to understand sales performance and identify patterns that can support better business and sales decisions.


## Table of Contents

- [1. Business Scenario](#1-business-scenario)
- [2. Dataset](#2-dataset)
- [3. Project Objective](#3-project-objective)
- [4. Key Questions](#4-key-questions)
- [5. Tools & Technologies](#5-tools--technologies)
- [6. Data Preparation & Processing](#6-data-preparation--processing)
- [7. Data Visualization Report & Key Insights](#7-data-visualization-report--key-insights)
  - [7.1. Report Overview](#71-report-overview)
  - [7.2. Sales Trend](#72-sales-trend)
  - [7.3. Product Performance](#73-product-performance)
  - [7.4. Customer Performance](#74-customer-performance)
  - [7.5. Operational Performance](#75-operational-performance)
- [8. Business Recommendation](#8-business-recommendation)
  - [8.1. Prepare for “Peak Season”](#81-prepare-for-peak-season)
  - [8.2. Promote Top-Selling Products](#82-promote-top-selling-products)
  - [8.3. Reward high-value customers](#83-reward-high-value-customers)
  - [8.4. Strengthen Distribution in High-Sales Areas](#84-strengthen-distribution-in-high-sales-areas)
  - [8.5. Prioritise High-Value Orders](#85-prioritise-high-value-orders)


</br>

## 1. Business Scenario
Superstore sells a wide range of products to customers across different regions, states, and cities in the United States. Management wants to understand sales performance and identify patterns that can support better business and sales decisions.

</br>

## 2. Dataset

The dataset contains retail transaction records covering a four-year period from **2015 to 2018**. Each record includes information about orders, customers, geographic location, products, product categories, shipping methods, and sales, allowing performance to be analyzed from multiple perspectives. </br>
*Data source: Superstore Sales Dataset  https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting*

</br>

## 3. Project Objective

The objective of this project is to transform raw sales data into an interactive dashboard that provides clear and actionable insights into business performance. The analysis focuses on identifying sales trends, high-performing products and markets, and differences across customer segments.

</br>

## 4. Key Questions

- How do sales change over time, and are there any noticeable trends or patterns?
- Which product categories, sub-categories, and products perform best?
- Which regions, states, and cities generate the highest sales?
- How do sales differ across customer segments?
- How shipping methods affect the processing time?
</br>

## 5. Tools & Technologies

**Power BI** is used for data cleaning and transformation, data modeling, DAX calculations, and interactive dashboard development. The project also uses **Power Query** for data preparation and **DAX** for creating analytical measures and KPIs.

</br>

## 6. Data Preparation & Processing

- **Remove duplicates**. Use command in Power Query to remove duplicate rows.
- **Modify data types.** Change data type of column “Postal Code” from Number into Text.
- **Create columns.** In Power Query, create a column “Processing Days” to indicate days taken to process each order, which helps to analysis the performance of processing time. 
<p align="center">
  <img src="images/create_column_image.png" width="60%">
</p>

- **New Measures & DAX.** In Power Query, create new measures to calculate Sales Growth Year-over-Year, and Average Sales per Order.
	```DAX
	-- Sales amount for Same Period Last Year (SPLY)
	Sales SPLY = 
		CALCULATE(
			[Total Sales], 
			SAMEPERIODLASTYEAR(superstore_sales_dataset[Order Date].[Date])
		)
		
	-- Sales growth Year-over-Year (YoY Growth)
	Sales YoY Growth = 
		DIVIDE(
    		[Total Sales] - [Sales SPLY],
    		[Sales SPLY],
    		BLANK()
		)
	
	-- Average Sales per Order
	Average Sales per Order = 
		DIVIDE(
    		[Total Sales],
    		DISTINCTCOUNT([Order ID]),
    		0
		)
	```

- **Create data hierarchy**. Group data by hierarchical relationship for later application of drill-down function in the visuals. 
<p align="center">
  <img src="images/hierarchy_image.png" width="25%">
</p>

</br>

## 7. Data Visualization Report & Key Insights

### 7.1. Report Overview

[Download PowerBI Report](./PowerBI/superstore_sales_dashboard.pbix)

The final report has 4 pages (dashboards). Each page contains several visuals focusing on one aspects of the sales data.

- Sales Trend -  Overall sales over time, yearly growth of each year.
- Product performance - Product category performance, top sales products.
- Customer performance - Top contribution customers, top sales by states and cities.
- Operational Performance - Corelation between processing days and value of orders, how ship mode affects the processing days.

### 7.2. Sales Trend

This page explores sales trends over the years, the latest year sales performance in each category, and year-over-year growth to identify key changes in business performance. 

<p align="center">
  <img src="images/dashboard_Sales_Trend.png">
</p>

The trend line shows overall sales has been going upwards from 2015 to 2018, so the forecasting line  shows an increasing trend in the following year. YoY Growth also confirms that there is a significant growth in 2017 and 2018.

A recurring pattern can be noticed that there is a higher sales from September to December in each year. Meaning this period of time would be the peak season for the company. 

The visual in the bottom right corner can be used as a filter, to explore further how sales trends changes for each states. For example, below screenshot shows the data visuals for California only.

<p align="center">
  <img src="images/sales_trend_California.png">
</p>


### 7.3. Product Performance

This page shows a detail performance of sales in terms of product categories, sub-categories, and specific products. 

<p align="center">
  <img src="images/dashboard_Product_Performance.png">
</p>

From the donut chart we can see the sales composition percentage of categories. Also the drill-down function allow us to explore the composition of sub-categories under each category, then further the specific products.

<p align="center">
  <img src="images/category_drill-down.png" width="60%">
</p>

The table and the bar charts give straight forward information about the top sales sub-categories and products. 

Interestingly, the top 1 selling product, which significantly outperformed the 2nd-ranked product, is a Cannon copier, while copier is only the 8th ranking sub-category in sales. That’s because the unit price of copier is much higher than other sub-categories, even it doesn’t have many orders.

<p align="center">
  <img src="images/Cannon_copier.png">
</p>

The slicer on top gives the option to filter the visuals in specific time range. For example, getting information for the latest year.

### 7.4. Customer Performance

Similar to the Product Performance page, this page shows the performance of sale in terms of the buying segment, customers, and the geographic distribution across United States.

<p align="center">
  <img src="images/dashboard_Customer_Performance.png">
</p>

From this page we can see buyers from California and New York contributes the most sales amount, and so as the biggest cities in these states — Los Angeles and New York City. This suggests that population is likely to be closely related to sales in a region.

The pie chart indicates that the Consumer segment takes up more than half of total sales, followed by the Corporate segment, while the Home Office segment accounts for the smallest share. 

### 7.5. Operational Performance

This page focus on the processing time required for orders.  

<p align="center">
  <img src="images/dashboard_Operational_Performance.png">
</p>

The matrix and column chart suggest that the number of days required to process orders is strongly associated with the selected ship mode. The “Same Day” ship mode takes the least time, as its name suggests, while the “Standard Class” ship mode takes the longest, usually more than four days.
The scatter chart on the right shows a negative correlation between the average processing time and average sales value across different sub-categories. In particular, expensive items such as Copiers and Machines tend to have shorter processing times than cheaper items.

</br>

## 8. Business Recommendation

### 8.1. Prepare for “Peak Season”

As the sales trend visuals suggest, the period from September to December is the peak sales period of the year. The company could make preparations in advance to better handle the increased demand. For example, it could hire temporary workers during this period, secure additional logistics capacity, and upgrade the infrastructure of its online shopping platforms to ensure they can handle higher traffic.

### 8.2. Promote Top-Selling Products

After identifying the top-selling products and sub-categories, the company can develop targeted marketing strategies to further promote these popular items, such as phones and chairs. These products could be given greater visibility by being displayed upfront of the online shopping website. The company could also offer targeted discounts on selected products to attract more orders and potentially increase sales.

### 8.3. Reward high-value customers

Since some customers generate significantly more revenue than others, offering them targeted rewards can boost loyalty and retention. It could offer exclusive VIP benefits, such as select discounts, faster shipping options, or premium customer support. The goal is to enhance the customer experience and incentivize these top-tier shoppers to remain loyal.

### 8.4. Strengthen Distribution in High-Sales Areas

The analysis identifies the states and cities that generate the highest sales. The company could allocate more inventory and logistics resources to these high-performing areas to better meet local demand. Establishing additional distribution capacity in key locations could also help reduce shipping times and improve customer satisfaction.

### 8.5. Prioritise High-Value Orders

Since high-value products tend to have shorter processing times, the company could consider prioritising high-value orders in its fulfilment process. Allocating sufficient operational resources to these orders may help maintain fast processing times and support a positive customer experience.

