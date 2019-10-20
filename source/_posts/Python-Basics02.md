---
title: Python Basics02
categories: Python
---

## 字符串

#### 基本特点：

- 字符串的本质是字符序列。Python的字符串是不可变的，我们无法对原字符串做任何修改，但是可以将字符串的一部分复制到新创建的字符串，达到“看起来修改”的效果。

- Python不支持单字符类型，单字符也是作为一个字符串使用的

  <!-- more -->

#### 字符串编码：

- Python3 支持Unicode，可以表示世界上任何书面语言的字符，Python3 的字符默认就是16位Unicode编码，ASCII码是Unicode编码的子集。

- 使用`ord()`可以把字符转换为对应的Unicode码，使用`chr()`可以把十进制数字转换为对应的字符。

#### 引号创建字符串：

- 可通过单引号或双引号创建字符串，根据情况使用两种引号。
- 连续三个单(双)引号，可以创建多行字符串。

#### 空字符串和len() 函数：

- Python允许空字符串的存在，不包含任何字符且长度为0，例如`c=‘’`
- len()用于计算字符串有多少字符

#### 转义字符：

- 使用`\+特殊字符`实现换行，回车，退格，制表等

-  `\续行符` `\\反斜杠` `\'单引号` `\"双引号` (和C相似)

#### 字符串操作：

- 拼接：可以使用+将多个字符串拼接起来，如`”aa“+”bb“+”cc“`，形成一个新字符串（新对象），如果+两边类型不同，会输出异常。因为使用+会生成新字符串对象，所以更推荐使用join()函数，因为此函数在拼接前会计算所有字符串长度，然后再逐一拷贝，仅新建一次对象。
- 复制：使用*实现复制，比如`“–” * 3`
- 不换行打印：调用print时会自动打印换行符，通过`end=“字符串”`进行改变。

```python
print("rapt",end=' ')
print("azure",end='##')
```
- 从控制台读取字符串：使用`input()`从控制台读取键盘输入的内容。

- `str()`实现数字转型字符串：比如`str(3.14e2)`>>>`314.0` ,调用`print()`函数时，解释器自动调用量str()将非字符串的对象转成了字符串。

- 使用[]提取字符：字符串的本质是字符序列，可以在[]里指定偏移量(索引)来提取该位置的单个字符，可以进行反向搜索。

  从左到右：`0` -> `len(str)-1`          从右到左：`-len(str)` <- `-1 `

- `replace()`实现字符串“替换”：字符串“不可变”，替换只能通过创建新字符串对象，原来的变量指向新字符串来实现。比如`a=a.replace(‘c’,‘a’)`

- `slice()`实现字符串切片：提取子字符串，格式`[start:end:step]`

  ```python
  Python 3.7.4 (default, Oct  4 2019, 06:57:26) 
  [GCC 9.2.0] on linux
  
  >>> a = "abcdefghijklmn"
  >>> a[2]
  'c'
  >>> a[1:5:1]
  'bcde'
  >>> a[1:5]
  'bcde'
  >>> a[1:5:2]
  'bd'
  >>> a[:]
  'abcdefghijklmn'
  >>> a[2:]
  'cdefghijklmn'
  >>> a[:2]
  'ab'
  >>> a[-3:]
  'lmn'
  >>> a[-8:-3]
  'ghijk'
  >>> a[::-1]
  'nmlkjihgfedcba'
  >>> a[2:400]
  'cdefghijklmn'
  ```

- `split()`分割和`join()`合并：split可以基于指定分隔符将字符串分割成多个子字符串（存储到列表中），如果不指定分隔符，默认使用空白字符(制表，换行，空格)。`join()`作用相反，用于合并一系列子字符串。

```python
>>> a = "2B or not 2B"
>>> a.split()
['2B', 'or', 'not', '2B']
>>> a.split('2B')
['', ' or not ', '']
>>> a =["2B","or","not","2B"]
>>> "*".join(a)
'2B*or*not*2B'
>>> " ".join(a)
'2B or not 2B'
```

- 一个小测试：使用join与+拼接字符串的不同效率

  ```python
  import time
  a = ""
  time01 = time.time()
  for i in range(1000000):
      a += "hit"    #创建1000000个对象
  time02 = time.time()
  print(time02-time01)
  
  time03 = time.time()
  li = []           #只有一个对象
  for i in range(1000000):
      li.append("hit")
  a = "".join(li)
  time04 = time.time()
  print(time04-time03)
  
  #0.16577386856079102
  #0.11212515830993652
  ```

#### 字符串驻留机制和字符串比较：

- 字符串驻留：仅保存一份相同且不可变字符串的方法，不同的值被存放在字符串驻留池中。Python支持字符串驻留机制，对于符合标识符规则(字母，下划线，数字)的字符串会启用字符串驻留机制。

```python
>>> a = "abd_22"
>>> b = "abd_22"
>>> a is b
True  # 同一个对象
>>> c = "dd#"
>>> d = "dd#"
>>> c is d
False
```

- 成员操作符：`in/not in`判断某个子字符串是否存在字符串中

  ```python
  >>> a = "23333"
  >>> "2" in a
  True
  ```

#### 字符串常用方法：

- 查找：

```python
>>> a = "this is a simple test"
>>> len(a)
21
>>> a.startswith("this")
True
>>> a.endswith("est")
True
>>> a.find(" ")
4
>>> a.rfind('s')
19   
>>> a.count("s")
4       #计数出现次数
>>> a.isalnum()
False   #是否全是字母和数字
```

- 去除首尾信息：


```python
>>> a = "#this is a test#"
>>> a.strip("#")
'this is a test'
>>> "*h*i*t*".rstrip("*")
'*h*i*t'  #去掉了右边的*
>>> "       hit     ".strip()
'hit'
```

- 大小写转换：以下都产生了新字符串


```python
>>> a = 'hit wh'
>>> a.capitalize()
'Hit wh'
>>> a.title()
'Hit Wh'
>>> a.upper()
'HIT WH'
>>> a.swapcase()
'HIT WH'  #所有字母大小写转换
```

- 格式排版：


```python
>>> a = 'HIT'
>>> a.center(10)
'   HIT    '
>>> a.center(9,'#')
'###HIT###'
>>> a.ljust(10,'#')
'HIT#######'
```

- 其他方法：
  - `isalnum()`是否为字母或数字
  - `isalpha()`检测字符串是否只由字母组成(含汉字) ->Unicode
  - `isdigit()`检测是否只由数字组成
  - `isspace()`检测是否为空白字符
  - `isupper()`是否为大写字母
  - `islower()`是否为小写字母

#### 字符串格式化

- `format()`基本用法：可以通过{索引}或者{参数名}直接映射参数值。

  ```python
  >>> a = "my name is: {0}. my age is: {1}"
  >>> a.format("raptazure",18)
  'my name is: raptazure. my age is: 18'
  >>> a.format("r",2)
  'my name is: r. my age is: 2'
  >>> b = "my name is {0} and {0} is good."
  >>> b.format("r")
  'my name is r and r is good.'
  >>> c = "name:{name}  age:{age}"
  >>> c.format(age = 19, name = 'r')
  'name:r  age:19'
  ```
- 填充与对齐：^ < > 分别是居中，左对齐，右对齐，后面带宽度。:后带填充的字符，只能是一个字符，不指定默认用空格填充。

```python
>>> "{:*>8}".format('2333')
'****2333'
>>> "I am {0},I like {1:*^8}".format("R","233")
'I am R,I like **233***'
```

#### 数字格式化：

- ```python
  >>> a = "I am {0} and my number is {1:.2f}"
  >>> a.format("R",23333.5566)
  'I am R and my number is 23333.56'
  # {:,} 三位用，隔开
  # {:.2e} 指数记法
  # {:.2%} 百分比格式
  # {:+.2f} 带符号保留小数点后两位
  # {:x<4d} 数字补x，填充右边，宽度为4
  # {:10d} 默认右对齐，宽度为10
  ```

#### 可变字符串：

- Python中的字符串属于不可变对象，不可原地修改，修改其中的值只能创建新字符串对象。如果确实需要原地修改字符串，可用`io.StringIO`对象或`array`模块。

```python
>>> import io
>>> s = "rapt"
>>> sio = io.StringIO(s)
>>> sio
<_io.StringIO object at 0x7f5e56094870>
>>> sio.getvalue()
'rapt'
>>> sio.seek(3)
3
>>> sio.write('9')
1
>>> sio.getvalue()
'rap9'
```

## 