# Machine Learning

## Preparing data

### Create a StringIndexer, OneHotEncoder

```python
from pyspark.ml.features import StringIndexer, OneHotEncoder, VectorAssembler

# StringIndexer
col_indexer = StringIndexer(
    inputCol="from_column_name",
    outputCol="to_column_name"
)

# OneHotEncoder
col_encoder = OneHotEncoder(
    inputCol="from_column_name",
    outputCol="to_column_name"
)

# VectorAssembler
vector_assembler = VectorAssembler(
    inputCols=["from_column_name1", "from_column_name2"]
    outputCol="to_column_name"
)
```

## Building Pipeline 

```python
from pyspark.ml import Pipeline

# Make the pipeline
flights_pipe = Pipeline(
    stages = [
        col_indexer,
        col_encoder,
        vector_assembler
    ]
)
```