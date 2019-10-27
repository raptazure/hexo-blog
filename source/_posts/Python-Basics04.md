---
title: Python Basics04
categories: Python

---
# 函数
## 基本概念：

- 函数代表一个任务或者一个功能，函数是代码复用的通用机制。

- 函数分类：内置函数，标准库函数，第三方库函数，用户自定义函数。

## 函数定义和调用：

- Python执行def会创建一个新的函数对象(对象在堆里)，并绑定到函数名变量(在栈里)上 -> 把对象地址给变量，可通过函数名变量找到对象。

- 圆括号内是形式参数表，有多个参数时应用`，`隔开。形参不需要声明变量类型，也不需要指定函数返回值类型，实参列表要与形参对应。

- return 返回值，不含return则返回None，要返回多个值可用序列存储。

- 调用函数前必须先定义函数(用def创建函数对象)：

  - 内置函数对象会自动创建
  - 标准库和第三方库函数，通过import导入模块时，会执行模块中的def语句。5

  ```python
  def my_func():
      print("$" * 8)
  for i in range(5):
      my_func()
  def printMax(a,b):
      '''compare two numbers and give the bigger one'''
      if a > b:
          print(a,"is bigger")
      else:
          print(b,"is bigger")
      
  printMax(10,20)
  printMax(2,34)
  # 打印文档字符串
  help(printMax)
  
  def test(x,y,z):
      return (x* 10, y * 10, z * 10)
  
  print(test(19, 29, 39))
  # (190, 290, 390)
  ```

```python
def test():
    print("object")
test()
c = test
c()
print(id(test))
print(id(c))
print(type(c))
'''
object
object
139964785728976
139964785728976
<class 'function'>
'''
```

- 全局变量：在函数和类定义之外声明的变量，作用域是定义的模块，一般做常量使用，函数内要改变全局变量的值需用global声明。

  局部变量：在函数体中声明的变量(包含形参)，局部变量存在栈帧里(Stack Frame)，局部变量的引用快于全局变量。若函数内局部变量与全局变量同名，则在函数内屏蔽全局变量。

  使用`print(locals())` `print(globals())`打印所有局部变量和全局变量

  ```python
  # 测试局部变量与全局变量效率
  import math
  import time
  def test():
      start = time.time()
      for i in range(100001):
          math.sqrt(30)
      end = time.time()
      print("time cost: {}".format(end - start))
  def test2():
      b = math.sqrt
      start = time.time()
      for i in range(100001):
          b(30)
      end = time.time()
      print("time cost: {}".format(end - start))
  test()
  test2()
  # time cost: 0.010730981826782227
  # time cost: 0.005475521087646484
  ```

- 参数传递：本质是从实参到形参的赋值操作，Python中一切皆对象，所有赋值操作都是引用的赋值，所以python中的参数传递是“引用传递”而非“值传递”。具体操作分为：

  - 对可变对象(字典，列表，集合，自定义的对象等)进行“写操作”，直接作用于原对象本身。传递参数是可变对象时，实际传递的是对象的引用，在函数中不创建新的对象拷贝，而是可以直接修改所传递的对象。

    ```python
    b = [10, 20]
    def f2(m):
        print("m",id(m))
        m.append(30)
    f2(b)
    print("b",id(b))
    print(b)
    '''
    m 140456535695920
    b 140456535695920
    [10, 20, 30]
    '''
    ```

  - 对不可变对象(数字，字符串，元组，布尔值，function等)进行“写操作”，会产生一个新的“对象空间”，并用新的值填充这块空间(起到其他语言的“值传递”效果但不是“值传递”)。传递对象是不可变对象时，实际传递的也是对象的引用，在“赋值操作”时，由于不可变对象无法修改，系统会新创建一个对象。

    ```python
    a = 10000
    def f(n):
        print("n",id(n))
        n = n + 200
        print("n",id(n))
        print(n)
    f(a)
    print("a",a,id(a))
    '''
    n 140526911552880
    n 140526912199440
    10200
    a 10000 140526911552880
    '''
    #n和a一开始是同一个对象，n值改变->新的对象
    ```

    