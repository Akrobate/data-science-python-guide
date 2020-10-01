# Usefull tricks

- [Usefull tricks](#usefull-tricks)
  * [Working with sklearn example datasets](#working-with-sklearn-example-datasets)
  * [Working with seaborn example datasets](#working-with-seaborn-example-datasets)
  * [Working with json](#working-with-json)
  * [Generating range Arrays](#generating-range-arrays)

## Working with sklearn example datasets

You can find some usefull datasets in sklearn library to perform tests.

```python
import numpy as np
import pandas as pd
from sklearn import datasets

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
```

Each dataset is composed of following fields:

* data - Array containing raw data (rows, cols)
* target - Array target data (or identifier for target name)
* target_names - name of the target
* DESCR - datafile description
* feature_names - data columns names
* filename


## Working with seaborn example datasets

Be aware that seaborn loader will load csv files online, so you need to be connected to load data. Save the dataset as CSV to use it locally

```python
from seaborn import load_dataset
titanic = load_dataset("titanic")
```


## Working with json

```python
import json

json_string = "{'test':1}"

# parse json
my_dictionnary = json.loads(json_string)
print(my_dictionnary['test'])
# output: 1

# stringify dictionnary to json
my_json_string = json.dumps(my_dictionnary)
print(my_json_string)
# will return something like json_string
```

## Generating range Arrays

```python
# integers ranges
list(range(1, 10, 2))
# [1, 3, 5, 7, 9]

import numpy as np

# float ranges
np.arange(1, 2, 0.1)
# array([1. , 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 1.8, 1.9])

# float ranges, with number of wanted values
np.linspace(1, 2, 10, endpoint = False)
# array([1. , 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 1.8, 1.9])

# float ranges, with number of wanted values
np.linspace(1, 2, 10, endpoint = True)
# array([1.        , 1.11111111, 1.22222222, 1.33333333, 1.44444444,
#       1.55555556, 1.66666667, 1.77777778, 1.88888889, 2.        ])
```


