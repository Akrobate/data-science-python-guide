# Data manipulation: Time series

## Panda Time Serie indexed by time

```python
index = pd.DatetimeIndex(['2013-05-01', '2014-05-01', '2015-07-04', '2016-05-01'])
data = pd.Series([0, 1, 2, 3], index=index)
```

