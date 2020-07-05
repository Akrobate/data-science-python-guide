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

### histograms

Exploring sepal length data set repartition by creating a simple histogram representation

#### Using pandas hist method

```python
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
iris_df['sepal length (cm)'].hist(bins=20)
```

![Iris sepal length hist](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-sepal-length-pandas-hist-20-bins.png?raw=true)


#### Using matplotlib to draw historgram

```python
import matplotlib.pyplot as plt
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
iris_df['sepal length (cm)'].plot(
    kind='hist',
    rot=90,       # X label angle
    logx=False,   # log scale on X axis
    logy=False,   # log scale on Y axis
    bins=20       # Number of wanted bars
)

plt.show()
```

![Iris sepal length hist](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-sepal-length-matplotlib-hist-20-bins.png?raw=true)


### Box plots

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

# load data and add targets to dataframe
iris = load_iris()
df= pd.DataFrame(
    data = np.c_[iris.data, iris.target],
    columns= iris.feature_names + ['target']
)

# Set categorical values in column named species
df['species'] = pd.Categorical.from_codes(
    iris.target,
    iris.target_names
)

df.boxplot(
    column='sepal width (cm)',
    by='species',
    rot=90
)

plt.show()
```

![Iris sepal width boxplot](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-sepal-width-pandas-boxplot.png?raw=true)

### Scatter plot of two variables

```python
import matplotlib.pyplot as plt
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
iris_df.plot(
    kind='scatter',
    x='petal length (cm)',   # variable on x axis
    y='petal width (cm)',    # variable on y axis
)

# Optionnal custumize axis labels
plt.xlabel('Petal length in centimeters)')
plt.ylabel('Petal width in centimeters')

# Optionnal specify axis limits
plt.xlim(0, 7)
plt.ylim(0, 2.5)

plt.show()
```

![Iris sepal width boxplot](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-pandas-2-vars-scatter-plot.png?raw=true)


### Matrix scatter plot

To quick preview how variables are correlated

```python
import pandas as pd
from sklearn.datasets import load_iris

df= pd.DataFrame(data = iris.data, columns= iris.feature_names)

_ = pd.plotting.scatter_matrix(
    df,
    c = iris.target,    # Colors are targets
    figsize=[10, 10],   # Size of all graph
    s = 100,            # Size of each marker
    marker = 'D',       # marker type
)

```
![Iris pandas plotting scatter matrix](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-pandas-matrix-scatter-plot.png?raw=true)
