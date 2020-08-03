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