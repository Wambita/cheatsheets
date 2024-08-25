# **Rust Programming Cheatsheet**

## **1. Basics of Rust Programming**

### **1.1. Hello World Program**
- **Description:** The simplest Rust program that outputs "Hello, World!".
  ```rust
  fn main() {
      println!("Hello, World!");
  }
  ```

### **1.2. Variables**
- **Description:** Store data values. By default, variables are immutable but can be made mutable with `mut`.
  ```rust
  let x = 5;         // Immutable variable
  let mut y = 10;    // Mutable variable
  y += 5;
  println!("x: {}, y: {}", x, y); // Outputs: x: 5, y: 15
  ```

### **1.3. Data Types**
- **Description:** Defines the type of data a variable can hold.
  - **Integer Types:**
    ```rust
    let a: i32 = 100;  // 32-bit integer
    let b: u64 = 1000; // 64-bit unsigned integer
    ```
  - **Floating-Point Types:**
    ```rust
    let pi: f64 = 3.14159; // 64-bit floating-point number
    ```
  - **Boolean Type:**
    ```rust
    let is_active: bool = true;
    ```
  - **Character Type:**
    ```rust
    let letter: char = 'A';
    ```

### **1.4. Operators**
- **Description:** Symbols that perform operations on variables and values.
  - **Arithmetic Operators:**
    ```rust
    let sum = 5 + 10;
    let diff = 15 - 5;
    let prod = 4 * 2;
    let quotient = 20 / 4;
    let remainder = 10 % 3;
    ```
  - **Comparison Operators:**
    ```rust
    let a = 10;
    let b = 20;
    assert_eq!(a == b, false);
    assert_eq!(a < b, true);
    ```
  - **Logical Operators:**
    ```rust
    let p = true;
    let q = false;
    assert_eq!(p && q, false);
    assert_eq!(p || q, true);
    assert_eq!(!p, false);
    ```

### **1.5. Control Structures**
- **Description:** Direct the flow of execution based on conditions.
  - **`if` Statement:**
    ```rust
    let age = 20;
    if age > 18 {
        println!("Adult");
    }
    ```
  - **`for` Loop:**
    ```rust
    for i in 0..5 {
        println!("{}", i); // Outputs: 0 1 2 3 4
    }
    ```
  - **`while` Loop:**
    ```rust
    let mut i = 0;
    while i < 5 {
        println!("{}", i); // Outputs: 0 1 2 3 4
        i += 1;
    }
    ```

### **1.6. Functions**
- **Description:** Blocks of code that perform a specific task and can be reused.
  ```rust
  fn add(a: i32, b: i32) -> i32 {
      a + b
  }

  fn main() {
      let sum = add(3, 5);
      println!("Sum: {}", sum); // Outputs: Sum: 8
  }
  ```

### **1.7. Structs**
- **Description:** Custom data types that can contain multiple values.
  ```rust
  struct Person {
      name: String,
      age: u32,
  }

  fn main() {
      let person = Person {
          name: String::from("Alice"),
          age: 30,
      };
      println!("Name: {}, Age: {}", person.name, person.age); // Outputs: Name: Alice, Age: 30
  }
  ```

### **1.8. Enums**
- **Description:** Define a type that can be one of several variants.
  ```rust
  enum Color {
      Red,
      Green,
      Blue,
  }

  fn main() {
      let color = Color::Green;
      match color {
          Color::Red => println!("Red"),
          Color::Green => println!("Green"),
          Color::Blue => println!("Blue"),
      }
  }
  ```

### **1.9. Strings**
- **Description:** Collections of characters.
  ```rust
  let mut s = String::from("Hello");
  s.push_str(", World!");
  println!("{}", s); // Outputs: Hello, World!
  ```

### **1.10. Error Handling**
- **Description:** Handle errors using `Result` and `Option` types.
  - **`Result` Type:**
    ```rust
    fn divide(a: i32, b: i32) -> Result<i32, &'static str> {
        if b == 0 {
            Err("Cannot divide by zero")
        } else {
            Ok(a / b)
        }
    }

    fn main() {
        match divide(10, 0) {
            Ok(result) => println!("Result: {}", result),
            Err(e) => println!("Error: {}", e),
        }
    }
    ```
  - **`Option` Type:**
    ```rust
    fn get_number() -> Option<i32> {
        Some(42)
    }

    fn main() {
        match get_number() {
            Some(num) => println!("Number: {}", num),
            None => println!("No number found"),
        }
    }
    ```

## **2. Advanced Rust Programming**

### **2.1. Ownership and Borrowing**
- **Description:** Rust's memory management system ensures safety without a garbage collector.
  - **Ownership:**
    ```rust
    fn main() {
        let s1 = String::from("hello");
        let s2 = s1; // Ownership moves from s1 to s2
        // println!("{}", s1); // Error: use of possibly-dangling reference
    }
    ```
  - **Borrowing:**
    ```rust
    fn print_length(s: &String) {
        println!("Length: {}", s.len());
    }

    fn main() {
        let s = String::from("hello");
        print_length(&s); // Pass by reference
        println!("Original: {}", s); // Outputs: Original: hello
    }
    ```

### **2.2. Lifetimes**
- **Description:** Ensure that references are valid as long as they are needed.
  ```rust
  fn longest<'a>(s1: &'a str, s2: &'a str) -> &'a str {
      if s1.len() > s2.len() {
          s1
      } else {
          s2
      }
  }

  fn main() {
      let s1 = String::from("short");
      let s2 = String::from("longer");
      let result = longest(&s1, &s2);
      println!("Longest: {}", result); // Outputs: Longest: longer
  }
  ```

### **2.3. Traits**
- **Description:** Define shared behavior across types.
  ```rust
  trait Speak {
      fn speak(&self);
  }

  struct Dog;
  struct Cat;

  impl Speak for Dog {
      fn speak(&self) {
          println!("Woof!");
      }
  }

  impl Speak for Cat {
      fn speak(&self) {
          println!("Meow!");
      }
  }

  fn main() {
      let dog = Dog;
      let cat = Cat;
      dog.speak(); // Outputs: Woof!
      cat.speak(); // Outputs: Meow!
  }
  ```

### **2.4. Concurrency**
- **Description:** Perform concurrent operations safely using threads and channels.
  - **Threads:**
    ```rust
    use std::thread;

    fn main() {
        let handle = thread::spawn(|| {
            for i in 1..10 {
                println!("Spawned thread: {}", i);
            }
        });

        handle.join().unwrap();
    }
    ```
  - **Channels:**
    ```rust
    use std::sync::mpsc;
    use std::thread;

    fn main() {
        let (tx, rx) = mpsc::channel();
        thread::spawn(move || {
            tx.send("Hello from the thread!").unwrap();
        });

        let received = rx.recv().unwrap();
        println!("{}", received); // Outputs: Hello from the thread!
    }
    ```

### **2.5. Async Programming**
- **Description:** Perform asynchronous operations with `async`/`await` syntax.
  ```rust
  use std::time::Duration;
  use tokio;

  #[tokio::main]
  async fn main() {
      let result = async_function().await;
      println!("{}", result);
  }

  async fn async_function() -> String {
      tokio::time::sleep(Duration::from_secs(2)).await;
      "Async result".to_string()
  }
  ```

### **2.6. Macros**
- **Description:** Define code that generates other code.
  ```rust
  macro_rules! say_hello {
      () => {
          println!("Hello, Macro!");
      };
  }

  fn main() {
      say_hello!(); // Outputs: Hello, Macro!
  }
  ```

### **2.7. Modules**
- **Description

:** Organize code into separate files or modules.
  ```rust
  // src/main.rs
  mod my_module;

  fn main() {
      my_module::hello();
  }

  // src/my_module.rs
  pub fn hello() {
      println!("Hello from my_module!");
  }
  ```

### **2.8. Error Handling with `Result` and `Option`**
- **Description:** Advanced error handling using combinators and pattern matching.
  ```rust
  fn read_file() -> Result<String, std::io::Error> {
      let content = std::fs::read_to_string("file.txt")?;
      Ok(content)
  }

  fn main() {
      match read_file() {
          Ok(content) => println!("File content: {}", content),
          Err(e) => println!("Error reading file: {}", e),
      }
  }
  ```

### **2.9. Unsafe Rust**
- **Description:** Bypass Rust’s safety guarantees for performance-critical code.
  ```rust
  unsafe {
      let x: i32 = 42;
      let y: *const i32 = &x;
      println!("Value: {}", *y); // Outputs: Value: 42
  }
  ```

### **2.10. Custom Derive Macros**
- **Description:** Automatically implement traits for custom types using procedural macros.
  ```rust
  #[derive(Debug, Clone)]
  struct Person {
      name: String,
      age: u32,
  }

  fn main() {
      let person = Person {
          name: String::from("Alice"),
          age: 30,
      };
      println!("{:?}", person); // Outputs: Person { name: "Alice", age: 30 }
  }
  ```