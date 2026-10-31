#### 练习 7.1：汽⻋租赁 
编写⼀个程序，询问⽤户要租什么样的汽⻋，并打印⼀条消息，如下所⽰。  
Let me see if I can find you a Subaru.
```python
car = input("What kind of car do you want to rent ?")
print(f"Let me see if I can find you a {car}.")
```

#### 练习 7.2：餐馆订位 
编写⼀个程序，询问⽤户有多少⼈⽤餐。如果超过 8 个⼈，就打印⼀条消息，指出没有空桌；否则指出有空桌。
```python
people = input("May I ask how many people are dining in total ? ")
people = int(people)
if people > 8:
    print("I'm very sorry, there are currently not so many locations available")
else:
    print("Okay, we have enough space now")
```

#### 练习 7.3：10 的整数倍 
让⽤户输⼊⼀个数，并指出这个数是否是 10 的整数倍。
```python
num = input("Please enter an integer：")
num = int(num)
if num % 10 == 0:
    print(f"{num} is a multiple of 10")
else:
    print(f"{num} is not a multiple of 10")
```

#### 练习 7.4：⽐萨配料 
编写⼀个循环，提⽰⽤户输⼊⼀系列⽐萨配料，并在⽤户输⼊ 'quit' 时结束循环。每当⽤户输⼊⼀种配料后，都打印⼀条消息，指出要在⽐萨中添加这种配料。
```python
while True:
    ingredient = input("What ingredients would you like to add to the pizza：")
    if ingredient == "quit":
        break
    else:
        print(f"I will add {ingredient} to the pizza")
```

#### 练习 7.5：电影票 
有家电影院根据观众的年龄收取不同的票价：不到3 岁的观众免费；3（含）〜12 岁的观众收费 10 美元；年满 12 岁的观众收费 15 美元。请编写⼀个循环，在其中询问⽤户的年龄，并指出其票价。
```python
while True:
    age = input("Please enter your age：")
    age = int(age)
    if age < 3:
        print("it is free")
    elif age < 12:
        print("Charge $10")
    else:
        print("Charge $15")
```

#### 练习 7.6：三种出路 
以不同的⽅式完成练习 7.4 或练习 7.5，在程序中采取如下做法。
- 在 while 循环中使⽤条件测试来结束循环。
- 使⽤变量 active 来控制循环结束的时机。
- 使⽤ break 语句在⽤户输⼊ 'quit' 时退出循环。
```python
# 方式一
ingredient = ""
while ingredient != "quit":
    ingredient = input("What ingredients would you like to add to the pizza：")
    if ingredient != "quit":
        print(f"I will add {ingredient} to the pizza")

# 方式二
active = True
while active:
    ingredient = input("What ingredients would you like to add to the pizza：")
    if ingredient == "quit":
        active = False
    else:
        print(f"I will add {ingredient} to the pizza")

# 方式三
while True:
    ingredient = input("What ingredients would you like to add to the pizza：")
    if ingredient == "quit":
        break
    else:
        print(f"I will add {ingredient} to the pizza")
```


#### 练习 7.8：熟⾷店 
创建⼀个名为 sandwich_orders 的列表，其中包含各种三明治的名字，再创建⼀个名为 finished_sandwiches 的空列表。遍历列表 sandwich_orders，对于其中的每种三明治，都打印⼀条消息，如“I made your tuna sandwich.”，并将其移到列表finished_sandwiches 中。当所有三明治都制作好后，打印⼀条消息，将这些三明治列出来。
```python
sandwich_orders = ["Club Sandwich", "BLT Sandwich", "Tuna Sandwich", "Egg Salad Sandwich", "Grilled Cheese Sandwich"]
finished_sandwiches = []
for sandwich in sandwich_orders:
    print(f"I made your {sandwich}.")
    finished_sandwiches.append(sandwich)

sandwich_orders.clear()
print("All the sandwiches are ready")
for sandwich in finished_sandwiches:
    print(sandwich, end = " ")

# if sandwich_orders == finished_sandwiches:
#     print("YES")
```

#### 练习 7.9：五⾹烟熏⽜⾁卖完了 
使⽤为练习 7.8 创建的列表sandwich_orders，并确保 'pastrami' 在其中⾄少出现了三次。在程序开头附近添加这样的代码：先打印⼀条消息，指出熟⾷店的五⾹烟熏⽜⾁（pastrami）卖完了；再使⽤⼀个 while 循环将列表 sandwich_orders 中的 'pastrami' 都删除。确认最终的列表 finished_sandwiches 中未包含 'pastrami'。
```python
sandwich_orders = ["Club Sandwich", "BLT Sandwich", "Tuna Sandwich", "Egg Salad Sandwich", "Grilled Cheese Sandwich"]
sandwich_orders.append("pastrami Sandwich")
sandwich_orders.append("pastrami Sandwich")
sandwich_orders.append("pastrami Sandwich")

if "pastrami Sandwich" in sandwich_orders:
    print(f"Sorry, pastrami Sandwich is already sold out")

while "pastrami Sandwich" in sandwich_orders:
    sandwich_orders.remove("pastrami Sandwich")

if "pastrami Sandwich" in sandwich_orders:
    print("error!")
```

#### 练习 7.10：梦想中的度假胜地 
编写⼀个程序，调查⽤户梦想中的度假胜地。使⽤类似于“If you could visit one place in the world, where would you go?”的提⽰，并编写⼀个打印调查结果的代码块。
```python
responses = {}

polling_active = True

while polling_active:
    name = input("\nWhat is your name：")
    place = input("If you could visit one place in the world, where would you go：")

    responses[name] = place

    repeat = input("Would you like to let another person respond? (yes/ no)")
    if repeat == "no":
        polling_active = False

print("\n--- Poll Results ---")
for name, place in responses.items():
    print(f"{name.title()} would like to visit {place.title()}")
```