# Retail_Sales_Analysis_Project
**Project Title:** Retail Sales Analysis
**Database:** PROJECTS
**Table:** RETAIL_SALES

## Objectives

* **Retail Sales Database Setup:** Create and populate a structured database using the provided retail sales data.
* **Data Cleaning:** Identify and remove records containing missing or null values to ensure clean and reliable analysis.
* **Exploratory Data Analysis (EDA):** Perform SQL-based exploration to understand trends, patterns, and distributions in the dataset.
* **Business Insights:** Write SQL queries to answer key business questions and extract meaningful insights that can support decision-making.

##  Data Exploration & Cleaning
* **Record Count:** Count the total number of records in the dataset.
* **Customer Distinct Count:** Find out how many unique customers are in the dataset.
* **Category Count:** Identify all unique product categories in the dataset.
* **Null Value Check:** Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) AS TOTAL_SALES FROM RETAIL_SALES;
SELECT COUNT(DISTINCT customer_id)AS UNIQUE_CUSTOMER_NUMBER FROM RETAIL_SALES;
SELECT DISTINCT CATEGORY FROM RETAIL_SALES;

SELECT * FROM RETAIL_SALES
WHERE transactions_id IS NULL
	OR
	sale_date IS NULL
	OR
	sale_time IS NULL
	OR
	customer_id IS NULL
	OR
	gender IS NULL
	OR
	age IS NULL	
	OR
	category IS NULL
	OR
	quantiy	IS NULL
	OR
	price_per_unit IS NULL
	OR
	cogs IS NULL
	OR
	total_sale IS NULL;

-- DELETING THE NULL RECORDS FROM THE TABLE

DELETE FROM RETAIL_SALES
WHERE transactions_id IS NULL
	OR
	sale_date IS NULL
	OR
	sale_time IS NULL
	OR
	customer_id IS NULL
	OR
	gender IS NULL
	OR
	age IS NULL	
	OR
	category IS NULL
	OR
	quantiy	IS NULL
	OR
	price_per_unit IS NULL
	OR
	cogs IS NULL
	OR
	total_sale IS NULL;
```
## Data Analysis & Business Key Problems & Answers

**Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05**

```sql
SELECT * FROM RETAIL_SALES
WHERE sale_date = '2022-11-05';
```

**Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**

```sql
SELECT *
	--FORMAT(sale_date,'yyyy-MM') AS YEAR_MONTH
FROM RETAIL_SALES
WHERE category ='Clothing'
	AND
	quantiy >= 4
	AND
	FORMAT(sale_date,'yyyy-MM') = '2022-11';
```

**Q.3 Write a SQL query to calculate the total sales (total_sale) and total_orders for each category.**

```sql
SELECT 
CATEGORY,
SUM(TOTAL_SALE) AS NET_SALES,
COUNT(*) AS TOTAL_ORDRES
FROM RETAIL_SALES
GROUP BY category;
```
**Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**

```sql
SELECT 
AVG(AGE) AS AVG_AGE
FROM RETAIL_SALES
WHERE category = 'Beauty';
```
**Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.**

```sql
SELECT * FROM RETAIL_SALES
WHERE total_sale > 1000;
```
**Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**

```sql
SELECT 
category,
gender,
COUNT(*) AS TOTAL_TRANSACTION
FROM RETAIL_SALES
GROUP BY category,gender;
```
**Q.7 Write a SQL query to calculate the average sale for each month. Find out best selling month in each year.**

```sql
WITH AVG_TBL AS ( 
				SELECT 
					YEAR(sale_date) AS YEAR,
					MONTH(sale_date) AS MONTH,
					AVG(total_sale) AS AVG_SALE,
					RANK()OVER(PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS RANKING
				FROM RETAIL_SALES
				GROUP BY YEAR(sale_date), MONTH(sale_date) 
				)
SELECT
YEAR,
MONTH,
AVG_SALE
FROM AVG_TBL
WHERE RANKING = 1;
```
**Q.8 Write a SQL query to find the top 5 customers based on the highest total sales** 

```sql
SELECT TOP 5
customer_id,
SUM(total_sale) AS TOTAL_SALES
FROM RETAIL_SALES
GROUP BY customer_id
ORDER BY SUM(total_sale) DESC


--ANOTHER METHOD

SELECT 
customer_id,
SUM(total_sale) AS TOTAL_SALES
FROM RETAIL_SALES
GROUP BY customer_id
ORDER BY SUM(total_sale) DESC
OFFSET 0 ROWS
FETCH NEXT 5 ROWS ONLY;
```

**Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.**

```sql
SELECT 
category,
COUNT(DISTINCT  customer_id) AS UNIQUE_NUMBER_CUSTOMER
FROM RETAIL_SALES
GROUP BY category;
```

**Q.10 Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**

```sql
WITH HOURLY_SALES AS(
				SELECT *,
					case
						when datepart(HOUR, sale_time)  < 12 then 'Morning'
						when datepart(HOUR, sale_time) between 12 and 17 then 'Afternoon'
						else 'Evening'
					end as shift
				FROM RETAIL_SALES
				)
SELECT
shift,
COUNT(*) AS NO_OF_ORDERS
FROM HOURLY_SALES
GROUP BY shift;
```

## Findings

- **Customer Demographics:** The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions:** Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends:** Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights:** The analysis identifies the top-spending customers and the most popular product categories.
