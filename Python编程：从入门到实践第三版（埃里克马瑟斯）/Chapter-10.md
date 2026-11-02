#### 练习 10.1：Python 学习笔记 
在⽂本编辑器中新建⼀个⽂件，写⼏句话来总结⼀下你⾄此学到的 Python 知识，其中每⼀⾏都以“In Python you can”打头。将这个⽂件命名为 learning_python.txt，并存储到为完成本章练习⽽编写的程序所在的⽬录中。编写⼀个程序，读取这个⽂件，并将你所写的内容打印两次：第⼀次打印时读取整个⽂件；第⼆次打印时先将所有⾏都存储在⼀个列表中，再遍历列表中的各⾏。
```python
# learning_python.txt
In Python you can use list.
In Python you can use functions.
In Python you can be enjoyful.
```
```python
from pathlib import Path

path = Path("learning_python.txt")
message = path.read_text(encoding = "utf-8")

print(message)

message_list = message.splitlines()
for mes in message_list:
    print(mes)
```


#### 练习 10.2：C 语⾔学习笔记 
可使⽤ replace() ⽅法将字符串中的特定单词替换为另⼀个单词。下⾯是⼀个简单的⽰例，演⽰了如何将句⼦中的 'dog' 替换为 'cat'：  
```python
>>> message = "I really like dogs."  
>>> message.replace('dog', 'cat')  
'I really like cats.' 
```
读取你刚创建的⽂件 learning_python.txt 中的每⼀⾏，将其中的 Python 都替换为另⼀门语⾔的名称，如 C。将修改后的各⾏都打印到屏幕上。  
```python
# learning_python.txt
In Python you can use list.
In Python you can use functions.
In Python you can be enjoyful.
```
```python
from pathlib import Path

path = Path("learning_python.txt")
message = path.read_text(encoding = "utf-8")

message = message.replace("Python", "C ++")
print(message)

message_list = message.splitlines()
for mes in message_list:
    print(mes)
```


#### 练习 10.3：简化代码 
本节前⾯的程序 file_reader.py 中使⽤了⼀个临时变量 lines，来说明 splitlines() 的⼯作原理。可省略这个临时变量，直接遍历 splitlines() 返回的列表：   
for line in contents.splitlines():  
对于本节的每个程序，都删除其中的临时变量，让代码更简洁。  
```python
# learning_python.txt
In Python you can use list.
In Python you can use functions.
In Python you can be enjoyful.
```
```python
from pathlib import Path

message = Path("learning_python.txt").read_text()
message = message.replace("Python", "C ++")

print(message)

for mes in message.splitlines():
    print(mes)
```


#### 练习 10.4：访客 
编写⼀个程序，提⽰⽤户输⼊其名字。在⽤户做出响应后，将其名字写⼊⽂件 guest.txt。
```python
from pathlib import Path

name = input("please enter a name：")
Path("guest.txt").write_text(name)
```
```python
# guest.txt
xiaochao
```


#### 练习 10.5：访客簿 
编写⼀个 while 循环，提⽰⽤户输⼊其名字。收集⽤户输⼊的所有名字，将其写⼊ guest_book.txt，并确保这个⽂件中的每条记录都独占⼀⾏。
```python
from pathlib import Path

guest_book_name = ""

print("if you want to exit, please enter \"quti\"")
while True:
    name = input("please enter a name：")
    if name == "quit":
        break
    guest_book_name += name + "\n"

Path("guest_book.text").write_text(guest_book_name)
```
```python
guest_book.txt
xiaochao
xiaoyue
xiaoling
xiaoxing
xiaoke

```


#### 练习 10.6：加法运算 
在提⽰⽤户提供数值输⼊时，常出现的⼀个问题是，⽤户提供的是⽂本⽽不是数。在这种情况下，当你尝试将输⼊转换为整数时，将引发 ValueError 异常。编写⼀个程序，提⽰⽤户输⼊两个数，再将它们相加并打印结果。在⽤户输⼊的任意⼀个值不是数时都捕获 ValueError 异常，并打印⼀条友好的错误消息。对你编写的程序进⾏测试：先输⼊两个数，再输⼊⼀些⽂本⽽不是数。
```python
number1 = input("Please enter the first number：")
number2 = input("Please enter the second number：")

try:
    number1 = int(number1)
    number2 = int(number2)
except ValueError:
    print("Attention, you need to enter two numbers.")
else:
    print(f"{number1} + {number2} = {number1 + number2}")
```


#### 练习 10.7：加法计算器 
将为练习 10.6 编写的代码放在⼀个 while 循环中，让⽤户在犯错（输⼊的是⽂本⽽不是数）后能够继续输⼊数。
```python
print("If you want to exit, please enter 'quit' at any time")

while True:
    number1 = input("Please enter the first number：")
    if number1 == "quit":
        print("Successfully exited")
        break

    number2 = input("Please enter the second number：")
    if number2 == "quit":
        print("Successfully exited")
        break

    try:
        number1 = int(number1)
        number2 = int(number2)
    except ValueError:
        print("Attention, you need to enter two numbers.")
    else:
        print(f"{number1} + {number2} = {number1 + number2}")
```


#### 练习 10.8：猫和狗 
创建⽂件 cats.txt 和 dogs.txt，在第⼀个⽂件中⾄少存储三只猫的名字，在第⼆个⽂件中⾄少存储三条狗的名字。编写⼀个程序，尝试读取这些⽂件，并将其内容打印到屏幕上。将这些代码放在⼀个 try-except 代码块中，以便在⽂件不存在时捕获FileNotFoundError 异常，并显⽰⼀条友好的消息。将任意⼀个⽂件移到另⼀个地⽅，并确认 except 代码块中的代码将正确地执⾏。
```python
from pathlib import Path

try:
    message_cats = Path("cats.txt").read_text()
    message_dogs = Path("dogs.txt").read_text()
except FileNotFoundError:
    print("The file was not found, please check")
else:
    print(message_cats)
    print(message_dogs)
```


#### 练习 10.9：静默的猫和狗 
修改你在练习 10.8 中编写的 except 代码块，让程序在⽂件不存在时静默失败。
```python
from pathlib import Path

try:
    message_cats = Path("cats.txt").read_text()
    message_dogs = Path("dogs.txt").read_text()
except FileNotFoundError:
    pass
else:
    print(message_cats)
    print(message_dogs)
```


#### 练习 10.10：常⻅单词 
访问古登堡计划，找⼀些你想分析的图书。下载这些作品的⽂本⽂件或将浏览器中的原始⽂本复制到⽂本⽂件中。  
可以使⽤⽅法 count() 来确定特定的单词或短语在字符串中出现了多少次。例如，下⾯的代码计算 'row' 在⼀个字符串中出现了多少次：  
```python
>>> line = "Row, row, row your boat"
>>> line.count('row')
2
>>> line.lower().count('row')
3
```  
请注意，通过使⽤ lower() 将字符串转换为全⼩写的，可捕捉要查找的单词的各种格式，⽽不管其⼤⼩写如何。  
编写⼀个程序，读取你在古登堡计划中获取的⽂件，并计算单词'the' 在每个⽂件中分别出现了多少次。这⾥计算得到的结果并不准确，因为诸如 'then' 和 'there' 等单词也被计算在内了。请尝试计算 'the '（包含空格）出现的次数，看看结果相差多少。  
```python
from pathlib import Path

story = Path("A_children's_story.text").read_text(encoding = "utf-8")
print(story.lower().count("you")) # 11
print(story.lower().count("i")) # 320
print(story.lower().count("i ")) # 9
print(story.lower().count("the")) # 84
print(story.lower().count("the ")) # 57
```



