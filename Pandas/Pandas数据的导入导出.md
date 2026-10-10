```python
import pandas as pd
```

#### csv文件的导入 pd.read_csv("需要导入的文件的地址")
```python
df = pd.read_csv("Pandas_Study_Data/Data1.csv")
print(type(df)) # 输出：<class 'pandas.DataFrame'>
print(df)
# 输出：
#      姓名 性别  年龄   身高     爱好      居住地           电话
# 0    张伟  男  28  175  篮球、跑步   北京市朝阳区  13000000001
# 1    王芳  女  24  163  阅读、瑜伽  上海市浦东新区  13000000002
# 2    李娜  女  31  168  旅行、摄影   广州市天河区  13000000003
# 3    刘洋  男  35  180  游泳、音乐   深圳市南山区  13000000004
# 4    陈静  女  29  160  烘焙、电影   杭州市西湖区  13000000005
# ..   .. ..  ..  ...    ...      ...          ...
# 125  蓝静  女  28  166  摄影、舞蹈   衡阳市蒸湘区  13000000126
# 126  佟浩  男  31  177  篮球、游戏   邵阳市双清区  13000000127
# 127  刁丽  女  27  162  旅行、阅读   岳阳市云溪区  13000000128
# 128  鄢磊  男  36  181  游泳、音乐   郴州市苏仙区  13000000129
# 129  荣雪  女  24  159  瑜伽、电影   永州市零陵区  13000000130
# 
# [130 rows x 7 columns]
```


#### csv文件的导出 文件名称.to_csv("需要导出到的文件地址")
```python
df["平均身高"] = df["身高"].mean()
df["男性平均身高"] = df[df["性别"] == "男"]["身高"].mean()
df["女性平均身高"] = df[df["性别"] == "女"]["身高"].mean()

# csv文件的的导出
df.to_csv("Pandas_Study_Data/new.csv")
```


#### json文件的导入
```python
df_json = pd.read_json("Pandas_Study_Data/Data2.json")
print(df_json)
# 输出：
#     姓名 性别  年龄   身高     爱好      居住地           电话
# 0   张伟  男  28  175  篮球、跑步   北京市朝阳区  13000000001
# 1   王芳  女  24  163  阅读、瑜伽  上海市浦东新区  13000000002
# 2   李娜  女  31  168  旅行、摄影   广州市天河区  13000000003
# 3   刘洋  男  35  180  游泳、音乐   深圳市南山区  13000000004
# 4   陈静  女  29  160  烘焙、电影   杭州市西湖区  13000000005
# 5   杨强  男  42  178  钓鱼、象棋   成都市武侯区  13000000006
# 6   赵敏  女  27  165  绘画、跑步   武汉市洪山区  13000000007
# 7   黄磊  男  33  182  健身、吉他   南京市鼓楼区  13000000008
# 8   周婷  女  26  158  舞蹈、阅读   西安市雁塔区  13000000009
# 9   吴刚  男  38  176  足球、旅行   重庆市渝北区  13000000010
# 10  徐丽  女  30  162  唱歌、烹饪   天津市和平区  13000000011
# 11  孙浩  男  25  174  编程、骑行  苏州市工业园区  13000000012
# 12  马超  男  36  181  篮球、游泳   长沙市岳麓区  13000000013
```
如果是复杂的json文件格式（比如爬虫获取的json文件格式中只有一个columns是"users"）
```python
df_complex_json = pd.read_json("Pandas_Study_Data/Complex_Data2.json")
# df_complex_json # 这样是有问题的，虽然是DataFrame，但是这个格式不对，columns只有一个users，然后值都是字典
# print(type(df_complex_json)) # <class 'pandas.DataFrame'>
print(df_complex_json)
# 输出：
#                                                users
# 0  {'id': 1, 'name': '张三', 'age': 28, 'email': 'z...
# 1  {'id': 2, 'name': '李四', 'age': 35, 'email': 'l...
# 2  {'id': 3, 'name': '王五', 'age': 24, 'email': 'w...
# 3  {'id': 4, 'name': '赵六', 'age': 31, 'email': 'z...
# 4  {'id': 5, 'name': '孙七', 'age': 45, 'email': 's...
# 5  {'id': 6, 'name': '周八', 'age': 22, 'email': 'z...
# 6  {'id': 7, 'name': '吴九', 'age': 29, 'email': 'w...
# 7  {'id': 8, 'name': '郑十', 'age': 38, 'email': 'z...
```
解决的办法是使用json库中的load函数将字典取出来，然后转化为DataFrame即可
```python
import json
with open("Pandas_Study_Data/Complex_Data2.json", encoding = "utf-8") as f:
    complex_json = json.load(f)
print(complex_json)

dff = pd.DataFrame(complex_json["users"])
print(dff)
# 输出：
#    id name  age                 email  is_active   join_date
# 0   1   张三   28  zhangsan@example.com       True  2022-03-15
# 1   2   李四   35      lisi@example.com      False  2021-11-02
# 2   3   王五   24    wangwu@example.com       True  2023-05-20
# 3   4   赵六   31   zhaoliu@example.com       True  2020-08-10
# 4   5   孙七   45     sunqi@example.com      False  2019-02-28
# 5   6   周八   22    zhouba@example.com       True  2024-01-05
# 6   7   吴九   29     wujiu@example.com      False  2022-07-19
# 7   8   郑十   38  zhengshi@example.com       True  2021-04-03
```

