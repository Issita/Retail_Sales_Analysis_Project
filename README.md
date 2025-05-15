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
