```python
import pandas as pd
data = {
    "name" : ["alice", "alice", "bob", "alice", "jack", "bob"],
    "age" : [26, 25, 30, 25, 55, 30],
    "city" : ["NY", "NY", "LA", "NY", "SF", "LA"]
}
df = pd.DataFrame(data)
    # name  age city
# 0  alice   26   NY
# 1  alice   25   NY
# 2    bob   30   LA
# 3  alice   25   NY
# 4   jack   55   SF
# 5    bob   30   LA
```

#### 判断是否是重复元素（各列值全部相等） pd.duplicated()
```python
print(df.duplicated()) # 一整条记录都是一样的，标记为重复，返回True
# 0    False
# 1    False
# 2    False
# 3     True
# 4    False
# 5     True
# dtype: bool
```

#### 删除重复元素 pd.drop_duplicates()
```python
print(df.drop_duplicates()) # 删除重复元素
#     name  age city
# 0  alice   26   NY
# 1  alice   25   NY
# 2    bob   30   LA
# 4   jack   55   SF
```

#### 自定义指定列去重 添加参数 subset = ["columns"]
```python
print(df.drop_duplicates(subset = ["name"])) 
    # name  age city
# 0  alice   26   NY
# 2    bob   30   LA
# 4   jack   55   SF
```

#### 去重元素保留的默认是第一次出现的元素，添加参数 keep = "last"使得去重后保留的元素是最后一次出现的
```python
print(df.drop_duplicates(subset = ["name"], keep = "last"))
#     name  age city
# 3  alice   25   NY
# 4   jack   55   SF
# 5    bob   30   LA
```

##### 数据类型转换
#### astype()
astype()是Pandas中用于数据类型转换的核心方法，可以对Series和DataFrame进行类型转换  
|类型字符串|含义|实例|
|---------|----|----|
|"int8", "int16", "int32", "int64"|有符号整数|astype("int32")|
|"uint8", "uint16", ...|无符号整数|astype("uint8")|
|"float8", "float16", "float32"|浮点数|astype("float32")|
|"str"/"string"|字符串|astype("str")|
|"category"|分类类型|astype("category")|
|"bool"|布尔值|astype("bool")|
|"datetime64[ns]"|日期时间|astype("datetime64[ns]")|


```python
sleep_df = pd.read_csv("Pandas_Study_Data/sleep.csv")
```
```python
print(sleep_df.dtypes) # 只看age这一个
# ...
# age                          int64
# ...
# dtype: object

sleep_df["age"] = sleep_df["age"].astype("int16")

print(sleep_df.dtypes)
# ...
# age                          int16
# ...
# dtype: object
```

```python
print(sleep_df.gender)
# 0       Male
# 1     Female
# 2       Male
# ...
# 38      Male
# 39    Female
# Name: gender, dtype: str

sleep_df["gender"] = sleep_df["gender"].astype("category")

# print(sleep_df.dtypes) # 只看gender这一个
# ...
# gender                     category
# ...
# dtype: object

print(sleep_df.gender)
# 0       Male
# 1     Female
# ...
# 38      Male
# 39    Female
# Name: gender, dtype: category
# Categories (2, str): ['Female', 'Male']


sleep_df["is_male"] = sleep_df["gender"].map({"Male" : True, "Female" : False})
print(sleep_df["is_male"])
# 0      True
# 1     False
# 2      True
# ...
# 39    False
# Name: is_male, dtype: category
# Categories (2, bool): [False, True]
```
