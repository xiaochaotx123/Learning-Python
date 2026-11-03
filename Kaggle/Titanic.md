#### 使用泰坦尼克号乘客的数据（姓名、年龄、票价等）来预测谁会幸存，谁会死亡。  
#### 数据中有三个文件：（1）train.csv，（2）test.csv 和（3）gender_submission.csv。  
#### （1）train.csv  
train.csv包含机上乘客子集的详细信息（确切地说是891名乘客，其中每位乘客在表中得到一个不同的行）  
第二列（“幸存”）中的值可用于确定每位乘客是否幸存：
- 如果是“1”，乘客幸存了下来。
- 如果是“0”，乘客就死了。

#### （2）test.csv 
使用train.csv中的模式，您必须预测机上其他418名乘客（test.csv中）是否幸存。  
请注意，test.csv没有“存活”列——这些信息对你来说是隐藏的，你预测这些隐藏值的能力将决定你在比赛中的得分有多高！  


#### （3）gender_submission.csv  
gender_submission.csv文件作为示例提供，显示了您应该如何构建预测。据预测，所有女性乘客幸存，所有男性乘客死亡。你关于生存的假设可能会有所不同，这将导致不同的提交文件。但是，就像这个文件一样，你的提交应该有：  
- “PassengerId”列，其中包含test.csv中每个乘客的ID。
- “幸存”列（您将创建！），其中“1”表示您认为乘客幸存的行，“0”表示您预测乘客死亡的行。  


您将训练自己的机器学习模型来改进您的预测  

首先要做的是创建一个Kaggle笔记本，在其中存储所有代码。您可以使用Kaggle笔记本快速编写代码，而无需在计算机上安装任何东西。（如果您对深度学习感兴趣，我们还提供免费的GPU访问！）  

```python
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session

# Use the kagglehub client library to attach Kaggle resources like competitions, datasets, and models to your session
# Learn more about kagglehub: https://github.com/Kaggle/kagglehub/blob/main/README.md

import kagglehub
# kagglehub.dataset_download('<owner>/<dataset-slug>')
```

```python
train_data = pd.read_csv("/kaggle/input/competitions/titanic/train.csv")
train_data.head()
```

```python
test_data = pd.read_csv("/kaggle/input/competitions/titanic/test.csv")
test_data.head()
```

```python
women = train_data.loc[train_data.Sex == 'female']["Survived"]
rate_women = sum(women)/len(women)

print("% of women who survived:", rate_women)
```

```python
men = train_data.loc[train_data.Sex == 'male']["Survived"]
rate_men = sum(men)/len(men)

print("% of men who survived:", rate_men)
```


正如你所想象的，通过考虑多列，我们可以发现更复杂的模式，这些模式可能会产生更明智的预测。由于很难同时考虑多个列（或者，同时考虑许多不同列中的所有可能模式需要很长时间），我们将使用机器学习为我们实现自动化。  

#### 你的第一个机器学习模型  
我们将构建所谓的随机森林模型。该模型由几棵“树”组成（下图中有三棵树，但我们将构建100棵！），它们将分别考虑每个乘客的数据，并对个人是否幸存进行投票。然后，随机森林模型做出了一个民主的决定：得票最多的结果获胜   
下面的代码单元格在数据的四个不同列（“Pclass”、“Sex”、“SibSp”和“Parch”）中查找模式。它根据train.csv文件中的模式在随机森林模型中构建树，然后在test.csv中为乘客生成预测。该代码还将这些新的预测保存在CSV文件submission.CSV中。  
```python
from sklearn.ensemble import RandomForestClassifier

y = train_data["Survived"]

features = ["Pclass", "Sex", "SibSp", "Parch"]
X = pd.get_dummies(train_data[features])
X_test = pd.get_dummies(test_data[features])

model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=1)
model.fit(X, y)
predictions = model.predict(X_test)

output = pd.DataFrame({'PassengerId': test_data.PassengerId, 'Survived': predictions})
output.to_csv('submission.csv', index=False)
print("Your submission was successfully saved!")
```
