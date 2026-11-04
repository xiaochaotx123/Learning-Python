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

#### csv文件中日期转换
正常这么读入文件：
```python
df = pd.read_csv("Pandas_Study_Data/weather.csv")
```
但是如果需要处理这个文件的日期信息等，因为一开始的date是字符串类型，所以需要加上：
```python
df["datetime"] = pd.to_datetime(df["date"])
```
或者直接覆盖：
```python
df["date"] = pd.to_datetime(df["date"])
```
将date的字符串类型转换为datetime64[us]类型

但是可以直接在读入文件的时候使用参数将字符串类型的日期信息直接修改为datetime64[us]类型
#### parse_dates
parse_dates是pd.read_csv()的一个参数，用于在读取CSV时直接将某些列解析为日期时间类型，省去了读完之后再pd.to_datetime()的步骤

```python
df = pd.read_csv("Pandas_Study_Data/weather.csv", parse_dates = ["date"])
```

- 在90%的场景下，只要CSV里的日期格式是标准的（比如 2026-10-12 或 2026/10/12）无脑用parse_dates，它是最优雅、最高效的
- 当你的日期数据非常脏（比如有的写2026-10-12，有的写2026年10月12日，有的甚至写未知），此时parse_dates会直接把无法解析的变成NaT甚至报错。这时候，就需要来手动清洗和容错（比如df["date"] = pd.to_datetime(df["date"], format="%Y-%m-%d", errors="coerce")）

```python
df = pd.read_csv("Pandas_Study_Data/weather.csv", parse_dates = ["date"])
df["week"] = df["date"].dt.day_name()
```

#### 将日期作为行索引获取单个元素或者切片获取元素
```python
df = pd.read_csv("Pandas_Study_Data/weather.csv", parse_dates = ["date"])

# 这个inplace = True参数使得直接修改，不需要再df = df.set_index("date")
df.set_index("date", inplace = True)

# 直接显式索引获取数据
print(df.loc["2012-01-01"])
# precipitation        0.0
# temp_max            12.8
# temp_min             5.0
# wind                 4.7
# weather          drizzle
# Name: 2012-01-01 00:00:00, dtype: object

# 切片获取数据
print(df.loc["2012-01-01" : "2012-01-25"])
#             precipitation  temp_max  temp_min  wind  weather
# date
# 2012-01-01            0.0      12.8       5.0   4.7  drizzle
# 2012-01-02           10.9      10.6       2.8   4.5     rain
# ...
# 2012-01-24            1.2       9.4       4.4   3.2  drizzle
# 2012-01-25            0.0       8.3       2.2   2.7      fog
```

 #### 时间间隔
 ```python
ts1 = pd.Timestamp("2006-07-28")
ts2 = pd.Timestamp("2026-10-12")
ts3 = ts2 - ts1
print(ts3) # 7381 days 00:00:00
print(type(ts3)) # <class 'pandas.Timedelta'>

df = pd.read_csv("Pandas_Study_Data/weather.csv", parse_dates = ["date"])
df["delta"] = df["date"] - df["date"][0]
df.set_index(["delta"], inplace = True)
print(df)
              # date  precipitation  temp_max  temp_min  wind  weather
# delta
# 0 days  2012-01-01            0.0      12.8       5.0   4.7  drizzle
# 1 days  2012-01-02           10.9      10.6       2.8   4.5     rain
# ...
# 33 days 2012-02-03            0.0       5.6      -2.2   1.8      fog
# 34 days 2012-02-04           13.8       9.4       3.9   7.2     rain

print(df.loc["3 days" : "7 days"])
#              date  precipitation  temp_max  temp_min  wind weather
# delta
# 3 days 2012-01-04           20.3      12.2       5.6   4.7    rain
# 4 days 2012-01-05            1.3       8.9       2.8   6.1    rain
# 5 days 2012-01-06            0.0       7.2       1.1   3.4     fog
# 6 days 2012-01-07            5.1       8.3       3.3   2.1    rain
# 7 days 2012-01-08            0.0       6.7      -1.1   1.5     sun
```

#### 生成时间序列
```python
# days = pd.date_range("2026-10-12", "2026-10-20")
# print(days)
# DatetimeIndex(['2026-10-12', '2026-10-13', '2026-10-14', '2026-10-15',
#                '2026-10-16', '2026-10-17', '2026-10-18', '2026-10-19',
#                '2026-10-20'],
#               dtype='datetime64[us]', freq='D')
# days = pd.Series(days)
# print(days)
# 0   2026-10-12
# 1   2026-10-13
# 2   2026-10-14
# 3   2026-10-15
# 4   2026-10-16
# 5   2026-10-17
# 6   2026-10-18
# 7   2026-10-19
# 8   2026-10-20
# dtype: datetime64[us]


# 参数freq设置时间间隔
days = pd.date_range("2026-10-12", "2026-10-20", freq = "3D")
print(days) # DatetimeIndex(['2026-10-12', '2026-10-15', '2026-10-18'], dtype='datetime64[us]', freq='3D')
days = pd.date_range("2026-10-12", "2026-10-20", freq = "W")
print(days) # DatetimeIndex(['2026-10-18'], dtype='datetime64[us]', freq='W-SUN')

# 参数periods设置长度
days = pd.date_range("2026-10-12", periods = 5, freq = "2D")
print(days)
# DatetimeIndex(['2026-10-12', '2026-10-14', '2026-10-16', '2026-10-18',
#                '2026-10-20'],
#               dtype='datetime64[us]', freq='2D')
```

#### 重新采样
```python
# 重新采样
df = pd.read_csv("Pandas_Study_Data/weather.csv", parse_dates = ["date"])
df.set_index(["date"], inplace = True)
print(df[["temp_max", "temp_min"]].resample("ME").mean())
            # temp_max  temp_min
# date
# 2012-01-31   7.86129  1.829032
# 2012-02-29   7.22500  0.700000


x = df[["temp_max", "temp_min"]].resample("ME").mean()
x.reset_index(inplace = True)
print(x)
        # date  temp_max  temp_min
# 0 2012-01-31   7.86129  1.829032
# 1 2012-02-29   7.22500  0.700000
```
