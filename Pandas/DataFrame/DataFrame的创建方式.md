```python
import numpy as np
import pandas as pd
```

### 一、通过字典来创建
这是实际工作中最常用的方式。字典的键会成为列名，字典的值会成为该列的数据。
#### 1.1 字典的值是列表
注意：每一列的列表长度必须相等，否则会报错
```python
df = pd.DataFrame(
    {
        "id" : [1, 2, 3, 4, 5],
        "name" : ["tom", "jack", "alice", "bob", "allen"],
        "age" : [15, 17, 20, 26, 30],
        "score" : [60.5, 80, 30.6, 70, 83.5]
    }, index = ["A", "B", "C", "D", "E"], columns = ["id", "name", "score", "age"]
)
print(df)
# 输出：
"""
   id   name  score  age
A   1    tom   60.5   15
B   2   jack   80.0   17
C   3  alice   30.6   20
D   4    bob   70.0   26
E   5  allen   83.5   30
"""
```

#### 1.2 字典的值是Series
很好的体现了 DataFrame就是多个Series的集合
```python
name_series = pd.Series(["张三", "李四", "王五"], name = "姓名")
age_series = pd.Series([25, 30, 22], name = "年龄")
df = pd.DataFrame({"姓名" : name_series, "年龄" : age_series})
print(df)
# 输出：
"""
   姓名  年龄
0  张三  25
1  李四  30
2  王五  22
"""
```

### 二、通过列表嵌套字典创建
每一个字典代表一行，字典的键会成为它们的列名。如果某个字典缺少某个键，对应位置会自动填充NaN
```python
data = [
    {"姓名" : "张三", "爱好" : "钓鱼", "城市" : "北京"},
    {"姓名" : "李四", "爱好" : "玩游戏", "城市" : "上海"},
    {"姓名" : "王五", "爱好" : "写代码"}, # 缺少"城市", 会是NaN  
]
df = pd.DataFrame(data)
print(df)
# 输出：
"""
   姓名   爱好   城市
0  张三   钓鱼   北京
1  李四  玩游戏   上海
2  王五  写代码  NaN
"""
```

### 三、从外部文件读取
#### 从 CSV 读取（最常用）
```python
df = pd.read_csv("filename.csv")
```
#### 从 Excel 读取
```python
df = pd.read_excel("filename.xlsx")
```
#### 从 JSON 读取
```python
df = pd.read_json("filename.json")
```
#### 从 SQL 数据库读取
```python
df = pd.read_sql("SELECT * FROM table", connection)
```
