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