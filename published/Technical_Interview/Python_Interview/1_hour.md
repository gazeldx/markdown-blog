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
- 动态类型：变量类型在运行时确定
- `is` vs `==`：
  ```python
  a = [1,2]; b = [1,2]
  print(a == b)  # True (值相等)
  print(a is b)  # False (不同对象)
  ```

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
```

### 3. 装饰器模板
```python
def decorator(func):
    def wrapper(*args, **kwargs):
        # 前置操作
        result = func(*args, **kwargs)
        # 后置操作
        return result
    return wrapper
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

## 四、高频算法

### 1. 反转链表
```python
def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev
```

### 2. 快速排序
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr)//2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
```

## 五、常考陷阱

### 1. 循环变量泄露
```python
funcs = [lambda x: x+i for i in range(3)]
# 所有lambda函数中的i都是最终值2
print([f(0) for f in funcs])  # 输出[2,2,2]
```

### 2. 修改迭代中的列表
```python
lst = [1,2,3,4]
for item in lst[:]:  # 创建副本迭代
    if item % 2 == 0:
        lst.remove(item)
```

## 速记清单
1. 可变对象：list/dict/set
2. 不可变对象：int/float/str/tuple
3. 浅拷贝只复制最外层
4. 装饰器本质是函数嵌套
5. GIL限制多线程并行
6. 生成器用`yield`节省内存
