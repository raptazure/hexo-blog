---
title: Python Exception
categories: Python
---

## 异常

- 异常即是一个事件，该事件会在程序执行过程中发生，影响了程序的正常执行。一般情况下，在Python无法正常处理程序时就会发生一个异常。当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。

  <!--more-->

- Python中引入了很多用来描述和处理异常的类，称为异常类。异常类定义中包含了该类异常的信息和对异常进行处理的方法。内建异常类的继承层次：比如`BaseException -> Exception -> NameError, ValueError, AttributeError etc.`

- Python中一切皆对象，异常也采用对象的方式进行处理：

  - 抛出异常：在执行一个方法时，如果发生异常，则这个方法生成代表该异常的一个对象，停止当前执行路径，并把异常对象提交给解释器。
  - 捕获异常：解释器得到该异常后，寻找相应代码来处理该异常。

- Python提供了异常处理和断言(Assertions)两个非常重要的功能来处理程序在运行中出现的异常和错误。

  | 异常名称                  | 描述                                               |
  | :------------------------ | :------------------------------------------------- |
  | BaseException             | 所有异常的基类                                     |
  | SystemExit                | 解释器请求退出                                     |
  | KeyboardInterrupt         | 用户中断执行(通常是输入^C)                         |
  | Exception                 | 常规错误的基类                                     |
  | StopIteration             | 迭代器没有更多的值                                 |
  | GeneratorExit             | 生成器(generator)发生异常来通知退出                |
  | StandardError             | 所有的内建标准异常的基类                           |
  | ArithmeticError           | 所有数值计算错误的基类                             |
  | FloatingPointError        | 浮点计算错误                                       |
  | OverflowError             | 数值运算超出最大限制                               |
  | ZeroDivisionError         | 除(或取模)零 (所有数据类型)                        |
  | AssertionError            | 断言语句失败                                       |
  | AttributeError            | 对象没有这个属性                                   |
  | EOFError                  | 没有内建输入,到达EOF 标记                          |
  | EnvironmentError          | 操作系统错误的基类                                 |
  | IOError                   | 输入/输出操作失败                                  |
  | OSError                   | 操作系统错误                                       |
  | WindowsError              | 系统调用失败                                       |
  | ImportError               | 导入模块/对象失败                                  |
  | LookupError               | 无效数据查询的基类                                 |
  | IndexError                | 序列中没有此索引(index)                            |
  | KeyError                  | 映射中没有这个键                                   |
  | MemoryError               | 内存溢出错误(对于Python 解释器不是致命的)          |
  | NameError                 | 未声明/初始化对象 (没有属性)                       |
  | UnboundLocalError         | 访问未初始化的本地变量                             |
  | ReferenceError            | 弱引用(Weak reference)试图访问已经垃圾回收了的对象 |
  | RuntimeError              | 一般的运行时错误                                   |
  | NotImplementedError       | 尚未实现的方法                                     |
  | SyntaxError               | Python 语法错误                                    |
  | IndentationError          | 缩进错误                                           |
  | TabError                  | Tab 和空格混用                                     |
  | SystemError               | 一般的解释器系统错误                               |
  | TypeError                 | 对类型无效的操作                                   |
  | ValueError                | 传入无效的参数                                     |
  | UnicodeError              | Unicode 相关的错误                                 |
  | UnicodeDecodeError        | Unicode 解码时的错误                               |
  | UnicodeEncodeError        | Unicode 编码时错误                                 |
  | UnicodeTranslateError     | Unicode 转换时错误                                 |
  | Warning                   | 警告的基类                                         |
  | DeprecationWarning        | 关于被弃用的特征的警告                             |
  | FutureWarning             | 关于构造将来语义会有改变的警告                     |
  | OverflowWarning           | 旧的关于自动提升为长整型(long)的警告               |
  | PendingDeprecationWarning | 关于特性将会被废弃的警告                           |
  | RuntimeWarning            | 可疑的运行时行为(runtime behavior)的警告           |
  | SyntaxWarning             | 可疑的语法的警告                                   |
  | UserWarning               | 用户代码生成的警告                                 |

## try…except

- 结构：

  ```python
  try:
  	<被监控的可能引发异常的语句块>        
  except BaseException [as e]：
  	<异常处理语句块> 
  ```
  
- 遇到异常的执行顺序：

  ```python
  try:
      print("step01")
      a = 3 / 0
      print("step02")
  except BaseException as e:
      print("step03")
      print(e)
      print(type(e))
  print("step04")
  # 跳过try块中异常以后的代码
  '''
  step01
  step03
  division by zero
  <class 'ZeroDivisionError'>
  step04
  '''
  ```

- 应用：循环输入数字，如果不是数字则处理异常，如果输入88则结束循环

  ```python
  while True:
      try:
          x = int(input("please input a number: "))
          print("last input:", x)
          if x == 88:
              print("exit the loop")
              break
      except BaseException as e:
          print(e)
          print("Input error!")
  print("exit!!!")
  ```

- try…多个except结构：从经典理论考虑，建议尽量捕获可能出现的多个异常(按照先子类后父类的顺序)，并且针对性地写出异常处理代码，为了避免遗漏可能出现的异常，可以在最后增加BaseException。

  ```python
  try:
  	<被监控的可能引发异常的语句块>   
  except Exception1:
      <处理Exception1的语句块>
  except Exception2:
      <处理Exception2的语句块>
  
      
  except BaseException：
  	<处理可能遗漏的异常的语句块> 
  ```

- 测试`try…多个except`结构：

  ```python
  try:
      a = input("please input a dividend:")
      b = input("please input a divisor:")
      c = float(a) / float(b)
      print(c)
  except ZeroDivisionError:
      print("can not divide by zero!")
  except ValueError:
      print("can not cast!")
  except NameError:
      print("Variable does not exist!")
  except BaseException as e:
      print(e)
  ```

