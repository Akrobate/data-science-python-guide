# Building sequential or functionnal models

There are two ways to build a model in keras, Sequential way and functionnal

## Sequential model example

```python
import keras

model = keras.models.Sequential()

model.add(keras.layers.Flatten(input_shape=[32, 32]))
model.add(keras.layers.Dense(256, activation="relu"))
model.add(keras.layers.Dense(128, activation="relu"))
model.add(keras.layers.Dense(8, activation="softmax"))

model.compile(loss="sparse_categorical_crossentropy", optimizer="adam", metrics=["accuracy"])
```

## Functionnal model example

```python
import keras

input_ = keras.layers.Input(shape=[28, 28])
x = layers.Dense(256, activation='relu')(input_)
x = layers.Dense(128, activation='relu')(x)
output_ = layers.Dense(8, activation='relu')(x)

model = keras.Model(inputs=[input_], outputs=[output_])

model.compile(loss="sparse_categorical_crossentropy", optimizer="adam", metrics=["accuracy"])
```