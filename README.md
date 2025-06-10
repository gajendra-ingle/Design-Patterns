 # 💡 Low-Level System Design and Patterns

Welcome to the **Low-Level System Design and Patterns** repository! This repository contains an overview of essential low-level design concepts, focusing on famous design patterns and their use cases in software engineering.

## 📚 Table of Contents

1. [Introduction to SOLID Principles](#introduction-to-solid-principles)
2. [Why Low-Level Design Patterns?](#why-low-level-design-patterns)
3. [Famous Design Patterns](#famous-design-patterns)
   - [1. Singleton Pattern](#singleton-pattern)
   - [2. Factory Pattern](#factory-pattern)
   - [3. Builder Pattern](#builder-pattern)
   - [4. Adapter Pattern](#adapter-pattern)
   - [5. Observer Pattern](#observer-pattern)
   - [6. Strategy Pattern](#strategy-pattern)
   - [7. Command Pattern](#command-pattern)
   - [8. Decorator Pattern](#decorator-pattern)

## Introduction to SOLID Principles

The SOLID principles are a set of five design principles that enable developers to write more maintainable, understandable, and flexible code. These principles form the foundation of good object-oriented design and are critical in creating scalable software systems.

- **S**: **Single Responsibility Principle (SRP)** - A class should have one, and only one, reason to change. It ensures that a class has only one job or responsibility.

- **O**: **Open/Closed Principle (OCP)** - Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. It promotes building systems that are easily extendable without altering existing code.

- **L**: **Liskov Substitution Principle (LSP)** - Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. It ensures that a derived class can be used in place of a base class.

- **I**: **Interface Segregation Principle (ISP)** - No client should be forced to depend on methods it does not use. It promotes creating small, specific interfaces rather than large, monolithic ones.

- **D**: **Dependency Inversion Principle (DIP)** - High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). This principle reduces the coupling between software modules.

## ❓ Why Low-Level Design Patterns?

Low-level design patterns are instrumental in solving recurring problems in software design. These patterns provide a template or blueprint for structuring code in a way that is both efficient and maintainable. They are particularly useful in:

- **Code Reusability**: Patterns like Singleton and Factory promote code reuse by standardizing object creation and management.
- **Flexibility and Extensibility**: Patterns such as Strategy and Decorator allow the system to adapt to new requirements with minimal changes.
- **Decoupling**: Patterns like Observer and Adapter reduce the dependencies between different parts of a system, making it more modular and easier to maintain.
- **Testability**: By following patterns, code becomes more modular, making it easier to write unit tests and achieve better test coverage.

##  🧩 Famous Design Patterns

### 1. 🔁 Singleton Pattern

The Singleton Pattern ensures a class has only one instance and provides a global point of access to it. This pattern is commonly used in scenarios where a single resource, such as a database connection or a configuration file, needs to be shared across the system.

**Example**:
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {} // private constructor

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 2. 🏭 Factory Pattern

The Factory Pattern provides an interface for creating objects but allows subclasses to alter the type of objects that will be created. It is widely used in cases where the exact type of the object might not be known until runtime.

**Example**:
```java
interface Animal {
    void speak();
}

class Dog implements Animal {
    public void speak() {
        System.out.println("Woof");
    }
}

class Cat implements Animal {
    public void speak() {
        System.out.println("Meow");
    }
}

class AnimalFactory {
    public static Animal getAnimal(String type) {
        return switch (type) {
            case "dog" -> new Dog();
            case "cat" -> new Cat();
            default -> throw new IllegalArgumentException("Unknown type");
        };
    }
}
```

### 3. 🏗️ Builder Pattern

The Builder Pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations. This pattern is particularly useful for creating objects with numerous optional parameters.

**Example**:
```java
class Car {
    private String engine;
    private String color;
    private int wheels;

    // Private constructor so objects can only be created via the Builder
    private Car() {}

    // Static nested Builder class
    public static class Builder {
        private final Car car = new Car();

        public Builder setEngine(String engine) {
            car.engine = engine;
            return this;
        }

        public Builder setColor(String color) {
            car.color = color;
            return this;
        }

        public Builder setWheels(int wheels) {
            car.wheels = wheels;
            return this;
        }

        public Car build() {
            return car;
        }
    }

    // For demonstration purposes
    @Override
    public String toString() {
        return "Car [engine=" + engine + ", color=" + color + ", wheels=" + wheels + "]";
    }
}
```

### 4. 🔌 Adapter Pattern

The Adapter Pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, enabling them to collaborate. This pattern is often used when integrating new components into a legacy system.

**Example**:
```java
class OldPrinter {
    public void printText(String text) {
        System.out.println(text);
    }
}

interface NewPrinter {
    void print(String text);
}

class PrinterAdapter implements NewPrinter {
    private final OldPrinter oldPrinter;

    public PrinterAdapter(OldPrinter oldPrinter) {
        this.oldPrinter = oldPrinter;
    }

    public void print(String text) {
        oldPrinter.printText(text);
    }
}
```

### 5. 👀 Observer Pattern

The Observer Pattern defines a one-to-many dependency between objects, so when one object changes state, all its dependents are notified and updated automatically. This pattern is commonly used in event-driven systems.

**Example**:
```java
interface Observer {
    void update(String msg);
}

class EmailClient implements Observer {
    public void update(String msg) {
        System.out.println("Email received: " + msg);
    }
}

class NotificationService {
    private final List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer o) { observers.add(o); }

    public void notifyObservers(String msg) {
        for (Observer o : observers) o.update(msg);
    }
}
```

### 6. 🧠 Strategy Pattern

The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. This pattern allows the algorithm to vary independently from clients that use it, promoting flexibility in choosing algorithms at runtime.

**Example**:
```java
interface PaymentStrategy {
    void pay(int amount);
}

class CreditCard implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class PayPal implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}

class PaymentContext {
    private PaymentStrategy strategy;

    public PaymentContext(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void executePayment(int amount) {
        strategy.pay(amount);
    }
}
```

### 7. 📝 Command Pattern

The Command Pattern encapsulates a request as an object, thereby allowing users to parameterize clients with queues, requests, and operations. It is often used in systems that require undo/redo operations.

**Example**:
```java
interface Command {
    void execute();
}

class Light {
    void turnOn() { System.out.println("Light ON"); }
}

class TurnOnCommand implements Command {
    private final Light light;

    public TurnOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class RemoteControl {
    public void submit(Command command) {
        command.execute();
    }
}
```

### 8. 🎨 Decorator Pattern

The Decorator Pattern attaches additional responsibilities to an object dynamically. This pattern is useful for adding functionalities to objects without altering their structure, promoting adherence to the Open/Closed Principle.

**Example**:
```java
interface Coffee {
    String getDescription();
}

class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Plain Coffee";
    }
}

class MilkDecorator implements Coffee {
    private final Coffee coffee;

    public MilkDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }
}
```
