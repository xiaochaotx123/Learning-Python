### 1.导入必要的库  
```python
import numpy as np
import pandas as pd
```

### 2.导入数据
```python
df = pd.read_csv("Pandas_Study_Data/penguins.csv")
```

### 3.数据清洗

#### 缺失值的检查并删除缺失值
```python
print(len(df)) # 50
print(df.isna().sum())
# species              0
# island               0
# bill_length_mm       5
# bill_depth_mm        1
# flipper_length_mm    2
# body_mass_g          1
# sex                  7
# dtype: int64


df = df.dropna()
print(len(df)) # 38
print(df.isna().sum())
# species              0
# island               0
# bill_length_mm       0
# bill_depth_mm        0
# flipper_length_mm    0
# body_mass_g          0
# sex                  0
# dtype: int64
```

### 4.数据特征的构造

#### 将sex从str类型转换为category类型
```python
print(df.dtypes)
# ...
# sex                      str
# dtype: object

df["sex"] = df["sex"].astype("category")

print(df.dtypes)
# ...
# sex                  category
# dtype: object
```

#### 新建bill长宽比例
```python
df["bill_ratio"] = round(df["bill_length_mm"] / df["bill_depth_mm"], 3)
```

### 5.数据分析

#### 数据分箱：将体重分为三个等级
```python
labels = ["低", "中", "高"]
df["mass_level"] = pd.cut(df["body_mass_g"], 3, labels = labels)
print(df["mass_level"].value_counts())
# mass_level
# 低    28
# 中     5
# 高     5
# Name: count, dtype: int64
```

#### 按照性别、岛屿分组聚合分析
```python
x = df.groupby(["sex", "island"]).agg(
    {
        "body_mass_g" : ["mean", "count"],
    }
)
print(x)
#                   body_mass_g
#                          mean count
# sex    island
# Female Biscoe     4094.444444     9
#        Dream      3509.375000     8
#        Torgersen  3437.500000     4
# Male   Biscoe     4654.545455    11
#        Dream      3850.000000     4
#        Torgersen  3821.428571     7
```
