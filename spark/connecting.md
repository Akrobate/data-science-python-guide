# Connecting to a spark cluster

## Creating context

```python
from pyspark import SparkContext, SparkConf

conf = SparkConf()
    .setMaster("local")
    .setAppName("My app")
    .set("spark.executor.memory", "1g")

sc = SparkContext(conf = conf)
```

