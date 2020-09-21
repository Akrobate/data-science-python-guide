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

## Concat dataframe rows / cols

Example of concatenating rows of n dataframes

```python
import pandas as pd

rows_concatenated_df = pd.concat(
    [df1, df2, dfn],
    axis = 0    # 0 is rows concatenation
)

cols_concatenated_df = pd.concat(
    [df1, df2, dfn],
    axis = 1    # 1 is cols concatenation
)
```

## Concat dataframe rows of splitted column value

Lets supose we have some values in json string format in one of fields of our dataframe. We want to get this data in its own column, with each value in it own row

```python
import pandas as pd
import json

example_data = [
    {
        'column1': 1,
        'column2':'{"id_list":[1,2,3]}'
    },
    {
        'column1': 2,
        'column2':'{"id_list":[1,2,3]}'
    },
]

input_data = pd.DataFrame(example_data)

result = pd.DataFrame()

for _, data in input_data.iterrows():
    column_json_decoded = json.loads(data['column2'])
    if 'id_list' in column_json_decoded:
        id_series = pd.Series(column_json_decoded['id_list'])
        temporary_dataframe = pd.DataFrame()
        temporary_dataframe['column2_id'] = id_series
        temporary_dataframe['column1'] = data['column1']
        result = result.append(temporary_dataframe)

print(result.head())
print(result.info())
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

### Pivot dataframe

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

## Managing indexes

```python
# Setting index
my_df = my_df.set_index('column name')

# resetting index
my_df = my_df['column name'].reset_index()
```

## Manipulating columns as string

```Python
import numpy as np
import pandas as pd
from sklearn.datasets import load_iris

iris = load_iris()
df = pd.DataFrame(
    data = np.c_[iris.data, iris.target],
    columns= iris.feature_names + ['target']
)

# Set categorical values in column named species
df['species'] = pd.Categorical.from_codes(iris.target, iris.target_names)


# in this column we are going to have s of setosa
df['First_letter'] = df.species.str[0]

# split will contain [set, sa] of setosa
df['split'] = df.species.str.split('o')

# get value from splitted value
df['split_first_part'] = df['split'].str.get(0)
df['split_second_part'] = df['split'].str.get(1)

```

## Changing columns types

Previews types with .info() dataframe method

### Object to categorical

When some data is imported strings will be of object type. It is possible to change it to categorical type when needed to improve performances

```python
df.my_col = df.my_col.astype('category')
```

### Object to numeric type

error coerce will put NaN values when value was not converted to numeric type

```python
df.my_col = pd.to_numeric(df['my_col'], errors='coerce')
```

## Sorting panda dataframe

```python
# sorting with a single value
result = df.sort_values('my_col_a', ascending = True)

# sorting by multiple values
result = df.sort_values(['my_col_a', 'my_col_b'], ascending=[1, 0])
```

## Grouping data

### Grouping counting rows

```python
grouped_data = df.groupby(['column_name_to_group_by']).size().reset_index(name='counts')
```
