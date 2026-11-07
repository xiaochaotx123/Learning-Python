### Tutorial  

#### 引言  

决策树会让你面临艰难的选择。一棵枝叶繁茂的树可能会因为每个预测都基于仅来自树顶几个样本的历史数据而出现过拟合的情况。而一棵枝叶稀疏的树则表现不佳，因为它无法捕捉到原始数据中的各种差异。  

即便是最先进的建模技术，也面临着过拟合与欠拟合之间的矛盾。不过，许多模型都包含了一些巧妙的设计思路，这些设计思路能够带来更好的性能。我们以`随机森林`为例来加以说明。  

随机森林使用**许多棵树**来进行预测，通过**汇总**每棵树的预测结果来做出最终预测。与单一决策树相比，随机森林的预测准确率通常要高得多，而且在使用默认参数时也能表现良好。如果你继续进行建模，还可以构建出性能更优秀的模型，不过许多模型对参数的选择非常敏感。    

#### 示例  

你已经多次看到用于加载数据的代码了。在数据加载完成后，我们会得到以下变量：  

- train_X
- val_X 
- train_y 
- val_y  

```python
import pandas as pd
    
# Load data
melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
melbourne_data = pd.read_csv(melbourne_file_path) 
# Filter rows with missing values
melbourne_data = melbourne_data.dropna(axis=0)
# Choose target and features
y = melbourne_data.Price
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'BuildingArea', 
                        'YearBuilt', 'Lattitude', 'Longtitude']
X = melbourne_data[melbourne_features]

from sklearn.model_selection import train_test_split

# split data into training and validation data, for both features and target
# The split is based on a random number generator. Supplying a numeric value to
# the random_state argument guarantees we get the same split every time we
# run this script.
train_X, val_X, train_y, val_y = train_test_split(X, y,random_state = 0)
```
  

我们构建随机森林模型的方式与在 scikit-learn 中构建决策树的方式类似——这次使用的是 `RandomForestRegressor` 类而不是 `DecisionTreeRegressor` 类。
```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

forest_model = RandomForestRegressor(random_state=1)
forest_model.fit(train_X, train_y)
melb_preds = forest_model.predict(val_X)
print(mean_absolute_error(val_y, melb_preds))

# 输出：
# 191669.7536453626
```  

#### 结论  

虽然还有进一步改进的空间，但与250000的最佳决策树错误相比，这是一个很大的改进。有一些参数可以让你自行调整随机森林的性能，就像我们调整单决策树的最大深度那样。不过，随机森林模型的一个优点就是，即使不需要进行这些调整，它们通常也能表现相当不错。  


### Exercies  

#### 回顾过去  

目前所写的代码：  

```python
# Code you have previously used to load data
import pandas as pd
from sklearn.metrics import mean_absolute_error
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeRegressor


# Path of the file to read
iowa_file_path = '../input/home-data-for-ml-course/train.csv'

home_data = pd.read_csv(iowa_file_path)
# Create target object and call it y
y = home_data.SalePrice
# Create X
features = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']
X = home_data[features]

# Split into validation and training data
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)

# Specify Model
iowa_model = DecisionTreeRegressor(random_state=1)
# Fit Model
iowa_model.fit(train_X, train_y)

# Make validation predictions and calculate mean absolute error
val_predictions = iowa_model.predict(val_X)
val_mae = mean_absolute_error(val_predictions, val_y)
print("Validation MAE when not specifying max_leaf_nodes: {:,.0f}".format(val_mae))

# Using best value for max_leaf_nodes
iowa_model = DecisionTreeRegressor(max_leaf_nodes=100, random_state=1)
iowa_model.fit(train_X, train_y)
val_predictions = iowa_model.predict(val_X)
val_mae = mean_absolute_error(val_predictions, val_y)
print("Validation MAE for best value of max_leaf_nodes: {:,.0f}".format(val_mae))


# Set up code checking
from learntools.core import binder
binder.bind(globals())
from learntools.machine_learning.ex6 import *
print("\nSetup complete")
```


数据科学并不总是如此简单。不过，用随机森林替代决策树确实是一个简单的改进。  

#### 步骤 1：使用随机森林模型  

```python
from sklearn.ensemble import RandomForestRegressor

# Define the model. Set random_state to 1
rf_model = RandomForestRegressor(random_state = 1)

# fit your model
rf_model.fit(train_X, train_y)

# Calculate the mean absolute error of your Random Forest model on the validation data
rf_val_mae = mean_absolute_error(val_y, rf_model.predict(val_X))

print("Validation MAE for Random Forest Model: {}".format(rf_val_mae))

# Check your answer
step_1.check()
```  