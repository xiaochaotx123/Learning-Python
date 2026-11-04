```python
import pandas as pd
data = {
    "ID" : [1, 2],
    "name" : ["alice", "bob"],
    "Math" : [90, 85],
    "English" : [88, 92],
    "Science" : [95, 89]
}
df = pd.DataFrame(data)
#    ID   name  Math  English  Science
# 0   1  alice    90       88       95
# 1   2    bob    85       92       89
```

#### 行列转置
```python
print(df.T)
#              0    1
# ID           1    2
# name     alice  bob
# Math        90   85
# English     88   92
# Science     95   89
```

#### pd.melt() —— 宽表转长表
pd.melt()是Pandas中用于将宽格式数据转换为长格式数据的函数，也被称为"逆透视"
```python
pd.melt(
    frame,           # 要转换的 DataFrame
    id_vars=None,    # 保持不变的列（标识列）
    value_vars=None, # 要被"融化"的列（默认：除 id_vars 外的所有列）
    var_name=None,   # 给"变量名"列起的名字
    value_name='value'  # 给"值"列起的名字
)
```
|参数|说明|例子|
|----|----|---|
|id_vars|保持不变的列，充当每天记录的"身份证"|["ID", "name"] - 这两列原样保留|
|value_vars|需要被"融化堆叠"的列（不指定则自动取剩下的所有列）|默认取了["Math", "English", "Science"]|
|var_name|原列名变成一列数据后，这一列叫什么名字|"科目" —— 把Math/English/Science存到这里|
|value_name|原数值变成一列数据后，这一列叫什么名字|"分数" —— 把80/88/95...存到这里|
```python
df1 = pd.melt(df, id_vars = ["ID", "name"], var_name = "科目", value_name = "分数")

print(df1)
#    ID   name       科目  分数
# 0   1  alice     Math  90
# 1   2    bob     Math  85
# 2   1  alice  English  88
# 3   2    bob  English  92
# 4   1  alice  Science  95
# 5   2    bob  Science  89
```

#### pd.pivot() —— 长表转宽表
pd.pivot()是Pandas中用于将长格式数据转换为宽格式数据的函数，也就是"透视"操作
```python
df.pivot(
    index=None,    # 作为新表行索引的列
    columns=None,  # 其唯一值将成为新表列名的列
    values=None    # 要填充到新表中的值所在的列
)
```
|参数|说明|例子|
|----|----|----|
|index|新表中用来确定每一行的列|["ID", "name"] —— 每行由(ID, name)唯一确定|
|columns|其唯一值展开为新表的列名|"科目" —— Math/English/Science三个值变成三列|
|values|填入新表单元格的数值来源|"分数" —— 90,88,95...填入对应位置|

```python
df2 = pd.pivot(df1, index = ["ID", "name"], columns = "科目", values = "分数")
print(df2)
# 科目        English  Math  Science
# ID name
# 1  alice       88    90       95
# 2  bob         92    85       89
```

#### 分列操作
在sleep.csv中存在一列值blood_pressure，比如124/70表示的这个人的最高血压是124，最低血压是70  
我们可以使用分列操作将这个blood_pressure分成2列：high_blood_pressure和low_blood_pressure  
```python
sleep_df[["high_blood_pressure", "low_blood_pressure"]] = sleep_df["blood_pressure"].str.split("/", expand = True)
```

|部分|说明|
|----|----|
|sleep_df["blood_pressure"].str|.str访问器，用于对Series中的每一个字符串元素调用字符串方法|
|.split("/", expand=True)|按照 / 分割每个字符串，expand = True将结果展开为一个DataFrame（多列），而非返回包含列表的Series|
|sleep_df[["high_blood_pressure", "low_blood_pressure"]]|左侧使用双括号[[...]]同时指定两个新列目标|

```python
sleep_df = pd.read_csv("Pandas_Study_Data/sleep.csv")
print(sleep_df["blood_pressure"])

sleep_df[["high_blood_pressure", "low_blood_pressure"]] = sleep_df["blood_pressure"].str.split("/", expand = True)

print(sleep_df.dtypes)
# ...
# high_blood_pressure            str
# low_blood_pressure             str
# dtype: object

sleep_df["high_blood_pressure"] = sleep_df["high_blood_pressure"].astype("int64")
sleep_df["low_blood_pressure"] = sleep_df["low_blood_pressure"].astype("int64")

print(sleep_df.dtypes)
# ...
# high_blood_pressure          int64
# low_blood_pressure           int64
# dtype: object

print(sleep_df["high_blood_pressure"].mean()) # 124.55
```
分列操作后的high_blood_pressure和low_blood_pressure的数据类型都是str类型，不能进行求最大值、平均数等计算，所以得使用astype()进行数据类型转换

