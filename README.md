# Retail Sales Analysis — SQL Project

## Project Overview
This project demonstrates end-to-end SQL data analysis skills using **MySQL**, covering database setup, data cleaning, exploratory data analysis (EDA), and solving real-world business questions on a retail sales dataset.

* **Database:** `sql_project_p1`
* **Dialect:** MySQL
* **Dataset Size:** 2,000 raw records (1,997 valid records after data cleaning)

---

## Objectives
1. **Database Setup:** Create and populate a structured relational database table (`retail_sales`) for retail transaction records.
2. **Data Cleaning:** Identify and remove records with missing (`NULL`) values in critical transactional fields while preserving rows with partial demographic info (`age`).
3. **Exploratory Data Analysis (EDA):** Understand dataset volume, customer reach, and product category distribution.
4. **Business Intelligence:** Write analytical SQL queries using aggregations, date/time functions, conditional logic (`CASE`), Common Table Expressions (CTEs), and window functions (`RANK()`) to answer 10 key business questions.

---

## Database Schema

```sql
CREATE DATABASE IF NOT EXISTS sql_project_p1;
USE sql_project_p1;

CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit DECIMAL(10, 2),
    cogs DECIMAL(10, 2),
    total_sale DECIMAL(10, 2)
);
```

---

## Workflow & SQL Implementation

### 1. Data Cleaning
* Checked for `NULL` values across all critical transactional columns (`transactions_id`, `sale_date`, `sale_time`, `customer_id`, `gender`, `category`, `quantity`, `price_per_unit`, `cogs`, `total_sale`).
* Removed **3 incomplete records** (`transactions_id` 679, 746, and 1225) with missing sales metrics, retaining **1,997 clean records**.

### 2. Exploratory Data Analysis (EDA)
* **Total Transactions:** `1,997`
* **Unique Customers:** `155`
* **Product Categories:** `Beauty`, `Clothing`, `Electronics`

### 3. Business Key Questions Answered
1. **Daily Sales Snapshot:** Retrieve all sales transactions made on `'2022-11-05'`.
2. **High-Volume Clothing Orders:** Filter `'Clothing'` transactions with `quantity > 4` during `November 2022`.
3. **Category Revenue & Order Volume:** Calculate net sales (`SUM(total_sale)`) and total order count per product category.
4. **Customer Demographics by Category:** Compute the average customer age (`ROUND(AVG(age), 2)`) for the `'Beauty'` category.
5. **High-Value Transactions:** Identify all orders where `total_sale > 1000`.
6. **Gender & Category Breakdown:** Count total transactions grouped by `category` and `gender`.
7. **Best-Selling Month per Year:** Use `EXTRACT()` and the `RANK()` window function partitioned by year to find the month with the highest average sale in each year.
8. **Top 5 Customers:** Rank the top 5 customers by cumulative spending (`SUM(total_sale)`).
9. **Category Customer Reach:** Count distinct customers (`COUNT(DISTINCT customer_id)`) purchasing from each category.
10. **Order Volume by Time Shift:** Categorize orders into **Morning** (`< 12:00`), **Afternoon** (`12:00–17:00`), and **Evening** (`> 17:00`) using a CTE and `CASE` statement to compare order distribution across shifts.

---

## How to Run This Project
1. Clone this repository or download `PROJECT.sql` and the dataset CSV file.
2. Open **MySQL Workbench** and connect to your local MySQL server.
3. Run Section 1 (`CREATE DATABASE` and `CREATE TABLE`) in `PROJECT.sql`.
4. Import the dataset CSV into the `retail_sales` table using the **Table Data Import Wizard**.
5. Execute Sections 2, 3, and 4 to clean the data and generate all analytical outputs.

---

## Key SQL Concepts Used
* **DDL & DML:** `CREATE DATABASE`, `CREATE TABLE`, `DELETE`
* **Filtering & Aggregation:** `WHERE`, `GROUP BY`, `ORDER BY`, `LIMIT`, `COUNT`, `SUM`, `AVG`, `ROUND`, `DISTINCT`
* **Date & Time Functions:** `DATE_FORMAT()`, `EXTRACT(YEAR / MONTH / HOUR FROM ...)`
* **Advanced SQL:** Common Table Expressions (`WITH`), Window Functions (`RANK() OVER (PARTITION BY ... ORDER BY ...)`), Conditional Logic (`CASE WHEN`)

