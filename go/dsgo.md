# **Data Structures in Go Cheatsheet**

## **1. Basic Data Structures**

### **1.1. Arrays**
- **Description:** Fixed-size collection of elements of the same type.
- **Example:**
  ```go
  var arr [5]int // Array of 5 integers
  arr[0] = 1
  arr[1] = 2
  ```

### **1.2. Slices**
- **Description:** Dynamic-sized, flexible view into the elements of an array.
- **Example:**
  ```go
  arr := []int{1, 2, 3, 4, 5} // Slice initialization
  arr = append(arr, 6) // Add element to the slice
  ```

### **1.3. Maps**
- **Description:** Unordered collection of key-value pairs.
- **Example:**
  ```go
  m := make(map[string]int) // Create a map
  m["a"] = 1
  m["b"] = 2

  value := m["a"] // Access value by key
  ```

### **1.4. Structs**
- **Description:** Composite data type that groups together variables (fields).
- **Example:**
  ```go
  type Person struct {
      Name string
      Age  int
  }

  p := Person{Name: "Alice", Age: 30}
  ```

## **2. Advanced Data Structures**

### **2.1. Linked Lists**
- **Description:** A collection of nodes where each node points to the next node.
- **Example:**
  ```go
  type Node struct {
      Value int
      Next  *Node
  }

  head := &Node{Value: 1}
  head.Next = &Node{Value: 2}
  ```

### **2.2. Queues**
- **Description:** FIFO (First In, First Out) data structure.
- **Example:**
  ```go
  type Queue struct {
      items []int
  }

  func (q *Queue) Enqueue(item int) {
      q.items = append(q.items, item)
  }

  func (q *Queue) Dequeue() int {
      item := q.items[0]
      q.items = q.items[1:]
      return item
  }
  ```

### **2.3. Stacks**
- **Description:** LIFO (Last In, First Out) data structure.
- **Example:**
  ```go
  type Stack struct {
      items []int
  }

  func (s *Stack) Push(item int) {
      s.items = append(s.items, item)
  }

  func (s *Stack) Pop() int {
      item := s.items[len(s.items)-1]
      s.items = s.items[:len(s.items)-1]
      return item
  }
  ```

### **2.4. Trees**
- **Description:** Hierarchical data structure with nodes connected by edges.
- **Example:**
  ```go
  type TreeNode struct {
      Value int
      Left  *TreeNode
      Right *TreeNode
  }

  root := &TreeNode{Value: 1}
  root.Left = &TreeNode{Value: 2}
  root.Right = &TreeNode{Value: 3}
  ```

### **2.5. Graphs**
- **Description:** Collection of nodes (vertices) connected by edges.
- **Example:**
  ```go
  type Graph struct {
      vertices map[string][]string
  }

  func (g *Graph) AddVertex(v string) {
      g.vertices[v] = []string{}
  }

  func (g *Graph) AddEdge(v1, v2 string) {
      g.vertices[v1] = append(g.vertices[v1], v2)
      g.vertices[v2] = append(g.vertices[v2], v1) // Undirected graph
  }
  ```

## **3. Implementing Data Structures**

### **3.1. Implementing a Linked List**
- **Description:** A singly linked list with basic operations.
- **Example:**
  ```go
  type ListNode struct {
      Value int
      Next  *ListNode
  }

  func (n *ListNode) Append(value int) *ListNode {
      current := n
      for current.Next != nil {
          current = current.Next
      }
      current.Next = &ListNode{Value: value}
      return n
  }
  ```

### **3.2. Implementing a Binary Search Tree (BST)**
- **Description:** A binary tree where each node has at most two children and the left child is less than the parent node, and the right child is greater.
- **Example:**
  ```go
  type BSTNode struct {
      Value int
      Left  *BSTNode
      Right *BSTNode
  }

  func (n *BSTNode) Insert(value int) {
      if value < n.Value {
          if n.Left == nil {
              n.Left = &BSTNode{Value: value}
          } else {
              n.Left.Insert(value)
          }
      } else {
          if n.Right == nil {
              n.Right = &BSTNode{Value: value}
          } else {
              n.Right.Insert(value)
          }
      }
  }
  ```

## **4. Go Data Structure Operations**

### **4.1. Iterating over Arrays and Slices**
- **Description:** Loop through elements.
- **Example:**
  ```go
  arr := []int{1, 2, 3, 4, 5}
  for i, v := range arr {
      fmt.Printf("Index: %d, Value: %d\n", i, v)
  }
  ```

### **4.2. Iterating over Maps**
- **Description:** Loop through key-value pairs.
- **Example:**
  ```go
  m := map[string]int{"a": 1, "b": 2}
  for key, value := range m {
      fmt.Printf("Key: %s, Value: %d\n", key, value)
  }
  ```

### **4.3. Iterating over Structs**
- **Description:** Access fields in a struct.
- **Example:**
  ```go
  p := Person{Name: "Alice", Age: 30}
  fmt.Println("Name:", p.Name)
  fmt.Println("Age:", p.Age)
  ```
