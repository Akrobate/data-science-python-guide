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

### Fill na with SimpleImputer

```python
from sklearn import datasets
from sklearn.impute import SimpleImputer
import numpy as np

iris = datasets.load_iris()
X = iris.data

imputer = SimpleImputer(missing_values=np.nan, strategy="mean")
imputer.fit(X)

prepared_data = imputer.transform([
        [np.nan, 0, 0, 0],
        [0, np.nan, 0, 0],
        [0, 0, np.nan, 0],
        [0, 0, 0, np.nan],
])

print(prepared_data)
# Output
# [[5.84333333 0.         0.         0.        ]
# [0.         3.05733333 0.         0.        ]
# [0.         0.         3.758      0.        ]
# [0.         0.         0.         1.19933333]]


print(X[:,0].mean())
# Output 5.843333333333334

print(X[:,1].mean())
# Output 3.0573333333333337

print(X[:,2].mean())
# Output 3.7580000000000005

print(X[:,3].mean())
# Output 1.1993333333333336
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