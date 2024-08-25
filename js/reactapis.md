# **React API Integration Cheatsheet**

## **1. Introduction**

### **What is an API?**
- **Description:** An Application Programming Interface (API) allows different software applications to communicate with each other. In React, APIs are commonly used to fetch data from backend services and interact with external resources.

## **2. Fetching Data in React**

### **Using `fetch`**
- **Description:** Use the Fetch API to make network requests.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function FetchExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      fetch('https://api.example.com/data')
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          setData(data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data found</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default FetchExample;
  ```

### **Using Axios**
- **Description:** Axios is a popular HTTP client library for making requests.
  ```javascript
  import React, { useEffect, useState } from 'react';
  import axios from 'axios';

  function AxiosExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      axios.get('https://api.example.com/data')
        .then(response => {
          setData(response.data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data found</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default AxiosExample;
  ```

## **3. Handling API Responses**

### **Checking Response Status**
- **Description:** Handle different response statuses appropriately.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function StatusCheckExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      fetch('https://api.example.com/data')
        .then(response => {
          if (!response.ok) {
            if (response.status === 404) {
              throw new Error('Resource not found');
            } else if (response.status === 500) {
              throw new Error('Server error');
            } else {
              throw new Error('Unknown error');
            }
          }
          return response.json();
        })
        .then(data => {
          setData(data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default StatusCheckExample;
  ```

## **4. Handling Authentication**

### **Using Tokens**
- **Description:** Include authentication tokens in your requests to access protected endpoints.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function AuthExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      fetch('https://api.example.com/protected', {
        headers: {
          'Authorization': 'Bearer your-token-here'
        }
      })
        .then(response => response.json())
        .then(data => {
          setData(data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default AuthExample;
  ```

### **Basic Authentication**
- **Description:** Use Basic Authentication by sending encoded credentials.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function BasicAuthExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    const username = 'user';
    const password = 'pass';
    const credentials = btoa(`${username}:${password}`);

    useEffect(() => {
      fetch('https://api.example.com/secure', {
        headers: {
          'Authorization': `Basic ${credentials}`
        }
      })
        .then(response => response.json())
        .then(data => {
          setData(data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default BasicAuthExample;
  ```

## **5. Error Handling**

### **Handling Fetch Errors**
- **Description:** Properly handle errors that occur during fetch requests.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function ErrorHandlingExample() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      fetch('https://api.example.com/data')
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          setData(data);
          setLoading(false);
        })
        .catch(error => {
          setError(error);
          setLoading(false);
        });
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default ErrorHandlingExample;
  ```

## **6. API Integration with React Hooks**

### **Using `useEffect` for Data Fetching**
- **Description:** Fetch data and handle side effects with the `useEffect` hook.
  ```javascript
  import React, { useEffect, useState } from 'react';

  function DataFetchComponent() {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      async function fetchData() {
        try {
          const response = await fetch('https://api.example.com/data');
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          const result = await response.json();
          setData(result);
        } catch (error) {
          setError(error);
        } finally {
          setLoading(false);
        }
      }

      fetchData();
    }, []);

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }

  export default DataFetchComponent;
  ```

## **7. API Integration with Context API**

### **Using Context for Global Data**
- **Description:** Share API data across components using React Context.
  ```javascript
  import React, { createContext, useContext, useEffect, useState } from 'react';

  const DataContext = createContext();

  export function DataProvider({ children }) {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      async function fetchData() {
        try {
          const response = await fetch('https://api.example.com/data');
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          const result = await response.json();
          setData(result);
        }

 catch (error) {
          setError(error);
        } finally {
          setLoading(false);
        }
      }

      fetchData();
    }, []);

    return (
      <DataContext.Provider value={{ data, loading, error }}>
        {children}
      </DataContext.Provider>
    );
  }

  export function useData() {
    return useContext(DataContext);
  }

  function DisplayComponent() {
    const { data, loading, error } = useData();

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    if (!data) return <p>No data available</p>;

    return <pre>{JSON.stringify(data, null, 2)}</pre>;
  }
  ```

## **8. Server-Side Rendering (SSR) with React**

### **Using Next.js for SSR**
- **Description:** Next.js provides SSR capabilities for React applications.
  ```javascript
  import React from 'react';
  import axios from 'axios';

  function HomePage({ data }) {
    return (
      <div>
        <h1>Server-Side Rendered Data</h1>
        <pre>{JSON.stringify(data, null, 2)}</pre>
      </div>
    );
  }

  export async function getServerSideProps() {
    const res = await axios.get('https://api.example.com/data');
    const data = res.data;

    return { props: { data } };
  }

  export default HomePage;
  ```

## **9. Routing with React Router**

### **Setting Up Routes**
- **Description:** Use React Router for client-side routing.
  ```javascript
  import React from 'react';
  import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

  function Home() {
    return <h2>Home</h2>;
  }

  function About() {
    return <h2>About</h2>;
  }

  function App() {
    return (
      <Router>
        <Switch>
          <Route path="/" exact component={Home} />
          <Route path="/about" component={About} />
        </Switch>
      </Router>
    );
  }

  export default App;
  ```

## **10. Handling API Errors**

### **Custom Error Pages**
- **Description:** Display custom error pages for different types of errors.
  ```javascript
  import React from 'react';

  function ErrorPage({ error }) {
    return (
      <div>
        <h1>Error</h1>
        <p>{error.message}</p>
      </div>
    );
  }

  export default ErrorPage;
  ```
