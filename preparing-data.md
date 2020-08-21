# Data preparation for machine learning

## Categorical Encoding data

Encoding categorical data to numerical values

```python
from sklearn.preprocessing import LabelEncoder
import numpy as np

label_encoder = LabelEncoder()
encoded_data = label_encoder.fit_transform(["paris", "paris", "tokyo", np.nan])

print(encoded_data)
# [1 1 2 0]

print(label_encoder.classes_)
# ['nan' 'paris' 'tokyo']

print(label_encoder.inverse_transform([2, 2, 1]))
# ['tokyo' 'tokyo' 'paris']
```

If you encounter an error like "unorderable types: str() < float()" that means that you are trying to deal with numpy serie with different types in elements. To fix it you can convert your numpy serie to a simple list, or fix all types of your serie (sounds better)

```python
from sklearn.preprocessing import LabelEncoder
from seaborn import load_dataset

titanic = load_dataset("titanic")

deck_le = LabelEncoder()

encoded_data = deck_le.fit_transform(titanic.deck)
# Will fail becase deck is a numpy serie and contains NaN values (float) 
# and Strings

encoded_data = deck_le.fit_transform(titanic.deck.astype(str))
# Will work, all NaN are converted to nan string

encoded_data = deck_le.fit_transform(list(titanic.deck))
# Will work, all NaN are converted to nan string in deck_le.classes_
```
