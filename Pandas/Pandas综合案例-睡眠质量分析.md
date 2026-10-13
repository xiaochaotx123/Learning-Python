### 1.导入库
```python
import numpy as np
import pandas as pd
```

### 2.导入数据
```python
df = pd.read_csv("Pandas_Study_Data/sleep.csv")
```

### 3.数据的清洗

#### 清洗缺失值
```python
print(df.isna().sum())
# person_id                   0
# gender                      0
# age                         0
# occupation                  0
# sleep_duration              0
# sleep_quality               0
# physical_activity_level     0
# stress_level                0
# bmi_category                0
# blood_pressure              0
# heart_rate                  0
# daily_steps                 0
# sleep_disorder             32
# dtype: int64
print(df["sleep_disorder"].value_counts())
# sleep_disorder
# Insomnia       9
# Sleep Apnea    9
# Name: count, dtype: int64

# 要么直接将sleep_disorder这一列直接删了，要么添加一种类型，将缺失值处理为未知
df = df.drop(columns = ["sleep_disorder"])

print(df.isna().sum()) # 全都等于0
```


### 4.数据特征的构造

#### 将gender类型从str转换到category类型
```python
print(df["gender"].dtypes) # str
df["gender"] = df["gender"].astype("category")
print(df["gender"].dtypes) # category
```

#### 血压分列
```python
df[["high_blood_pressure", "low_blood_pressure"]] = df["blood_pressure"].str.split("/", expand = True)
```

#### 睡眠质量分箱
```python
sleep_labels = ["差", "中", "优"]
df["sleep_level"] = pd.cut(df["sleep_quality"], 3, labels = sleep_labels)
```

#### 年龄分箱
```python
age_labels = ["青少年", "中年", "老年"]
df["age_level"] = pd.cut(df["age"], 3, labels = age_labels)
```


### 5.数据的统计与分析

#### 根据不同的年龄和bmi分组，睡眠质量
```python
sort_age_bmi_sleep = df.groupby(["age_level", "bmi_category"]).agg(
    {
        "sleep_duration" : "mean",
        "sleep_quality" : "mean",
        "stress_level" : "mean"
    }
)
print(sort_age_bmi_sleep)
#                         sleep_duration  sleep_quality  stress_level
# age_level bmi_category
# 青少年       Normal              6.958333       7.000000      5.666667
#           Obese               7.066667       7.333333      8.666667
#           Overweight          6.566667       7.000000      6.000000
#           Underweight         8.900000       9.500000      3.000000
# 中年        Normal              6.400000       6.357143      6.285714
#           Obese               6.285714       5.957143      6.142857
#           Overweight          6.350000       5.875000      7.000000
#           Underweight         6.100000       6.000000      4.000000
# 老年        Normal              9.333333       9.600000      1.666667
#           Obese               8.150000       8.475000      4.000000
#           Overweight          7.660000       7.700000      4.800000
```
