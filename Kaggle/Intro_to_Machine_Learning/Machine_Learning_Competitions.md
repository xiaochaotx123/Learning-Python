### Tutorial  

机器学习竞赛是提升你的数据科学能力并衡量你进步情况的绝佳方式。  

在下一个练习中，你将需要创建并提交关于 `Kaggle` 学习用户住宅价格竞赛的预测结果。  

### Exercise  

#### 引言  

在这个练习中，你将创建一个预测模型，并提交给 Kaggle 竞赛使用。之后，你可以不断改进模型（例如通过添加更多特征），以应用你所学的知识，从而在排行榜上不断提升自己的排名。    

首先，运行下面的代码单元格，以配置代码检查和数据集的路径。  

```python
# Set up code checking
from learntools.core import binder
binder.bind(globals())
from learntools.machine_learning.ex7 import *

# Set up filepaths
import os
if not os.path.exists("../input/train.csv"):
    os.symlink("../input/home-data-for-ml-course/train.csv", "../input/train.csv")  
    os.symlink("../input/home-data-for-ml-course/test.csv", "../input/test.csv")   
```  


这是你们迄今为止编写的部分代码。请再次运行这些代码。  

```python
# Import helpful libraries
import pandas as pd
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error
from sklearn.model_selection import train_test_split

# Load the data, and separate the target
iowa_file_path = '../input/train.csv'
home_data = pd.read_csv(iowa_file_path)
y = home_data.SalePrice

# Create X (After completing the exercise, you can return to modify this line!)
features = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']

# Select columns corresponding to features, and preview the data
X = home_data[features]
X.head()

# Split into validation and training data
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)

# Define a random forest model
rf_model = RandomForestRegressor(random_state=1)
rf_model.fit(train_X, train_y)
rf_val_predictions = rf_model.predict(val_X)
rf_val_mae = mean_absolute_error(rf_val_predictions, val_y)

print("Validation MAE for Random Forest Model: {:,.0f}".format(rf_val_mae))
```  

#### 为比赛训练模型  

上述代码单元是在 `train_X` 和 `train_y` 上训练随机森林模型的步骤。  

请使用下方的代码来构建随机森林模型，并对其进行训练，训练的数据包括 `X` 和 `y` 的所有数据。  

```python
# To improve accuracy, create a new Random Forest model which you will train on all training data
rf_model_on_full_data = RandomForestRegressor(random_state = 1)


# fit rf_model_on_full_data on all data from the training data
rf_model_on_full_data.fit(X, y)
```    

现在，读取“test”数据文件，然后应用你的模型来进行预测。  

```python
# path to file you will use for predictions
test_data_path = '../input/test.csv'

# read test data file using pandas
test_data = pd.read_csv(test_data_path)

# create test_X which comes from test_data but includes only the columns you used for prediction.
# The list of columns is stored in a variable called features
test_X = test_data[features]

# make predictions which we will submit. 
test_preds = rf_model_on_full_data.predict(test_X)
```  
