### 题目一：销售数据分析
场景：某公司销售数据如下，请完成以下任务：
- 计算每种产品的总销售额（销售额 = 单价 × 数量）
- 找出销售额最高的产品
- 按销售额从高到低排序，并输出所有产品信息
```python
data = {
    "产品名称" : ["A", "B", "C", "D"],
    "单价" : [100, 150, 200, 120],
    "销量" : [50, 30, 20, 40],
}
```

```python
import pandas as pd
```
```python
sell = pd.DataFrame(data)
#   产品名称   单价  销量
# 0    A  100  50
# 1    B  150  30
# 2    C  200  20
# 3    D  120  40
```


#### 计算每种产品的总销售额（销售额 = 单价 × 数量）
```python
sell["销售额"] = sell["单价"] * sell["销量"]
print(sell)
# 输出：
#   产品名称   单价  销量   销售额
# 0    A  100  50  5000
# 1    B  150  30  4500
# 2    C  200  20  4000
# 3    D  120  40  4800
```

#### 找出销售额最高的产品
```python
print(sell.nlargest(1, ["销售额"]))
```

#### 按销售额从高到低排序，并输出所有产品信息
```python
sorted_sell = sell.sort_values(by = ["销售额"], ascending = [False])
print(sorted_sell)
# 输出：
#   产品名称   单价  销量   销售额
# 0    A  100  50  5000
# 3    D  120  40  4800
# 1    B  150  30  4500
# 2    C  200  20  4000
```

### 题目二：电商用户行为分析
场景：某电商平台用户行为数据如下，请完成以下任务：
- 计算每位用户的总消费金额（消费金额 = 商品单价 × 购买数量）
- 找出消费金额最高的用户，并输出其全部信息
- 计算所有用户的平均消费金额（保留2位小数）
- 统计电子产品的总购买数量
```python
data = {
    "用户ID" : [101, 102, 103, 104, 105],
    "用户名" : ["Alice", "Bob", "Charlie", "David", "Eve"],
    "商品类别" : ["电子产品", "服饰", "电子产品", "家具", "服饰"],
    "商品单价" : [1200, 300, 800, 150, 200],
    "购买数量" : [1, 3, 2, 5, 4],
}
```

```python
import pandas as pd
```
```python
behavior_data = pd.DataFrame(data)
print(behavior_data)
# 输出：
#    用户ID      用户名  商品类别  商品单价  购买数量
# 0   101    Alice  电子产品  1200     1
# 1   102      Bob    服饰   300     3
# 2   103  Charlie  电子产品   800     2
# 3   104    David    家具   150     5
# 4   105      Eve    服饰   200     4
```

#### 计算每位用户的总消费金额（消费金额 = 商品单价 × 购买数量）
```python
behavior_data["总消费金额"] = behavior_data["商品单价"] * behavior_data["购买数量"]
print(behavior_data)
# 输出：
#    用户ID      用户名  商品类别  商品单价  购买数量  总消费金额
# 0   101    Alice  电子产品  1200     1   1200
# 1   102      Bob    服饰   300     3    900
# 2   103  Charlie  电子产品   800     2   1600
# 3   104    David    家具   150     5    750
# 4   105      Eve    服饰   200     4    800
```

#### 找出消费金额最高的用户，并输出其全部信息
```python
print(behavior_data.nlargest(1, ["总消费金额"]))
# 输出：
#    用户ID      用户名  商品类别  商品单价  购买数量  总消费金额
# 2   103  Charlie  电子产品   800     2   1600
```

#### 计算所有用户的平均消费金额（保留2位小数）
```python
average_money = round(behavior_data["总消费金额"].mean(), 2)
print(average_money)
# round(behavior_data["总消费金额"].sum(axis = 0) / len(behavior_data), 2) 也是可以的
```

#### 统计电子产品的总购买数量
```python
# 1. 首先筛选出来商品类别是电子产品的
# print(behavior_data[behavior_data["商品类别"] == "电子产品"])
# 输出：
#    用户ID      用户名  商品类别  商品单价  购买数量  总消费金额
# 0   101    Alice  电子产品  1200     1   1200
# 2   103  Charlie  电子产品   800     2   1600

# 2. 然后就可以直接计算了
print(behavior_data[behavior_data["商品类别"] == "电子产品"]["购买数量"].sum(axis = 0))
```


