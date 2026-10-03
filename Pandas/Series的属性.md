|属性|说明|
|----|----|
|index|Series的索引对象|
|valudes|Series的值|
|dtype或dtypes|Series的元素类型|
|shape|Series的形状|
|ndim|Series的维度|
|size|Series的元素个数|
|name|Series的名称|
|loc[]|显式索引，按标签索引或切片|
|iloc[]|隐式索引，按位置索引或切片|
|at[]|使用标签访问单个元素|
|iat[]|使用位置访问单个元素|


### 一、基础属性
#### 1. index —— Series的索引对象  
返回Series的索引，类型是pandas.Index
```python
import pandas as pd
s = pd.Series([10, 20, 30], index = ["A", "B", "C"], name = "数据")
print(s.index) # 输出：Index(["A", "B", "C"], dtype = "str")
```

#### 2. value —— Series的值
返回Series的值，类型是numpy.ndarray
```python
print(s.values) # 输出：[10 20 30]
```

#### 3. dtype/dtypes —— Series的元素类型
dtype是属性，dtypes是方法（两者在Series中等价），返回数据类型
```python
print(s.dtype) # 输出：int64

# 创建浮点型 Series
s2 = pd.Series([1.1, 2.2, 3.3])
print(s2.dtype) # 输出：float64
```

#### 4. shape —— Series的形状
返回一个元组，表示维度。Series是一维的，所以形状是(n, )
```python
print(s.shape) # 输出：(3, )
```

#### 5. ndim —— Series的维度
Series始终是一维数据结构，所以ndim永远是一维
```python
print(s.ndim) # 输出：1
```

#### 6. size —— Series中元素的个数
返回Series中元素的个数
```python
print(s.size) # 输出：3
```

#### 7. name —— Series的名称
Series的名称，在创建的时候可以通过name参数指定
```python
print(s.name) # 输出：数据

# 可以修改name
s.name = "新数据"
print(s.name) # 输出：新数据
```

### 二、索引访问器（4个）
#### 8. loc[] —— 显式索引（按标签）
通过标签（index的值）来访问元素或切片
```python
print(s.loc["B"]) # 输出：20

# 切片（包含终点！这是于iloc的区别）
print(s.loc["A" : "B"]) 
# 输出：
"""
A 10
B 20
Name: 数据, dtype: int64
"""
```

#### 9. iloc[] —— 隐式索引（按位置）
通过整数位置（从0开始）来访问元素或切片
```python
print(s.iloc[1]) # 输出：20

# 切片（不包含终点，于python列表切片一致）
print(s.iloc[0 : 1])
# 输出：
"""
A 10
Name: 数据, dtype: int64
"""
```

#### 10. at[] —— 按照标签访问单个元素
专门用于快速访问单个标量值，比loc更快。不能切片操作
```python
print(s.at["C"]) # 输出：30
```

#### 11. iat[] —— 按照位置访问单个元素
专门用于快速访问单个标量值，比iloc更快。不能切片操作
```python
print(s.iat[0]) # 输出：10
```
