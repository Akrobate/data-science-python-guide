# Data loading

## Join data

Example of making a merge with a left join very similar to mysql left join style

```python
import pandas as pd

dataframe_a = pd.merge(
    left=dataframe_a, 
    right=dataframe_b,
    how='left', 
    left_on='a_b_id',
    right_on='id')
```
