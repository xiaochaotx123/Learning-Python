```python
import pandas as pd
import numpy as np
```

#### np.nan —— Numpy的"非数字"
np.nan 是IEEE 754浮点数标准中定义的NaN(Not a Number)
- 类型：float
- 本质：是一个特殊的浮点数值
- 适用场景：数值计算、Numpy/Pandas的数值列
```python
x = np.nan
print(type(x))  # <class 'float'>
print(x + 1)    # nan（不会报错，但结果仍是 nan）
print(x == x)   # False（NaN 不等于任何值，包括它自己！）

np.nan == np.nan # False
```
这就是为什么pandas提供了isna()/isnull()方法来检测缺失值，而不是 ==

#### None —— Python原生的空值
None是Python内置的单例对象，表示"没有值"或"空"
- 类型：NoneType
- 本质：是一个Python对象，占用内存
- 适用场景：纯Python代码、混合类型数据
```python
x = None
print(type(x))  # <class 'NoneType'>
```
在数值计算中会报错（None + 1 → TypeError）  
在Pandas中，None存入object类型的列时保持为None，但存入数值列表时会自动转换为NaN

#### pd.NA —— Pandas的统一缺失值(1.0+)
pd.NA时Pandas从1.0版本开始引入的实验性缺失值标记，旨在统一None和np.nan
- 类型：pd.NA是pandas._libs.missing.NAType 的单例
- 本质：与None类似，是"缺失"的语义标记，但不局限于浮点数
- 适用场景：Pandas的可空数据类型(Int64, boolean, string等)
```python
x = pd.NA
print(type(x))  # <class 'pandas._libs.missing.NAType'>
print(x == x)   # <NA>（同样不等于自身）
```
#### 无论哪种缺失值，统一使用 pd.isna()/pd.null() 都能检测：

```python
s = pd.Series([1, 2, np.nan, None, pd.NA])
# print(s)
# 输出：
# 0       1
# 1       2
# 2     NaN
# 3    None
# 4    <NA>
# dtype: object
```

#### 检查是否是缺失值 pd.isna()/isnull()
```python
# print(s.isna()
# 输出：
# 0    False
# 1    False
# 2     True
# 3     True
# 4     True
# dtype: bool


df = pd.DataFrame([[1, pd.NA, 2], [2, 3, 5], [None, 4, 6]], index = ["第一行", "第二行", "第三行"], columns = ["第一列", "第二列", "第三列"])
#      第一列   第二列  第三列
# 第一行  1.0  <NA>    2
# 第二行  2.0     3    5
# 第三行  NaN     4    6
 
# print(df.isna())
# print(df.isnull())
# 输出：
#        第一列    第二列    第三列
# 第一行  False   True  False
# 第二行  False  False  False
# 第三行   True  False  False
```

#### 查看缺失值的个数 pd.isna().sum(axis = 0 / 1)
```python
print(s.isna().sum()) 输出：3

print(df.isna().sum(axis = 0))
# 输出：
# 第一列    1
# 第二列    1
# 第三列    0
# dtype: int64

print(df.isna().sum(axis = 1))
# 输出：
# 第一行    1
# 第二行    0
# 第三行    1
# dtype: int64
```

#### 删除缺失值 pd.dropna()
```python
# 因为Series是一维的，所以如果是缺失值，直接就删除了，只保留非缺失值的值
# print(s.dropna())
# 输出：
# 0    1
# 1    2
# dtype: object

# 因为DataFrame是二维的，dropna()默认是如果某一行中存在缺失值，直接将这一行给删除掉
# 当然可以适用axis = 1来删除存在缺失值的列
print(df.dropna())
# 输出：
#      第一列 第二列  第三列
# 第二行  2.0   3    5

print(df.dropna(axis = 1))
# 输出：
#      第三列
# 第一行    2
# 第二行    5
# 第三行    6



# pd.dropna(how = "all") 表示只有当（默认）这一行中所有的元素都是缺失值时才删除这一行
# pd.dropna(thresh = n) 表示（默认）这一行中至少有n个不是缺失值，那就保留这一行
# pd.dropna(subset = ["第一列]) 表示只判断第一列，如果这一列的某行存在缺失值，就删除这一行

print(df.dropna(subset = ["第一列", "第三列"]))
# 输出：
#      第一列   第二列  第三列
# 第一行  1.0  <NA>    2
# 第二行  2.0     3    5
```

#### 填充缺失值 pd.fillna({字典})、
```python
df1 = pd.DataFrame(
    {
        "name" : ["小超", "小月", np.nan, "小城", np.nan],
        "age" : [np.nan, 23, 21, 30, 22],
        "hobby" : ["代码", np.nan, "画画", "看书", "鞋子"],

    }, index = ["第一行", "第二行", "第三行", "第四行", "第五行"]
)
#     name   age hobby
# 第一行   小超   NaN    代码
# 第二行   小月  23.0   NaN
# 第三行  NaN  21.0    画画
# 第四行   小城  30.0    看书
# 第五行  NaN  22.0    鞋子



fillnaed_df1 = df1.fillna(
    {
        "name" : "无名",
        "age" : 0,
        "hobby" : "无",
    }
)
print(fillnaed_df)
#     name   age hobby
# 第一行   小超   0.0    代码
# 第二行   小月  23.0     无
# 第三行   无名  21.0    画画
# 第四行   小城  30.0    看书
# 第五行   无名  22.0    鞋子


# ffill()：用前面的相邻值填充
# bfill()：用后面的相邻值填充
```
