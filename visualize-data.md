# Data visualisation with panda

## Histograms

Exploring sepal length data set repartition by creating a simple histogram representation

### Using pandas hist method

```python
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)
iris_df['sepal length (cm)'].hist(bins=20)
```

![Iris sepal length hist](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-sepal-length-pandas-hist-20-bins.png?raw=true)


### Using matplotlib to draw historgram

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

## 2D Histogram

### Standart 2D histogram

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

iris = load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

plt.hist2d(
    iris_df['petal length (cm)'],
    iris_df['petal width (cm)'],
    bins=(10, 10),      # x bins, y bins
    range=((0,8),(0,3)) # ((xmin, xmax), (ymin, ymax))
)

plt.colorbar()

plt.xlabel('petal length (cm)')
plt.ylabel('petal width (cm)')
plt.title('2D Histogram')
plt.show()
```

![Iris Plot 2d histogram](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-plot-2dhist.png?raw=true)

### Hexbin 2D histogram

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

iris = load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

plt.hexbin(
    iris_df['petal length (cm)'],
    iris_df['petal width (cm)'],
    gridsize=(10,8),      # x bins, y bins
    extent = (0,8,0,3),   # xmin, xmax, ymin, ymax
)

plt.colorbar()

plt.xlabel('petal length (cm)')
plt.ylabel('petal width (cm)')
plt.title('2D hexbin histogram')
plt.show()
```

![Hexbin 2D histogram](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/2D-hexbin-histogram-example.png?raw=true)


## 2D Graph

### Raw 2D graph

```python
import numpy as np
import matplotlib.pyplot as plt

# Linear array from -10 to 10 with 25 elements
x_array = np.linspace(-10, 10, 25)

# Linear array from -5 to 5 with 12 elements
y_array = np.linspace(-5, 5, 12)

# Meshgrid will generate 2 2D arrays
X, Y = np.meshgrid(x_array, y_array)

plt.pcolor(X + Y)
plt.show()
```

![2D graph example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/2D-graph-example.png?raw=true)


### Contour graph

```python
import numpy as np
import matplotlib.pyplot as plt

x_array = np.linspace(-10, 10, 25)
y_array = np.linspace(-5, 5, 12)

X, Y = np.meshgrid(x_array, y_array)

Z = X + Y

# Example contour graph with 5 contours
plt.subplot(1,2,1)
plt.contour(X, Y, Z, 5)  # 5 is number of contours

# Example filled contour graph with 5 contours
plt.subplot(1,2,2)
plt.contourf(X, Y, Z, 5)

plt.tight_layout()
plt.show()
```
![2D graph contour](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/2D-graph-contour.png?raw=true)



## Box plots

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

## Strip plots
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

iris = load_iris()
df= pd.DataFrame(
    data = np.c_[iris.data, iris.target],
    columns= iris.feature_names + ['target']
)

df['species'] = pd.Categorical.from_codes(
    iris.target,
    iris.target_names
)

sns.stripplot(
    y='sepal width (cm)',
    x='species',
    data=df,
    size=7,
    jitter=True
)

plt.show()
```

![Seaborn strip plot example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/seaborn-strip-plot-example.png?raw=true)

## Scatter plot of two variables

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


## Draw multiple plots on same chart

```python
import matplotlib.pyplot as plt

plt.plot(x_axis_data, y_axis_1_data, color='red')
plt.plot(x_axis_data, y_axis_2_data, color='blue')
plt.show()
```

## Draw multiple datagrame plots with subplots

```python
import matplotlib.pyplot as plt
from sklearn import datasets
import pandas as pd

iris = datasets.load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

figure, axe = plt.subplots(2,1)  # rows, cols

iris_df.plot(
    ax=axe[0],
    kind='scatter',
    x='petal length (cm)',   # variable on x axis
    y='petal width (cm)',    # variable on y axis
    color='green'
)

iris_df.plot(
    ax=axe[1],
    kind='scatter',
    x='sepal length (cm)',   # variable on x axis
    y='sepal width (cm)',    # variable on y axis
    color='red'
)

plt.tight_layout()      # Method to adjust subplots sizes params
plt.show()
```

![Iris subplot dataframe plot](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/iris-subplot-dataframe-plot.png?raw=true)

## Matrix scatter plot

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

## Preview Linear regressions

### Simple linear regression

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

iris = load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

sns.lmplot(x='petal width (cm)', y='petal length (cm)', data=iris_df)
plt.show()
```

![Seaborn linear regression example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/seaborn-linear-regression-example.png?raw=true)

### Linear regression setting ordrer

Some times line as linear regressions is not a good enough solution. So it is possible to set the order of the regression function with "order" param. This param is also available in redisplot method.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

iris = load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

sns.lmplot(
    x='petal width (cm)',
    y='petal length (cm)',
    order = 2, # Set the order here
    data=iris_df
)
plt.show()
```

![seaborn linear regression order 2 example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/seaborn-linear-regression-order-2-example.png?raw=true)

### Previewing residuals around regression

This graph will represent how points are variating around the regression

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

iris = load_iris()
iris_df = pd.DataFrame(iris.data, columns = iris.feature_names)

sns.residplot(
    x = 'petal width (cm)',
    y = 'petal length (cm)',
    data = iris_df,
    color = 'red'
)
plt.show()
```

![seaborn regression residual plot example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/seaborn-regression-residual-plot-example.png?raw=true)

### Make regression on grouped data

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

iris = load_iris()
df = pd.DataFrame(
    data = np.c_[iris.data, iris.target],
    columns= iris.feature_names + ['target']
)
df['species'] = pd.Categorical.from_codes(
    iris.target,
    iris.target_names
)

sns.lmplot(
    x='sepal width (cm)',
    y='sepal length (cm)',
    data=df,
    hue='species',
    palette='Set1'
)

plt.show()
```

![Seaborn linear regression grouped example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/seaborn-linear-regression-grouped-example.png?raw=true)

## Customize plots

```python
# Name plot
plt.title('The name of the chart')
```

```python
# Generate a legend
plt.legend(loc='lower center')
```

```python
# Name axis
plt.xlabel('Time')
plt.ylabel('My value')
```

```python
# Setting figure size
from matplotlib.pyplot import figure
figure(figsize = (8, 6), dpi=80) # witdh, height, resolution
```

```python
# Specifing coordinates and size of a plot in chart

# first plot
plt.axes([
    0, # x plot start at 0
    0, # y plot start at 0
    0.5, # plot width (50% of chart)
    0.9 # plot height (100% of chart)
])
plt.plot(....)

# second plot
plt.axes(....)
plt.plot(....)
....
```

```python
# Setting axis ranges per axis
plt.xlim([10,20])
plt.ylim([0,30])

# setting both at once
plt.axis((10,20,0,30))
```



### Color maps

Some methods with color map param

```python
# setting colormap in graphs with cmap param
plt.contour(... , cmap = 'summer')
plt.contourf(... , cmap = 'winter')
plt.pcolor(... , cmap = 'copper')
plt.hist2d(... , cmap = 'hot')

# 'binary', 'gist_yarg', 'gist_gray', 'gray'
# 'bone', 'pink', 'spring', 'summer',
# 'autumn', 'winter', 'cool', 'Wistia',
# 'hot', 'afmhot', 'gist_heat', 'copper'

```

Previes available colormaps

```python
import numpy as np
import matplotlib.pyplot as plt

cmap_list = [
    'binary',
    'gist_yarg',
    'gist_gray',
    'gray',
    'bone',
    'pink',
    'spring',
    'summer',
    'autumn',
    'winter',
    'cool',
    'Wistia',
    'hot',
    'afmhot',
    'gist_heat',
    'copper'
]

plt.figure(figsize=(10, 8))

for index, cmap in enumerate(cmap_list):
    plt.subplot(8,2, index + 1)
    plt.title(cmap)
    plt.pcolor([np.linspace(-10, 10, 25)], cmap = cmap)

plt.tight_layout()
plt.show()
```

![Color map example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/color-map-example.png?raw=true)


## Saving plot

```python
plt.savefig('my_plot_chart.png')
```


