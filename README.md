# Design-Pattern-With-Java
All design patterns explained with the java code example

### Creational Patterns
Creational design patterns deal with object creation mechanisms, aiming to create objects in a manner suitable to the situation.

1. **Singleton**: Ensures that a class has only one instance and provides a global point of access to it.
2. **Factory Method**: Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.
3. **Abstract Factory**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
4. **Builder**: Separates the construction of a complex object from its representation so that the same construction process can create different representations.
5. **Prototype**: Specifies the kinds of objects to create using a prototypical instance and creates new objects by copying this prototype.

### Structural Patterns
Structural patterns deal with object composition or the way classes and objects are composed to form larger structures.

6. **Adapter**: Allows the interface of an existing class to be used as another interface.
7. **Bridge**: Separates an object’s interface from its implementation, allowing the two to vary independently.
8. **Composite**: Composes objects into tree structures to represent part-whole hierarchies. It allows clients to treat individual objects and compositions uniformly.
9. **Decorator**: Attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
10. **Facade**: Provides a simplified interface to a complex subsystem.
11. **Flyweight**: Uses sharing to support large numbers of fine-grained objects efficiently.
12. **Proxy**: Provides a surrogate or placeholder for another object to control access to it.

### Behavioral Patterns
Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects.

13. **Chain of Responsibility**: Passes a request along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain.
14. **Command**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
15. **Interpreter**: Defines a representation for a grammar and an interpreter to deal with this grammar.
16. **Iterator**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
17. **Mediator**: Defines an object that encapsulates how a set of objects interact. It promotes loose coupling by keeping objects from referring to each other explicitly.
18. **Memento**: Without violating encapsulation, captures and externalizes an object’s internal state, allowing the object to be restored to this state later.
19. **Observer**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
20. **State**: Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.
21. **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the algorithm vary independently from the clients that use it.
22. **Template Method**: Defines the skeleton of an algorithm in an operation, deferring some steps to subclasses.
23. **Visitor**: Represents an operation to be performed on the elements of an object structure. It lets you define a new operation without changing the classes of the elements on which it operates.

These design patterns are well-established solutions to common software design problems and are widely used in software engineering to improve code flexibility, scalability, and maintainability.



-------------------------------------------------------------------------

## Singleton Design Pattern

The Singleton design pattern is a creational pattern that ensures a class has only one instance and provides a global point of access to that instance. This pattern is useful when exactly one object is needed to coordinate actions across the system.

### When to Use Singleton

You should consider using the Singleton pattern in situations where:

1. **Controlled Access to a Single Instance**: You need to control access to some shared resource (like a configuration object or a logger) and ensure that only one instance of that resource exists.

2. **Global State Management**: You need a single object to manage a global state for the application.

3. **Resource Sharing**: When multiple objects or components need to share a single instance of a class to save resources or enforce consistency.

4. **Preventing Duplication**: You want to prevent the creation of multiple instances of a class that could lead to issues with resource management or logic errors.

### Singleton Pattern Implementation in Java

Here's an example of how to implement the Singleton pattern in Java:

```java
public class Singleton {
    // Static variable to hold the single instance of the class
    private static Singleton instance;

    // Private constructor to prevent instantiation from other classes
    private Singleton() {}

    // Public method to provide access to the instance
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }

    // Example method to demonstrate functionality
    public void showMessage() {
        System.out.println("Hello, this is a Singleton pattern example!");
    }
}
```

### Explanation

1. **Private Constructor**: The constructor of the Singleton class is made private to prevent instantiation from outside the class.

2. **Static Instance**: A static variable `instance` holds the single instance of the class.

3. **Public Method for Access**: The `getInstance()` method provides a global access point to get the instance of the Singleton class. It includes double-checked locking to ensure thread safety while creating the instance.

4. **Lazy Initialization**: The instance is created only when it is needed (lazy initialization), which can be useful for resource management.

### Example Usage

Here is an example of how to use the Singleton class:

```java
public class SingletonDemo {
    public static void main(String[] args) {
        // Get the single instance of the Singleton class
        Singleton singleton = Singleton.getInstance();

        // Use the instance
        singleton.showMessage();
    }
}
```

In this example, the `Singleton` class ensures that only one instance of the class is created. The `getInstance()` method provides a way to access that single instance, and the `showMessage()` method is used to demonstrate the Singleton's functionality.

### Considerations

- **Thread Safety**: The double-checked locking mechanism in the `getInstance()` method ensures thread safety and avoids unnecessary synchronization once the instance is initialized.

- **Performance**: Singleton can improve performance by avoiding repeated creation of objects and ensuring shared access to a common instance.

- **Testing**: Singleton can make testing difficult due to its global state. Dependency injection is often used to manage Singleton dependencies in unit tests.

Overall, the Singleton pattern is a useful tool when you need to ensure that a class has only one instance, especially in situations requiring centralized control or access to a shared resource.


--------------------------------------------------------------------------------

## Factory Method Design Pattern

The Factory Method design pattern is a creational pattern that defines an interface for creating objects but allows subclasses to alter the type of objects that will be created. This pattern promotes loose coupling by reducing the dependency of the code on specific classes.

### When to Use Factory Method

The Factory Method pattern is useful in situations where:

1. **Decoupling Object Creation**: You want to decouple the creation of objects from their implementation so that the code can depend on an interface rather than a concrete class.

2. **Object Creation Complexity**: When the process of creating an object is complex or involves multiple steps, a factory method can simplify the object creation process.

3. **Dynamic Object Creation**: When objects need to be created at runtime based on specific conditions or input parameters.

4. **Extensibility**: When you anticipate that new types of objects may be added to your system and want to make it easy to introduce new classes without changing existing code.

### Factory Method Pattern Implementation in Java

Here's an example of how to implement the Factory Method pattern in Java:

```java
// Step 1: Define a Product interface
interface Product {
    void use();
}

// Step 2: Implement concrete products
class ConcreteProductA implements Product {
    @Override
    public void use() {
        System.out.println("Using Concrete Product A");
    }
}

class ConcreteProductB implements Product {
    @Override
    public void use() {
        System.out.println("Using Concrete Product B");
    }
}

// Step 3: Create an abstract Creator class
abstract class Creator {
    // Factory method to create products
    public abstract Product createProduct();

    // Other methods that use the product
    public void someOperation() {
        Product product = createProduct();
        product.use();
    }
}

// Step 4: Implement concrete creators
class ConcreteCreatorA extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProductA();
    }
}

class ConcreteCreatorB extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProductB();
    }
}
```

### Explanation

1. **Product Interface**: The `Product` interface defines the type of objects that the factory method will create. It specifies a common interface for all products.

2. **Concrete Products**: `ConcreteProductA` and `ConcreteProductB` are implementations of the `Product` interface. They represent the actual objects that the factory method will create.

3. **Creator Class**: The `Creator` abstract class declares the factory method `createProduct()`, which subclasses must implement. It also includes a method `someOperation()` that uses the created product.

4. **Concrete Creators**: `ConcreteCreatorA` and `ConcreteCreatorB` implement the factory method to create specific product instances. Each concrete creator is responsible for creating one specific type of product.

### Example Usage

Here's how you can use the Factory Method pattern:

```java
public class FactoryMethodDemo {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        Creator creatorB = new ConcreteCreatorB();

        // Create and use products
        creatorA.someOperation(); // Output: Using Concrete Product A
        creatorB.someOperation(); // Output: Using Concrete Product B
    }
}
```

### Considerations

- **Flexibility**: The Factory Method pattern allows adding new products without changing existing code, making it easy to extend.

- **Single Responsibility Principle**: This pattern separates the responsibility of object creation into different classes.

- **Interface-Based Programming**: Clients depend on interfaces rather than concrete classes, promoting loose coupling.

- **Complexity**: While adding flexibility, the Factory Method pattern can introduce additional complexity, especially if there are many product variations.

The Factory Method pattern is an excellent choice when you need flexibility in the creation of objects and want to decouple the instantiation process from the use of those objects. It is widely used in frameworks and libraries to allow users to customize the creation of components.