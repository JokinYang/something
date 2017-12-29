---
title: Python 内置函数
date: 2017-12-26 09:20:49
tags:
---
Python有很多内置函数，比如map(),filter(),reduce(),sorted() 这些内置函数能够很简洁的完成一些需求，学习这些函数的用法能大大提高~~开发效率~~逼格  
Tips：可用help函数查看这些函数的官方文档 如：help(map)
# Python中的“三目运算符”
在C语言和Java中三目运算符是个简洁、好用的运算符，但是在Python中并不能直接使用这种三目运算符
```java
int a=2;
int b=3;
//返回a b中较大的值
a>b ? a : b
```
> <表达式1> ? <表达式2> : <表达式3>
> 如果 表达式1 为真则执行 表达式2 否则执行 表达式3

但是在Python中有一种间接代替了三目运算符的用法

```python
a=2
b=3
#返回a b中较大的值
a if a>b else b
```
>类比以上写法 这种用法可以归纳为：
><表达式2> if <表达式1> else <表达式3>
>如果 表达式1 为真则执行 表达式2 否则执行 表达式3

# 列表生成器
列表生成器用法如下：
``` python
#当以代码在[]内时返回的是list对象
arr = [1, 2, 3]
square = [x * x for x in arr]
print(square)
>>> [1, 4, 9]

#当代码在()内时，返回的是generator的对象
arr = [1, 2, 3]
square = (x * x for x in arr)
print(square)
>>> <generator object <genexpr> at 0x00000220BE731F68>
#此时如需获得计算的结果可用next()函数
next(square)
>>> 1
next(square)
>>> 4
next(square)
>>> 9
#当调用next的次数大于square的长度时会报错
next(square)
>>> Traceback (most recent call last):
>>> next(square)
>>> StopIteration
```
在列表生成器中for语句是可以嵌套的
```python
arr = [[1, 2], [3, 4], [5, 6]]
square = [[ans * ans for ans in x] for x in arr]
>>> [[1, 4], [9, 16], [25, 36]]
```

# lambda表达式

lambda表达式，即为匿名函数。在开发过程中熟练使用可使代码整洁、精炼。
``` python
square_l=lambda x:x*x

def square_d(x):
	return x*x
#square_l()和square_d()的效果是完全一样的
square_l(3)
>>> 9
square_d(3)
>>> 9
#也可以直接使用lambda表达式
(lambda x:x*x)(3)
>>> 9
```



# map()
map函数接收两个或三个变量，第一个变量为函数句柄，第二个为Iterable对象，第三个（可选）也为Iterable对象。
>map(func:Callable[[_T1,_T2],_S],iter1:Iterable[_T1],iter2:Iterable[_T2])

通俗的讲，map函数将接收的可迭代对象以此传入接收的函数中，并将函数返回的结果加入一个集合中并返回这个集合

map 接收两个参数时：
``` Python
num_list=[1,2,3,4]
def square(num):
	return num*num

#map返回的为Iterable对象，需调用next()取得其中的值
ans_iter=map(square,num_list)
print(ans_iter)
>>> <map object at 0x0000024B8AE6A5C0>

#可使用列表生成器将ans_iter转换为list
ans_list=[x for x in iter(ans_iter)]
print(ans_list)
>>> [1,4,9,16]
```

map接收三个参数时：

``` python
a=[1,2,3]
b=[4,5,6]
def list_add(m,n):
	return m+n

ans=map(list_add,a,b)
print([x for x in iter(ans)])
>>> [5,7,9]
#很明显ans为a、b对应元素相加的结果
```


# filter()
filter函数的官方文档：
> filter(function or None, sequence) -> list, tuple, or string

>    Return those items of sequence for which function(item) is true.  If
>    function is None, return the items that are true.  If sequence is a tuple
>    or string, return the same type, else return a list.

filter和map函数相似，接收一个函数句柄和一个可迭代对象，将可迭代对象的元素以此传入函数中，若满足则将该值加入返回值的集合中，若不满足则将其剔除
```python
a=[1,3,4,5,6,7,8,9]
#判断传入数据是否大于5
def judge(num):
	return num>5
ans=filter(judge,a)
print([x for x in iter(ans)])
>>> [7,8,9]
```

可见用filter函数过滤数据很是方便

# reduce()
不知道怎么描述这个函数的用法，直接看官方的帮助吧
>reduce(function, sequence[, initial]) -> value
>Apply a function of two arguments cumulatively to the items of a sequence,
>from left to right, so as to reduce the sequence to a single value.
>For example, reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]) calculates
>((((1+2)+3)+4)+5).  If initial is present, it is placed before the items
>of the sequence in the calculation, and serves as a default when the sequence is empty.

```python
#实现元素的累加,reduce是将列表的第一个和第二个元素传入add中，并将返回的值和下一个元素一起传入，直到列表的元素都传入过。
a=[1,2,3,4,5]
def add(x,y):
	return x+y

reduce(add,a)
>>> 15
#传入三个参数时，传入三个参数时，将第三个函数和列表的第一个函数传入add中，并将返回的值和下一个元素一起传入，直到列表的元素都传入过。
reduce(add,a,100)
>>> 115
```

# sorted()
sorted是一个内置的排序函数
> sorted(iterable, cmp=None, key=None, reverse=False) --> new sorted list

cmp为排序函数，key指定的函数将作用于list的每一个元素上，并根据key函数的返回结果进行排序，reverse可指定排序结果是否倒置

```python
a=[1,2,3,4,5]
#通过reverse可实现列表的倒置
sorted(a,reverse=True)
>>> [5,4,3,2,1]

b=[1,2,-3,4,-5]
sorted(a,key=abs)
>>> [1,2,3,4,5]


#也可自己实现排序函数cmp
def cmp(x,y):
	if x>y:
    	return -1
    elif x<y:
    	return 1
    return 0

```
