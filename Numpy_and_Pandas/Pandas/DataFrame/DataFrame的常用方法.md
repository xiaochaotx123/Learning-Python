|方法|说明|
|----|----|
|head()|查看前n行数据，默认5行|
|tail()|查看后n行数据，默认5行|
|isin()|判断元素是否包含在参数集合中|
|isna()|判断是否为缺失值（如NaN或None）|
|sum()|求和，自动忽略缺失值|
|cumsum()|累积和|
|cummax()|累积最大值|
|max()|最大值|
|min()|最小值|
|mean()|平均值|
|median()|中位数|
|mode()|众数（可返回多个）|
|var()|方差|
|std()|标准差|
|quantile(q)|分数为，q取0~1之间|
|describle()|常见统计信息（count、mean、st、min、25%、50%、75%、max）|
|count()|非缺失值的数量|
|value_counts()|每一个唯一值出现的次数|
|duplicated()|是否重复|
|drop_duplicates()|去除重复项|
|sample()|随机抽样|
|sort_index()|按索引排序|
|sort_values()|按值排序|
|nlargest()|返回某列最大的n条数据|
|nsmallest()|返回某列最小的n条数据|

```python
import numpy as np
import pandas as pd
```
```python
df = pd.DataFrame(
    {
        "name" : ["tom", "jack", "alice", "bob", "allen"],
        "age" : [15, 17, 20, 26, 30],
        "score" : [60.5, 80, 30.6, 70, 83.5],
    }, index = [1, 2, 3, 4, 5], columns = ["name", "score", "age"]
)
#     name  score  age
# 1    tom   60.5   15
# 2   jack   80.0   17
# 3  alice   30.6   20
# 4    bob   70.0   26
# 5  allen   83.5   30
```

#### head(), tail()
```python
print(df.head())
print(df.tail(1))
```

#### isin()
```python
print(df.isin(["jack", 20]))
# 输出：
#     name  score    age
# 1  False  False  False
# 2   True  False  False
# 3  False  False   True
# 4  False  False  False
# 5  False  False  False
```

#### isna()
```python
print(df.isna())
# 输出：
#     name  score    age
# 1  False  False  False
# 2  False  False  False
# 3  False  False  False
# 4  False  False  False
# 5  False  False  False
```

#### sum()
```python
print(df.sum())
# 输出：
# name     tomjackaliceboballen
# score                   324.6
# age                       108
# dtype: object

# 求年龄这一列的总和
print(df["score"].sum()) # 输出：324.6
```

#### cumsum()
```python
# 求累积和
print(df.cumsum())
# 输出：
#                    name  score  age
# 1                   tom   60.5   15
# 2               tomjack  140.5   32
# 3          tomjackalice  171.1   52
# 4       tomjackalicebob  241.1   78
# 5  tomjackaliceboballen  324.6  108
```

#### cummax()
```python
# 求分数这一列的累积最大值
print(df.score.cummax())
# 输出：
# 1    60.5
# 2    80.0
# 3    80.0
# 4    80.0
# 5    83.5
# Name: score, dtype: float64
```

#### max()
```python
# 求成绩这一列的最大值
print(df.score.max()) # 输出：83.5
```

#### min()
```python
# 求成绩这一列的最小值
print(df.score.min()) # 输出：30.6
```

#### mean()
```python
# 求成绩这一列的平均数
print(df.score.mean()) # 输出：64.92
```

#### median()
```python
# 求成绩这一列的中位数
print(df.score.median()) # 输出：70.0
```

#### mode()
```python
# 求成绩这一列的众数
print(df.score.mode())
# 输出：
# 0    30.6
# 1    60.5
# 2    70.0
# 3    80.0
# 4    83.5
# Name: score, dtype: float64
```

#### var()
```python
# 求成绩这一列的方差
print(df.score.var()) # 输出：448.957
```

#### std()
```python
# 求成绩这一列的标准差
print(df.score.std()) # 输出：21.188605428390044
```

#### quantile()
```python
# 求成绩这一列的第25%分位数
print(df.score.quantile(0.25)) # 输出：60.5
```

#### describe
```python
# 求成绩这一列的所有基本信息
print(df.score.describe())
# 输出：
# count     5.000000
# mean     64.920000
# std      21.188605
# min      30.600000
# 25%      60.500000
# 50%      70.000000
# 75%      80.000000
# max      83.500000
# Name: score, dtype: float64
```

#### count()
```python
# 求每一列的非缺失值个数
print(df.count())
# 输出：
# name     5
# score    5
# age      5
# dtype: int64

# 求score这一行的非缺失值个数
print(df.score.count()) # 输出：5
```

#### value_counts()
```python
df1 = pd.DataFrame(
    {
        "name" : ["XC", "XC", "XY"],
        "score" : [66, 66, 90],
        "Age" : [20, 20, 21],
    }, index = [1, 2, 3]
)
#   name  score  Age
# 1   XC     66   20
# 2   XC     66   20
# 3   XY     90   21

# 求df1中每一个唯一值出现的次数
print(df1.value_counts())
# 输出：
# name  score  Age
# XC    66     20     2
# XY    90     21     1
# Name: count, dtype: int64

# 求df1的name中每一个唯一值出现的次数
print(df1.name.value_counts())
# 输出：
# name
# XC    2
# XY    1
# Name: count, dtype: int64
```

#### duplicated()
```python
# 判断是否重复
print(df1.duplicated())
# 输出：
# 1    False
# 2     True
# 3    False
# dtype: bool
```

#### drop_duplicates()
```python
# 去除掉重复值
droped_df1 = df1.drop_duplicates()
print(droped_df1)
# 输出：
#   name  score  Age
# 1   XC     66   20
# 3   XY     90   21
```

#### sample()
```python
# 随机抽样
print(df.sample(2))
```

#### sort_index()
```python
print(df.index) # 输出：Index([1, 2, 3, 4, 5], dtype='int64')

# 按照索引从大到小排序
print(df.sort_index(ascending = False))
# 输出：
#     name  score  age
# 5  allen   83.5   30
# 4    bob   70.0   26
# 3  alice   30.6   20
# 2   jack   80.0   17
# 1    tom   60.5   15
```

#### sort_values()
```python
# 这样直接写会报错TypeError，必须指定到底是对哪一列进行排序
# print(df.sort_values())

# 对分数这一列进行从大到小排序
print(df.score.sort_values(ascending = False))
# 输出：
# 5    83.5
# 2    80.0
# 4    70.0
# 1    60.5
# 3    30.6
# Name: score, dtype: float64

# 先按照分数从大到小排序，如果分数相同情况则按照年龄从小到大排序
print(df.sort_values(by = ["score", "age"], ascending = [False, True]))
# 输出：
#     name  score  age
# 5  allen   83.5   30
# 2   jack   80.0   17
# 4    bob   70.0   26
# 1    tom   60.5   15
# 3  alice   30.6   20
```

#### nlargest() 
```python
# 直接这么写也是报错TypeError，需要指定是求哪一列
# print(df.nlargest())

# 输出分数最大的前两个元素
print(df.nlargest(2, columns = ["score"]))
# 输出：
#     name  score  age
# 5  allen   83.5   30
# 2   jack   80.0   17


# 可以会输出超过2个元素，因为对于score这一列来说，最大值可以有多个，这时候可以继续按照其他要素求最大的
print(df.nlargest(2, columns = ["score", "age"]))
```

#### nsmallest()
和nlargest是类似的
