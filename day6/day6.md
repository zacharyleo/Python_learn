# 一、函数

- 参数是函数
- 返回值是函数

## 1. 定义 

- 函数以def关键词开头，后接函数名和圆括号()。
- 函数执行的代码以冒号起始，并且缩进。
- return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回None。

``` python
def functionname(parameters):
    "函数_文档字符串"
    function_suite
    return [expression]
```

## 2.调用


```python
def printme(str):
    print(str)


printme("我要调用用户自定义函数!")  
printme("再次调用同一函数") 
temp = printme('hello') 
print(temp)  
```

    我要调用用户自定义函数!
    再次调用同一函数
    hello
    None
    

## 3.函数文档


```python
def MyFirstFunction(name):
    "函数定义过程中name是形参"
    print('传递进来的{0}叫做实参，因为Ta是具体的参数值！'.format(name))


MyFirstFunction('老马的程序人生')  
# 传递进来的老马的程序人生叫做实参，因为Ta是具体的参数值！

print(MyFirstFunction.__doc__)  
# 函数定义过程中name是形参

help(MyFirstFunction)
# Help on function MyFirstFunction in module __main__:
# MyFirstFunction(name)
#    函数定义过程中name是形参
```

    传递进来的老马的程序人生叫做实参，因为Ta是具体的参数值！
    函数定义过程中name是形参
    Help on function MyFirstFunction in module __main__:
    
    MyFirstFunction(name)
        函数定义过程中name是形参
    
    

## 4. 函数参数

- 位置参数 (positional argument)
- 默认参数 (default argument)
- 可变参数 (variable argument)
- 关键字参数 (keyword argument)
- 命名关键字参数 (name keyword argument)
- 参数组合

### 4.1 位置参数

``` python
def functionname(arg1):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- arg1 - 位置参数 ，这些参数在调用函数 (call function) 时位置要固定。

### 4.2  默认参数

``` python
def functionname(arg1, arg2=v):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- arg2 = v - 默认参数 = 默认值，调用函数时，默认参数的值如果没有传入，则被认为是默认值。
- 默认参数一定要放在位置参数 后面，不然程序会报错。


```python
def printinfo(name, age=8):
    print('Name:{0},Age:{1}'.format(name, age))


printinfo('小马')  # Name:小马,Age:8
printinfo('小马', 10)  # Name:小马,Age:10
```

    Name:小马,Age:8
    Name:小马,Age:10
    

### 4.3 可变参数

- 可变参数就是传入的参数个数是可变的，可以是 0, 1, 2 到任意个，是不定长的参数。

``` python
def functionname(arg1, arg2=v, *args):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- *args - 可变参数，可以是从零个到任意个，自动组装成元组。
- 加了星号（*）的变量名会存放所有未命名的变量参数。


```python
def printinfo(arg1, *args):
    print(arg1)
    for var in args:
        print(var)


printinfo(10)  # 10
printinfo(70, 60, 50)
```

    10
    70
    60
    50
    

### 4.4 关键字参数

``` python
def functionname(arg1, arg2=v, *args, **kw):
    "函数_文档字符串"
    function_suite
    return [expression]
```

- **kw - 关键字参数，可以是从零个到任意个，自动组装成字典。


```python
def printinfo(arg1, *args, **kwargs):
    print(arg1)
    print(args)
    print(kwargs)


printinfo(70, 60, 50)
# 70
# (60, 50)
# {}
printinfo(70, 60, 50, a=1, b=2)
# 70
# (60, 50)
# {'a': 1, 'b': 2}
```

    70
    (60, 50)
    {}
    70
    (60, 50)
    {'a': 1, 'b': 2}
    

- 可变参数允许传入零个到任意个参数，它们在函数调用时自动组装为一个元组 (tuple)。
- 关键字参数允许传入零个到任意个参数，它们在函数内部自动组装为一个字典 (dict)。

## 5. 返回值


```python
def add(a, b):
    return a + b


print(add(1, 2))  # 3
print(add([1, 2, 3], [4, 5, 6]))  # [1, 2, 3, 4, 5, 6]
```

    3
    [1, 2, 3, 4, 5, 6]
    


```python
def back():
    return [1, '小马的程序人生', 3.14]


print(back())  # [1, '小马的程序人生', 3.14]
```

    [1, '小马的程序人生', 3.14]
    


```python
def back():
    return 1, '小马的程序人生', 3.14


print(back())  # (1, '小马的程序人生', 3.14)
```

    (1, '小马的程序人生', 3.14)
    


```python
def printme(str):
    print(str)

temp = printme('hello') # hello
print(temp) # None
print(type(temp))  # <class 'NoneType'>
```

    hello
    None
    <class 'NoneType'>
    

### 6. 变量作用域

- Python 中，程序的变量并不是在哪个位置都可以访问的，访问权限决定于这个变量是在哪里赋值的。
- 定义在函数内部的变量拥有局部作用域，该变量称为局部变量。
- 定义在函数外部的变量拥有全局作用域，该变量称为全局变量。
- 局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。


```python
def discounts(price, rate):
    final_price = price * rate
    return final_price


old_price = float(input('请输入原价:'))  # 98
rate = float(input('请输入折扣率:'))  # 0.9
new_price = discounts(old_price, rate)
print('打折后价格是:%.2f' % new_price)  # 88.20
```

    请输入原价:98
    请输入折扣率:0.9
    打折后价格是:88.20
    

- 修改外部作用域的变量时，就要用到global和nonlocal


```python
num = 1


def fun1():
    global num  # 需要使用 global 关键字声明
    print(num)  # 1
    num = 123
    print(num)  # 123


fun1()
print(num)  # 123
```

    1
    123
    123
    

### 6.1 闭包

- 是函数式编程的一个重要的语法结构，是一种特殊的内嵌函数。
- 如果在一个内部函数里对外层非全局作用域的变量进行引用，那么内部函数就被认为是闭包。
- 通过闭包可以访问外层非全局作用域的变量，这个作用域称为 闭包作用域。


```python
def funX(x):
    def funY(y):
        return x * y

    return funY


i = funX(8)
print(type(i))  # <class 'function'>
print(i(5))  # 40
```

    <class 'function'>
    40
    

- 修改闭包作用域中的变量则需要 nonlocal


```python
def outer():
    num = 10

    def inner():
        nonlocal num  # nonlocal关键字声明
        num = 100
        print(num)

    inner()
    print(num)


outer()

# 100
# 100
```

    100
    100
    

### 6.2 递归

- 如果一个函数在内部调用自身本身，这个函数就是递归函数。

- n! = 1 x 2 x 3 x ... x n


```python
# 利用循环
n = 5
for k in range(1, 5):
    n = n * k
print(n)  # 120

# 利用递归
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n - 1)


print(factorial(5)) # 120
```

    120
    120
    

- 斐波那契数列 f(n)=f(n-1)+f(n-2), f(0)=0 f(1)=1


```python
# 利用循环
i = 0
j = 1
lst = list([i, j])
for k in range(2, 11):
    k = i + j
    lst.append(k)
    i = j
    j = k
print(lst)  
# [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

# 利用递归
def recur_fibo(n):
    if n <= 1:
        return n
    return recur_fibo(n - 1) + recur_fibo(n - 2)


lst = list()
for k in range(11):
    lst.append(recur_fibo(k))
print(lst)  
# [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
    [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
    

- 设置递归的层数，Python默认递归层数为 100


```python
import sys

sys.setrecursionlimit(1000)
```

# 二、Lambda 表达式

## 1. 定义

在 Python 里有两类函数：

- 第一类：用 def 关键词定义的正规函数
- 第二类：用 lambda 关键词定义的匿名函数

python 使用 lambda 关键词来创建匿名函数，而非def关键词，它没有函数名，其语法结构如下：

``` python
lambda argument_list: expression
```

- ambda - 定义匿名函数的关键词。
- argument_list - 函数参数，它们可以是位置参数、默认参数、关键字参数，和正规函数里的参数类型一样。
- :- 冒号，在函数参数和表达式中间要加个冒号。
- expression - 只是一个表达式，输入函数参数，输出一些值。
注意：

- expression 中没有 return 语句，因为 lambda 不需要它来返回，表达式本身结果就是返回值。
匿名函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。


```python
def sqr(x):
    return x ** 2


print(sqr)
# <function sqr at 0x000000BABD3A4400>

y = [sqr(x) for x in range(10)]
print(y)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

lbd_sqr = lambda x: x ** 2
print(lbd_sqr)
# <function <lambda> at 0x000000BABB6AC1E0>

y = [lbd_sqr(x) for x in range(10)]
print(y)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


sumary = lambda arg1, arg2: arg1 + arg2
print(sumary(10, 20))  # 30

func = lambda *args: sum(args)
print(func(1, 2, 3, 4, 5))  # 15
```

    <function sqr at 0x000001FF41C4EAF8>
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
    <function <lambda> at 0x000001FF41C4E828>
    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
    30
    15
    

### 2. 应用

- 非函数式编程


```python
def f(x):
    for i in range(0, len(x)):
        x[i] += 10
    return x


x = [1, 2, 3]
f(x)
print(x)
# [11, 12, 13]
```

    [11, 12, 13]
    

- 函数式编程

函数式编程 是指代码中每一块都是不可变的，都由纯函数的形式组成。这里的纯函数，是指函数本身相互独立、互不影响，对于相同的输入，总会有相同的输出，没有任何副作用。


```python
def f(x):
    y = []
    for item in x:
        y.append(item + 10)
    return y


x = [1, 2, 3]
f(x)
print(x)
# [1, 2, 3]
```

    [1, 2, 3]
    

# 3.练习题：

1. 怎么给函数编写⽂档？
2. 怎么给函数参数和返回值注解？
3. 闭包中，怎么对数字、字符串、元组等不可变元素更新。
4. 分别根据每一行的首元素和尾元素大小对二维列表 a = [[6, 5], [3, 7], [2, 8]] 排序。(利用lambda表达式)
5. 利用python解决汉诺塔问题？

有a、b、c三根柱子，在a柱子上从下往上按照大小顺序摞着64片圆盘，把圆盘从下面开始按大小顺序重新摆放在c柱子上，尝试用函数来模拟解决的过程。（提示：将问题简化为已经成功地将a柱上面的63个盘子移到了b柱）



1. 怎么给函数编写⽂档？


```python
def functionname(parameters):
    "函数_文档字符串"
    function_suite
    return [expression]
'''查看函数文档'''
print(MyFirstFunction.__doc__)  
help(MyFirstFunction)
```

    函数定义过程中name是形参
    Help on function MyFirstFunction in module __main__:
    
    MyFirstFunction(name)
        函数定义过程中name是形参
    
    

2. 怎么给函数参数和返回值注解？

- 参数注解就是，在定义函数的时候，参数列表内部的参数后面，加上冒号和要传入的类型，例：
``` python
def accumlate(x:int, y:int):
    return x*y
```

- 写了参数注解也无法强制限定变量的类型，只能作为提示，来告知使用者应该传入什么类型的参数。
- 返回值注解就是：
``` python
def accumlate(x:int, y:int) -> int:
    return x*y
```

3. 闭包中，怎么对数字、字符串、元组等不可变元素更新。

- 闭包是函数式编程的一个重要的语法结构，是一种特殊的内嵌函数。
- 如果在一个内部函数里对外层非全局作用域的变量进行引用，那么内部函数就被认为是闭包。
- 通过闭包可以访问外层非全局作用域的变量，这个作用域称为 闭包作用域。
- 闭包的返回值通常是函数。
- 如果要修改闭包作用域中的变量则需要 nonlocal 关键字

4. 分别根据每一行的首元素和尾元素大小对二维列表 a = [[6, 5], [3, 7], [2, 8]] 排序。(利用lambda表达式)


```python
a=[[6, 5], [3, 7], [2, 8]] 
print(a)
x = sorted(a, key=lambda a: a[0], reverse=False)
print("按照首字符正序排列：",x)
x = sorted(a, key=lambda a: a[0], reverse=True)
print("按照首字符逆序排列：",x)
x = sorted(a, key=lambda a: a[1], reverse=False)
print("按照尾字符正序排列：",x)
x = sorted(a, key=lambda a: a[1], reverse=True)
print("按照尾字符逆序排列：",x)
```

    [[6, 5], [3, 7], [2, 8]]
    按照首字符正序排列： [[2, 8], [3, 7], [6, 5]]
    按照首字符逆序排列： [[6, 5], [3, 7], [2, 8]]
    按照尾字符正序排列： [[6, 5], [3, 7], [2, 8]]
    按照尾字符逆序排列： [[2, 8], [3, 7], [6, 5]]
    

5 . 利用python解决汉诺塔问题？

有a、b、c三根柱子，在a柱子上从下往上按照大小顺序摞着64片圆盘，把圆盘从下面开始按大小顺序重新摆放在c柱子上，尝试用函数来模拟解决的过程。（提示：将问题简化为已经成功地将a柱上面的63个盘子移到了b柱）

采用递归

当n=1时，H(1)=1,即A—>C；

当n=2时，H(2)=3,即A—>B,A—>C,B—>C;

当n>2时，可以将第1个盘子到第n-1个盘子看成一个整体为①，这样就仍为两个盘子：

第一步：①从A—>B：共H(n-1)步;

第二步：n 从A—>C：共1步;

第三步：①从B—>C：共H(n-1)步.

把上63个看成整体，可便于理解

代码：




```python
def Hanoi(n,a,b,c):
    if n == 1:
        print(str(a)+"移动到"+str(c))
    else:
        Hanoi(n-1, a, c, b)# 把上面（n-1）个盘子从A移到B
        Hanoi(1, a, b, c)# 最底下的1个盘子，从A移到C
        Hanoi(n-1, b, a, c)# 把（n-1）个盘子从B移到C
Hanoi(64, 'a', 'b', 'c')
```


```python

```
