# **Algorithms in Go Cheatsheet**

## **1. Sorting Algorithms**

### **1.1. Bubble Sort**
- **Description:** Repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.
- **Example:**
  ```go
  func bubbleSort(arr []int) {
      n := len(arr)
      for i := 0; i < n-1; i++ {
          for j := 0; j < n-i-1; j++ {
              if arr[j] > arr[j+1] {
                  arr[j], arr[j+1] = arr[j+1], arr[j]
              }
          }
      }
  }
  ```

### **1.2. Selection Sort**
- **Description:** Finds the minimum element from the unsorted part and swaps it with the first unsorted element.
- **Example:**
  ```go
  func selectionSort(arr []int) {
      n := len(arr)
      for i := 0; i < n-1; i++ {
          minIndex := i
          for j := i + 1; j < n; j++ {
              if arr[j] < arr[minIndex] {
                  minIndex = j
              }
          }
          arr[i], arr[minIndex] = arr[minIndex], arr[i]
      }
  }
  ```

### **1.3. Insertion Sort**
- **Description:** Builds the final sorted array one item at a time by inserting each new element into its correct position.
- **Example:**
  ```go
  func insertionSort(arr []int) {
      n := len(arr)
      for i := 1; i < n; i++ {
          key := arr[i]
          j := i - 1
          for j >= 0 && arr[j] > key {
              arr[j+1] = arr[j]
              j--
          }
          arr[j+1] = key
      }
  }
  ```

### **1.4. Merge Sort**
- **Description:** Divide-and-conquer algorithm that divides the array into halves, recursively sorts them, and then merges the sorted halves.
- **Example:**
  ```go
  func mergeSort(arr []int) {
      if len(arr) < 2 {
          return
      }
      mid := len(arr) / 2
      left := make([]int, mid)
      right := make([]int, len(arr)-mid)

      copy(left, arr[:mid])
      copy(right, arr[mid:])

      mergeSort(left)
      mergeSort(right)
      merge(arr, left, right)
  }

  func merge(arr, left, right []int) {
      i, j, k := 0, 0, 0
      for i < len(left) && j < len(right) {
          if left[i] <= right[j] {
              arr[k] = left[i]
              i++
          } else {
              arr[k] = right[j]
              j++
          }
          k++
      }
      for i < len(left) {
          arr[k] = left[i]
          i++
          k++
      }
      for j < len(right) {
          arr[k] = right[j]
          j++
          k++
      }
  }
  ```

### **1.5. Quick Sort**
- **Description:** Efficient, divide-and-conquer algorithm that selects a pivot and partitions the array into elements less than and greater than the pivot.
- **Example:**
  ```go
  func quickSort(arr []int, low, high int) {
      if low < high {
          p := partition(arr, low, high)
          quickSort(arr, low, p-1)
          quickSort(arr, p+1, high)
      }
  }

  func partition(arr []int, low, high int) int {
      pivot := arr[high]
      i := low
      for j := low; j < high; j++ {
          if arr[j] < pivot {
              arr[i], arr[j] = arr[j], arr[i]
              i++
          }
      }
      arr[i], arr[high] = arr[high], arr[i]
      return i
  }
  ```

### **1.6. Heap Sort**
- **Description:** Uses a binary heap to sort elements. Builds a max heap and extracts the maximum element repeatedly.
- **Example:**
  ```go
  func heapSort(arr []int) {
      n := len(arr)
      for i := n/2 - 1; i >= 0; i-- {
          heapify(arr, n, i)
      }
      for i := n - 1; i > 0; i-- {
          arr[0], arr[i] = arr[i], arr[0]
          heapify(arr, i, 0)
      }
  }

  func heapify(arr []int, n, i int) {
      largest := i
      left := 2*i + 1
      right := 2*i + 2
      if left < n && arr[left] > arr[largest] {
          largest = left
      }
      if right < n && arr[right] > arr[largest] {
          largest = right
      }
      if largest != i {
          arr[i], arr[largest] = arr[largest], arr[i]
          heapify(arr, n, largest)
      }
  }
  ```

### **1.7. Counting Sort**
- **Description:** Non-comparison-based sorting algorithm that counts occurrences of each distinct element.
- **Example:**
  ```go
  func countingSort(arr []int) {
      if len(arr) == 0 {
          return
      }

      maxVal := arr[0]
      for _, val := range arr {
          if val > maxVal {
              maxVal = val
          }
      }

      count := make([]int, maxVal+1)
      for _, val := range arr {
          count[val]++
      }

      index := 0
      for i, c := range count {
          for c > 0 {
              arr[index] = i
              index++
              c--
          }
      }
  }
  ```

## **2. Searching Algorithms**

### **2.1. Linear Search**
- **Description:** Sequentially checks each element until the desired element is found or the list ends.
- **Example:**
  ```go
  func linearSearch(arr []int, target int) int {
      for i, v := range arr {
          if v == target {
              return i
          }
      }
      return -1
  }
  ```

### **2.2. Binary Search**
- **Description:** Efficiently finds an item in a sorted array by repeatedly dividing the search interval in half.
- **Example:**
  ```go
  func binarySearch(arr []int, target int) int {
      low, high := 0, len(arr)-1
      for low <= high {
          mid := low + (high-low)/2
          if arr[mid] == target {
              return mid
          } else if arr[mid] < target {
              low = mid + 1
          } else {
              high = mid - 1
          }
      }
      return -1
  }
  ```

## **3. Graph Algorithms**

### **3.1. Depth-First Search (DFS)**
- **Description:** Traverses a graph by exploring as far as possible along each branch before backtracking.
- **Example:**
  ```go
  type Graph struct {
      vertices map[string][]string
  }

  func (g *Graph) DFS(start string, visited map[string]bool) {
      if visited[start] {
          return
      }
      visited[start] = true
      fmt.Println(start)

      for _, neighbor := range g.vertices[start] {
          if !visited[neighbor] {
              g.DFS(neighbor, visited)
          }
      }
  }
  ```

### **3.2. Breadth-First Search (BFS)**
- **Description:** Traverses a graph level by level, exploring all neighbors of a node before moving on to their neighbors.
- **Example:**
  ```go
  func (g *Graph) BFS(start string) {
      visited := make(map[string]bool)
      queue := []string{start}
      visited[start] = true

      for len(queue) > 0 {
          node := queue[0]
          queue = queue[1:]
          fmt.Println(node)

          for _, neighbor := range g.vertices[node] {
              if !visited[neighbor] {
                  visited[neighbor] = true
                  queue = append(queue, neighbor)
              }
          }
      }
  }
  ```

## **4. Dynamic Programming**

### **4.1. Fibonacci Sequence**
- **Description:** Computes the nth Fibonacci number using memoization.
- **Example:**
  ```go
  func fibonacci(n int, memo map[int]int) int {
      if n <= 1 {
          return n
      }
      if _, exists := memo[n]; exists {
          return memo[n]
      }
      memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo)
      return memo[n]
  }
  ```

### **4.2. Knapsack Problem**
- **Description:** Solves the problem of selecting items with given weights and values to maximize total value without exceeding the weight limit.
- **Example:**
  ```go
  func knapsack(weights []int, values []int, capacity int) int {
      n := len(weights)
      dp := make([]int, capacity+

1)

      for i := 0; i < n; i++ {
          for w := capacity; w >= weights[i]; w-- {
              if dp[w] < dp[w-weights[i]]+values[i] {
                  dp[w] = dp[w-weights[i]] + values[i]
              }
          }
      }
      return dp[capacity]
  }
  ```

## **5. Advanced Algorithms**

### **5.1. Dijkstra's Algorithm**
- **Description:** Finds the shortest path from a source node to all other nodes in a weighted graph.
- **Example:**
  ```go
  import (
      "math"
      "container/heap"
  )

  type Graph struct {
      adj map[string]map[string]int
  }

  func (g *Graph) Dijkstra(start string) map[string]int {
      dist := make(map[string]int)
      for node := range g.adj {
          dist[node] = math.MaxInt32
      }
      dist[start] = 0

      pq := &PriorityQueue{}
      heap.Push(pq, &Item{node: start, priority: 0})

      for pq.Len() > 0 {
          u := heap.Pop(pq).(*Item).node
          for v, weight := range g.adj[u] {
              alt := dist[u] + weight
              if alt < dist[v] {
                  dist[v] = alt
                  heap.Push(pq, &Item{node: v, priority: alt})
              }
          }
      }
      return dist
  }

  type Item struct {
      node     string
      priority int
      index    int
  }

  type PriorityQueue []*Item

  func (pq PriorityQueue) Len() int           { return len(pq) }
  func (pq PriorityQueue) Less(i, j int) bool { return pq[i].priority < pq[j].priority }
  func (pq PriorityQueue) Swap(i, j int)      { pq[i], pq[j] = pq[j], pq[i]; pq[i].index = i; pq[j].index = j }

  func (pq *PriorityQueue) Push(x interface{}) {
      n := len(*pq)
      item := x.(*Item)
      item.index = n
      *pq = append(*pq, item)
  }

  func (pq *PriorityQueue) Pop() interface{} {
      old := *pq
      n := len(old)
      item := old[n-1]
      old[n-1] = nil
      item.index = -1
      *pq = old[0 : n-1]
      return item
  }
  ```