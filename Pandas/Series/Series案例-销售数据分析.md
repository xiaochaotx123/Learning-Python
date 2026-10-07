某产品过去12个月的销售量Series：
- 计算季度平均销量（每三个月为一个季度）
- 找出销量最高的月份
- 计算月环比增长率
- 找出连续增长的超过两个月的月份
```python
sales_value = [120, 135, 145, 160, 155, 170, 180, 175, 190, 200, 210, 220]
sales_index = pd.date_range("2022-01-01", periods = 12, freq = "ME")
sales = pd.Series(sales_value, sales_index)
```
#### resample() 时间序列重采样
resample()是Pandas中专门用于时间序列重采样的方法。它可以将时间序列数据从一个频率转化为另一个频率。
|频率|含义|
|---|----|
|D|天|
|MS|月初|
|ME|月末|
|QS|季初|
|QE|季末|
|YS|年初|
|YE|年末|
```python
# 计算季度平均销量（每三个月为一个季度）
quarterly_sales = sales.resample("QE").mean()
print(quarterly_sales)
# 输出：
"""
2022-03-31    133.333333
2022-06-30    161.666667
2022-09-30    181.666667
2022-12-31    210.000000
Freq: QE-DEC, dtype: float64
"""
```

```python
# 找出销量最高的月份
print(sales.idxmax())
```

```python
# 计算月环比增长率
percent_sales = sales.pct_change()
print(percent_sales)
# 输出：
"""
2022-01-31         NaN
2022-02-28    0.125000
2022-03-31    0.074074
2022-04-30    0.103448
2022-05-31   -0.031250
2022-06-30    0.096774
2022-07-31    0.058824
2022-08-31   -0.027778
2022-09-30    0.085714
2022-10-31    0.052632
2022-11-30    0.050000
2022-12-31    0.047619
Freq: ME, dtype: float64
"""
```

#### rolling() 滑动窗口计算
rolling()是Pandas中用于滚动窗口的计算的方法。它在时间序列或普通序列上滑动一个固定大小的窗口，对窗口内的数据执行聚合操作。

```python
# 找出连续增长的超过两个月的月份
bool_percent_sales = percent_sales > 0
is_percent_sales = bool_percent_sales.rolling(3).sum() == 3
print(is_percent_sales[is_percent_sales].index.tolist())
```
