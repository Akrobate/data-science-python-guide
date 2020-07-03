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
