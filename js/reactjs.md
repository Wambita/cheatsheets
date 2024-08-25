# **React.js Cheatsheet**

## **1. Introduction**

### **What is React?**
- **Description:** React is a JavaScript library for building user interfaces, primarily for single-page applications. It allows you to build reusable UI components.
- **Installation:**
  ```bash
  npx create-react-app my-app
  cd my-app
  npm start
  ```

## **2. Components**

### **Function Components**
- **Description:** Components defined as functions. They can use hooks for state and lifecycle features.
- **Example:**
  ```javascript
  function Greeting({ name }) {
    return <h1>Hello, {name}!</h1>;
  }
  ```

### **Class Components**
- **Description:** Components defined as ES6 classes with state and lifecycle methods.
- **Example:**
  ```javascript
  class Greeting extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}!</h1>;
    }
  }
  ```

### **JSX (JavaScript XML)**
- **Description:** A syntax extension that allows you to write HTML elements and components in JavaScript.
- **Example:**
  ```javascript
  const element = <h1>Hello, world!</h1>;
  ```

## **3. Props and State**

### **Props**
- **Description:** Short for properties, they are used to pass data from parent to child components.
- **Example:**
  ```javascript
  function Welcome(props) {
    return <h1>Welcome, {props.name}</h1>;
  }

  function App() {
    return <Welcome name="Sara" />;
  }
  ```

### **State**
- **Description:** A built-in object used to hold data that can change over time in a component.
- **Example:**
  ```javascript
  function Counter() {
    const [count, setCount] = React.useState(0);

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>Click me</button>
      </div>
    );
  }
  ```

## **4. Lifecycle Methods**

### **Class Component Lifecycle**
- **Description:** Methods that are called at specific points in a component’s life cycle.
- **Examples:**
  ```javascript
  class MyComponent extends React.Component {
    componentDidMount() {
      console.log('Component did mount');
    }

    componentDidUpdate(prevProps, prevState) {
      console.log('Component did update');
    }

    componentWillUnmount() {
      console.log('Component will unmount');
    }

    render() {
      return <div>My Component</div>;
    }
  }
  ```

### **Using Effects in Function Components**
- **Description:** `useEffect` hook allows you to perform side effects in function components.
- **Example:**
  ```javascript
  function MyComponent() {
    React.useEffect(() => {
      console.log('Component mounted or updated');

      return () => {
        console.log('Cleanup on unmount');
      };
    }, []); // Empty array means this effect runs once after initial render

    return <div>My Component</div>;
  }
  ```

## **5. Handling Events**

### **Event Handling**
- **Description:** Handle events like clicks, form submissions, etc.
- **Example:**
  ```javascript
  function MyButton() {
    const handleClick = () => {
      alert('Button clicked!');
    };

    return <button onClick={handleClick}>Click me</button>;
  }
  ```

## **6. Conditional Rendering**

### **Description**
- **Definition:** Render different UI based on conditions.
- **Examples:**
  ```javascript
  function UserGreeting(props) {
    return <h1>Welcome back!</h1>;
  }

  function GuestGreeting(props) {
    return <h1>Please sign up.</h1>;
  }

  function Greeting(props) {
    if (props.isLoggedIn) {
      return <UserGreeting />;
    }
    return <GuestGreeting />;
  }
  ```

## **7. Lists and Keys**

### **Rendering Lists**
- **Description:** Use `map` to render a list of elements.
- **Example:**
  ```javascript
  function NumberList(props) {
    const numbers = props.numbers;
    const listItems = numbers.map((number) =>
      <li key={number.toString()}>{number}</li>
    );
    return (
      <ul>{listItems}</ul>
    );
  }
  ```

## **8. Forms**

### **Controlled Components**
- **Description:** Form elements are controlled by React state.
- **Example:**
  ```javascript
  function NameForm() {
    const [name, setName] = React.useState('');

    const handleChange = (event) => {
      setName(event.target.value);
    };

    const handleSubmit = (event) => {
      alert('A name was submitted: ' + name);
      event.preventDefault();
    };

    return (
      <form onSubmit={handleSubmit}>
        <label>
          Name:
          <input type="text" value={name} onChange={handleChange} />
        </label>
        <button type="submit">Submit</button>
      </form>
    );
  }
  ```

## **9. Context API**

### **Description**
- **Definition:** Provides a way to pass data through the component tree without having to pass props manually at every level.
- **Example:**
  ```javascript
  const ThemeContext = React.createContext('light');

  function ThemedComponent() {
    const theme = React.useContext(ThemeContext);
    return <div style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Themed Component</div>;
  }

  function App() {
    return (
      <ThemeContext.Provider value="dark">
        <ThemedComponent />
      </ThemeContext.Provider>
    );
  }
  ```

## **10. Hooks**

### **useState**
- **Description:** Adds state to function components.
- **Example:**
  ```javascript
  const [count, setCount] = React.useState(0);
  ```

### **useEffect**
- **Description:** Performs side effects in function components.
- **Example:**
  ```javascript
  React.useEffect(() => {
    console.log('Effect runs');
  }, [dependencies]);
  ```

### **Custom Hooks**
- **Description:** Allows you to reuse stateful logic between components.
- **Example:**
  ```javascript
  function useCounter(initialValue) {
    const [count, setCount] = React.useState(initialValue);

    const increment = () => setCount(count + 1);
    const decrement = () => setCount(count - 1);

    return { count, increment, decrement };
  }

  function Counter() {
    const { count, increment, decrement } = useCounter(0);
    return (
      <div>
        <p>{count}</p>
        <button onClick={increment}>+</button>
        <button onClick={decrement}>-</button>
      </div>
    );
  }
  ```

## **11. Routing with React Router**

### **Description**
- **Definition:** A library for routing in React applications.
- **Installation:**
  ```bash
  npm install react-router-dom
  ```

### **Basic Routing**
- **Example:**
  ```javascript
  import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom';

  function Home() {
    return <h2>Home</h2>;
  }

  function About() {
    return <h2>About</h2>;
  }

  function App() {
    return (
      <Router>
        <nav>
          <ul>
            <li><Link to="/">Home</Link></li>
            <li><Link to="/about">About</Link></li>
          </ul>
        </nav>
        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </Router>
    );
  }
  ```

---

This cheatsheet provides a quick reference to essential React.js concepts, including components, state management, lifecycle methods, event handling, conditional rendering, and routing. It's designed to help both beginners and experienced developers quickly understand and use React features.

## **3. Advanced Concepts**

### **1. Higher-Order Components (HOCs)**

- **Description:** A pattern for reusing component logic. A higher-order component is a function that takes a component and returns a new component with additional props or behavior.
- **Example:**
  ```javascript
  function withLogger(WrappedComponent) {
    return class extends React.Component {
      componentDidMount() {
        console.log('Component mounted');
      }

      render() {
        return <WrappedComponent {...this.props} />;
      }
    };
  }

  const HelloWorld = () => <h1>Hello, world!</h1>;
  const HelloWorldWithLogger = withLogger(HelloWorld);
  ```

### **2. Render Props**

- **Description:** A pattern for sharing code between React components using a prop whose value is a function.
- **Example:**
  ```javascript
  class MouseTracker extends React.Component {
    state = { x: 0, y: 0 };

    handleMouseMove = (event) => {
      this.setState({
        x: event.clientX,
        y: event.clientY
      });
    };

    render() {
      return (
        <div onMouseMove={this.handleMouseMove}>
          {this.props.render(this.state)}
        </div>
      );
    }
  }

  function App() {
    return (
      <MouseTracker render={({ x, y }) => (
        <h1>Mouse position: ({x}, {y})</h1>
      )} />
    );
  }
  ```

### **3. Error Boundaries**

- **Description:** Components that catch JavaScript errors anywhere in their child component tree and log those errors, and display a fallback UI.
- **Example:**
  ```javascript
  class ErrorBoundary extends React.Component {
    constructor(props) {
      super(props);
      this.state = { hasError: false };
    }

    static getDerivedStateFromError() {
      return { hasError: true };
    }

    componentDidCatch(error, info) {
      console.error("Error caught by ErrorBoundary:", error, info);
    }

    render() {
      if (this.state.hasError) {
        return <h1>Something went wrong.</h1>;
      }

      return this.props.children;
    }
  }

  function MyComponent() {
    throw new Error('Oops!');
    return <div>My Component</div>;
  }

  function App() {
    return (
      <ErrorBoundary>
        <MyComponent />
      </ErrorBoundary>
    );
  }
  ```

### **4. React.memo**

- **Description:** A higher-order component that prevents unnecessary re-renders of function components by memoizing their output.
- **Example:**
  ```javascript
  const MyComponent = React.memo(function MyComponent({ value }) {
    console.log('Rendering:', value);
    return <div>{value}</div>;
  });

  function App() {
    const [count, setCount] = React.useState(0);
    return (
      <div>
        <button onClick={() => setCount(count + 1)}>Increment</button>
        <MyComponent value={count} />
      </div>
    );
  }
  ```

### **5. Lazy Loading and Code Splitting**

- **Description:** Techniques to split your code into smaller chunks that can be loaded on demand, improving performance.
- **Example:**
  ```javascript
  const OtherComponent = React.lazy(() => import('./OtherComponent'));

  function App() {
    return (
      <React.Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </React.Suspense>
    );
  }
  ```

### **6. Server-Side Rendering (SSR)**

- **Description:** The process of rendering your React components on the server and sending the fully-rendered page to the client.
- **Example:**
  ```javascript
  // server.js
  import express from 'express';
  import React from 'react';
  import ReactDOMServer from 'react-dom/server';
  import App from './App';

  const app = express();

  app.get('/', (req, res) => {
    const appHtml = ReactDOMServer.renderToString(<App />);
    res.send(`
      <!DOCTYPE html>
      <html>
        <head>
          <title>Server-Side Rendering</title>
        </head>
        <body>
          <div id="root">${appHtml}</div>
          <script src="/static/bundle.js"></script>
        </body>
      </html>
    `);
  });

  app.listen(3000, () => console.log('Server running on port 3000'));
  ```

### **7. Context API with useReducer**

- **Description:** Use `useReducer` hook with Context API for more complex state management.
- **Example:**
  ```javascript
  const CountContext = React.createContext();

  function countReducer(state, action) {
    switch (action.type) {
      case 'increment':
        return { count: state.count + 1 };
      case 'decrement':
        return { count: state.count - 1 };
      default:
        throw new Error();
    }
  }

  function CountProvider({ children }) {
    const [state, dispatch] = React.useReducer(countReducer, { count: 0 });

    return (
      <CountContext.Provider value={{ state, dispatch }}>
        {children}
      </CountContext.Provider>
    );
  }

  function Counter() {
    const { state, dispatch } = React.useContext(CountContext);
    return (
      <div>
        <p>Count: {state.count}</p>
        <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
        <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
      </div>
    );
  }

  function App() {
    return (
      <CountProvider>
        <Counter />
      </CountProvider>
    );
  }
  ```

## **8. Performance Optimization**

### **Description**
- **Memoization:** Use `React.memo`, `useMemo`, and `useCallback` to optimize performance.
- **Example:**
  ```javascript
  const ExpensiveComponent = React.memo(function ExpensiveComponent({ value }) {
    return <div>{value}</div>;
  });

  function App() {
    const [count, setCount] = React.useState(0);
    const memoizedValue = React.useMemo(() => computeExpensiveValue(count), [count]);

    return (
      <div>
        <button onClick={() => setCount(count + 1)}>Increment</button>
        <ExpensiveComponent value={memoizedValue} />
      </div>
    );
  }
  ```
