# **Go API Development Cheatsheet**

## **1. Introduction**

### **What is an API?**
- **Description:** An Application Programming Interface (API) allows different software applications to communicate with each other. In web development, APIs are often used to interact with backend services over HTTP.

## **2. Setting Up a Basic API**

### **Creating a Simple HTTP Server**
- **Description:** Use the `net/http` package to create a basic HTTP server.
  ```go
  package main

  import (
      "fmt"
      "net/http"
  )

  func main() {
      http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Hello, World!")
      })
      http.ListenAndServe(":8080", nil)
  }
  ```

## **3. Routing**

### **Using `gorilla/mux` for Advanced Routing**
- **Description:** The `gorilla/mux` package provides a powerful router for handling HTTP requests.
  ```go
  import (
      "github.com/gorilla/mux"
      "net/http"
  )

  func main() {
      r := mux.NewRouter()
      r.HandleFunc("/", HomeHandler)
      r.HandleFunc("/api/{id:[0-9]+}", ApiHandler)
      http.ListenAndServe(":8080", r)
  }

  func HomeHandler(w http.ResponseWriter, r *http.Request) {
      fmt.Fprintf(w, "Home Page")
  }

  func ApiHandler(w http.ResponseWriter, r *http.Request) {
      vars := mux.Vars(r)
      id := vars["id"]
      fmt.Fprintf(w, "API ID: %s", id)
  }
  ```

## **4. Handling JSON**

### **Encoding and Decoding JSON**
- **Description:** Use the `encoding/json` package to handle JSON data in your API.
  ```go
  import (
      "encoding/json"
      "net/http"
  )

  type Person struct {
      Name string `json:"name"`
      Age  int    `json:"age"`
  }

  func main() {
      http.HandleFunc("/person", func(w http.ResponseWriter, r *http.Request) {
          person := Person{Name: "Alice", Age: 30}
          jsonData, _ := json.Marshal(person)
          w.Header().Set("Content-Type", "application/json")
          w.Write(jsonData)
      })
      http.ListenAndServe(":8080", nil)
  }
  ```

### **Parsing JSON from Requests**
- **Description:** Read and parse JSON from HTTP requests.
  ```go
  import (
      "encoding/json"
      "net/http"
  )

  func main() {
      http.HandleFunc("/create", func(w http.ResponseWriter, r *http.Request) {
          var person Person
          if err := json.NewDecoder(r.Body).Decode(&person); err != nil {
              http.Error(w, err.Error(), http.StatusBadRequest)
              return
          }
          fmt.Fprintf(w, "Received: %+v", person)
      })
      http.ListenAndServe(":8080", nil)
  }
  ```

## **5. Error Handling**

### **Handling Errors in API**
- **Description:** Properly handle errors and return appropriate HTTP status codes.
  ```go
  import (
      "encoding/json"
      "net/http"
  )

  func main() {
      http.HandleFunc("/divide", func(w http.ResponseWriter, r *http.Request) {
          a := r.URL.Query().Get("a")
          b := r.URL.Query().Get("b")
          if a == "" || b == "" {
              http.Error(w, "Missing parameters", http.StatusBadRequest)
              return
          }
          // Assuming successful operation
          fmt.Fprintf(w, "Result: %s divided by %s", a, b)
      })
      http.ListenAndServe(":8080", nil)
  }
  ```

## **6. Middleware**

### **Creating Middleware**
- **Description:** Use middleware to perform operations before passing the request to handlers, such as logging or authentication.
  ```go
  import (
      "fmt"
      "net/http"
  )

  func loggingMiddleware(next http.Handler) http.Handler {
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          fmt.Println("Request received:", r.URL.Path)
          next.ServeHTTP(w, r)
      })
  }

  func main() {
      mux := http.NewServeMux()
      mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Home Page")
      })

      http.ListenAndServe(":8080", loggingMiddleware(mux))
  }
  ```

## **7. Authentication**

### **Basic Authentication**
- **Description:** Protect your API using basic authentication.
  ```go
  import (
      "net/http"
      "encoding/base64"
      "strings"
  )

  func basicAuthMiddleware(next http.Handler) http.Handler {
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          user, pass, ok := r.BasicAuth()
          if !ok || user != "username" || pass != "password" {
              w.Header().Set("WWW-Authenticate", `Basic realm="Restricted"`)
              http.Error(w, "Unauthorized", http.StatusUnauthorized)
              return
          }
          next.ServeHTTP(w, r)
      })
  }

  func main() {
      mux := http.NewServeMux()
      mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Welcome!")
      })

      http.ListenAndServe(":8080", basicAuthMiddleware(mux))
  }
  ```

## **8. Rate Limiting**

### **Implementing Rate Limiting**
- **Description:** Prevent abuse by limiting the rate of requests.
  ```go
  import (
      "net/http"
      "time"
  )

  func rateLimitMiddleware(next http.Handler) http.Handler {
      limiter := time.NewTicker(1 * time.Second)
      return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
          <-limiter.C
          next.ServeHTTP(w, r)
      })
  }

  func main() {
      mux := http.NewServeMux()
      mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Welcome!")
      })

      http.ListenAndServe(":8080", rateLimitMiddleware(mux))
  }
  ```

## **9. API Versioning**

### **Versioning API Endpoints**
- **Description:** Manage different versions of your API.
  ```go
  import (
      "net/http"
  )

  func main() {
      mux := http.NewServeMux()
      mux.HandleFunc("/v1/resource", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Resource v1")
      })
      mux.HandleFunc("/v2/resource", func(w http.ResponseWriter, r *http.Request) {
          fmt.Fprintf(w, "Resource v2")
      })

      http.ListenAndServe(":8080", mux)
  }
  ```

## **10. Testing APIs**

### **Unit Testing Handlers**
- **Description:** Write tests for your API handlers using the `testing` and `net/http/httptest` packages.
  ```go
  import (
      "net/http"
      "net/http/httptest"
      "testing"
  )

  func TestHomeHandler(t *testing.T) {
      req := httptest.NewRequest("GET", "http://example.com/", nil)
      w := httptest.NewRecorder()
      HomeHandler(w, req)

      res := w.Result()
      if res.StatusCode != http.StatusOK {
          t.Errorf("Expected status OK; got %v", res.Status)
      }
  }
  ```

### **Integration Testing**
- **Description:** Test your entire API, including its interaction with databases and other services.
  ```go
  import (
      "database/sql"
      _ "github.com/lib/pq"
      "net/http"
      "net/http/httptest"
      "testing"
  )

  func TestDatabaseInteraction(t *testing.T) {
      // Setup database connection and test
  }
  ```

## **11. Documentation**

### **Generating API Documentation**
- **Description:** Use tools like Swagger to generate API documentation.
  - **Install Swagger:** [Swagger Installation](https://swagger.io/tools/swagger-ui/)
  - **Add Comments in Code:** Use comments to document your API endpoints, which Swagger can use to generate docs.
