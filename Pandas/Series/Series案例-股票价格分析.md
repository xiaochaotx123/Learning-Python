给定某股票连续10个交易日的收盘价Series：  
- 计算每日收益率（当日收盘价 / 前日收盘价 - 1）
- 找出收益率最高和最低的日期
- 计算波动率（收益率的标准差）
```python
prices_value = [102.3, 103.5, 105.1, 104.8, 106.2, 107.0, 106.5, 108.1, 109.3, 110.2]
prices_index = pd.date_range("2023-01-01", periods = 10)
prices = pd.Series(prices_value, prices_index)
```
#### pd.date_range("起始日期", periods = n) 生成一个一起始日期开始的n个日期

#### pct_chage() 计算百分比变化
pct_change()是Pandas中Series和DatFrame的一个方法，用于计算每一个元素相对于前一个元素的百分比变化率（涨跌幅）  
计算公式是：（当前值 - 上一个值）/ 上一个值 × 100%

```python
# 计算每日收益率
yield_rate = prices.pct_change()
print(yield_rate)
# 输出：
"""
2023-01-01         NaN
2023-01-02    0.011730
2023-01-03    0.015459
2023-01-04   -0.002854
2023-01-05    0.013359
2023-01-06    0.007533
2023-01-07   -0.004673
2023-01-08    0.015023
2023-01-09    0.011101
2023-01-10    0.008234
Freq: D, dtype: float64
"""
```

```python
# 找出收益率最高和最低的日期
# sorted_yieldrate = yield_rate.sort_values(ascending = False)
#
# # 输出收益率最高的日期
# print(sorted_yieldrate.index[0])
#
# sorted_yieldrate = yield_rate.sort_values()
#
# # 输出收益率最低的日期
# print(sorted_yieldrate.index[0])

# 可以直接使用方法找出最高和最低
print(f"收益率最高的日期：{sorted_yieldrate.idxmax()}")
print(f"收益率最低的日期：{sorted_yieldrate.idxmin()}")
```

```python
# 计算波动率（收益率的标准差）
print(sorted_yieldrate.std())
```
