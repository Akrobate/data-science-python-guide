# Data manipulation

- [Data manipulation](#data-manipulation)
  * [Creating and setting panda DataFrame](#creating-and-setting-panda-dataframe)
  * [Managing indexes](#managing-indexes)
  * [Filtering data in panda](#filtering-data-in-panda)
  * [Join data](#join-data)
  * [Concat dataframe rows / cols](#concat-dataframe-rows---cols)
  * [Append data to dataframe](#append-data-to-dataframe)
  * [Concat dataframe rows of splitted column value](#concat-dataframe-rows-of-splitted-column-value)
  * [Melt / Pivot data](#melt---pivot-data)
    + [Melt dataframe](#melt-dataframe)
    + [Pivot dataframe](#pivot-dataframe)
  * [Manipulating columns as string](#manipulating-columns-as-string)
  * [Rename columns names](#rename-columns-names)
  * [Changing columns types](#changing-columns-types)
    + [Object to categorical](#object-to-categorical)
    + [Object to numeric type](#object-to-numeric-type)
  * [Sorting panda dataframe](#sorting-panda-dataframe)
    + [Sorting on columns values](#sorting-on-columns-values)
    + [Sorting on index](#sorting-on-index)
  * [Grouping data](#grouping-data)
    + [Grouping counting rows](#grouping-counting-rows)
  * [Removing data from dataframe](#removing-data-from-dataframe)
    + [Remove a row by index value](#remove-a-row-by-index-value)
    + [Remove a row by row number](#remove-a-row-by-row-number)
    + [Remove a column](#remove-a-column)


## Creating and setting panda DataFrame

This two example will generate exactly the same dataframe

```python
import pandas as pd
example_data = {
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
}
df = pd.DataFrame(example_data)
```

```python
import pandas as pd
example_data = [
    {
        'column1': 1,
        'column2':'A'
    },
    {
        'column1': 2,
        'column2':'B'
    },
    {
        'column1': 3,
        'column2':'C'
    },
]
df = pd.DataFrame(example_data)
```

## Managing indexes

```python
# Setting index
my_df = my_df.set_index('column name')

# resetting index
my_df = my_df['column name'].reset_index()
```

## Selecting columns from a dataset

```python
import pandas as pd
example_data = {
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
    'column3':['A1', 'B2', 'C3']
}

df = pd.DataFrame(example_data)

# Subselection of dataframe
df_selection = df[['column1', 'column2']]

# New dataframe from column
df_new = df[['column1', 'column2']].copy()
```


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

## Filtering data in panda

Boolean Filtering

```python
import pandas as pd
df = pd.DataFrame({
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
})
# Will return the first and the third row
df[[True, False, True]]
```

Creating boolean filter

```python
import pandas as pd
df = pd.DataFrame({
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
})

# boolean_filter will contain [False, True, True]
boolean_filter = df.column1 >= 2

# Will return the two last rows
df[boolen_filter]
```

Filtering using loc.

```python
import pandas as pd
df = pd.DataFrame({
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
})
# Will return the two last rows
df.loc[df.column1 >= 2]

# Will return the two last rows and select the column2
df.loc[df.column1 >= 2, ['column2']]
```

Filtering using iloc.

```python
import pandas as pd
df = pd.DataFrame({
    'column1': [1, 2, 3],
    'column2':['A', 'B', 'C']
})
# Will return the first row
df.iloc[0]

# Will return the first row and select the column2
df.iloc[0, [1]]
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

## Append data to dataframe

```python
import pandas as pd

example_data = {
    'column1': [1,2],
    'column2': ['A', 'B']
}

example_row_to_append = {
    'column1': [3],
    'column2': ['C']
}

dataframe = pd.DataFrame(example_data)
appendeted_dataframe = dataframe.append(pd.DataFrame(example_row_to_append), ignore_index=True)
appendeted_dataframe
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
        result = result.append(temporary_dataframe, ignore_index=True)

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

## Rename columns names

```Python
import numpy as np
import pandas as pd
from sklearn.datasets import load_iris

iris = load_iris()
df = pd.DataFrame(
    data = np.c_[iris.data, iris.target],
    columns= iris.feature_names + ['target']
)

df.rename(columns = { 'target':'specie_name' }, inplace = True)
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

### Sorting on columns values

```python
# sorting with a single value
result = df.sort_values('my_col_a', ascending = True)

# sorting by multiple values
result = df.sort_values(['my_col_a', 'my_col_b'], ascending=[1, 0])
```

### Sorting on index

```python
# sorting rows on index
result = df.sort_index(axis = 0, ascending = True)

# Interesting trick sort_index with axis to 1 will sort columns names in dataframe
result = df.sort_index(axis = 1, ascending = True)
```

## Grouping data

### Grouping counting rows

```python
grouped_data = df.groupby(['column_name_to_group_by']).size().reset_index(name='counts')
```

## Removing data from dataframe

### Remove a row by index value

```python
import pandas as pd
data = {'col_1': ['A', 'B', 'C'], 
        'col_2': [1, 2, 3]}
df = pd.DataFrame(data, index = ['index_a', 'index_b', 'index_c'])

df.drop(['index_a', 'index_b'])
```

### Remove a row by row number

```python
import pandas as pd
data = {'col_1': ['A', 'B', 'C'], 
        'col_2': [1, 2, 3]}
df = pd.DataFrame(data, index = ['index_a', 'index_b', 'index_c'])

# Will remove first row
df.drop(df.index[0])
```

### Remove a column

```python
import pandas as pd
data = {'col_1': ['A', 'B', 'C'], 
        'col_2': [1, 2, 3]}
df = pd.DataFrame(data, index = ['index_a', 'index_b', 'index_c'])

df.drop('col_2', axis=1)
```
