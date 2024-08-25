# **Design Patterns Cheat Sheet**

Design patterns are standard solutions to common problems in software design. This guide covers basic and advanced design patterns with simple examples.

Design patterns are general reusable solutions to common problems in software design. 


## **1. Creational Patterns**

### **1.1. Singleton**
- **Description:** Ensures only one instance of a class exists and provides a global point of access to it.
- **Example:**
  ```go
  package main

  import "sync"

  type Singleton struct {
      // Add fields if needed
  }

  var instance *Singleton
  var once sync.Once

  // GetInstance returns the single instance of Singleton
  func GetInstance() *Singleton {
      once.Do(func() {
          instance = &Singleton{}
      })
      return instance
  }
  ```

### **1.2. Factory Method**
- **Description:** Creates objects without specifying the exact class of object that will be created.
- **Example:**
  ```go
  package main

  import "fmt"

  type Product interface {
      Operation() string
  }

  type ConcreteProductA struct{}
  func (p *ConcreteProductA) Operation() string {
      return "Product A"
  }

  type Creator interface {
      FactoryMethod() Product
  }

  type ConcreteCreatorA struct{}
  func (c *ConcreteCreatorA) FactoryMethod() Product {
      return &ConcreteProductA{}
  }

  func ClientCode(c Creator) {
      product := c.FactoryMethod()
      fmt.Println(product.Operation())
  }
  ```

### **1.3. Abstract Factory**
- **Description:** Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
- **Example:**
  ```go
  package main

  import "fmt"

  type ProductA interface {
      OperationA() string
  }

  type ProductB interface {
      OperationB() string
  }

  type ConcreteProductA1 struct{}
  func (p *ConcreteProductA1) OperationA() string {
      return "ConcreteProductA1"
  }

  type ConcreteProductB1 struct{}
  func (p *ConcreteProductB1) OperationB() string {
      return "ConcreteProductB1"
  }

  type ConcreteProductA2 struct{}
  func (p *ConcreteProductA2) OperationA() string {
      return "ConcreteProductA2"
  }

  type ConcreteProductB2 struct{}
  func (p *ConcreteProductB2) OperationB() string {
      return "ConcreteProductB2"
  }

  type AbstractFactory interface {
      CreateProductA() ProductA
      CreateProductB() ProductB
  }

  type ConcreteFactory1 struct{}
  func (f *ConcreteFactory1) CreateProductA() ProductA {
      return &ConcreteProductA1{}
  }
  func (f *ConcreteFactory1) CreateProductB() ProductB {
      return &ConcreteProductB1{}
  }

  type ConcreteFactory2 struct{}
  func (f *ConcreteFactory2) CreateProductA() ProductA {
      return &ConcreteProductA2{}
  }
  func (f *ConcreteFactory2) CreateProductB() ProductB {
      return &ConcreteProductB2{}
  }

  func ClientCode(f AbstractFactory) {
      productA := f.CreateProductA()
      productB := f.CreateProductB()
      fmt.Println(productA.OperationA())
      fmt.Println(productB.OperationB())
  }
  ```

## **2. Structural Patterns**

### **2.1. Adapter**
- **Description:** Allows incompatible interfaces to work together by wrapping an existing class with a new interface.
- **Example:**
  ```go
  package main

  import "fmt"

  type OldSystem struct{}
  func (o *OldSystem) OldOperation() string {
      return "Old System Operation"
  }

  type NewSystem interface {
      NewOperation() string
  }

  type Adapter struct {
      old *OldSystem
  }

  func (a *Adapter) NewOperation() string {
      return a.old.OldOperation()
  }

  func ClientCode(n NewSystem) {
      fmt.Println(n.NewOperation())
  }
  ```

### **2.2. Decorator**
- **Description:** Adds new behavior to objects dynamically without altering their structure.
- **Example:**
  ```go
  package main

  import "fmt"

  type Component interface {
      Operation() string
  }

  type ConcreteComponent struct{}
  func (c *ConcreteComponent) Operation() string {
      return "Concrete Component"
  }

  type Decorator struct {
      component Component
  }

  func (d *Decorator) Operation() string {
      return "Decorator(" + d.component.Operation() + ")"
  }

  func ClientCode(c Component) {
      fmt.Println(c.Operation())
  }
  ```

### **2.3. Composite**
- **Description:** Allows you to compose objects into tree structures to represent part-whole hierarchies.
- **Example:**
  ```go
  package main

  import "fmt"

  type Component interface {
      Operation() string
  }

  type Leaf struct{}
  func (l *Leaf) Operation() string {
      return "Leaf"
  }

  type Composite struct {
      children []Component
  }

  func (c *Composite) Operation() string {
      result := "Composite: "
      for _, child := range c.children {
          result += child.Operation() + " "
      }
      return result
  }

  func (c *Composite) Add(child Component) {
      c.children = append(c.children, child)
  }

  func ClientCode(c Component) {
      fmt.Println(c.Operation())
  }
  ```

### **2.4. Bridge**
- **Description:** Separates an abstraction from its implementation, allowing them to vary independently.
- **Example:**
  ```go
  package main

  import "fmt"

  type Implementor interface {
      Operation() string
  }

  type ConcreteImplementorA struct{}
  func (c *ConcreteImplementorA) Operation() string {
      return "ConcreteImplementorA"
  }

  type Abstraction struct {
      implementor Implementor
  }

  func (a *Abstraction) Operation() string {
      return a.implementor.Operation()
  }

  func ClientCode(a *Abstraction) {
      fmt.Println(a.Operation())
  }
  ```

## **3. Behavioral Patterns**

### **3.1. Strategy**
- **Description:** Defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable.
- **Example:**
  ```go
  package main

  import "fmt"

  type Strategy interface {
      Execute() string
  }

  type StrategyA struct{}
  func (s *StrategyA) Execute() string {
      return "Strategy A"
  }

  type StrategyB struct{}
  func (s *StrategyB) Execute() string {
      return "Strategy B"
  }

  type Context struct {
      strategy Strategy
  }

  func (c *Context) SetStrategy(strategy Strategy) {
      c.strategy = strategy
  }

  func (c *Context) ExecuteStrategy() {
      fmt.Println(c.strategy.Execute())
  }

  func ClientCode() {
      context := &Context{}
      context.SetStrategy(&StrategyA{})
      context.ExecuteStrategy()
      context.SetStrategy(&StrategyB{})
      context.ExecuteStrategy()
  }
  ```

### **3.2. Observer**
- **Description:** Allows an object to notify other objects about changes in its state.
- **Example:**
  ```go
  package main

  import "fmt"

  type Observer interface {
      Update(string)
  }

  type Subject struct {
      observers []Observer
      state     string
  }

  func (s *Subject) Attach(observer Observer) {
      s.observers = append(s.observers, observer)
  }

  func (s *Subject) SetState(state string) {
      s.state = state
      s.Notify()
  }

  func (s *Subject) Notify() {
      for _, observer := range s.observers {
          observer.Update(s.state)
      }
  }

  type ConcreteObserver struct {
      name string
  }

  func (o *ConcreteObserver) Update(state string) {
      fmt.Printf("%s received state %s\n", o.name, state)
  }

  func ClientCode() {
      subject := &Subject{}
      observer1 := &ConcreteObserver{name: "Observer1"}
      subject.Attach(observer1)
      subject.SetState("New State")
  }
  ```

### **3.3. Command**
- **Description:** Encapsulates a request as an object, allowing parameterization and queuing of requests.
- **Example:**
  ```go
  package main

  import "fmt"

  type Command interface {
      Execute()
  }

  type Receiver struct{}
  func (r *Receiver) Action() {
      fmt.Println("Receiver Action")
  }

  type ConcreteCommand struct {
      receiver *Receiver
  }

  func (c *ConcreteCommand) Execute() {
      c.receiver.Action()
  }

  type Invoker struct {
      command Command
  }

  func (i *Invoker) SetCommand(command Command) {
      i.command = command
  }

  func (i *Invoker) Invoke() {
      i.command.Execute()
  }

  func ClientCode() {
      receiver := &Receiver{}
      command := &ConcreteCommand{receiver: receiver}
      invoker := &Invoker{}
      invoker.SetCommand(command)
      invoker.Invoke()
  }
  ```

### **3.4. Template Method**
- **Description:** Defines the skeleton of an algorithm in a superclass but lets subclasses override specific steps of the algorithm without changing its structure.
- **Example:

**
  ```go
  package main

  import "fmt"

  type AbstractClass interface {
      TemplateMethod()
      PrimitiveOperation1()
      PrimitiveOperation2()
  }

  type ConcreteClass struct{}

  func (c *ConcreteClass) TemplateMethod() {
      fmt.Println("ConcreteClass: TemplateMethod")
      c.PrimitiveOperation1()
      c.PrimitiveOperation2()
  }

  func (c *ConcreteClass) PrimitiveOperation1() {
      fmt.Println("ConcreteClass: PrimitiveOperation1")
  }

  func (c *ConcreteClass) PrimitiveOperation2() {
      fmt.Println("ConcreteClass: PrimitiveOperation2")
  }

  func ClientCode(c AbstractClass) {
      c.TemplateMethod()
  }

  func main() {
      c := &ConcreteClass{}
      ClientCode(c)
  }
  ```