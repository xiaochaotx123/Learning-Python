### Tutorial

### 模型验证：评估模型的性能，以便对各种方案进行测试和比较。    


你已经构建了一个模型。但是，这个模型的性能如何呢？  

如何使用模型验证来衡量模型的质量。准确评估模型质量是逐步改进模型的关键所在。

#### 什么是模型验证    

你需要对几乎每一个自己构建的模型进行评估。在大多数情况下（尽管不是所有情况），衡量模型质量的关键指标就是预测准确性。换句话说，模型的预测结果是否会接近实际发生的情况。  

许多人在使用预测准确性进行评估时犯了一个严重的错误。他们利用训练数据做出预测，然后将这些预测结果与训练数据中的真实值进行比较。你会很快意识到这种方法的缺陷以及如何解决它。不过，我们先来思考一下该如何进行这种评估吧。    


首先，需要将模型预测的结果进行整理，使其易于理解。如果你比较了 10,000 栋房屋的预测价值和实际价值，你会发现预测结果中有好的，也有不好的。而试图逐一查看这 10,000 栋房屋的预测值和实际价值则毫无意义。我们需要将这些信息汇总为一个单一的指标来呈现。  


有很多指标可以用来总结模型的质量，但我们首先从其中一个叫做**平均绝对误差** `Mean Absolute Error (also called MAE)`的指标开始介绍。让我们从这个指标的最后一个词 **“误差”** 入手来解析这个指标。  


每栋房子的预测误差为： 
```python
error=actual−predicted
```  


所以，如果一栋房子的价格为 15 万美元，而你的预测价格是 10 万美元，那么误差就是 5 万美元。  


我们使用 MAE 度量标准，即取每个误差的绝对值。这样就能将每个误差转化为正数。然后，我们计算这些绝对误差的平均值。这就是我们用来衡量模型质量的标准。用简单的语言来说，就是这样的计算方法。   


平均来说，我们的预测误差在大约 X 左右。  


要计算 MAE，我们首先需要一个模型：

```python
# Data Loading Code Hidden Here
import pandas as pd

# Load data
melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
melbourne_data = pd.read_csv(melbourne_file_path) 
# Filter rows with missing price values
filtered_melbourne_data = melbourne_data.dropna(axis=0)
# Choose target and features
y = filtered_melbourne_data.Price
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'BuildingArea', 
                        'YearBuilt', 'Lattitude', 'Longtitude']
X = filtered_melbourne_data[melbourne_features]

from sklearn.tree import DecisionTreeRegressor
# Define model
melbourne_model = DecisionTreeRegressor()
# Fit model
melbourne_model.fit(X, y)
```

一旦我们有了模型，就可以按照以下方法来计算平均绝对误差了：  
```python
from sklearn.metrics import mean_absolute_error

predicted_home_prices = melbourne_model.predict(X)
mean_absolute_error(y, predicted_home_prices)
```  


#### “以样本分数作为评判标准”的问题   

我们刚刚计算出的这个指标可以被称为“样本内”得分。在构建模型和评估模型时，我们都只使用了单个样本的房屋数据。这样做其实存在缺陷。  

想象一下，在大型房地产市场中，房子的门的颜色与房价并无关联。  

然而，在用于构建模型的样本数据中，所有带有绿色门面的房屋都价格非常昂贵。模型的任务就是找出可以预测房屋价格的规律，因此它会注意到这种规律，并会始终将带有绿色门面的房屋的价格预测为较高。  

由于这种模式是从训练数据中衍生出来的，因此该模型在训练数据中的表现看起来是准确的。  

但是，如果这种模式在模型处理新数据时不再适用，那么这种模型在实际应用中的准确性就会大大降低。  

由于模型的实用价值在于能够对新数据做出预测，因此我们通常会使用那些并未用于构建模型的数据进行性能评估。实现这一目的最简单的方法就是：在模型构建过程中排除某些数据，然后使用这些未被使用的数据来测试模型的准确性。这类数据被称为验证数据。 

#### 编程  


`scikit-learn` 库中有一个函数 `train_test_split` ，可以将数据分为两部分。我们将使用其中一部分数据作为训练数据来拟合模型，而另一部分数据则作为验证数据来进行计算 `mean_absolute_error` 。  

以下是代码：
```python
from sklearn.model_selection import train_test_split

# 将数据分为特征和目标的训练和验证数据。
# 分割基于随机数生成器
# 为 random_state 参数提供一个数值可以保证每次运行此脚本时都得到相同的分割。
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 0)
# 定义模型
melbourne_model = DecisionTreeRegressor()
# 拟合模型
melbourne_model.fit(train_X, train_y)

# 在验证数据上获取预测价格
val_predictions = melbourne_model.predict(val_X)
print(mean_absolute_error(val_y, val_predictions))
```

在样本数据范围内，你的绝对误差约为 500 美元。而在样本数据之外，误差则超过了 25 万美元。  

这就是那种几乎完全正确的模型与那些在实际使用中完全不可用的模型之间的区别。作为参考，验证数据中的平均房屋价值为 110 万美元。因此，新数据中的误差大约相当于平均房屋价值的四分之一。  

改进这个模型的方法有很多，比如尝试使用更有效的特征或不同类型的模型。

### 总结  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
- 用 **训练时没见过** 的数据来评估模型，分数才有意义。
- **MAE** 怎么算：误差 = 真实值 − 预测值  
一套房真实 15 万，你预测 10 万 → 误差 = +5 万。另一套真实 10 万，你预测 15 万 → 误差 = −5 万。正负会互相抵消 （5 万和 −5 万加起来是 0），所以 MAE 取 绝对值 ，再求平均：
```python
from sklearn.metrics import mean_absolute_error
mean_absolute_error(y, predictions)
```

- 为什么"样本内分数"是骗人的  
真实世界里，门的颜色和房价 **毫无关系** 。
但在你的训练样本里，恰好所有绿门的房子都很贵。模型的任务是"找规律"，**它不管这规律是真是假**，它只会发现： 绿门 → 高价 ，然后把这个规律记下来。   

结果：    

|评估方式|MAE|说明了什么|
|-------|---|---------|
|样本内 （用训练数据评估）|约 500 美元|假象。模型记住了绿门这条"规律"，在见过的数据上完美|
|样本外 （用没见过的数据评估|超过 25 万美元|真相。新房子里绿门不代表贵，规律失效|    

对照参考：验证集平均房价约 110 万美元 ，25 万的误差 ≈ 房价的四分之一 。这个模型在实际使用中基本没用。  
500 美元 → 25 万美元，差 500 倍。 这就是"背答案"和"会做题"的真实差距。  

- 为什么样本内 MAE 是 500 而不是 0？  
之前的"叶子平均值"——有些房子特征完全相同、挤在同一片叶子里，输出的是它们的平均价，所以有微小误差。500 美元就是这么来的。  

- train_test_split 拆解：
```python
from sklearn.model_selection import train_test_split

train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=0)
```  

|参数/细节|说明|
|--------|----|
|作用|把数据随机切成两份：训练集（默认 75%）和验证集（默认 25%）|
|返回 4 个值|顺序是`train_X, val_X, train_y, val_y` —— **先两个 X 再两个 y** ，不是 X/y 交替|
|random_state=0|锁定切分方式，保证每次运行切得一样，结果可复现|
|为什么必须随机|如果按行号切（比如前 75% 训练），数据可能有隐藏顺序（比如按年份排列），导致验证集失真|  

```python
melbourne_model.fit(train_X, train_y)          # 只用训练集学
val_predictions = melbourne_model.predict(val_X)  # 只在验证集上预测
mean_absolute_error(val_y, val_predictions)   # 拿验证集真实值对比
```  
```python
train_X, train_y  →  fit 用
val_X             →  predict 用
val_y             →  算误差用（模型从来没见过它）
```


- `train_test_split` 有个弱点： 切法随机，分数会抖 。你换个`random_state` ，验证 MAE 可能差几千美元。所以真实比赛中会用 **K 折交叉验证（cross-validation）** ：把数据切成 5 折，轮流拿 1 折当验证、其余训练，跑 5 次取平均。 分数更稳、更可信 。这是你打 Playground 时必用的技能，现在知道有这么个东西就行。
### 总结  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Exercise  


运行下面的单元格，以设置你的编码环境，也就是之前练习中未完成的那些设置。  

```python
# Code you have previously used to load data
import pandas as pd
from sklearn.tree import DecisionTreeRegressor

# Path of the file to read
iowa_file_path = '../input/home-data-for-ml-course/train.csv'

home_data = pd.read_csv(iowa_file_path)
y = home_data.SalePrice
feature_columns = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']
X = home_data[feature_columns]

# Specify Model
iowa_model = DecisionTreeRegressor()
# Fit Model
iowa_model.fit(X, y)

print("First in-sample predictions:", iowa_model.predict(X.head()))
print("Actual target values for those homes:", y.head().tolist())

# Set up code checking
from learntools.core import binder
binder.bind(globals())
from learntools.machine_learning.ex4 import *
print("Setup Complete")
```  


#### 步骤 1：分割你的数据  

使用 `train_test_split` 函数来分割你的数据。

请为 `random_state=1` 提供该参数，这样 `check` 在验证代码时就能知道该如何处理。

记住，你的特征数据被加载到了 DataFrame X 中，而目标变量则被加载到了 y 中。  

```python
# Import the train_test_split function and uncomment
from sklearn.model_selection import train_test_split  

# fill in and uncomment
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 1)

# Check your answer
step_1.check()
```

#### 步骤 2：指定模型并对其进行拟合   

创建一個 `DecisionTreeRegressor` 模型，并将其适配到相关数据上。在创建模型时，将 `random_state` 设置为 1。  

```python
# You imported DecisionTreeRegressor in your last exercise
# and that code has been copied to the setup code above. So, no need to
# import it again

# Specify the model
iowa_model = DecisionTreeRegressor(random_state = 1)  

# Fit iowa_model with the training data.
iowa_model.fit(train_X, train_y)

# Check your answer
step_2.check()
```  

#### 步骤 3：使用验证数据进行预测  


```python
# Predict with all validation observations
val_predictions = iowa_model.predict(val_X)

# Check your answer
step_3.check()
```  

检查你的预测结果与验证数据中的实际值是否一致。  

```python
# print the top few validation predictions
print(val_predictions[0:5])
# print the top few actual prices from validation data
print(val_y[0:5])
```

#### 步骤 4：计算验证数据中的平均绝对误差  

```python
from sklearn.metrics import mean_absolute_error
val_mae = mean_absolute_error(val_y, val_predictions)

# uncomment following line to see the validation_mae
print(val_mae)

# Check your answer
step_4.check()
```  