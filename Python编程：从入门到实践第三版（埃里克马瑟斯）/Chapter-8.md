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
def make_shirt(Size, Word = "I love Python"):
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


