---
id: react_one_hour
title: React.js Interview Questions & Answers (1-Hour Crash Course)
permalink: /
date: 2025-04-27 15:08:24
thumbnail: interview/javascript/reactjs_1_hour.png
tags: [React.js, Interview]
---

# React.js 面试题目与答案（1小时速览版）

这些题目涵盖了React的主要概念，适合1小时快速复习。

## 基础概念

### 1. 什么是React？它的核心特点是什么？
**答案**：
React是一个用于构建用户界面的JavaScript库，由Facebook开发。核心特点：
- **组件化**：UI被拆分为独立可复用的组件
- **虚拟DOM**：高效更新视图的机制
- **单向数据流**：数据从父组件流向子组件
- **JSX**：JavaScript语法扩展，允许在JS中写HTML-like代码

### 2. React组件有哪两种类型？它们有什么区别？
**答案**：
- **函数组件**：简单的JavaScript函数，接收props返回React元素
  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```
- **类组件**：ES6类，继承React.Component，可以使用state和生命周期方法
  ```jsx
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```

主要区别：
- 函数组件更简单，性能更好（React 16.8后有了Hooks，功能差距缩小）
- 类组件有state和生命周期方法（现在函数组件通过Hooks也能实现）

## 核心概念

### 3. 什么是JSX？它与HTML有什么区别？
**答案**：
JSX是JavaScript的语法扩展，允许在JavaScript代码中写类似HTML的标记。

区别：
- 使用`className`代替`class`
- 样式使用对象形式：`style={{color: 'red'}}`而不是字符串
- 事件处理使用驼峰命名：`onClick`而不是`onclick`
- 必须闭合所有标签：`<input />`而不是`<input>`
- 可以嵌入JavaScript表达式：`{variable}`

### 4. React中的props和state有什么区别？
**答案**：
- **props**（属性）：
    - 从父组件传递给子组件
    - 只读，子组件不能修改
    - 用于组件间通信

- **state**（状态）：
    - 组件内部维护的数据
    - 可变的，通过`setState()`（类组件）或状态Hook（函数组件）更新
    - 状态变化会触发组件重新渲染

### 5. 什么是React生命周期方法？列举几个重要的生命周期方法
**答案**：
生命周期方法是类组件中在不同阶段自动调用的方法。

主要生命周期方法：
- **挂载阶段**：
    - `constructor()`：初始化state和绑定方法
    - `render()`：返回JSX
    - `componentDidMount()`：组件挂载后执行，适合API调用

- **更新阶段**：
    - `shouldComponentUpdate()`：决定是否重新渲染
    - `render()`
    - `componentDidUpdate()`：组件更新后执行

- **卸载阶段**：
    - `componentWillUnmount()`：清理工作如取消定时器

## Hooks

### 6. 什么是React Hooks？为什么要引入它们？
**答案**：
Hooks是React 16.8引入的特性，允许函数组件使用state和其他React特性。

常用Hooks：
- `useState`：管理状态
- `useEffect`：处理副作用（替代生命周期方法）
- `useContext`：访问context
- `useReducer`：复杂状态逻辑

引入原因：
- 解决类组件中逻辑难以复用的问题
- 简化组件逻辑，使相关代码更集中
- 避免类组件中`this`的混淆问题

### 7. 解释useState和useEffect Hook
**答案**：
**useState**：
```jsx
const [count, setCount] = useState(0);
```
- 返回当前状态和更新状态的函数
- 参数是初始状态
- 状态更新会触发组件重新渲染

**useEffect**：
```jsx
useEffect(() => {
  // 副作用代码
  document.title = `You clicked ${count} times`;
  
  return () => {
    // 清理函数（可选）
  };
}, [count]); // 依赖数组
```
- 处理副作用（数据获取、订阅、手动DOM操作）
- 第一个参数是effect函数
- 第二个参数是依赖数组，控制effect执行时机
- 返回的函数用于清理工作

## 高级概念

### 8. React中如何优化性能？
**答案**：
- **React.memo**：记忆函数组件，避免不必要的重新渲染
- **useMemo**：记忆计算结果，避免重复计算
- **useCallback**：记忆函数，避免子组件不必要的更新
- **虚拟DOM**：React自动使用虚拟DOM进行高效更新
- **代码分割**：使用`React.lazy`和`Suspense`进行懒加载
- **避免内联函数和对象**：作为props传递时会导致子组件不必要更新

### 9. 什么是Context API？何时使用它？
**答案**：
Context提供了一种在组件树中共享数据的方法，而不必逐层传递props。

使用场景：
- 主题设置（如暗黑/明亮模式）
- 用户认证信息
- 多语言/国际化
- 全局状态管理（替代Redux的简单场景）

示例：
```jsx
const ThemeContext = React.createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>I am styled by theme!</button>;
}
```

### 10. 解释React中的key属性及其重要性
**答案**：
`key`是React用于识别列表中元素的特殊属性。

重要性：
- 帮助React识别哪些元素被添加/修改/删除
- 提高列表渲染性能
- 避免因元素位置变化导致的意外行为

最佳实践：
- 使用唯一且稳定的标识作为key（如ID）
- 避免使用数组索引作为key（除非列表静态不变）
- key只需在兄弟节点中唯一

```jsx
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

## 实际应用

### 11. 如何在React中处理表单？
**答案**：
React中有两种处理表单的方式：

1. **受控组件**：
    - 表单数据由React state管理
    - 每个状态变化都有对应的处理函数
    - 推荐方式，更符合React哲学

```jsx
function MyForm() {
  const [value, setValue] = useState('');

  const handleChange = (event) => {
    setValue(event.target.value);
  };

  const handleSubmit = (event) => {
    alert('A name was submitted: ' + value);
    event.preventDefault();
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={value} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

2. **非受控组件**：
    - 表单数据由DOM自身处理
    - 使用ref获取表单值
    - 适合简单场景或集成非React代码

```jsx
function MyForm() {
  const inputRef = useRef(null);

  const handleSubmit = (event) => {
    alert('A name was submitted: ' + inputRef.current.value);
    event.preventDefault();
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

### 12. 如何在React中发送HTTP请求？
**答案**：
通常在`useEffect` Hook中发送请求：

```jsx
function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchUsers = async () => {
      setLoading(true);
      try {
        const response = await fetch('https://api.example.com/users');
        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };

    fetchUsers();
  }, []); // 空依赖数组表示只在组件挂载时执行

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

最佳实践：
- 使用`async/await`或Promise处理异步
- 处理加载和错误状态
- 在`useEffect`的清理函数中取消未完成的请求（如使用AbortController）
- 考虑使用专门的HTTP库（如axios）

祝您面试顺利！
