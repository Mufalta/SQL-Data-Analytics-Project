# SQL-Data-Analytics-Project

Hi 👋, good to see you again, welcome to the **Data Analytics Project** repository!  
First of all, a huge thanks to **Baraa Khatib Salkini** for inspiring me to build this project about Data Analytics. This project continues the Data Warehouse project, so please check the repository by [clicking here](https://github.com/Mufalta/SQL-Data-Warehouse-Project.git).  
On this page, we're going to dive into a thorough analysis to find some business insights from organized data in the data warehouse.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [What is Data Analytics](#what-is-data-analytics)
3. [Create Database and Schema](#create-database-and-schema)

---

## Project Overview

This project involves:
1. **Exploratory Data Analysis (EDA):** to explore and understand the structure, dimensions, and patterns within the data.
2. **Advanced Analytics:** to generate insights, track performance, and support decision-making using the organized data.

---

## What is Data Analytics

It's essential to understand what data analytics really is. Look at the image below:  
![](https://github.com/Mufalta/SQL-Data-Analytics-Project/blob/main/images/Data-Analytics.png)

---

## Create Database and Schema

The first thing we're going to do is create a database named 'DataWarehouseAnalytics' after checking if it already exists. If the database exists, it is dropped and recreated. Additionally, we create a schema called gold.  
```
USE master;
GO

-- Drop and recreate the 'DataWarehouseAnalytics' database
IF EXISTS (SELECT 1 FROM sys.databases WHERE name = 'DataWarehouseAnalytics')
BEGIN
    ALTER DATABASE DataWarehouseAnalytics SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
    DROP DATABASE DataWarehouseAnalytics;
END;
GO

-- Create the 'DataWarehouseAnalytics' database
CREATE DATABASE DataWarehouseAnalytics;
GO

USE DataWarehouseAnalytics;
GO

-- Create Schemas

CREATE SCHEMA gold;
GO

CREATE TABLE gold.dim_customers(
	customer_key int,
	customer_id int,
	customer_number nvarchar(50),
	first_name nvarchar(50),
	last_name nvarchar(50),
	country nvarchar(50),
	marital_status nvarchar(50),
	gender nvarchar(50),
	birthdate date,
	create_date date
);
GO

CREATE TABLE gold.dim_products(
	product_key int ,
	product_id int ,
	product_number nvarchar(50) ,
	product_name nvarchar(50) ,
	category_id nvarchar(50) ,
	category nvarchar(50) ,
	subcategory nvarchar(50) ,
	maintenance nvarchar(50) ,
	cost int,
	product_line nvarchar(50),
	start_date date 
);
GO

CREATE TABLE gold.fact_sales(
	order_number nvarchar(50),
	product_key int,
	customer_key int,
	order_date date,
	shipping_date date,
	due_date date,
	sales_amount int,
	quantity tinyint,
	price int 
);
GO

TRUNCATE TABLE gold.dim_customers;
GO

BULK INSERT gold.dim_customers
FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_customers.csv'
WITH (
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
GO

TRUNCATE TABLE gold.dim_products;
GO

BULK INSERT gold.dim_products
FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.dim_products.csv'
WITH (
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
GO

TRUNCATE TABLE gold.fact_sales;
GO

BULK INSERT gold.fact_sales
FROM 'C:\sql\sql-data-analytics-project\datasets\csv-files\gold.fact_sales.csv'
WITH (
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
GO
```

