# **Go Backend Development Cheatsheet**

## **1. Setting Up a Go Backend**

### **Project Structure**
- **Description:** Organize your Go project into directories for clarity and maintainability.
  ```
  /project
  ├── /cmd          # Main applications
  ├── /pkg          # Library code
  ├── /internal     # Private application and library code
  ├── /api          # API definitions
  ├── /web          # Web-related files (HTML, CSS, JS)
  ├── /config       # Configuration files
  └── /scripts      # Build and deployment scripts
  ```

### **Modules**
- **Description:** Manage dependencies with Go modules. Initialize a module with `go mod init <module-name>`.
  ```bash
  go mod init myapp
  ```

## **2. HTTP Handling**

### **Creating a Basic HTTP Server**
- **Description:** Set up a simple HTTP server using the `net/http` package.
  ```go
  package main

  import (
      "fmt"
      "net/http"
  )

  func handler(w http.ResponseWriter, r *http.Request) {
      fmt.Fprintf(w, "Hello, World!")
  }

  func main() {
      http.HandleFunc("/", handler)
      http.ListenAndServe(":8080", nil)
  }
  ```

### **Routing**
- **Description:** Use `gorilla/mux` or `chi` for advanced routing.
  ```go
  import (
      "github.com/gorilla/mux"
      "net/http"
  )

  func main() {
      r := mux.NewRouter()
      r.HandleFunc("/", handler)
      http.ListenAndServe(":8080", r)
  }
  ```

### **Middleware**
- **Description:** Functions that intercept requests before they reach your handlers.
  ```go
  func loggingMiddleware(next http.Handler) http.Handler {
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          fmt.Println("Request received")
          next.ServeHTTP(w, r)
      })
  }

  func main() {
      r := mux.NewRouter()
      r.Use(loggingMiddleware)
      r.HandleFunc("/", handler)
      http.ListenAndServe(":8080", r)
  }
  ```

## **3. Working with Databases**

### **Connecting to a Database**
- **Description:** Use `database/sql` and a driver (e.g., `pq` for PostgreSQL).
  ```go
  import (
      "database/sql"
      _ "github.com/lib/pq"
  )

  func main() {
      connStr := "user=username dbname=mydb sslmode=disable"
      db, err := sql.Open("postgres", connStr)
      if err != nil {
          log.Fatal(err)
      }
      defer db.Close()
  }
  ```

### **Performing Queries**
- **Description:** Execute SQL queries using `db.Query` and `db.Exec`.
  ```go
  rows, err := db.Query("SELECT id, name FROM users")
  if err != nil {
      log.Fatal(err)
  }
  defer rows.Close()

  for rows.Next() {
      var id int
      var name string
      if err := rows.Scan(&id, &name); err != nil {
          log.Fatal(err)
      }
      fmt.Println(id, name)
  }
  ```

## **4. Handling JSON**

### **Encoding and Decoding JSON**
- **Description:** Use `encoding/json` to handle JSON data.
  ```go
  import "encoding/json"

  type Person struct {
      Name string `json:"name"`
      Age  int    `json:"age"`
  }

  func main() {
      person := Person{Name: "Alice", Age: 30}
      jsonData, _ := json.Marshal(person)
      fmt.Println(string(jsonData))

      var p Person
      json.Unmarshal(jsonData, &p)
      fmt.Println(p)
  }
  ```

## **5. Error Handling**

### **Custom Error Types**
- **Description:** Define custom error types for more informative error handling.
  ```go
  type MyError struct {
      Message string
  }

  func (e *MyError) Error() string {
      return e.Message
  }

  func doSomething() error {
      return &MyError{Message: "Something went wrong"}
  }
  ```

## **6. Concurrency**

### **Goroutines**
- **Description:** Lightweight threads that allow concurrent execution of functions.
  ```go
  go func() {
      fmt.Println("Running in a goroutine")
  }()
  ```

### **Channels**
- **Description:** Communication mechanisms between goroutines.
  ```go
  ch := make(chan int)

  go func() {
      ch <- 42
  }()

  value := <-ch
  fmt.Println(value)
  ```

### **Select Statement**
- **Description:** Used to handle multiple channels.
  ```go
  select {
  case msg := <-ch1:
      fmt.Println("Received from ch1:", msg)
  case msg := <-ch2:
      fmt.Println("Received from ch2:", msg)
  case <-time.After(time.Second):
      fmt.Println("Timeout")
  }
  ```

## **7. Advanced Concepts**

### **Context Package**
- **Description:** Manage request-scoped values, cancellation signals, and deadlines.
  ```go
  import "context"

  func doWork(ctx context.Context) {
      select {
      case <-ctx.Done():
          fmt.Println("Work cancelled")
      case <-time.After(2 * time.Second):
          fmt.Println("Work completed")
      }
  }

  func main() {
      ctx, cancel := context.WithTimeout(context.Background(), 1*time.Second)
      defer cancel()
      go doWork(ctx)
      time.Sleep(3 * time.Second)
  }
  ```

### **Reflection**
- **Description:** Inspect and manipulate types and values at runtime.
  ```go
  import "reflect"

  func main() {
      var x float64 = 3.4
      t := reflect.TypeOf(x)
      v := reflect.ValueOf(x)

      fmt.Println("type:", t)
      fmt.Println("value:", v)
  }
  ```

### **Generics (Go 1.18+)**
- **Description:** Write functions and data structures that can handle multiple types.
  ```go
  func Print[T any](value T) {
      fmt.Println(value)
  }

  func main() {
      Print(123)
      Print("Hello")
  }
  ```

### **Dependency Injection**
- **Description:** Provide dependencies to components in a flexible and testable way.
  ```go
  type Service interface {
      DoSomething() string
  }

  type MyService struct{}

  func (s *MyService) DoSomething() string {
      return "Service working"
  }

  func NewHandler(s Service) http.Handler {
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintln(w, s.DoSomething())
      })
  }

  func main() {
      service := &MyService{}
      handler := NewHandler(service)
      http.ListenAndServe(":8080", handler)
  }
  ```

### **Server-Side Rendering (SSR)**
- **Description:** Generate HTML on the server and send it to the client.
  ```go
  import "html/template"

  func handler(w http.ResponseWriter, r *http.Request) {
      tmpl := template.Must(template.New("index").Parse("<h1>{{.}}</h1>"))
      tmpl.Execute(w, "Hello, World!")
  }

  func main() {
      http.HandleFunc("/", handler)
      http.ListenAndServe(":8080", nil)
  }
  ```

## **8. Testing**

### **Unit Testing**
- **Description:** Write tests for individual functions or components using Go's testing package.
  ```go
  import "testing"

  func TestAdd(t *testing.T) {
      result := add(2, 3)
      if result != 5 {
          t.Errorf("Expected 5, got %d", result)
      }
  }
  ```

### **Benchmark Testing**
- **Description:** Measure the performance of functions.
  ```go
  func BenchmarkAdd(b *testing.B) {
      for i := 0; i < b.N; i++ {
          add(2, 3)
      }
  }
  ```
