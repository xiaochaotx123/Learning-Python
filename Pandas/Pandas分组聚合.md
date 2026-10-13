```python
import pandas as pd
df = pd.read_csv("Pandas_Study_Data/employees.csv")
```

#### df.groupby("分组的字段")["聚合的字段"].聚合函数()
|代码|说明|作用|
|----|----|---|
|df.groupby("分组的字段")|分组|按指定列的值将数据拆分成多个"组"，返回一个DataFrameGroupBy对象。此时没有任何计算，只是将数据"分组"了|
|["聚合的字段"]/[["聚合的字段"]]|选列|["聚合的字段"]返回SeriesGroupBy（一维），[["salary"]]返回DataFrameGroupBy（二维，保留表格结构）|
|.聚合函数()|计算|.mean() /.sum() /.count() /.max() /.min() /.std() /.median()|

### 计算不同部门的平均薪资
#### 首先对数据进行清洗
- df["department_id"]中可能存在NaN，所以首先需要将department_id = NaN的删除  
- 然后将数据类型从浮点数修改为整数类型
```python
df = df.dropna(subset = ["department_id"])
df["department_id"] = df["department_id"].astype("int64")
```

#### 简单介绍一下 df.groupby().groups 和 df.groupby().get_group()
df.groupby().groups就是将df.groupby()分好的组全部一一的列举出来  
df.groupby().get_group()就是你可以查询具体的分好的组中的某一组的情况
```python
print(df.groupby("department_id").groups) # {30: [14, 15, 16, 17, 18], 50: [19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29], 60: [3, 4, 5, 6, 7], 80: [12, 13], 90: [0, 1, 2], 100: [8, 9, 10, 11]}
print(df.groupby("department_id").get_group(30)) # 将具体的组中数据输出出来
#     employee_id first_name last_name     email  phone_number    job_id  salary  commission_pct  manager_id  department_id
# 14          114        Den  Raphaely  DRAPHEAL  515.127.4561    PU_MAN   14  11000.0             NaN       114.0             30
# 15          115  Alexander      Khoo     AKHOO  515.127.4562  PU_CLERK   15   3100.0             NaN       114.0             30
# 16          116     Shelli     Baida    SBAIDA  515.127.4563  PU_CLERK   16   2900.0             NaN       114.0             30
# 17          117      Sigal    Tobias   STOBIAS  515.127.4564  PU_CLERK   17   2800.0             NaN       114.0             30
# 18          118        Guy    Himuro   GHIMURO  515.127.4565  PU_CLERK   18   2600.0             NaN       114.0             30
```

#### 计算不同部门的平均薪资
这是Series
```python
print(df.groupby("department_id")["salary"].mean())
# department_id
# 30      4480.000000
# 50      4790.909091
# 60      5760.000000
# 80      7350.000000
# 90     19333.333333
# 100     9225.000000
# Name: salary, dtype: float64
```
这是DataFrame
```python
df2 = df.groupby("department_id")[["salary"]].mean()
print(df2)
#                      salary
# department_id
# 30              4480.000000
# 50              4790.909091
# 60              5760.000000
# 80              7350.000000
# 90             19333.333333
# 100             9225.000000

# 保留三位小数
df2["salary"] = round(df2["salary"], 3)
print(df2)
#                   salary
# department_id
# 30              4480.000
# 50              4790.909
# 60              5760.000
# 80              7350.000
# 90             19333.333
# 100             9225.000
```
一般使用DataFrame吧，可以搭配reset_index(inplace = True)使用
```python
df2.reset_index(inplace = True)
print(df2)
#    department_id     salary
# 0             30   4480.000
# 1             50   4790.909
# 2             60   5760.000
# 3             80   7350.000
# 4             90  19333.333
# 5            100   9225.000

# 按照薪资从大到小排序
df2.sort_values("salary", ascending = False, inplace = True)
print(df2)
#    department_id     salary
# 4             90  19333.333
# 5            100   9225.000
# 3             80   7350.000
# 2             60   5760.000
# 1             50   4790.909
# 0             30   4480.000
```

#### 计算不同岗位并且不同部门的平均薪资
```python
print(df.groupby(["job_id", "department_id"]).groups)
# {('AD_PRES', 90): RangeIndex(start=0, stop=1, step=1), ('AD_VP', 90): RangeIndex(start=1, stop=3, step=1), ('FI_ACCOUNT', 100): RangeIndex(start=9, stop=12, step=1), ('FI_MGR', 100): RangeIndex(start=8, stop=9, step=1), ('IT_PROG', 60): RangeIndex(start=3, stop=8, step=1), ('PU_CLERK', 30): RangeIndex(start=15, stop=19, step=1), ('PU_MAN', 30): RangeIndex(start=14, stop=15, step=1), ('SA_REP', 80): RangeIndex(start=12, stop=14, step=1), ('ST_CLERK', 50): Index([19, 25, 26, 27, 28, 29], dtype='int64'), ('ST_MAN', 50): RangeIndex(start=20, stop=25, step=1)}
```
```python
different_job_and_department_df = df.groupby(["job_id", "department_id"])[["salary"]].mean()
print(different_job_and_department_df)
# job_id      department_id
# AD_PRES     90               24000.000000
# AD_VP       90               17000.000000
# FI_ACCOUNT  100               8300.000000
# FI_MGR      100              12000.000000
# IT_PROG     60                5760.000000
# PU_CLERK    30                2850.000000
# PU_MAN      30               11000.000000
# SA_REP      80                7350.000000
# ST_CLERK    50                2716.666667
# ST_MAN      50                7280.000000
# Name: salary, dtype: float64

print(different_job_and_department_df.loc[("AD_PRES", 90)]) # 24000.0

different_job_and_department_df.reset_index(inplace = True)
print(different_job_and_department_df)
#        job_id  department_id        salary
# 0     AD_PRES             90  24000.000000
# 1       AD_VP             90  17000.000000
# 2  FI_ACCOUNT            100   8300.000000
# 3      FI_MGR            100  12000.000000
# 4     IT_PROG             60   5760.000000
# 5    PU_CLERK             30   2850.000000
# 6      PU_MAN             30  11000.000000
# 7      SA_REP             80   7350.000000
# 8    ST_CLERK             50   2716.666667
# 9      ST_MAN             50   7280.000000
```
