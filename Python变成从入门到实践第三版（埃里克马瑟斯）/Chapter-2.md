#### 练习 2.3：个性化消息  
用变量表示一个人的名字，并向其显示一条消息。显示的消息应非常简单，如下所示。  

Hello Eric, would you like to learn some Python today?


```python  
name = "xiaochao"
print(f"Hello {name.title()}, would you like to learn some Python today?")
```


#### 练习 2.4：调整名字的大小写  
用变量表示一个人的名字，再分别以全小写、全大写和首字母大写的方式显示这个人名。
```python
name = "xiaochao"
print(name.lower())
print(name.upper())
print(name.title())
```


#### 练习 2.5：名言 1　  
找到你钦佩的名人说的一句名言，将这个名人的姓名和名言打印出来。  
输出应类似于下面这样（包括引号）。  

Albert Einstein once said, “A person who never made a mistake never tried anything new.” 
```python
name = "Jewel Tarik"
Famous_quote = "I have stepped on the mountaintop and entered the valley, both of which have benefited me greatly. Although the process of climbing is long, the scenery at the peak is worth it. Failure is always the best mentor. Control your fate, otherwise fate will control you."

print(f"{name.title()} once said, \"{Famous_quote}\"") 
```

#### 练习 2.7：删除人名中的空白　  
用变量表示一个人的名字，并在其开头和末尾都包含一些空白字符。务必至少使用字符组合 "\t" 和 "\n" 各一次。  

打印这个人名，显示其开头和末尾的空白。然后，分别使用函数 lstrip()、rstrip() 和 strip() 对人名进行处理，并将结果打印出来。

```python
name = "  xiaochao  \t\n"
print(name)
print(name.strip())
print(name.lstrip())
print(name.rstrip())
```
strip()不传入参数时，默认删除字符串两段的所有空白字符，包括  
- 普通空格" "  
- 制表符 \t
- 换行符 \n
- 回车符 \r
- 换页符 \f
- 垂直制表符 \v
- 以及其他 Unicode 空白字符

#### 练习 2.8：⽂件扩展名 
Python 提供了 removesuffix() ⽅法，其⼯作原理与 removeprefix() 很像。请将值 'python_notes.txt'
赋给变量 filename，再使⽤ removesuffix() ⽅法来显⽰不包含
扩展名的⽂件名，就像⽂件浏览器所做的那样。
```python
filename = "python_notes.txt"
filename = filename.removesuffix(".txt")
print(filename)
```

#### 练习 2.9：数字 8 
编写 4 个表达式，分别使⽤加法、减法、乘法和除
法运算，但结果都是数字 8。为了使⽤函数调⽤ print() 来显⽰结
果，务必将这些表达式⽤括号括起来。也就是说，你应该编写 4 ⾏类
似于这样的代码：  
print(5+3)  
```python
print(4 + 4)
print(10 - 2)
print(2 * 4)
print((int)(16 / 2))
```  


#### 练习 2.10：最喜欢的数   
⽤⼀个变量来表⽰你最喜欢的数，再使⽤这
个变量创建⼀条消息，指出你最喜欢的数是什么，然后将这条消息打
印出来。  
```python
favorite_num = 19
print(f"我最喜欢的数字是{favorite_num}，因为我觉得{favorite_num}很有个性")
```