# Pipelines

## Simple example of a pipeline

```python
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.pipeline import Pipeline

X, y = make_classification(random_state=0)

X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('svc', SVC())
])

pipeline.fit(X_train, y_train)
pipe.score(X_test, y_test)
```