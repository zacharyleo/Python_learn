# 一、字典

## 1. 可变类型与不可变类型

- 序列是以连续的整数为索引，与此不同的是，字典以"关键字"为索引，关键字可以是任意不可变类型，通常用字符串或数值。
- 字典是 Python 唯一的一个 映射类型，字符串、元组、列表属于序列类型。

判断一个数据类型 X 是不是可变类型有两种方法：

- 麻烦方法：用 id(X) 函数，对 X 进行某种操作，比较操作前后的 id，如果不一样，则 X 不可变，如果一样，则 X 可变。
- 便捷方法：用 hash(X)，只要不报错，证明 X 可被哈希，即不可变，反过来不可被哈希，即可变。


```python

i = 1
print(id(i))  # 140732167000896

i = i + 2
print(id(i))  # 140732167000960

l = [1, 2]
print(id(l))  # 4300825160
l.append('Python')
print(id(l))  # 4300825160

```

    140712870453648
    140712870453712
    1957660551368
    1957660551368
    

- 整数 i 在加 1 之后的 id 和之前不一样，因此加完之后的这个 i (虽然名字没变)，但不是加之前的那个 i 了，因此整数是不可变类型。
- 列表 l 在附加 'Python' 之后的 id 和之前一样，因此列表是可变类型。


```python
print(hash('Name'))  # -9215951442099718823

print(hash((1, 2, 'Python')))  # 823362308207799471

print(hash([1, 2, 'Python']))
# TypeError: unhashable type: 'list'

print(hash({1, 2, 3}))
# TypeError: unhashable type: 'set'
```

    -1079747040041844027
    7214583587858808257
    


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-2-74ebb8223a13> in <module>
          3 print(hash((1, 2, 'Python')))  # 823362308207799471
          4 
    ----> 5 print(hash([1, 2, 'Python']))
          6 # TypeError: unhashable type: 'list'
          7 
    

    TypeError: unhashable type: 'list'


- 数值、字符和元组 都能被哈希，因此它们是不可变类型。
- 列表、集合、字典不能被哈希，因此它是可变类型。

## 2. 定义

字典 是无序的 键:值（key:value）对集合，键必须是互不相同的（在同一个字典之内）。

- dict 内部存放的顺序和 key 放入的顺序是没有关系的。
- dict 查找和插入的速度极快，不会随着 key 的增加而增加，但是需要占用大量的内存。

字典 定义语法为 {元素1, 元素2, ..., 元素n}

- 其中每一个元素是一个「键值对」-- 键:值 (key:value)
- 关键点是「大括号 {}」,「逗号 ,」和「冒号 :」
- 大括号 -- 把所有元素绑在一起
- 逗号 -- 将每个键值对分开
- 冒号 -- 将键和值分开

## 3. 创建和访问


```python
brand = ['李宁', '耐克', '阿迪达斯']
slogan = ['一切皆有可能', 'Just do it', 'Impossible is nothing']
print('耐克的口号是:', slogan[brand.index('耐克')])  
# 耐克的口号是: Just do it

dic = {'李宁': '一切皆有可能', '耐克': 'Just do it', '阿迪达斯': 'Impossible is nothing'}
print('耐克的口号是:', dic['耐克'])  
# 耐克的口号是: Just do it
```

    耐克的口号是: Just do it
    耐克的口号是: Just do it
    

- 通过字符串或数值作为key来创建字典。


```python
dic1 = {1: 'one', 2: 'two', 3: 'three'}
print(dic1)  
print(dic1[1])  
print(dic1[3])  

dic2 = {'rice': 35, 'wheat': 101, 'corn': 67}
print(dic2)
print(dic2['rice'])  
```

    {1: 'one', 2: 'two', 3: 'three'}
    one
    three
    {'rice': 35, 'wheat': 101, 'corn': 67}
    35
    

- 通过构造函数dict来创建字典。
dict() 创建一个空的字典。
- 通过key直接把数据放入字典中，但一个key只能对应一个value，多次对一个key放入 value，后面的值会把前面的值冲掉。


```python
dic = dict()
dic['a'] = 1
dic['b'] = 2
dic['c'] = 3

print(dic)
# {'a': 1, 'b': 2, 'c': 3}

dic['a'] = 11
print(dic)
# {'a': 11, 'b': 2, 'c': 3}

dic['d'] = 4
print(dic)
# {'a': 11, 'b': 2, 'c': 3, 'd': 4}
```

    {'a': 1, 'b': 2, 'c': 3}
    {'a': 11, 'b': 2, 'c': 3}
    {'a': 11, 'b': 2, 'c': 3, 'd': 4}
    

## 4. 内置方法

- dict.fromkeys(seq[, value]) 用于创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值。


```python
seq = ('name', 'age', 'sex')
dic1 = dict.fromkeys(seq)
print(dic1)


dic2 = dict.fromkeys(seq, 10)
print(dic2)


dic3 = dict.fromkeys(seq, ('小马', '8', '男'))
print(dic3)

```

    {'name': None, 'age': None, 'sex': None}
    {'name': 10, 'age': 10, 'sex': 10}
    {'name': ('小马', '8', '男'), 'age': ('小马', '8', '男'), 'sex': ('小马', '8', '男')}
    

- dict.keys()返回一个可迭代对象，可以使用 list() 来转换为列表，列表为字典中的所有键。


```python
dic = {'Name': 'lsgogroup', 'Age': 7}
print(dic.keys()) 
lst = list(dic.keys())  
print(lst) 
```

    dict_keys(['Name', 'Age'])
    ['Name', 'Age']
    

- dict.values()返回一个迭代器，可以使用 list() 来转换为列表，列表为字典中的所有值。


```python
dic = {'Sex': 'female', 'Age': 7, 'Name': 'Zara'}
print(dic.values())


print(list(dic.values()))

```

    dict_values(['female', 7, 'Zara'])
    ['female', 7, 'Zara']
    

- dict.items()以列表返回可遍历的 (键, 值) 元组数组。


```python
dic = {'Name': 'Lsgogroup', 'Age': 7}
print(dic.items())


print(tuple(dic.items()))


print(list(dic.items()))

```

    dict_items([('Name', 'Lsgogroup'), ('Age', 7)])
    (('Name', 'Lsgogroup'), ('Age', 7))
    [('Name', 'Lsgogroup'), ('Age', 7)]
    

- key in dict in 操作符用于判断键是否存在于字典中，如果键在字典 dict 里返回true，否则返回false。而not in操作符刚好相反，如果键在字典 dict 里返回false，否则返回true。


```python
dic = {'Name': 'Lsgogroup', 'Age': 7}

# in 检测键 Age 是否存在
if 'Age' in dic:
    print("键 Age 存在")
else:
    print("键 Age 不存在")

# 检测键 Sex 是否存在
if 'Sex' in dic:
    print("键 Sex 存在")
else:
    print("键 Sex 不存在")

# not in 检测键 Age 是否存在
if 'Age' not in dic:
    print("键 Age 不存在")
else:
    print("键 Age 存在")

```

    键 Age 存在
    键 Sex 不存在
    键 Age 存在
    

- dict.pop(key[,default])删除字典给定键 key 所对应的值，返回值为被删除的值。key 值必须给出。若key不存在，则返回 default 值。
- del dict[key] 删除字典给定键 key 所对应的值。


```python
dic1 = {1: "a", 2: [1, 2]}
print(dic1.pop(1), dic1)  # a {2: [1, 2]}


print(dic1.pop(3, "nokey"), dic1)  # nokey {2: [1, 2]}

del dic1[2]
print(dic1) 
```

    a {2: [1, 2]}
    nokey {2: [1, 2]}
    {}
    

- 直接赋值和 copy 的区别


```python
dic1 = {'user': 'lsgogroup', 'num': [1, 2, 3]}


dic2 = dic1  

dic3 = dic1.copy()  

print(id(dic1)) 
print(id(dic2)) 
print(id(dic3)) 


dic1['user'] = 'root'
dic1['num'].remove(1)


print(dic1)  # {'user': 'root', 'num': [2, 3]}
print(dic2)  # {'user': 'root', 'num': [2, 3]}
print(dic3)  # {'user': 'runoob', 'num': [2, 3]}
```

    2567489824392
    2567489824392
    2567489824312
    {'user': 'root', 'num': [2, 3]}
    {'user': 'root', 'num': [2, 3]}
    {'user': 'lsgogroup', 'num': [2, 3]}
    

## 5. 练习题：

``` python
1. 字典内容如下:

dic = {
    'python': 95,
    'java': 99,
    'c': 100
    }
```

- 字典的长度是多少

print(len(list(dic.keys())))
- 请修改'java' 这个key对应的value值为98

dic['java'] = 98
- 删除 c 这个key

1.使用del直接删除元素

del dic['c']

print(dic)

2.使用dict的内置方法pop,删除并可获得删除的值

c = dic.pop('c')

print(dic,c)

- 增加一个key-value对，key值为 php, value是90

dic['PHP']=90

print(dic)
 
dic2 = {'PHP':90}

dic.update(dic2)


print(dic)

- 获取所有的key值，存储在列表里
- 获取所有的value值，存储在列表里
- 判断 javascript 是否在字典中
- 获得字典里所有value 的和
- 获取字典里最大的value
- 获取字典里最小的value
- 字典 dic1 = {'php': 97}， 将dic1的数据更新到dic中


```python
dic = {'python': 95, 'java': 99, 'c': 100}
print(len(dic))
dic['java'] = 98
print(dic)
del dic['c']
print(dic)
dic.setdefault('php', 90)
print(dic)
lst1 = list(dic.keys())
print(lst1)
lst2 = list(dic.values())
print(lst2)
print('javascript' in dic)
print(sum(lst2))
print(max(lst2))
print(min(lst2))
dic1 = {'php': 97}
dic.update(dic1)
print(dic)
```

    3
    {'python': 95, 'java': 98, 'c': 100}
    {'python': 95, 'java': 98}
    {'python': 95, 'java': 98, 'php': 90}
    ['python', 'java', 'php']
    [95, 98, 90]
    False
    283
    98
    90
    {'python': 95, 'java': 98, 'php': 97}
    

2. 字典中的value

有一个字典，保存的是学生各个编程语言的成绩，内容如下

各门课程的考试成绩存储方式并不相同，有的用字典，有的用列表，但是分数都是字符串类型，请实现函数transfer_score(score_dict)，将分数修改成int类型


```python

def transfer_score(x):
    x['python']['上学期'] = int(x['python']['上学期'])
    x['python']['下学期'] = int(x['python']['下学期'])
    for i in range(len(x['c++'])):
        x['c++'][i] = int(data['c++'][i])
    x['java'][0]['月考'] = int(x['java'][0]['月考'])
    x['java'][0]['期中考试'] = int(x['java'][0]['期中考试'])
    x['java'][0]['期末考试'] = int(x['java'][0]['期末考试'])
    return x
data = {
        'python': {'上学期': '90', '下学期': '95'},
        'c++': ['95', '96', '97'],
        'java': [{'月考':'90', '期中考试': '94', '期末考试': '98'}]
        }
print(transfer_score(data))
```

    {'python': {'上学期': 90, '下学期': 95}, 'c++': [95, 96, 97], 'java': [{'月考': 90, '期中考试': 94, '期末考试': 98}]}
    

## 二、集合

Python 中set与dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

注意，key为不可变类型，即可哈希的值。


```python
num = {}
print(type(num))  # <class 'dict'>
num = {1, 2, 3, 4}
print(type(num))  # <class 'set'>

```

    <class 'dict'>
    <class 'set'>
    

## 1. 创建

- 先创建对象再加入元素。
- 在创建空集合的时候只能使用s = set()，因为s = {}创建的是空字典。


```python
basket = set()
basket.add('apple')
basket.add('banana')
print(basket) 
```

    {'apple', 'banana'}
    

- 直接把一堆元素用花括号括起来{元素1, 元素2, ..., 元素n}。
- 重复元素在set中会被自动被过滤。


```python
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket)  
```

    {'apple', 'orange', 'banana', 'pear'}
    

- 使用set(value)工厂函数，把列表或元组转换成集合。


```python
a = set('abracadabra')
print(a)  


b = set(("Google", "Lsgogroup", "Taobao", "Taobao"))
print(b)  


c = set(["Google", "Lsgogroup", "Taobao", "Google"])
print(c)  

```

    {'a', 'r', 'b', 'd', 'c'}
    {'Lsgogroup', 'Taobao', 'Google'}
    {'Lsgogroup', 'Taobao', 'Google'}
    

- 去掉列表中重复的元素


```python
lst = [0, 1, 2, 3, 4, 5, 5, 3, 1]

temp = []
for item in lst:
    if item not in temp:
        temp.append(item)

print(temp)  
a = set(lst)
print(list(a))  
```

    [0, 1, 2, 3, 4, 5]
    [0, 1, 2, 3, 4, 5]
    

## 2. 访问集合中的值

- 可以使用len()內建函数得到集合的大小。


```python
s = set(['Google', 'Baidu', 'Taobao'])
print(len(s)) 
```

    3
    

- 可以使用for把集合中的数据一个个读取出来。


```python
s = set(['Google', 'Baidu', 'Taobao'])
for item in s:
    print(item)

```

    Baidu
    Taobao
    Google
    

## 3. 内置方法

- set.add(elmnt)用于给集合添加元素，如果添加的元素在集合中已存在，则不执行任何操作。


```python
fruits = {"apple", "banana", "cherry"}
fruits.add("orange")
print(fruits)  


fruits.add("apple")
print(fruits)  

```

    {'apple', 'banana', 'orange', 'cherry'}
    {'apple', 'banana', 'orange', 'cherry'}
    

- set.update(set)用于修改当前集合，可以添加新的元素或集合到当前集合中，如果添加的元素在集合中已存在，则该元素只会出现一次，重复的会忽略。


```python
x = {"apple", "banana", "cherry"}
y = {"google", "baidu", "apple"}
x.update(y)
print(x)


y.update(["lsgo", "dreamtech"])
print(y)

```

    {'banana', 'baidu', 'google', 'cherry', 'apple'}
    {'baidu', 'google', 'dreamtech', 'lsgo', 'apple'}
    

- set.remove(item) 用于移除集合中的指定元素。如果元素不存在，则会发生错误。


```python
fruits = {"apple", "banana", "cherry"}
fruits.remove("banana")
print(fruits)  
```

    {'apple', 'cherry'}
    

- set.discard(value) 用于移除指定的集合元素。remove() 方法在移除一个不存在的元素时会发生错误，而 discard() 方法不会。


```python
fruits = {"apple", "banana", "cherry"}
fruits.discard("banana")
print(fruits)  # {'apple', 'cherry'}
```

    {'apple', 'cherry'}
    

由于 set 是无序和无重复元素的集合，所以两个或多个 set 可以做数学意义上的集合操作。

- set.intersection(set1, set2) 返回两个集合的交集。
- set1 & set2 返回两个集合的交集。
- set.intersection_update(set1, set2) 交集，在原始的集合上移除不重叠的元素。


```python
a = set('abracadabra')
b = set('alacazam')
print(a)  # {'r', 'a', 'c', 'b', 'd'}
print(b)  # {'c', 'a', 'l', 'm', 'z'}

c = a.intersection(b)
print(c)  # {'a', 'c'}
print(a & b)  # {'c', 'a'}
print(a)  # {'a', 'r', 'c', 'b', 'd'}

a.intersection_update(b)
print(a)  # {'a', 'c'}
```

    {'a', 'r', 'b', 'd', 'c'}
    {'a', 'z', 'm', 'l', 'c'}
    {'a', 'c'}
    {'a', 'c'}
    {'a', 'r', 'b', 'd', 'c'}
    {'a', 'c'}
    

- set.union(set1, set2) 返回两个集合的并集。
- set1 | set2 返回两个集合的并集。


```python
a = set('abracadabra')
b = set('alacazam')
print(a)  # {'r', 'a', 'c', 'b', 'd'}
print(b)  # {'c', 'a', 'l', 'm', 'z'}

print(a | b)  
# {'l', 'd', 'm', 'b', 'a', 'r', 'z', 'c'}

c = a.union(b)
print(c)  
# {'c', 'a', 'd', 'm', 'r', 'b', 'z', 'l'}
```

    {'a', 'r', 'b', 'd', 'c'}
    {'a', 'z', 'm', 'l', 'c'}
    {'a', 'r', 'z', 'l', 'b', 'm', 'd', 'c'}
    {'a', 'r', 'z', 'l', 'b', 'm', 'd', 'c'}
    

- set.difference(set) 返回集合的差集。
- set1 - set2 返回集合的差集。
- set.difference_update(set) 集合的差集，直接在原来的集合中移除元素，没有返回值。


```python
a = set('abracadabra')
b = set('alacazam')
print(a)  # {'r', 'a', 'c', 'b', 'd'}
print(b)  # {'c', 'a', 'l', 'm', 'z'}

c = a.difference(b)
print(c)  # {'b', 'd', 'r'}
print(a - b)  # {'d', 'b', 'r'}

print(a)  # {'r', 'd', 'c', 'a', 'b'}
a.difference_update(b)
print(a)  # {'d', 'r', 'b'}
```

    {'a', 'r', 'b', 'd', 'c'}
    {'a', 'z', 'm', 'l', 'c'}
    {'r', 'd', 'b'}
    {'r', 'd', 'b'}
    {'a', 'r', 'b', 'd', 'c'}
    {'r', 'b', 'd'}
    

- set.symmetric_difference(set)返回集合的异或。
- set1 ^ set2 返回集合的异或。
- set.symmetric_difference_update(set)移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。


```python
a = set('abracadabra')
b = set('alacazam')
print(a)  # {'r', 'a', 'c', 'b', 'd'}
print(b)  # {'c', 'a', 'l', 'm', 'z'}

c = a.symmetric_difference(b)
print(c)  # {'m', 'r', 'l', 'b', 'z', 'd'}
print(a ^ b)  # {'m', 'r', 'l', 'b', 'z', 'd'}

print(a)  # {'r', 'd', 'c', 'a', 'b'}
a.symmetric_difference_update(b)
print(a)  # {'r', 'b', 'm', 'l', 'z', 'd'}
```

    {'a', 'r', 'b', 'd', 'c'}
    {'a', 'z', 'm', 'l', 'c'}
    {'b', 'm', 'r', 'l', 'z', 'd'}
    {'b', 'm', 'r', 'l', 'z', 'd'}
    {'a', 'r', 'b', 'd', 'c'}
    {'r', 'z', 'l', 'b', 'm', 'd'}
    

- set.issubset(set)判断集合是不是被其他集合包含，如果是则返回 True，否则返回 False。
- set1 <= set2 判断集合是不是被其他集合包含，如果是则返回 True，否则返回 False。


```python
x = {"a", "b", "c"}
y = {"f", "e", "d", "c", "b", "a"}
z = x.issubset(y)
print(z)  # True
print(x <= y)  # True

x = {"a", "b", "c"}
y = {"f", "e", "d", "c", "b"}
z = x.issubset(y)
print(z)  # False
print(x <= y)  # False
```

    True
    True
    False
    False
    

- set.issuperset(set)用于判断集合是不是包含其他集合，如果是则返回 True，否则返回 False。
- set1 >= set2 判断集合是不是包含其他集合，如果是则返回 True，否则返回 False。


```python
x = {"f", "e", "d", "c", "b", "a"}
y = {"a", "b", "c"}
z = x.issuperset(y)
print(z)  # True
print(x >= y)  # True

x = {"f", "e", "d", "c", "b"}
y = {"a", "b", "c"}
z = x.issuperset(y)
print(z)  # False
print(x >= y)  # False
```

    True
    True
    False
    False
    

- set.isdisjoint(set) 用于判断两个集合是不是不相交，如果是返回 True，否则返回 False。


```python
x = {"f", "e", "d", "c", "b"}
y = {"a", "b", "c"}
z = x.isdisjoint(y)
print(z)  # False

x = {"f", "e", "d", "m", "g"}
y = {"a", "b", "c"}
z = x.isdisjoint(y)
print(z)  # True
```

    False
    True
    

## 4.集合的转换


```python
se = set(range(4))
li = list(se)
tu = tuple(se)

print(se, type(se))  # {0, 1, 2, 3} <class 'set'>
print(li, type(li))  # [0, 1, 2, 3] <class 'list'>
print(tu, type(tu))  # (0, 1, 2, 3) <class 'tuple'>
```

    {0, 1, 2, 3} <class 'set'>
    [0, 1, 2, 3] <class 'list'>
    (0, 1, 2, 3) <class 'tuple'>
    

## 5. 不可变集合

Python 提供了不能改变元素的集合的实现版本，即不能增加或删除元素，类型名叫frozenset。需要注意的是frozenset仍然可以进行集合操作，只是不能用带有update的方法。

- frozenset([iterable]) 返回一个冻结的集合，冻结后集合不能再添加或删除任何元素。


```python
a = frozenset(range(10))  # 生成一个新的不可变集合
print(a)  
# frozenset({0, 1, 2, 3, 4, 5, 6, 7, 8, 9})

b = frozenset('lsgogroup')
print(b)  
# frozenset({'g', 's', 'p', 'r', 'u', 'o', 'l'})
```

    frozenset({0, 1, 2, 3, 4, 5, 6, 7, 8, 9})
    frozenset({'r', 'p', 'o', 'g', 's', 'u', 'l'})
    

## 练习题：

1. 怎么表示只包含⼀个数字1的元组。


```python
s = (1,)
print(s)
```

    (1,)
    

2. 创建一个空集合，增加 {‘x’,‘y’,‘z’} 三个元素。


```python
s = set()
s.add('x')
s.add('y')
s.add('z')
print(s)
```

    {'z', 'y', 'x'}
    

3. 列表['A', 'B', 'A', 'B']去重。


```python
a = ['A', 'B', 'A', 'B']
a = list(set(a))
print(a)
```

    ['B', 'A']
    

4. 求两个集合{6, 7, 8}，{7, 8, 9}中不重复的元素（差集指的是两个集合交集外的部分）。


```python
e={6,7,8}
f={7,8,9}
e1=set(e)
f1=set(f)
g=(e1|f1)-(e1&f1)
print(g)
```

    {9, 6}
    

5. 求{'A', 'B', 'C'}中元素在 {'B', 'C', 'D'}中出现的次数。


```python
dic1={'A','B','C'}
dic2={'B','C','D'}
set1=list(dic1)
set2=list(dic2)
for i in range(0,len(set1)):
    count=0
    if set1[i] in set2:
        count+=1
    print(set1[i],'在第二个集合中出现的次数为',count)
    continue
```

    C 在第二个集合中出现的次数为 1
    B 在第二个集合中出现的次数为 1
    A 在第二个集合中出现的次数为 0
    

# 三、序列

在 Python 中，序列类型包括字符串、列表、元组、集合和字典，这些序列支持一些通用的操作，但比较特殊的是，集合和字典不支持索引、切片、相加和相乘操作。

## 1. 针对序列的内置函数

- list(sub) 把一个可迭代对象转换为列表。


```python
a = list()
print(a)  

b = 'I Love LsgoGroup'
b = list(b)
print(b)  
# ['I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p']

c = (1, 1, 2, 3, 5, 8)
c = list(c)
print(c)  # [1, 1, 2, 3, 5, 8]
```

    []
    ['I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p']
    [1, 1, 2, 3, 5, 8]
    

- tuple(sub) 把一个可迭代对象转换为元组。


```python
a = tuple()
print(a)  # ()

b = 'I Love LsgoGroup'
b = tuple(b)
print(b)  
# ('I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p')

c = [1, 1, 2, 3, 5, 8]
c = tuple(c)
print(c)  # (1, 1, 2, 3, 5, 8)
```

    ()
    ('I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p')
    (1, 1, 2, 3, 5, 8)
    

- str(obj) 把obj对象转换为字符串


```python
a = 123
a = str(a)
print(a)  # 123
```

    123
    

- len(s) 返回对象（字符、列表、元组等）长度或元素个数。
  -  s对象。


```python
a = list()
print(len(a))  # 0

b = ('I', ' ', 'L', 'o', 'v', 'e', ' ', 'L', 's', 'g', 'o', 'G', 'r', 'o', 'u', 'p')
print(len(b))  # 16

c = 'I Love LsgoGroup'
print(len(c))  # 16
```

    0
    16
    16
    

- max(sub)返回序列或者参数集合中的最大值


```python
print(max(1, 2, 3, 4, 5))  # 5
print(max([-8, 99, 3, 7, 83]))  # 99
print(max('IloveLsgoGroup'))  # v
```

    5
    99
    v
    

- min(sub)返回序列或参数集合中的最小值


```python
print(min(1, 2, 3, 4, 5))  # 1
print(min([-8, 99, 3, 7, 83]))  # -8
print(min('IloveLsgoGroup'))  # G
```

    1
    -8
    G
    

- sum(iterable[, start=0]) 返回序列iterable与可选参数start的总和。


```python
print(sum([1, 3, 5, 7, 9]))  # 25
print(sum([1, 3, 5, 7, 9], 10))  # 35
print(sum((1, 3, 5, 7, 9)))  # 25
print(sum((1, 3, 5, 7, 9), 20))  # 45
```

    25
    35
    25
    45
    

- sorted(iterable, key=None, reverse=False) 对所有可迭代的对象进行排序操作。
 - iterable -- 可迭代对象。
 - key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。
 - reverse -- 排序规则，reverse = True 降序 ， reverse = False 升序（默认）。
 - 返回重新排序的列表。


```python
x = [-8, 99, 3, 7, 83]
print(sorted(x))  # [-8, 3, 7, 83, 99]
print(sorted(x, reverse=True))  # [99, 83, 7, 3, -8]

t = ({"age": 20, "name": "a"}, {"age": 25, "name": "b"}, {"age": 10, "name": "c"})
x = sorted(t, key=lambda a: a["age"])
print(x)
# [{'age': 10, 'name': 'c'}, {'age': 20, 'name': 'a'}, {'age': 25, 'name': 'b'}]
```

    [-8, 3, 7, 83, 99]
    [99, 83, 7, 3, -8]
    [{'age': 10, 'name': 'c'}, {'age': 20, 'name': 'a'}, {'age': 25, 'name': 'b'}]
    

- reversed(seq) 函数返回一个反转的迭代器。
 - seq -- 要转换的序列，可以是 tuple, string, list 或 range。


```python
s = 'lsgogroup'
x = reversed(s)
print(type(x))  # <class 'reversed'>
print(x)  # <reversed object at 0x000002507E8EC2C8>
print(list(x))
# ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']

t = ('l', 's', 'g', 'o', 'g', 'r', 'o', 'u', 'p')
print(list(reversed(t)))
# ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']

r = range(5, 9)
print(list(reversed(r)))
# [8, 7, 6, 5]

x = [-8, 99, 3, 7, 83]
print(list(reversed(x)))
# [83, 7, 3, 99, -8]
```

    <class 'reversed'>
    <reversed object at 0x000001ED43184D08>
    ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']
    ['p', 'u', 'o', 'r', 'g', 'o', 'g', 's', 'l']
    [8, 7, 6, 5]
    [83, 7, 3, 99, -8]
    

- enumerate(sequence, [start=0])

用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。


```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
a = list(enumerate(seasons))
print(a)  
# [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]

b = list(enumerate(seasons, 1))
print(b)  
# [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]

for i, element in a:
    print('{0},{1}'.format(i, element))
```

    [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    0,Spring
    1,Summer
    2,Fall
    3,Winter
    

- zip(iter1 [,iter2 [...]])
 - 用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。
 - 我们可以使用 list() 转换来输出列表。
 - 如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。


```python
a = [1, 2, 3]
b = [4, 5, 6]
c = [4, 5, 6, 7, 8]

zipped = zip(a, b)
print(zipped)  # <zip object at 0x000000C5D89EDD88>
print(list(zipped))  # [(1, 4), (2, 5), (3, 6)]
zipped = zip(a, c)
print(list(zipped))  # [(1, 4), (2, 5), (3, 6)]

a1, a2 = zip(*zip(a, b))
print(list(a1))  # [1, 2, 3]
print(list(a2))  # [4, 5, 6]
```

    <zip object at 0x000001ED42EB34C8>
    [(1, 4), (2, 5), (3, 6)]
    [(1, 4), (2, 5), (3, 6)]
    [1, 2, 3]
    [4, 5, 6]
    

## 练习题：

1. 怎么找出序列中的最⼤、⼩值？

``` python
max(),min()
```

2. sort() 和 sorted() 区别


```python
x = [-8, 99, 3, 7, 83]
x.sort()
print(x)
x = [-8, 99, 3, 7, 83]
sorted(x)
print(x)
#sort()改变了原序列的顺序，且使用方法为对象.sort()
#sorted()没有改变原序列的顺序，而是生成一个新序列，使用方法为sorted（对象）
```

    [-8, 3, 7, 83, 99]
    [-8, 99, 3, 7, 83]
    

3. 怎么快速求 1 到 100 所有整数相加之和？


```python
sum(i for i in range(101))
```




    5050



4. 求列表 [2,3,4,5] 中每个元素的立方根。


```python
a = [2,3,4,5]
b = list()
for i in a:
    i=i**(1/3)
    b.append(i)
print(b)
```

    [1.2599210498948732, 1.4422495703074083, 1.5874010519681994, 1.7099759466766968]
    

5. 将[‘x’,‘y’,‘z’] 和 [1,2,3] 转成 [(‘x’,1),(‘y’,2),(‘z’,3)] 的形式。


```python
letter = ['x','y','z']
num = [1,2,3]
com = zip(letter,num)
print(list(com))
```

    [('x', 1), ('y', 2), ('z', 3)]
    
