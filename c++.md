# **C++ Programming Cheatsheet**

## **1. Basics of C++ Programming**

### **1.1. Hello World Program**
- **Description:** The simplest C++ program that outputs "Hello, World!".
  ```cpp
  #include <iostream>

  int main() {
      std::cout << "Hello, World!" << std::endl;
      return 0;
  }
  ```

### **1.2. Variables**
- **Description:** Storage locations with a name and type to hold data.
  ```cpp
  int age = 25;        // Integer
  double height = 5.9; // Floating-point number
  char initial = 'A';  // Character
  ```

### **1.3. Data Types**
- **Description:** Defines the type of data a variable can hold.
  - **`int`**: Integer numbers.
    ```cpp
    int age = 30;
    std::cout << "Age: " << age << std::endl;  // Outputs: Age: 30
    ```
  - **`double`**: Double precision floating-point numbers.
    ```cpp
    double pi = 3.1415926535;
    std::cout << "Pi: " << pi << std::endl;  // Outputs: Pi: 3.1415926535
    ```
  - **`char`**: Single characters.
    ```cpp
    char grade = 'A';
    std::cout << "Grade: " << grade << std::endl;  // Outputs: Grade: A
    ```

### **1.4. Operators**
- **Description:** Symbols that perform operations on variables and values.
  - **Arithmetic Operators:**
    ```cpp
    int a = 10, b = 5;
    std::cout << "Sum: " << (a + b) << std::endl;      // Outputs: Sum: 15
    std::cout << "Difference: " << (a - b) << std::endl; // Outputs: Difference: 5
    std::cout << "Product: " << (a * b) << std::endl;  // Outputs: Product: 50
    std::cout << "Quotient: " << (a / b) << std::endl; // Outputs: Quotient: 2
    std::cout << "Remainder: " << (a % b) << std::endl; // Outputs: Remainder: 0
    ```
  - **Comparison Operators:**
    ```cpp
    int x = 10, y = 20;
    std::cout << "x == y: " << (x == y) << std::endl;  // Outputs: x == y: 0 (false)
    std::cout << "x != y: " << (x != y) << std::endl;  // Outputs: x != y: 1 (true)
    std::cout << "x > y: " << (x > y) << std::endl;    // Outputs: x > y: 0 (false)
    std::cout << "x < y: " << (x < y) << std::endl;    // Outputs: x < y: 1 (true)
    ```
  - **Logical Operators:**
    ```cpp
    bool p = true, q = false;
    std::cout << "p && q: " << (p && q) << std::endl;  // Outputs: p && q: 0 (false)
    std::cout << "p || q: " << (p || q) << std::endl;  // Outputs: p || q: 1 (true)
    std::cout << "!p: " << (!p) << std::endl;          // Outputs: !p: 0 (false)
    ```

### **1.5. Control Structures**
- **Description:** Direct the flow of execution based on conditions.
  - **`if` Statement:**
    ```cpp
    int age = 20;
    if (age > 18) {
        std::cout << "Adult" << std::endl; // Outputs: Adult
    }
    ```
  - **`for` Loop:**
    ```cpp
    for (int i = 0; i < 5; i++) {
        std::cout << i << std::endl; // Outputs: 0 1 2 3 4
    }
    ```
  - **`while` Loop:**
    ```cpp
    int i = 0;
    while (i < 5) {
        std::cout << i << std::endl; // Outputs: 0 1 2 3 4
        i++;
    }
    ```

### **1.6. Functions**
- **Description:** Blocks of code that perform a specific task and can be reused.
  ```cpp
  int add(int a, int b) {
      return a + b;
  }

  int main() {
      int sum = add(3, 5);
      std::cout << "Sum: " << sum << std::endl; // Outputs: Sum: 8
      return 0;
  }
  ```

### **1.7. Arrays**
- **Description:** Collection of variables of the same type.
  ```cpp
  int numbers[5] = {1, 2, 3, 4, 5};
  std::cout << numbers[2] << std::endl;  // Outputs: 3
  ```

### **1.8. Pointers**
- **Description:** Variables that store memory addresses.
  ```cpp
  int value = 10;
  int *ptr = &value;  // Pointer to value
  std::cout << *ptr << std::endl;  // Outputs: 10
  ```

### **1.9. Strings**
- **Description:** Arrays of characters ending with a null character `'\0'`.
  ```cpp
  std::string name = "John Doe";
  std::cout << name << std::endl;  // Outputs: John Doe
  ```

### **1.10. Classes and Objects**
- **Description:** Define data types with attributes and methods.
  ```cpp
  class Person {
  public:
      std::string name;
      int age;
      
      void introduce() {
          std::cout << "Hi, I'm " << name << " and I'm " << age << " years old." << std::endl;
      }
  };

  int main() {
      Person person1;
      person1.name = "Alice";
      person1.age = 30;
      person1.introduce(); // Outputs: Hi, I'm Alice and I'm 30 years old.
      return 0;
  }
  ```

## **2. Advanced C++ Programming**

### **2.1. Dynamic Memory Allocation**
- **Description:** Allocate and deallocate memory at runtime using `new` and `delete`.
  ```cpp
  int *array = new int[10];  // Allocate memory for 10 integers
  // Use the array...
  delete[] array;  // Free allocated memory
  ```

### **2.2. File I/O**
- **Description:** Read from and write to files.
  ```cpp
  #include <fstream>
  
  int main() {
      std::ofstream file("example.txt");
      if (file.is_open()) {
          file << "Hello, File!" << std::endl;
          file.close();
      }
  
      std::ifstream file2("example.txt");
      std::string line;
      if (file2.is_open()) {
          while (getline(file2, line)) {
              std::cout << line << std::endl;  // Outputs: Hello, File!
          }
          file2.close();
      }
      return 0;
  }
  ```

### **2.3. Templates**
- **Description:** Write generic functions and classes that work with any data type.
  ```cpp
  template <typename T>
  T add(T a, T b) {
      return a + b;
  }

  int main() {
      std::cout << add(3, 5) << std::endl;     // Outputs: 8 (int)
      std::cout << add(3.5, 2.5) << std::endl; // Outputs: 6.0 (double)
      return 0;
  }
  ```

### **2.4. Inheritance**
- **Description:** Create new classes based on existing classes.
  ```cpp
  class Animal {
  public:
      void eat() {
          std::cout << "Eating..." << std::endl;
      }
  };

  class Dog : public Animal {
  public:
      void bark() {
          std::cout << "Woof!" << std::endl;
      }
  };

  int main() {
      Dog dog;
      dog.eat();  // Outputs: Eating...
      dog.bark(); // Outputs: Woof!
      return 0;
  }
  ```

### **2.5. Polymorphism**
- **Description:** Allow different classes to be treated as instances of the same class through a common interface.
  ```cpp
  class Base {
  public:
      virtual void show() {
          std::cout << "Base class" << std::endl;
      }
  };

  class Derived : public Base {
  public:
      void show() override {
          std::cout << "Derived class" << std::endl;
      }
 

 };

  int main() {
      Base *bptr;
      Derived d;
      bptr = &d;
      bptr->show();  // Outputs: Derived class
      return 0;
  }
  ```

### **2.6. Exception Handling**
- **Description:** Handle runtime errors using `try`, `catch`, and `throw`.
  ```cpp
  int divide(int a, int b) {
      if (b == 0) throw std::runtime_error("Division by zero");
      return a / b;
  }

  int main() {
      try {
          int result = divide(10, 0);
          std::cout << "Result: " << result << std::endl;
      } catch (const std::runtime_error &e) {
          std::cout << "Error: " << e.what() << std::endl; // Outputs: Error: Division by zero
      }
      return 0;
  }
  ```

### **2.7. Smart Pointers**
- **Description:** Use smart pointers like `std::unique_ptr` and `std::shared_ptr` for automatic memory management.
  ```cpp
  #include <memory>
  #include <iostream>

  int main() {
      std::unique_ptr<int> ptr1 = std::make_unique<int>(10);
      std::cout << "Value: " << *ptr1 << std::endl;  // Outputs: Value: 10

      std::shared_ptr<int> ptr2 = std::make_shared<int>(20);
      std::cout << "Value: " << *ptr2 << std::endl;  // Outputs: Value: 20
      return 0;
  }
  ```

### **2.8. Lambda Expressions**
- **Description:** Define anonymous functions for concise code.
  ```cpp
  #include <iostream>

  int main() {
      auto add = [](int a, int b) { return a + b; };
      std::cout << "Sum: " << add(3, 5) << std::endl; // Outputs: Sum: 8
      return 0;
  }
  ```

### **2.9. STL (Standard Template Library)**
- **Description:** Collection of template classes and functions including vectors, maps, and algorithms.
  - **Vectors:**
    ```cpp
    #include <vector>
    #include <iostream>

    int main() {
        std::vector<int> vec = {1, 2, 3, 4, 5};
        for (int num : vec) {
            std::cout << num << std::endl;  // Outputs: 1 2 3 4 5
        }
        return 0;
    }
    ```
  - **Maps:**
    ```cpp
    #include <map>
    #include <iostream>

    int main() {
        std::map<std::string, int> ages;
        ages["Alice"] = 30;
        ages["Bob"] = 25;

        for (const auto &pair : ages) {
            std::cout << pair.first << " is " << pair.second << " years old." << std::endl;
            // Outputs: Alice is 30 years old.
            // Outputs: Bob is 25 years old.
        }
        return 0;
    }
    ```

### **2.10. File Handling**
- **Description:** Read from and write to files using `fstream`.
  ```cpp
  #include <fstream>
  #include <iostream>

  int main() {
      std::ofstream outFile("output.txt");
      if (outFile.is_open()) {
          outFile << "Hello, File!" << std::endl;
          outFile.close();
      }

      std::ifstream inFile("output.txt");
      std::string line;
      if (inFile.is_open()) {
          while (getline(inFile, line)) {
              std::cout << line << std::endl;  // Outputs: Hello, File!
          }
          inFile.close();
      }
      return 0;
  }
  ```
