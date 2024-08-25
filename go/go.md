# **Go Language Cheatsheet**

## **1. Introduction**

### **What is Go?**
- **Description:** Go (or Golang) is an open-source programming language developed by Google, known for its simplicity, efficiency, and strong support for concurrency.

### **Installation**
- **Download:** [Go Download](https://golang.org/dl/)
- **Verify Installation:**
  ```bash
  go version
  ```

## **2. Basic Concepts**

### **Hello World**
- **Description:** The simplest program that prints "Hello, World!" to the screen.
  ```go
  package main

  import "fmt"

  func main() {
      fmt.Println("Hello, World!")
  }
  ```

### **Variables**
- **Description:** Used to store data values. You can declare them with a specific type or let Go infer the type.
  ```go
  var name string = "John"  // Declare with type
  age := 30                 // Short declaration, Go infers the type
  ```

### **Data Types**
- **Description:** Defines the type of data a variable can hold. Common types include integers, floating-point numbers, strings, and booleans.
  ```go
  var age int = 30
  var height float64 = 5.9
  var name string = "Alice"
  var isStudent bool = true
  ```

### **Constants**
- **Description:** Similar to variables but cannot be changed once set. Used for values that should remain constant throughout the program.
  ```go
  const Pi = 3.14
  ```

### **Control Structures**
- **Description:** Used to control the flow of the program, including decision-making (if-else) and looping (for).
  ```go
  // If-Else
  if age > 18 {
      fmt.Println("Adult")
  } else {
      fmt.Println("Minor")
  }

  // For Loop
  for i := 0; i < 5; i++ {
      fmt.Println(i)
  }
  ```

## **3. Functions**

### **Function Declaration**
- **Description:** A reusable block of code that performs a specific task. Functions can take inputs (parameters) and return outputs.
  ```go
  func add(a int, b int) int {
      return a + b
  }
  ```

### **Multiple Return Values**
- **Description:** Functions can return more than one value. Useful for returning results and errors.
  ```go
  func divide(a int, b int) (int, int) {
      quotient := a / b
      remainder := a % b
      return quotient, remainder
  }
  ```

### **Named Return Values**
- **Description:** Return values can be named, making it easier to return them without explicitly specifying them.
  ```go
  func multiply(a int, b int) (result int) {
      result = a * b
      return
  }
  ```

### **Variadic Functions**
- **Description:** Functions that can take a variable number of arguments. Useful for functions that need to handle an unknown number of inputs.
  ```go
  func sum(numbers ...int) int {
      total := 0
      for _, number := range numbers {
          total += number
      }
      return total
  }
  ```

## **4. Arrays and Slices**

### **Arrays**
- **Description:** Fixed-size lists of elements of the same type. Once set, the size cannot change.
  ```go
  var arr [5]int
  arr[0] = 1
  ```

### **Slices**
- **Description:** Dynamic-size lists that can grow and shrink. More flexible than arrays.
  ```go
  slice := []int{1, 2, 3}
  slice = append(slice, 4)  // Add an element
  ```

## **5. Maps**

### **Maps**
- **Description:** Unordered collections of key-value pairs. Useful for fast lookups and data organization.
  ```go
  m := make(map[string]int)
  m["age"] = 30
  age := m["age"]  // Access value by key
  ```

## **6. Structs and Interfaces**

### **Structs**
- **Description:** Custom data types that group related variables (fields) together.
  ```go
  type Person struct {
      Name string
      Age  int
  }

  var p Person
  p.Name = "Alice"
  p.Age = 30
  ```

### **Interfaces**
- **Description:** Define methods that a type must implement. Used to achieve polymorphism.
  ```go
  type Shape interface {
      Area() float64
  }
  ```

## **7. Concurrency**

### **Goroutines**
- **Description:** Lightweight threads managed by Go. Useful for running multiple tasks concurrently.
  ```go
  go func() {
      fmt.Println("Running in a goroutine")
  }()
  ```

### **Channels**
- **Description:** Allow goroutines to communicate and synchronize by passing data between them.
  ```go
  ch := make(chan int)

  go func() {
      ch <- 42  // Send data to channel
  }()

  value := <-ch  // Receive data from channel
  ```

### **Multiplexing**
- **Description:** Using channels to handle multiple concurrent operations. Channels can be used with the `select` statement to handle multiple channels.
  ```go
  ch1 := make(chan int)
  ch2 := make(chan int)

  go func() {
      ch1 <- 1
  }()

  go func() {
      ch2 <- 2
  }()

  select {
  case msg1 := <-ch1:
      fmt.Println("Received", msg1)
  case msg2 := <-ch2:
      fmt.Println("Received", msg2)
  }
  ```

## **8. Error Handling**

### **Basic Error Handling**
- **Description:** Handle and manage errors using the `error` type to indicate problems during function execution.
  ```go
  import "errors"

  func divide(a, b int) (int, error) {
      if b == 0 {
          return 0, errors.New("division by zero")
      }
      return a / b, nil
  }
  ```

## **9. Advanced Concepts**

### **Subroutines**
- **Description:** Functions or methods that are called by other functions. They help break down complex tasks into simpler, manageable pieces.
  ```go
  func mainTask() {
      subTask()
  }

  func subTask() {
      fmt.Println("Subtask executed")
  }
  ```

### **Enum**
- **Description:** Go does not have an `enum` type like some other languages. Instead, you can use `const` with iota to create a set of related constants.
  ```go
  const (
      Red = iota
      Green
      Blue
  )
  ```

### **Trees**
- **Description:** A hierarchical data structure with nodes connected by edges. Commonly used in algorithms and data management.
  ```go
  type Node struct {
      Value    int
      Children []*Node
  }

  root := Node{Value: 1}
  child := Node{Value: 2}
  root.Children = append(root.Children, &child)
  ```

### **Pointers**
- **Description:** Variables that store the memory address of another variable. Useful for performance optimization and modifying data in functions.
  ```go
  var x int = 10
  var p *int = &x  // p is a pointer to x
  *p = 20          // Modify x through the pointer
  ```

### **Linked Lists**
- **Description:** A linear data structure where elements are stored in nodes. Each node contains a value and a reference to the next node.
  ```go
  type Node struct {
      Value int
      Next  *Node
  }

  head := &Node{Value: 1}
  second := &Node{Value: 2}
  head.Next = second
  ```

### **Stacks**
- **Description:** A stack is a data structure that follows Last In, First Out (LIFO) principle. Elements are added and removed from the top.
  ```go
  type Stack struct {
      items []int
  }

  func (s *Stack) Push(item int) {
      s.items = append(s.items, item)
  }

  func (s *Stack) Pop() (int, bool) {
      if len(s.items) == 0 {
          return 0, false
      }
      item := s.items[len(s.items)-1]
      s.items = s.items[:len(s.items)-1]
      return item, true
  }
  ```