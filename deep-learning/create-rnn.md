# Building a Recurent Neuronal Network

```python
# Building RNN
from keras.models import Sequential
from keras.layers import Dense, LSTM, Dropout

regressor = Sequential()

# Layer 1
regressor.add(LSTM(units = 50, return_sequences = True, input_shape=(100, 1)))
regressor.add(Dropout(0.2))

# Layer 2
regressor.add(LSTM(units = 50, return_sequences = True))
regressor.add(Dropout(0.2))

# Layer 3
regressor.add(LSTM(units = 50, return_sequences = True))
regressor.add(Dropout(0.2))

# Layer 4
regressor.add(LSTM(units = 50, return_sequences = False))
regressor.add(Dropout(0.2))


# Output layer
regressor.add(Dense(units = 1))

# Compile regressor
regressor.compile(optimizer = 'adam', loss = "mean_squared_error")

# Fitting the model
fit_result = regressor.fit(X_train, y_train, epochs = 200, batch_size = 32)
```
