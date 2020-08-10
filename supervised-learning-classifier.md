# Classifier

## KNN

```python
from sklearn import datasets
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split 

iris = datasets.load_iris()

X = iris.data
y = iris.target

# Preparing test / train datasets
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size = 0.3,
    random_state=123,
    stratify = y
)

# Declaring Classifier
knn = KNeighborsClassifier(n_neighbors = 7)

# Training
knn.fit(X_train, y_train)

# Predicting
y_prediction = knn.predict(X)

# Scoring
print(knn.score(X_test, y_test))
```

### Overfitting / Underfitting curve

```python
from sklearn import datasets
import numpy as np
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split 
import matplotlib.pyplot as plt

iris = datasets.load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size = 0.1,
    random_state = 123,
    stratify = y
)

neighbors = np.arange(1, 9)
train_accuracy = np.empty(len(neighbors))
test_accuracy = np.empty(len(neighbors))

for index, k in enumerate(neighbors):
    knn = KNeighborsClassifier(n_neighbors = k)
    knn.fit(X_train, y_train)
    train_accuracy[index] = knn.score(X_train, y_train)
    test_accuracy[index] = knn.score(X_test, y_test)

plt.title('KNN: Under/Over Fitting curve')
plt.plot(neighbors, test_accuracy, label = 'Test score')
plt.plot(neighbors, train_accuracy, label = 'Train score')
plt.legend()
plt.xlabel('Number of Neighbors')
plt.ylabel('Score')
plt.show()
```

![ML KNN overfit underfit curve](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-knn-overfit-underfit-curve.png?raw=true)


# Logistic Regression

```python
from sklearn import datasets
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split 
from sklearn.metrics import confusion_matrix, classification_report

iris = datasets.load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size = 0.2,
    random_state=123,
    stratify = y
)

logisitic_regression = LogisticRegression(max_iter = 200)
logisitic_regression.fit(X_train, y_train)

y_test_predict = logisitic_regression.predict(X_test)

```

## Scoring

### Score the model

Score method return the accuracy of the model, and is the average of F1 scores of each class of the model

```python
logisitic_regression.score(X_test, y_test)
```

**Returns**

```python
0.9666666666666667
```


### Calculate the confustion matrix

```python
confusion_matrix(y_test, y_test_predict)
```

||predicted<br>setosa|predicted<br>versicolor|predicted<br>virginica|
|-|-|-|-|
|setosa|10|0|0|
|versicolor|0|9|1|
|virginica|0|0|10|

### Full classification repport

```python
classification_report(y_test, y_test_predict)
```

![ml classification report example](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-classification-report-example.png?raw=true)


### Metrics

#### Precision

![{\color{Golden}Precision=\frac{TruePositive}{TruePositive+FalsePositive}}](https://latex.codecogs.com/svg.latex?\bg_white&space;\large&space;{\color{Golden}Precision=\frac{TruePositive}{TruePositive+FalsePositive}})

#### Recall

![{\color{Golden}Precision=\frac{TruePositive}{TruePositive+FalseNegative}}](https://latex.codecogs.com/svg.latex?\bg_white&space;\large&space;{\color{Golden}Precision=\frac{TruePositive}{TruePositive+FalseNegative}})

#### F1 Score

![{\color{Golden}F1Score=2\cdot\frac{precision\cdot recall}{precision+recall}}](https://latex.codecogs.com/svg.latex?\bg_white&space;\large&space;{\color{Golden}F1Score=2\cdot\frac{precision\cdot%20recall}{precision+recall}})


#### ROC Curve (receiver operating characteristic)

```python
from sklearn import datasets
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split 
from sklearn.metrics import roc_curve
import matplotlib.pyplot as plt

iris = datasets.load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=123, stratify = y)

logisitic_regression = LogisticRegression(max_iter = 200)
logisitic_regression.fit(X_train, y_train)


# Category to analyse
category_index = 2
y_pred_proba = logisitic_regression.predict_proba(X_test)[:, category_index]

false_positive_rate, true_positive_rate, thresholds = roc_curve((y_test == category_index), y_pred_proba)

plt.plot([0,1],[0,1], 'k--')
plt.plot(false_positive_rate, true_positive_rate)
plt.title("Roc curve " + iris.target_names[category_index] + " prediction")
plt.xlabel('False positive rate')
plt.ylabel('True positive rate')
plt.show()
```

![ml Metric ROC Iris](https://github.com/Akrobate/data-science-python-guide/blob/master/assets/images/ml-metric-roc-iris.png?raw=true)


#### ROC - AUC metric (Area Under the Curve)

```python
# ROC
# Logistic Regression scorings

from sklearn import datasets
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split 
from sklearn.metrics import roc_auc_score
import matplotlib.pyplot as plt

iris = datasets.load_iris()

X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state=123, stratify = y)

logisitic_regression = LogisticRegression(max_iter = 200)
logisitic_regression.fit(X_train, y_train)

# Category to analyse
category_index = 2
y_pred_proba = logisitic_regression.predict_proba(X_test)[:, category_index]
roc_auc_score(y_test == category_index, y_pred_proba)
```

**Returns**

```python
0.995
```