---
title: "Python笔记"
date: 2022-01-28T21:12:48+08:00
description: 学习记录Python语言
slug: python
categories:
    - Python
tags:
    - Python语法
---

# Pyhton语法笔记
## 列表生成式
```python
# 列表生成式即List Comprehensions, 用来生成特定的列表
# 在列表生成式中，可以使用条件判断语句
# if放在for前面是表达式，可以使用else
# if放在for后面是过滤条件，不可使用else
 [x if x % 2 == 0 else -x for x in range(1, 11)]
 [-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]

# 列表生成式可以嵌套使用
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```
## 生成器
```python
# 可以和列表生成式类似，使用()代替[]来生成generator
>>> g = (x * x for x in range(3))
# 使用next调用generator生成下一个数据
>>> next(g)
0
>>> next(g)
1
# 使用for遍历generator
>>> for n in g:
...    print(n)
...
0
1
4

# 在函数中可使用yield生成generator，yield和return类似。
# 下次函数调用会从yield以后开始执行，且此时的yield返回为None。
# 可以使用send来让yield返回特定的值。
>>> def test(x):
...     while True:
...         y = yield x
...         if y == None:
...             x = x + 1
...         else:
...             x = y
...
>>> g = test(10)
>>> next(g)
10
>>> next(g)
11
>>> g.send(1)
1
>>> next(g)
2
```

## 函数式编程
### map  
```python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### reduce
```python
>>> def add(x, y):
...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25
```

### filter
```python
>>> def is_odd(n):
...     return n % 2 == 1
...
>>> list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
[1, 5, 9, 15]
```

### lambda
```python
>>> f = lambda x: x * x
>>> f
<function <lambda> at 0x101c6ef28>
>>> f(5)
25
```

### 装饰器
```python
from functools import wraps

# 定义装饰器函数
# 参数为要装饰的函数
# 返回装饰后的函数
def square(func):
    def wrap_func(a, b):
        c = func(a, b)
        return pow(c, 2)
    return wrap_func

# 使用wraps装饰器包装装饰器函数
# 使用wraps后，被装饰的函数的__name__属性返回被装饰的函数名称而不是装饰器函数
def square2(func):
    @wraps(func)
    def decorated(a, b):
        c = func(a, b)
        return pow(c, 2)
    return decorated


@square
def add(a, b):
    return a + b


print(add(1, 2))
print(add.__name__)

@square2
def add(a, b):
    return a + b


print(add(1, 2))
print(add.__name__)

# output:
9
wrap_func
9
add
```

### 自带装饰器函数  
#### @property
```python
class C:
    def __init__(self):
        self._x = None

    @property
    def x(self):
        return self._x

    @x.setter
    def x(self, value):
        self._x = value

    @x.deleter
    def x(self):
        del self._x


c = C()
c.x = 123
print(c.x)
del c.x

# output
123

```

#### @classmethod
```python
class A:
number = 10

@classmethod
def get_a(cls):  # cls 接收的是当前类，类在使用时会将自身传入到类方法的第一个参数
    print('这是类本身：', cls)  # 如果子类调用，则传入的是子类
    print('这是类属性:', cls.number)


class B(A):
    number = 20
    pass


# 调用类方法 不需要实例化可以执行调用类方法
A.get_a()
B.get_a()

# output
这是类本身： <class '__main__.A'>
这是类属性: 10
这是类本身： <class '__main__.B'>
这是类属性: 20
```

#### @staticmethod
```python
class A:
@staticmethod
def static_func():
    print('class name: ', A.__name__)


class B(A):
    pass


A.static_func()
B.static_func()

# output
class name: A
class name: A
```

### 偏函数
```python
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```
