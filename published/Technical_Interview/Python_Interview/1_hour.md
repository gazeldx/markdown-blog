---
id: python_1
title: Python 面试常见题目与答案（1小时速览版）
permalink: /python-interview-common-questions-and-answers-1-hour-quick-review
date: 2025-05-12 18:38:14
thumbnail: interview/python/python_1_hour.png
tags: [ Python, Interview ]
---

# Python面试一小时速览

## 一、Python基础

### 1. 变量与数据类型

- 动态类型：变量类型在运行时确定，并且类型可以被修改。

### 2. 列表 vs 元组

| 特性       | 列表(list) | 元组(tuple) |
|------------|------------|-------------|
| 可变性     | 可变       | 不可变      |
| 语法       | `[]`       | `()`        |
| 作为字典键 | 不能       | 可以        |

### 3. 字典与集合

```python
# 字典操作
d = {'a': 1}
d.get('b', 0)  # 安全访问，key不存在返回0

# 集合操作
s = {1,2,3}
s.add(4)  # 添加元素
```

## 二、核心概念

### 1. 深浅拷贝

```python
import copy
lst = [1, [2,3]]
shallow = lst.copy()        # 浅拷贝
deep = copy.deepcopy(lst)   # 深拷贝
```

### 2. 函数参数陷阱

```python
# 错误示范
def func(a, lst=[]):  # 默认列表会持久化
    lst.append(a)
    return lst


print(func(1))  # 输出 [1]
print(func(2))  # 输出 [1, 2] 而不是预期的 [2]
print(func(3))  # 输出 [1, 2, 3] 而不是预期的 [3]
```

```python
# 正确示范
def func(a, lst=None):
    if lst is None:
        lst = []  # 每次调用都会创建一个新列表
    lst.append(a)
    return lst


print(func(1))  # 输出 [1]
print(func(2))  # 输出 [2]
print(func(3, [1, 2]))  # 输出 [1, 2, 3]
```

这个问题的根本原因是 Python 中默认参数是在函数定义时赋值的，而不是在每次调用时。

### 3. 装饰器模板

```python
@decorator1
def my_function(a, b):
    return a + b

# 等同于：
# my_function = decorator1(my_function)
```

举例：日志装饰器

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"调用函数: {func.__name__}, 参数: {args}, {kwargs}")
        result = func(*args, **kwargs)
        print(f"函数 {func.__name__} 返回: {result}")
        return result
    return wrapper

@logger
def add(a, b):
    return a + b

add(3, 5)
# 输出:
# 调用函数: add, 参数: (3, 5), {}
# 函数 add 返回: 8
```

## 三、面向对象

### 类结构示例
```python
class MyClass:
    class_var = 0  # 类变量
    
    def __init__(self, x):
        self.x = x  # 实例变量
    
    @staticmethod
    def static_method():
        pass
        
    @classmethod
    def class_method(cls):
        pass
```

## 五、常考陷阱

### 1. 循环变量泄露

```python
funcs = [lambda x: x + i for i in range(3)]
# 所有lambda函数中的i都是最终值2
print([f(0) for f in funcs])  # 输出[2,2,2]，而不是预期的[0,1,2]
```

#### 为什么会这样？

1. 闭包的特性：
    - lambda 函数创建了一个闭包，它捕获的是变量 `i` 本身，而不是创建时的值
    - Python 的闭包是"迟绑定"的，意味着它们会在调用时查找变量的值，而不是在定义时

2. 循环的执行过程：
    - 当列表推导式执行时，`i` 的值依次为 0, 1, 2
    - 但是 lambda 函数并没有立即执行，它们只是被创建
    - 所有的 lambda 函数都引用同一个变量 `i`

3. 实际调用时的情况：
    - 当循环结束后，`i` 的最终值是 2
    - 当我们调用 `f(0)` 时，所有的 lambda 函数都会查找 `i` 的当前值，也就是 2
    - 所以每个函数都计算 `0 + 2`，结果为 2

#### 如何解决这个问题？

使用闭包函数。

```python
def make_adder(i):
    return lambda x: x + i

funcs = [make_adder(i) for i in range(3)]
print([f(0) for f in funcs])  # 输出[0,1,2]
```

- 通过一个工厂函数 `make_adder`，每次调用都会创建一个新的作用域
- 每个 lambda 捕获的是不同作用域中的 `i`

## 速记清单

1. 可变对象：list/dict/set
2. 不可变对象：int/float/str/tuple
3. 浅拷贝只复制最外层
4. 装饰器本质是函数嵌套
5. GIL(Global Interpreter Lock)，是一个互斥锁（mutex），它确保同一时刻只有一个线程可以执行 Python 字节码
