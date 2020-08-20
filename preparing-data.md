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
