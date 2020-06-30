# Data manipulation

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

## Melt / Pivot data

### Melt dataframe

Usefull trick to transform cols to rows

```python
import pandas as pd
melted_df = pd.melt(
    frame=my_df,
    value_vars=['Cols', 'to', 'melt'],
    id_vars=['ColsToPreserve'],
    var_name='VariableColumnName',        # Optionnal: set the name of variable column
    value_name='ValueColumnName'          # Optionnal: set the name of the value column
)
```

### Pivot datafram

Permit to transform a melted data to columns based data. If multiple lines for specific index, an agregation function can be used.

```python
import pandas as pd
import numpy as np
my_dataframe = melted_df.pivot_table(
    index=['PreservedCols'],
    columns='VariableColumnName',
    values='ValueColumnName',
    aggfunc=np.mean             # here we provide the average value of all sames preserved cols
)

```

After pivoting data, the index can be altered. To get back a simple incremental RangeIndex you need to reset_index() on the dataframe

```Python
# reseting indexes on dataframe
my_dataframe = my_dataframe.index.reset_index()
print(my_dataframe.index) # will show new RangeIndex
```