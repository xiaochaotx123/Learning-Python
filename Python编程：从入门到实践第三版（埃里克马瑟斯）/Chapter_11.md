#### 练习 11.1：城市和国家 
编写⼀个函数，它接受两个形参：⼀个城市名和⼀个国家名。这个函数返回⼀个格式为 City, Country 的字符串，如 Santiago, Chile。将这个函数存储在⼀个名为city_functions.py 的模块中，并将这个⽂件存储在⼀个新的⽂件夹中，以免 pytest 在运⾏时，尝试运⾏之前编写的测试。  
创建⼀个名为 test_cities.py 的程序，对刚编写的函数进⾏测试。编写⼀个名为 test_city_country() 的函数，核实在使⽤类似于'santiago' 和 'chile' 这样的值来调⽤该函数时，得到的字符串是正确的。运⾏测试，确认 test_city_country() 通过了。  
```python
# city_functions.py
def city_country(city, country):
    full_name = f"{city}, {country}"
    return full_name
```
```python
# test_cities.py 
from city_functions import city_country

def test_city_country():
    full_name = city_country('Chongqing', 'China')
    assert full_name == 'Chongqing, China'
```


练习 11.2：⼈⼝数量 
修改前⾯的函数，使其包含第三个必不可少的形参 population，并返回⼀个格式为 City, Country - population xxx 的字符串，如 Santiago, Chile - population 5000000。运⾏测试，确认 test_city_country()未通过。  
修改上述函数，将形参 population 设置为可选的。再次运⾏测试，确认 test_city_country() ⼜通过了。  
再编写⼀个名为 test_city_country_population() 的测试，核实可以使⽤类似于 'santiago'、'chile' 和'population=5000000' 这样的值来调⽤这个函数。再次运⾏测试，确认 test_city_country_population() 通过了。
```python
# city_functions.py
def city_country(city, country, population = None):

    if population is None:
        full_name = f"{city}, {country}"
    else:
        full_name = f"{city}, {country} - population {population}"

    return full_name
```
```python
# test_cities.py
from city_functions import city_country

def test_city_country():
    full_name = city_country('Chongqing', 'China')
    assert full_name == 'Chongqing, China'

def test_city_country_population():
    full_name = city_country('Chongqing', 'China', 1900000)
    assert full_name == 'Chongqing, China - population 1900000'
```


#### 练习 11.3：雇员 
编写⼀个名为 Employee 的类，其 __init__() ⽅法接受名、姓和年薪，并将它们都存储在属性中。编写⼀个名为give_raise() 的⽅法，它默认将年薪增加 5000 美元，同时能够接受其他的年薪增加量。  
为 Employee 类编写⼀个测试⽂件，其中包含两个测试函数：test_give_default_raise() 和 test_give_custom_raise()。在不使⽤夹具的情况下编写这两个测试，并确保它们都通过了。然后，编写⼀个夹具，以免在每个测试函数中都创建⼀个 Employee 对象。重新运⾏测试，确认两个测试都通过了。  
```python
# employee.py
class Employee:

    def __init__(self, employee_name, employee_age, employee_salary):
        self.name = employee_name
        self.age = employee_age
        self.salary = employee_salary

    def give_raise(self, add_salary = 5000):
        self.salary += add_salary
```
```python
# test_employee.py
from employee_functions import Employee

def test_give_default_raise():
    employee = Employee('xiaochao', 21, 10000)
    employee.give_raise()

    assert employee.salary == 15000

def test_give_custom_raise():
    employee = Employee('xiaochao', 21, 12000)
    employee.give_raise(8000)

    assert employee.salary == 20000
```
```python
# test_employee_two.py
import pytest
from employee_functions import Employee

@pytest.fixture
def employee():

    employee = Employee('xiaochao', 21, 10000)
    return employee

def test_give_default_raise(employee):
    employee.give_raise()
    assert employee.salary == 15000

def test_give_custom_raise(employee):
    employee.give_raise(10000)
    assert employee.salary == 20000
```