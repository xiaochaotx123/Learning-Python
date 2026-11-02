#### 练习 9.1：餐馆 
创建⼀个名为 Restaurant 的类，为其__init__() ⽅法设置两个属性：restaurant_name 和 cuisine_type。创建⼀个名为 describe_restaurant() 的⽅法和⼀个名为 open_restaurant() 的⽅法，其中前者打印前述两项信息，⽽后者打印⼀条消息，指出餐馆正在营业。  
根据这个类创建⼀个名为 restaurant 的实例，分别打印其两个属性，再调⽤前述两个⽅法。
```python
class Restaurant:

    def __init__(self,  restaurant_name, cuisine_type):
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

    def __init__(self,  restaurant_name, cuisine_type):
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

    def __init__(self,  restaurant_name, cuisine_type, number_served = 0):
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

    def __init__(self,  restaurant_name, cuisine_type):
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