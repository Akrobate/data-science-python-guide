# Data preparation for machine learning

## Categorical to numeric encode data

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

## Categorical data to binary new columns encode

```python
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer
import numpy as np

data = np.array([["paris", 2], ["paris", 2], ["tokyo", 3], [np.nan, 0]])
print(data)
# [['paris' '2']
#  ['paris' '2']
#  ['tokyo' '3']
#  ['nan' '0']]

column_to_hot_encode = 0 # City name column
column_transformer = ColumnTransformer(
        [
            (
                "name_of_the_step",
                OneHotEncoder(),
                [column_to_hot_encode]
            )
        ],
        remainder = 'passthrough'
)
data = column_transformer.fit_transform(data)
print(data)
# [['0.0' '1.0' '0.0' '2']
#  ['0.0' '1.0' '0.0' '2']
#  ['0.0' '0.0' '1.0' '3']
#  ['1.0' '0.0' '0.0' '0']]
```

## Standardization of data

The standardization method calculation

standard_value = (value - average(column)) / standard_deviation(column)

```python
from sklearn.preprocessing import StandardScaler

data = np.array(
        [['0.0', '1.0', '0.0', '2'],
         ['0.0', '1.0', '0.0', '2'],
         ['0.0', '0.0', '1.0', '3'],
         ['1.0', '0.0', '0.0', '0']]
)

standard_scaler = StandardScaler()
data = standard_scaler.fit_transform(data.astype(np.float))
print(data)
# [[-0.57735027  1.         -0.57735027  0.22941573]
#  [-0.57735027  1.         -0.57735027  0.22941573]
#  [-0.57735027 -1.          1.73205081  1.14707867]
#  [ 1.73205081 -1.         -0.57735027 -1.60591014]]
```