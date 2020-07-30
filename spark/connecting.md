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

### With SparkSession method current way

```python
import findspark
findspark.init("/path/to/decompressed/spark-3.0.0-bin-hadoop3.2")
from pyspark import SparkContext, SparkConf

spark_session = SparkSession.builder
    .master("local")
    .appName("Test application")
    .config("spark.some.config.option", "some-value")
    .getOrCreate()

# disconnect app from cluster
spark_session.stop()
```

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
