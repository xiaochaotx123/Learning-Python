#### 什么是DataFrame？
DataFrame是Pandas中最核心、最常用的数据结构。可以理解为一张二维的、带标签的表格，类似于Excel中的工作表或SQL中的数据库表。

#### Series和DataFrame的关系
- Series是一列数据，好比Excel表格中的某一列
- DataFrame是多列数据的集合，好比Excel中的整张表格
更准确的说，DataFrame可以看作是多个Series的容器——DataFrame中的每一列本质都是一个Series，而且这些Series共享一个索引（行标签）

#### DataFrame的三个核心组成部分
任何一个DataFrame都由以下三部分组成：  

1.数据(Values)：实际的二维数据内容，是一个N行 × M列的矩阵  

2.行索引(index)：标识每一行的标签。默认是从0开始的整数，但完全可以自定义为日期、字符串等标签。这和Series中的index是类似的  

3.列索引(columns)：表示的每一列数据。每一列都有一个列明（比如"姓名"、"年龄"、"工资"等），这也是一种索引

### DateFrame的关键性质
#### 1.异构数据类型
这是DateFrame区别于NumPy二维数组的一个重要特性。在NumPy的ndarray中吗，所有元素必须是同一种数据类型；  
而DataFrame中，不同列可以有不同的数据类型。比如一列存字符串（姓名），一列存整数（年龄），一列存浮点数（工资）

#### 2.大小可变
DataFrame的行和列都是可以动态增删的，你可以随时添加新列、删除列、插入行、删除行

#### 3.支持标签索引和位置索引
和Series一样，DataFrame既可以通过标签来访问数据(.loc())，也可以通过整数位置来访问数据(.iloc())。这为数据选取提供了极大的灵活性

#### 4.自动数据对其
当对两个DataFrame进行运算时，Pandas会自动按照行标签和列标签进行对其。这一点和Series的自动对齐机制一脉相承，只是现在对其的是沿着行和列两个维度同时进行的

#### 5.处理缺失值
DataFrame天然支持缺失值(NaN)，并提供了丰富的方法来处理它们，比如删除、填充等

#### DataFrame的常用场景
- 数据清洗与预处理：筛选、去重、处理缺失值、类型转换
- 数据探索与分析：排序、分组、聚合、描述性统计
- 数据可视化：与Matplotlib、Seaborn等库无缝集成，直接绘图
- 数据导入导出：从CSV、Excel、SQL、JSON等多种格式读取数据并写入

#### 理解DataFrame的维度
- 0维：标量（一个单独的值）
- 1维：Series（一列数据）
- 2维：DataFrame（一张表格）
- 3维及以上：Panel（Pandas中已弃用，现在推荐使用Xarray或Multilndex）
所以DataFrame就是二维的带标签数据结构
