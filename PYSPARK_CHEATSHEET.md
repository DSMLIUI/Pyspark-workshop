# PySpark Quick Reference Cheat Sheet

## Essential Imports

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.types import *
from pyspark.sql.window import Window
```

---

## Creating SparkSession

```python
# In Databricks, spark is already available
spark.version

# For local/standalone setup
spark = SparkSession.builder \
    .appName("MyApp") \
    .config("spark.driver.memory", "4g") \
    .getOrCreate()
```

---

## Reading Data

```python
# Parquet (recommended)
df = spark.read.parquet("path/to/file.parquet")

# CSV
df = spark.read.csv("path/to/file.csv", header=True, inferSchema=True)

# JSON
df = spark.read.json("path/to/file.json")

# With explicit schema
schema = StructType([
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])
df = spark.read.schema(schema).csv("path/to/file.csv")

# Delta Lake
df = spark.read.format("delta").load("path/to/delta")
```

---

## Writing Data

```python
# Parquet
df.write.mode("overwrite").parquet("path/to/output")

# CSV
df.write.mode("append").csv("path/to/output", header=True)

# Partitioned write
df.write.partitionBy("year", "month").parquet("path/to/output")

# Delta Lake
df.write.format("delta").mode("overwrite").save("path/to/delta")
```

---

## DataFrame Basics

```python
# Show data
df.show(10)                    # Show 10 rows
df.show(10, truncate=False)    # Don't truncate long strings

# Schema
df.printSchema()               # Print schema tree
df.columns                     # List column names
df.dtypes                      # List columns with types

# Basic info
df.count()                     # Count rows (action)
df.rdd.getNumPartitions()     # Number of partitions

# Statistics
df.describe().show()           # Summary statistics
df.summary().show()            # Extended statistics
```

---

## Selecting & Filtering

```python
# Select columns
df.select("col1", "col2")
df.select(col("col1"), col("col2"))
df.select(df.col1, df["col2"])

# Filter rows
df.filter(col("age") > 25)
df.where(col("age") > 25)      # Same as filter

# Multiple conditions
df.filter((col("age") > 25) & (col("city") == "NYC"))
df.filter((col("age") < 18) | (col("age") > 65))

# Filter with SQL expression
df.filter("age > 25 AND city = 'NYC'")

# Drop columns
df.drop("col1", "col2")

# Distinct
df.distinct()
df.dropDuplicates(["col1"])
```

---

## Adding & Modifying Columns

```python
# Add new column
df.withColumn("new_col", lit(100))
df.withColumn("age_plus_10", col("age") + 10)

# Rename column
df.withColumnRenamed("old_name", "new_name")

# Conditional column
df.withColumn("category",
    when(col("age") < 18, "minor")
    .when(col("age") < 65, "adult")
    .otherwise("senior")
)

# Cast column type
df.withColumn("age", col("age").cast("integer"))
df.withColumn("price", col("price").cast(DoubleType()))
```

---

## Aggregations

```python
# Basic aggregations
df.count()
df.select(avg("price"), sum("quantity"), max("score")).show()

# Group by
df.groupBy("category").count()
df.groupBy("category").agg(
    count("*").alias("count"),
    avg("price").alias("avg_price"),
    sum("quantity").alias("total_qty"),
    max("score").alias("max_score"),
    min("score").alias("min_score")
)

# Multiple group by columns
df.groupBy("category", "region").agg(sum("sales"))

# Pivot
df.groupBy("year").pivot("category").sum("sales")
```

---

## Joins

```python
# Inner join (default)
df1.join(df2, df1.id == df2.id)
df1.join(df2, "id")  # When column name is same

# Left outer join
df1.join(df2, "id", "left")

# Right outer join
df1.join(df2, "id", "right")

# Full outer join
df1.join(df2, "id", "full")

# Cross join
df1.crossJoin(df2)

# Broadcast join (for small tables)
from pyspark.sql.functions import broadcast
df1.join(broadcast(df2), "id")
```

---

## Window Functions

```python
from pyspark.sql.window import Window

# Define window
window = Window.partitionBy("category").orderBy("date")

# Running total
df.withColumn("running_total", sum("amount").over(window))

# Row number
df.withColumn("row_num", row_number().over(window))

# Rank
df.withColumn("rank", rank().over(window))
df.withColumn("dense_rank", dense_rank().over(window))

# Lead/Lag
df.withColumn("prev_value", lag("value", 1).over(window))
df.withColumn("next_value", lead("value", 1).over(window))

# Moving average (last 3 rows)
window_rows = Window.partitionBy("id").orderBy("date").rowsBetween(-2, 0)
df.withColumn("moving_avg", avg("value").over(window_rows))
```

---

## Common Functions

```python
# String functions
col("name").substr(1, 3)           # Substring
col("name").lower()                 # Lowercase
col("name").upper()                 # Uppercase
col("email").contains("@gmail")     # Contains
col("text").startswith("A")         # Starts with
concat(col("first"), lit(" "), col("last"))  # Concatenate
split(col("text"), " ")             # Split string
length(col("name"))                 # String length
trim(col("name"))                   # Trim whitespace
regexp_replace(col("phone"), "[^0-9]", "")  # Regex replace

# Numeric functions
round(col("price"), 2)              # Round
abs(col("value"))                   # Absolute value
sqrt(col("value"))                  # Square root
col("a") + col("b")                 # Addition
col("a") - col("b")                 # Subtraction
col("a") * col("b")                 # Multiplication
col("a") / col("b")                 # Division

# Date/Time functions
current_date()                      # Current date
current_timestamp()                 # Current timestamp
year(col("date"))                   # Extract year
month(col("date"))                  # Extract month
dayofmonth(col("date"))            # Extract day
dayofweek(col("date"))             # Day of week (1=Sunday)
hour(col("timestamp"))              # Extract hour
minute(col("timestamp"))            # Extract minute
date_add(col("date"), 7)           # Add days
date_sub(col("date"), 7)           # Subtract days
datediff(col("end"), col("start")) # Difference in days
to_date(col("string"), "yyyy-MM-dd")  # Parse date
date_format(col("date"), "yyyy-MM-dd") # Format date

# Null handling
col("value").isNull()               # Check if null
col("value").isNotNull()           # Check if not null
coalesce(col("a"), col("b"), lit(0))  # First non-null
fillna(0)                           # Fill nulls
df.na.drop()                        # Drop rows with nulls
df.na.fill({"col1": 0, "col2": ""}) # Fill specific columns
```

---

## SQL Queries

```python
# Register DataFrame as temp view
df.createOrReplaceTempView("my_table")

# Run SQL query
result = spark.sql("""
    SELECT category, COUNT(*) as count, AVG(price) as avg_price
    FROM my_table
    WHERE price > 100
    GROUP BY category
    ORDER BY count DESC
""")
```

---

## Performance Optimization

```python
# Cache DataFrame
df.cache()
df.persist()  # Same as cache
df.unpersist()  # Remove from cache

# Repartition
df.repartition(10)              # 10 partitions
df.repartition(10, "col_name")  # Partition by column
df.coalesce(1)                  # Reduce partitions (no shuffle)

# Broadcast small tables
from pyspark.sql.functions import broadcast
large_df.join(broadcast(small_df), "id")

# Show execution plan
df.explain()
df.explain(extended=True)
```

---

## Machine Learning

```python
from pyspark.ml.feature import VectorAssembler, StringIndexer
from pyspark.ml.regression import LinearRegression
from pyspark.ml.classification import RandomForestClassifier
from pyspark.ml.evaluation import RegressionEvaluator

# Feature engineering
assembler = VectorAssembler(
    inputCols=["feature1", "feature2"],
    outputCol="features"
)
df_vectorized = assembler.transform(df)

# String indexing
indexer = StringIndexer(inputCol="category", outputCol="category_index")
indexer_model = indexer.fit(df)
df_indexed = indexer_model.transform(df)

# Train model
train_df, test_df = df.randomSplit([0.8, 0.2])
lr = LinearRegression(featuresCol="features", labelCol="label")
model = lr.fit(train_df)

# Predictions
predictions = model.transform(test_df)

# Evaluation
evaluator = RegressionEvaluator(metricName="rmse")
rmse = evaluator.evaluate(predictions)
```

---

## Structured Streaming

```python
# Read stream
streaming_df = spark.readStream \
    .format("csv") \
    .schema(schema) \
    .option("maxFilesPerTrigger", 1) \
    .load("path/to/streaming/input")

# Transformations (same as batch)
result = streaming_df.filter(col("value") > 100) \
    .groupBy("category").count()

# Write stream
query = result.writeStream \
    .outputMode("update") \
    .format("console") \
    .start()

# With watermarking
result = streaming_df \
    .withWatermark("timestamp", "10 minutes") \
    .groupBy(window(col("timestamp"), "1 minute")) \
    .count()

# Manage query
query.stop()
query.awaitTermination()
query.status
```

---

## Delta Lake

```python
# Read Delta table
df = spark.read.format("delta").load("path/to/delta")

# Write Delta table
df.write.format("delta").mode("overwrite").save("path/to/delta")

# Time travel
df = spark.read.format("delta").option("versionAsOf", 0).load("path")
df = spark.read.format("delta").option("timestampAsOf", "2024-01-01").load("path")

# Optimize
spark.sql("OPTIMIZE delta.`path/to/delta`")

# Vacuum (remove old files)
spark.sql("VACUUM delta.`path/to/delta` RETAIN 168 HOURS")

# Z-ordering
spark.sql("OPTIMIZE delta.`path/to/delta` ZORDER BY (col1, col2)")
```

---

## Common Patterns

```python
# Count distinct
df.select(countDistinct("user_id")).show()

# Collect to driver (careful with large data!)
rows = df.collect()
first_row = df.first()
sample_rows = df.take(10)

# Convert to Pandas (small data only!)
pandas_df = df.toPandas()

# From Pandas to Spark
spark_df = spark.createDataFrame(pandas_df)

# Handle nested data
df.select(col("address.city"), col("address.zipcode"))
df.select(explode(col("array_column")))

# Union DataFrames
df1.union(df2)
df1.unionByName(df2)  # Match by column name
```

---

## Debugging Tips

```python
# Check execution plan
df.explain()

# Check partitions
print(df.rdd.getNumPartitions())

# Sample data for testing
df.sample(0.1).show()  # 10% sample

# Get first N rows as list
df.head(10)

# Check for nulls
df.select([count(when(col(c).isNull(), c)).alias(c) for c in df.columns]).show()
```

---

## Quick Tips

1. **Transformations are lazy** - Nothing happens until an action
2. **Actions trigger execution** - `.count()`, `.show()`, `.collect()`, `.write()`
3. **Avoid `.collect()`** on large datasets - brings all data to driver
4. **Use `.cache()`** for DataFrames used multiple times
5. **Broadcast small tables** in joins to avoid shuffles
6. **Parquet > CSV** for performance and schema preservation
7. **Partition data** by frequently filtered columns
8. **Use Delta Lake** for production pipelines (ACID, time travel)

---

## Resources

- **Official Docs**: https://spark.apache.org/docs/latest/api/python/
- **Databricks Guides**: https://docs.databricks.com/spark/
- **PySpark API**: https://spark.apache.org/docs/latest/api/python/reference/

