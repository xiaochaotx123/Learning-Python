#### 练习 5.3：外星⼈颜⾊ 1 
假设玩家在游戏中消灭了⼀个外星⼈，请创建⼀个名为 alien_color 的变量，并将其赋值为'green'、'yellow' 或 'red'。
- 编写⼀条 if 语句，测试外星⼈是否是绿⾊的。如果是，就打印⼀条消息，指出玩家获得了 5 分。
- 编写这个程序的两个版本，上述条件测试在其中的⼀个版本中通过，在另⼀个版本中未通过（未通过条件测试时没有输出）。
```python
alien_color = "green"
if alien_color == "green":
    print("scored 5 points!")

alien_color = "red"
if alien_color == "green":
    print("scored 5 points!")
```

#### 练习 5.4：外星⼈颜⾊ 2 
像练习 5.3 那样设置外星⼈的颜⾊，并编写⼀个 if-else 结构。
- 如果外星⼈是绿⾊的，就打印⼀条消息，指出玩家因消灭该外星⼈获得了 5 分。
- 如果外星⼈不是绿⾊的，就打印⼀条消息，指出玩家获得了 10 分。
- 编写这个程序的两个版本，在⼀个版本中将执⾏ if 代码块，在另⼀个版本中将执⾏ else 代码块。 
```python
alien_color = "green"
if alien_color == "green":
    print("scored 5 points!")
else:
    print("scored 10 points!")

alien_color = "red"
if alien_color == "green":
    print("scored 5 points!")
else:
    print("scored 10 points!")
```

#### 练习 5.5：外星⼈颜⾊ 3 将练习 5.4 中的 if-else 结构改为 if-elif-else 结构。
- 如果外星⼈是绿⾊的，就打印⼀条消息，指出玩家获得了 5 分。
- 如果外星⼈是⻩⾊的，就打印⼀条消息，指出玩家获得了 10 分。
- 如果外星⼈是红⾊的，就打印⼀条消息，指出玩家获得了 15 分。
- 编写这个程序的三个版本，分别在外星⼈为绿⾊、⻩⾊和红⾊时打印⼀条消息。
```python
alien_color = "green"
if alien_color == "green":
    print("scored 5 points!")
elif alien_color == "yellow":
    print("scored 10 points!")
elif alien_color == "red":
    print("scored 15 points!")

alien_color = "yellow"
if alien_color == "green":
    print("scored 5 points!")
elif alien_color == "yellow":
    print("scored 10 points!")
elif alien_color == "red":
    print("scored 15 points!")

alien_color = "red"
if alien_color == "green":
    print("scored 5 points!")
elif alien_color == "yellow":
    print("scored 10 points!")
elif alien_color == "red":
    print("scored 15 points!")
```

#### 练习 5.6：⼈⽣的不同阶段 设置变量 age 的值，再编写⼀个if-elif-else 结构，根据 age 的值判断这个⼈处于⼈⽣的哪个阶段。
- 如果年龄⼩于 2 岁，就打印⼀条消息，指出这个⼈是婴⼉。
- 如果年龄为 2（含）〜4 岁，就打印⼀条消息，指出这个⼈是幼⼉。
- 如果年龄为 4（含）〜13 岁，就打印⼀条消息，指出这个⼈是⼉童。
- 如果年龄为 13（含）〜18 岁，就打印⼀条消息，指出这个⼈是少年。
- 如果年龄为 18（含）〜65 岁，就打印⼀条消息，指出这个⼈是中⻘年⼈。
- 如果年龄达到 65 岁，就打印⼀条消息，指出这个⼈是⽼年⼈。
```python
age = 21
if age < 2:
    print("You are a baby")
elif (2 <= age) and (age < 4):
    print("You are a toddler")
elif (4 <= age) and (age < 13):
    print("You are a child")
elif (13 <= age) and (age < 18):
    print("You are a teenager")
elif (18 <= age) and (age < 65):
    print("You are an adult")
elif 65 <= age:
    print("You are a senior")
```

#### 练习 5.7：喜欢的⽔果 
创建⼀个列表，其中包含你喜欢的⽔果，再编写⼀系列独⽴的 if 语句，检查列表中是否包含特定的⽔果。
- 将该列表命名为 favorite_fruits，并让其包含三种⽔果。
- 编写 5 条 if 语句，每条都检查某种⽔果是否在列表中。如果是，就打印⼀条像下⾯这样的消息。  
You really like bananas!  

```python
favorite_fruits = ["apple", "banana", "orange"]
if "apple" in favorite_fruits:
    print("You really like apple!")
if "Grape" in favorite_fruits:
    print("You really like Grape!")
if "banana" in favorite_fruits:
    print("You really like banana!")
if "Strawberry" in favorite_fruits:
    print("You really like Strawberry!")
if "orange" in favorite_fruits:
    print("You really like orange!")
```


#### 练习 5.8：以特殊⽅式跟管理员打招呼 
创建⼀个⾄少包含 5 个⽤户名的列表，并且其中⼀个⽤户名为 'admin'。想象你要编写代码，在每个⽤户登录⽹站后都打印⼀条问候消息。遍历⽤户名列表，向每个⽤户打印⼀条问候消息。
- 如果⽤户名为 'admin'，就打印⼀条特殊的问候消息，如下所⽰。  
Hello admin, would you like to see a status report?
- 否则，打印⼀条普通的问候消息，如下所⽰。
Hello Jaden, thank you for logging in again.  
```python
user_name = ["n1", "n2", "n3", "admin", "n5"]
for name in user_name:
    if name == "admin":
        print("Hello admin, would you like to see a status report?")
    else:
        print(f"Hello {name}, thank you for logging in again.")
```

#### 练习 5.9：处理没有⽤户的情形 
在为练习 5.8 编写的程序中，添加⼀条 if 语句，检查⽤户名列表是否为空。
- 如果为空，就打印如下消息。  
We need to find some users!
- 删除列表中的所有⽤户名，确认将打印正确的消息。
```python
user_name = ["n1", "n2", "n3", "admin", "n5"]

if not user_name:
    print("We need to find some users!")
else:
    for name in user_name:
        if name == "admin":
            print("Hello admin, would you like to see a status report?")
        else:
            print(f"Hello {name}, thank you for logging in again.")

user_name.clear()
if not user_name:
    print("We need to find some users!")
```

#### 练习 5.10：检查⽤户名 按照下⾯的说明编写⼀个程序，模拟⽹站如何确保每个⽤户的⽤户名都独⼀⽆⼆。
- 创建⼀个⾄少包含 5 个⽤户名的列表，并将其命名为current_users。
- 再创建⼀个包含 5 个⽤户名的列表，将其命名为 new_users，并确保其中有⼀两个⽤户名也在列表 current_users 中。
- 遍历列表 new_users，检查其中的每个⽤户名是否已被使⽤。如果是，就打印⼀条消息，指出需要输⼊别的⽤户名；否则，打印⼀条消息，指出这个⽤户名未被使⽤。
- 确保⽐较时不区分⼤⼩写。换句话说，如果⽤户名 'John' 已被使⽤，应拒绝⽤户名 'JOHN'。（为此，需要创建列表current_users 的副本，其中包含当前所有⽤户名的全⼩写版本。）
```python
current_users = ["xiaoChao", "xiAoYue", "xiaoXING", "xiaochen", "xIAOling"]
new_users = ["xiaochao", "xiaoyue", "xiaOXiao", "xiaoMing", "Xiaotian"]

current_users_lower = [name.lower() for name in current_users]
# print(current_users_lower)

for name in new_users:
    if name.lower() in current_users_lower:
        print("Need to input another user name")
    else:
        print(f"{name} has not been used")
```

#### 练习 5.11：序数 
序数表⽰顺序位置，如 1st 和 2nd。序数⼤多以 th 结尾，只有 1st、2nd、3rd 例外
- 在⼀个列表中存储数字 1〜9。
- 遍历这个列表。
- 在循环中使⽤⼀个 if-elif-else 结构，打印每个数字对应的序数。输出内容应为 "1st 2nd 3rd 4th 5th 6th 7th 8th9th"，每个序数都独占⼀⾏。
```python
nums = list(range(1, 10, 1))
for num in nums:
    if num == 1:
        print("1st")
    elif num == 2:
        print("2nd")
    elif num == 3:
        print("3rd")
    elif num >= 4:
        print(f"{num}th")
```