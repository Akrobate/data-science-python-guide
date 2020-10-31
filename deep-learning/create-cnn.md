# Creating a CNN neural network

```python
from keras.models import Sequential
from keras.layers import Convolution2D
from keras.layers import MaxPooling2D
from keras.layers import Flatten
from keras.layers import Dense

# Initialize Sequelize
classifier = Sequential()

# Adding Convolution layer
classifier.add(Convolution2D(
    filters = 32,
    kernel_size = (3, 3),
    strides = 1,
    input_shape = (64, 64, 3),
    activation = 'relu'
))

# Adding pooling layer
classifier.add(MaxPooling2D(
    pool_size = (2, 2),
    strides = None
))

# Adding flatten layer
classifier.add(Flatten())

# Adding full connected ANN
classifier.add(Dense(units = 128, activation = 'relu'))

# Output layer (sigmoid => if 1 neuron output, SoftMax if multiple)
classifier.add(Dense(units = 1, activation = 'sigmoid'))

# Compiling neural network
# binary_crossentropy => classification of 1 neural output
# categorical_crossentropy => classification of multiple neural output
classifier.compile(
    optimizer = 'adam',
    loss = 'binary_crossentropy',
    metrics = ['accuracy']
)
```