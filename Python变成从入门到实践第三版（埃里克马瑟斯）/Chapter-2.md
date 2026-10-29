```python
# 练习 2.3：个性化消息　用变量表示一个人的名字，并向其显示一条消息。显示的消息应非常简单，如下所示。
# Hello Eric, would you like to learn some Python today?
  
name = "xiaochao"
print(f"Hello {name.title()}, would you like to learn some Python today?")
```

```python
# 练习 2.4：调整名字的大小写　用变量表示一个人的名字，再分别以全小写、全大写和首字母大写的方式显示这个人名。
name = "xiaochao"
print(name.lower())
print(name.upper())
print(name.title())
```

```python
# 练习 2.5：名言 1　找到你钦佩的名人说的一句名言，将这个名人的姓名和名言打印出来。输出应类似于下面这样（包括引号）。
# Albert Einstein once said, “A person who never made a mistake never tried anything new.” 

name = "Jewel Tarik"
Famous_quote = "I have stepped on the mountaintop and entered the valley, both of which have benefited me greatly. Although the process of climbing is long, the scenery at the peak is worth it. Failure is always the best mentor. Control your fate, otherwise fate will control you."

print(f"{name.title()} once said, \"{Famous_quote}\"") 
```

```python
# 练习 2.7：删除人名中的空白　用变量表示一个人的名字，并在其开头和末尾都包含一些空白字符。务必至少使用字符组合 "\t" 和 "\n" 各一次。
# 打印这个人名，显示其开头和末尾的空白。然后，分别使用函数 lstrip()、rstrip() 和 strip() 对人名进行处理，并将结果打印出来。

name = "  xiaochao  \t\n"
print(name)
print(name.strip())
print(name.lstrip())
print(name.rstrip())
```
