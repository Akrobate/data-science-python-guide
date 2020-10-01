# Regression

- [Regression](#regression)
  * [Simple linear regression](#simple-linear-regression)
    + [Scoring linear regression](#scoring-linear-regression)
      - [R2 score](#r2-score)
      - [Root Mean Squarred Error](#root-mean-squarred-error)
  * [Ridge](#ridge)
  * [Lasso](#lasso)
    + [Lasso feature selection](#lasso-feature-selection)

## Simple linear regression

```python
from sklearn import datasets
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
import numpy as np

boston = datasets.load_boston()

X = boston.data
y = boston.target

# Selecting Room number feature
room_column_index = boston.feature_names.tolist().index('RM')
X_rooms = X[:, room_column_index].reshape(-1,1)

linear_regression = LinearRegression()

# Training model
linear_regression.fit(X_rooms, y)

# Generating some values for prediction
X_values_to_predict = np.linspace(min(X_rooms), max(X_rooms), 50)

# Predicting
prediction = linear_regression.predict(X_values_to_predict)

plt.scatter(X_rooms, y, color = 'green', s=5, alpha=0.3)
plt.plot(X_values_to_predict, prediction, color='red')
plt.show()
```


![ml linear regression example.png](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-linear-regression-example.png?raw=true)

### Scoring linear regression

#### R2 score
```python
linear_regression.score(X, y)
```

#### Root Mean Squarred Error
```python
from sklearn.metrics import mean_squared_error
import numpy as np

mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
```


## Ridge

```python
from sklearn import datasets
from sklearn.linear_model import LinearRegression, Ridge
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split 

import numpy as np

boston = datasets.load_boston()

X = boston.data
y = boston.target

# Preparing data
room_column_index = boston.feature_names.tolist().index('RM')
X_rooms = X[:, room_column_index].reshape(-1,1)
X_values_to_predict = np.linspace(min(X_rooms), max(X_rooms), 50)

X_train, X_test, y_train, y_test = train_test_split(X_rooms, y, test_size = 0.3, shuffle = True)


# Linear Regression fit and predict
linear_regression = LinearRegression()
linear_regression.fit(X_train, y_train)
linear_regression_prediction = linear_regression.predict(X_values_to_predict)

# Ridge fit and predict
ridge = Ridge(alpha=0.1, normalize=True)
ridge.fit(X_train, y_train)
ridge_prediction = ridge.predict(X_values_to_predict)

plt.scatter(X_rooms, y, color = 'green', s=5, alpha=0.3)
plt.plot(X_values_to_predict, linear_regression_prediction, color='red', label="Linear regression")
plt.plot(X_values_to_predict, ridge_prediction, color='blue', label="Ridge")

plt.legend()

plt.show()

print(linear_regression.score(X_test, y_test))
print(ridge.score(X_test, y_test))
```

![ML linear ridge regression example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-linear-ridge-regression-example.png?raw=true)


## Lasso

```python
from sklearn import datasets
from sklearn.linear_model import LinearRegression, Lasso
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split 
import numpy as np

boston = datasets.load_boston()

X = boston.data
y = boston.target

# Preparing data
room_column_index = boston.feature_names.tolist().index('RM')
X_rooms = X[:, room_column_index].reshape(-1,1)
X_values_to_predict = np.linspace(min(X_rooms), max(X_rooms), 50)

X_train, X_test, y_train, y_test = train_test_split(X_rooms, y, test_size = 0.3, shuffle = True)

# Linear Regression fit and predict
linear_regression = LinearRegression()
linear_regression.fit(X_train, y_train)
linear_regression_prediction = linear_regression.predict(X_values_to_predict)

# Ridge fit and predict
lasso = Lasso(alpha=0.1, normalize = True)
lasso.fit(X_train, y_train)
lasso_prediction = lasso.predict(X_values_to_predict)

plt.scatter(X_rooms, y, color = 'green', s=5, alpha=0.3)
plt.plot(X_values_to_predict, linear_regression_prediction, color='red', label="Linear regression")
plt.plot(X_values_to_predict, lasso_prediction, color='blue', label="Lasso")

plt.legend()

plt.show()
print(linear_regression.score(X_test, y_test))
print(lasso.score(X_test, y_test))
```

![ML linear lasso regression example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-linear-lasso-regression-example.png?raw=true)

### Lasso feature selection

```python
from sklearn import datasets
from sklearn.linear_model import Lasso
import matplotlib.pyplot as plt
import numpy as np

boston = datasets.load_boston()

X = boston.data
y = boston.target

lasso = Lasso(alpha=0.1, normalize = True)
lasso.fit(X, y)

# Extract lasso coefs
lasso_coefs = lasso.coef_

# plot lasso coefs
range_feature_names = range(len(boston.feature_names))
plt.plot(range_feature_names, lasso_coefs, color = 'blue', alpha = 0.5)

positive_lasso_coefs = (lasso_coefs > 0) * lasso_coefs
negative_lasso_coefs = (lasso_coefs < 0) * lasso_coefs

plt.bar(range_feature_names, positive_lasso_coefs, color = 'green', alpha = 0.7)
plt.bar(range_feature_names, negative_lasso_coefs, color = 'red', alpha = 0.7)
plt.xticks(range_feature_names, boston.feature_names, rotation = 70)
plt.ylabel('Lasso coefs')
plt.show()
```

![ml linear lasso feature selection example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-linear-lasso-feature-selection-example.png?raw=true)

