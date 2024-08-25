# **C Programming Cheatsheet**

## **1. Basics of C Programming**

### **1.1. Hello World Program**
- **Description:** The simplest C program that outputs "Hello, World!".
  ```c
  #include <stdio.h>

  int main() {
      printf("Hello, World!\n");
      return 0;
  }
  ```

### **1.2. Variables**
- **Description:** Storage locations with a name and type to hold data.
  ```c
  int age = 25;        // Integer
  float height = 5.9;  // Floating-point number
  char initial = 'A';  // Character
  ```

### **1.3. Data Types**
- **Description:** Defines the type of data a variable can hold.
  - **`int`**: Integer numbers.
    ```c
    int age = 30;
    printf("Age: %d\n", age);  // Outputs: Age: 30
    ```
  - **`float`**: Floating-point numbers.
    ```c
    float height = 5.9;
    printf("Height: %.1f\n", height);  // Outputs: Height: 5.9
    ```
  - **`double`**: Double precision floating-point numbers.
    ```c
    double pi = 3.1415926535;
    printf("Pi: %.10f\n", pi);  // Outputs: Pi: 3.1415926535
    ```
  - **`char`**: Single characters.
    ```c
    char grade = 'A';
    printf("Grade: %c\n", grade);  // Outputs: Grade: A
    ```

### **1.4. Operators**
- **Description:** Symbols that perform operations on variables and values.
  - **Arithmetic Operators:**
    ```c
    int a = 10, b = 5;
    printf("Sum: %d\n", a + b);      // Outputs: Sum: 15
    printf("Difference: %d\n", a - b); // Outputs: Difference: 5
    printf("Product: %d\n", a * b);  // Outputs: Product: 50
    printf("Quotient: %d\n", a / b); // Outputs: Quotient: 2
    printf("Remainder: %d\n", a % b); // Outputs: Remainder: 0
    ```
  - **Comparison Operators:**
    ```c
    int x = 10, y = 20;
    printf("x == y: %d\n", x == y);  // Outputs: x == y: 0 (false)
    printf("x != y: %d\n", x != y);  // Outputs: x != y: 1 (true)
    printf("x > y: %d\n", x > y);    // Outputs: x > y: 0 (false)
    printf("x < y: %d\n", x < y);    // Outputs: x < y: 1 (true)
    printf("x >= y: %d\n", x >= y);  // Outputs: x >= y: 0 (false)
    printf("x <= y: %d\n", x <= y);  // Outputs: x <= y: 1 (true)
    ```
  - **Logical Operators:**
    ```c
    int p = 1, q = 0;
    printf("p && q: %d\n", p && q);  // Outputs: p && q: 0 (false)
    printf("p || q: %d\n", p || q);  // Outputs: p || q: 1 (true)
    printf("!p: %d\n", !p);          // Outputs: !p: 0 (false)
    ```

### **1.5. Control Structures**
- **Description:** Direct the flow of execution based on conditions.
  - **`if` Statement:**
    ```c
    int age = 20;
    if (age > 18) {
        printf("Adult\n"); // Outputs: Adult
    }
    ```
  - **`for` Loop:**
    ```c
    for (int i = 0; i < 5; i++) {
        printf("%d\n", i); // Outputs: 0 1 2 3 4
    }
    ```
  - **`while` Loop:**
    ```c
    int i = 0;
    while (i < 5) {
        printf("%d\n", i); // Outputs: 0 1 2 3 4
        i++;
    }
    ```

### **1.6. Functions**
- **Description:** Blocks of code that perform a specific task and can be reused.
  ```c
  int add(int a, int b) {
      return a + b;
  }

  int main() {
      int sum = add(3, 5);
      printf("Sum: %d\n", sum); // Outputs: Sum: 8
      return 0;
  }
  ```

### **1.7. Arrays**
- **Description:** Collection of variables of the same type.
  ```c
  int numbers[5] = {1, 2, 3, 4, 5};
  printf("%d\n", numbers[2]);  // Outputs: 3
  ```

### **1.8. Pointers**
- **Description:** Variables that store memory addresses.
  ```c
  int value = 10;
  int *ptr = &value;  // Pointer to value
  printf("%d\n", *ptr);  // Outputs: 10
  ```

### **1.9. Strings**
- **Description:** Arrays of characters ending with a null character `'\0'`.
  ```c
  char name[] = "John Doe";
  printf("%s\n", name);  // Outputs: John Doe
  ```

### **1.10. Structs**
- **Description:** User-defined data types that group related variables.
  ```c
  struct Person {
      char name[50];
      int age;
  };

  int main() {
      struct Person person1;
      strcpy(person1.name, "Alice");
      person1.age = 30;
      printf("%s is %d years old.\n", person1.name, person1.age); // Outputs: Alice is 30 years old.
      return 0;
  }
  ```

## **2. Advanced C Programming**

### **2.1. Dynamic Memory Allocation**
- **Description:** Allocate memory at runtime using `malloc`, `calloc`, `realloc`, and `free`.
  ```c
  int *array = malloc(10 * sizeof(int));  // Allocate memory for 10 integers
  if (array == NULL) {
      printf("Memory allocation failed\n");
      return 1;
  }
  // Use the array...
  free(array);  // Free allocated memory
  ```

### **2.2. File I/O**
- **Description:** Read from and write to files.
  ```c
  FILE *file = fopen("example.txt", "w");
  if (file != NULL) {
      fprintf(file, "Hello, File!\n");
      fclose(file);
  }

  char buffer[100];
  FILE *file2 = fopen("example.txt", "r");
  if (file2 != NULL) {
      while (fgets(buffer, sizeof(buffer), file2)) {
          printf("%s", buffer);  // Outputs: Hello, File!
      }
      fclose(file2);
  }
  ```

### **2.3. Recursion**
- **Description:** A function that calls itself to solve a problem.
  ```c
  int factorial(int n) {
      if (n == 0) return 1;
      return n * factorial(n - 1);
  }

  int main() {
      printf("Factorial of 5: %d\n", factorial(5)); // Outputs: Factorial of 5: 120
      return 0;
  }
  ```

### **2.4. Linked Lists**
- **Description:** A data structure consisting of nodes where each node points to the next node.
  ```c
  struct Node {
      int data;
      struct Node *next;
  };

  void printList(struct Node *n) {
      while (n != NULL) {
          printf("%d -> ", n->data);
          n = n->next;
      }
      printf("NULL\n");
  }
  ```

### **2.5. Binary Trees**
- **Description:** A tree data structure where each node has at most two children.
  ```c
  struct TreeNode {
      int data;
      struct TreeNode *left;
      struct TreeNode *right;
  };

  void inorderTraversal(struct TreeNode *root) {
      if (root != NULL) {
          inorderTraversal(root->left);
          printf("%d ", root->data);
          inorderTraversal(root->right);
      }
  }
  ```

### **2.6. Enums**
- **Description:** Define a set of named integer constants.
  ```c
  enum Day { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };

  int main() {
      enum Day today = Wednesday;
      printf("Day %d\n", today);  // Outputs: Day 3
      return 0;
  }
  ```

### **2.7. Error Handling**
- **Description:** Manage

 errors using return codes and error messages.
  ```c
  int divide(int a, int b, float *result) {
      if (b == 0) return -1;  // Error code for division by zero
      *result = (float)a / b;
      return 0;  // Success
  }

  int main() {
      float result;
      if (divide(10, 0, &result) == -1) {
          printf("Error: Division by zero\n");
      } else {
          printf("Result: %.2f\n", result);
      }
      return 0;
  }
  ```

### **2.8. Macros and Preprocessor Directives**
- **Description:** Use preprocessor directives to define constants and macros.
  ```c
  #define PI 3.14
  #define SQUARE(x) ((x) * (x))

  int main() {
      printf("PI: %f\n", PI);
      printf("Square of 5: %d\n", SQUARE(5));
      return 0;
  }
  ```

### **2.9. Multi-threading (with POSIX Threads)**
- **Description:** Use threads to perform concurrent operations.
  ```c
  #include <pthread.h>
  #include <stdio.h>

  void* printMessage(void* msg) {
      printf("%s\n", (char*)msg);
      return NULL;
  }

  int main() {
      pthread_t thread;
      const char* message = "Hello from thread!";
      pthread_create(&thread, NULL, printMessage, (void*)message);
      pthread_join(thread, NULL);
      return 0;
  }
  ```

### **2.10. Function Pointers**
- **Description:** Pointers that point to functions, allowing dynamic function calls.
  ```c
  #include <stdio.h>

  void greet() {
      printf("Hello, World!\n");
  }

  void execute(void (*func)()) {
      func();
  }

  int main() {
      void (*funcPtr)() = greet;
      execute(funcPtr);
      return 0;
  }
  ```
