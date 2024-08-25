# **JavaScript Concepts Cheatsheet**

## **1. JavaScript Objects**

### **Description**
- **Definition:** Objects are collections of key-value pairs, where keys are strings (or symbols) and values can be of any type.
- **Example:**
  ```javascript
  const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 30,
    greet: function() {
      console.log('Hello, ' + this.firstName);
    }
  };

  console.log(person.firstName); // "John"
  person.greet(); // "Hello, John"
  ```

## **2. Literal Notations**

### **Object Literal**
- **Description:** A concise way to create an object using curly braces.
- **Example:**
  ```javascript
  const car = {
    brand: 'Toyota',
    model: 'Corolla',
    year: 2021
  };
  ```

### **Array Literal**
- **Description:** Creates an array using square brackets.
- **Example:**
  ```javascript
  const fruits = ['Apple', 'Banana', 'Cherry'];
  ```

### **Function Literal**
- **Description:** Defines a function using the `function` keyword.
- **Example:**
  ```javascript
  function add(a, b) {
    return a + b;
  }
  ```

## **3. Constructors**

### **Description**
- **Definition:** Constructors are functions used to create and initialize objects. They are invoked with the `new` keyword.
- **Example:**
  ```javascript
  function Person(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.greet = function() {
      console.log('Hello, ' + this.firstName);
    };
  }

  const person1 = new Person('John', 'Doe', 30);
  person1.greet(); // "Hello, John"
  ```

## **4. Prototypes**

### **Description**
- **Definition:** Every JavaScript object has a prototype, which is another object from which it inherits methods and properties.
- **Example:**
  ```javascript
  function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  // Adding a method to Person's prototype
  Person.prototype.greet = function() {
    console.log('Hello, ' + this.firstName);
  };

  const person1 = new Person('John', 'Doe');
  person1.greet(); // "Hello, John"
  ```

### **Prototype Chain**
- **Description:** The prototype chain is used to implement inheritance in JavaScript. Objects can inherit properties and methods from other objects.
- **Example:**
  ```javascript
  function Animal(name) {
    this.name = name;
  }

  Animal.prototype.speak = function() {
    console.log(this.name + ' makes a noise.');
  };

  function Dog(name) {
    Animal.call(this, name); // Call Animal constructor
  }

  Dog.prototype = Object.create(Animal.prototype); // Inherit from Animal
  Dog.prototype.constructor = Dog;

  const dog = new Dog('Rex');
  dog.speak(); // "Rex makes a noise."
  ```

## **5. Underscore Objects Within Objects**

### **Description**
- **Definition:** Objects can contain other objects as values, allowing for nested structures.
- **Example:**
  ```javascript
  const user = {
    name: 'Jane',
    address: {
      street: '123 Main St',
      city: 'Somewhere',
      postalCode: '12345'
    },
    contact: {
      email: 'jane@example.com',
      phone: '555-555-5555'
    }
  };

  console.log(user.address.city); // "Somewhere"
  console.log(user.contact.email); // "jane@example.com"
  ```

## **6. Event Listeners**

### **Description**
- **Definition:** Event listeners are used to handle events such as clicks, keypresses, and other user interactions.
- **Example:**
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Listener Example</title>
  </head>
  <body>
    <button id="myButton">Click Me</button>

    <script>
      // Add event listener to a button
      document.getElementById('myButton').addEventListener('click', function() {
        alert('Button was clicked!');
      });
    </script>
  </body>
  </html>
  ```
