# Preview Keras models

## Quick preview of model in text

```python
# Lets suppose model var is available and refers to a keras model
model.summary()
```

## Graphical preview of a model

```python
# Lets suppose model var is available and refers to a keras model
from tensorflow.keras.utils import plot_model

plot_model(model, to_file='model_plot.png', show_shapes=True, show_layer_names=True)
```