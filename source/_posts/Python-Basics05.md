---
title: Python Basics05
categories: Python
---
# 面向对象编程

## 简介
​		面向对象编程将数据和操作数据相关方法封装到对象中，组织代码和数据的方式更加接近人的思维，从而大大提高编程效率。更加关注软件中对象中的关系，是一种设计者思维，适合编写大规模程序。面向对象离不开面向过程，二者相辅相成，宏观使用面向对象把握，微观处理仍是面向过程。遇到复杂问题，面向对象先从问题中找名词(面向过程更多的是找动词)，确定这些名词哪些可以作为类，再根据问题需求确定类的属性和方法，确定类之间的关系。

<!--more-->
## 对象

​		将不同类型的数据，方法(函数)放在一起 -> 对象

```python
class Student: # 类名一般首字母大写，采用驼峰规则
    compony = "233"    # 类属性
    count = 0          # 类属性
    def __init__(self, name, score): #self必须位于第一个参数 
        self.name = name      # 实例属性
        self.score = score
        Student.count = Student.count + 1
    def say_score(self):      # 实例方法
        print("my compony is 233")
```

## 类的定义

- 通过类定义数据类型的属性(变量)和方法(行为)，类将行为和状态打包在一起。从一个类创建对象时，每个对象会共享这个类的行为(类中定义的方法)，但会有自己的属性(不共享状态)，更具体一些：“方法代码共享，属性数据不共享”。

- Python中一切皆对象，类也叫做类对象，类的实例也叫做实例对象。

  ```python
  class Student: # 类名一般首字母大写，采用驼峰规则
      compony = "233"    # 类属性
      def __init__(self, name, score):  # self必须位于第一个参数 
          self.name = name      # 实例属性
          self.score = score
      def say_score(self):      # 实例方法
          print(f"{self.name}'s score is {self.score}.")
  
  s1 = Student("rapt", 18) # 通过类名()调用构造函数
  s1.say_score()  #s1是实例对象，自动调用__init()__方法
  ```

## 构造函数`__init__()`

- 类是抽象的，也称为“对象的模板”，通过类这个模板创建类的实例对象，然后才能使用类定义的功能。

- Python对象包含如下部分：id，type，value (attribute, method)

- 创建对象需要定义构造函数`__init__()`方法，构造方法用于执行“实例对象的初始化工作”，即对象创建后，初始化当前对象的相关属性，无返回值。

- `__inti__`名称固定，第一个参数必须为`self`，self就是指刚创建好的实例对象。构造函数通常用来初始化实例对象的实例属性。

- 通过“类名(参数列表)”来调用构造函数，将创建好的对象返回给相应的变量。比如`s1 = Student(‘rapt’, 18)`

- `__init__()`方法：初始化创建好的对象(给实例属性赋值)

  `__new()__`方法：用于创建对象，但一般无需重定义该方法

- Python中的self相当于C++中的self指针，Java和C#中的this关键字，Python中self必须为构造函数的第一个参数，名字可以任意修改。但一般遵守惯例，都叫做self。

## 实例属性

- 从属于实例对象的属性，也称为“实例变量”
- 一般在`__init__()`方法中通过`self.实例属性名 = 初始值`定义
- 在本类的其他实例方法中，也是通过self进行访问 `self.实例属性名`
- 创建实例对象后，通过实例对象访问：
  - `obj01 = 类名()`  创建对象，调用`__init__()`初始化属性
  - `obj01.实例属性名 = 值` 给已有属性赋值，也可以新加属性

## 实例方法

- 从属于对象的方法，定义格式：

  ```python
  def 方法名(self, [形参列表]):
      函数体
  '''
  方法的调用格式如下：
  	对象：方法名([实参列表])
  '''
  ```

- 定义实例方法时，第一个参数必须为self(指当前的实例对象)

- 调用实例方法时，self由解释器自动传参

  ```python
  # 实例对象的方法调用本质：
  a = Student()
  a.say_score()
  # 解释器翻译为 -> Stduent.say_score(a)
  ```

- 其他操作：
  - `dir(obj)` 获得对象的所有属性，方法
  - `obj.__dict__()` 对象(定义)的属性字典
  - `pass` 空语句
  - `isinstance(对象, 类型)` 判断‘对象’是不是‘指定类型’

## 类对象

- 解释器执行class语句时就会创建一个类对象

  ```python
  class Student:
      pass
  
  print(type(Student))
  print(id(Student))
  Stu2 = Student
  s1 = Stu2()
  print(s1)
  '''
  <class 'type'>
  94630656980368
  <__main__.Student object at 0x7f25bddc1ad0>
  '''
  ```
## 类属性和类方法
- 类属性是从属于“类对象”的属性，可以被所有实例对象共享

  ```python
  class Student:
      company = 'microsoft'
      count = 0
      def __init__(self, name, score):
          self.name = name
          self.score = score
          Student.count += 1
      def say_score(self):
          print("my company is:", Student.company)
          print(self.name, "score is", self.score)
  
  s1 = Student("rapt", 100)
  s1.say_score()
  
  s2 = Student("r", 99)
  s2.say_score()
  
  print("created {0} objects in total".format(Student.count))
  '''
  my company is: microsoft
  rapt score is 100
  my company is: microsoft
  r score is 99
  created 2 objects in total
  '''
  ```
  
- 类方法是从属于“类对象”的方法，通过装饰器`@classmethod`来定义

  - 定义时装饰器必须位于方法上面一行

  - 要在第一个位置写上cls (cls指“类对象”本身)

  - 类方法中访问实例属性会导致错误 -> 还不能调self

  - 子类继承父类方法时，传入cls是子类对象，而非父类对象

```python
class Student:
    company = 'radhat'  # 类属性
    @classmethod
    def printCompany(cls):
        print(cls.company)

Student.printCompany()
```

- 静态方法：Python中允许定义与”类对象“无关的方法，称为静态方法

  - 静态方法和在模块中定义普通函数没有区别，只是静态方法放到了类的命名空间里面，需要通过类调用。

  - 通过装饰器`@staticmethod`定义

  - 静态方法中访问实例属性和实例方法会导致错误

```python
class Student:
    company = 'radhat'  # 类属性
    @staticmethod
    def add(a, b):
        print(f"{a} + {b} = {a + b}")
        return a + b

Student.add(4, 5)
```
## 析构函数和垃圾回收机制

- `__del__()`称为析构方法，用于实现对象被销毁时所需的操作，比如：释放对象占用的资源，例如：打开的文件资源，网络连接等。

- Python实现自动的垃圾回收，当对象没有被引用时(引用计数为0)，由垃圾回收器调用`__del__()`方法。

- 也可以通过del语句删除对象，从而调用`__del__()`方法。

- 系统会自动提供`__del__()`方法，一般不需要自定义析构方法。

```python
class Person:
    def __del__(self):
        print("delete object: {0}".format(self))

p1 = Person()
p2 = Person()
del p2
print("the end")
# 之后销毁p1
'''
delete object: <__main__.Person object at 0x7f781ef1d990>
the end
delete object: <__main__.Person object at 0x7f781ef1d910>
'''
```