给定某城市一周每天的最高温度Series，完成一下任务：
- 找出温度超过30度的天数
- 计算平均温度
- 将温度从高到低排序
- 找出温度变化最大的两天
```python
temperatures = pd.Series([28, 31, 29, 32, 30, 27, 33],
               index = ["周一", "周二", "周三", "周四", "周五", "周六", "周日"])
```

```python
# 计算温度超过30度的天数
print(f"温度超过30度的天数：{len(temperatures[temperatures > 30])}")

# 具体是哪些天
# print(temperatures[temperatures > 30])
# print(temperatures[temperatures > 30].index)
print(list(temperatures[temperatures > 30].index))
```
```python
# 计算平均气温
print(f"平均气温：{round(temperatures.mean(), 3)}")
```

#### ascending = False
sort_values()将Series中的数据默认按照values从小到大排序，sort_index()将Series中的数据默认按照index从小到大排序。
排序的依据Unicode码点的。sort_valuesh()和sort_index()都可以使用参数ascending = False来将排序方式修改为从大到小排序。
```python
# 将温度从高到低排序
sorted_temperatures = temperatures.sort_values(ascending = False)
print(sorted_temperatures)
```

#### diff() 计算当前值与前一个值的差
```python
print(temperatures.diff())
# 输出：
"""
周一    NaN    # 第一个元素没有前一个元素，所以差值是NaN
周二    3.0
周三   -2.0
周四    3.0
周五   -2.0
周六   -3.0
周日    6.0
dtype: float64
"""
```

```python
# 将温度从高到低排序
diffs = temperatures.diff()
sorted_diffs = diffs.sort_values(ascending = False)
# print(sorted_diffs)
# print(sorted_diffs.index[0:2:1])
print(sorted_diffs.index[0:2:1].tolist())
print(list(sorted_diffs.index[0:2:1]))
# print(*sorted_diffs.index[0:2:1].tolist())
```
