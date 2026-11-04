|属性|说明|
|----|----|
|index|DataDrame的行索引|
|columns|DataFrame的列标签|
|values|DataFrame的值|
|ndim|DataFrame的维度|
|shape|DataFrame的形状|
|size|DataFrame的元素个数|
|dtypes|DataFrame的元素类型|
|T|行列转置|
|loc[]|显式索引，按行列标签索引或切片|
|iloc[]|隐式索引，按行列位置索引或切片|
|at[]|使用行列标签访问单个元素|
|iat[]|使用行列位置访问单个元素|

```python
import numpy as np
import pandas as pd
```
```python
df = pd.DataFrame(
    {
        "name" : ["tom", "jack", "alice", "bob", "allen"],
        "score" : [60.5, 80.0, 30.6, 70.0, 83.5],
        "age" : [15, 17, 20, 26, 30],
    }, index = [1, 2, 3, 4, 5], columns = ["name", "score", "age"]
)
#     name  score  age
# 1    tom   60.5   15
# 2   jack   80.0   17
# 3  alice   30.6   20
# 4    bob   70.0   26
# 5  allen   83.5   30
```

#### 行索引 index
```python
print(df.index) # 输出：Index([1, 2, 3, 4, 5], dtype='int64')
# 转化为列表
# print(df.index.tolist()) # 输出：[1, 2, 3, 4, 5]
# print(df.index.tolist()[0:2:1]) # 输出：[1, 2]
```

#### 列标签 columns
```python
print(df.columns) # 输出：Index(['name', 'score', 'age'], dtype='str')
# print(df.columns.tolist()) # 输出：['name', 'score', 'age']
```

#### 值 values 
```python
print(df.values)
# 输出：
# [['tom' 60.5 15]
#  ['jack' 80.0 17]
#  ['alice' 30.6 20]
#  ['bob' 70.0 26]
#  ['allen' 83.5 30]]

# arr = np.array(df.values)
# print(arr)
```

#### 维度 ndim
```python
print(df.ndim) # 输出：2
```

#### 形状 shape
```python
print(df.shape) # 输出：(5, 3)
```

#### 元素个数 size
```python
print(df.size) # 输出：15
```

#### 元素类型 dtype
```python
print(df.dtypes)
# 输出：
# name         str
# score    float64
# age        int64
# dtype: object
```

#### 行列转置 T
```python
df_T = df.T
print(df_T)
# 输出：
#           1     2      3     4      5
# name    tom  jack  alice   bob  allen
# score  60.5  80.0   30.6  70.0   83.5
# age      15    17     20    26     30

print(df_T.index) # 输出：Index(['name', 'score', 'age'], dtype='str')
print(df_T.columns) # 输出：Index([1, 2, 3, 4, 5], dtype='int64')
```

#### 显式索引 loc；隐式索引 iloc；获取单个元素显式索引 at；获取单个元素隐式索引 iat
```python
df1 = pd.DataFrame(
    {
        "姓名" : ["小超", "小月", "小星", "小程"],
        "年龄" : [21, 22, 21, 22],
        "爱好" : ["写代码", "探索", "画画", "打游戏"],
    }, index = ["C", "Y", "X", "CH"]
)
#     姓名  年龄   爱好
# C   小超  21  写代码
# Y   小月  22   探索
# X   小星  21   画画
# CH  小程  22  打游戏

# 输出某行：
print(df1.loc["C"]) # print(df1.iloc[0])
# 输出：
# 姓名     小超
# 年龄     21
# 爱好    写代码
# Name: C, dtype: object

# 输出某列：
print(df1.loc[:, "爱好"])
# 输出：
# C     写代码
# Y      探索
# X      画画
# CH    打游戏
# Name: 爱好, dtype: str

print(df1.iloc[:, 1])
# 输出：
# CY     22
# X     21
# CH    22
# Name: 年龄, dtype: int64     21


# 获取单个元素
print(df1.at["Y", "爱好"]) # 输出：探索
print(df1.iat[2, 1]) # 输出：21
```
