```python
import pandas as pd
```

#### pd.Timestamp()
pd.Timestamp()是pandas库中用于表示单个时间戳的核心类。它是Python标准库datetime.datetime的pandas替代品，功能更强大、更灵活。
```python
ts = pd.Timestamp("2026-10-12 18:04")
print(ts) # 2026-10-12 18:04:00       自动将后面的秒补充为 00
print(type(ts)) # <class 'pandas.Timestamp'>
```

#### 时间戳的一些基本属性
|属性|说明|
|----|----|
|ts.year|求时间戳的年|
|ts.quarter|求时间戳的季度|
|ts.month|求时间戳的月|
|ts.day|求时间戳的日|
|ts.hour|求时间戳的小时|
|ts.minute|求时间戳的分钟|
|ts.second|求时间戳的秒|
|ts.is_leap_year|判断时间戳的年是否是闰年|
|ts.is_year_start|判断时间戳的日期是否是该年的第一天|
|ts.is_year_end|判断时间戳的日期是否是该年的最后一天|
