# home_sales

This project focused on the utilization of Big Data tools, specifically SparkSQL, to conduct in-depth analysis of residential property sales records. Here's a summary of the workflow and methodologies applied:

Package Integration:
Initiated the process by integrating essential libraries such as findspark for Spark initialization and pyspark.sql to leverage SparkSQL's capabilities.

Establishing Spark Connection:
A SparkSession was established with SparkSession.builder.appName("SparkSQL").getOrCreate() to interface with the Spark engine.

Data Ingestion:
Residential sales data was ingested into a DataFrame directly from an S3 bucket utilizing the respective URL.

Data Framing for SQL Operations:
A temporary SQL-accessible view named "my_table" was constructed from the DataFrame using the createOrReplaceTempView() function, facilitating the execution of SQL commands on the data.

Data Exploration Through SQL:
Performed a series of SQL queries to derive insights, such as determining the mean sales price for four-bedroom houses annually and computing the average value of properties contingent upon attributes like the number of bedrooms, bathrooms, and total area.

Optimizing with Caching:
To enhance query efficiency, the DataFrame "home_sales_df" was cached via spark.catalog.cacheTable(), allowing recurrent queries to draw data from memory rather than re-reading from disk.

Performance Benchmarking:
The execution time of a particular SQL query was benchmarked by capturing timestamps before and after its run, comparing the performance with cached data against that sourced from Parquet files.

Data Serialization to Parquet:
Transformed the home sales data into a partitioned Parquet format, stratified by the "date_built" attribute using the partitionBy().parquet() sequence.

Parquet Data Retrieval:
Accessed the Parquet-stored data, bringing it into a DataFrame to continue our analysis.

Establishing a Parquet Data View:
A temporary view titled "parquet_table" was constructed for the Parquet DataFrame to permit SQL queries, using the createOrReplaceTempView() procedure.

Analyzing Parquet Data:
Ran SQL queries on the Parquet DataFrame, specifically filtering to identify homes with view ratings and an average price threshold of $350,000 or more, with performance times measured for comparison against the cached data.

Data Uncaching:
Post-analysis, the "home_sales" table was uncached through spark.catalog.uncacheTable(), thus liberating memory resources.

Verifying Cache Status:
Finally, confirmed the caching status of the "home_sales" table using spark.catalog.isCached() to ensure it was no longer stored in memory.

In summary, the project adeptly demonstrated how SparkSQL can be harnessed to read, process, cache, and analyze vast datasets, offering valuable insights on property prices based on a variety of housing characteristics.





