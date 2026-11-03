#### 练习 4.1：⽐萨 
想出⾄少三种你喜欢的⽐萨，将其名称存储在⼀个列表中，再使⽤ for 循环将每种⽐萨的名称打印出来。
- 修改这个 for 循环，使其打印包含⽐萨名称的句⼦，⽽不仅仅是⽐萨的名称。对于每种⽐萨都显⽰⼀⾏输出，如下所⽰。  
I like pepperoni pizza. 
- 在程序末尾添加⼀⾏代码（不包含在 for 循环中），指出你有多喜欢⽐萨。输出应包含针对每种⽐萨的消息，还有⼀个总结性的句⼦，如下所⽰。  
I really love pizza!
```python
pizzas = ["p1", "p2", "p3", "p4", "p5"]
for pizza in pizzas:
    print(f"I like {pizza} pizza.")
print("I really love pizza!")
```

#### 练习 4.2：动物
想出⾄少三种有共同特征的动物，将其名称存储在⼀个列表中，再使⽤ for 循环将每种动物的名称打印出来
- 修改这个程序，使其针对每种动物都打印⼀个句⼦，如下所⽰。  
A dog would make a great pet.
- 在程序末尾添加⼀⾏代码，指出这些动物的共同之处，如打印下⾯这样的句⼦。  
Any of these animals would make a great pet!
```python
animals = ['dog', 'cat', 'rabbit']
for animal in animals:
    print(f"A {animal} would make a great pet.")
print("Any of these animals would make a great pet!")
```

#### 练习 4.3：数到 20 
使⽤⼀个 for 循环打印数 1〜20（含）。   
```python
for i in range(1, 21, 1):
    print(i, end = " ")
```

#### 练习 4.4：100 万 
创建⼀个包含数 1〜1 000 000 的列表，再使⽤⼀个for 循环将这些数打印出来。（如果输出的时间太⻓，按 Ctrl + C 停⽌输出，或关闭输出窗⼝。）  
```python
list_num = list(range(1, 1_000_000 + 1, 1))
for num in list_num:
    print(num, end = " ")
```

#### 练习 4.5：100 万求和 
创建⼀个包含数 1〜1 000 000 的列表，再使⽤min() 和 max() 核实该列表确实是从 1 开始、到 1 000 000 结束的。另外，对这个列表调⽤函数 sum()，看看 Python 将 100 万个数相加需要多⻓时间。  
```python
list_num = list(range(1, 1_000_000 + 1, 1))
print(min(list_num))
print(max(list_num))
print(sum(list_num))
```

#### 练习 4.6：奇数 
通过给 range() 函数指定第三个参数来创建⼀个列表，其中包含 1〜20 的奇数；再使⽤⼀个 for 循环将这些数打印出来。
```python
list_num = list(range(1, 21, 2))
for i in list_num:
    print(i, end = " ")
```

#### 练习 4.7：3 的倍数 
创建⼀个列表，其中包含 3〜30 内能被 3 整除的数，再使⽤⼀个 for 循环将这个列表中的数打印出来。
```python
list_num = [num for num in range(3, 31, 1) if num % 3 == 0]
for num in list_num:
    print(num, end = " ")
```

#### 练习 4.8：⽴⽅ 
将同⼀个数乘三次称为⽴⽅。例如，在 Python 中，2 的⽴⽅⽤ 2**3 表⽰。创建⼀个列表，其中包含前 10 个整数（1〜10）的⽴⽅，再使⽤⼀个 for 循环将这些⽴⽅数打印出来。
```python
list_num = [num ** 3 for num in range(1, 11, 1)]
for num in list_num:
    print(num, end = " ")
```

#### 练习 4.9：⽴⽅推导式 
使⽤列表推导式⽣成⼀个列表，其中包含前 10 个整数的⽴⽅。
```python
list_num = [num ** 3 for num in range(1, 11, 1)]
```

#### 练习 4.10：切⽚ 
选择你在本章编写的⼀个程序，在末尾添加⼏⾏代码，以完成如下任务。
- 打印消息“The first three items in the list are:”，再使⽤切⽚来打印列表的前三个元素。
- 打印消息“Three items from the middle of the list are:”，再使⽤切⽚来打印列表中间的三个元素。
-  打印消息“The last three items in the list are:”，再使⽤切⽚来打印列表末尾的三个元素。
```python
list_num = list(range(1, 10, 1))
first_three = list_num[0:3:1]
mid_three = list_num[3:6:1]
last_three = list_num[6:9:1]
print("The first three items in the list are:", end = " ")
for num in first_three:
    print(num, end = " ")
print()
print("Three items from the middle of the list are:", end = " ")
for num in mid_three:
    print(num, end = " ")
print()
print("The last three items in the list are:", end = " ")
for num in last_three:
    print(num, end = " ")
```

#### 练习 4.11：你的⽐萨，我的⽐萨 
在你为练习 4.1 编写的程序中，创建⽐萨列表的副本，并将其赋给变量 friend_pizzas，再完成如下任务。
- 在原来的⽐萨列表中添加⼀种⽐萨。
- 在列表 friend_pizzas 中添加另⼀种⽐萨。
- 核实有两个不同的列表。为此，打印消息“My favorite pizza are:”，再使⽤⼀个 for 循环来打印第⼀个列表；打印消息“My friend's favorite pizzas are:”，再使⽤⼀个 for 循环来打印第⼆个列表。核实新增的⽐萨被添加到了正确的列表中。
```python
pizzas = ["p1", "p2", "p3", "p4", "p5"]
friend_pizzas = pizzas[:]
pizzas.append("add_one")
friend_pizzas.append("add_two")
print("My favorite pizzas are:", end = " ")
for pizza in pizzas:
    print(pizza, end = " ")
print()
print("My friend's favorite pizzas are:", end = " ")
for pizza in friend_pizzas:
    print(pizza, end = " ")
```

#### 练习 4.13：⾃助餐 
有⼀家⾃助式餐馆，只提供 5 种简单的⾷品。请想出 5 种简单的⾷品，并将其存储在⼀个元组中。
- 使⽤⼀个 for 循环将该餐馆提供的 5 种⾷品都打印出来。
- 尝试修改其中的⼀个元素，核实 Python 确实会拒绝你这样做。
- 餐馆调整菜单，替换了两种⾷品。请编写⼀⾏给元组变量赋值的代码，并使⽤⼀个 for 循环将新元组的每个元素都打印出来。
```python
food1, food2, food3, food4, food5 = "noodles", "rice", "fried noodles", "fried rice", "dumplings"
foods = (food1, food2, food3, food4, food5)

for food in foods:
    print(food, end = " ")
# foods[0] = "tangyuan" TypeError: 'tuple' object does not support item assignment

print()
food4 = "tangyuan"
food5 =  "cake"
foods = (food1, food2, food3, food4, food5)
for food in foods:
    print(food, end = " ")
```