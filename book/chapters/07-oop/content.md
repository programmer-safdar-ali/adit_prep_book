# Chapter 7: Object-Oriented Programming (OOP)

---

## Chapter Overview

- **Domain**: Software Engineering and Programming Paradigms
- **Estimated Study Time**: 5-6 hours
- **Prerequisites**: Basic programming concepts, Chapter 6 (Data Structures)
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Define** the four pillars of OOP: encapsulation, inheritance, polymorphism, and abstraction (B)
2. **Explain** classes, objects, constructors, and access modifiers (B)
3. **Implement** inheritance hierarchies and understand method overriding (I)
4. **Apply** polymorphism through interfaces and abstract classes (I)
5. **Analyze** code for adherence to SOLID principles (A)
6. **Evaluate** appropriate design patterns for common software problems (A)
7. **Design** class hierarchies and UML diagrams for complex systems (E)
8. **Assess** trade-offs between composition and inheritance in software architecture (E)

---

## Introduction

Object-Oriented Programming is the dominant programming paradigm in enterprise software development. Understanding OOP concepts is essential for evaluating software architecture, communicating with development teams, and making informed decisions about technology choices.

As an Assistant Director IT, you will encounter OOP concepts when reviewing technical specifications, evaluating vendor solutions, and overseeing software projects. Whether systems are built in Java, C#, Python, or other OOP languages, the fundamental concepts remain consistent.

This chapter covers OOP fundamentals, design principles, and common design patterns. These concepts connect to software development methodologies (Chapter 8), programming languages (Chapter 25), and system design principles used throughout modern software.

---

## Section 7.1: Core OOP Concepts (B)

Object-Oriented Programming organizes software around objects that contain data and behavior.

### 7.1.1 Classes and Objects

**Class**: A blueprint or template that defines attributes (data) and methods (behavior).

**Object**: An instance of a class with specific values for its attributes.

**Example**:
```
Class: Employee
├── Attributes: name, employeeId, salary, department
└── Methods: calculateBonus(), promote(), getDetails()

Object: employee1
├── name = "Ahmed Khan"
├── employeeId = "E001"
├── salary = 75000
└── department = "IT"
```

### 7.1.2 The Four Pillars of OOP

**1. Encapsulation**:
- Bundling data and methods that operate on that data
- Hiding internal state from outside access
- Providing controlled access through public methods (getters/setters)
- Protects data integrity

**Example**:
```
class BankAccount:
    private balance = 0

    public deposit(amount):
        if amount > 0:
            balance += amount

    public getBalance():
        return balance

# External code cannot directly modify balance
# Must use deposit() method which validates input
```

**2. Inheritance**:
- Creating new classes based on existing classes
- Child class inherits attributes and methods from parent
- Promotes code reuse
- Establishes "is-a" relationships

**Example**:
```
class Person:
    name, dateOfBirth

class Employee extends Person:
    employeeId, salary, department
    # Inherits name and dateOfBirth

class Manager extends Employee:
    teamSize, budget
    # Inherits all from Person and Employee
```

**3. Polymorphism**:
- Objects of different classes responding to the same method call
- "Many forms" - same interface, different implementations
- Enables flexible and extensible code

**Types**:
- **Compile-time (Method Overloading)**: Same method name, different parameters
- **Runtime (Method Overriding)**: Subclass provides different implementation

**Example**:
```
class Shape:
    abstract calculateArea()

class Circle extends Shape:
    calculateArea():
        return π * radius²

class Rectangle extends Shape:
    calculateArea():
        return width * height

# Same method call, different behavior
shapes = [Circle(5), Rectangle(4, 6)]
for shape in shapes:
    print(shape.calculateArea())  # Polymorphic call
```

**4. Abstraction**:
- Hiding complex implementation details
- Exposing only essential features
- Reducing complexity for users of the class

**Mechanisms**:
- Abstract classes: Can have abstract and concrete methods
- Interfaces: Only define method signatures

### Practical Example 7.1: OOP in Practice

**Scenario**: Design a government document management system.

**Class Hierarchy**:
```
Document (Abstract)
├── Attributes: id, title, createdDate, author
├── Methods: display(), archive(), getMetadata()
│
├── OfficialDocument
│   ├── Attributes: approvalStatus, signatory
│   ├── Methods: approve(), reject()
│   │
│   ├── Policy extends OfficialDocument
│   │   └── Attributes: effectiveDate, department
│   │
│   └── Contract extends OfficialDocument
│       └── Attributes: parties, value, expiryDate
│
└── InternalMemo
    ├── Attributes: recipients, priority
    └── Methods: send(), recall()
```

**Design Benefits**:
- Encapsulation: Document details protected
- Inheritance: Shared attributes in parent classes
- Polymorphism: `archive()` works differently for each type
- Abstraction: Users interact with simple interfaces

---

## Section 7.2: Classes and Objects in Detail (B)

### 7.2.1 Class Members

**Instance Variables**: Belong to each object instance
**Static/Class Variables**: Shared across all instances
**Instance Methods**: Operate on instance data
**Static/Class Methods**: Operate on class-level data

```
class Employee:
    # Static variable
    static employeeCount = 0

    # Instance variables
    name
    salary

    # Constructor
    constructor(name, salary):
        this.name = name
        this.salary = salary
        Employee.employeeCount += 1

    # Instance method
    getDetails():
        return f"{this.name}: {this.salary}"

    # Static method
    static getTotalEmployees():
        return Employee.employeeCount
```

### 7.2.2 Constructors and Destructors

**Constructor**: Special method called when creating an object
- Initializes object state
- Can be overloaded (multiple constructors)
- Default constructor takes no arguments
- Parameterized constructor accepts initial values

**Destructor**: Called when object is destroyed
- Releases resources (file handles, connections)
- Automatic in garbage-collected languages
- Explicit in languages like C++

**Constructor Types**:
| Type | Description | Example |
|------|-------------|---------|
| Default | No parameters | `Employee()` |
| Parameterized | Takes parameters | `Employee(name, salary)` |
| Copy | Creates copy of object | `Employee(otherEmployee)` |
| Move | Transfers ownership | `Employee(std::move(temp))` |

### 7.2.3 Access Modifiers

Access modifiers control visibility of class members:

| Modifier | Same Class | Subclass | Package | Other |
|----------|------------|----------|---------|-------|
| private | ✓ | ✗ | ✗ | ✗ |
| protected | ✓ | ✓ | ✓* | ✗ |
| public | ✓ | ✓ | ✓ | ✓ |
| default/package | ✓ | ✓* | ✓ | ✗ |

*Varies by language

**Best Practice**: Use most restrictive access possible
- Private: Internal implementation details
- Protected: For subclass extension
- Public: External API

### Practical Example 7.2: Proper Encapsulation

**Scenario**: Implement a secure employee salary management.

**Poor Design** (no encapsulation):
```
class Employee:
    public salary  # Direct access - dangerous!

employee.salary = -50000  # Invalid salary allowed!
```

**Good Design** (proper encapsulation):
```
class Employee:
    private salary

    public setSalary(amount):
        if amount < 0:
            raise InvalidSalaryError
        if amount > 10000000:
            raise SalaryLimitExceeded
        this.salary = amount

    public getSalary():
        return this.salary
```

---

## Section 7.3: Inheritance (I)

### 7.3.1 Types of Inheritance

**Single Inheritance**: One parent class
```
Animal → Dog
```

**Multiple Inheritance**: Multiple parent classes (not all languages support)
```
FlyingObject, Animal → Bird
```

**Multilevel Inheritance**: Chain of inheritance
```
Animal → Mammal → Dog
```

**Hierarchical Inheritance**: Multiple children from one parent
```
        Animal
       /  |  \
     Dog Cat Bird
```

### 7.3.2 Method Overriding

Subclass provides specific implementation of inherited method:

```
class Animal:
    speak():
        print("Some sound")

class Dog extends Animal:
    @Override
    speak():
        print("Bark!")

class Cat extends Animal:
    @Override
    speak():
        print("Meow!")

# Runtime polymorphism
animals = [Dog(), Cat()]
for animal in animals:
    animal.speak()  # Outputs: Bark! Meow!
```

**Rules for Overriding**:
- Same method signature
- Return type must be same or covariant
- Access cannot be more restrictive
- Cannot override `final` methods
- Use `super` to call parent implementation

### 7.3.3 The 'super' Keyword

Calls parent class methods or constructor:

```
class Manager extends Employee:
    teamSize

    constructor(name, salary, teamSize):
        super(name, salary)  # Call parent constructor
        this.teamSize = teamSize

    getDetails():
        return super.getDetails() + f", Team: {this.teamSize}"
```

### Practical Example 7.3: Inheritance Hierarchy

**Scenario**: Design class hierarchy for government vehicles.

```
Vehicle (Abstract)
├── Attributes: registrationNumber, make, model, year
├── Methods: start(), stop(), getMaintenanceSchedule()
│
├── GroundVehicle
│   ├── Attributes: numberOfWheels, fuelType
│   │
│   ├── Car
│   │   └── Attributes: seatingCapacity, trunkSize
│   │
│   ├── Motorcycle
│   │   └── Attributes: engineCC, hasSidecar
│   │
│   └── Truck
│       └── Attributes: loadCapacity, axleCount
│
└── WaterVehicle
    ├── Attributes: hullType, displacement
    │
    └── Boat
        └── Attributes: passengerCapacity, maxSpeed
```

---

## Section 7.4: Polymorphism and Abstraction (I)

### 7.4.1 Abstract Classes

Abstract classes cannot be instantiated and may contain abstract methods:

```
abstract class Document:
    title
    author

    # Concrete method
    getMetadata():
        return f"{this.title} by {this.author}"

    # Abstract method - must be implemented by subclasses
    abstract process()
    abstract validate()

class Contract extends Document:
    process():
        # Contract-specific processing
        validateSignatures()
        checkExpiry()

    validate():
        # Contract-specific validation
        return parties.length >= 2
```

### 7.4.2 Interfaces

Interfaces define contracts that implementing classes must fulfill:

```
interface Printable:
    print()
    getPrintPreview()

interface Exportable:
    exportToPDF()
    exportToWord()

class Report implements Printable, Exportable:
    print():
        # Implementation

    getPrintPreview():
        # Implementation

    exportToPDF():
        # Implementation

    exportToWord():
        # Implementation
```

**Abstract Class vs Interface**:

| Aspect | Abstract Class | Interface |
|--------|----------------|-----------|
| Instantiation | No | No |
| Constructor | Yes | No |
| Concrete methods | Yes | No (traditionally)* |
| Multiple inheritance | No | Yes |
| State (variables) | Yes | No (constants only) |
| Access modifiers | Any | Public only |

*Modern languages (Java 8+, C# 8+) allow default implementations

### 7.4.3 Compile-time Polymorphism (Overloading)

Method overloading: Same name, different parameters

```
class Calculator:
    add(a, b):
        return a + b

    add(a, b, c):
        return a + b + c

    add(numbers[]):
        return sum(numbers)

calc = Calculator()
calc.add(5, 3)        # Returns 8
calc.add(5, 3, 2)     # Returns 10
calc.add([1,2,3,4])   # Returns 10
```

### Practical Example 7.4: Interface-Based Design

**Scenario**: Design a notification system that supports multiple channels.

```
interface NotificationChannel:
    send(message, recipient)
    getDeliveryStatus(messageId)

class EmailNotification implements NotificationChannel:
    send(message, recipient):
        # Send via SMTP
        smtpClient.send(recipient.email, message)

    getDeliveryStatus(messageId):
        return emailTracker.getStatus(messageId)

class SMSNotification implements NotificationChannel:
    send(message, recipient):
        # Send via SMS gateway
        smsGateway.send(recipient.phone, message)

    getDeliveryStatus(messageId):
        return smsGateway.getStatus(messageId)

class PushNotification implements NotificationChannel:
    send(message, recipient):
        # Send push notification
        pushService.send(recipient.deviceToken, message)

    getDeliveryStatus(messageId):
        return pushService.getStatus(messageId)

# Usage - polymorphic behavior
class NotificationService:
    channels: List<NotificationChannel>

    notify(message, recipient):
        for channel in channels:
            channel.send(message, recipient)  # Works for all types
```

---

## Section 7.5: SOLID Principles (A)

SOLID principles guide good object-oriented design.

### 7.5.1 Single Responsibility Principle (SRP)

A class should have only one reason to change.

**Violation**:
```
class Employee:
    calculateSalary()      # Payroll responsibility
    generateReport()       # Reporting responsibility
    saveToDatabase()       # Persistence responsibility
```

**Correct Design**:
```
class Employee:
    name, salary, department

class PayrollCalculator:
    calculateSalary(employee)

class EmployeeReportGenerator:
    generateReport(employee)

class EmployeeRepository:
    save(employee)
    find(id)
```

### 7.5.2 Open/Closed Principle (OCP)

Classes should be open for extension, closed for modification.

**Violation**:
```
class DiscountCalculator:
    calculateDiscount(customer):
        if customer.type == "Regular":
            return 0.1
        elif customer.type == "Premium":
            return 0.2
        elif customer.type == "VIP":    # New type requires modifying class
            return 0.3
```

**Correct Design**:
```
interface DiscountStrategy:
    calculate(customer)

class RegularDiscount implements DiscountStrategy:
    calculate(customer): return 0.1

class PremiumDiscount implements DiscountStrategy:
    calculate(customer): return 0.2

class VIPDiscount implements DiscountStrategy:
    calculate(customer): return 0.3

# New discount types don't require modifying existing code
```

### 7.5.3 Liskov Substitution Principle (LSP)

Subtypes must be substitutable for their base types.

**Violation**:
```
class Rectangle:
    setWidth(w), setHeight(h)
    getArea(): return width * height

class Square extends Rectangle:
    setWidth(w): width = w; height = w  # Breaks LSP!
    setHeight(h): width = h; height = h

# This fails:
rect = Square()
rect.setWidth(5)
rect.setHeight(10)
rect.getArea()  # Expected: 50, Actual: 100
```

**Correct Design**: Don't use inheritance when behavior differs significantly.

### 7.5.4 Interface Segregation Principle (ISP)

Clients should not depend on interfaces they don't use.

**Violation**:
```
interface Worker:
    work()
    eat()
    sleep()

class Robot implements Worker:
    work(): # OK
    eat(): # Robots don't eat - forced to implement!
    sleep(): # Robots don't sleep!
```

**Correct Design**:
```
interface Workable:
    work()

interface Feedable:
    eat()

interface Restable:
    sleep()

class Human implements Workable, Feedable, Restable:
    work(), eat(), sleep()

class Robot implements Workable:
    work()  # Only implements what it needs
```

### 7.5.5 Dependency Inversion Principle (DIP)

High-level modules should depend on abstractions, not low-level modules.

**Violation**:
```
class NotificationService:
    emailSender = new EmailSender()  # Tight coupling to concrete class

    notify(message):
        emailSender.send(message)
```

**Correct Design**:
```
interface MessageSender:
    send(message)

class NotificationService:
    sender: MessageSender  # Depends on abstraction

    constructor(sender: MessageSender):
        this.sender = sender

    notify(message):
        sender.send(message)

# Can inject any implementation
service = NotificationService(new EmailSender())
service = NotificationService(new SMSSender())
```

---

## Section 7.6: Design Patterns (A)

Design patterns are proven solutions to common software design problems.

### 7.6.1 Creational Patterns

**Singleton**: Ensure only one instance exists
```
class ConfigurationManager:
    private static instance

    private constructor()  # Prevent external instantiation

    static getInstance():
        if instance == null:
            instance = new ConfigurationManager()
        return instance
```

**Factory Method**: Create objects without specifying exact class
```
interface Document:
    open()

class PDFDocument implements Document
class WordDocument implements Document

class DocumentFactory:
    static createDocument(type):
        if type == "PDF": return new PDFDocument()
        if type == "Word": return new WordDocument()
```

**Builder**: Construct complex objects step by step
```
class ReportBuilder:
    setTitle(title): return this
    addSection(section): return this
    addChart(chart): return this
    build(): return Report(...)

# Usage
report = ReportBuilder()
    .setTitle("Monthly Report")
    .addSection(intro)
    .addChart(salesChart)
    .build()
```

### 7.6.2 Structural Patterns

**Adapter**: Convert interface to compatible interface
```
# Legacy system uses XML
class LegacyXMLService:
    processXML(xml)

# New system uses JSON
interface ModernService:
    processJSON(json)

class XMLAdapter implements ModernService:
    legacyService: LegacyXMLService

    processJSON(json):
        xml = convertJSONtoXML(json)
        legacyService.processXML(xml)
```

**Facade**: Provide simplified interface to complex system
```
class GovernmentServiceFacade:
    # Hides complexity of multiple subsystems

    registerCitizen(data):
        nadraService.createCNIC(data)
        taxService.registerTaxpayer(data)
        voterService.registerVoter(data)
        return "Registration complete"
```

**Decorator**: Add behavior to objects dynamically
```
interface Coffee:
    getCost()
    getDescription()

class SimpleCoffee implements Coffee:
    getCost(): return 100
    getDescription(): return "Coffee"

class MilkDecorator implements Coffee:
    coffee: Coffee

    getCost(): return coffee.getCost() + 20
    getDescription(): return coffee.getDescription() + ", Milk"

# Usage
coffee = MilkDecorator(SimpleCoffee())
# Cost: 120, Description: "Coffee, Milk"
```

### 7.6.3 Behavioral Patterns

**Observer**: Notify dependent objects of state changes
```
interface Observer:
    update(data)

interface Subject:
    attach(observer)
    detach(observer)
    notify()

class StockPrice implements Subject:
    observers: List<Observer>
    price

    setPrice(newPrice):
        price = newPrice
        notify()

    notify():
        for observer in observers:
            observer.update(price)

class StockAlert implements Observer:
    update(price):
        if price > threshold:
            sendAlert()
```

**Strategy**: Define family of algorithms, make them interchangeable
```
interface SortStrategy:
    sort(data)

class QuickSortStrategy implements SortStrategy:
    sort(data): # Quick sort implementation

class MergeSortStrategy implements SortStrategy:
    sort(data): # Merge sort implementation

class DataProcessor:
    strategy: SortStrategy

    process(data):
        strategy.sort(data)
```

**Template Method**: Define algorithm skeleton, defer steps to subclasses
```
abstract class ReportGenerator:
    # Template method
    final generateReport():
        collectData()
        processData()
        formatReport()
        output()

    abstract collectData()
    abstract processData()

    formatReport():  # Default implementation
        # Standard formatting

    abstract output()

class PDFReportGenerator extends ReportGenerator:
    collectData(): # PDF-specific
    processData(): # PDF-specific
    output(): # Output as PDF
```

### Practical Example 7.5: Applying Design Patterns

**Scenario**: Design a logging system for government applications.

**Patterns Applied**:

1. **Singleton**: LogManager instance
```
class LogManager:
    private static instance
    static getInstance(): return instance
```

2. **Strategy**: Different logging strategies
```
interface LogStrategy:
    log(message)

class FileLogStrategy implements LogStrategy
class DatabaseLogStrategy implements LogStrategy
class ConsoleLogStrategy implements LogStrategy
```

3. **Decorator**: Add features to logs
```
class TimestampDecorator implements LogStrategy
class EncryptionDecorator implements LogStrategy
```

4. **Observer**: Multiple log consumers
```
class LogManager:
    observers: [FileLogger, AlertSystem, AuditService]

    log(message):
        for observer in observers:
            observer.update(message)
```

---

## Section 7.7: UML Diagrams (E)

Unified Modeling Language (UML) provides standard notation for visualizing software design.

### 7.7.1 Class Diagrams

Show classes, attributes, methods, and relationships.

**Relationships**:

| Relationship | Symbol | Meaning |
|--------------|--------|---------|
| Association | → | Uses |
| Aggregation | ◇→ | Has-a (weak) |
| Composition | ◆→ | Has-a (strong) |
| Inheritance | △→ | Is-a |
| Implementation | △--→ | Implements |
| Dependency | - - - → | Depends on |

**Class Notation**:
```
┌─────────────────────┐
│     ClassName       │
├─────────────────────┤
│ - privateAttr       │
│ # protectedAttr     │
│ + publicAttr        │
├─────────────────────┤
│ + publicMethod()    │
│ - privateMethod()   │
│ # protectedMethod() │
└─────────────────────┘
```

### 7.7.2 Sequence Diagrams

Show object interactions over time.

```
User        UI        Controller      Service       Database
  |          |            |              |              |
  |--click-->|            |              |              |
  |          |--request-->|              |              |
  |          |            |--getData()-->|              |
  |          |            |              |--query()---->|
  |          |            |              |<--results----|
  |          |            |<--data-------|              |
  |          |<--display--|              |              |
  |<-response|            |              |              |
```

### 7.7.3 Use Case Diagrams

Show system functionality from user perspective.

```
                    ┌─────────────────────────────┐
                    │   Government Portal System  │
                    │                             │
  ┌───────┐         │  ┌───────────────────┐      │
  │Citizen│────────>│  │ Apply for License │      │
  └───────┘         │  └───────────────────┘      │
      │             │                             │
      │             │  ┌───────────────────┐      │
      └────────────>│  │ Check Status      │      │
                    │  └───────────────────┘      │
                    │                             │
  ┌───────┐         │  ┌───────────────────┐      │
  │ Admin │────────>│  │ Process Request   │      │
  └───────┘         │  └───────────────────┘      │
                    └─────────────────────────────┘
```

### 7.7.4 Activity Diagrams

Show workflow and process flow.

```
    ●
    │
    ▼
┌─────────────┐
│Submit Form  │
└─────────────┘
    │
    ▼
◇───────────────────────◇
│                       │
│   [Valid]    [Invalid]│
│                       │
▼                       ▼
┌───────────┐    ┌──────────────┐
│ Process   │    │ Show Errors  │
└───────────┘    └──────────────┘
│                       │
│                       │
└──────────┬────────────┘
           │
           ▼
          ◉
```

---

## Section 7.8: Composition vs Inheritance (E)

### 7.8.1 Composition

Objects contain other objects ("has-a" relationship).

```
class Engine:
    start()
    stop()

class Car:
    engine: Engine  # Composition

    start():
        engine.start()
```

**Advantages**:
- More flexible at runtime
- No tight coupling to parent
- Easier to test (mock dependencies)
- Avoids inheritance hierarchy problems

### 7.8.2 When to Use Each

| Criteria | Inheritance | Composition |
|----------|-------------|-------------|
| Relationship | "Is-a" | "Has-a" |
| Reuse | Whole class behavior | Selective behavior |
| Flexibility | Less (compile-time) | More (runtime) |
| Coupling | Tight | Loose |
| Testing | Harder | Easier |

**Prefer Composition When**:
- Relationship is "has-a" not "is-a"
- Need to swap behavior at runtime
- Parent class may change
- Need to combine behaviors from multiple sources

**Use Inheritance When**:
- Clear "is-a" relationship
- Want to use polymorphism
- Parent class is stable
- Code reuse fits naturally

### Practical Example 7.6: Refactoring to Composition

**Before (Inheritance)**:
```
class TextReport extends Report
class PDFReport extends Report
class EncryptedTextReport extends TextReport  # Gets messy!
class EncryptedPDFReport extends PDFReport    # Duplication!
```

**After (Composition)**:
```
interface Formatter:
    format(data)

interface Encryptor:
    encrypt(data)

class Report:
    formatter: Formatter
    encryptor: Encryptor

    generate():
        data = formatter.format(raw)
        if encryptor:
            data = encryptor.encrypt(data)
        return data

# Mix and match any combination
report = Report(PDFFormatter(), AESEncryptor())
```

---

## Hands-on Labs

### Lab 7.1: Class Design and Encapsulation

See [labs/lab-07-01-encapsulation.md](labs/lab-07-01-encapsulation.md) for complete lab instructions.

**Objective**: Design classes with proper encapsulation and access modifiers.

### Lab 7.2: Inheritance Hierarchies

See [labs/lab-07-02-inheritance.md](labs/lab-07-02-inheritance.md) for complete lab instructions.

**Objective**: Build inheritance hierarchies and implement method overriding.

### Lab 7.3: Interfaces and Polymorphism

See [labs/lab-07-03-polymorphism.md](labs/lab-07-03-polymorphism.md) for complete lab instructions.

**Objective**: Implement interfaces and demonstrate polymorphic behavior.

### Lab 7.4: Design Patterns

See [labs/lab-07-04-design-patterns.md](labs/lab-07-04-design-patterns.md) for complete lab instructions.

**Objective**: Apply Singleton, Factory, and Observer patterns.

### Lab 7.5: UML Diagram Creation

See [labs/lab-07-05-uml.md](labs/lab-07-05-uml.md) for complete lab instructions.

**Objective**: Create class diagrams and sequence diagrams for a system.

---

## Chapter Summary

Key points covered in this chapter:

- OOP organizes software around objects containing data (attributes) and behavior (methods).
- The four pillars of OOP are encapsulation (data hiding), inheritance (code reuse), polymorphism (many forms), and abstraction (hiding complexity).
- Access modifiers (private, protected, public) control visibility and protect internal state.
- Inheritance establishes "is-a" relationships; method overriding enables runtime polymorphism.
- Abstract classes and interfaces define contracts; interfaces support multiple inheritance.
- SOLID principles guide good design: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.
- Design patterns provide proven solutions: Creational (Singleton, Factory, Builder), Structural (Adapter, Facade, Decorator), Behavioral (Observer, Strategy, Template Method).
- UML diagrams (class, sequence, use case, activity) visualize software design.
- Composition is often preferred over inheritance for flexibility and loose coupling.

---

## Key Takeaways

1. **Encapsulation protects data integrity**: Always use private fields with public getters/setters that validate input.

2. **Favor composition over inheritance**: More flexible, easier to test, and avoids deep inheritance hierarchies.

3. **Program to interfaces, not implementations**: Depend on abstractions for flexibility and testability.

4. **SOLID principles improve maintainability**: Apply them consistently for code that's easier to extend and modify.

5. **Design patterns are tools, not rules**: Use them when they solve real problems, not for their own sake.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Explain encapsulation** with an example of a BankAccount class. How does proper encapsulation prevent invalid states? (B/I)

2. **Compare abstract classes and interfaces**. When would you use each, and what are the limitations of each approach? (I/A)

3. **Analyze this code for SOLID violations**:
   ```
   class ReportService:
       generatePDFReport()
       generateExcelReport()
       sendEmailWithReport()
       saveReportToDatabase()
   ```
   Refactor it to follow SOLID principles. (A)

4. **Design a class hierarchy** for a government human resource system that handles different employee types (permanent, contract, consultant) with different leave policies and benefits calculations. Include UML class diagram. (E)

5. **Evaluate the trade-offs** between using inheritance vs. composition for a document management system that needs to support different document types (PDF, Word, Image) with different operations (view, edit, print, encrypt). Propose a design using composition and justify your choices. (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 40 Beginner (B) questions (25%)
- 56 Intermediate (I) questions (35%)
- 48 Advanced (A) questions (30%)
- 16 Expert (E) questions (10%)

Total: 160 MCQs

---

## References

- Gamma, Erich, et al. "Design Patterns: Elements of Reusable Object-Oriented Software." Addison-Wesley, 1994.
- Martin, Robert C. "Clean Code: A Handbook of Agile Software Craftsmanship." Prentice Hall, 2008.
- Martin, Robert C. "Agile Software Development, Principles, Patterns, and Practices." Prentice Hall, 2002.
- Bloch, Joshua. "Effective Java." 3rd Edition. Addison-Wesley, 2018.
- Freeman, Eric, et al. "Head First Design Patterns." O'Reilly, 2020.
- Fowler, Martin. "UML Distilled." 3rd Edition. Addison-Wesley, 2003.
- OMG. "Unified Modeling Language Specification." https://www.omg.org/spec/UML/

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
