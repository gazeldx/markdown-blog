---
id: ruby_1
title: Ruby 面试常见题目与答案（1小时速览版）
permalink: /ruby-interview-common-questions-and-answers-1-hour-quick-review
date: 2025-05-12 18:54:17
thumbnail: interview/ruby/ruby_1_hour.png
tags: [ Ruby, Interview ]
---

# Ruby 面试速览指南 (1小时版)

## 基础概念 (10分钟)

### Ruby 特点
- 动态、解释型、面向对象
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

### 符号 vs 字符串
- 符号是不可变的，用作标识符
- 字符串是可变的，用于文本处理

### 哈希新语法
```ruby
old_syntax = {:name => "Alice"}
new_syntax = {name: "Alice"}  # Ruby 1.9+
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
- `protected`
- `private`

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
- 当前类 → 混入模块 (后include的先查) → 父类

### Proc 与 Lambda
```ruby
p = Proc.new { |x, y| [x, y] }
l = lambda { |x, y| [x, y] }  # 或 ->(x,y){ [x,y] }
# 区别: lambda检查参数数量，return行为不同
```

## Rails 相关 (10分钟)

### ActiveRecord
- 约定优于配置
- 关联关系: `has_many`, `belongs_to`
- 回调: `before_save`, `after_create`

### MVC 架构
- Model: 数据与业务逻辑
- View: 展示层 (通常使用ERB/HAML)
- Controller: 处理请求与响应

### RESTful 路由
```ruby
resources :articles do
  member { post :publish }
  collection { get :search }
end
```

## 常见面试题 (5分钟)
1. 解释 Ruby 中的 `nil?`, `empty?`, `blank?`, `present?`
2. 什么是 Ruby 的块 (block)、Proc 和 lambda？它们有什么区别？
3. 解释 Ruby 的单例类 (eigenclass) 是什么？
4. 如何在 Ruby 中实现多线程？有什么注意事项？
5. 解释 Rails 中的 `has_many :through` 关联。
