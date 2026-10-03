```python
# Series的创建
import pandas as pd

# 1. 通过列表创建（默认索引 0，1，2，...）
s1 = pd.Series([1, 2, 3, 4, 5])
print(s1)

# 2. 自定义索引
s2 = pd.Series([1, 2, 3, 4, 5], index = ["A", "B", "C", "D", "E"])
print(s2)

# 3. 定义 name （列名）
s3 = pd.Series([1, 2, 3, 4, 5], index = ["A", "B", "C", "D", "E"], name = "月")
print(s3)

# 4. 标量 + index：用同一个值填充所有行
s4 = pd.Series(100, index = ["A", "B", "C", "D", "E"])
print(s4)

# 5. 指定 dtype 数据类型
s5 = pd.Series([1, 2, 3, 4, 5], index = ["A", "B", "C", "D", "E"], dtype = "float")
print(s5)
```

```python
# 通过字典来创建
s = pd.Series({"A" : 1, "B" : 2, "C" : 3, "D" : 4, "E" : 5})
print(s)

# 通过已有 Series + 指定 index 筛选/重排
s1 = pd.Series(s, index = ["A", "B", "C"])
print(s1)

# index 中包含字典没有的 key → 该位置填充 Nan
s2 = pd.Series(s, index = ["A", "B", "F", "D"])
print(s2)
```
