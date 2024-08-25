# **JavaScript API Development Cheatsheet**

## **1. Introduction**

### **What is an API?**
- **Description:** An Application Programming Interface (API) allows different software applications to communicate with each other. In JavaScript, APIs are often used to interact with backend services and external data sources.

## **2. Fetch API**

### **Basic Fetch Request**
- **Description:** Use the Fetch API to make network requests and handle responses.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

### **POST Request with Fetch**
- **Description:** Send data to a server using the POST method.
  ```javascript
  fetch('https://api.example.com/submit', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ name: 'John', age: 30 })
  })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

## **3. Axios**

### **Basic Axios Request**
- **Description:** Use Axios, a popular HTTP client library, for making API requests.
  ```javascript
  const axios = require('axios');

  axios.get('https://api.example.com/data')
    .then(response => console.log(response.data))
    .catch(error => console.error('Error:', error));
  ```

### **POST Request with Axios**
- **Description:** Send data to a server using the POST method with Axios.
  ```javascript
  axios.post('https://api.example.com/submit', {
    name: 'John',
    age: 30
  })
    .then(response => console.log(response.data))
    .catch(error => console.error('Error:', error));
  ```

## **4. Asynchronous JavaScript**

### **Using Async/Await**
- **Description:** Simplify asynchronous code with async/await.
  ```javascript
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  fetchData();
  ```

## **5. Handling Responses**

### **Checking Response Status**
- **Description:** Check if a response is successful before processing it.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

### **Handling JSON**
- **Description:** Convert API responses to JSON format.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => {
      console.log(data);
      // Access specific properties
      console.log(data.property);
    })
    .catch(error => console.error('Error:', error));
  ```

## **6. Error Handling**

### **Handling Network Errors**
- **Description:** Catch and handle errors in API requests.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

### **Handling API Errors**
- **Description:** Check for and handle API-specific errors.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => {
      if (data.error) {
        throw new Error(data.error);
      }
      console.log(data);
    })
    .catch(error => console.error('Error:', error));
  ```

## **7. CORS (Cross-Origin Resource Sharing)**

### **Understanding CORS**
- **Description:** CORS is a security feature that restricts how resources on a web page can be requested from another domain.
  - **Server Configuration:** Ensure the server is configured to allow requests from your domain.
  - **Handling CORS Errors:** Ensure proper headers are set:
    ```javascript
    headers: {
      'Access-Control-Allow-Origin': '*'
    }
    ```

## **8. Authentication**

### **Using Tokens**
- **Description:** Send authentication tokens in headers to access protected routes.
  ```javascript
  fetch('https://api.example.com/protected', {
    headers: {
      'Authorization': 'Bearer your-token-here'
    }
  })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

### **Basic Authentication**
- **Description:** Use Basic Authentication by sending a base64-encoded username and password.
  ```javascript
  const username = 'user';
  const password = 'pass';
  const credentials = btoa(`${username}:${password}`);

  fetch('https://api.example.com/secure', {
    headers: {
      'Authorization': `Basic ${credentials}`
    }
  })
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```

## **9. API Documentation**

### **Generating API Documentation**
- **Description:** Document your API using tools like Swagger (OpenAPI).
  - **Swagger UI:** Provides interactive API documentation.
  - **Setup Swagger:** 
    - Add comments to your code.
    - Generate documentation with tools like [Swagger Editor](https://editor.swagger.io/).

## **10. Error Handling in API Responses**

### **Handling Different Status Codes**
- **Description:** React to different HTTP status codes appropriately.
  ```javascript
  fetch('https://api.example.com/data')
    .then(response => {
      switch (response.status) {
        case 200:
          return response.json();
        case 404:
          throw new Error('Resource not found');
        case 500:
          throw new Error('Server error');
        default:
          throw new Error('Unknown error');
      }
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
  ```