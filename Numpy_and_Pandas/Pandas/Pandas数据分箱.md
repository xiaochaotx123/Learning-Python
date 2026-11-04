```python
import pandas as pd
df = pd.read_csv("Pandas_Study_Data/employees.csv")
# df
```
#### pd.cut()
pd.cut()是Pandas中用于数据分箱的核心函数，它将连续型数值数据划分为离散的区间（bins），常用于数据离散化、特征工程等场景
```python
pd.cut(x, bins, labels = None)
```
|参数|说明|
|----|---|
|x|要分箱的一维数组（Series或array-like）|
|bins|分箱的方式（主要有两种方式）|
|labels|给每一个箱指定标签，长度必须等于箱的数量|

```python
df1 = df.head(10)[["employee_id", "salary"]]
#    employee_id   salary
# 0          100  24000.0
# 1          101  17000.0
# 2          102  17000.0
# 3          103   9000.0
# 4          104   6000.0
# 5          105   4800.0
# 6          106   4800.0
# 7          107   4200.0
# 8          108  12000.0
# 9          109   9000.0
```

#### bins第一种分箱方式：bins = n，表示需要分箱为几段
pandas会自动计算数据的min和max，然后等宽地切成n个区间
```python
print(pd.cut(df1["salary"], bins = 3))
# 0    (17400.0, 24000.0]
# 1    (10800.0, 17400.0]
# 2    (10800.0, 17400.0]
# 3     (4180.2, 10800.0]
# 4     (4180.2, 10800.0]
# 5     (4180.2, 10800.0]
# 6     (4180.2, 10800.0]
# 7     (4180.2, 10800.0]
# 8    (10800.0, 17400.0]
# 9     (4180.2, 10800.0]
# Name: salary, dtype: category
# Categories (3, interval[float64, right]): [(4180.2, 10800.0] < (10800.0, 17400.0] < (17400.0, 24000.0]]
```

#### bins第二种分箱方式：bins = []，自定义分箱的区间
```python
print(pd.cut(df1["salary"], bins = [0, 10000, 20000, 30000, 40000]))
# 0    (20000, 30000]
# 1    (10000, 20000]
# 2    (10000, 20000]
# 3        (0, 10000]
# 4        (0, 10000]
# 5        (0, 10000]
# 6        (0, 10000]
# 7        (0, 10000]
# 8    (10000, 20000]
# 9        (0, 10000]
# Name: salary, dtype: category
# Categories (4, interval[int64, right]): [(0, 10000] < (10000, 20000] < (20000, 30000] < (30000, 40000]]

print(pd.cut(df1["salary"], bins = [0, 10000, 20000, 30000, 40000]).value_counts())
# salary
# (0, 10000]        6
# (10000, 20000]    3
# (20000, 30000]    1
# (30000, 40000]    0
# Name: count, dtype: int64
```

使用labels可以较为形象的归类
```python
print(pd.cut(df1["salary"], bins = [0, 10000, 20000, 30000, 40000], labels = ["低", "中", "较高", "高"]))
# 0    较高
# 1     中
# 2     中
# 3     低
# 4     低
# 5     低
# 6     低
# 7     低
# 8     中
# 9     低
# Name: salary, dtype: category
# Categories (4, str): ['低' < '中' < '较高' < '高']


分完类后可以直接新建一列
df1["收入水平"] = pd.cut(df1["salary"], bins = [0, 10000, 20000, 30000, 40000], labels = ["低", "中", "较高", "高"])
print(df1)
#    employee_id   salary 收入水平
# 0          100  24000.0   较高
# 1          101  17000.0    中
# 2          102  17000.0    中
# 3          103   9000.0    低
# 4          104   6000.0    低
# 5          105   4800.0    低
# 6          106   4800.0    低
# 7          107   4200.0    低
# 8          108  12000.0    中
# 9          109   9000.0    低
```

#### 与pd.cut()类似的是pd.qcut()
pd.qcut()是Pandas中等频分箱函数，与pd.cut()的"等宽"不同，它保证每个箱中的数据量尽可能相同
```python
pd.qcut(x, q, labels = None)
```
|参数|说明|
|----|----|
|x|要分箱的一维数据|
|q|箱的数量|
|labels|给每个箱的标签|



```python
print(pd.qcut(df1["salary"], 10).value_counts())
# salary
# (4740.0, 4800.0]      2
# (7800.0, 9000.0]      2
# (13500.0, 17000.0]    2
# (4199.999, 4740.0]    1
# (5640.0, 7800.0]      1
# (10200.0, 13500.0]    1
# (17700.0, 24000.0]    1
# (4800.0, 5640.0]      0
# (9000.0, 10200.0]     0
# (17000.0, 17700.0]    0
# Name: count, dtype: int64
```
pd.qcut()的目标是等频分箱，但当数据中存在重复值时，等频就做不到了。  
pd.qcut()的工作原理是：  
1.先计算分位数边界（如10%、20%、30%...）  
2.再把每个数据放入对应区间  
但如果多个数据值完全相同，它们会落在同一个箱里，无法被拆分到不同箱  
建议：pd.qcut(df, q)中的参数q应该远小于数据量，比如10条数据分q=3或q=4比较合理  


```python
df2 = pd.DataFrame(
    {
        "name" : ["jack", "alice", "tom", "bob"],
        "age" : [20, 30, 40, 50],
        "gender" : ["female", "male", "female", "male"],
    }
)
# print(df2)
#     name  age  gender
# 0   jack   20  female
# 1  alice   30    male
# 2    tom   40  female
# 3    bob   50    male
```

#### pd.set_index() —— 将列"提升"为索引
```python
df2 = df2.set_index(["name", "age"])
print(df2)
#            gender
# name  age
# jack  20   female
# alice 30     male
# tom   40   female
# bob   50     male


# print(df2.index)
# MultiIndex([( 'jack', 20),
#             ('alice', 30),
#             (  'tom', 40),
#             (  'bob', 50)],
#            names=['name', 'age'])


print(df2.loc[('jack', 20)])
# gender    female
# Name: (jack, 20), dtype: str
```
- name和age这两列不再是不同数据列了，它们变成了左边的行变迁
- 原来的0，1，2索引消失了
- 现在可以使用pd.loc[(name, age)]来访问元素了

#### reset_index() —— 将索引"降级"回普通列
和set_index()正好相反，把行索引变回普通数据列
```python
df3 = df2.reset_index()
print(df3)
#     name  age  gender
# 0   jack   20  female
# 1  alice   30    male
# 2    tom   40  female
# 3    bob   50    male
```


#### pd.rename() —— 给DataFrame重命名
用来修改DataFrame的行标签（索引名）或列名
- index = {}表示想要修改的索引
- columns = {}表示想要修改的列名
- 不需要全部修改，可以只修改其中一部分
```python
df4 = df3.rename(index = {0:4, 1:5}, columns = {"name":"名字", "gender":"性别"})
print(df4)
#       名字  age      性别
# 4   jack   20  female
# 5  alice   30    male
# 2    tom   40  female
# 3    bob   50    male
```
