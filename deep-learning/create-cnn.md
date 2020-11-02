# Creating a CNN neural network

## Building and compiling a CNN

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


## Fitting the CNN and augmenting images

```python

# Lets assume previous code was evaluted and classifier variable is available

from keras.preprocessing.image import ImageDataGenerator

train_datagen = ImageDataGenerator(
    rescale=1./255,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True)

test_datagen = ImageDataGenerator(rescale=1./255)

training_set = train_datagen.flow_from_directory(
    'cnn_dataset/training_set',
    target_size=(64, 64),
    batch_size=32,
    class_mode='binary'
)

test_set = test_datagen.flow_from_directory(
    'cnn_dataset/test_set',
    target_size=(64, 64),
    batch_size=32,
    class_mode='binary')


classifier.fit(
    training_set,
    steps_per_epoch = 250,
    epochs = 25,
    validation_data = test_set,
    validation_steps = 63
)
```


## Making prediction on a signle image

```python
import numpy as np
from keras.preprocessing import image

test_image = image.load_img(
    'cnn_dataset/image_to_predict',
    target_size=(64,64))

test_image = image.img_to_array(test_image)
test_image = np.expand_dims(test_image, axis = 0)


classes_mapping = training_set.class_indices
prediction = classifier.predict(test_image)
```
