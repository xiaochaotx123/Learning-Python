### Tutorial

#### 选择建模数据  

你的数据集有太多的变量，你无法理解，甚至无法很好地打印出来。你如何将如此庞大的数据量缩减到你能理解的程度？  

要选择变量/列，我们需要看到数据集中所有列的列表。这是通过DataFrame的columns属性（下面的代码底线）完成的。  
s
```python
import pandas as pd

melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
melbourne_data = pd.read_csv(melbourne_file_path) 
melbourne_data.columns
```
`.columns` 返回所有列名。数据列太多时，先看列名，才知道有哪些牌可以打。  


```python
# The Melbourne data has some missing values (some houses for which some variables weren't recorded.)
# We'll learn to handle missing values in a later tutorial.  
# Your Iowa data doesn't have missing values in the columns you use. 
# So we will take the simplest option for now, and drop houses from our data. 
# Don't worry about this much for now, though the code is:

# dropna drops missing values (think of na as "not available")
melbourne_data = melbourne_data.dropna(axis=0)
```
- melbourne_data = melbourne_data.dropna(axis=0) 表示删除所有存在缺失值的行，axis = 0表示操作行；pd.dropna()表示删除缺失值


#### 选择预测目标  

我们将使用点表示法来选择想要预测的列，这个列被称为预测目标。按照惯例，预测目标被命名为y。因此，我们需要保存墨尔本数据集中房屋价格信息的代码就是： 
```python
y = melbourne_data.Price
```
`melbourne_data.Price` 这种 点表示法 只有在列名是合法的 Python 名字（无空格、无特殊字符）时才能用。列名里有空格就必须写`melbourne_data['Sale Price']` 。所以 方括号写法更通用 ，点表示法只是省事。  





#### 选择“特征”  

输入到我们模型中的列（后来用于进行预测）称为“特征”。在我们的例子中，这些列将用于确定房价。有时，您将使用除目标之外的所有列作为特征。其他时候，你会用更少的功能做得更好。  

现在，我们将构建一个只有少数功能的模型。稍后，您将看到如何迭代和比较使用不同功能构建的模型。  

我们通过在括号内提供列名列表来选择多个功能。该列表中的每个项目都应该是一个字符串（带引号）。  

以下是一个示例：  

```python
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'Lattitude', 'Longtitude']
```  
1. 为什么用列表选多列`df[['列A','列B']]` → 返回 DataFrame（二维表格）`df['列A']` → 返回 Series（一维） 所以`X` 是二维的（样本 × 特征），`y` 是一维的。 模型的输入永远是二维，标签是一维 ——这个维度概念必须建立。    
2. 特征选择本身就是个决策 课文说"有时用更少的特征效果更好"。这不是套话：特征多了会有噪声、会过拟合。 选哪些列，就是 Kaggle 上最大的功夫所在。  




 
按照惯例，这些数据被称为X。  

```python
X = melbourne_data[melbourne_features]
```

让我们快速回顾一下我们将用于预测房价的数据。我们会使用 `describe` 方法和 `head` 方法，后者展示了其中几行数据的情况。  

```python
X.describe()
```

```python
X.head()
```

使用这些命令来可视化地检查数据，是数据科学家工作的重要部分。你经常会发现数据集中有一些值得进一步研究的惊喜之处。  


#### 构建你的模型  

你将使用 `scikit-learn` 库来构建你的模型。在编程时，这个库通常被称为 `sklearn`，正如你在示例代码中看到的那样。`scikit-learn` 无疑是用于处理通常以 `DataFrame` 形式存储的数据的最流行的库。

构建和使用模型的步骤如下：  
- 定义：这将是一种什么样的模型呢？是决策树模型吗？还是其他类型的模型呢？此外，该模型类型的一些参数也被明确规定了。  
- 功能：从给定的数据中提取模式。这正是建模的核心所在。 
- 预测：正如听起来那样  
- 评估：确定模型预测结果的准确性。  

以下是一个使用 `scikit-learn` 库定义决策树模型并对其进行拟合的例子。其中，特征变量和目标变量被用于模型的训练过程。  

```python
from sklearn.tree import DecisionTreeRegressor

# 定义：这是一棵"回归树"
melbourne_model = DecisionTreeRegressor(random_state=1)

# 拟合：把题目 X 和答案 y 喂进去，让它自己学
melbourne_model.fit(X, y)
```

许多机器学习模型允许在模型训练中引入一定的随机性。指定一个数值 `random_state` 可以确保每次运行都能得到相同的结果。这被认为是一种良好的实践方式。你可以使用任何数值，而模型的质量并不会因为你选择的数值不同而产生显著变化。    

现在我们已经有了可以用来进行预测的完整模型了。  

在实践中，你通常需要对即将上市的新房屋进行预测，而不是已经定价好的现有房屋。不过，我们会先对训练数据的前几行进行预测，以了解预测函数的运作方式。  

```python
print("Making predictions for the following 5 houses:")
print(X.head())
print("The predictions are")
print(melbourne_model.predict(X.head()))
```
  


```python
from sklearn.tree import DecisionTreeRegressor

# 定义：这是一棵"回归树"
melbourne_model = DecisionTreeRegressor(random_state=1)

# 拟合：把题目 X 和答案 y 喂进去，让它自己学
melbourne_model.fit(X, y)
```  


#### sklearn.tree 和 DecisionTreeRegressor 是什么  
先理层级关系：  
```python
sklearn （scikit-learn，机器学习库）
└── tree （子模块，专门放"树模型"这一家族）
    ├── DecisionTreeRegressor   ← 回归树（预测数值）
    ├── DecisionTreeClassifier  ← 分类树（预测类别）
    └── ExtraTreeRegressor 等
```  

所以`from sklearn.tree import DecisionTreeRegressor` 的意思是：从`sklearn` 这个库下面的`tree` 模块里，取出`DecisionTreeRegressor` 这个类  

`sklearn` 是什么 ：Python 最主流的机器学习库，以后打 Kaggle 用到的 XGBoost、随机森林、交叉验证，大半都是这个家族的。  

`DecisionTreeRegressor` 是什么 ：一棵决策树 ，专门做回归 （输出连续数值，比如房价 25 万、30 万）。  

决策树的本质就是一堆 if/else   
它学出来的模型长这样（示意）：  
```python
Landsize > 500 ?
├── 是 → Rooms > 3 ?
│        ├── 是 → 预测 950,000
│        └── 否 → 预测 720,000
└── 否 → Bathroom > 1 ?
         ├── 是 → 预测 480,000
         └── 否 → 预测 310,000
```  
一条数据进来，沿着问题一路往下走，最后落到某个"叶子"，叶子上的值就是预测结果。  

它怎么长出这些问题的？ 在建树时，它尝试每个特征、每个切分点，找"切完之后两半的数据最'纯'"的那一刀（回归里用误差平方和来衡量纯度），然后递归地切下去。  

#### random_state=1 是什么  

它是"随机种子"，作用是让结果可复现。  

先说为什么会有随机：训练时如果有多个切分方案"同样好"，sklearn 会随机挑一个；有些参数（如特征子采样）本身也带随机。同一个脚本跑两次，理论上可能得到略有不同的树。  

`random_state=1` 就是告诉它：用 1 作为随机数的种子，每次都从同一个"随机序列"开始  


#### fit(X, y) 是什么  

`fit` = 训练。 这是整个机器学习里最重要的一个方法名，所有 sklearn 模型都有它。  

```python
melbourne_model.fit(X, y)
```
用一句话说： 把"题目"和"答案"一起交给模型，让它自己总结规律。  

具体到决策树，`fit` 内部干的事是：  
1.看当前这批数据，尝试所有特征、所有可能的切分点  
2.选出让"误差下降最多"的那一刀，把数据切成两半  
3.对两半分别重复上面两步  
4.直到满足停止条件（切不动了 / 到深度上限 / 样本太少）  

`fit` 跑完之后， 模型对象内部就被"写满"了 ：  

```python
melbourne_model.feature_importances_   # 每个特征的重要性分数
melbourne_model.tree_.node_count       # 树总共有多少个节点
melbourne_model.get_params()           # 看看它当前有哪些参数
```  

|坑|说明|
|--|----|
|`fit` 是原地修改|它改的是`melbourne_model` 这个对象本身，所以模型必须赋给变量保存下来|
|X 和 y 的行数必须一致|`X` 有 1000 行，`y` 也必须是 1000 个，否则直接报`ValueError`|
|X 必须是数值型二维表|有字符串列会报错（Titanic 里你用`get_dummies` 就是为了解决这个）|




### Exercise  


#### 步骤1：指定预测目标  
选择与销售价格对应的目标变量。将其保存到一个名为y的新变量中。您需要打印列列表以找到所需列的名称  

```python
# print the list of columns in the dataset to find the name of the prediction target
print(home_data.columns)
```  
```python
y = home_data['SalePrice']

# Check your answer
step_1.check()
```   


#### 第二步：创建X  

现在，您将创建一个名为X的DataFrame，其中包含预测特征。  

由于您只需要原始数据中的一些列，因此您将首先在X中创建一个包含所需列名称的列表。  

您将仅使用列表中的以下列（您可以复制并粘贴整个列表以节省一些输入，但仍需要添加引号）：  

- LotArea
- YearBuilt
- 1stFlrSF
- 2ndFlrSF
- FullBath
- BedroomAbvGr
- TotRmsAbvGrd

创建该功能列表后，使用它创建用于拟合模型的DataFrame  

```python
# Create the list of features below
feature_names = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']

# Select data corresponding to features in feature_names
X = home_data[feature_names]

# Check your answer
step_2.check()
```


审查数据  
在构建模型之前，快速查看X以验证其是否合理   
```python
# Review data
# print description or statistics from X
print(home_data.describe())

# print the top few lines
print(home_data.head())
```

#### 步骤3：指定并拟合模型  

创建一个“DecisionTreeRegressor”并将其保存为iowa_model。确保您已从sklearn完成相关导入以运行此命令。  

然后，使用您在上面保存的“X”和“y”中的数据来拟合您刚才创建的模型。   

```python
from sklearn.tree import DecisionTreeRegressor
#specify the model. 
#For model reproducibility, set a numeric value for random_state when specifying the model
iowa_model = DecisionTreeRegressor(random_state = 1)

# Fit the model
iowa_model.fit(X, y)

# Check your answer
step_3.check()
```  


#### 第四步：做出预测  
使用“X”作为数据，使用模型的“predict”命令进行预测。将结果保存到一个名为“predictions”的变量中。

```python
predictions = iowa_model.predict(X)
print(predictions)

# Check your answer
step_4.check()
```


想想你的结果  
使用“head”方法将前几个预测值与这些房屋的实际房屋价值（以“y”表示）进行比较。有什么奇怪的吗？  
```python
# You can write code in this cell

print(iowa_model.predict(X))

y_head  = home_data['SalePrice'].head()

from sklearn.tree import DecisionTreeRegressor

model1 = DecisionTreeRegressor(random_state = 1)
model1.fit(X.head(), y_head)

print(model1.predict(X))
```  
输出：
```python
[208500. 181500. 223500. ... 266500. 142125. 147500.]
[208500. 181500. 223500. ... 250000. 140000. 140000.]
```  

#### 这里的“模型”到底是什么  
就是决策树，具体的来说：模型是`iowa_model`这个Python对象，它内部存了两样东西：    


|内部存的东西|内容|
|-----------|----|
|结构|一串 if/else 规则（哪个特征、阈值多少、往左还是往右）|
|叶子上的数值|走到这片叶子时，应该输出多少价格|  

在`fit()`之前，这个对象是`空白`的，只有默认参数。`fit()` 之后，树的结构和叶子数值被填满了—— "模型"就是这棵被数据填满的树 。  
  


#### 什么叫"不限深度"、"切到叶子只剩一两个样本"、"过拟合  
刚才说到这个决策树模型实际上是if/else 不断的自动分组实现预测的，这样的分割将数据使得形成了类似于树的结构   

不限深度的意思是 只要当前的数据仍能分割，就会不断的分割下去，直到不能分割  

不能分割的条件就是：
1.叶子里的样本 特征完全相同 ，无论怎么切都分不开  
2.叶子只剩 1 个样本 （sklearn 默认`min_samples_leaf=1` ）  
3.再切也不会让误差下降    


因为叶子最终只剩 1 个样本，而叶子的预测值就等于样本的价格——所以训练集的预测会 100% 等于真实值。  


这就叫`"过拟合"`：模型太复杂（树太深），把训练数据的每一个细节都记了下来，包括偶然的噪声。结果：训练集上完美，新数据上崩盘。  

用学习打比方： 你把练习册的每一道题的答案（甚至连题号、页码）全背了下来 。这本练习册再考一遍，你满分；换一本新练习册，你一道都做不出来——因为你背的是"答案"，不是"解题方法"。

反过来，如果树太浅（比如`max_depth=1` ），它只能问一个问题，什么都学不到，这叫 `欠拟合` 。两个极端都不好，中间才是最佳点  


#### 为什么后面几个预测值不一样？"平均值"是什么意思  

关键在这里： 叶子可以装不止 1 套房。    
 
前面说"切到最后每片叶子只剩 1 个样本"，但有个例外—— 如果两套房在全部 7 个特征上完全相同，树根本没能力区分它们 。  

7 个特征一模一样，树切到这里切不动了，两套房只能挤在同一片叶子里。

那这片叶子的预测值该是多少？ 取叶子内所有样本的平均值

所以你看到`266500 → 250000` 、`142125 → 140000` 这种"对不上"的值，就是 这片叶子装了好几个样本，输出的是它们的平均价 ，不是任何一套房的精确价格。  
 

**记住这条规律：决策树的每个叶子，输出的都是叶子内样本标签的平均值。**  


#### 喂多少数据就只能输出多少种预测值？  

基本对，精确表述是：输出值的种类数 ≤ 叶子数量 ≤ 训练样本数  