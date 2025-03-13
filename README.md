# Home Sales Analysis using PySpark

## Overview

This project analyzes home sales data using **Apache Spark (PySpark)** to process large datasets efficiently. The analysis covers key aspects such as average home prices based on different criteria, caching performance comparisons, and partitioned data optimization.

## Technologies Used

- **Python (Jupyter Notebook / Google Colab)**
- **Apache Spark (PySpark)**
- **SQL (SparkSQL)**

## Objectives

1. **Load and process home sales data** using Google Colab and PySpark.
2. **Create a temporary table (`home_sales`)** to run SQL queries on the dataset.
3. **Perform data analysis** to answer key real estate questions using SparkSQL:
   - Average home prices for four-bedroom homes by year.
   - Average price of homes built in different years with 3 beds, 3 baths.
   - Price comparison for homes meeting specific size and floor requirements.
   - Effect of `view` rating on home prices.
4. **Optimize query performance** through:
   - **Caching (`cacheTable`)**: Improve query efficiency by storing intermediate results in memory.
   - **Partitioning (`partitionBy`)**: Organizing data for faster access based on `date_built`.
5. **Compare performance metrics** of uncached, cached, and partitioned queries.
6. **Uncache and verify the `home_sales` temporary table.**

## Requirements

### **DataFrame Creation & SQL Processing**

- A **Spark DataFrame** is created from the dataset.
- A **temporary table** of the original DataFrame is created.
- Queries written to compute:
  - **Average price of four-bedroom homes by year**
  - **Average price of 3-bed, 3-bath homes per build year**
  - **Average price of 3-bed, 3-bath, 2-floor homes ≥2000 sqft per build year**
  - **Average price per `view` rating where avg price ≥ $350,000** (includes run time)

### **Optimization & Performance Analysis**

- **Caching (`cacheTable`) is implemented and verified.**
- The **query on `view` ratings is run on the cached table**, and run time is computed.
- **Partitioning by `date_built`** is applied, and data is read as Parquet.
- A **temporary table of the Parquet data** is created.
- The **query on `view` ratings is run on the partitioned table**, and run time is computed.

### **Final Step**

- The **temporary `home_sales` table is uncached and verified.**

## Steps Performed

### 1. Data Loading

- Imported required PySpark SQL functions.
- Uploaded `home_sales_revised.csv` directly into Google Colab and read it into a PySpark DataFrame.
- Created a **temporary SQL table (`home_sales`)**.

### 2. Data Analysis with SparkSQL

- Computed **average home prices** based on various conditions using SQL queries.
- Utilized **SparkSQL functions (`ROUND()`, `AVG()`, `GROUP BY`)** to derive insights.

### 3. Performance Optimization

#### **Caching for Faster Queries**

- Used `spark.catalog.cacheTable("home_sales")` to cache the dataset.
- Checked caching with `spark.catalog.isCached("home_sales")`.
- Compared the execution time of cached vs. uncached queries.

#### **Partitioning for Improved Performance**

- Partitioned data by `date_built` using:
  ```python
  df.write.partitionBy("date_built").parquet("home_sales_partitioned", mode="overwrite")
  ```
- Read the partitioned Parquet data into a DataFrame and created a new temporary table.
- Reran key queries on the **partitioned** dataset and compared execution time.

### 4. Final Step: Uncaching and Verification

- The `home_sales` temporary table was uncached and checked for successful removal.

## Conclusion

This project demonstrates how **PySpark and SparkSQL** can be used to efficiently analyze large real estate datasets. By leveraging **caching** and **partitioning**, query performance was significantly improved, making this approach ideal for big data analytics.

## Acknowledgments

- **Apache Spark** for distributed data processing.
- **Google Colab** for hosting and running the notebook.

---

**Note:** This project is intended for educational purposes in demonstrating PySpark capabilities for real estate analytics.

