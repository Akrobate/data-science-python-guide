# Data manipulation - Time series

## Python datetime

Print current datetime

```python
from datetime import datetime
now = datetime.now()
date_time = now.strftime("%m/%d/%Y %H:%M:%S")
print(date_time)
```
Datetime from a timestamp, and timestamp from a datetime

```python
from datetime import datetime
timestamp = 1458987543
date_time = datetime.fromtimestamp(timestamp)
print(date_time)

timestamp_regenerated = datetime.timestamp(date_time)
print(timestamp_regenerated)
```

Get a datetime from string

```python
from datetime import datetime
date_string = "21 May, 1985"
date_time = datetime.strptime(date_string, "%d %B, %Y")
```

Get a datetime from string automaticly

```python
from dateutil import parser
date_string = "21 May, 1985"
date_time = parser.parse(date_string)
```

## Panda transform string to Timestamp object

```python
import pandas as pd
datetime_string = "21 May, 1985"
date = pd.to_datetime(datetime_string)
```

## Panda Time Serie indexed by time

```python
import pandas as pd
index = pd.DatetimeIndex(['2013-05-01', '2014-05-01', '2015-07-04', '2016-05-01'])
data = pd.Series([0, 1, 2, 3], index=index)
```

### Using existing column to define as time index
```python
import pandas as pd

# my_dataframe have a colum date with string date value inside
my_dataframe['date'] = pd.to_datetime(my_dataframe['date'])
my_dataframe.set_index('date', inplace=True)
```

## Panda generate range of dates

```python
import pandas as pd
data = pd.date_range('1998-03-10', '1998-03-15', freq='D')
```
Possible frequencies:

* 'H' - hourly
* 'D' - Daily
* 'B' - Buisiness daily
* 'W' - Weekly
* 'M' - Monthly
* 'Q' - Quarterly
* 'A' - Annual

## Panda filter dataframe by indexed date range

```python
import pandas as pd

# my_dataframe an index of datetime type

# select all data that match year: 2020
df_2020 = my_dataframe['2020':'2020']
```

## Pandas resample time data

### Resample and count lines

```python
import pandas as pd
my_dataframe = my_dataframe.set_index('datetime_column')

my_dataframe = my_dataframe.datetime_column.resample('D').count() 
```

### Resample and sum values

```python
import pandas as pd
my_dataframe = my_dataframe.set_index('datetime_column')

summed_serie = my_dataframe.serie_to_sum.resample('D').sum() 
```

### Resample with cutom method

```python
import pandas as pd
my_dataframe = my_dataframe.set_index('datetime_column')

def custom_sum(array_like):
    return np.sum(array_like)

summed_serie = my_dataframe.serie_to_sum.resample('D').apply(custom_sum)
```

