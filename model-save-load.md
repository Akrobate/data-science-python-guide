# Save load trained model

## Save model with joblist

```python
from joblib import dump, load

model = ...

dump(model, 'filename.joblib')
```

## Save model with joblist

```python
model = load('filename.joblib')
```