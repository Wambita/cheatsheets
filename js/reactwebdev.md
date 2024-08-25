
# **React.js Website Development Cheatsheet**

## **1. Introduction**

-  comprehensive React.js cheatsheet that covers concepts and practices for building a React website with API calls, server-side rendering (SSR), routing, and other essential features.

### **What is React?**
- **Description:** A JavaScript library for building user interfaces, primarily for single-page applications.
- **Installation:**
  ```bash
  npx create-react-app my-app
  cd my-app
  npm start
  ```

## **2. Core Concepts**

### **Components**
- **Function Components:** Stateless and functional components.
  ```javascript
  function MyComponent() {
    return <h1>Hello World</h1>;
  }
  ```
- **Class Components:** Stateful components with lifecycle methods.
  ```javascript
  class MyComponent extends React.Component {
    render() {
      return <h1>Hello World</h1>;
    }
  }
  ```

### **JSX (JavaScript XML)**
- **Description:** A syntax extension for writing HTML-like code in JavaScript.
  ```javascript
  const element = <h1>Hello, world!</h1>;
  ```

### **Props and State**
- **Props:** Immutable data passed from parent to child components.
  ```javascript
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```
- **State:** Mutable data that changes over time within a component.
  ```javascript
  function Counter() {
    const [count, setCount] = React.useState(0);
    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  }
  ```

## **3. API Calls**

### **Fetching Data**
- **Description:** Use `fetch` or `axios` to call APIs and handle data.
- **Example with `fetch`:**
  ```javascript
  function DataFetcher() {
    const [data, setData] = React.useState(null);

    React.useEffect(() => {
      fetch('https://api.example.com/data')
        .then(response => response.json())
        .then(data => setData(data));
    }, []);

    return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
  }
  ```

### **Using Axios**
- **Installation:**
  ```bash
  npm install axios
  ```
- **Example:**
  ```javascript
  import axios from 'axios';

  function DataFetcher() {
    const [data, setData] = React.useState(null);

    React.useEffect(() => {
      axios.get('https://api.example.com/data')
        .then(response => setData(response.data));
    }, []);

    return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
  }
  ```

## **4. Routing with React Router**

### **Installation**
- **Description:** A library for handling routing in React applications.
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

## **5. Server-Side Rendering (SSR)**

### **Description**
- **Definition:** Rendering React components on the server and sending the HTML to the client.
  
### **Setup with Express**
- **Installation:**
  ```bash
  npm install express react react-dom
  ```
- **Server Code Example:**
  ```javascript
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

### **Client-Side Hydration**
- **Example:**
  ```javascript
  import React from 'react';
  import ReactDOM from 'react-dom';
  import App from './App';

  ReactDOM.hydrate(<App />, document.getElementById('root'));
  ```

## **6. Advanced Concepts**

### **Higher-Order Components (HOCs)**
- **Description:** A pattern for reusing component logic.
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
  ```

### **Render Props**
- **Description:** A pattern for sharing code between components using a prop that is a function.
- **Example:**
  ```javascript
  class MouseTracker extends React.Component {
    state = { x: 0, y: 0 };
    handleMouseMove = (event) => {
      this.setState({ x: event.clientX, y: event.clientY });
    };
    render() {
      return <div onMouseMove={this.handleMouseMove}>{this.props.render(this.state)}</div>;
    }
  }
  ```

### **Error Boundaries**
- **Description:** Components that catch JavaScript errors in their child component tree.
- **Example:**
  ```javascript
  class ErrorBoundary extends React.Component {
    state = { hasError: false };
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
  ```

### **React.memo**
- **Description:** Prevents unnecessary re-renders of function components.
- **Example:**
  ```javascript
  const MyComponent = React.memo(function MyComponent({ value }) {
    return <div>{value}</div>;
  });
  ```

### **Lazy Loading and Code Splitting**
- **Description:** Techniques to split your code into smaller chunks for improved performance.
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

### **Context API with useReducer**
- **Description:** Manage complex state logic using Context API and `useReducer`.
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

## **7. Testing**

### **Unit Testing with Jest and React Testing Library**
- **Description:** Test individual components and logic.
- **Installation:**
  ```bash
  npm install --save-dev @testing-library/react @testing-library/jest-dom jest
  ```
- **Example:**
  ```javascript
  import { render, screen, fireEvent } from '@testing-library/react';
  import Counter from './Counter';

  test('increments count', () => {
    render(<Counter />);
    fireEvent.click(screen.getByText(/increment/i));
    expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
  });
  ```
