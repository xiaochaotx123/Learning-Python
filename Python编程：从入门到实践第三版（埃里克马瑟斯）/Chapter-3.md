#### 练习 3.1：姓名 
将⼀些朋友的姓名存储在⼀个列表中，并将其命名为
names。依次访问该列表的每个元素，从⽽将每个朋友的姓名都打印
出来。
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
print(friends_name)
```

#### 练习 3.2：问候语 继续使⽤练习 
3.1 中的列表，但不打印每个朋友的
姓名，⽽是为每⼈打印⼀条消息。每条消息都包含相同的问候语，但
抬头为相应朋友的姓名。
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"Good Morning! {name.title()}")
```  

#### 练习 3.3：⾃⼰的列表   
想想你喜欢的通勤⽅式，如骑摩托⻋或开汽
⻋，并创建⼀个包含多种通勤⽅式的列表。根据该列表打印⼀系列有
关这些通勤⽅式的陈述，如下所⽰。    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
I would like to own a Honda motorcycle.
```python
transportation_name = ["airplane", "train", "car", "bicycle", "motorcycle", "walk"]
for name in transportation_name:
    print(f"I would like to own a {name}.")
```



#### 练习 3.4：嘉宾名单  
 如果你可以邀请任何⼈⼀起共进晚餐（⽆论是在
世的还是故去的），你会邀请哪些⼈？请创建⼀个列表，其中包含⾄
少三个你想邀请的⼈，然后使⽤这个列表打印消息，邀请这些⼈都来
与你共进晚餐  
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")
``` 



#### 练习 3.5：修改嘉宾名单   
你刚得知有位嘉宾⽆法赴约，因此需要另外邀请⼀位嘉宾。  
- 以完成练习 3.4 时编写的程序为基础，在程序末尾添加函数调⽤print()，指出哪位嘉宾⽆法赴约
- 修改嘉宾名单，将⽆法赴约的嘉宾的姓名替换为新邀请的嘉宾的
姓名。 
- 再次打印⼀系列消息，向名单中的每位嘉宾发出邀请。  
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

print("xiaochao has no time to have dinner with me")
friends_name.remove("xiaochao")
friends_name.append("xiaochao_brother")

for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")
```

#### 练习 3.6：添加嘉宾   
你刚找到了⼀张更⼤的餐桌，可容纳更多的嘉宾就座。请想想你还想邀请哪三位嘉宾。  
以完成练习 3.4 或练习 3.5 时编写的程序为基础，在程序末尾添加函数
调⽤ print()，指出你找到了⼀张更⼤的餐桌。  
- 使⽤ insert() 将⼀位新嘉宾添加到名单开头。
- 使⽤ insert() 将另⼀位新嘉宾添加到名单中间。
- 使⽤ append() 将最后⼀位新嘉宾添加到名单末尾。
- 打印⼀系列消息，向名单中的每位嘉宾发出邀请。

```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

print("Good news! I found a bigger table, so I can invite three more people.")

friends_name.insert(0, "friend_one")
friends_name.insert(3, "friend_two")
friends_name.append("friend_three")

for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")
```

#### 练习 3.7：缩短名单   
你刚得知新购买的餐桌⽆法及时送达，因此只能邀请两位嘉宾。
- 以完成练习 3.6 时编写的程序为基础，在程序末尾添加⼀⾏代码，打印⼀条你只能邀请两位嘉宾共进晚餐的消息。 
- 使⽤ pop() 不断地删除名单中的嘉宾，直到只有两位嘉宾为⽌。每次从名单中弹出⼀位嘉宾时，都打印⼀条消息，让该嘉宾知道你很抱歉，⽆法邀请他来共进晚餐。
- 对于余下两位嘉宾中的每⼀位，都打印⼀条消息，指出他依然在受邀之列。
- 使⽤ del 将最后两位嘉宾从名单中删除，让名单变成空的。打印该名单，核实名单在程序结束时确实是空的。  
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

friends_name.insert(0, "friend_one")
friends_name.insert(3, "friend_two")
friends_name.append("friend_three")

for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

print("I'm sorry, due to some reasons, I can only invite two of you to have dinner with me.")

while(len(friends_name) > 2) :
    name = friends_name.pop()
    print(f"Dear {name.title()}, I'm sorry, due to some reasons, I can't invite you this time, but I will definitely invite you next time")

for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

del friends_name[0]
del friends_name[0]
print(friends_name, len(friends_name))
```

#### 练习 3.8：放眼世界   
想出⾄少 5 个你想去旅游的地⽅。
- 将这些地⽅存储在⼀个列表中，并确保其中的元素不是按字⺟顺序排列的。
- 按原始排列顺序打印该列表。不要考虑输出是否整洁，只管打印原始 Python 列表就好。
- 使⽤ sorted() 按字⺟顺序打印这个列表，不要修改它。
- 再次打印该列表，核实排列顺序未变。
- 使⽤ sorted() 按与字⺟顺序相反的顺序打印这个列表，不要修改它。
- 再次打印该列表，核实排列顺序未变。
- 使⽤ reverse() 修改列表元素的排列顺序。打印该列表，核实排列顺序确实变了。
- 使⽤ reverse() 再次修改列表元素的排列顺序。打印该列表，核实已恢复到原来的排列顺序。
- 使⽤ sort() 修改该列表，使其元素按字⺟顺序排列。打印该列表，核实排列顺序确实变了。
- 使⽤ sort() 修改该列表，使其元素按与字⺟顺序相反的顺序排列。打印该列表，核实排列顺序确实变了。
```python
places_name = ["chengdu", "wuhan", "chongqing", "xiamen", "xian", "beijing", "shanghai", "aomen"]
print(places_name)
print(sorted(places_name))
print(places_name)
print(sorted(places_name, reverse = True))
print(places_name)
places_name.reverse()
print(places_name)
places_name.reverse()
print(places_name)
places_name.sort()
print(places_name)
places_name.sort(reverse = True)
print(places_name)
```

#### 练习 3.9：晚餐嘉宾  
 选择你为完成练习 3.4〜练习 3.7 ⽽编写的⼀个程序，在其中使⽤ len() 打印⼀条消息，指出你邀请了多少位嘉宾来共进晚餐。
```python
friends_name = ["xiaochao", "xiaoyue", "xiaoke", "xiaosheng", "xiaoxing"]
for name in friends_name:
    print(f"{name.title()}, would you like to have dinner with me?")

print(f"I am inviting {len(friends_name)} guests to dinner.")
```