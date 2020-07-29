# Connecting to a spark or spark cluster

## Creating context

### With SparkContext method (old way)
```python
from pyspark import SparkContext, SparkConf

conf = SparkConf()
    .setMaster("local")
    .setAppName("My app")
    .set("spark.executor.memory", "1g")

sc = SparkContext(conf = conf)
```

### With SparkSession method current way
```python
from pyspark import SparkContext, SparkConf

spark = SparkSession.builder
    .master("local")
    .appName("Word Count")
    .config("spark.some.config.option", "some-value")
    .getOrCreate()
```

### Possible master params

```python
# Connect to a spark cluster:
master = "spark://IP:PORT"

# Local
master = 'local'
```