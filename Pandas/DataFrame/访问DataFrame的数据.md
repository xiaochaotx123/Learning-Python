```python
import numpy as np
import pandas as pd
```
```python
df = pd.DataFrame(
    {
        "姓名" : ["小超", "小可", "小月", "小零"],
        "爱好" : ["写代码", "学习", "探索", "钓鱼"],
        "居住地" : ["重庆", "湖南", "北京", "香港"],
        "身高" : [180, 165, 172, 177],
    }, index = ["XC", "XK", "XY", "XL"]
)
#     姓名   爱好 居住地   身高
# XC  小超  写代码  重庆  180
# XK  小可   学习  湖南  165
# XY  小月   探索  北京  172
# XL  小零   钓鱼  香港  177
```

#### 获取单列数据
```python
print(df["居住地"])
# 输出：
# XC    重庆
# XK    湖南
# XY    北京
# XL    香港
# Name: 居住地, dtype: str
print(type(df["居住地"])) # 输出：<class 'pandas.Series'>


print(df.姓名)
# 输出：
# XC    小超
# XK    小可
# XY    小月
# XL    小零
# Name: 姓名, dtype: str
print(type(df.姓名)) # 输出：<class 'pandas.Series'>
```

无论是df["居住地"]还是df.姓名都是一个Series  
这个df[["姓名", "身高"]]可以返回多列数据，数据类型是DataFrame

#### 获取多列数据
```python
print(df[["姓名", "身高"]])
# 输出：
#     姓名   身高
# XC  小超  180
# XK  小可  165
# XY  小月  172
# XL  小零  177
print(type(df[["姓名", "身高"]])) # 输出：<class 'pandas.DataFrame'>

# df.head(n)和df.tail()
print(df.head(2))
# 输出：
#     姓名   爱好 居住地   身高
# XC  小超  写代码  重庆  180
# XK  小可   学习  湖南  165
```

#### 筛选数据
```python
print(df[df.身高 > 175])
# 输出：
#     姓名   爱好 居住地   身高
# XC  小超  写代码  重庆  180
# XL  小零   钓鱼  香港  177
print(type(df[df.身高 > 175])) # 输出：<class 'pandas.DataFrame'>

print(df[(df.身高 > 175) | (df.爱好 == "探索")])
# 输出：
#     姓名   爱好 居住地   身高
# XC  小超  写代码  重庆  180
# XY  小月   探索  北京  172
# XL  小零   钓鱼  香港  177
```

#### 随机抽样 sample()函数
sample()是Pandas中用于随机抽样的方法，可以从DataFrame或Series中随机抽取若干行或列。它在数据探索、验证集划分、减少数据规模等场景中非常有用
```python
# 随机抽取，不是按照顺序去的，都是随机的
print(df.sample()) # 默认随机抽取一行数据

print(df.sample(3)) # 随机抽取3行数据
```
