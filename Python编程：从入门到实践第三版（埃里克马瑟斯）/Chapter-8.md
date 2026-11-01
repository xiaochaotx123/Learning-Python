#### 练习 8.1：消息 
编写⼀个名为 display_message() 的函数，让它打印⼀个句⼦，指出本章的主题是什么。调⽤这个函数，确认显⽰的消息正确⽆误。
```python
def display_message():
    print("Learn to write functions")

display_message()
```


#### 练习 8.2：喜欢的书 
编写⼀个名为 favorite_book() 的函数，其中包含⼀个名为 title 的形参。让这个函数打印⼀条像下⾯这样的消息。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;One of my favorite books is Alice in Wonderland.  
调⽤这个函数，并将⼀本书的书名作为实参传递给它。
```python
def favorite_book(title):
    print(f"One of my favorite books is {title}.")

favorite_book("Hello C")
```


#### 练习 8.3：T 恤 
编写⼀个名为 make_shirt() 的函数，它接受⼀个尺码以及要印到 T 恤上的字样。这个函数应该打印⼀个句⼦，简要地说明 T 恤的尺码和字样。  
先使⽤位置实参调⽤这个函数来制作⼀件 T 恤，再使⽤关键字实参来调⽤这个函数。
```python
def make_shirt(Size, Word):
    print(f"The size of this T-shirt is {Size}")
    print(f"The words on this T-shirt are {Word}")

make_shirt("XL", "NB")
make_shirt(Size = "XXXL", Word = "NBB")
```


#### 练习 8.4：⼤号 T 恤 
修改 make_shirt() 函数，使其在默认情况下制作⼀件印有“I love Python”字样的⼤号 T 恤。调⽤这个函数分别制作⼀件印有默认字样的⼤号 T 恤，⼀件印有默认字样的中号 T 恤，以及⼀件印有其他字样的 T 恤（尺码⽆关紧要）。
```python
def make_shirt(Size = "L", Word = "I love Python"):
    print(f"The size of this T-shirt is {Size}")
    print(f"The words on this T-shirt are {Word}")

make_shirt("4XL")
make_shirt("middle")
make_shirt("XL", "LEARNING!")
```


#### 练习 8.5：城市 
编写⼀个名为 describe_city() 的函数，它接受⼀座城市的名字以及该城市所属的国家。这个函数应该打印⼀个像下⾯这样简单的句⼦。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reykjavik is in Iceland.  
给⽤于存储国家的形参指定默认值。为三座不同的城市调⽤这个函数，其中⾄少有⼀座城市不属于默认的国家。
```python
def describe_city(city, country = "China"):
    print(f"{city} is in {country}")

describe_city("Beijing")
describe_city("New York", "The USA")
describe_city(city = "London", country = "The UK")
```


#### 练习 8.6：城市名 
编写⼀个名为 city_country() 的函数，它接受城市的名称及其所属的国家。这个函数应返回⼀个格式类似于下⾯的字符串：  
"Santiago, Chile"  
⾄少使⽤三个城市⾄国家对调⽤这个函数，并打印它返回的值。
```python
def city_country(city, country):
    s = f"{city}, {country}"
    return s

print(city_country("Beijing", "China"))
print(city_country("New York", "The USA"))
print(city_country("Tokyo", "Japan"))   
```


#### 练习 8.7：专辑 
编写⼀个名为 make_album() 的函数，它创建⼀个描述⾳乐专辑的字典。这个函数应接受歌⼿名和专辑名，并返回⼀个包含这两项信息的字典。使⽤这个函数创建三个表⽰不同专辑的字典，并打印每个返回的值，以核实字典正确地存储了专辑的信息。  
给 make_album() 函数添加⼀个默认值为 None 的可选形参，以便存储专辑包含的歌曲数。如果调⽤这个函数时指定了歌曲数，就将这个值添加到表⽰专辑的字典中。调⽤这个函数，并⾄少在⼀次调⽤中指定专辑包含的歌曲数。
```python
def  make_album(singer_name, album_title):
    return {
        "singer_name" : singer_name,
        "album_title" : album_title,
    }

print(make_album("xiaochao", "xc"))
print(make_album("xiaoyue", "xy"))
print(make_album("xiaoling", "xl"))

def make_album1(singer_name, album_title, number = None):
    if number is not None:
        number = int(number)
        return {
            "singer_name": singer_name,
            "album_title": album_title,
            "number" : number,
        }
    else:
        return {
            "singer_name": singer_name,
            "album_title": album_title,
        }

print(make_album1("xiaochao", "xc", 5))
print(make_album1("xiaoyue", "xy", 3))
print(make_album1("xiaoling", "xl"))
print(make_album1("xiaoling", "xl", "0"))
print(make_album1("xiaoling", "xl", 0))
```


#### 练习 8.8：⽤户的专辑 
在为练习 8.7 编写的程序中，编写⼀个 while循环，让⽤户输⼊歌⼿名和专辑名。获取这些信息后，使⽤它们来调⽤ make_album() 函数并将创建的字典打印出来。在这个 while 循环中，务必提供退出途径。
```python
def make_album(singer_name, album_title, number = None):
    if number:
        return {
            "singer_name": singer_name,
            "album_title": album_title,
            "number" : number,
        }
    else:
        return {
            "singer_name": singer_name,
            "album_title": album_title,
        }


print("If you want to exit, just enter 'quit' at any time")
while True:
    singer_name = input("Please enter the singer's name：")
    if singer_name == "quit":
        break

    album_title = input("Please enter the album name：")
    if album_title == "quit":
        break

    number = input("How many songs does this album have? (or 'quit' to exit): ")
    if number == "quit":
        break
        
    print(make_album(singer_name, album_title, number))
```


#### 练习 8.9：消息 
创建⼀个列表，其中包含⼀系列简短的⽂本消息。将这个列表传递给⼀个名为 show_messages() 的函数，这个函数会打印列表中的每条⽂本消息。
```python
def show_messages(number):
    for num in number:
        print(num, end = " ")



num = list(range(1, 11, 1))
show_messages(num)
```


#### 练习 8.10：发送消息 
在为练习 8.9 编写的程序中，编写⼀个名为send_messages() 的函数，将每条消息都打印出来并移到⼀个名为sent_messages 的列表中。调⽤ send_messages() 函数，再将两个列表都打印出来，确认把消息移到了正确的列表中。
```python
def show_messages(number):
    for num in send_number:
        print(num, end=" ")

def send_messages(number, send_number):
    while number:
        num = number.pop()
        print(f"{num} is send!")
        send_number.append(num)

number= list(range(1, 11, 1))
send_number = []
show_messages(number)
send_messages(number, send_number)

print(number)
print(send_number)
```


#### 练习 8.11：消息归档 
修改为练习 8.10 编写的程序，在调⽤函数send_messages() 时，向它传递消息列表的副本。调⽤send_messages() 函数后，将两个列表都打印出来，确认原始列表保留了所有的消息。
```python
def show_messages(number, send_number):
    while number:
        num = number.pop()
        print(f"{num} is send!")
        send_number.append(num)

def send_messages(send_number):
    for num in send_number:
        print(num, end = " ")

number= list(range(1, 11, 1))
send_number = []
show_messages(number[:], send_number)
print(number)
send_messages(send_number)
```

#### 练习 8.12：三明治 
编写⼀个函数，它接受顾客要在三明治中添加的⼀系列⾷材。这个函数只有⼀个形参（它收集函数调⽤中提供的所有⾷材），并打印⼀条消息，对顾客点的三明治进⾏概述。调⽤这个函数三次，每次都提供不同数量的实参。
```python
def add_toppings(*toppings):
    if toppings:
        for topping in toppings:
            print(f"We will add {topping} to the sandwich dish")
    else:
        print("We will make a plain sandwich for you!")

add_toppings(1)
add_toppings(1, 2, 3, 4)
add_toppings(9, 10, 11111, 222323, 99999)
add_toppings()
```


#### 练习 8.13：⽤户简介 
复制前⾯的程序 user_profile.py，在其中调⽤build_profile() 来创建有关你的简介。在调⽤这个函数时，指定你的名和姓，以及三个⽤来描述你的键值对。
```python'
def build_profile(first, last, **user_info):
    """创建⼀个字典，其中包含我们知道的有关⽤户的⼀切"""
    user_info['first_name'] = first
    user_info['last_name'] = last
    return user_info

user_profile = build_profile("xiao", "chao",
                             like = "play games",
                             food = "rice",
                             male = "nan"
                             )
print(user_profile)
```

#### 练习 8.14：汽⻋ 
编写⼀个函数，将⼀辆汽⻋的信息存储在字典中。这个函数总是接受制造商和型号，还接受任意数量的关键字实参。在调⽤这个函数时，提供必不可少的信息，以及两个名值对，如颜⾊和选装配件。这个函数必须能够像下⾯这样调⽤：  
car = make_car('subaru', 'outback', color='blue', tow_package=True)  
打印返回的字典，确认正确地处理了所有的信息。  
```python
def make_car(Manufacturer, model, **car_info):
    car_info["Manufacturer"] = Manufacturer
    car_info["model"] = model
    return car_info

my_car = make_car("huawei", "Mercedes-Benz",
                  color = "black",
                  size = "big",
                  )
print(my_car)
```


#### 练习 8.15：打印模型 
将⽰例 printing_models.py 中的函数放在⼀个名为 printing_ functions.py 的⽂件中。在 printing_models.py 的开头编写⼀条 import 语句，并修改这个⽂件以使⽤导⼊的函数。
```python
printing_functions.py

def painting():
    # ⾸先创建⼀个列表，其中包含⼀些要打印的设计
    unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
    completed_models = []
    # 模拟打印每个设计，直到没有未打印的设计为⽌
    # 打印每个设计后，都将其移到列表 completed_models 中
    while unprinted_designs:
        current_design = unprinted_designs.pop()
        print(f"Printing model: {current_design}")
        completed_models.append(current_design)
    # 显⽰打印好的所有模型
    print("\nThe following models have been printed:")
    for completed_model in completed_models:
        print(completed_model)
```
```python
import printing_functions

printing_functions.painting()
```


#### 练习 8.16：导⼊ 
选择⼀个你编写的且只包含⼀个函数的程序，将这个函数放在另⼀个⽂件中。在主程序⽂件中，使⽤下述各种⽅法导⼊这个函数，再调⽤它：  
import module_name  
from module_name import function_name  
from module_name import function_name as fn  
import module_name as mn  
from module_name import *  
```python
xc_functions.py

def add(a, b):
    print(a + b)

def mul(a, b):
    print(a * b)
```
```python
# 方式1
# import xc_functions

# xc_functions.add(3, 4)
# xc_functions.mul(3, 4)

# 方式2
# from xc_functions import add, mul
#
# add(3, 4)
# mul(3, 4)

# 方式3
# from xc_functions import add as ad
# from xc_functions import mul as mu
#
# ad(3, 4)
# mu(3, 4)

# 方式4
# import xc_functions as xc
#
# xc.add(3, 4)
# xc.mul(3, 4)

# 方式5
# from xc_functions import *
# 
# add(3, 4)
# mul(3, 4)
```