# 01. 变量、运算符与数据类型

## 3.变量和赋值



```python
myTeacher = "老马的程序人生"
yourTeacher = "小马的程序人生"
print(myTeacher)
```

    老马的程序人生
    


```python
print(myTeacher+','+yourTeacher)
```

    老马的程序人生,小马的程序人生
    

## 4. 数据类型与转换

Python 里面万物皆对象（object），整型也不例外，只要是对象，就有相应的属性 （attributes） 和方法（methods）。


```python
a = 1031
print(bin(a)) 
```

    0b10000000111
    


```python
print(a.bit_length())  

```

    11
    


```python
print(1, type(1))

```

    1 <class 'int'>
    


```python

print(1., type(1.))

```

    1.0 <class 'float'>
    


```python
import decimal
a = decimal.getcontext()
print(a)
```

    Context(prec=28, rounding=ROUND_HALF_EVEN, Emin=-999999, Emax=999999, capitals=1, clamp=0, flags=[], traps=[InvalidOperation, DivisionByZero, Overflow])
    

想保留浮点型的小数点后 n 位。可以用 decimal 包里的 Decimal 对象和 getcontext() 方法来实现。



```python
from decimal import Decimal
decimal.getcontext().prec = 4
c = Decimal(1)/ 3
print(c)
```

    0.3333
    

使 1/3 保留 4 位，用 getcontext().prec 来调整精度。

### 布尔型

除了直接给变量赋值 True 和 False，还可以用 bool(X) 来创建变量，其中 X 可以是

基本类型：整型、浮点型、布尔型

容器类型：字符串、元组、列表、字典和集合

bool 作用在基本类型变量：X 只要不是整型 0、浮点型 0.0，bool(X) 就是 True


```python
print(bool(0), bool(1))
```

    False True
    


```python
print(bool(0.00), bool(10.31))
```

    False True
    


```python
print(bool(False), bool(True))
```

    False True
    

确定bool(X) 的值是 True 还是 False，就看 X 是不是空，空的话就是 False，不空的话就是 True。



```python
print(type(''), bool(''), bool('python'))
```

    <class 'str'> False True
    


```python
print(type(()), bool(()), bool((10,)))
```

    <class 'tuple'> False True
    


```python
print(type([]), bool([]), bool([1, 2]))
```

    <class 'list'> False True
    


```python
print(type({}), bool({}), bool({'a': 1, 'b': 2}))
```

    <class 'dict'> False True
    


```python
print(type(set()), bool(set()), bool({1, 2}))
```

    <class 'set'> False True
    

对于数值变量，0, 0.0 都可认为是空的。

对于容器变量，里面没元素就是空的。

### 类型转换

- 转换为整型 int(x, base=10)
- 转换为字符串 str(object='')
- 转换为浮点型 float(x)


```python
print(int('520')) 
```

    520
    


```python
print(int(520.52))  
```

    520
    


```python
print(float('520.52')) 
```

    520.52
    


```python
print(float(520))  
```

    520.0
    


```python
print(str(10 + 10)) 
```

    20
    


```python
print(str(10.1 + 5.2)) 
```

    15.3
    

### print 打印


```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
for item in shoplist:
    print(item)
```

    apple
    mango
    carrot
    banana
    


```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
for item in shoplist:
    print(item, 'another string', sep=' & ')
```

    apple & another string
    mango & another string
    carrot & another string
    banana & another string
    

item值与'another string'两个值之间用sep设置的参数 & 分割。由于end参数没有设置，因此默认是输出解释后换行，即end参数的默认值为\n。

# 练习题
1. 怎样对python中的代码进行注释？
2. python有哪些运算符，这些运算符的优先级是怎样的？
3. python 中 is, is not 与 ==, != 的区别是什么？
4. python 中包含哪些数据类型？这些数据类型之间如何转换？

1. 怎样对python中的代码进行注释？

#作用于整行

''' ''' 或者 """ """，在三引号之间的所有内容被注释

2. python有哪些运算符，这些运算符的优先级是怎样的？

算术运算符、比较运算符、逻辑运算符、位运算符、三元运算符、其他运算符

运算符的优先级

- 一元运算符优于二元运算符。
- 先算术运算，后移位运算，最后位运算。
- 逻辑运算最后结合。

3. python 中 is, is not 与 ==, != 的区别是什么？

- is, is not 对比的是两个变量的内存地址

- ==, != 对比的是两个变量的值

4. python 中包含哪些数据类型？这些数据类型之间如何转换？

- int	整型 
- float 浮点型
- bool 布尔型

- 转换为整型 int(x)
- 转换为字符串 str(object='')
- 转换为浮点型 float(x)

# 02. 位运算

## 1. 原码、反码和补码

原码：就是其二进制表示（注意，最高位是符号位）。

00 00 00 11 -> 3

10 00 00 11 -> -3

反码：正数的反码就是原码，负数的反码是符号位不变，其余位取反（对应正数按位取反）。

00 00 00 11 -> 3

11 11 11 00 -> -3

补码：正数的补码就是原码，**负数的补码是反码+1。**

00 00 00 11 -> 3

11 11 11 01 -> -3

符号位：最高位为符号位，0表示正数，1表示负数。在位运算中符号位也参与运算


```python
11 << 3
```




    88



00 00 10 11 -> 11

01 01 10 00 -> 88 

### 利用位运算实现快速计算

#### 通过 <<，>> 快速计算2的倍数问题。


```python
n=4;
n << 1
```




    8



计算 n*2


```python
n >> 1
```




    2



计算n/2


```python
1 << n
```




    16



计算2^n

## 练习题：

leetcode 习题 136. 只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

尝试使用位运算解决此题。

题目说明:
"""
Input file
example1: [2,2,1]
example2: [4,1,2,1,2]

Output file
result1: 1
result2: 4
"""

<code>    
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        


        r = 0
        for num in nums:
            r ^= num
        return r
<code/>

由于异或的两个性质
- 任何数与 0 异或都不改变它的值，即 a⊕0=a
- 任何数与其自身异或都为 0，即 a⊕a=0

假设题目中描述的数组为 [a1,a1,a2,a2,…,an,an,ax] ，其中，ax 只出现一次，其余的元素都出现两次。对该数组中的所有元素进行异或运算，结果为ax本身。


