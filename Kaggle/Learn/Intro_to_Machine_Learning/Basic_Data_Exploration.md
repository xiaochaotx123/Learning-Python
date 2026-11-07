### Tutorial

#### 使用Pandas熟悉您的数据    

任何机器学习项目的第一步都是熟悉数据。您将使用Pandas库进行此操作。Pandas是数据科学家用来探索和操纵数据的主要工具。大多数人在代码中将pandas缩写为pd  

```python
import pandas as pd
```
Pandas库最重要的部分是DataFrame。DataFrame包含您可能认为是表的数据类型。这类似于Excel中的工作表或SQL数据库中的表。  

Pandas对于你想用这类数据做的大多数事情都有强大的方法。

例如，我们将查看澳大利亚墨尔本的房价数据。在实践练习中，您将把相同的过程应用于一个新的数据集，该数据集包含爱荷华州的房价。  

示例（墨尔本）数据位于文件路径中。../input/melbourne-housing-snapshot/melb_data.csv。 我们使用以下命令加载和浏览数据：  

```python
# save filepath to variable for easier access
melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
# read the data and store data in DataFrame titled melbourne_data
melbourne_data = pd.read_csv(melbourne_file_path) 
# print a summary of the data in Melbourne data
melbourne_data.describe()
```

#### 解读数据描述    

结果显示原始数据集中每列有8个数字。第一个数字是计数，显示有多少行没有缺失值。    

缺失值的出现有很多原因。例如，在调查一间卧室的房子时，不会收集第二间卧室的大小。我们将回到缺失数据的话题。  

第二个值是平均值，即平均值。在这种情况下，std是标准偏差，它衡量的是数值的分散程度。  

要解释最小值、25%、50%、75%和最大值，想象一下从最低值到最高值对每列进行排序。第一个（最小）值是最小值。如果你遍历列表的四分之一，你会发现一个大于值的25%但小于值的75%的数字。这就是25%的值（发音为“25th percentury”）。第50和第75百分位数的定义类似，最大值是最大的数字。



### Exercise  

这项练习将考验你读取数据文件并理解其中统计信息的能力。  

在后续的练习中，你将运用各种技术来筛选数据、构建机器学习模型，并不断对模型进行优化。  

该课程的示例均使用了墨尔本的数据。为了确保您能够独立运用这些技巧，您需要将它们应用到另一个数据集上——也就是爱荷华州的房价数据。

#### Exercises
运行下面的代码，以启用代码检查功能。该功能会随时验证你的代码是否正确。  

```python
# Set up code checking
from learntools.core import binder
binder.bind(globals())
from learntools.machine_learning.ex2 import *
print("Setup Complete")
```  
这是练习题的自动判卷系统，不是机器学习代码。`learntools` 是 Kaggle 自己开发的内部库，你在真实比赛和工作中永远见不到它。



#### Step 1: Loading Data
将Iowa数据文件读取到名为home_data的Pandas DataFrame中。

```python
import pandas as pd

# Path of the file to read
iowa_file_path = '../input/home-data-for-ml-course/train.csv'

# Fill in the line below to read the file into a variable home_data
home_data = pd.read_csv(iowa_file_path)

# Call line below with no argument to check that you've loaded the data correctly
step_1.check()
```

#### Step 2: Review The Data  

使用您学习的命令查看数据的摘要统计信息。然后填写变量以回答以下问题  

```python
# Print summary statistics in next line
print(home_data.describe())
```

```python
# What is the average lot size (rounded to nearest integer)?
avg_lot_size = round(home_data['LotArea'].mean())

# As of today, how old is the newest home (current year - the date in which it was built)
newest_home_age = 2026 - home_data['YearBuilt'].max()

# Checks your answers
step_2.check()
```

#### Think About Your Data  
`newest_home_age` 算出来是 16 年左右，说明最新房子是 2010 年建的。为什么数据里没有 2011 年以后的房子？题目给了两个解释，问你对模型的"信任度"会怎么变：   
|解释|对模型的信任度|
|----|------------|
|当地就没再建新房|信任度不受影响。房子的存量没变，模型学的规律和现实一致|
|数据是很多年前收集的|信任度要打折扣。2011–2026 年建的新房不在数据里，你的模型根本没见过，用它预测今天的房子就是外推 ——超出它学过的范围|  

第 2 种情况在机器学习里有个专门的名字：**数据漂移**（data drift） 。模型只对你训练数据覆盖的那段世界有效