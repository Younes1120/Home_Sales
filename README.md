# Home Sales Data Analysis using SparkSQL

## Overview

This project focuses on analyzing home sales data using Apache Spark and SparkSQL. The primary objective is to gain valuable insights into average home prices based on various criteria, such as bedrooms, bathrooms, square footage, and construction year. Additionally, caching techniques are employed to optimize query performance, and the analysis includes a comparison of runtime between cached and uncached versions.

## Project Steps

1. **Importing Packages:** The project starts by importing essential packages, including `findspark` for initializing Spark and `pyspark.sql` for SparkSQL operations.

2. **Creating a SparkSession:** A SparkSession is created using `SparkSession.builder.appName("SparkSQL").getOrCreate()` to establish a connection to Spark, enabling SparkSQL functionalities.

3. **Reading Data:** The home sales data is read from an AWS S3 bucket into a DataFrame using the provided URL. This DataFrame serves as the foundation for all subsequent analysis.

4. **Creating a Temporary View:** A temporary view named "my_table" is created for the DataFrame using `createOrReplaceTempView()` method. This allows running SQL queries on the DataFrame as if it were a database table.

5. **Data Analysis:** Several SQL queries are executed to analyze the home sales data. Key metrics, such as the average price for a four-bedroom house sold in each year and the average price of homes based on different criteria, are calculated.

6. **Caching for Performance:** To optimize query execution, the temporary table "home_sales_df" is cached using `spark.catalog.cacheTable()` method. Caching stores the data in memory, reducing disk read overhead during subsequent queries.

7. **Query Runtime Comparison:** The runtime of a specific query is compared between the cached and uncached versions. The start time is recorded using `time.time()` before executing each query, and the time difference is calculated to measure the query's runtime performance.

8. **Writing Parquet Data:** The formatted home sales data is written to Parquet format with partitioning based on the "date_built" field using the `partitionBy().parquet()` method. Parquet's columnar storage format optimizes data storage and retrieval efficiency.

9. **Reading Parquet Data:** The Parquet data is read into a DataFrame for further analysis.

10. **Creating a Temporary Table for Parquet Data:** A temporary table named "parquet_table" is created for the Parquet DataFrame using `createOrReplaceTempView()` method. This facilitates SQL-based querying on the Parquet data.

11. **Querying Parquet Data:** SQL queries are executed on the Parquet DataFrame to filter view ratings with an average price greater than or equal to $350,000. The runtime is measured and compared to the cached version, evaluating the impact of caching on Parquet data.

12. **Uncaching the Temporary Table:** The temporary table "home_sales" is uncached using `spark.catalog.uncacheTable()` method to release memory resources after completing the analysis.

13. **Checking Caching Status:** The caching status of the table "home_sales" is checked using `spark.catalog.isCached()` method to confirm whether it is still cached or not.

## Conclusion

This project demonstrates the effective use of SparkSQL to analyze and query home sales data. By leveraging Apache Spark's distributed computing capabilities and caching features, we achieve efficient data processing and analysis on large-scale datasets. The analysis provides valuable insights into average home prices across various attributes, enabling stakeholders to make informed decisions. Moreover, the adoption of the Parquet format further enhances data storage and retrieval efficiency. The findings from this project can be instrumental in understanding market trends and making data-driven decisions in the real estate domain.

