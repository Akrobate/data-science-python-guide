# Manipulating data

## List existing tables

```python
list_tables = spark_session.catalog.listTables()
print(list_tables)
```

## Query data 

### Simple selecting data

```python
query = "FROM my_spark_table SELECT * LIMIT 100"

spark_df = spark_session.sql(query)
spark_df.show()
```

#### Returning result as a Pandas Dataframe

```python
query = "FROM my_spark_table SELECT * LIMIT 100"

spark_df = spark_session.sql(query)
pandas_dataframe = spark_df.toPandas()
pandas_dataframe.head()
```

## Selecting columns in Spark DataFrame

```python
# Simple selecting
spark_df.select("col1", "col2", "col3")
# Or
spark_df.select(spark_df.col1, spark_df.col2, spark_df.col3)


# Adding new column with select
new_col = (spark_df.col1 + spark_df.col2).alias("new_col")
new_spark_df = spark_df.select("col1", "col2", "col3", new_col)
# Or
new_spark_df = spark_df.selectExpr("col1", "col2", "col3", "col1 + col2 as new_col")
```

## Filtering Spark DataFrame

```python
# Filter with a string
spark_df_filtered_1 = spark_df.filter("column > 0")

# Filter with a boolean filter
spark_df_filtered_2 = spark_df.filter(spark_df.column > 0)

# Filtering excluding not null values
spark_df_filtered_3 = spark_df.filter(
    "col1 is not NULL ans col2 is not NULL"
)
```

## Grouping Spark Dataframe

```python
# Group methods can be: count, min, max, avg, sum...

spark_df
    .filter(spark_df.col1 == 'value')
    .groupBy()
    .min("distance")
    .show()
```

```python
# Number of rows for each col1 value
spark_df.groupBy("col1").count().show()

# Max value of col2 grouped by col1
spark_df.groupBy("col1").max("col2").show()
```

### Custom grouping aggregation functions

```python
# Some additionnal agregating functions
import pyspark.sql.functions as F

# Number of rows for each col1 value
grouped_data = spark_df.groupBy("col1", "col2")

# Here standart deviation
grouped_data.agg(F.stddev("col3")).show()
```

## Joining Spark DataFrame

```python
joined_df = spark_df_1.join(
    spark_df_1,
    on = "column_to_join_on",
    how = "leftouter"
)
```

## Creating DataFrame Spark and adding fields

```python
# Create the Spark DataFrame
spark_df = spark_session.table("SparkDataframe")

# Preview
spark_df.show()

# Add a column
spark_df = spark_df.withColumn("column2", spark_df.column1)

# Rename a column
spark_df = spark_df.withColumnRenamed("column2", "col2")

# Preview
spark_df.show()
```

## Fields types management

```python
spark_df = spark_df.withColumn(
    "col1",
    spark_df.col1.cast("integer")
)

spark_df = spark_df.withColumn(
    "col2",
    spark_df.col2.cast("double")
)
```
