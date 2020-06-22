# Data exploration

## Fundamentals

```python
import pandas as pd

# Summary about dataframe
my_dataframe.info()

# detailed metric about dataframe
my_dataframe.describe()

# Returns a tuple (number_of_rows, number_of_colums)
my_dataframe.shape

# Preview first dataframe rows
my_dataframe.head()

# Preview last dataframe rows
my_dataframe.tail()

```

## Data exploring
```python
# returns list of column names
my_dataframe.columns

# returns count of each value in column (with NaN here)
my_dataframe['ColumnName'].value_counts(dropna=False)

```


## Data visualisation with panda

Exploring sepal length data set repartition by creating a simple histogram representation

```python
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
iris_df['sepal length (cm)'].hist(bins=20)
```

![Iris sepal length hist](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-sepal-length-hist-20-bins.png?raw=true)
