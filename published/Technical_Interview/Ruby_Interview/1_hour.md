---
id: ruby_1
title: Ruby 面试常见题目与答案（1小时速览版）
permalink: /ruby-interview-common-questions-and-answers-1-hour-quick-review
date: 2025-05-12 18:54:17
thumbnail: interview/ruby/ruby_1_hour.png
tags: [ Ruby, Interview ]
---

## 基础概念 (10分钟)

### Ruby 特点
- 动态、[解释型](https://zhangjian.dev/blog/a43-a42l)、面向对象
- 一切皆对象 (包括数字、nil)
- 鸭子类型 (Duck Typing)
- 强大的元编程能力

### 变量类型
```ruby
local_var = "local"    # 局部变量
@instance_var = "iv"   # 实例变量
@@class_var = "cv"     # 类变量
$global_var = "gv"     # 全局变量
CONSTANT = "const"     # 常量
```

### 真假值
- 只有 `false` 和 `nil` 为假，其他都为真

## 核心语法 (15分钟)

### Ruby 中有至少三种创建一个类的方式，是哪三种？

#### 1. 使用 `class` 关键字

```ruby
class MyClass
  def hello
    puts "Hello from MyClass!"
  end
end

obj = MyClass.new
obj.hello # 输出: "Hello from MyClass!"
```

#### 2. 用 `Class.new`

```ruby
MyDynamicClass = Class.new do
  def hello
    puts "Hello from dynamic class!"
  end
end

obj = MyDynamicClass.new
obj.hello # 输出: "Hello from dynamic class!"
```

#### 3. 使用 `Struct`（快速创建类）
```ruby
Person = Struct.new(:name, :age) do
  def greet
    puts "Hi, I'm #{name}, aged #{age}!"
  end
end

person = Person.new("Alice", 30)
puts person.name # 输出: "Alice"
person.greet # 输出: "Hi, I'm Alice, aged 30!"
```

### 方法定义
```ruby
def greet(name = "World")
  "Hello, #{name}!"
end

# 带块的方法
def with_log
  puts "Start"
  yield if block_given?
  puts "End"
end
```

### 数组操作
```ruby
%w[a b c]        # => ["a", "b", "c"]
[1, 2, 3].map { |x| x * 2 }  # => [2, 4, 6]
```

## 面向对象 (10分钟)

### 类与继承
```ruby
class Animal
  def speak
    "Animal sound"
  end
end

class Dog < Animal
  def speak
    super + ": Woof!"
  end
end
```

### 访问控制
- `public` (默认)
- `protected` (用 `protected` 修饰的方法，只能在本类或子类的“实例方法的定义体”中调用，在其它任何地方调用都会报错！)
- `private`（用 `private` 修饰的方法，不能显式地写出接收者；只能隐式地用调用，接收者为`self`）

`protected`使用举例：

```ruby
class Person
  def initialize(age)
    @age = age
  end

  def older_than?(other_person)
    age > other_person.age  # Can access other_person's protected method
  end

  protected
  
  attr_reader :age
end

alice = Person.new(30)
bob = Person.new(25)

puts alice.older_than?(bob)  # => true
# bob.age  # Would raise NoMethodError (protected method)

class Man < Person
  def print_friend_age(man)
    puts man.age
  end
end

jack = Man.new(43)
jack.print_friend_age(bob) # => 25
```

### 模块与混入
```ruby
module Loggable
  def log(msg)
    puts "[LOG] #{msg}"
  end
end

class Product
  include Loggable
end
```

## 高级特性 (10分钟)

### 元编程
```ruby
# 动态定义方法
class MyClass
  define_method :dynamic_method do |arg|
    "Called with #{arg}"
  end
end
```

### 方法查找路径
- 当前类 → 混入模块 (后`include`的先查) → 父类

### Proc 与 Lambda 的区别
```ruby
p = Proc.new { |x, y| [x, y] }
l = lambda { |x, y| [x, y] }  # 或 ->(x,y){ [x,y] }
# 区别: lambda检查参数数量，return行为不同
```

#### 1. 参数检查严格性
- **Lambda**：严格检查参数数量，不匹配时抛出 `ArgumentError`。  

```ruby
lam = lambda { |x, y| [x, y] }
lam.call(1)  # ArgumentError: wrong number of arguments (given 1, expected 2)
```

- **Proc**: 宽松处理参数，缺少时补 `nil`，多余时忽略。

```ruby
proc = Proc.new { |x, y| [x, y] }
proc.call(1)  # [1, nil]（不报错）
```

#### 2. `return` 行为差异
- **Lambda**: `return` 仅退出当前 lambda，类似方法返回。

```ruby
def test_lambda
  lam = lambda { return }
  lam.call
  puts "This line runs!"
end

test_lambda  # 输出 "This line runs!"
```

- **Proc**: `return` 会直接跳出包含它的整个方法。

```ruby
def test_proc
  proc = Proc.new { return }
  proc.call
  puts "This line never runs!"
end

test_proc  # 无输出（方法提前退出）
```
