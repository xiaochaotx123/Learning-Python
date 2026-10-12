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
|ts.is_quarter_start|判断时间戳的日期是否是该季度的第一天|
|ts.is_quarter_end|判断时间戳的日期是否是该季度的最后一天|
|ts.is_month_start|判断时间戳的日期是否是该月的第一天|
|ts.is_month_start|判断时间戳的日期是否是该月的最后一天|
|ts.day_name()|求时间戳的日期是星期几|
|ts.to_period("Y")|求时间戳的日期的年时间段|
|ts.to_period("Q")|求时间戳的日期的季度时间段|
|ts.to_period("M")|求时间戳的日期的月时间段|
|ts.to_period("W")|求时间戳的日期的周时间段|
|ts.to_period("D")|求时间戳的天时间段|
|ts.to_period("h")|求时间戳的小时时间段|

在Pandas中，一周的结束日是该周的星期天  
ts.to_period("W")输出格式：该周起始日/该周结束日，所以2026-10-12是这一周的起始日，2026-10-18是该周的结束日，中间用 / 隔开
```python
print(ts.year) # 2026
print(ts.quarter) # 4
print(ts.month) # 10
print(ts.day) # 12
print(ts.hour) # 18
print(ts.minute) # 4
print(ts.second) # 0

print(ts.is_leap_year) # False
print(ts.is_year_start) # False
print(ts.is_year_end) # False
print(ts.is_quarter_start) # False
print(ts.is_quarter_end) # False
print(ts.is_month_start) # False
print(ts.is_month_start) # False

print(ts.day_name()) # Monday
print(ts.to_period("Y")) # 2026
print(ts.to_period("Q")) # 2026Q4
print(ts.to_period("M")) # 2026-10
print(ts.to_period("W")) # 2026-10-12/2026-10-18
print(ts.to_period("D")) # 2026-10-12
print(ts.to_period("h")) # 2026-10-12 18:00
```

#### pd.to_datetime()
pd.to_datetime()是pandas中将各种格式的数据批量转换为日期时间类型的核心函数。与pd.Timestamp()（处理单个值）不同，pd.to_datetime() 擅长处理数组、列表、Series、DataFrame 列等批量数据
```python
# 字符串转化为日期类型
string_date = "2026-10-12 18:46"
dt = pd.to_datetime(string_date)

print(type(string_date)) # <class 'str'>
print(type(dt)) # <class 'pandas.Timestamp'>

print(dt.day_name()) # Monday
```

#### 为什么直接使用df["datetime"].day_name()会报错
day_name()不是pd.Series的方法，而是.dt访问器上的方法。


#### 为什么加上.dt就可以了？
.dt是pandas中Series的日期时间属性访问器（accessor）。当Series的dtype是datetime64时，可以通过.dt快速提取各种日期时间组件，避免了逐行遍历的低效操作。单个Timestamp直接调用.day_name()，一列数据（Series）必须经过.dt 再调用.day_name()。

```python
df = pd.DataFrame(
    {
        "sales" : [100, 200, 300],
        "date" : ["20250601", "20250602", "20250603"],
    }
)
print(df)
#    sales      date
# 0    100  20250601
# 1    200  20250602
# 2    300  20250603

df["datetime"] = pd.to_datetime(df["date"])
print(df)
#    sales      date   datetime
# 0    100  20250601 2025-06-01
# 1    200  20250602 2025-06-02
# 2    300  20250603 2025-06-03

print(df.info()) # datetime这一列的数据类型是用于表示时间点的数据类型
# ...
#  2   datetime  3 non-null      datetime64[us]
# ...


print(type(df["datetime"])) # <class 'pandas.Series'>
# 这个df["datetime"]是Series类型
# 所以如果直接使用df["datetime"].day_name()会报错！
# 需要加上.dt处理

print(df["datetime"].dt.day_name())
# 0     Sunday
# 1     Monday
# 2    Tuesday
# Name: datetime, dtype: str

df["week"] = df["datetime"].dt.day_name()
print(df)
#    sales      date   datetime     week
# 0    100  20250601 2025-06-01   Sunday
# 1    200  20250602 2025-06-02   Monday
# 2    300  20250603 2025-06-03  Tuesday

print(df["datetime"].dt.year)
# 0    2025
# 1    2025
# 2    2025
# Name: datetime, dtype: int32
```
