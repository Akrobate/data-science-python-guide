# Cleaning data

## Dealing with NaN values

### Fill na with mean serie values

Lets supose some values of 'sepal length (cm)' are not setted, and we want to fill it mith serie mean value

```python
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

sepal_length_cm_mean = iris_df['sepal length (cm)'].mean()
iris_df['sepal length (cm)'].fillna(sepal_length_cm_mean)
```

### Drop na values

```python
import pandas as pd
my_df.dropna(
    axis = 0,       # 0 for rows remove, 1 cols remove
    how = 'any',    # any to remove if any NaN is found, all if all is NaN,
    inplace = True  # Modify the current df
)
```

## Dealing with Duplicate

### Drop duplicates on a Serie

```python
import pandas as pd
field_a = my_df.field_a
field_a = field_a.drop_duplicates()
```

### Drop duplicates on a Dataframe

```python
import pandas as pd
my_df.drop_duplicates(
    subset = ['field_a', 'field_b'],    # Fields to consider for duplication
    keep = 'first',                     # 'first', 'last'
    inplace = True,                     # Modify the current df
    ignore_index = False                # True value will create new index 0,1...
)

```


## Checking by Asserting null data

```python
# check no null data
assert pd.notnull(iris_df).all().all()

# Check all values are >= 0
assert  (iris_df >= 0).all().all()
```

## Checking by Asserting types


```python
# Assert if field_a is type object
assert my_df.field_a.dtypes == np.object

# Assert if field_b is type int64
assert my_df.field_b.dtypes == np.int64

# Assert if field_b is type float64
assert my_df.field_c.dtypes == np.float64
```