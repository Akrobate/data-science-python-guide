# Keras Grid search

## Motivation

GridSearch will help to test all possible parameters for the network and give us the best params to get the best score

```python
import numpy as np
import keras
from keras.models import Sequential
from keras.layers import Dense
from keras.wrappers.scikit_learn import KerasClassifier
from sklearn.model_selection import GridSearchCV

def build_classifier(optimizer = 'adam', dropout_rate = '0.1'):
    # Initialize
    classifier = Sequential()

    # Add first layer
    classifier.add(Dense(units = 6, activation = 'relu', kernel_initializer = 'uniform', input_dim = 11))

    # Adding Dropout on the first layer
    classifier.add(Dropout(rate = dropout_rate))

    # Add hidden layer
    classifier.add(Dense(units = 6, activation = 'relu', kernel_initializer = 'uniform'))

    # Adding Dropout on the hidden layer
    classifier.add(Dropout(rate = dropout_rate))
    
    # Add output layer
    classifier.add(Dense(units = 1, activation = 'sigmoid', kernel_initializer = 'uniform'))

    # Compile model
    classifier.compile(optimizer = optimizer, loss = 'binary_crossentropy', metrics = ['accuracy'])
    
    return classifier

classifier = KerasClassifier(build_fn = build_classifier)

parameters = {
    'batch_size': [5, 10, 20],
    'epochs': [100, 200],
    'optimizer': ['Adam', 'rmsprop'],
    'dropout_rate': [0.1, 0.2],
}

grid_search = GridSearchCV(
    estimator=classifier,
    param_grid=parameters,
    scoring='accuracy',
    cv=5
)

grid_search.fit(X_train, y_train)

best_parameters = grid_search.best_params_
best_score = grid_search.best_score_
```