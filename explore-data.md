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

# returns unique values of a column
my_dataframe['ColumnName'].unique()
```
