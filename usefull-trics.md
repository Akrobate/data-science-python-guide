# Usefull tricks


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
