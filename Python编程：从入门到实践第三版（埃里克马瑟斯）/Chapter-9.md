#### 练习 9.1：餐馆 
创建⼀个名为 Restaurant 的类，为其__init__() ⽅法设置两个属性：restaurant_name 和 cuisine_type。创建⼀个名为 describe_restaurant() 的⽅法和⼀个名为 open_restaurant() 的⽅法，其中前者打印前述两项信息，⽽后者打印⼀条消息，指出餐馆正在营业。  
根据这个类创建⼀个名为 restaurant 的实例，分别打印其两个属性，再调⽤前述两个⽅法。
```python
class Restaurant:

    def __init__(self, restaurant_name, cuisine_type):
        self.name = restaurant_name
        self.type = cuisine_type

    def describe_restaurant(self):
        print(f"The name of this restaurant is {self.name}")
        print(f"The type of food sold is {self.type}")

    def open_restaurant(self):
        print("This restaurant is currently open for business")


restaurant = Restaurant("Chongqing Noodles", "noodles")
print(restaurant.name, restaurant.type)

restaurant.describe_restaurant()
restaurant.open_restaurant()
```

#### 练习 9.2：三家餐馆 
根据为练习 9.1 编写的类创建三个实例，并对每个实例调⽤ describe_restaurant() ⽅法。
```python
class Restaurant:

    def __init__(self, restaurant_name, cuisine_type):
        self.name = restaurant_name
        self.type = cuisine_type

    def describe_restaurant(self):
        print(f"The name of this restaurant is {self.name}")
        print(f"The type of food sold is {self.type}")

    def open_restaurant(self):
        print("This restaurant is currently open for business")

restaurant1 = Restaurant("Chongqing small noodles", "noodles")
restaurant2 = Restaurant("Xi'an Shaobing", "corn cake")
restaurant3 = Restaurant("Beijing Douzhi", "tofu")

restaurant1.describe_restaurant()
restaurant2.describe_restaurant()
restaurant3.describe_restaurant()
```


#### 练习 9.3：⽤户 
创建⼀个名为 User 的类，其中包含属性 first_name 和 last_name，还有⽤户简介中通常会有的其他⼏个属性。在类 User 中定义⼀个名为 describe_user() 的⽅法，⽤于打印⽤户信息摘要。再定义⼀个名为 greet_user() 的⽅法，⽤于向⽤户发出个性化的问候。
```python
class User:

    def __init__(self, first_name, last_name, age, gender):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")

user1 = User("xiao", "chao", 21, "male")
user1.describe_user()
user1.greet_user()
```


#### 练习 9.4：就餐⼈数 
在为练习 9.1 编写的程序中，添加⼀个名为 number_served 的属性，并将其默认值设置为 0。根据这个类创建⼀个名为 restaurant 的实例。打印有多少⼈在这家餐馆就餐过，然后修改这个值并再次打印。  
添加⼀个名为 set_number_served() 的⽅法，⽤来设置就餐⼈数。调⽤这个⽅法并向它传递新的就餐⼈数，然后再次打印这个值。    
添加⼀个名为 increment_number_served() 的⽅法，⽤来让就餐⼈数递增。调⽤这个⽅法并向它传递⼀个这样的值：你认为这家餐馆每天可能接待的就餐⼈数。

```python
class Restaurant:

    def __init__(self, restaurant_name, cuisine_type, number_served = 0):
        self.name = restaurant_name
        self.type = cuisine_type
        self.number = number_served

    def describe_restaurant(self):
        print(f"The name of this restaurant is {self.name}")
        print(f"The type of food sold is {self.type}")

    def open_restaurant(self):
        print("This restaurant is currently open for business")

    def set_number_served(self, number_served):
        self.number = number_served

    def increment_number_served(self, add_number_served):
        self.number = self.number + add_number_served



restaurant = Restaurant("Chongqing Noodles", "noodles")
print(f"{restaurant.number} people have dined at {restaurant.name}")

restaurant.number = 7
print(f"{restaurant.number} people have dined at {restaurant.name}")

restaurant.set_number_served(30)
print(f"{restaurant.number} people have dined at {restaurant.name}")

restaurant.increment_number_served(70)
print(f"{restaurant.number} people have dined at {restaurant.name}")
```

#### 练习 9.5：尝试登录次数 
在为练习 9.3 编写的 User 类中，添加⼀个名为 login_attempts 的属性。编写⼀个名为 increment_login_attempts() 的⽅法，⽤来将属性login_attempts 的值加 1。再编写⼀个名为 reset_login_attempts() 的⽅法，⽤来将属性login_attempts 的值重置为 0。  
根据 User 类创建⼀个实例，再调⽤increment_login_attempts() ⽅法多次。打印属性login_attempts 的值，确认它正确地递增了。然后，调⽤⽅法reset_login_attempts()，并再次打印属性 login_attempts 的值，确认它被重置为 0。
```python
class User:

    def __init__(self, first_name, last_name, age, gender, login_attempts = 0):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender
        self.login_attempts = login_attempts

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")

    def increment_login_attempts(self):
        self.login_attempts += 1

    def reset_login_attempts(self):
        self.login_attempts = 0


user1 = User("xiao", "chao", 21, "male", 10)
print(user1.login_attempts)

user1.increment_login_attempts()
user1.increment_login_attempts()
user1.increment_login_attempts()
print(user1.login_attempts)

user1.reset_login_attempts()
print(user1.login_attempts)
```


#### 练习 9.6：冰激凌⼩店 
冰激凌⼩店是⼀种特殊的餐馆。编写⼀个名为IceCreamStand 的类，让它继承你为练习 9.1 或练习 9.4 编写的Restaurant 类。这两个版本的 Restaurant 类都可以，挑选你更喜欢的那个即可。添加⼀个名为 flavors 的属性，⽤于存储⼀个由各种口味的冰激凌组成的列表。编写⼀个显⽰这些冰激凌⼝味的⽅法。创建⼀个 IceCreamStand 实例，并调⽤这个⽅法。
```python
class Restaurant:

    def __init__(self, restaurant_name, cuisine_type):
        self.name = restaurant_name
        self.type = cuisine_type

    def describe_restaurant(self):
        print(f"The name of this restaurant is {self.name}")
        print(f"The type of food sold is {self.type}")

    def open_restaurant(self):
        print("This restaurant is currently open for business")



class IceCreamStand(Restaurant):

    def __init__(self, restaurant_name, cuisine_type, *favors):
        super().__init__(restaurant_name, cuisine_type)
        self.favors = favors

    def all_favors(self):
        for favor in self.favors:
            print(favor, end = " ")



ice = IceCreamStand("Hunan ice cream", "Frozen products", "Strawberries", "mangoes", "grapes", "bananas")
ice.all_favors()
```

#### 练习 9.7：管理员 
管理员是⼀种特殊的⽤户。编写⼀个名为 Admin 的类，让它继承你为练习 9.3 或练习 9.5 完成编写的 User 类。添加⼀个名为 privileges 的属性，⽤来存储⼀个由字符串（如 "can add post"、"can delete post"、"can ban user" 等）组成的列表。编写⼀个名为 show_privileges() 的⽅法，显⽰管理员的权限。创建⼀个 Admin 实例，并调⽤这个⽅法。
```python
class User:

    def __init__(self, first_name, last_name, age, gender):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")



class Admin(User):

    def __init__(self, first_name, last_name, age, gender):
        super().__init__(first_name, last_name, age, gender)
        self.privileges = ["can add post", "can delete post", "can ban user", "view backend data"]

    def show_privileges(self):
        print("\nthe administrator's permissions include：", end = " ")
        for privilege in self.privileges:
            print(privilege, end = ", ")



admin = Admin("xiao", "chao", 21, "male")
admin.show_privileges()
```


#### 练习 9.8：权限 
编写⼀个名为 Privileges 的类，它只有⼀个属性privileges，其中存储了练习 9.7 所述的字符串列表。将⽅法 show_privileges() 移到这个类中。在 Admin 类中，将⼀个Privileges 实例⽤作其属性。创建⼀个 Admin 实例，并使⽤⽅法show_privileges() 来显⽰权限。
```python
class Privileges:

    def __init__(self):
        self.privileges = ["can add post", "can delete post", "can ban user", "view backend data"]

    def show_privileges(self):
        print("\nthe administrator's permissions include：", end=" ")
        for privilege in self.privileges:
            print(privilege, end=", ")


class User:

    def __init__(self, first_name, last_name, age, gender):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")


class Admin(User):

    def __init__(self, first_name, last_name, age, gender):
        super().__init__(first_name, last_name, age, gender)
        self.privileges = Privileges()


admin = Admin("xiao", "chao", 21, "male")
admin.privileges.show_privileges()
```


#### 练习 9.9：电池升级 
在本节最后⼀个 electric_car.py 版本中，给Battery 类添加⼀个名为 upgrade_battery() 的⽅法。这个⽅法检查电池容量，如果电池容量不是 65，就设置为 65。创建⼀辆电池容量为默认值的电动汽⻋，调⽤⽅法 get_range()，然后对电池进⾏升级，并再次调⽤ get_range()。你将看到这辆汽⻋的续航⾥程增加了。
```python
class Car:
    """一次模拟汽车的简单尝试"""

    def __init__(self, make, model, year):
        """初始化描述汽车的属性"""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """返回格式规范的描述性名称"""
        long_name = f"{self.year} {self.make} {self.model}"
        return long_name.title()

    def read_odometer(self):
        """打印一个句子，指出汽车的行驶里程"""
        print(f"This car has {self.odometer_reading} miles on it.")

    def update_odometer(self, mileage):
        """将里程表读数设置为给定的值"""
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't rool back an odometer!")

    def increment_odometer(self, miles):
        """让里程表读数增加给定的量"""
        self.odometer_reading += miles


class Battery:
    """一次模拟电动汽车电池的简单尝试"""

    def __init__(self, battery_size = 40):
        """初始化电池的属性"""
        self.battery_size = battery_size

    def describe_battery(self):
        """打印⼀条描述电池容量的消息"""
        print(f"This car has a {self.battery_size}-kWh battery.")

    def get_range(self):
        """打印一条消息，指出电池的续航里程"""
        if self.battery_size == 40:
            range = 150
        elif self.battery_size == 65:
            range = 225
        print(f"this car can go about {range} miles on a full charge.")

    def upgrade_battery(self):
        if self.battery_size != 65:
            self.battery_size = 65



class ElectricCar(Car):
    """电动汽车的独特之处"""

    def __init__(self, make, model, year):
        """初始化父类的属性"""
        super().__init__(make, model, year)
        self.battery = Battery()


electric_car = ElectricCar("China", "Benchi", 2026)
electric_car.battery.get_range()
electric_car.battery.upgrade_battery()
electric_car.battery.get_range()
```


#### 练习 9.10：导⼊ Restaurant 类 
将最新的 Restaurant 类存储在⼀个模块中。在另⼀个⽂件中导⼊ Restaurant 类，创建⼀个 Restaurant 实例，并调⽤ Restaurant 的⼀个⽅法，以确认import 语句正确⽆误。
```python
# t1.py
class Restaurant:

    def __init__(self, restaurant_name, cuisine_type):
        self.name = restaurant_name
        self.type = cuisine_type

    def describe_restaurant(self):
        print(f"The name of this restaurant is {self.name}")
        print(f"The type of food sold is {self.type}")

    def open_restaurant(self):
        print("This restaurant is currently open for business")
```
```python
from t1 import Restaurant

restaurant = Restaurant("Chong Qing noodles", "noodles")
restaurant.describe_restaurant()
restaurant.open_restaurant()
```


#### 练习 9.11：导⼊ Admin 类 
以为完成练习 9.8 ⽽做的⼯作为基础。将 User 类、Privileges 类和 Admin 类存储在⼀个模块中，再创建⼀个⽂件，在其中创建⼀个 Admin 实例并对其调⽤show_privileges() ⽅法，以确认⼀切都能正确地运⾏。
```python
# t1.py
class Privileges:

    def __init__(self):
        self.privileges = ["can add post", "can delete post", "can ban user", "view backend data"]

    def show_privileges(self):
        print("\nthe administrator's permissions include：", end=" ")
        for privilege in self.privileges:
            print(privilege, end=", ")


class User:

    def __init__(self, first_name, last_name, age, gender):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")


class Admin(User):

    def __init__(self, first_name, last_name, age, gender):
        super().__init__(first_name, last_name, age, gender)
        self.privileges = Privileges()
```
```python
from t1 import Admin

admin = Admin("xiao", "chao", 21, "male")
admin.privileges.show_privileges()
```


#### 练习 9.12：多个模块 
将 User 类存储在⼀个模块中，并将 Privileges 类和 Admin 类存储在另⼀个模块中。再创建⼀个⽂件，在其中创建⼀个 Admin 实例并对其调⽤ show_privileges() ⽅法，以确认⼀切依然能够正确地运⾏。
```python
# t1.py
class User:

    def __init__(self, first_name, last_name, age, gender):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
        self.gender = gender

    def describe_user(self):
        print(f"this user's name：{self.first_name} {self.last_name}")
        print(f"this user's age：{self.age}")
        print(f"this user's gender：{self.gender}")

    def greet_user(self):
        print(f"Hello! How are you? {self.first_name} {self.last_name}")
```
```python
# t2.py
from t1 import User

class Privileges:

    def __init__(self):
        self.privileges = ["can add post", "can delete post", "can ban user", "view backend data"]

    def show_privileges(self):
        print("\nthe administrator's permissions include：", end=" ")
        for privilege in self.privileges:
            print(privilege, end=", ")


class Admin(User):

    def __init__(self, first_name, last_name, age, gender):
        super().__init__(first_name, last_name, age, gender)
        self.privileges = Privileges()
```
```python
from t2 import Admin

admin = Admin("xiao", "chao", 21, "male")
admin.privileges.show_privileges()
```


#### 练习 9.13：骰⼦ 
创建⼀个 Die 类，它包含⼀个名为 sides 的属性，该属性的默认值为 6。编写⼀个名为 roll_die() 的⽅法，它打印位于 1 和骰⼦⾯数之间的随机数。创建⼀个 6 ⾯的骰⼦并掷 10 次。  
创建⼀个 10 ⾯的骰⼦和⼀个 20 ⾯的骰⼦，再分别掷 10 次。
```python
from random import randint

class Die:

    def __init__(self, sides = 6):
        self.sides = sides

    def roll_die(self):
        print(randint(1, self.sides))

die1 = Die()
for i in range(1, 11, 1):
    print(f"\nsides = {die1.sides}", end = " ")
    die1.roll_die()

die2 = Die(10)
for i in range(1, 11, 1):
    print(f"\nsides = {die2.sides}", end=" ")
    die2.roll_die()

die3 = Die(20)
for i in range(1, 11, 1):
    print(f"\nsides = {die3.sides}", end=" ")
    die3.roll_die()
```


#### 练习 9.14：彩票 
创建⼀个列表或元组，其中包含 10 个数和 5 个字⺟。从这个列表或元组中随机选择 4 个数或字⺟，并打印⼀条消息，指出只要彩票上是这 4 个数或字⺟，就中⼤奖了。
```python
from random import sample

list = [20, 2, 26, 61, 11, 12, 21, 16, 9, 10, "x", "y", "k", "n", "w"]

print(f"If your ticket is {sample(list, 4)}, then you have won the big prize!")
# If your ticket is ['y', 10, 61, 'n'], then you have won the big prize!
```


#### 练习 9.15：彩票分析 
可以使⽤⼀个循环来理解中前述彩票⼤奖有多难。为此，创建⼀个名为 my_ticket 的列表或元组，再编写⼀个循环，不断地随机选择数或字⺟，直到中⼤奖为⽌。请打印⼀条消息，报告执⾏多少次循环才中了⼤奖。
```python
from random import sample, shuffle

my_ticket = []

for i in range(1, 51, 1):
    my_ticket.append(i)
for i in range(ord("a"), ord("z") + 1, 1):
    my_ticket.append(chr(i))

shuffle(my_ticket)

prize_ticket = [19, 31, "w", "x"]
cnt = 0
while True:
    print(f"cnt == {cnt}")
    if sorted(sample(my_ticket, k = 4), key = str) == sorted(prize_ticket, key = str):
        break
    else:
        cnt += 1

print(f"randomly drew {cnt} times before winning")
# randomly drew 1041063 times before winning
```

### 练习 9.16：Python 3 Module of the Week 
要了解 Python 标准库，⼀个很不错的资源是⽹站 Python 3 Module of the Week。请访问该⽹站并查看其中的⽬录，找⼀
个你感兴趣的模块进⾏探索，从模块 random开始可能是个不错的选择。  

#### 1. 导入模块
```python
import random
```

#### 2. 生成随机浮点数
- random.random()：生成一个 [0.0, 1.0) 之间的随机浮点数
- random.uniform(a, b)：生成一个 [a, b] 之间的随机浮点数
```python
print(random.random()) # 0.1482560820611496 
print(random.uniform(1., 1.1)) # 1.0990825428837556
```

#### 3. 生成随机整数
- random.randint(a, b)：生成一个 [a, b] 之间的随机整数（包含 a 和 b）
```python
print(random.randint(1, 10)) # 9
```

#### 4. 从序列中随机选择
- random.choice(seq)：从非空序列（如列表、元组、字符串）中随机选择一个元素。
- random.choices(seq, k = n)：从非空序列（如列表、元组、字符串）中随机选择 n 元素（可以重复）。
- random.sample(seq, k = n)：从非空序列（如列表、元组、字符串）中随机选择 n 元素（不可以重复）。
```python
print(random.choice(s)) # 7
print(random.choices(s, k = 3)) # ['4', '2', '4']
print(random.sample(s, k = 3)) # ['2', '9', '7']
```

#### 5. 打乱序列
- random.shuffle(seq)：原地打乱一个可变序列（如列表）。注意它返回 None
```python
list = list(range(1, 11, 1))
print(list) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

random.shuffle(list)
print(list) # [2, 3, 5, 8, 9, 4, 7, 10, 1, 6]
```