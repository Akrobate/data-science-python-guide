# Connecting to a spark or spark cluster

## Connecting

### SparkContext

```python
import findspark
findspark.init("/path/to/decompressed/spark-3.0.0-bin-hadoop3.2")
from pyspark import SparkContext, SparkConf

conf = SparkConf()
    .setMaster("local")
    .setAppName("Test application")
    .set("spark.executor.memory", "1g")

spark_context = SparkContext(conf = conf)

# disconnect app from cluster
spark_context.stop()
```

### SparkSession

```python
import findspark
findspark.init("/path/to/decompressed/spark-3.0.0-bin-hadoop3.2")
from pyspark.sql import SparkSession

spark_session = SparkSession.builder
    .master("local")
    .appName("Test application")
    .config("spark.some.config.option", "some-value")
    .getOrCreate()

# disconnect app from cluster
spark_session.stop()
```

### SparkSession from SparkContext

```python
from pyspark import SparkContext, SparkConf
from pyspark.sql import SparkSession

conf = SparkConf()
    .setMaster("local")
    .setAppName("Test application")
    .set("spark.executor.memory", "1g")

spark_context = SparkContext(conf = conf)

spark_session = SparkSession
    .builder
    .config(spark_context.getConf)
    .getOrCreate()
```

### Parameters to set

In some cases you will have to manually set PYSPARK_PYTHON variable. If you worker returns an error of not found python executor, you will have to set it manually

```python
import findspark
findspark.init("/path/to/decompressed/spark-3.0.0-bin-hadoop3.2")

import os
os.environ['PYSPARK_PYTHON'] = '/opt/bitnami/python/bin/python'

from pyspark import SparkContext, SparkConf
from pyspark.sql import SparkSession
...
```

In some cases just setting python as variable solves the problem

```python
import os
os.environ['PYSPARK_PYTHON'] = 'python'
```

Be aware that setting environment variable must be setted after findpark init.

### Possible master params

```python
# Connect to a spark cluster:
master = "spark://IP:PORT"

# Local
master = 'local'

# Local with automatic cores
master = 'local[*]'

# Local with 4 cores
master = 'local[4]'
```
