# Regression

## Simple linear regression

```python
from sklearn import datasets
from sklearn.linear_model import LinearRegression
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