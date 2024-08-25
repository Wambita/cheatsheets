# **Underscore.js Cheatsheet**

## **1. Overview**

### **What is Underscore.js?**
- **Description:** Underscore.js is a JavaScript library that provides utility functions for common programming tasks, making it easier to work with arrays, objects, and other data types.
- **Installation:**
  ```bash
  npm install underscore
  ```

## **2. Core Functions**

### **1. Arrays**

- **`_.each`**
  - **Description:** Iterates over elements of a collection, executing a callback for each element.
  - **Example:**
    ```javascript
    _.each([1, 2, 3], function(num) {
      console.log(num);
    });
    ```

- **`_.map`**
  - **Description:** Creates a new array with the results of calling a provided function on every element in the calling array.
  - **Example:**
    ```javascript
    const doubled = _.map([1, 2, 3], function(num) {
      return num * 2;
    });
    console.log(doubled); // [2, 4, 6]
    ```

- **`_.filter`**
  - **Description:** Filters elements from an array based on a predicate function.
  - **Example:**
    ```javascript
    const evens = _.filter([1, 2, 3, 4], function(num) {
      return num % 2 === 0;
    });
    console.log(evens); // [2, 4]
    ```

- **`_.reduce`**
  - **Description:** Reduces an array to a single value by applying a function iteratively to each element.
  - **Example:**
    ```javascript
    const sum = _.reduce([1, 2, 3, 4], function(accumulator, num) {
      return accumulator + num;
    }, 0);
    console.log(sum); // 10
    ```

### **2. Objects**

- **`_.keys`**
  - **Description:** Returns an array of the keys of an object.
  - **Example:**
    ```javascript
    const keys = _.keys({ a: 1, b: 2 });
    console.log(keys); // ["a", "b"]
    ```

- **`_.values`**
  - **Description:** Returns an array of the values of an object.
  - **Example:**
    ```javascript
    const values = _.values({ a: 1, b: 2 });
    console.log(values); // [1, 2]
    ```

- **`_.extend`**
  - **Description:** Copies the properties of one or more source objects to a target object.
  - **Example:**
    ```javascript
    const target = { a: 1 };
    const source = { b: 2, c: 3 };
    _.extend(target, source);
    console.log(target); // { a: 1, b: 2, c: 3 }
    ```

- **`_.pick`**
  - **Description:** Creates a shallow copy of an object by picking the specified keys.
  - **Example:**
    ```javascript
    const obj = { a: 1, b: 2, c: 3 };
    const picked = _.pick(obj, ['a', 'c']);
    console.log(picked); // { a: 1, c: 3 }
    ```

### **3. Utility Functions**

- **`_.identity`**
  - **Description:** Returns the first argument passed to it.
  - **Example:**
    ```javascript
    console.log(_.identity('hello')); // "hello"
    ```

- **`_.isEqual`**
  - **Description:** Performs a deep comparison between two values to determine if they are equivalent.
  - **Example:**
    ```javascript
    console.log(_.isEqual({ a: 1 }, { a: 1 })); // true
    console.log(_.isEqual({ a: 1 }, { a: 2 })); // false
    ```

- **`_.random`**
  - **Description:** Returns a random integer between the specified range.
  - **Example:**
    ```javascript
    console.log(_.random(1, 10)); // Random number between 1 and 10
    ```

## **4. Chaining**

### **Description**
- **Definition:** Underscore.js supports method chaining, allowing multiple operations to be performed on the result of previous operations.
- **Example:**
  ```javascript
  const result = _( [1, 2, 3, 4] )
    .filter(num => num % 2 === 0)
    .map(num => num * 2)
    .value();
  
  console.log(result); // [4, 8]
  ```
