#### 练习 6.1：⼈ 
使⽤⼀个字典来存储⼀个⼈的信息，包括名、姓、年龄和居住的城市。该字典应包含键 first_name、last_name、age 和 city。将存储在该字典中的每项信息都打印出来。
```python
messages = {
    "second_name" : "chao",
    "first_name" : "xiao",
    "age" : 21,
    "live" : "cs",
}
print(messages)
```

#### 练习 6.2：喜欢的数 1 
使⽤⼀个字典来存储⼀些⼈喜欢的数。请想出5 个⼈的名字，并将这些名字⽤作字典中的键。再想出每个⼈喜欢的⼀个数，并将这些数作为值存储在字典中。打印每个⼈的名字和喜欢的数。为了让这个程序更有趣，通过询问朋友确保数据是真实的。
```python
messages = {
    "n1" : 1,
    "n2" : 2,
    "n3" : 3,
    "n4" : 4,
    "n5" : 5,
}
print(messages)
```

#### 练习 6.3：词汇表 1 
Python 字典可⽤于模拟现实⽣活中的字典。为避免混淆，我们将后者称为词汇表。
- 想出你在前⾯学过的 5 个编程术语，将它们⽤作词汇表中的键，并将它们的含义作为值存储在词汇表中。
- 以整洁的⽅式打印每个术语及其含义。为此，既可以先打印术语，在它后⾯加上⼀个冒号，再打印其含义；也可以先在⼀⾏⾥打印术语，再使⽤换⾏符（\n）插⼊⼀个空⾏，然后在下⼀⾏⾥以缩进的⽅式打印其含义。
```python
glossary = {
    "变量": "用于存储数据值的命名内存位置。",
    "函数": "一段可重用的、用于执行特定任务的代码块。",
    "列表": "一种有序且可变的数据集合。",
    "字典": "一种使用键值对（key-value）来存储数据的数据结构。",
    "循环": "用于重复执行一段代码的控制结构。",
}
for key, value in glossary.items():
    print(f"{key}：{value}")

# print(glossary.keys())
# print(glossary.values())
```

#### 练习 6.4：词汇表 2 
现在你知道了如何遍历字典，请整理你为练习 6.3编写的代码，将其中的⼀系列函数调⽤ print() 替换为⼀个遍历字典中键和值的循环。确保该循环正确⽆误后，再在词汇表中添加 5 个Python 术语。当你再次运⾏这个程序时，这些新术语及其含义将⾃动包含在输出中。
```python
glossary = {
    "变量": "用于存储数据值的命名内存位置。",
    "函数": "一段可重用的、用于执行特定任务的代码块。",
    "列表": "一种有序且可变的数据集合。",
    "字典": "一种使用键值对（key-value）来存储数据的数据结构。",
    "循环": "用于重复执行一段代码的控制结构。",
}
new_key = ["类", "对象", "模块", "异常", "元组"]
new_value = [
    "用于创建对象的蓝图或模板，定义了对象的属性和方法。",
    "类的实例，包含了类中定义的属性和方法。",
    "一个包含 Python 代码的文件，可以导入到其他程序中使用。",
    "程序执行过程中发生的错误事件，可以用 try-except 语句来捕获和处理。",
    "一种有序且不可变的数据集合，通常用圆括号表示。"
]
for i in range(0, 5, 1):
    glossary[new_key[i]] = new_value[i]

for key, value in glossary.items():
    print(f"{key}：{value}")

# for key in glossary.keys():
#     print(f"{key}：{glossary[key]}")
```

#### 练习 6.5：河流 
创建⼀个字典，在其中存储三条河流及其流经的国家。例如，⼀个键值对可能是 'nile': 'egypt'。
- 使⽤循环为每条河流打印⼀条消息，如下所⽰。
The Nile runs through Egypt.
- 使⽤循环将该字典中每条河流的名字打印出来。
- 使⽤循环将该字典包含的每个国家的名字打印出来。
```python
rivers = {
    'nile': 'egypt',
    'amazon': 'brazil',
    'yangtze': 'china'
}

for key, value in rivers.items():
    print(f"The {key} runs through {value}.")

for key in rivers.keys():
    print(key, end = " ")
print()
for value in rivers.values():
    print(value, end = " ")
```

#### 练习 6.6：调查 
在 6.3.1 节编写的程序 favorite_languages.py 中执⾏以下操作。
- 创建⼀个应该会接受调查的⼈的名单，其中有些⼈已在字典中，⽽其他⼈不在字典中。
- 遍历这个名单。对于已参与调查的⼈，打印⼀条消息表⽰感谢；对于还未参与调查的⼈，打印⼀条邀请参加调查的消息。
```python
favorite_languages = {
    "jen" : "python",
    "sarah" : "c",
    "edward" : "rust",
    "phil" : "python",
}
peoples = ["jen", "xiaochao", "xiaoyue", "phil"]

for people in peoples:
    if people in favorite_languages.keys():
        print(f"{people}, Thank you for participating in the survey!")
    else:
        print(f"{people}, We sincerely invite you to participate in the survey!")
```

#### 练习 6.7：⼈们 
在为练习 6.1 编写的程序中，再创建两个表⽰⼈的字典，然后将这三个字典都存储在⼀个名为 people 的列表中。遍历这个列表，将其中每个⼈的所有信息都打印出来。
```python
messages1 = {
    "second_name" : "chao",
    "first_name" : "xiao",
    "age" : 21,
    "live" : "cs",
}
messages2 = {
    "second_name": "chao",
    "first_name": "yue",
    "age": 20,
    "live": "cs",
}
messages3 = {
    "second_name": "chao",
    "first_name": "ling",
    "age": 21,
    "live": "cs",
}

people = [messages1, messages2, messages3]
for message in people:
    print(message)
```

#### 练习 6.8：宠物 
创建多个表⽰宠物的字典，每个字典都包含宠物的类型及其主⼈的名字。将这些字典存储在⼀个名为 pets 的列表中，再遍历该列表，并将有关每个宠物的所有信息打印出来。
```python
pet_1 = {
    "type" : "dog",
    "owner" : "Alice",
}
pet_2 = {
    "type" : "cat",
    "owner" : "Bob",
}
pet_3 = {
    "type" : "parrot",
    "owner" : "Charlie",
}
pets = [pet_1, pet_2, pet_3]
for pet in pets:
    print(pet)
```

#### 练习 6.9：喜欢的地⽅ 
创建⼀个名为 favorite_places 的字典。在这个字典中，将三个⼈的名字⽤作键，并存储每个⼈喜欢的 1〜3 个地⽅。为让这个练习更有趣些，让⼀些朋友说出他们喜欢的⼏个地⽅。遍历这个字典，并将其中每个⼈的名字及其喜欢的地⽅打印出来。
```python
favorite_places = {
    "xiaochao" : ["chongqing", "beijing", "shenzheng", "hangzhou"],
    "xiaoyue" : ["chongqing", "shangcha"],
    "xiaoling" : ["shanghai"]
}
for key, value in favorite_places.items():
    print(f"{key}'s favorite palaces：", end = " ")
    for place in value:
        print(place, end = " ")
    print()
```

#### 练习 6.10：喜欢的数 2 
修改为练习 6.2 编写的程序，让每个⼈都可以有多个喜欢的数字，然后将每个⼈的名字及其喜欢的数打印出来。
```python
messages = {
    "n1" : [1, 2, 3],
    "n2" : [3, 4, 5],
    "n3" : [7],
    "n4" : [9, 91],
    "n5" : [100],
}
for key, value in messages.items():
    print(f"{key}'s favorite num: ", end = " ")
    for num in value:
        print(num, end = " ")
    print()
```

#### 练习 6.11：城市 
创建⼀个名为 cities 的字典，将三个城市名⽤作键。对于每座城市，都创建⼀个字典，并在其中包含该城市所属的国家、⼈⼝约数以及⼀个有关该城市的事实。表⽰每座城市的字典都应包含 country、population 和 fact 等键。将每座城市的名字以及
相关信息都打印出来。
```python
cities = {
    "Beijing" : {
        "country" : "China",
        "population" : "21 million",
        "fact" : "It has a history of over 3,000 years.",
    },
    "New York" : {
        "country" : "USA",
        "population" : "8.5 million",
        "fact" : "It is known as \"The Big Apple\".",
    },
    "Tokyo" : {
        "country" : "Japan",
        "population" : "14 million",
        "fact" : "It is the most populous metropolitan area in the world.",
    },
}

for city_name, city_info in cities.items():
    print(f"\n城市名称：{city_name}")
    print(f"  所属国家：{city_info["country"]}")
    print(f"  人口约数：{city_info["population"]}")
    print(f"  相关事实：{city_info["fact"]}")
```