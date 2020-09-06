# Data manipulation: Time series

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
datetime_string = "21 May, 1985"
date_time = datetime.strptime(date_string, "%d %B, %Y")
```

Get a datetime from string automaticly

```python
from dateutil import parser
datetime_string = "21 May, 1985"
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
index = pd.DatetimeIndex(['2013-05-01', '2014-05-01', '2015-07-04', '2016-05-01'])
data = pd.Series([0, 1, 2, 3], index=index)
```

