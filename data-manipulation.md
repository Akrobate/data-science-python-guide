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

Permit to transform a melted data to columns based data

```python
import pandas as pd
my_dataframe = melted_df.pivot_table(
    index=['PreservedCols'],
    columns='VariableColumnName',
    values='ValueColumnName'
)

```

