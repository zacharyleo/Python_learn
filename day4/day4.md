# 一、列表

## 1.定义
``` python
语法为 [元素1, 元素2, ..., 元素n]。

关键点是 中括号 []和 逗号 ,
中括号 把所有元素绑在一起
逗号 将每个元素一一分开
```

## 2.创建

- 直接赋值


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(x, type(x))


x = [2, 3, 4, 5, 6, 7]
print(x, type(x))

```

    ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'] <class 'list'>
    [2, 3, 4, 5, 6, 7] <class 'list'>
    

- 利用 list(range())创建列表


```python
x = list(range(10))
print(x, type(x))


x = list(range(1, 11, 2))
print(x, type(x))


x = list(range(10, 1, -2))
print(x, type(x))

```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] <class 'list'>
    [1, 3, 5, 7, 9] <class 'list'>
    [10, 8, 6, 4, 2] <class 'list'>
    

- 利用推导式创建列表


```python
x = [0] * 5
print(x, type(x))


x = [0 for i in range(5)]
print(x, type(x))


x = [i for i in range(10)]
print(x, type(x))


x = [i for i in range(1, 10, 2)]
print(x, type(x))


x = [i for i in range(10, 1, -2)]
print(x, type(x))


x = [i ** 2 for i in range(1, 10)]
print(x, type(x))


x = [i for i in range(100) if (i % 2) != 0 and (i % 3) == 0]
print(x, type(x))


```

    [0, 0, 0, 0, 0] <class 'list'>
    [0, 0, 0, 0, 0] <class 'list'>
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] <class 'list'>
    [1, 3, 5, 7, 9] <class 'list'>
    [10, 8, 6, 4, 2] <class 'list'>
    [1, 4, 9, 16, 25, 36, 49, 64, 81] <class 'list'>
    [3, 9, 15, 21, 27, 33, 39, 45, 51, 57, 63, 69, 75, 81, 87, 93, 99] <class 'list'>
    

- 创建一个 4×3的二维数组


```python
x = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [0, 0, 0]]
print(x, type(x))


for i in x:
    print(i, type(i))


x = [[0 for col in range(3)] for row in range(4)]
print(x, type(x))


x[0][0] = 1
print(x, type(x))


x = [[0] * 3 for row in range(4)]
print(x, type(x))


x[1][1] = 1
print(x, type(x))

```

    [[1, 2, 3], [4, 5, 6], [7, 8, 9], [0, 0, 0]] <class 'list'>
    [1, 2, 3] <class 'list'>
    [4, 5, 6] <class 'list'>
    [7, 8, 9] <class 'list'>
    [0, 0, 0] <class 'list'>
    [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>
    [[1, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>
    [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>
    [[0, 0, 0], [0, 1, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>
    

#### 一个注意
x = [a] * 4操作中，只是创建4个指向list的引用，所以一旦a改变，x中4个a也会随之改变。


```python
a = [0] * 3
x = [a] * 4
print(x, type(x))


x[0][0] = 1
print(x, type(x))

```

    [[0, 0, 0], [0, 0, 0], [0, 0, 0], [0, 0, 0]] <class 'list'>
    [[1, 0, 0], [1, 0, 0], [1, 0, 0], [1, 0, 0]] <class 'list'>
    

可见4个都改变了

- 创建一个混合列表


```python
mix = [1, 'lsgo', 3.14, [1, 2, 3]]
print(mix, type(mix))  

```

    [1, 'lsgo', 3.14, [1, 2, 3]] <class 'list'>
    

- 创建一个空列表，使用 [ ]


```python
empty = []
print(empty, type(empty)) 
```

    [] <class 'list'>
    

## 3.修改列表

列表内容可更改 (mutable)，因此附加 (append, extend)、插入 (insert)、删除 (remove, pop) 这些操作都可以用在它身上。

### 3.1添加元素### 

- 
``` python
list.append(obj) 在列表末尾添加新的对象，只接受一个参数，参数可以是任何数据类型，被追加的元素在 list 中保持着原结构类型。
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.append('Thursday')
print(x)  


print(len(x))  
```

    ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Thursday']
    6
    

``` python
此元素如果是一个 list，那么这个 list 将作为一个整体进行追加
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.append(['Thursday', 'Sunday'])
print(x)  


print(len(x))
```

    ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', ['Thursday', 'Sunday']]
    6
    

- 注意append()和extend()的区别

严格来说 append 是追加，把一个东西整体添加在列表后，而 extend 是扩展，把一个东西里的所有元素添加在列表后。
- 
``` python
list.extend(seq) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）,即使追加一个list，也直接融入原来的list，而不是作为整体，分隔开。
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.extend(['Thursday', 'Sunday'])
print(x)  


print(len(x))
```

    ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Thursday', 'Sunday']
    7
    

- 
``` python
list.insert(index, obj) 在编号 index 位置插入 obj。
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.insert(2, 'Sunday')
print(x)


print(len(x)) 
```

    ['Monday', 'Tuesday', 'Sunday', 'Wednesday', 'Thursday', 'Friday']
    6
    

### 3.2 删除元素

``` python
remove 和 pop 都可以删除元素，
remove是指定具体要删除的元素，是一个命令 list.remove(obj)
pop则可以被赋值，y=list.pop(),为被删除的元素
```

- 
``` python
list.remove(obj) 移除列表中某个值的第一个匹配项
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.remove('Monday')
print(x)
```

    ['Tuesday', 'Wednesday', 'Thursday', 'Friday']
    


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
x.remove('Tuesday')
print(x)
```

    ['Monday', 'Wednesday', 'Thursday', 'Friday']
    

- 
``` python
list.pop([index=-1]) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
y = x.pop()
print(y)  

y = x.pop(0)
print(y)  

y = x.pop(-2) #在前两个删除的基础上，-2指倒数第二个元素，也就是Wednesday
print(y)  
print(x)  
```

    Friday
    Monday
    Wednesday
    ['Tuesday', 'Thursday']
    

- 
``` python
del [var1, var2 ……] 删除单个或多个对象。
```
如果知道要删除的元素在列表中的位置，可使用del语句。


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
del x[0:2]
print(x)  
```

    ['Wednesday', 'Thursday', 'Friday']
    

注意[0:2]只删索引为0、1的两个元素，2的不删除，即不删除尾值

如果要从列表中删除一个元素，且不再以任何方式使用它，就使用del语句；如果你要在删除元素后还能继续使用它，就使用方法pop()。

### 3.3 获取元素

- 
``` python
通过元素的索引值，从列表获取单个元素，注意，列表索引值是从0开始的。
通过将索引指定为-1，可让Python返回最后一个列表元素，索引 -2 返回倒数第二个列表元素，以此类推。
```


```python
x = ['Monday', 'Tuesday', 'Wednesday', ['Thursday', 'Friday']]
print(x[0], type(x[0]))  
print(x[-1], type(x[-1]))  
print(x[-2], type(x[-2]))  
```

    Monday <class 'str'>
    ['Thursday', 'Friday'] <class 'list'>
    Wednesday <class 'str'>
    

- 
``` python
切片的通用写法是 start : stop : step
```
- 情况 1 

"start :"
以 step 为 1 (默认) 从编号 start 往列表尾部切片。


```python
x = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(x[3:])  
print(x[-3:])  
```

    ['Thursday', 'Friday']
    ['Wednesday', 'Thursday', 'Friday']
    

- 情况 2

": stop"
以 step 为 1 (默认) 从列表头部往编号 stop 切片。


```python
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(week[:3])  
print(week[:-3])  
```

    ['Monday', 'Tuesday', 'Wednesday']
    ['Monday', 'Tuesday']
    

注意stop 末尾的所在索引元素不在内

- 情况 3

"start : stop"
以 step 为 1 (默认) 从编号 start 往编号 stop 切片。


```python
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(week[1:3])  
print(week[-3:-1])  
```

    ['Tuesday', 'Wednesday']
    ['Wednesday', 'Thursday']
    

注意stop 末尾的所在索引元素不在内

- 情况 4

"start : stop : step"
以具体的 step 从编号 start 往编号 stop 切片。注意最后把 step 设为 -1，相当于将列表反向排列。


```python
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(week[1:4:2])  
print(week[:4:2])  
print(week[1::2])  
print(week[::-1])  

```

    ['Tuesday', 'Thursday']
    ['Monday', 'Wednesday']
    ['Tuesday', 'Thursday']
    ['Friday', 'Thursday', 'Wednesday', 'Tuesday', 'Monday']
    

- 情况 5

" : "
复制列表中的所有元素（浅拷贝）。


```python
week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
print(week[:])  
```

    ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday']
    

浅拷贝与深拷贝...没搞懂


```python
list1 = [123, 456, 789, 213]
list2 = list1
list3 = list1[:]

print(list2)  
print(list3) 
list1.sort()
print(list2)  
print(list3) 

list1 = [[123, 456], [789, 213]]
list2 = list1
list3 = list1[:]
print(list2)  
print(list3) 
list1[0][0] = 111
print(list2) 
print(list3)  
```

    [123, 456, 789, 213]
    [123, 456, 789, 213]
    [123, 213, 456, 789]
    [123, 456, 789, 213]
    [[123, 456], [789, 213]]
    [[123, 456], [789, 213]]
    [[111, 456], [789, 213]]
    [[111, 456], [789, 213]]
    

### 3.4 常用操作符

等号操作符：==

连接操作符 +

重复操作符 *

成员关系操作符 in、not in

等号 ==，只有成员、成员位置都相同时才返回True。

列表拼接有两种方式，用加号 + 和 乘号 *，前者首尾拼接，后者复制拼接。


```python
list1 = [123, 456]
list2 = [456, 123]
list3 = [123, 456]

print(list1 == list2)  # False
print(list1 == list3)  # True

list4 = list1 + list2  # extend()
print(list4)  # [123, 456, 456, 123]

list5 = list3 * 3
print(list5)  # [123, 456, 123, 456, 123, 456]

list3 *= 3
print(list3)  # [123, 456, 123, 456, 123, 456]

print(123 in list3)  # True
print(456 not in list3)  # False
```

    False
    True
    [123, 456, 456, 123]
    [123, 456, 123, 456, 123, 456]
    [123, 456, 123, 456, 123, 456]
    True
    False
    

前面三种方法（append, extend, insert）可对列表增加元素，它们没有返回值，是直接修改了原数据对象。 而将两个list相加，需要创建新的 list 对象，从而需要消耗额外的内存，特别是当 list 较大时，尽量不要使用 “+” 来添加list。

### 3.5 其它方法

- list.count(obj) 统计某个元素在列表中出现的次数


```python
list1 = [123, 456] * 3
print(list1) 
num = list1.count(123)
print(num)  
```

    [123, 456, 123, 456, 123, 456]
    3
    

- list.index(x, start, end) 从列表中找出某个值第一个匹配项的索引位置


```python
list1 = [123, 456] * 5
print(list1.index(123))  
print(list1.index(123, 1)) 
print(list1.index(123, 3, 7))  
```

    0
    2
    4
    

- list.reverse() 反向列表中元素


```python
x = [123, 456, 789]
x.reverse()
print(x)  
```

    [789, 456, 123]
    

- list.sort(key=None, reverse=False) 对原列表进行排序。

- key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
- reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）。
- 该方法没有返回值，但是会对列表的对象进行排序。


```python
x = [123, 456, 789, 213]
x.sort()
print(x)


x.sort(reverse=True)
print(x)



# 获取列表的第二个元素
def takeSecond(elem):
    return elem[1]


x = [(2, 2), (3, 4), (4, 1), (1, 3)]
x.sort(key=takeSecond)
print(x)


x.sort(key=lambda a: a[0])
print(x)

```

    [123, 213, 456, 789]
    [789, 456, 213, 123]
    [(4, 1), (2, 2), (1, 3), (3, 4)]
    [(1, 3), (2, 2), (3, 4), (4, 1)]
    

## 练习题：

1、列表操作练习

列表lst 内容如下

lst = [2, 5, 6, 7, 8, 9, 2, 9, 9]

请写程序完成下列操作：

1. 在列表的末尾增加元素15
2. 在列表的中间位置插入元素20
3. 将列表[2, 5, 6]合并到lst中
4. 移除列表中索引为3的元素
5. 翻转列表里的所有元素
6. 对列表里的元素进行排序，从小到大一次，从大到小一次


```python
lst=[2, 5, 6, 7, 8, 9, 2, 9, 9]
lst.append(15)  #在列表的末尾增加元素15
print(lst)
lst.insert(round(len(lst)/2),20) #在列表的中间位置插入元素20
print(lst)
lst1 = [2, 5, 6]
lst += lst1    #将列表[2, 5, 6]合并到lst中
print(lst)
lst.pop(3)     #移除列表中索引为3的元素
print(lst)
lst.reverse()  #翻转列表里的所有元素
print(lst)
lst.sort()     #从小到大排序
print(lst)
lst.sort(reverse=True)   #从大到小排序
print(lst)
```

    [2, 5, 6, 7, 8, 9, 2, 9, 9, 15]
    [2, 5, 6, 7, 8, 20, 9, 2, 9, 9, 15]
    [2, 5, 6, 7, 8, 20, 9, 2, 9, 9, 15, 2, 5, 6]
    [2, 5, 6, 8, 20, 9, 2, 9, 9, 15, 2, 5, 6]
    [6, 5, 2, 15, 9, 9, 2, 9, 20, 8, 6, 5, 2]
    [2, 2, 2, 5, 5, 6, 6, 8, 9, 9, 9, 15, 20]
    [20, 15, 9, 9, 9, 8, 6, 6, 5, 5, 2, 2, 2]
    

2、修改列表

问题描述：

lst = [1, [4, 6], True]

请将列表里所有数字修改成原来的两倍


```python
lst = [1, [4, 6], True]
for index, elem in enumerate(lst):
    if isinstance(elem, list):
        for index1, elem1 in enumerate(elem):
            lst[index][index1] = elem1 * 2
    elif isinstance(elem, bool):
        pass
    else:
        lst[index] = elem * 2
print(lst)
# [2, [8, 12], True]
```

    [2, [8, 12], True]
    


```python
# enumerate用法
#组合为一个索引序列，同时列出数据和数据下标
lst= ['a','b','c']
for i in enumerate(lst,start=1):
    print(i)
 
"""
(1, 'a')
(2, 'b')
(3, 'c')
"""
 
```

    (1, 'a')
    (2, 'b')
    (3, 'c')
    




    "\n(1, 'a')\n(2, 'b')\n(3, 'c')\n"



3、leetcode 852题 山脉数组的峰顶索引

如果一个数组k符合下面两个属性，则称之为山脉数组

数组的长度大于等于3

存在$i$，$i$ >0 且$i<\operatorname{len}(k)-1$， 使得$$\mathrm{k}[0]<\mathrm{k}[1]<\ldots<\mathrm{k}[\mathrm{i}-1]<\mathrm{k}[\mathrm{j}]>\mathrm{k}[\mathrm{i}+1] \ldots>\mathrm{k}[\operatorname{len}(\mathrm{k})-1]$$

这个$i$就是顶峰索引。

现在，给定一个山脉数组，求顶峰索引。

示例:

输入：[1, 3, 4, 5, 3]

输出：True

输入：[1, 2, 4, 6, 4, 5]

输出：False


```python
class Solution(object):
    def peakIndexInMountainArray(self, A):
        return A.index(max(A))
lst= [1,3,4,5,3]
lst2 = [1,2,7,6,4,5]
a = Solution()
#a.peakIndexInMountainArray(lst)
a.peakIndexInMountainArray(lst2)    
```




    2



# 二、元组

## 1. 定义

语法为：(元素1, 元素2, ..., 元素n)
- 小括号把所有元素绑在一起
- 逗号将每个元素一一分开

## 2. 创建和访问

- Python 的元组与列表类似，不同之处在于tuple被创建后就不能对其进行修改，类似字符串。
- 元组tuple使用小括号，列表list使用方括号。
- 元组与列表类似，也用整数来对它进行索引 (indexing) 和切片 (slicing)。


```python
t1 = (1, 10.31, 'python')
t2 = 1, 10.31, 'python'
#创建元组可以用小括号 ()，也可以什么都不用，为了可读性，建议还是用 ()。

print(t1, type(t1))
print(t2, type(t2))


tuple1 = (1, 2, 3, 4, 5, 6, 7, 8)
print(tuple1[1])  
print(tuple1[5:])  
print(tuple1[:5])  
tuple2 = tuple1[:]
print(tuple2)  
```

    (1, 10.31, 'python') <class 'tuple'>
    (1, 10.31, 'python') <class 'tuple'>
    2
    (6, 7, 8)
    (1, 2, 3, 4, 5)
    (1, 2, 3, 4, 5, 6, 7, 8)
    


- 元组中只包含一个元素时，需要在元素后面添加逗号，否则括号会被当作运算符使用。


```python
x = (1)
print(type(x))  # <class 'int'>
x = 1, 
print(type(x))  # <class 'tuple'>
x = ()
print(type(x))  # <class 'tuple'>
x = (1,)
print(type(x))  # <class 'tuple'>
x = []
print(type(x))  # <class 'list'>
```

    <class 'int'>
    <class 'tuple'>
    <class 'tuple'>
    <class 'tuple'>
    <class 'list'>
    


```python
print(8 * (8))  
print(8 * (8,))  
```

    64
    (8, 8, 8, 8, 8, 8, 8, 8)
    

- 创建二维元组


```python
x = (1, 10.31, 'python'), ('data', 11)
print(x)
# ((1, 10.31, 'python'), ('data', 11))
print(x[0])
# (1, 10.31, 'python')
print(x[0][0])
# 1 
print(x[0][0:2])
# 不算stop位，也就是只有第1和第2个索引

```

    ((1, 10.31, 'python'), ('data', 11))
    (1, 10.31, 'python')
    1
    (1, 10.31)
    

## 3. 更新和删除


```python
week = ('Monday', 'Tuesday', 'Thursday', 'Friday')
week = week[:2] + ('Wednesday',) + week[2:]
print(week)  
```

    ('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')
    

第2个和第3个之间插入新元素

- 元组有不可更改 (immutable) 的性质，因此不能直接给元组的元素赋值，但是只要元组中的元素可更改 (mutable)，那么我们可以直接更改其元素，注意这跟赋值其元素不同。


```python
t1 = (1, 2, 3, [4, 5, 6])
print(t1)  

t1[3][0] = 9
print(t1)  
```

    (1, 2, 3, [4, 5, 6])
    (1, 2, 3, [9, 5, 6])
    

## 4. 元组相关的操作符

- 等号操作符：==
- 连接操作符 +
- 重复操作符 *
- 成员关系操作符 in、not in

「等号 ==」，只有成员、成员位置都相同时才返回True。

元组拼接有两种方式，用「加号 +」和「乘号 *」，前者首尾拼接，后者复制拼接。


```python
t1 = (123, 456)
t2 = (456, 123)
t3 = (123, 456)

print(t1 == t2)  
print(t1 == t3)  

t4 = t1 + t2
print(t4)  

t5 = t3 * 3
print(t5)  

t3 *= 3
print(t3)  

print(123 in t3)  
print(456 not in t3)  
```

    False
    True
    (123, 456, 456, 123)
    (123, 456, 123, 456, 123, 456)
    (123, 456, 123, 456, 123, 456)
    True
    False
    

## 5. 内置方法

元组大小和内容都不可更改，因此只有 count 和 index 两种方法。


```python
t = (1, 10.31, 'python')
print(t.count('python'))   
print(t.index('python'))  
```

    1
    2
    

- count('python') 是记录在元组 t 中该元素出现几次，显然是 1 次
- index(10.31) 是找到该元素在元组 t 的索引，显然是 2

## 6.  解压元组

- 解压（unpack）一维元组（有几个元素左边括号定义几个变量）


```python
t = (1, 10.31, 'python')
(a, b, c) = t
print(a, b, c)
```

    1 10.31 python
    

- 解压二维元组（按照元组里的元组结构来定义变量）


```python
t = (1, 10.31, ('OK', 'python'))
(a, b, (c, d)) = t
print(a, b, c, d)
```

    1 10.31 OK python
    

- 如果只想要元组其中几个元素，用通配符「*」，英文叫 wildcard，在计算机语言中代表一个或多个元素。下例就是把多个元素丢给了 rest 变量。


```python
t = 1, 2, 3, 4, 5
a, b, *rest, c = t
print(a, b, c) 
print(rest) 
print(*rest)

```

    1 2 5
    [3, 4]
    3 4
    

*rest 就代表去除掉a,b,c匹配的1,2,5 之后，剩下的元素

也可以用通配符「*」加上下划线「_」


```python
t = 1, 2, 3, 4, 5
a, b, *_ = t
print(a, b)  
print(_)
print(*_)
```

    1 2
    [3, 4, 5]
    3 4 5
    

或许*也表示解码？


## 练习题：

1、元组概念

写出下面代码的执行结果和最终结果的类型

(1, 2)*2

(1, )*2

(1)*2

分析为什么会出现这样的结果.


```python
a = (1, 2)*2

b = (1, )*2

c = (1)*2

print(type(a))
print(type(b))
print(type(c))
```

    <class 'tuple'>
    <class 'tuple'>
    <class 'int'>
    

因为a是标准元组
b和c是因为对于单个元素  有逗号，表示此为元组，五逗号，将被是为数据类型

2、 拆包过程是什么？

a, b = 1, 2
上述过程属于拆包吗？

可迭代对象拆包时，怎么赋值给占位符？

拆包就是将序列中的元素拆成一个一个数据的过程，如：去掉元组、列表、字典直接获取元素的过程。

上述过程不属于拆包

上述是以拆包的形式定义变量，给变量赋值。


在变量的前面加上通配符*

# 三、 字符串

## 1. 定义

- Python 中字符串被定义为引号之间的字符集合。
- Python 支持使用成对的 单引号'' 或 双引号""。


```python
t1 = 'i love Python!'
print(t1, type(t1))


t2 = "I love Python!"
print(t2, type(t2))


print(5 + 8)  
print('5' + '8')  
```

    i love Python! <class 'str'>
    I love Python! <class 'str'>
    13
    58
    

- 常用转义字符

\\	反斜杠符号

\'	单引号

\"	双引号

\n	换行

\t	横向制表符(TAB)

\r	回车

- 如果字符串中需要出现单引号或双引号，可以使用转义符号\对字符串中的符号进行转义。


```python
print('let\'s go')  # let's go
print("let's go")  # let's go
print('C:\\now')  # C:\now
print("C:\\Program Files\\Intel\\Wifi\\Help")
```

    let's go
    let's go
    C:\now
    C:\Program Files\Intel\Wifi\Help
    

- 三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。


```python
para_str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
"""
print(para_str)


para_str = '''这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
'''
print(para_str)

```

    这是一个多行字符串的实例
    多行字符串可以使用制表符
    TAB ( 	 )。
    也可以使用换行符 [ 
     ]。
    
    这是一个多行字符串的实例
    多行字符串可以使用制表符
    TAB ( 	 )。
    也可以使用换行符 [ 
     ]。
    
    

## 2. 切片与拼接

- 类似于元组具有不可修改性
- 从 0 开始 (和 Java 一样)
- 切片通常写成 start:end 这种形式，包括「start 索引」对应的元素，不包括「end索引」对应的元素。
- 索引值可正可负，正索引从 0 开始，从左往右；负索引从 -1 开始，从右往左。
- 使用负数索引时，会从最后一个元素开始计数。最后一个元素的位置编号是 -1。


```python
str1 = 'I Love LsgoGroup'
print(str1[:6])  # I Love
print(str1[5])  # e
print(str1[:6] + " 中间插入的字符串 " + str1[6:])  


s = 'Python'
print(s)  
print(s[2:4]) 
print(s[-5:-2])  
print(s[2])  
print(s[-1])  
```

    I Love
    e
    I Love 中间插入的字符串  LsgoGroup
    Python
    th
    yth
    t
    n
    

## 3. 常用内置方法

- capitalize() 将字符串的第一个字符转换为大写。


```python
str2 = 'xiaoxie'
print(str2.capitalize())  
```

    Xiaoxie
    

- lower() 转换字符串中所有大写字符为小写。
- upper() 转换字符串中的小写字母为大写。
- swapcase() 将字符串中大写转换为小写，小写转换为大写。


```python
str2 = "DAXIExiaoxie"
print(str2.lower())  
print(str2.upper())  
print(str2.swapcase())  
```

    daxiexiaoxie
    DAXIEXIAOXIE
    daxieXIAOXIE
    

- count(str, beg= 0,end=len(string)) 返回str在 string 里面出现的次数，如果beg或者end指定则返回指定范围内str出现的次数。


```python
str2 = "DAXIExiaoxie"
print(str2.count('xi'))  
```

    2
    

- endswith(suffix, beg=0, end=len(string)) 检查字符串是否以指定子字符串 suffix 结束，如果是，返回 True，否则返回 False。如果 beg 和 end 指定值，则在指定范围内检查。
- startswith(substr, beg=0,end=len(string)) 检查字符串是否以指定子字符串 substr 开头，如果是，返回 True，否则返回 False。如果 beg 和 end 指定值，则在指定范围内检查。


```python
str2 = "DAXIExiaoxie"
print(str2.endswith('ie'))  # True
print(str2.endswith('xi'))  # False
print(str2.startswith('Da'))  # False
print(str2.startswith('DA'))  # True
```

    True
    False
    False
    True
    

## 4. 格式化

- format 格式化函数


```python
str8 = "{0} Love {1}".format('I', 'Lsgogroup')  # 位置参数
print(str8)  

str8 = "{a} Love {b}".format(a='I', b='Lsgogroup')  # 关键字参数
print(str8)  

str8 = "{0} Love {b}".format('I', b='Lsgogroup')  # 位置参数要在关键字参数之前
print(str8)  

str8 = '{0:.2f}{1}'.format(27.658, 'GB')  # 保留小数点后两位
print(str8) 
```

    I Love Lsgogroup
    I Love Lsgogroup
    I Love Lsgogroup
    27.66GB
    

- 格式化符号

%c	格式化字符及其ASCII码

%s	格式化字符串，用str()方法处理对象

%r	格式化字符串，用rper()方法处理对象

%d	格式化整数

%o	格式化无符号八进制数

%x	格式化无符号十六进制数

%X	格式化无符号十六进制数（大写）

%f	格式化浮点数字，可指定小数点后的精度

%e	用科学计数法格式化浮点数

%E	作用同%e，用科学计数法格式化浮点数

%g	根据值的大小决定使用%f或%e

%G	作用同%g，根据值的大小决定使用%f或%E


```python
print('%c' % 97)  # a
print('%c %c %c' % (97, 98, 99))  # a b c
print('%d + %d = %d' % (4, 5, 9))  # 4 + 5 = 9
print("我叫 %s 今年 %d 岁!" % ('小明', 10))  # 我叫 小明 今年 10 岁!
print('%o' % 10)  # 12
print('%x' % 10)  # a
print('%X' % 10)  # A
print('%f' % 27.658)  # 27.658000
print('%e' % 27.658)  # 2.765800e+01
print('%E' % 27.658)  # 2.765800E+01
print('%g' % 27.658)  # 27.658
text = "I am %d years old." % 22
print("I said: %s." % text)  # I said: I am 22 years old..
print("I said: %r." % text)  # I said: 'I am 22 years old.'
```

    a
    a b c
    4 + 5 = 9
    我叫 小明 今年 10 岁!
    12
    a
    A
    27.658000
    2.765800e+01
    2.765800E+01
    27.658
    I said: I am 22 years old..
    I said: 'I am 22 years old.'.
    

- 格式化操作符辅助指令

m.n	m 是显示的最小总宽度,n 是小数点后的位数（如果可用的话）

-用作左对齐

+在正数前面显示加号( + )

#在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')

0显示的数字前面填充'0'而不是默认的空格



```python
print('%5.1f' % 27.658)  # ' 27.7'
print('%.2e' % 27.658)  # 2.77e+01
print('%10d' % 10)  # '        10'
print('%-10d' % 10)  # '10        '
print('%+d' % 10)  # +10
print('%#o' % 10)  # 0o12
print('%#x' % 108)  # 0x6c
print('%010d' % 5)  # 0000000005
```

     27.7
    2.77e+01
            10
    10        
    +10
    0o12
    0x6c
    0000000005
    

# 练习题：

1、字符串函数回顾


- 怎么批量替换字符串中的元素？

replce()
- 怎么把字符串按照空格进⾏拆分？

split(" ")
- 怎么去除字符串⾸位的空格？

lstrip()

2、 实现isdigit函数

题目要求

实现函数isdigit， 判断字符串里是否只包含数字0~9




```python
def isdigit(string):
    if string.isnumeric():
        flag = True
    else:
        flag = False
    return flag

input_data = input("请输入：")
flag = isdigit(input_data)
print(flag)
```

    请输入：10
    True
    

3、leetcode 5题 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例:

输入: "babad"

输出: "bab"

输入: "cbbd"

输出: "bb"


```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        l = len(s)
        maxlength = 0
        maxstr = ''
        for i in range(l):
            for j in range(i+1,l+1):
                temp =s[i:j] 
                if temp == temp[::-1] and j-i > maxlength:
                    maxstr = s[i:j]
                    maxlength = j-i
        return maxstr


```
