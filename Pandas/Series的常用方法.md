### 一、查看数据方法
#### 1. head(n) 查看前 n 行
默认 5 行
```python
import pandas as pd
s = pd.Series([10, 20, 30, 40, 50, 60, 70, 80])

print(s.head())
# 输出：
"""
0    10
1    20
2    30
3    40
4    50
dtype: int64
"""

print(s.head(3))
# 输出：
"""
0    10
1    20
2    30
dtype: int64
"""
```

#### 2. tail(n) 查看后 n 行
默认 5 行
```python
print(s.tail())
# 输出：
"""
3    40
4    50
5    60
6    70
7    80
dtype: int64
"""

print(s.tail(2))
# 输出：
"""
6    70
7    80
dtype: int64
"""
```

### 二、统计方法
#### 3. count() 非缺失值数量
```python
import pandas as pd

s = pd.Series([1, 2, None, 4, 5])
print(s.count()) # 输出：4（忽略None）
```

#### 4. sum() 求和
```python
print(s.sum()) # 输出：12.0（因为存在None，所以是float64）
```

#### 5. mean() 平均值
```python
print(s.mean()) # 输出：3.0
```

#### 6. min()/max() 最小值/最大值
```python
print(s.min()) # 输出：1.0
print(s.max()) # 输出：5.0
```

#### 7. var() 方差
```python
print(s.var())
```

#### 8. std() 标准差
```python
print(s.std())
```

#### 9. median() 中位数
```python
s = pd.Series([9, 1, 3, 7, 5])
print(s.median()) # 输出：5.0
```

#### 10. mode() 众数
```python
s = pd.Series([1, 2, 2, 3, 3, 4])
print(s.mode())
# 输出：
"""
0    2
1    3
dtype: int64
"""
```

#### 11. quantile(q) 分位数
q 取 0~1 之间
```python
s = pd.Series([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

print(s.quantile(0.25)) # 输出：3.25
print(s.quantile(0.5)) # 输出：5.5
print(s.quantile(0.75)) # 输出：7.75
```

#### 12 describe() 综合统计信息
```python
print(s.describe())
# 输出：
"""
count    10.00000
mean      5.50000
std       3.02765
min       1.00000
25%       3.25000
50%       5.50000
75%       7.75000
max      10.00000
dtype: float64
"""
```

### 三、唯一值与重复值方法
#### 13. unique() 获取去重后的数组
返回Numpy数组
```python
s = pd.Series([1, 2, 2, 3, 3, 3, 4])
print(s.unique()) # 输出：[1 2 3 4]
```

#### 14. nunique() 唯一值的个数
```python
print(s.nunique()) # 输出：4
```

#### 15. value_counts() 每个唯一值的出现次数
非常的试用！默认按照频次降序排序
```python
print(s.value_counts())
# 输出：
"""
3    3
2    2
1    1
4    1
Name: count, dtype: int64
"""
```

#### 16. drop_duplicates() 去除重复项
保留第一次出现的值
```python
print(s.drop_duplicates())
# 输出：
"""
0    1
1    2
3    3
6   4
dtype: int64
"""
```


### 四、排序方法
17. sort_values() 按值排序
```python
s = pd.Series([3, 1, 4, 1, 5, 9, 2, 6])

# 升序（默认）
print(s.sort_values())
# 输出：
"""
1    1
3    1
6    2
0    3
2    4
4    5
7    6
5    9
dtype: int64
"""

# 降序
print(s.sort_values(ascending = False))
# 输出：
"""
5    9
7    6
4    5
2    4
0    3
6    2
3    1
1    1
dtype: int64
"""
```

#### 18. sort_index() 按索引排序
```python
s = pd.Series([10, 20, 30], index = ["C", "A", "B"])
print(s.sort_index())
# 输出：
"""
A    20
B    30
C    10
dtype: int64
"""
```
### 五、判断与筛选方法
#### 19. isin(values) 判断元素是否在集合中
```python
s = pd.Series([1, 2, 3, 4, 5])
print(s.isin([2, 6, 4]))
# 输出：
"""
0    False
1     True
2    False
3     True
4    False
dtype: bool
"""
```

#### 20. isna() 判断是否为缺失值；isna().sum() 统计缺失值的个数
```python
import pandas as pd
import numpy as np
s = pd.Series([1, 2, None, 4, np.nan])

print(s)
# 输出：
"""
0    1.0
1    2.0
3    NaN
4    4.0
5    NaN
dtype: float64
"""

print(s.isna())
# 输出：
"""
0    False
1    False
2     True
3    False
4     True
5    False
dtype: bool
"""

print(s.isna().sum()) # 输出：2
```

### 六、替换方法
#### 21. replace() 替换值
```python
#%%
import pandas as pd
import numpy as np

s = pd.Series([1, 2, 3, 4, 5])

# 单个替换值
print(s.replace(2, 20)) # s 没有发生变化
# 输出：
"""
0    1
1   20
2    3
3    4
4    5
dtype: int64
"""

# 多个值替换（字典形式）
print(s.replace({1 : 10, 3 : 30, 5 : 50}))
# 输出：
"""
0    10
1     2
2    30
3     4
4    50
dtype: int64
"""

# 替换缺失值
s1 = pd.Series([1, 2, None, 4, None])
print(s1.replace(np.nan, 999))
# 输出：
"""
0      1.0
1      2.0
2    999.0
3      4.0
4    999.0
dtype: float64
"""
```
