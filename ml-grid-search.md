# Grid Search

- [Grid Search](#grid-search)

Grid search is a technique for model optimization. With grid search technic you'll be able to find the best hyper parameter of your model. Grid search tries all passed hyperparameters to find wich one provides the best score. You have to know that this technic is like a brut force technic wich will try all combination of hyperparameters

```python
from sklearn.model_selection import GridSearchCV
from sklearn.linear_model import LogisticRegression
from sklearn import datasets

iris = datasets.load_iris()

X = iris.data
y = iris.target

logistic_regression = LogisticRegression(penalty='l2')

param_grid = dict(
    dual=[True, False],
    max_iter=[100, 110, 120, 130, 140]
)

grid_search_cv = GridSearchCV(
    estimator=logistic_regression,
    param_grid=param_grid,
    cv = 3,
    n_jobs = -1
)

grid_result = grid_search_cv.fit(X, y)

print("Best: %f using %s" % (grid_result.best_score_, grid_result.best_params_))
```