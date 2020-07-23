# 条件语句

注意if和else后都要有：

【例子】



```python
temp = input("猜一猜想的是哪个数字？")
guess = int(temp) # input 函数将接收的任何数据类型都默认为 str。
if guess == 666:
    print("你太了解小姐姐的心思了！")
    print("哼，猜对也没有奖励！")
else:
    print("猜错了，小姐姐现在心里想的是666！")
print("游戏结束，不玩儿啦！")
```

    猜一猜想的是哪个数字？666
    你太了解小姐姐的心思了！
    哼，猜对也没有奖励！
    游戏结束，不玩儿啦！
    

##  if - else 嵌套

Python 使用缩进而不是大括号来标记代码块边界，因此要特别注意else的悬挂问题。

【例子】


```python
hi = 1
if hi > 2:
    if hi > 7:
        print('好棒!好棒!')
else:
    print('切~')
```

    切~
    


```python
temp = input("不妨猜一下小哥哥现在心里想的是那个数字：")
guess = int(temp)
if guess > 8:
    print("大了，大了")
else:
    if guess == 8:
        print("你这么懂小哥哥的心思吗？")
        print("哼，猜对也没有奖励！")
    else:
        print("小了，小了")
print("游戏结束，不玩儿啦！")
```

    不妨猜一下小哥哥现在心里想的是那个数字：8
    你这么懂小哥哥的心思吗？
    哼，猜对也没有奖励！
    游戏结束，不玩儿啦！
    

## if - elif - else 

elif 语句即为 else if，用来检查多个表达式是否为真，并在为真时执行特定代码块中的代码。

【例子】


```python
temp = input('请输入成绩:')
source = int(temp)
if 100 >= source >= 90:
    print('A')
elif 90 > source >= 80:
    print('B')
elif 80 > source >= 60:
    print('C')
elif 60 > source >= 0:
    print('D')
else:
    print('输入错误！')
```

    请输入成绩:101
    输入错误！
    

## assert 关键词

assert 这个关键词我们称之为“断言”，当这个关键词后边的条件为 False 时，程序自动崩溃并抛出AssertionError的异常。

【例子】


```python
my_list = ['lsgogroup']
my_list.pop(0)
assert len(my_list) > 0

# AssertionError
```


    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    <ipython-input-20-d6a31436682c> in <module>
          1 my_list = ['lsgogroup']
          2 my_list.pop(0)
    ----> 3 assert len(my_list) > 0
          4 
          5 # AssertionError
    

    AssertionError: 


在进行单元测试时，可以用来在程序中置入检查点，只有条件为 True 才能让程序正常工作。


```python
assert 3 > 7

# AssertionError
```


    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    <ipython-input-24-2b14821de816> in <module>
    ----> 1 assert 3 > 7
          2 
          3 # AssertionError
    

    AssertionError: 



```python
assert 8 > 7

# AssertionError
```

# 循环语句


## while

while循环的代码块会一直循环执行，直到布尔表达式的值为布尔假，后面也加：

【例子】


```python
count = 0
while count < 3:
    temp = input("不妨猜一下小哥哥现在心里想的是那个数字：")
    guess = int(temp)
    if guess > 8:
        print("大了，大了")
    else:
        if guess == 8:
            print("你是小哥哥心里的蛔虫吗？")
            print("哼，猜对也没有奖励！")
            count = 3
        else:
            print("小了，小了")
    count = count + 1
print("游戏结束，不玩儿啦！")
```

    不妨猜一下小哥哥现在心里想的是那个数字：1
    小了，小了
    不妨猜一下小哥哥现在心里想的是那个数字：2
    小了，小了
    不妨猜一下小哥哥现在心里想的是那个数字：3
    小了，小了
    游戏结束，不玩儿啦！
    


```python
string = 'abcd'
while string:
    print(string)
    string = string[1:]
```

    abcd
    bcd
    cd
    d
    

从第二个开始的字符串赋值为新字符串

## while - else 循环

当while循环正常执行完的情况下，执行else输出，如果while循环中执行了跳出循环的语句，比如 break，将不执行else代码块的内容。




```python
count = 0
while count < 5:
    print("%d is  less than 5" % count)
    count = 6
    break
else:
    print("%d is not less than 5" % count)


```

    0 is  less than 5
    

## for 循环

可以遍历任何有序序列，如str、list、tuple等，也可以遍历任何可迭代对象，如dict。


```python
member = ['张三', '李四', '刘德华', '刘六', '周润发']
for i in range(len(member)):
    print(member[i])
```

    张三
    李四
    刘德华
    刘六
    周润发
    


```python
dic = {'a': 1, 'b': 2, 'c': 3, 'd': 4}

for key, value in dic.items():
    print(key, value, sep=':', end='    ')
```

    a:1    b:2    c:3    d:4    

## for - else 循环


```python
for num in range(10, 20):  # 迭代 10 到 20 之间的数字
    for i in range(2, num):  # 根据因子迭代
        if num % i == 0:  # 确定第一个因子,能否整除
            j = num / i  # 计算第二个因子，确定整数部分
            print('%d 等于 %d * %d' % (num, i, j))
            break  # 跳出当前循环
    else:  # 循环的 else 部分
        print(num, '是一个质数')
```

    10 等于 2 * 5
    11 是一个质数
    12 等于 2 * 6
    13 是一个质数
    14 等于 2 * 7
    15 等于 3 * 5
    16 等于 2 * 8
    17 是一个质数
    18 等于 2 * 9
    19 是一个质数
    

## range() 函数

range([start], [stop],[ step=1])

生成一个从start参数的值开始到stop参数的值结束的数字序列，该序列包含start的值但不包含stop的值。step默认为1。


```python
for i in range(1, 10, 2):
    print(i)

```

    1
    3
    5
    7
    9
    

## enumerate()函数

enumerate(sequence, [start=0])


```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
lst = list(enumerate(seasons))
print(lst)

lst = list(enumerate(seasons, start=1))  # 下标从 1 开始
print(lst)

```

    [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    

enumerate()与 for 循环的结合使用
```python
    for i, a in enumerate(A)
    do something with a  
    
用 enumerate(A) 不仅返回了 A 中的元素，还顺便给该元素一个索引值 (默认从 0 开始)。此外，用 enumerate(A, j) 还可以确定索引起始值为 j。

```


```python
languages = ['Python', 'R', 'Matlab', 'C++']
for language in languages:
    print('I love', language)
print('Done!')


```

    I love Python
    I love R
    I love Matlab
    I love C++
    Done!
    


```python
for i, language in enumerate(languages, 1):
    print(i, 'I love', language)
print('Done!')

```

    1 I love Python
    2 I love R
    3 I love Matlab
    4 I love C++
    Done!
    

## break 语句

break语句可以跳出当前所在层的循环。

## continue 语句

continue终止本轮循环并开始下一轮循环。

## pass 语句

pass 语句的意思是“不做任何事”，如果你在需要有语句的地方不写任何语句，那么解释器会提示出错，而 pass 语句就是用来解决这些问题的。


```python
def a_func():

```


      File "<ipython-input-13-a2e1e12e0a2a>", line 1
        def a_func():
                     ^
    SyntaxError: unexpected EOF while parsing
    



```python
def a_func():
    pass
```

这时就可用pass

pass是空语句，不做任何操作，只起到占位的作用，其作用是为了保持程序结构的完整性。尽管pass语句不做任何操作，但如果暂时不确定要在一个位置放上什么样的代码，可以先放置一个pass语句，让代码可以正常运行。

## 综合例子


```python
passwdList = ['123', '345', '890']
valid = False
count = 3
while count > 0:
    password = input('enter password:')
    for item in passwdList:
        if password == item:
            valid = True
            break
            
    if not valid:
        print('invalid input')
        count -= 1
        continue
    else:
        break
```

    enter password:3
    invalid input
    enter password:4
    invalid input
    enter password:5
    invalid input
    

## 练习题：

1、编写一个Python程序来查找那些既可以被7整除又可以被5整除的数字，介于1500和2700之间。


```python
for i in range(1500, 2701):
    if (i%35 == 0):
        print(i)
```

    1505
    1540
    1575
    1610
    1645
    1680
    1715
    1750
    1785
    1820
    1855
    1890
    1925
    1960
    1995
    2030
    2065
    2100
    2135
    2170
    2205
    2240
    2275
    2310
    2345
    2380
    2415
    2450
    2485
    2520
    2555
    2590
    2625
    2660
    2695
    

2、龟兔赛跑游戏

题目描述：

话说这个世界上有各种各样的兔子和乌龟，但是研究发现，所有的兔子和乌龟都有一个共同的特点——喜欢赛跑。于是世界上各个角落都不断在发生着乌龟和兔子的比赛，小华对此很感兴趣，于是决定研究不同兔 子和乌龟的赛跑。他发现，兔子虽然跑比乌龟快，但它们有众所周知的毛病——骄傲且懒惰，于是在与乌龟的比赛中，一旦任一秒结束后兔子发现自己领先t米或以 上，它们就会停下来休息s秒。对于不同的兔子，t，s的数值是不同的，但是所有的乌龟却是一致——它们不到终点决不停止。

然而有些比赛相当漫长，全程观看会耗费大量时间，而小华发现只要在每场比赛开始后记录下兔子和乌龟的数据——兔子的速度v1（表示每秒兔子能跑v1 米），乌龟的速度v2，以及兔子对应的t，s值，以及赛道的长度l——就能预测出比赛的结果。但是小华很懒，不想通过手工计算推测出比赛的结果，于是他找 到了你——清华大学计算机系的高才生——请求帮助，请你写一个程序，对于输入的一场比赛的数据v1，v2，t，s，l，预测该场比赛的结果。

输入:

输入只有一行，包含用空格隔开的五个正整数v1，v2，t，s，l，其中(v1,v2< =100;t< =300;s< =10;l< =10000且为v1,v2的公倍数)

输出:

输出包含两行，第一行输出比赛结果——一个大写字母“T”或“R”或“D”，分别表示乌龟获胜，兔子获胜，或者两者同时到达终点。

第二行输出一个正整数，表示获胜者（或者双方同时）到达终点所耗费的时间（秒数）。

样例输入：

10 5 5 2 20

样例输出

D
4


```python

```
