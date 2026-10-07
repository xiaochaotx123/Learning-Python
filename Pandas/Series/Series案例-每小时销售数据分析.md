某商店每小时销售额Series：
- 按天采样计算每日总销售额
- 计算每天营业时间（8:00 - 22:00）和非营业时间的销售额比例
- 找出销售额最高的3个小时
```python
np.random.seed(42)
hourly_sales_values = np.random.randint(0, 100, 24)
hourly_sales_index = pd.date_range("2025-01-01", periods = 24, freq = "h")
hourly_sales = pd.Series(hourly_sales_values, hourly_sales_index)

2025-01-01 00:00:00    51
2025-01-01 01:00:00    92
2025-01-01 02:00:00    14
2025-01-01 03:00:00    71
2025-01-01 04:00:00    60
2025-01-01 05:00:00    20
2025-01-01 06:00:00    82
2025-01-01 07:00:00    86
2025-01-01 08:00:00    74
2025-01-01 09:00:00    74
2025-01-01 10:00:00    87
2025-01-01 11:00:00    99
2025-01-01 12:00:00    23
2025-01-01 13:00:00     2
2025-01-01 14:00:00    21
2025-01-01 15:00:00    52
2025-01-01 16:00:00     1
2025-01-01 17:00:00    87
2025-01-01 18:00:00    29
2025-01-01 19:00:00    37
2025-01-01 20:00:00     1
2025-01-01 21:00:00    63
2025-01-01 22:00:00    59
2025-01-01 23:00:00    20
Freq: h, dtype: int32
```

```python
# 按天采样计算每日的总销售额
daily_sales = hourly_sales.resample("D").sum()
print(daily_sales)
```

```python
# 计算每天营业时间和非营业时间的销售额比例
# business_sales = hourly_sales.values[0:23:1].sum() - hourly_sales.values[0:8:1].sum()
# business_sales_rate = business_sales / hourly_sales.values.sum()
# # print(round(business_sales_rate, 10))
# notbusiness_sales = hourly_sales.values.sum() - business_sales
# notbusiness_sales_rate = notbusiness_sales / hourly_sales.values.sum()
# # print(round(notbusiness_sales_rate, 10))
# # 
# # print(business_sales_rate / notbusiness_sales_rate)


business_sales = hourly_sales.values[8:23:1].sum()
business_sales_rate = business_sales / hourly_sales.values.sum()
# print(business_sales)
# print(business_sales_rate)
notbusiness_sales = hourly_sales.values.sum() - business_sales
notbusiness_sales_rate = notbusiness_sales / hourly_sales.values.sum()
print(business_sales_rate / notbusiness_sales_rate)
```

```python
# 找出销售额最高的三个小时
# three_hourly_sales = hourly_sales.rolling(3).sum()
# max_three_sales = three_hourly_sales.idxmax()
# print(pd.date_range(end = max_three_sales, periods = 3, freq = "h"))

# sorted_three_hourly_sales = three_hourly_sales.sort_values(ascending = False)
# print(sorted_three_hourly_sales.index[0:3:1])

sorted_hourly_sales = hourly_sales.sort_values(ascending = False)
# print(sorted_hourly_sales[0:3:1])
print(sorted_hourly_sal.index[0:3:1])
```

