# Python Interview 1-Hour Quick Review

## I. Python Basics

### 1. Variables & Data Types

- Dynamic Typing: Variable types are determined at runtime and can be modified.

### 2. List vs Tuple

| Feature    | List (list) | Tuple (tuple) |
|------------|-------------|---------------|
| Mutability | Mutable     | Immutable     |
| Syntax     | `[]`        | `()`          |
| As dict key| Cannot      | Can           |

### 3. Dictionary & Set

```python
# Dictionary operations
d = {'a': 1}
d.get('b', 0)  # Safe access, returns 0 if key doesn't exist

# Set operations
s = {1,2,3}
s.add(4)  # Add element
```

## II. Core Concepts

### 1. Deep vs Shallow Copy

```python
import copy
lst = [1, [2,3]]
shallow = lst.copy()        # Shallow copy
deep = copy.deepcopy(lst)   # Deep copy
```

### 2. Function Parameter Pitfalls

```python
# Incorrect example
def func(a, lst=[]):  # Default list will persist
    lst.append(a)
    return lst

print(func(1))  # Output [1]
print(func(2))  # Output [1, 2] instead of the expected [2]
print(func(3))  # Output [1, 2, 3] instead of the expected [3]
```

```python
# Correct example
def func(a, lst=None):
    if lst is None:
        lst = []  # A new list is created on each call
    lst.append(a)
    return lst

print(func(1))  # Output [1]
print(func(2))  # Output [2]
print(func(3, [1, 2]))  # Output [1, 2, 3]
