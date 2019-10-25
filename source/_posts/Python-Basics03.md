---
title: Python Basics03
categories: Python
---

# 常见结构

## 选择结构：

#### 单分支选择结构：

- if 条件表达式(逻辑，关系，算术)，注意缩进。

  ```python
  num = input("please input a number")
  if int(num)<10:
      print(num)
  ```
  
  <!-- more -->
  
- 条件表达式值为False的情况如下：False，0，0.0，None空值，空序列对象（空列表，空元组，空字典，空字符串），空range对象，空迭代对象,其他均为True。条件表达式中不能有赋值操作符‘=’(报语法错误)
  
  ```python
  if 3:
      print("ok")
  a = []
  if a:
      print("empty list,False")
  s = "False"
  if s:
      print("string,True")
  c = 9
  if 3<c<10:
      print("True")
  ‘’‘
  ok
  string,True
  True
  ’‘’
  ```
#### 多分支选择结构:

```python
#VS Code Python3.7.4
s = input("please input a number")
if int(s) < 10:
    print("s is smaller than 10")
else:
    print("s is bigger")
# 三元条件运算符
num = input("please input another number")
print(num if int(num) < 10 else "too big")

#多分支结构种分支有逻辑关系,不可随意颠倒顺序
score = int(input("please input your score "))
grade = ""
if score < 60:
    grade = 'E'
elif score < 80:
    grade = 'D'
elif score < 90:
    grade = 'B'
else:
    grade = 'A'
print("your score is {0} and your grade is {1}".format(score,grade))
# 多分支也可只用if,但推荐elif
# 选择结构嵌套注意缩进
score = int(input("please input your score "))
degree = 'ABCDE'
num = 0
if score > 100 or score < 0:
    print("please input a number between 0 and 100")
else:
    num = score//10
    if num < 5:
        num = 5
    print(degree[9-num])
```

## 循环结构：

```python
## while
num = 0
while num < 100:
    print(num,end = '\t')
    num += 1
## for  用于可迭代对象的遍历
for x in (20,30,40):
    print(x*3)
for x in "rapt":
    print(x)
d = {'name':'rapt','age':18}
for x in d:
    print(x)
for x in d.values():
    print(x)
for x in d.keys():
    print(x)
for x in d.items():
    print(x)
'''
name
age
rapt
18
name
age
('name', 'rapt')
('age', 18)
'''
sum_even = 0
sum_odd = 0
for num in range(101):
    if num%2==0:
        sum_even += num
    else:
        sum_odd += num
print("even sum = {0}, odd sum = {1}".format(sum_even,sum_odd))
## 嵌套循环
for x in range(5):
    for y in range(5):
        print(x,end = '\t')
    print()
'''
0	0	0	0	0	
1	1	1	1	1	
2	2	2	2	2	
3	3	3	3	3	
4	4	4	4	4	
'''
# 打印乘法表
for m in range(1,10):
    for n in range(1,m+1):
        print("{0} * {1} = {2}".format(m,n,(m*n)), end = '\t')
    print()
# 与字典配合
r1 = dict(name='rapt1',age=18)
r2 = dict(name='rapt2',age=19)
r3 = dict(name='rapt3',age=20)
table = [r1,r2,r3]
for x in table:
    if x.get('age') >= 19:
        print(x)
# break结束整个循环 & continue结束本次循环进入下一次
empNum = 0
salarySum = 0
salary = []
while True:
    s = input("Please enter the salary:")
    if s.upper() == 'Q':
        print("quit")
        break
    if float(s) < 0:
        continue
    empNum += 1
    salary.append(float(s))
    salarySum += float(s)
print("the number of employees:{0}".format(empNum))
print("salary:",salary)
print(f"average salary:{salarySum/empNum}")
# while，for循环可以附带一个else语句，如果for，while没有被break结束，则会执行else子句
empNum = 0
salarySum = 0
salary = []
for i in range(4):
    s = input("Please enter the salary:")
    if s.upper() == 'Q':
        print("quit")
        break
    if float(s) < 0:
        continue
    empNum += 1
    salary.append(float(s))
    salarySum += float(s)
else:
    print("you have entered salary of all the employees")
print("the number of employees:{0}".format(empNum))
print("salary:",salary)
print(f"average salary:{salarySum/empNum}")
```

- 循环代码优化：

  - 尽量减少循环内部不必要的计算
- 嵌套循环中尽量减少内层循环计算，尽可能外提
  - 局部变量查询较快，尽量使用局部变量
- 连续多个字符串，使用`join()`不用+
  - 列表进行元素插入和删除，尽量在列表尾部操作

 ```python
import  time
start = time.time()
for i in range(1000):
    result = []
    for m in range(10000):
        result.append(i*1000+m*100)
end = time.time()
print(f'time cost:{end - start}')

start2 = time.time()
for i in range(1000):
    result = []
    c = i*1000 
    for m in range(10000):
        result.append(c+m*100)
end2 = time.time()
print(f"time cost:{end2 - start2}")
# time cost:1.810370922088623
# time cost:1.4288480281829834
 ```

- `zip()`进行并行迭代：

  ```python
  names = ['rapt','azure','linux']
  ages = [18,19,50]
  jobs = ['stu','pro','opt']
  
  for name,age,job in zip(names,ages,jobs):
      print("{0}--{1}--{2}".format(name,age,job))
  # 相同功能也可通过以下代码实现
  for i in range(3):
      print("{0}--{1}--{2}".format(names[i],ages[i],jobs[i]))
  
  '''
  rapt--18--stu
  azure--19--pro
  linux--50--opt
  '''
  ```

  

