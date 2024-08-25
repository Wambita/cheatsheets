# **Python Programming Cheatsheet**

## **1. Basics of Python Programming**

### **1.1. Hello World Program**
- **Description:** The simplest Python program that outputs "Hello, World!".
  ```python
  print("Hello, World!")
  ```

### **1.2. Variables**
- **Description:** Store data values. Variables are dynamically typed in Python.
  ```python
  x = 5          # Integer
  y = 3.14       # Float
  name = "Alice" # String
  ```

### **1.3. Data Types**
- **Description:** Defines the type of data a variable can hold.
  - **Integer:**
    ```python
    age = 30
    ```
  - **Float:**
    ```python
    price = 19.99
    ```
  - **String:**
    ```python
    greeting = "Hello"
    ```
  - **Boolean:**
    ```python
    is_active = True
    ```

### **1.4. Operators**
- **Description:** Symbols that perform operations on variables and values.
  - **Arithmetic Operators:**
    ```python
    sum = 5 + 3
    difference = 5 - 3
    product = 5 * 3
    quotient = 5 / 3
    remainder = 5 % 3
    ```
  - **Comparison Operators:**
    ```python
    a = 10
    b = 20
    is_equal = (a == b)   # False
    is_greater = (a > b) # False
    ```
  - **Logical Operators:**
    ```python
    p = True
    q = False
    and_result = p and q # False
    or_result = p or q   # True
    not_result = not p   # False
    ```

### **1.5. Control Structures**
- **Description:** Direct the flow of execution based on conditions.
  - **`if` Statement:**
    ```python
    age = 20
    if age >= 18:
        print("Adult")
    ```
  - **`for` Loop:**
    ```python
    for i in range(5):
        print(i)  # Outputs: 0 1 2 3 4
    ```
  - **`while` Loop:**
    ```python
    i = 0
    while i < 5:
        print(i)  # Outputs: 0 1 2 3 4
        i += 1
    ```

### **1.6. Functions**
- **Description:** Blocks of code that perform a specific task and can be reused.
  ```python
  def add(a, b):
      return a + b

  result = add(3, 5)
  print(result)  # Outputs: 8
  ```

### **1.7. Lists**
- **Description:** Ordered, mutable collections of items.
  ```python
  fruits = ["apple", "banana", "cherry"]
  fruits.append("orange")
  print(fruits)  # Outputs: ['apple', 'banana', 'cherry', 'orange']
  ```

### **1.8. Dictionaries**
- **Description:** Collections of key-value pairs.
  ```python
  person = {"name": "Alice", "age": 30}
  print(person["name"])  # Outputs: Alice
  ```

### **1.9. Strings**
- **Description:** Collections of characters with various methods for manipulation.
  ```python
  s = "Hello, World!"
  print(s.upper())  # Outputs: HELLO, WORLD!
  print(s.lower())  # Outputs: hello, world!
  print(s.replace("World", "Python"))  # Outputs: Hello, Python!
  ```

### **1.10. File Handling**
- **Description:** Read from and write to files.
  - **Write to File:**
    ```python
    with open('output.txt', 'w') as file:
        file.write("Hello, File!")
    ```
  - **Read from File:**
    ```python
    with open('output.txt', 'r') as file:
        content = file.read()
    print(content)  # Outputs: Hello, File!
    ```

## **2. Advanced Python Programming**

### **2.1. List Comprehensions**
- **Description:** Concise way to create lists.
  ```python
  squares = [x**2 for x in range(10)]
  print(squares)  # Outputs: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
  ```

### **2.2. Generators**
- **Description:** Functions that return an iterable set of items, one at a time.
  ```python
  def count_up_to(n):
      count = 1
      while count <= n:
          yield count
          count += 1

  for number in count_up_to(5):
      print(number)  # Outputs: 1 2 3 4 5
  ```

### **2.3. Decorators**
- **Description:** Functions that modify the behavior of other functions or methods.
  ```python
  def my_decorator(func):
      def wrapper():
          print("Something is happening before the function is called.")
          func()
          print("Something is happening after the function is called.")
      return wrapper

  @my_decorator
  def say_hello():
      print("Hello!")

  say_hello()
  ```
  - **Output:**
    ```
    Something is happening before the function is called.
    Hello!
    Something is happening after the function is called.
    ```

### **2.4. Context Managers**
- **Description:** Automatically manage resources.
  ```python
  class FileManager:
      def __enter__(self):
          self.file = open('output.txt', 'w')
          return self.file

      def __exit__(self, exc_type, exc_value, traceback):
          self.file.close()

  with FileManager() as file:
      file.write("Managed resource!")
  ```

### **2.5. Exception Handling**
- **Description:** Handle runtime errors using `try`, `except`, `finally`, and `raise`.
  ```python
  try:
      result = 10 / 0
  except ZeroDivisionError:
      print("Cannot divide by zero")
  finally:
      print("This block always executes")
  ```

### **2.6. Classes and Objects**
- **Description:** Define custom data types using classes.
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name
          self.age = age

      def greet(self):
          print(f"Hello, my name is {self.name} and I am {self.age} years old.")

  person = Person("Alice", 30)
  person.greet()  # Outputs: Hello, my name is Alice and I am 30 years old.
  ```

### **2.7. Inheritance**
- **Description:** Derive new classes from existing ones.
  ```python
  class Animal:
      def speak(self):
          print("Animal sound")

  class Dog(Animal):
      def speak(self):
          print("Woof!")

  dog = Dog()
  dog.speak()  # Outputs: Woof!
  ```

### **2.8. Modules and Packages**
- **Description:** Organize code into separate files and directories.
  - **Module:**
    ```python
    # module.py
    def greet(name):
        return f"Hello, {name}!"
    ```
  - **Package:**
    ```python
    # my_package/__init__.py
    from .module import greet

    # main.py
    from my_package import greet
    print(greet("Alice"))  # Outputs: Hello, Alice!
    ```

### **2.9. Abstract Base Classes (ABCs)**
- **Description:** Define abstract methods that must be implemented by subclasses.
  ```python
  from abc import ABC, abstractmethod

  class Shape(ABC):
      @abstractmethod
      def area(self):
          pass

  class Circle(Shape):
      def __init__(self, radius):
          self.radius = radius

      def area(self):
          return 3.14 * self.radius ** 2

  circle = Circle(5)
  print(circle.area())  # Outputs: 78.5
  ```

### **2.10. Type Hinting**
- **Description:** Provide type hints for function parameters and return values.
  ```python
  def add(a: int, b: int) -> int:
      return a + b

  print(add(5, 3))  # Outputs: 8
  ```
