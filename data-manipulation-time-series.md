# Data manipulation - Time series

- [Data manipulation - Time series](#data-manipulation---time-series)
  * [Python datetime](#python-datetime)
  * [Panda transform string to Timestamp object](#panda-transform-string-to-timestamp-object)
  * [Panda Time Serie indexed by time](#panda-time-serie-indexed-by-time)
    + [Using existing column to define as time index](#using-existing-column-to-define-as-time-index)
  * [Panda generate range of dates](#panda-generate-range-of-dates)
  * [Panda filter dataframe by indexed date range](#panda-filter-dataframe-by-indexed-date-range)
  * [Pandas resample time data](#pandas-resample-time-data)
    + [Resample and count lines](#resample-and-count-lines)
    + [Resample and sum values](#resample-and-sum-values)
    + [Othe possible method on resampled data](#othe-possible-method-on-resampled-data)
    + [Resample with cutom method](#resample-with-cutom-method)
- [Possible frequencies:](#possible-frequencies-)

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

Important: To prevent errors while converting to datetime use errors parameter
For instance errors='coerce' will put NaT values in invalid values

```python
import pandas as pd

# my_dataframe have a colum date with string date value inside
my_dataframe['date'] = pd.to_datetime(my_dataframe['date'], errors='coerce')
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

Refer to the full list in the bottom of page

## Panda filter dataframe by indexed date range

```python
import pandas as pd

# my_dataframe an index of datetime type

# select all data that match year: 2020
df_2020 = my_dataframe.loc['2020':'2020']
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

### Othe possible method on resampled data

* resample('D').mean()
* resample('D').first()
* resample('D').last()

### Resample with cutom method

```python
import pandas as pd
my_dataframe = my_dataframe.set_index('datetime_column')

def custom_sum(array_like):
    return np.sum(array_like)

summed_serie = my_dataframe.serie_to_sum.resample('D').apply(custom_sum)
```

# Possible frequencies:

* B         business day frequency
* C         custom business day frequency (experimental)
* D         calendar day frequency
* W         weekly frequency
* M         month end frequency
* SM        semi-month end frequency (15th and end of month)
* BM        business month end frequency
* CBM       custom business month end frequency
* MS        month start frequency
* SMS       semi-month start frequency (1st and 15th)
* BMS       business month start frequency
* CBMS      custom business month start frequency
* Q         quarter end frequency
* BQ        business quarter endfrequency
* QS        quarter start frequency
* BQS       business quarter start frequency
* A         year end frequency
* BA, BY    business year end frequency
* AS, YS    year start frequency
* BAS, BYS  business year start frequency
* BH        business hour frequency
* H         hourly frequency
* T, min    minutely frequency
* S         secondly frequency
* L, ms     milliseconds
* U, us     microseconds
* N         nanoseconds