This covers the **essential React interview topics** in a concise format.

## Core Concepts

### 1. What is React? What are its key features?

**Answer**:  

React is a JavaScript library for building user interfaces, developed by Facebook.

**Key Features**:

- **Component-Based**: UI is broken into reusable components.
- **Virtual DOM**: Efficient UI updates.
- **Unidirectional Data Flow**: Data flows from parent to child.
- **JSX**: JavaScript syntax extension for writing HTML-like code in JS.

### 2. What are the two types of React components? How do they differ?

**Answer**:

- **Functional Components**: Simple JavaScript functions that accept `props` and return React elements.

    ```jsx
    function Welcome(props) {
      return <h1>Hello, {props.name}</h1>;
    }
    ```
  
- **Class Components**:
    - ES6 classes that extend `React.Component`.
    - Have `state` and lifecycle methods.

    ```jsx
    class Welcome extends React.Component {
      render() {
        return <h1>Hello, {this.props.name}</h1>;
      }
    }
    ```  

**Key Differences**:

- Functional components are simpler and perform better (Hooks reduced the gap).
- Class components have `state` and lifecycle methods (now possible with Hooks).

### 3. What is JSX? How is it different from HTML?
**Answer**:  

JSX is a syntax extension for JavaScript that allows writing HTML-like markup in JS.

**Differences from HTML**:

- Use `className` instead of `class`.
- Inline styles are objects: `style={{ color: 'red' }}`.
- Event handlers use camelCase: `onClick` instead of `onclick`.
- Must close all tags: `<input />` instead of `<input>`.
- Can embed JS expressions: `{variable}`.

### 4. What are `props` and `state` in React?
**Answer**:  

| **Props** | **State** |
|-----------|----------|
| Passed from parent to child | Managed within a component |
| Immutable (read-only) | Mutable (via `setState` or `useState`) |
| Used for component communication | Triggers re-renders when updated |

### 5. Explain React lifecycle methods (Class Components).

**Answer**:

- **Mounting**:
    - `constructor()` → `render()` → `componentDidMount()` (API calls here).
- **Updating**:
    - `shouldComponentUpdate()` → `render()` → `componentDidUpdate()`.
- **Unmounting**:
    - `componentWillUnmount()` (cleanup like timers).

## React Hooks

### 6. What are React Hooks? Why were they introduced?
**Answer**: 

Hooks (introduced in React 16.8) let functional components use state and other React features.

**Common Hooks**:
 
- `useState` → Manage state.
- `useEffect` → Side effects (replaces lifecycle methods).
- `useContext` → Access context.
- `useReducer` → Complex state logic.

**Why Hooks?**

- Solve code reuse issues in classes.
- Simplify component logic.
- Avoid `this` confusion.

### 7. Explain `useState` and `useEffect`.
**Answer**:  

**`useState`**:

```jsx
const [count, setCount] = useState(0); // Initial state = 0
```  

- Returns `[state, setState]`.
- Updates trigger re-renders.

**`useEffect`**:

```jsx
useEffect(() => {
  // Side effect (API call, subscription)
  return () => { /* Cleanup */ }; // Optional
}, [dependencies]); // Runs when dependencies change
```  

## Advanced Topics

### 8. How to optimize React performance?

**Answer**:

- **`React.memo`**: Memoize components.
- **`useMemo`/`useCallback`**: Memoize values/functions.
- **Virtual DOM**: Minimizes direct DOM updates.
- **Code Splitting**: `React.lazy` + `Suspense`.
- **Avoid inline functions/objects in props**.

### 9. What is Context API? When to use it?
**Answer**:  

Context provides a way to share data globally without prop-drilling.

**Use Cases**:
 
- Theme (dark/light mode).
- User authentication.
- Localization (i18n).
- Simple state management (alternative to Redux).

### 10. Why are `keys` important in React lists?
**Answer**:

- Helps React identify added/removed items.
- Improves rendering performance.
- Must be **unique** and **stable** (avoid array indices).

```jsx
{todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
```  

## Practical Questions

### 11. How to handle forms in React?

**Answer**:

- **Controlled Components** (recommended):

```jsx
const [value, setValue] = useState("");
<input value={value} onChange={(e) => setValue(e.target.value)} />
```

- **Uncontrolled Components**:

```jsx
const inputRef = useRef();
<input ref={inputRef} />
// Access via inputRef.current.value
```

### 12. How to fetch data in React?
**Answer**:

```jsx
useEffect(() => {
  const fetchData = async () => {
    const res = await fetch("api.example.com/data");
    const data = await res.json(); // Must use await!
    setData(data);
  };
  fetchData();
}, []); // Empty dependency = runs once on mount
```  

**Key Notes**:

- Always use `await res.json()` (not just `res.json()`).
- Handle loading/error states.
- Cancel requests in cleanup (e.g., `AbortController`).

Good luck with your interview! 🚀
