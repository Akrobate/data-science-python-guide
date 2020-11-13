# Preview Keras models

## Quick preview of model in text

```python
# Lets suppose model var is available and refers to a keras model
model.summary()

# Output example
# Model: "sequential_1"
# _________________________________________________________________
# Layer (type)                 Output Shape              Param #   
# =================================================================
# dense_1 (Dense)              (None, 6)                 72        
# _________________________________________________________________
# dropout_1 (Dropout)          (None, 6)                 0         
# _________________________________________________________________
# dense_2 (Dense)              (None, 6)                 42        
# _________________________________________________________________
# dropout_2 (Dropout)          (None, 6)                 0         
# _________________________________________________________________
# dense_3 (Dense)              (None, 1)                 7         
# =================================================================
# Total params: 121
# Trainable params: 121
# Non-trainable params: 0
# _________________________________________________________________

```


## Graphical preview of a model

You'll need to install pydot and graphviz

```sh
conda install -c conda-forge pydot  graphviz
```

```python
# Lets suppose model var is available and refers to a keras model
from tensorflow.keras.utils import plot_model

plot_model(model, to_file='model_plot.png', show_shapes=True, show_layer_names=True)
```
