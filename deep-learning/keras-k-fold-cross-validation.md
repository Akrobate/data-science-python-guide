# Keras K Fold cross validation

```python
import numpy as np
import keras
from keras.models import Sequential
from keras.layers import Dense
from keras.wrappers.scikit_learn import KerasClassifier
from sklearn.model_selection import cross_val_score

def build_classifier():
    # Initialize
    classifier = Sequential()

    # Add first layer
    classifier.add(Dense(units = 6, activation = 'relu', kernel_initializer = 'uniform', input_dim = 11))

    # Add hidden layer
    classifier.add(Dense(units = 6, activation = 'relu', kernel_initializer = 'uniform'))

    # Add output layer
    classifier.add(Dense(units = 1, activation = 'sigmoid', kernel_initializer = 'uniform'))

    # Compile model
    classifier.compile(optimizer = 'adam', loss = 'binary_crossentropy', metrics = ['accuracy'])
    
    return classifier

classifier = KerasClassifier(build_fn = build_classifier, batch_size = 10, epochs = 100)
scores_list = cross_val_score(classifier, X_train, y_train, cv = 5)
mean_score = np.mean(scores_list)

print(scores_list)
print(mean_score)

```