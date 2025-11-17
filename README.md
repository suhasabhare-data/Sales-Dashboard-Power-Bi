# 📊 Sales Dashboard Powe Bi Project
This repository provides a step-by-step approach to creating a comprehensive sales analysis dashboard that visualizes key performance indicators (KPIs), sales trends, and comparative analysis using Power BI.

[Sale Dashboard Report](https://github.com/suhasabhare-data/Sales-Dashboard-Power-Bi/blob/main/Sales%20Dashboard.pbix)

## 🌟 Project Overview

This project showcases the creation of a dynamic and interactive Sales & Profit Dashboard using **Power BI**. The goal is to provide comprehensive financial and sales performance insights through advanced data modeling, DAX calculations, and intuitive visualizations.

## ✨ Project Objectives

* Calculate and visualize key metrics: **Total Sales, Profit, Orders, and Profit Margin**.
* Compare **Year-Over-Year (YoY)** sales and profit performance by product, month, and sales channel.
* Analyze sales performance by **customer** and highlight **top-performing locations**.
* Create dynamic, interactive dashboards with slicers for user-friendly filtering by **Date, City, Product, and Channel**.

## 🚀 Key Features

* **Total Sales Calculation:** A complete sales overview for the selected period.
* **Profit and Profit Margin Analysis:** Visualizations of financial performance.
* **Year-Over-Year Comparisons:** Insights into product performance and monthly trends.
* **Top 5 Cities Analysis:** Highlights the most lucrative locations for focused marketing.
* **Customer Sales Analysis:** Detailed customer-level insights.
* **Dynamic Slicers:** Filters for personalized data interaction and drill-down analysis.

## 🛠️ Skills Demonstrated

* **Power BI Reporting & Visualization**
* **Data Cleaning & Preparation** (using Power Query)
* **Data Modeling & Relationship Building**
* **DAX Calculations** (Measures and Calculated Columns)
* **Sales & Profit Analysis**

---

## 🏗️ Steps Followed to Create the Dashboard

### 1. Gather Data
* **Source:** Sample sales data provided in **Excel** format.

### 2. Power Query – Data Extract, Transform & Load (ETL)
* The **Power Query Editor** in Power BI was used for data cleaning and transformation to make the data suitable for analysis.
* This involved:
    * Removing duplicates.
    * Handling missing values.
    * Merging datasets (if applicable).
    * Creating calculated columns for immediate use.

### 3. Create a Date Table
* A dedicated **Date Table** was created as a prerequisite for utilizing **DAX Time Intelligence functions** for accurate YoY comparisons.

### 4. Create Data Model
* A data model was designed to represent relationships between the tables, define keys, and establish hierarchies for accurate, robust, and efficient analysis.

### 5. Develop Reports
* Interactive reports were built in **Power BI Desktop** using various visualizations (charts, tables, maps).
* **Slicers** were implemented for **Date, City, Product, and Channel**.
* Key Visualizations developed:
    * Sales by Product (YoY comparison)
    * Sales by Month (YoY comparison)
    * Top 5 Cities by Sales
    * Profit by Channel (YoY comparison)
    * Sales by Customer (YoY comparison)
    * Key Metrics Card (Sales, Profit, Profit Margin, Products Sold)

---

## 🔢 DAX Calculations Implemented

The following Data Analysis Expressions (DAX) were used to create measures for advanced financial and time-intelligence calculations:

| Measure Name | DAX Formula | Purpose |
| :--- | :--- | :--- |
| **Sales** | `SUM(Sales_Data[Sales])` | Total sales for the selected context. |
| **Sales PY** | `CALCULATE([Sales], SAMEPERIODLASTYEAR(DateTable[Date]))` | Sales for the Prior Year. |
| **Sales vs PY** | `[Sales] - [Sales PY]` | Absolute variance between current sales and prior year sales. |
| **Sales vs PY %** | `DIVIDE([Sales vs PY], [Sales], 0)` | Percentage variance in sales (YoY). |
| **Profit** | `SUM(Sales_Data[Profit])` | Total profit for the selected context. |
| **Profit LY** | `CALCULATE([Profit], SAMEPERIODLASTYEAR(DateTable[Date]))` | Profit for the Last Year. |
| **Profit vs LY** | `[Profit] - [Profit LY]` | Absolute variance between current profit and last year profit. |
| **Profit vs LY %** | `[Profit vs LY] / [Profit]` | Percentage variance in profit (YoY). |
| **Profit Margin** | `DIVIDE([Profit], [Sales], 0)` | Ratio of profit to sales. |

---

## 📅 Creating a Simple Date Table (DAX Formula)

This is the DAX code used to generate the necessary Date Table with relevant time hierarchy columns:

```dax
DateTable = 
ADDCOLUMNS (
    CALENDARAUTO(), // Automatically determines the date range based on all dates in the data model
    "Year", YEAR([Date]),
    "Quarter", "Q" & FORMAT(CEILING(MONTH([Date])/3, 1), "#"),
    "Quarter No", CEILING(MONTH([Date])/3, 1),
    "Month No", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Month Short Name", FORMAT([Date], "MMM"),
    "Month Short Name Plus Year", FORMAT([Date], "MMM,yy"),
    "DateSort", FORMAT([Date], "yyyyMMdd"),
    "Day Name", FORMAT([Date], "dddd"),
    "Details", FORMAT([Date], "dd-MMM-yyyy"),
    "Day Number", DAY([Date])
)
