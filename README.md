# Revenue-Bike-Store
-  [Interact with the dashboard here](https://public.tableau.com/views/UpdatebikeSales/Dashboard1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)

## Introduction
Walter Reed Bike Company data analysis is a recent project that aims to give a detailed summary of the revenue of a bike company for 3 years consecutively. The aim was to provide an executive dashboard for the company showing the revenue changes for the company in 3 tears. 
## Objectives
The goal of the analysis was to visualize;
- Total Revenue for the years
- Sales by category
- Revenue per month basis
- Revenue by store
- Revenue by Customer
- Revenue by State

## Data Source
The data used for this project was derived from the company’s database

## Tools
-  SQL - For extracting data from the database of the company. I used a lot of join to join more than 5 different tables from the company’s database

-  Tableau
For data visualization

## Data ANatomy
- The database of the company consisted of more than 5 different tables which included
- Production brands
- Production category
- Production Products
- Sales Category
- Sales Stores
- Sales Staffs
- Sales Items

However, the challenge was that there was not a single table in the company's database that demonstrated this data. So I hard to write SQL queries to join the different tables together from the company’s database.
``` SQL

SELECT 
       ord.order_id,
	   concat(cus.first_name, '  ', cus.last_name) as 'Customer Full_name',
	   cus.city,
	   cus.state,
	   ord.order_date,
	   SUM(ite.quantity) as total_units,
	   SUM(ite.quantity * ite.list_price) as revenue,
	   pro.product_name,
	   cat.category_name,
	   sto.store_name,
	   CONCAT(sta.first_name, '  ', sta.last_name) as 'Sales rep'
FROM Sales.orders ord
JOIN sales.customers cus
ON ord.customer_id = cus.customer_id
JOIN sales.order_items ite
ON ord.order_id = ite.order_id
JOIN production.products pro
ON ite.product_id = pro.product_id
JOIN production.categories cat
ON pro.category_id = cat.category_id
JOIN sales.stores sto
ON ord.store_id = sto.store_id
JOIN sales.staffs sta
ON ord.staff_id = sta.staff_id
GROUP BY ord.order_id,
	   concat(cus.first_name, '  ', cus.last_name),
	   cus.city,
	   cus.state,
	   ord.order_date,
	   pro.product_name,
	   cat.category_name,
	   sto.store_name,
	  CONCAT(sta.first_name, '  ', sta.last_name)
ORDER by ord.order_id
```
This helped me to generate the query


## Data Cleaning
The data was clean on inspection and as such there was no need for data cleaning and transformation


## Insights

- From the dashboard, the company had an overall revenue of $ 8.5 million in the 3 years of the company’s operation. With 2017 being the year the company generated the highest revenue. Also, The state of New York generated the highest revenue for the company in 3 years altogether.

- The company had a 41.93% growth in revenue from sales of Bikes in 4 states however the company had a whopping 47% revenue decline in 2018 compared to the previous year.

- There was 0.18% growth in revenue in California in 2017 8 while the same California experienced a 15% decline in revenue in 2018

- New York which had the highest number of sales in 2017 and 2018 had a 55% increase in revenue in 2017 but unfortunately made a loss of revenue in 2018 which was about 52%

- While Texas had a 50.62 increase in revenue in 2017 but unfortunately had a loss of 52% in revenue in 2018


- Overall the company has experienced a decline in revenue which can be attributed to many factors among another thing might be because of the competitive nature of the business
   The market seemed competitive 


- Despite more sales in California, the state appears to have made less revenue yield year on compared to Texas


### Why was there a drop in revenue despite more sales in California compared to Texas?
It appears as if the company has reached its saturating point in the state of California and as such there is not too much room for growth compared to a state like Texas and New York

## Recommendation

- Revisit the employer’s database to visualize records of sales within the company
  This could reveal more insight into what could have happened 

- The company should consider expanding operations in Texas to get more volume of sales to increase revenue


