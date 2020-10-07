# Loading data to spark cluster

- [Loading data to spark cluster](#loading-data-to-spark-cluster)
  * [Loading using panda dataframe](#loading-using-panda-dataframe)
  * [Loading csv data directly with Spark](#loading-csv-data-directly-with-spark)

## Loading using panda dataframe

```python
import pandas as pd
import numpy as np

# creating a dataframe to load to spark
df = pd.DataFrame(
    np.random.random(1000),
    columns = ['data']
)

# Create Spark Dataframe from pandas Dataframe
spark_df = spark_session.createDataFrame(df)

# Persist data in Spark Cluster
spark_df.createOrReplaceTempView("test_rdd")

print(spark_session.catalog.listTables())
```

## Loading csv data directly with Spark

Warning: Be aware that each worker have to have access to the csv file on its own file system.

```python
# Create Spark DataFrame
spark_df = spark.read.csv('./file_path.csv', header=True)

# You can preview th spark_df
print(spark_df.show())

# Persist data in Spark Cluster
spark_df.createOrReplaceTempView("test_rdd")

print(spark_session.catalog.listTables())
```