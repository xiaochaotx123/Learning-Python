https://www.kaggle.com/code/lazer999/top-1-housing-price-eda-random-for-everyone/notebook  

# 1.导入库文件
```python
import pandas as pd 
```  
这个就是读数据、处理表格。


```python
import seaborn as sns
import matplotlib.pyplot as plt
sns.set_style('darkgrid')
```
画图工具。`seaborn` 是 `matplotlib` 的'美化版'，画统计图更省事（一行代码出热力图、分布图）。  
sns.set_style('darkgrid') 只是设置图表风格为灰底网格，纯外观。 

```python
from sklearn.model_selection import train_test_split
```
切割训练集/验证集

```python
from sklearn.metrics import mean_absolute_error
```
算MAE

```python
from sklearn.ensemble import GradientBoostingRegressor
```
**梯度提升回归器**。和随机森林同一个家族（集成学习），但机制不同：
||随机森林|梯度提升|
|-|-|-|
|训练方式|100棵树**同时**独立训练|100棵树**串行**，后一棵树专门修正前一棵树的错误|
|类比|100个人各自答题，投票|100个学生接力改同一份卷子，每人只改错的地方|
|效果|好|通常**更好**，但对参数更敏感|  

用法和随机森林 完全一样 ：`model.fit(X, y)` →`model.predict(X_test)` 。这就是 sklearn 统一接口的好处。  

##### 问题：混合类型数据太麻烦  
数据有81列，分为两种：
1. 数值列：LotArea、GrLivArea、YearBuilt   → 缺失值要填中位数
2. 类别列：Neighborhood、SaleCondition     → 缺失值要填"None"，还要转 0/1 编码  
现在有两个麻烦：
1. 手动处理两边要写两套代码 ，容易乱  
2. 致命问题 ：用训练集算出的中位数去填验证集，才不会数据泄漏；但手动做很容易用全量数据算中位数 → 泄漏 

### 解决的办法是使用 `SimpleImputer`，`OneHotEncoder`，`ColumnTransformer`，`Pipeline`
#### SimpleImputer —— 填缺失值的机器人
```python
from sklearn.impute import SimpleImputer
```  
```python
SimpleImputer(strategy='median')      # 用中位数填  
SimpleImputer(strategy='most_frequent')  # 用众数填（类别列用）
```  
它记住"训练集的中位数是多少"，之后对验证集/测试集都 **用同一个值** 填。这就防住了数据泄漏。

#### OneHotEncode —— 类别转数字的机器人
```python
from sklearn.preprocessing import OneHotEncoder
```  
```python
OneHotEncoder(handle_unknown='ignore')
```  
- `handle_unknown='ignore'` ：测试集出现训练集没见过的类别时，不报错，直接全 0
- 它会记住训练时的类别列表，保证训练集和测试集编码出的列完全一致

#### ColumnTransformer —— 分发器
```python
from sklearn.compose import ColumnTransformer
```  
```python
ColumnTransformer(transformers=[
    ('num', 数值列的处理流程, 数值列名列表),
    ('cat', 类别列的处理流程, 类别列名列表),
])
```
作用就一句话： "**数值列走左边这条路，类别列走右边这条路**" ，各自用各自的机器人处理。

#### Pipeline —— 流水线 
```python
from sklearn.pipeline import Pipeline
``` 
```python
Pipeline(steps=[
    ('prep', ColumnTransformer对象),
    ('model', GradientBoostingRegressor()),
])
```  
把"预处理"和"模型"焊成一个整体。之后你只需要：    
```python
pipe.fit(train_X, train_y)          # 预处理 + 训练，一步完成  
preds = pipe.predict(val_X)          # 预处理 + 预测，一步完成
```  
**关键好处：预处理被"包"在模型里了**。 交叉验证时，每一折都会 **独立地** 用该折的训练部分算中位数/类别列表，绝对不会泄漏。手动做几乎做不到这一点。




# 2. 加载数据

```python
df_train = pd.read_csv('/kaggle/input/competitions/home-data-for-ml-course/train.csv')
df_test = pd.read_csv('/kaggle/input/competitions/home-data-for-ml-course/test.csv')

df_train.head()
```
读取训练集和测试集，查看前五行  


# 3.让我们去探索吧！！！

## 3.1 查看数据范围有多大
```python
r, c = df_train.shape
print(f"The training data has {r} rows and {c} columns")
r, c = df_test.shape
print(f"The validation data has {r} rows and {c} columns")

# The training data has 1460 rows and 81 columns
# The validation data has 1459 rows and 80 columns
```

## 3.2 查看每列是什么类型的数据，缺失值有多少
```python
df_train.info()

# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 1460 entries, 0 to 1459
# Data columns (total 81 columns):
#  '#'   Column         Non-Null Count  Dtype  
# ---  ------         --------------  -----  
#  0   Id             1460 non-null   int64  
#  1   MSSubClass     1460 non-null   int64  
#  2   MSZoning       1460 non-null   object 
#  3   LotFrontage    1201 non-null   float64
#  4   LotArea        1460 non-null   int64  
#  5   Street         1460 non-null   object 
#  6   Alley          91 non-null     object 
#  7   LotShape       1460 non-null   object 
#  8   LandContour    1460 non-null   object 
#  9   Utilities      1460 non-null   object 
#  10  LotConfig      1460 non-null   object 
#  11  LandSlope      1460 non-null   object 
#  12  Neighborhood   1460 non-null   object 
#  13  Condition1     1460 non-null   object 
#  14  Condition2     1460 non-null   object 
#  15  BldgType       1460 non-null   object 
#  16  HouseStyle     1460 non-null   object 
#  17  OverallQual    1460 non-null   int64  
#  18  OverallCond    1460 non-null   int64  
#  19  YearBuilt      1460 non-null   int64  
#  20  YearRemodAdd   1460 non-null   int64  
#  21  RoofStyle      1460 non-null   object 
#  22  RoofMatl       1460 non-null   object 
#  23  Exterior1st    1460 non-null   object 
#  24  Exterior2nd    1460 non-null   object 
#  25  MasVnrType     588 non-null    object 
#  26  MasVnrArea     1452 non-null   float64
#  27  ExterQual      1460 non-null   object 
#  28  ExterCond      1460 non-null   object 
#  29  Foundation     1460 non-null   object 
#  30  BsmtQual       1423 non-null   object 
#  31  BsmtCond       1423 non-null   object 
#  32  BsmtExposure   1422 non-null   object 
#  33  BsmtFinType1   1423 non-null   object 
#  34  BsmtFinSF1     1460 non-null   int64  
#  35  BsmtFinType2   1422 non-null   object 
#  36  BsmtFinSF2     1460 non-null   int64  
#  37  BsmtUnfSF      1460 non-null   int64  
#  38  TotalBsmtSF    1460 non-null   int64  
#  39  Heating        1460 non-null   object 
#  40  HeatingQC      1460 non-null   object 
#  41  CentralAir     1460 non-null   object 
#  42  Electrical     1459 non-null   object 
#  43  1stFlrSF       1460 non-null   int64  
#  44  2ndFlrSF       1460 non-null   int64  
#  45  LowQualFinSF   1460 non-null   int64  
#  46  GrLivArea      1460 non-null   int64  
#  47  BsmtFullBath   1460 non-null   int64  
#  48  BsmtHalfBath   1460 non-null   int64  
#  49  FullBath       1460 non-null   int64  
#  50  HalfBath       1460 non-null   int64  
#  51  BedroomAbvGr   1460 non-null   int64  
#  52  KitchenAbvGr   1460 non-null   int64  
#  53  KitchenQual    1460 non-null   object 
#  54  TotRmsAbvGrd   1460 non-null   int64  
#  55  Functional     1460 non-null   object 
#  56  Fireplaces     1460 non-null   int64  
#  57  FireplaceQu    770 non-null    object 
#  58  GarageType     1379 non-null   object 
#  59  GarageYrBlt    1379 non-null   float64
#  60  GarageFinish   1379 non-null   object 
#  61  GarageCars     1460 non-null   int64  
#  62  GarageArea     1460 non-null   int64  
#  63  GarageQual     1379 non-null   object 
#  64  GarageCond     1379 non-null   object 
#  65  PavedDrive     1460 non-null   object 
#  66  WoodDeckSF     1460 non-null   int64  
#  67  OpenPorchSF    1460 non-null   int64  
#  68  EnclosedPorch  1460 non-null   int64  
#  69  3SsnPorch      1460 non-null   int64  
#  70  ScreenPorch    1460 non-null   int64  
#  71  PoolArea       1460 non-null   int64  
#  72  PoolQC         7 non-null      object 
#  73  Fence          281 non-null    object 
#  74  MiscFeature    54 non-null     object 
#  75  MiscVal        1460 non-null   int64  
#  76  MoSold         1460 non-null   int64  
#  77  YrSold         1460 non-null   int64  
#  78  SaleType       1460 non-null   object 
#  79  SaleCondition  1460 non-null   object 
#  80  SalePrice      1460 non-null   int64  
# dtypes: float64(3), int64(35), object(43)
# memory usage: 924.0+ KB
```
#### 前三行数据：
```python
<class 'pandas.core.frame.DataFrame'>   → 这是个 DataFrame
RangeIndex: 1460 entries, 0 to 1459     → 1460 行，索引从 0 到 1459
Data columns (total 81 columns):        → 共 81 列
```

#### 中间部分的那张表：
|字段|含义|
|-|-|
|#|列的位置编号（0, 1, 2…）|
|Column|列名|
|Non-Null Count|这一列有多少个非空值|
|Dtype|这一列的数据类型|
拿`LotFrontage` 举例：`1201 non-null` 。总行数是 1460，所以缺失 = 1460 − 1201 = 259 。
**这个减法就是 info() 最实用的地方** ：你不用另外写`isnull()` ，扫一眼就知道哪列缺。反过来，凡是写着`1460 non-null` 的列（比如`Id` 、`MSSubClass` ）就是完全干净的。

#### 三种dtype需要分清楚
```python
int64    → 整数
float64  → 小数
object   → 文本（字符串）
``` 
最后的汇总就是告诉所有列名的数据类型的个数之和
```python
dtypes: float64(3), int64(35), object(43)
```

#### 坑1：dtype 是 pandas 对存储格式的判断，不是对语义的判断。  
看`MSSubClass` ：dtype 是`int64` ，看起来是数字。但它其实是 **建筑类型的编码** ——20 代表 1 层半，60 代表 2 层，120 代表 1 层……这些数字的大小 **没有任何数学含义** ，120 不代表“比 20 大 6 倍”。
比如还有：  
`OverallQual` /`OverallCond` ：int64，但语义是 1~10 的 等级评分 （有序类别）  
`YearBuilt` /`YearRemodAdd` ：int64，但语义是 年份 ，算平均值没意义  
`MoSold` ：int64，但语义是月份，12 月和 1 月是相邻的  


