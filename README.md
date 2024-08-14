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


-------------------------------------------------------------------------------------------

## Abstract Factory

The Abstract Factory design pattern is a creational pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. This pattern is particularly useful when a system needs to be independent of how its objects are created, composed, and represented.

### When to Use Abstract Factory

The Abstract Factory pattern is ideal in the following situations:

1. **Families of Related Products**: When you need to create families of related or dependent objects that must be used together.

2. **Consistency Across Products**: When you want to ensure that products are used consistently across the system.

3. **Product Variations**: When the system needs to be configured with one of multiple families of products, and you want to avoid hardcoding specific classes.

4. **Decoupling Code from Concrete Classes**: When you want to decouple your code from the specifics of the product classes to make it more flexible and extensible.

### Abstract Factory Pattern Implementation in Java

Here's an example of how to implement the Abstract Factory pattern in Java:

```java
// Step 1: Define product interfaces
interface Button {
    void paint();
}

interface Checkbox {
    void paint();
}

// Step 2: Implement concrete products for each variant
class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in Windows style.");
    }
}

class MacOSButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in MacOS style.");
    }
}

class WindowsCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in Windows style.");
    }
}

class MacOSCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in MacOS style.");
    }
}

// Step 3: Define an abstract factory interface
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Step 4: Implement concrete factories for each product family
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}
```

### Explanation

1. **Product Interfaces**: Interfaces such as `Button` and `Checkbox` define the abstract products that the factory creates. These interfaces ensure that products from different families adhere to the same structure.

2. **Concrete Products**: Classes like `WindowsButton`, `MacOSButton`, `WindowsCheckbox`, and `MacOSCheckbox` implement the product interfaces. These are the concrete implementations of the products, each corresponding to a particular variant (e.g., Windows or MacOS).

3. **Abstract Factory Interface**: The `GUIFactory` interface declares the methods for creating each type of product (buttons and checkboxes).

4. **Concrete Factories**: `WindowsFactory` and `MacOSFactory` implement the `GUIFactory` interface and create products for their respective platforms.

### Example Usage

Here's how you can use the Abstract Factory pattern:

```java
public class AbstractFactoryDemo {
    private static Application configureApplication() {
        Application app;
        GUIFactory factory;

        // Assume we determine the operating system at runtime
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("mac")) {
            factory = new MacOSFactory();
        } else {
            factory = new WindowsFactory();
        }

        app = new Application(factory);
        return app;
    }

    public static void main(String[] args) {
        Application app = configureApplication();
        app.paint();
    }
}

class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(GUIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }

    public void paint() {
        button.paint();
        checkbox.paint();
    }
}
```

### Explanation

- **Application Configuration**: The `configureApplication()` method determines which factory to use based on the operating system. It then creates an `Application` instance using the chosen factory.

- **Decoupling and Flexibility**: The application code is decoupled from concrete product implementations. You can easily switch between product families (Windows, MacOS) without changing the application's logic.

- **Consistent Usage**: The factory ensures that all products created belong to the same family, maintaining consistency across the system.

### Considerations

- **Scalability**: The Abstract Factory pattern makes it easy to add new product families without modifying existing code, making the system more scalable and extensible.

- **Complexity**: This pattern can introduce additional complexity, especially if there are many product families or types.

- **Design Overhead**: Implementing this pattern requires creating multiple interfaces and classes, which can increase the design overhead.

Overall, the Abstract Factory pattern is a powerful tool for managing complex systems where multiple families of related objects need to be created and used consistently, promoting flexibility and scalability.

------------------------------------------------------------------------------------------

## Builder Design Pattern

The Builder design pattern is a creational pattern used to construct complex objects step by step. It separates the construction of a complex object from its representation, allowing the same construction process to create different representations. The Builder pattern is particularly useful when an object requires numerous parameters or when complex initialization is needed.

### When to Use Builder

The Builder pattern is ideal in the following situations:

1. **Complex Object Construction**: When you have a complex object with many fields, especially when many of them are optional.

2. **Immutability**: When you want to create immutable objects, as it allows setting all properties at once before finalizing the object.

3. **Readable Code**: When you want to improve code readability and reduce the chance of errors by using a clear and fluent interface for object construction.

4. **Object Variations**: When the object can have different representations or configurations, and you want to separate the construction logic from the representation.

### Builder Pattern Implementation in Java

Here's an example of how to implement the Builder pattern in Java:

```java
// Step 1: Define the complex object
public class Car {
    // Required parameters
    private final String engine;
    private final String transmission;

    // Optional parameters
    private final boolean airConditioning;
    private final boolean gps;
    private final boolean sunroof;

    // Private constructor
    private Car(CarBuilder builder) {
        this.engine = builder.engine;
        this.transmission = builder.transmission;
        this.airConditioning = builder.airConditioning;
        this.gps = builder.gps;
        this.sunroof = builder.sunroof;
    }

    // Getters
    public String getEngine() {
        return engine;
    }

    public String getTransmission() {
        return transmission;
    }

    public boolean hasAirConditioning() {
        return airConditioning;
    }

    public boolean hasGps() {
        return gps;
    }

    public boolean hasSunroof() {
        return sunroof;
    }

    @Override
    public String toString() {
        return "Car{" +
                "engine='" + engine + '\'' +
                ", transmission='" + transmission + '\'' +
                ", airConditioning=" + airConditioning +
                ", gps=" + gps +
                ", sunroof=" + sunroof +
                '}';
    }

    // Step 2: Create a static nested Builder class
    public static class CarBuilder {
        private final String engine;
        private final String transmission;
        private boolean airConditioning;
        private boolean gps;
        private boolean sunroof;

        // Constructor with required parameters
        public CarBuilder(String engine, String transmission) {
            this.engine = engine;
            this.transmission = transmission;
        }

        // Methods to set optional parameters
        public CarBuilder setAirConditioning(boolean airConditioning) {
            this.airConditioning = airConditioning;
            return this;
        }

        public CarBuilder setGps(boolean gps) {
            this.gps = gps;
            return this;
        }

        public CarBuilder setSunroof(boolean sunroof) {
            this.sunroof = sunroof;
            return this;
        }

        // Method to build the final product
        public Car build() {
            return new Car(this);
        }
    }
}
```

### Explanation

1. **Complex Object**: The `Car` class is the complex object being constructed. It has both required (`engine`, `transmission`) and optional (`airConditioning`, `gps`, `sunroof`) parameters.

2. **Private Constructor**: The constructor for `Car` is private and accepts a `CarBuilder` object, which contains all the necessary parameters to construct a `Car` instance.

3. **Nested Builder Class**: The `CarBuilder` class is a static nested class that constructs the `Car` object. It has methods for setting optional parameters and a `build()` method to create the `Car` instance.

4. **Fluent Interface**: The builder methods return `this`, allowing method chaining for a fluent interface.

### Example Usage

Here's how you can use the Builder pattern to construct a `Car` object:

```java
public class BuilderPatternDemo {
    public static void main(String[] args) {
        // Create a Car using the Builder pattern
        Car car = new Car.CarBuilder("V6", "Automatic")
                .setAirConditioning(true)
                .setGps(true)
                .setSunroof(false)
                .build();

        System.out.println(car);
    }
}
```

### Explanation

- **Building the Object**: The `CarBuilder` is used to set the required parameters (`engine`, `transmission`) and optional parameters (`airConditioning`, `gps`, `sunroof`).

- **Finalizing the Object**: The `build()` method is called to create the `Car` instance.

### Considerations

- **Immutability**: The Builder pattern is often used to create immutable objects, where all properties are set at the time of object creation.

- **Readability**: The pattern enhances code readability and makes the object construction process more intuitive.

- **Complexity**: It adds complexity by introducing additional classes, but this is often justified by the clarity and flexibility it provides.

The Builder pattern is a powerful tool for constructing complex objects with numerous optional parameters. It improves code maintainability, readability, and ensures that objects are constructed in a controlled manner.

----------------------------------------------------------------------------------

## Prototype Design Pattern

The Prototype design pattern is a creational pattern that allows objects to be cloned to produce new objects. Instead of creating new instances from scratch, the Prototype pattern provides a way to copy or clone existing objects, thus enhancing performance and simplifying object creation when the cost of creating a new instance is more expensive than copying an existing one.

### When to Use Prototype

The Prototype pattern is useful in the following situations:

1. **Expensive Object Creation**: When creating an instance of a class is resource-intensive or time-consuming.

2. **Avoiding Subclassing**: When you want to avoid a proliferation of subclasses in a factory hierarchy.

3. **Dynamic Object Creation**: When the exact type of the objects to be created is determined at runtime.

4. **Object Caching**: When you need to cache and reuse objects to improve performance.

### Prototype Pattern Implementation in Java

Here's an example of how to implement the Prototype pattern in Java:

```java
import java.util.HashMap;
import java.util.Map;

// Step 1: Create a Prototype interface
interface Prototype {
    Prototype clone();
}

// Step 2: Create concrete classes implementing the Prototype interface
class Rectangle implements Prototype {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    @Override
    public Rectangle clone() {
        return new Rectangle(width, height);
    }

    @Override
    public String toString() {
        return "Rectangle{" +
                "width=" + width +
                ", height=" + height +
                '}';
    }
}

class Circle implements Prototype {
    private int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    public int getRadius() {
        return radius;
    }

    @Override
    public Circle clone() {
        return new Circle(radius);
    }

    @Override
    public String toString() {
        return "Circle{" +
                "radius=" + radius +
                '}';
    }
}

// Step 3: Create a Prototype Registry
class PrototypeRegistry {
    private Map<String, Prototype> prototypes = new HashMap<>();

    public void addPrototype(String key, Prototype prototype) {
        prototypes.put(key, prototype);
    }

    public Prototype getPrototype(String key) {
        return prototypes.get(key).clone();
    }
}
```

### Explanation

1. **Prototype Interface**: The `Prototype` interface declares a `clone()` method for cloning objects.

2. **Concrete Prototypes**: Classes like `Rectangle` and `Circle` implement the `Prototype` interface and define their cloning logic in the `clone()` method.

3. **Prototype Registry**: The `PrototypeRegistry` class holds a collection of prototype objects. It allows clients to clone objects using the `getPrototype()` method, which returns a copy of the registered prototype.

### Example Usage

Here's how you can use the Prototype pattern:

```java
public class PrototypePatternDemo {
    public static void main(String[] args) {
        // Create a Prototype Registry
        PrototypeRegistry registry = new PrototypeRegistry();

        // Add prototypes to the registry
        registry.addPrototype("Large Rectangle", new Rectangle(100, 50));
        registry.addPrototype("Small Circle", new Circle(10));

        // Clone objects from the registry
        Rectangle clonedRectangle = (Rectangle) registry.getPrototype("Large Rectangle");
        Circle clonedCircle = (Circle) registry.getPrototype("Small Circle");

        System.out.println(clonedRectangle); // Output: Rectangle{width=100, height=50}
        System.out.println(clonedCircle);    // Output: Circle{radius=10}
    }
}
```

### Explanation

- **Cloning Objects**: The `PrototypeRegistry` is used to store prototypes and retrieve clones of these prototypes. Clients can get copies of objects without knowing the details of their creation.

- **Decoupling**: The Prototype pattern decouples the client code from the specifics of the object creation process.

### Considerations

- **Cloning Complexity**: The Prototype pattern simplifies object creation but can be complex to implement if objects have complex state or deep copy requirements.

- **Performance**: Cloning objects can improve performance when creating new instances is expensive.

- **Shallow vs. Deep Copy**: It's essential to decide whether to perform shallow or deep copying, depending on the use case. Deep copying may require handling mutable objects or collections within the prototype.

The Prototype pattern is particularly effective when you need to create many similar objects, optimize resource usage, or simplify complex object creation processes. It provides flexibility and decouples the client code from concrete classes, allowing for dynamic object creation and reusability.

-----------------------------------------------------------------------------------

## Adapter Design Pattern

The Adapter design pattern is a structural pattern that allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces by wrapping an existing class with a new interface. The Adapter pattern is particularly useful when you need to integrate a class into your application that doesn’t match the existing interfaces.

### When to Use Adapter

The Adapter pattern is useful in the following situations:

1. **Incompatible Interfaces**: When you want to use an existing class but its interface does not match the one you need.

2. **Integration with Legacy Code**: When you need to integrate with legacy code or third-party libraries with incompatible interfaces.

3. **Multiple Interface Implementations**: When you want to reuse an existing class in a different context with a different interface.

4. **Target Interface Adherence**: When you want to ensure that your class conforms to a particular interface without altering the original class.

### Adapter Pattern Implementation in Java

Here's an example of how to implement the Adapter pattern in Java:

```java
// Step 1: Define the target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Step 2: Create an existing class with an incompatible interface
class AdvancedMediaPlayer {
    void playVlc(String fileName) {
        System.out.println("Playing VLC file. Name: " + fileName);
    }

    void playMp4(String fileName) {
        System.out.println("Playing MP4 file. Name: " + fileName);
    }
}

// Step 3: Create the adapter class implementing the target interface
class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedMusicPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer = new AdvancedMediaPlayer();
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMusicPlayer = new AdvancedMediaPlayer();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer.playVlc(fileName);
        } else if (audioType.equalsIgnoreCase("mp4")) {
            advancedMusicPlayer.playMp4(fileName);
        }
    }
}

// Step 4: Create a class using the adapter
class AudioPlayer implements MediaPlayer {
    private MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        // Built-in support for mp3 music
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file. Name: " + fileName);
        }
        // MediaAdapter is providing support for other formats
        else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType + " format not supported.");
        }
    }
}
```

### Explanation

1. **Target Interface**: `MediaPlayer` is the interface that the client expects to interact with. It has a `play()` method to handle audio playback.

2. **Existing Class**: `AdvancedMediaPlayer` is an existing class with an incompatible interface. It has methods `playVlc()` and `playMp4()` for different media formats.

3. **Adapter Class**: `MediaAdapter` implements the target interface (`MediaPlayer`) and uses an instance of `AdvancedMediaPlayer` to handle specific media formats. The adapter translates the calls from the `MediaPlayer` interface to the appropriate methods in `AdvancedMediaPlayer`.

4. **Client Class**: `AudioPlayer` is a client class that uses the `MediaAdapter` to play various audio formats.

### Example Usage

Here's how you can use the Adapter pattern:

```java
public class AdapterPatternDemo {
    public static void main(String[] args) {
        AudioPlayer audioPlayer = new AudioPlayer();

        audioPlayer.play("mp3", "song.mp3");
        audioPlayer.play("mp4", "video.mp4");
        audioPlayer.play("vlc", "movie.vlc");
        audioPlayer.play("avi", "myMovie.avi");
    }
}
```

### Explanation

- **Playing Audio**: The `AudioPlayer` class uses the `MediaAdapter` to play media files of different formats. If the format is not supported directly, it delegates the task to the adapter.

- **Incompatible Interfaces**: The Adapter pattern allows the `AudioPlayer` to work with different media formats without modifying the `AdvancedMediaPlayer` class.

### Considerations

- **Single Responsibility**: The Adapter pattern adheres to the Single Responsibility Principle by separating the interface adaptation logic into its own class.

- **Interface Mismatch**: It resolves interface mismatches by translating calls between the target interface and the existing class.

- **Complexity**: Introducing an adapter class can add complexity to the codebase, especially if there are many methods to adapt.

- **Performance**: There may be a slight performance overhead due to the additional layer of abstraction, but this is generally negligible.

The Adapter pattern is an effective way to enable incompatible interfaces to work together, allowing you to reuse existing code without modification. It is widely used in scenarios where you need to integrate with third-party libraries or legacy systems with different interfaces.

-----------------------------------------------------------------------------------

## The bridge Design Pattern

The Bridge design pattern is a structural pattern that separates an abstraction from its implementation, allowing both to evolve independently. This pattern is used to bridge the gap between an abstraction and its implementation, providing a way to vary both independently without affecting the other.

### When to Use Bridge

The Bridge pattern is useful in the following scenarios:

1. **Multiple Variants**: When you have multiple abstractions that need to be implemented in different ways, and you want to avoid a proliferation of subclasses.

2. **Independent Evolution**: When you want to allow both the abstraction and its implementation to evolve independently.

3. **Complex Hierarchies**: When the combination of different abstractions and implementations creates a complex hierarchy.

4. **Decoupling**: When you want to decouple the abstraction from its implementation so that changes to one do not affect the other.

### Bridge Pattern Implementation in Java

Here's an example of how to implement the Bridge pattern in Java:

```java
// Step 1: Define the Implementor interface
interface DrawingAPI {
    void drawCircle(double x, double y, double radius);
}

// Step 2: Create concrete Implementors
class DrawingAPI1 implements DrawingAPI {
    @Override
    public void drawCircle(double x, double y, double radius) {
        System.out.println("Drawing circle using API1 at (" + x + ", " + y + ") with radius " + radius);
    }
}

class DrawingAPI2 implements DrawingAPI {
    @Override
    public void drawCircle(double x, double y, double radius) {
        System.out.println("Drawing circle using API2 at (" + x + ", " + y + ") with radius " + radius);
    }
}

// Step 3: Define the Abstraction
abstract class Shape {
    protected DrawingAPI drawingAPI;

    protected Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw();
    public abstract void resizeByPercentage(double pct);
}

// Step 4: Create refined abstractions
class Circle extends Shape {
    private double x, y, radius;

    public Circle(double x, double y, double radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    @Override
    public void draw() {
        drawingAPI.drawCircle(x, y, radius);
    }

    @Override
    public void resizeByPercentage(double pct) {
        radius *= (1 + pct / 100);
    }
}
```

### Explanation

1. **Implementor Interface**: `DrawingAPI` is the interface for the implementation classes. It declares the methods that concrete implementations must provide.

2. **Concrete Implementors**: `DrawingAPI1` and `DrawingAPI2` are concrete implementations of the `DrawingAPI` interface, providing different ways to draw circles.

3. **Abstraction**: `Shape` is an abstract class that uses an instance of `DrawingAPI`. It provides an abstract method `draw()` that subclasses must implement.

4. **Refined Abstractions**: `Circle` is a concrete subclass of `Shape` that implements the `draw()` method using the provided `DrawingAPI`. It also provides a method to resize the circle.

### Example Usage

Here's how you can use the Bridge pattern:

```java
public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape circle1 = new Circle(5, 10, 15, new DrawingAPI1());
        Shape circle2 = new Circle(20, 30, 25, new DrawingAPI2());

        circle1.draw();
        circle2.draw();

        circle1.resizeByPercentage(10);
        circle1.draw();
    }
}
```

### Explanation

- **Drawing Different Circles**: The `Circle` objects use different `DrawingAPI` implementations to draw circles. `circle1` uses `DrawingAPI1`, while `circle2` uses `DrawingAPI2`.

- **Independent Evolution**: The `Circle` class can evolve independently from the `DrawingAPI` implementations. Similarly, the `DrawingAPI` implementations can evolve without affecting the `Circle` class.

### Considerations

- **Flexibility**: The Bridge pattern provides flexibility by decoupling the abstraction and implementation. This allows changes to one without affecting the other.

- **Complexity**: Introducing an additional layer of abstraction can add complexity to the codebase, especially if the number of abstractions and implementations increases.

- **Maintainability**: The pattern improves maintainability by separating concerns and adhering to the Single Responsibility Principle.

The Bridge pattern is an effective way to handle situations where you need to manage multiple variations of an abstraction and its implementation. It promotes flexibility, maintainability, and decoupling, making it easier to evolve and manage complex systems.

---------------------------------------------------------------------------------

## The Composite Design Pattern

The Composite design pattern is a structural pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly. In other words, the Composite pattern allows you to group objects into a tree structure and work with these objects as if they were individual objects.

### When to Use Composite

The Composite pattern is useful in the following scenarios:

1. **Hierarchical Structures**: When you need to represent a tree structure, such as a file system, organizational chart, or graphical user interface.

2. **Uniformity**: When you want to treat individual objects and compositions of objects uniformly, allowing clients to interact with both in the same way.

3. **Recursive Structures**: When dealing with recursive structures where a component can be made up of subcomponents of the same type.

4. **Complex Objects**: When you want to build complex objects by combining simpler objects.

### Composite Pattern Implementation in Java

Here's an example of how to implement the Composite pattern in Java:

```java
// Step 1: Define the Component interface
interface Employee {
    void showEmployeeDetails();
}

// Step 2: Create Leaf classes that implement the Component interface
class Developer implements Employee {
    private String name;
    private long empId;
    private String position;

    public Developer(long empId, String name, String position) {
        this.empId = empId;
        this.name = name;
        this.position = position;
    }

    @Override
    public void showEmployeeDetails() {
        System.out.println(empId + " " + name + " (" + position + ")");
    }
}

class Manager implements Employee {
    private String name;
    private long empId;
    private String position;

    public Manager(long empId, String name, String position) {
        this.empId = empId;
        this.name = name;
        this.position = position;
    }

    @Override
    public void showEmployeeDetails() {
        System.out.println(empId + " " + name + " (" + position + ")");
    }
}

// Step 3: Create the Composite class that implements the Component interface
class CompanyDirectory implements Employee {
    private List<Employee> employeeList = new ArrayList<>();

    @Override
    public void showEmployeeDetails() {
        for (Employee emp : employeeList) {
            emp.showEmployeeDetails();
        }
    }

    public void addEmployee(Employee emp) {
        employeeList.add(emp);
    }

    public void removeEmployee(Employee emp) {
        employeeList.remove(emp);
    }
}
```

### Explanation

1. **Component Interface**: `Employee` is the component interface that defines the operations that can be performed on both leaf nodes and composites. In this case, it has the method `showEmployeeDetails()`.

2. **Leaf Classes**: `Developer` and `Manager` are leaf classes that implement the `Employee` interface. These classes represent individual objects in the composition and provide their own implementation of `showEmployeeDetails()`.

3. **Composite Class**: `CompanyDirectory` is the composite class that implements the `Employee` interface. It contains a list of `Employee` objects (which can be either leaf nodes or other composites) and implements `showEmployeeDetails()` by iterating over this list. It also provides methods to add and remove employees from the directory.

### Example Usage

Here's how you can use the Composite pattern:

```java
public class CompositePatternDemo {
    public static void main(String[] args) {
        Employee dev1 = new Developer(100, "John Doe", "Pro Developer");
        Employee dev2 = new Developer(101, "Jane Doe", "Developer");

        Employee manager1 = new Manager(200, "Mike Smith", "Manager");

        CompanyDirectory engineeringDirectory = new CompanyDirectory();
        engineeringDirectory.addEmployee(dev1);
        engineeringDirectory.addEmployee(dev2);

        CompanyDirectory managerDirectory = new CompanyDirectory();
        managerDirectory.addEmployee(manager1);

        CompanyDirectory companyDirectory = new CompanyDirectory();
        companyDirectory.addEmployee(engineeringDirectory);
        companyDirectory.addEmployee(managerDirectory);

        companyDirectory.showEmployeeDetails();
    }
}
```

### Explanation

- **Creating Objects**: In this example, individual `Developer` and `Manager` objects are created, representing the leaf nodes.

- **Creating Composites**: `CompanyDirectory` objects are created to represent groups of employees. The engineering directory contains developers, and the manager directory contains managers.

- **Composite of Composites**: The main `companyDirectory` is a composite that contains both the engineering and manager directories, effectively creating a tree structure.

- **Uniform Operation**: When you call `showEmployeeDetails()` on `companyDirectory`, it recursively traverses the entire tree and displays the details of all employees, whether they are individual objects or groups of objects.

### Considerations

- **Simplicity**: The Composite pattern simplifies client code by allowing uniform treatment of individual objects and compositions of objects.

- **Flexibility**: It provides flexibility in representing complex structures as simple trees, making it easier to add new components or composites.

- **Overhead**: The pattern may introduce overhead if the structure is not truly hierarchical or if the uniform treatment of objects is not necessary.

- **Complexity**: The pattern can lead to overly generalized code if not used carefully, especially in systems with deep hierarchies.

The Composite pattern is ideal for scenarios where you need to work with tree-like structures and want to treat individual objects and compositions uniformly. It simplifies the management of complex structures and is widely used in file systems, GUI frameworks, and other applications involving hierarchical data.

----------------------------------------------------------------------------------

## Decorator Design Pattern

The Decorator design pattern is a structural pattern that allows you to add new behaviors to objects dynamically without altering their structure. It provides a flexible alternative to subclassing for extending functionality, making it possible to enhance or modify an object’s behavior at runtime by wrapping it with one or more decorator objects.

### When to Use the Decorator Pattern

1. **Adding Functionality Dynamically**: When you need to add responsibilities to individual objects without affecting other objects of the same class.
   
2. **Combining Behaviors**: When you want to combine multiple behaviors or responsibilities in an object dynamically, rather than statically through inheritance.

3. **Avoiding Subclass Explosion**: When extending functionality through inheritance would result in an impractical number of subclasses.

4. **Open/Closed Principle**: When you want to adhere to the open/closed principle, allowing classes to be open for extension but closed for modification.

### Decorator Pattern Implementation in Java

Here’s how to implement the Decorator pattern in Java:

```java
// Step 1: Define the Component interface
interface Coffee {
    String getDescription();
    double getCost();
}

// Step 2: Create Concrete Components
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple Coffee";
    }

    @Override
    public double getCost() {
        return 5.0;
    }
}

// Step 3: Create the Decorator class that implements the Component interface
abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// Step 4: Create Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Milk";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 1.5;
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return decoratedCoffee.getDescription() + ", Sugar";
    }

    @Override
    public double getCost() {
        return decoratedCoffee.getCost() + 0.5;
    }
}
```

### Explanation

1. **Component Interface**: `Coffee` is the component interface that defines the basic operations, such as `getDescription()` and `getCost()`.

2. **Concrete Component**: `SimpleCoffee` is a concrete class that implements the `Coffee` interface. It represents the basic version of the object that can be decorated.

3. **Decorator Class**: `CoffeeDecorator` is an abstract class that implements the `Coffee` interface. It holds a reference to a `Coffee` object and delegates the methods to the wrapped object. This class serves as the base for concrete decorators.

4. **Concrete Decorators**: `MilkDecorator` and `SugarDecorator` are concrete decorators that extend `CoffeeDecorator`. They add their own behavior by enhancing the methods from the `Coffee` interface. For example, `MilkDecorator` adds the description and cost of milk to the base coffee.

### Example Usage

Here’s how you can use the Decorator pattern:

```java
public class DecoratorPatternDemo {
    public static void main(String[] args) {
        Coffee simpleCoffee = new SimpleCoffee();
        System.out.println(simpleCoffee.getDescription() + " $" + simpleCoffee.getCost());

        Coffee milkCoffee = new MilkDecorator(simpleCoffee);
        System.out.println(milkCoffee.getDescription() + " $" + milkCoffee.getCost());

        Coffee milkSugarCoffee = new SugarDecorator(milkCoffee);
        System.out.println(milkSugarCoffee.getDescription() + " $" + milkSugarCoffee.getCost());
    }
}
```

### Explanation

- **Simple Coffee**: Initially, a `SimpleCoffee` object is created, which represents the basic coffee with a description and cost.

- **Adding Milk**: A `MilkDecorator` is created to wrap the `SimpleCoffee` object, effectively adding the description and cost of milk.

- **Adding Sugar**: Finally, a `SugarDecorator` is created to wrap the `MilkDecorator` object, adding the description and cost of sugar.

### Output

```
Simple Coffee $5.0
Simple Coffee, Milk $6.5
Simple Coffee, Milk, Sugar $7.0
```

### Considerations

- **Flexibility**: The Decorator pattern provides great flexibility in extending an object’s functionality. You can combine decorators in different ways to achieve various effects.

- **Transparency**: Since decorators implement the same interface as the original object, they can be used transparently without the client needing to know that additional behavior has been added.

- **Complexity**: The pattern can introduce complexity due to the large number of small classes that might be created for each decorator.

- **Performance**: Each decorator adds a level of indirection and can lead to increased memory usage or slower performance if overused.

The Decorator pattern is a powerful tool when you need to dynamically add or change the behavior of objects at runtime. It is particularly useful in scenarios where you need to enhance the functionality of objects in a flexible and maintainable way without altering the underlying class structure.

---------------------------------------------------------------------------------

## The Facade Design Pattern

The **Facade** design pattern is a structural pattern that provides a simplified interface to a complex system, library, or framework. It hides the complexities of the system and provides a single entry point through which clients can interact with the system. The goal is to make the system easier to use by reducing the number of methods a client has to deal with and to make the interface more intuitive.

### When to Use the Facade Pattern

1. **Simplifying Complex Systems**: When you have a complex system with multiple subsystems and you want to provide a simpler interface for common use cases.
   
2. **Decoupling**: When you want to decouple clients from the complex system by hiding its implementation details behind a simplified interface.

3. **Legacy Systems**: When integrating with a legacy system or a third-party library that has a complex or inconvenient API, and you want to wrap it in a simpler interface.

4. **Modularizing Code**: When you want to organize your code into layers and provide a simple API for higher-level modules to interact with the lower-level subsystems.

### Facade Pattern Implementation in Java

Here’s an example of how to implement the Facade pattern in Java:

```java
// Step 1: Subsystem classes (complex internal operations)
class CPU {
    public void freeze() {
        System.out.println("Freezing CPU.");
    }

    public void jump(long position) {
        System.out.println("Jumping to position " + position);
    }

    public void execute() {
        System.out.println("Executing instructions.");
    }
}

class Memory {
    public void load(long position, String data) {
        System.out.println("Loading data '" + data + "' into position " + position);
    }
}

class HardDrive {
    public String read(long lba, int size) {
        return "Some data from sector " + lba;
    }
}

// Step 2: Facade class (provides a simplified interface)
class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;

    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }

    public void start() {
        cpu.freeze();
        memory.load(100, hardDrive.read(200, 1024));
        cpu.jump(100);
        cpu.execute();
    }
}
```

### Explanation

1. **Subsystem Classes**: `CPU`, `Memory`, and `HardDrive` are individual classes that represent the internal subsystems of the computer. Each has its own complex set of operations.

2. **Facade Class**: `ComputerFacade` is the facade that hides the complexity of these subsystems by providing a simple `start()` method. This method internally calls the necessary operations on the CPU, memory, and hard drive to start the computer.

### Example Usage

Here’s how you can use the Facade pattern:

```java
public class FacadePatternDemo {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.start();
    }
}
```

### Output

```
Freezing CPU.
Loading data 'Some data from sector 200' into position 100
Jumping to position 100
Executing instructions.
```

### Explanation

- The `ComputerFacade` hides the complexities of starting a computer. Instead of manually interacting with the `CPU`, `Memory`, and `HardDrive` classes, the client simply calls the `start()` method of `ComputerFacade`, which handles the internal details.

### Benefits of the Facade Pattern

1. **Simplifies Usage**: The Facade pattern provides a simple interface to a complex system, reducing the number of objects the client has to interact with.

2. **Encapsulates Complexity**: It hides the complexity of the subsystems, making the system easier to use and maintain.

3. **Decouples the Client**: The client is decoupled from the details of the subsystems. This makes it easier to change or refactor the subsystems without affecting the client.

4. **Improves Readability**: By providing a higher-level API, the Facade pattern makes the code more readable and intuitive, especially when dealing with complex systems.

5. **Flexible and Extensible**: The Facade pattern can be used to provide different levels of abstraction, depending on the use case. You can add new operations to the facade without changing the underlying subsystems.

### Considerations

- **Not Always Necessary**: If the system is simple and doesn’t have complex subsystems, a facade may add unnecessary complexity. The pattern is most beneficial when you are dealing with large and complicated systems.

- **Tight Coupling with Subsystems**: The Facade pattern can introduce tight coupling between the facade and the subsystems it wraps. If the subsystems change frequently, the facade may require regular updates.

### Real-World Example

A common real-world example of the Facade pattern is using a library like JDBC to interact with a database. Instead of interacting with the low-level details of database connections, queries, and result sets, JDBC provides a simplified API for querying and managing the database.

Another example is a **hotel booking system**:
- The client doesn't need to know how to book a room, how to reserve a car, or how to schedule an airport pickup. They can simply interact with a `BookingFacade` class, which manages all the underlying details.

The **Facade** pattern is an excellent choice when you need to simplify complex interactions, reduce dependencies on low-level details, and provide a unified interface for clients. It is widely used in large-scale systems to provide clear and intuitive APIs for complex operations.

----------------------------------------------------------------------------------

## Flyweight Design Pattern

The **Flyweight** design pattern is a structural pattern used to minimize memory usage and improve performance by sharing as much data as possible between similar objects. It is especially useful when you need to create a large number of objects that share some common data.

Instead of creating multiple objects for the same data, the Flyweight pattern allows you to share objects, reducing the overall memory footprint. This is achieved by separating the object’s state into **intrinsic** (shared) and **extrinsic** (unique) states.

### When to Use the Flyweight Pattern

1. **Large Number of Objects**: When your system needs to handle a large number of objects that would consume a significant amount of memory if instantiated individually.

2. **Shared State**: When many objects share common data or state that can be extracted and shared to reduce memory consumption.

3. **Performance Concerns**: When memory usage or performance is a concern due to the large number of objects created at runtime.

4. **Immutable Objects**: When the objects being shared are immutable (i.e., their state does not change after creation), Flyweight can be very effective.

### Flyweight Pattern Implementation in Java

Here’s an example of the Flyweight pattern using a text editor scenario, where characters are shared to reduce memory usage:

#### Step 1: Flyweight Interface
This interface represents the flyweight objects that will be shared.

```java
// Flyweight Interface
interface CharacterFlyweight {
    void display(int fontSize);
}
```

#### Step 2: Concrete Flyweight Class
This class implements the flyweight interface. Instances of this class represent the shared part (intrinsic state) of the object, such as the character itself.

```java
// Concrete Flyweight
class Character implements CharacterFlyweight {
    private final char symbol; // Intrinsic state (shared)
    
    public Character(char symbol) {
        this.symbol = symbol;
    }

    @Override
    public void display(int fontSize) {
        System.out.println("Displaying character '" + symbol + "' with font size " + fontSize);
    }
}
```

#### Step 3: Flyweight Factory
This class ensures that flyweight objects are reused and shared. It returns either a new or an existing flyweight object based on the character symbol.

```java
// Flyweight Factory
import java.util.HashMap;
import java.util.Map;

class CharacterFactory {
    private Map<Character, CharacterFlyweight> flyweightMap = new HashMap<>();

    public CharacterFlyweight getCharacter(char symbol) {
        CharacterFlyweight flyweight = flyweightMap.get(symbol);
        if (flyweight == null) {
            flyweight = new Character(symbol);
            flyweightMap.put(symbol, flyweight);
        }
        return flyweight;
    }
}
```

#### Step 4: Client Code
The client code uses the `CharacterFactory` to get flyweight objects and interact with them.

```java
public class FlyweightPatternDemo {
    public static void main(String[] args) {
        CharacterFactory factory = new CharacterFactory();

        // Use shared flyweight objects for characters
        CharacterFlyweight c1 = factory.getCharacter('A');
        CharacterFlyweight c2 = factory.getCharacter('B');
        CharacterFlyweight c3 = factory.getCharacter('A');  // Reuse flyweight for 'A'

        // Display characters with different extrinsic state (font size)
        c1.display(12);
        c2.display(14);
        c3.display(16);
    }
}
```

### Explanation

- **Flyweight Interface (`CharacterFlyweight`)**: This interface defines the method `display()` that will be used to render the character with a specific font size.
  
- **Concrete Flyweight (`Character`)**: This class implements the `CharacterFlyweight` interface and stores the intrinsic state (the actual character symbol) that will be shared across instances.

- **Flyweight Factory (`CharacterFactory`)**: This factory class manages flyweight objects. It ensures that only one instance of each unique character is created and reused whenever needed.

- **Client Code**: The client interacts with the `CharacterFactory` to retrieve characters and display them with different font sizes. Even though the character 'A' is displayed multiple times, it is only created once, thanks to the Flyweight pattern.

### Output

```
Displaying character 'A' with font size 12
Displaying character 'B' with font size 14
Displaying character 'A' with font size 16
```

### Key Concepts in the Flyweight Pattern

1. **Intrinsic State**: This is the state that is shared between objects. It is immutable and can be reused by multiple objects. In the example, the character symbol (e.g., 'A', 'B') is intrinsic.

2. **Extrinsic State**: This is the state that is unique to each object and must be passed in at runtime. In the example, the font size is extrinsic and passed to the `display()` method.

3. **Flyweight Factory**: This factory ensures that flyweight objects are shared and reused. It keeps a pool of already-created flyweights and returns existing ones when possible, instead of creating new instances.

### Benefits of the Flyweight Pattern

1. **Reduced Memory Usage**: By sharing objects instead of creating multiple instances, the Flyweight pattern reduces memory consumption significantly.

2. **Increased Performance**: Reducing the number of objects created can improve the performance of the application, especially in memory-constrained environments.

3. **Separation of Concerns**: By separating intrinsic (shared) and extrinsic (unique) states, the pattern helps manage data more effectively.

### Considerations

- **Complexity**: The Flyweight pattern introduces complexity because you need to distinguish between intrinsic and extrinsic states. The client needs to manage the extrinsic state, which can increase complexity.

- **Performance Overhead**: Although the pattern saves memory, it can introduce performance overhead due to object management and the need to look up shared instances.

- **Use with Immutable Objects**: The Flyweight pattern is more suitable for immutable objects where the intrinsic state does not change after creation.

### Real-World Example

A real-world example of the Flyweight pattern can be seen in **GUI frameworks** (like Java's Swing). In such systems, graphical elements like buttons, labels, or text components can be reused and shared, reducing memory consumption.

Another example is a **game** where objects like trees, rocks, or characters can share intrinsic data (such as texture, color, or type) while keeping their positions or sizes unique.

The Flyweight pattern is particularly useful when dealing with systems that require a large number of similar objects, like text rendering engines, particle systems in games, or graphical object management systems. It optimizes memory usage and helps in managing a large number of instances effectively.

------------------------------------------------------------------------------------

## Proxy Design Pattern

The **Proxy** design pattern is a structural pattern that provides a placeholder or surrogate for another object to control access to it. A proxy acts as an intermediary between the client and the real object, offering additional functionalities like lazy initialization, access control, logging, or even caching, without changing the real object’s interface.

### When to Use the Proxy Pattern

1. **Lazy Initialization**: When you want to delay the creation or initialization of a resource until it’s actually needed. For example, in a complex or resource-heavy system (like opening a file or establishing a network connection).

2. **Access Control**: When you need to control access to an object, such as in authentication or permission systems.

3. **Logging or Auditing**: When you want to track or log operations performed on an object.

4. **Remote Proxy**: When an object resides in a different address space or server, and the proxy provides access to it remotely (common in distributed systems).

5. **Caching**: When you want to cache the results of expensive operations to avoid redundant computations.

### Types of Proxies

1. **Virtual Proxy**: Controls access to a resource that is expensive to create, like lazy initialization.
   
2. **Protection Proxy**: Controls access to a resource, based on user permissions or authentication.
   
3. **Remote Proxy**: Manages interactions between a client and an object in a different location, such as over a network.

4. **Smart Proxy**: Adds additional functionality (like logging, reference counting) to manage the behavior of the real object.

### Proxy Pattern Implementation in Java

Let’s look at an example of a **virtual proxy** that delays the loading of an image file until it’s actually requested.

#### Step 1: Subject Interface
This defines the common interface between the real object and the proxy. Both will implement this interface.

```java
// Subject Interface
interface Image {
    void display();
}
```

#### Step 2: Real Object
This is the object that does the real work, such as loading and displaying an image.

```java
// Real Object
class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadImageFromDisk(); // Load image during construction
    }

    private void loadImageFromDisk() {
        System.out.println("Loading image from disk: " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying image: " + filename);
    }
}
```

#### Step 3: Proxy Object
This proxy controls access to the `RealImage`. The image will only be loaded from disk when `display()` is called, demonstrating lazy initialization.

```java
// Proxy Object
class ImageProxy implements Image {
    private RealImage realImage;
    private String filename;

    public ImageProxy(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename); // Lazy initialization
        }
        realImage.display();
    }
}
```

#### Step 4: Client Code
The client interacts with the `Image` interface and doesn’t need to know whether it’s interacting with the proxy or the real object.

```java
public class ProxyPatternDemo {
    public static void main(String[] args) {
        Image image = new ImageProxy("photo.jpg");

        // The image will be loaded from disk only when display is called
        System.out.println("First call to display:");
        image.display();

        // The image will not be loaded again
        System.out.println("\nSecond call to display:");
        image.display();
    }
}
```

### Output

```
First call to display:
Loading image from disk: photo.jpg
Displaying image: photo.jpg

Second call to display:
Displaying image: photo.jpg
```

### Explanation

- **Subject (`Image`)**: This is the common interface between `RealImage` (the real object) and `ImageProxy` (the proxy).
  
- **Real Object (`RealImage`)**: This class represents the actual object that performs the resource-intensive operations, like loading an image from disk.

- **Proxy (`ImageProxy`)**: This class controls access to `RealImage`. It uses lazy initialization to delay the loading of the image until `display()` is called.

- **Client**: The client code interacts with the `Image` interface, which is either a real object or a proxy, but it doesn't need to know the difference.

### Benefits of the Proxy Pattern

1. **Lazy Initialization**: The proxy delays the creation of a resource until it’s needed. This is useful for expensive resources like files, network connections, or large datasets.

2. **Access Control**: The proxy can control access to the real object, enforcing permissions or authentication.

3. **Separation of Concerns**: The proxy can handle additional responsibilities, like logging, caching, or auditing, without changing the real object’s code.

4. **Remote Access**: Proxies can act as intermediaries in distributed systems, providing a local representation of a remote object.

5. **Memory and Performance Optimization**: By creating and loading resources only when necessary, the proxy pattern can reduce memory usage and improve system performance.

### Real-World Examples of the Proxy Pattern

- **Remote Proxy**: Java’s **RMI (Remote Method Invocation)** framework uses proxies to provide access to objects located on remote machines.
  
- **Virtual Proxy**: Many GUI frameworks (e.g., image loading) use virtual proxies to display placeholder images until the real image is loaded.

- **Protection Proxy**: Proxies can be used to control access to sensitive or restricted parts of a system. For example, a proxy might restrict access to certain files based on user permissions.

- **Smart Proxy**: A proxy that manages reference counting or logging. In some systems, a smart proxy is used to track the number of references to an object and delete it when no references are left.

### Considerations

- **Increased Complexity**: The proxy pattern introduces an additional layer between the client and the real object, which can complicate the system design.

- **Potential Performance Overhead**: While proxies can improve performance by reducing memory usage, they may introduce additional overhead by adding more method calls or performing additional tasks (like logging).

### Example Scenario for Proxy

Imagine a **banking system** where the customer data is sensitive and access to it should be controlled. A `CustomerProxy` class could be used to:
- Ensure that only authenticated users can access certain operations on `Customer` objects.
- Log all access to the customer data for audit purposes.

The **Proxy** design pattern is very flexible and can be adapted to a wide range of use cases, such as enhancing performance, securing access, logging operations, and managing resources effectively. It provides a way to add functionality without modifying the existing classes, adhering to the Open/Closed principle.

------------------------------------------------------------------------------------------

## Chain of responsibility

The **Chain of Responsibility** pattern is a behavioral design pattern that allows multiple objects (handlers) to process a request without the sender needing to know which handler will process it. This chain allows multiple handlers to either process the request or pass it along the chain to the next handler.

Each handler in the chain has two choices:
1. Handle the request and stop further processing.
2. Pass the request to the next handler in the chain.

This pattern promotes loose coupling between the sender of a request and its receivers by giving multiple objects a chance to handle the request.

### When to Use the Chain of Responsibility Pattern

- **Multiple Handlers**: When you want several objects to have a chance to handle a request, but you don’t know which object will handle it in advance.
  
- **Dynamic Request Handling**: When you want to dynamically set the sequence of handlers at runtime.

- **Command Execution**: When a request should be passed along a chain of handlers and the first handler that can process it does so.

- **Decoupling of Sender and Receiver**: When you want to decouple the sender of a request from the receiver, allowing for more flexible and extensible systems.

### Example Scenario

Imagine a **tech support system** where different levels of support (e.g., junior support, senior support, technical lead) exist. If a junior support engineer can’t solve a problem, they pass it up the chain to senior support, and if the senior engineer can’t resolve it, they pass it to the technical lead.

### Components of Chain of Responsibility

1. **Handler (Abstract class or Interface)**: Declares an interface for handling requests. Optionally, it defines a method to set the next handler in the chain.

2. **Concrete Handlers**: Implement the handler's interface and process requests they are capable of handling. If they can’t handle the request, they pass it to the next handler in the chain.

3. **Client**: Sends the request to the handler. The client is unaware of which handler will process the request.

### Chain of Responsibility Pattern Implementation in Java

Let's implement a **support system** where a customer query is passed through various levels of support staff.

#### Step 1: Handler Interface
The `SupportHandler` interface defines a method for handling requests and setting the next handler in the chain.

```java
// Handler Interface
abstract class SupportHandler {
    protected SupportHandler nextHandler;

    // Method to set the next handler in the chain
    public void setNextHandler(SupportHandler nextHandler) {
        this.nextHandler = nextHandler;
    }

    // Method to process the request
    public abstract void handleRequest(String issue);
}
```

#### Step 2: Concrete Handlers
Each concrete handler tries to process the request or passes it to the next handler in the chain.

```java
// Junior Support Handler
class JuniorSupport extends SupportHandler {
    @Override
    public void handleRequest(String issue) {
        if (issue.equals("Basic")) {
            System.out.println("Junior Support: Handling basic issue.");
        } else {
            System.out.println("Junior Support: Can't handle, passing to Senior Support.");
            if (nextHandler != null) {
                nextHandler.handleRequest(issue);
            }
        }
    }
}

// Senior Support Handler
class SeniorSupport extends SupportHandler {
    @Override
    public void handleRequest(String issue) {
        if (issue.equals("Intermediate")) {
            System.out.println("Senior Support: Handling intermediate issue.");
        } else {
            System.out.println("Senior Support: Can't handle, passing to Technical Lead.");
            if (nextHandler != null) {
                nextHandler.handleRequest(issue);
            }
        }
    }
}

// Technical Lead Handler
class TechnicalLead extends SupportHandler {
    @Override
    public void handleRequest(String issue) {
        if (issue.equals("Advanced")) {
            System.out.println("Technical Lead: Handling advanced issue.");
        } else {
            System.out.println("Technical Lead: Issue not supported.");
        }
    }
}
```

#### Step 3: Client Code
The client sets up the chain of responsibility and sends a request.

```java
public class ChainOfResponsibilityDemo {
    public static void main(String[] args) {
        // Create handlers
        SupportHandler juniorSupport = new JuniorSupport();
        SupportHandler seniorSupport = new SeniorSupport();
        SupportHandler techLead = new TechnicalLead();

        // Build the chain of responsibility
        juniorSupport.setNextHandler(seniorSupport);
        seniorSupport.setNextHandler(techLead);

        // Make requests
        System.out.println("Sending 'Basic' issue:");
        juniorSupport.handleRequest("Basic");

        System.out.println("\nSending 'Intermediate' issue:");
        juniorSupport.handleRequest("Intermediate");

        System.out.println("\nSending 'Advanced' issue:");
        juniorSupport.handleRequest("Advanced");

        System.out.println("\nSending 'Unknown' issue:");
        juniorSupport.handleRequest("Unknown");
    }
}
```

### Output

```
Sending 'Basic' issue:
Junior Support: Handling basic issue.

Sending 'Intermediate' issue:
Junior Support: Can't handle, passing to Senior Support.
Senior Support: Handling intermediate issue.

Sending 'Advanced' issue:
Junior Support: Can't handle, passing to Senior Support.
Senior Support: Can't handle, passing to Technical Lead.
Technical Lead: Handling advanced issue.

Sending 'Unknown' issue:
Junior Support: Can't handle, passing to Senior Support.
Senior Support: Can't handle, passing to Technical Lead.
Technical Lead: Issue not supported.
```

### Explanation

- **Handler Interface (`SupportHandler`)**: Defines an interface for handling requests and passing the request to the next handler in the chain.

- **Concrete Handlers (`JuniorSupport`, `SeniorSupport`, `TechnicalLead`)**: Each handler checks whether it can process the request. If it can’t, it passes the request to the next handler.

- **Client**: The client code sets up the chain and sends requests. It doesn’t know or care which handler processes the request.

### Benefits of Chain of Responsibility Pattern

1. **Decoupling of Sender and Receiver**: The sender of the request is decoupled from the object that handles the request. Multiple handlers have a chance to process the request, promoting flexibility.

2. **Simplifies Object Relationships**: The pattern eliminates direct dependencies between sender and receiver, making it easier to maintain the code.

3. **Flexible Chain Structure**: The chain can be modified at runtime by dynamically changing the order of the handlers or adding/removing handlers.

4. **Single Responsibility**: Each handler has a single responsibility — either process the request or pass it on.

### Real-World Examples of Chain of Responsibility

- **Logging Systems**: Loggers often implement the Chain of Responsibility pattern, where different log levels (e.g., DEBUG, INFO, ERROR) pass the log message up the chain until the appropriate level is reached.

- **Event Handling in GUI Frameworks**: In many GUI frameworks, events are passed through a chain of handlers, such as mouse or keyboard events, where each handler has the chance to process or pass the event.

- **Middleware in Web Frameworks**: In web frameworks like **Express.js** or **ASP.NET Core**, middleware components form a chain, where each middleware can handle the request or pass it to the next middleware.

### Considerations

- **Performance Overhead**: If the chain of responsibility is long, there may be performance overhead as the request is passed through many handlers.

- **Uncertain Handling**: There is no guarantee that the request will be handled, as it depends on the chain's structure. You may need a fallback mechanism for unhandled requests.

The **Chain of Responsibility** pattern is ideal when there are multiple potential handlers for a request, but only one should handle it. It provides flexibility, decoupling, and a clean approach to handling requests in a system where many handlers might be involved.

-----------------------------------------------------------------------------------------

## The Command Design Pattern

The **Command design pattern** is a behavioral design pattern that turns a request into a stand-alone object, which contains all the information about the request. This encapsulation allows for parameterizing methods with different requests, queuing requests, logging their execution, and supporting undoable operations.

### Key Components of the Command Pattern

1. **Command Interface**: This interface declares a method for executing commands.
2. **Concrete Command**: A class that implements the `Command` interface and performs specific actions by invoking methods on a receiver.
3. **Receiver**: The object that performs the actual work related to the command.
4. **Invoker**: The object responsible for executing commands. It stores a command and calls its `execute()` method.
5. **Client**: The client creates command objects and sets them in the invoker.

### When to Use the Command Pattern

- **Undo/Redo Functionality**: When you need to implement undo and redo actions in an application.
  
- **Parameterization of Actions**: When you need to parameterize objects with operations, like passing a command to an object to execute later.

- **Request Queuing**: When you need to queue and execute requests at a later time, possibly in different order.

- **Macro Commands**: When you need to group multiple commands into a single one (e.g., executing a series of commands in sequence).

### Command Pattern Example

Imagine a **smart home system** where a remote control can turn devices (lights, fans, etc.) on and off. Each device has specific operations, and we want to encapsulate these operations into command objects to be executed when the remote control buttons are pressed.

### Java Implementation of Command Pattern

#### Step 1: Command Interface
The `Command` interface declares a method `execute()` for performing an action.

```java
// Command Interface
interface Command {
    void execute();
}
```

#### Step 2: Receiver Class
The receiver class knows how to perform the operations. Here, we have a `Light` class with `on()` and `off()` methods.

```java
// Receiver class
class Light {
    public void on() {
        System.out.println("Light is ON");
    }

    public void off() {
        System.out.println("Light is OFF");
    }
}
```

#### Step 3: Concrete Command Classes
Concrete command classes implement the `Command` interface and encapsulate a receiver's action. For example, we have commands to turn the light on and off.

```java
// Concrete Command for turning on the light
class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.on();
    }
}

// Concrete Command for turning off the light
class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.off();
    }
}
```

#### Step 4: Invoker Class
The `Invoker` class is responsible for storing and invoking commands.

```java
// Invoker class (Remote Control)
class RemoteControl {
    private Command command;

    // Set the command to be executed
    public void setCommand(Command command) {
        this.command = command;
    }

    // Execute the stored command
    public void pressButton() {
        command.execute();
    }
}
```

#### Step 5: Client Code
The client configures the invoker with the appropriate commands.

```java
public class CommandPatternDemo {
    public static void main(String[] args) {
        // Receiver: Light
        Light livingRoomLight = new Light();

        // Concrete Commands
        Command lightOnCommand = new LightOnCommand(livingRoomLight);
        Command lightOffCommand = new LightOffCommand(livingRoomLight);

        // Invoker: Remote Control
        RemoteControl remote = new RemoteControl();

        // Turn on the light
        remote.setCommand(lightOnCommand);
        remote.pressButton(); // Output: Light is ON

        // Turn off the light
        remote.setCommand(lightOffCommand);
        remote.pressButton(); // Output: Light is OFF
    }
}
```

### Output

```
Light is ON
Light is OFF
```

### Explanation

- **Command Interface (`Command`)**: Declares the `execute()` method, which all concrete commands must implement.
  
- **Concrete Command (`LightOnCommand`, `LightOffCommand`)**: Encapsulate a receiver (the `Light` object) and define specific actions that invoke methods on the receiver.

- **Receiver (`Light`)**: Contains the actual business logic that executes the action.

- **Invoker (`RemoteControl`)**: Stores the command and triggers its execution when required.

- **Client**: Sets up the command objects and assigns them to the invoker. The client doesn't need to know the details of how commands are executed.

### Use Cases for the Command Pattern

1. **Undo/Redo Functionality**: Since each command knows how to execute and reverse an operation, it’s perfect for undoable actions. Each action can store its reverse command (e.g., undo turning on a light by turning it off).

2. **Macro Commands**: In a macro command, multiple commands can be grouped together and executed in sequence. For example, pressing one button could turn on the lights, start the fan, and play music.

3. **Task Scheduling**: Commands can be queued and executed later. For example, in a task scheduler, you could queue a series of commands that need to be executed at specific times.

4. **Callback Functionality**: When you need to send a callback to an object for execution later (e.g., GUI buttons where the action is not hard-coded).

### Benefits of the Command Pattern

1. **Decouples the Invoker and Receiver**: The invoker (e.g., remote control) doesn’t need to know which object (receiver) is performing the task. It just knows how to call the `execute()` method on a command.

2. **Supports Undo/Redo Operations**: You can store the history of commands and reverse actions by calling undo commands.

3. **Easily Extensible**: New commands can be added without modifying the invoker. You simply create new concrete command classes.

4. **Encapsulates Actions**: Commands encapsulate all the details required to perform an action, making them easily transferable and reusable.

### Real-World Examples of Command Pattern

1. **GUI Buttons**: Buttons in a graphical user interface often use the Command pattern. The button stores a command, and when clicked, it invokes that command. The same button can trigger different actions by swapping the command at runtime.

2. **Transaction Management**: In databases, a series of actions (e.g., SQL commands) can be treated as a command object. These can be queued, executed, and rolled back if necessary.

3. **Home Automation**: A remote control for various smart devices (e.g., lights, thermostats, or appliances) uses the command pattern to control the devices with ease.

The **Command design pattern** is a powerful way to encapsulate method calls, provide flexibility in scheduling and executing requests, and implement undo/redo functionality in a clean and structured way.

--------------------------------------------------------------------------------

## Interpreter Design Pattern

The **Interpreter design pattern** is a behavioral design pattern used to define a grammatical representation of a language and provide an interpreter to evaluate sentences in that language. It is particularly useful when you have a language with a simple grammar and you want to interpret or execute its sentences.

### Key Components of the Interpreter Pattern

1. **Abstract Expression**: Declares an interface for interpreting an operation.
2. **Terminal Expression**: Implements the interpretation method for the simplest elements (terminal symbols) in the grammar.
3. **Non-Terminal Expression**: Represents complex expressions, often defined recursively. These expressions can contain terminal expressions and other non-terminal expressions.
4. **Context**: Contains global information that's shared across the interpreter.
5. **Client**: The client builds the abstract syntax tree representing the language and invokes the `interpret` method to evaluate the expressions.

### When to Use the Interpreter Pattern

- When the grammar is simple and relatively stable.
- When the language needs to be evaluated dynamically or at runtime.
- When you need to interpret expressions, scripts, or rules that follow a specific grammar.

### Example of Interpreter Pattern

Consider an example where we want to evaluate simple mathematical expressions like `"3 + 2"` or `"5 - 1"`. We'll define an interpreter that can understand and compute these expressions.

### Java Implementation of Interpreter Pattern

#### Step 1: Expression Interface
The `Expression` interface declares an `interpret` method that will be implemented by all concrete expression classes.

```java
// Abstract Expression
interface Expression {
    int interpret();
}
```

#### Step 2: Terminal Expressions
The terminal expressions represent the simplest form of expressions, such as numbers.

```java
// Terminal Expression for Numbers
class NumberExpression implements Expression {
    private int number;

    public NumberExpression(int number) {
        this.number = number;
    }

    @Override
    public int interpret() {
        return number;
    }
}
```

#### Step 3: Non-Terminal Expressions
Non-terminal expressions represent more complex expressions, such as addition or subtraction, and are composed of simpler expressions (which may themselves be terminal or non-terminal).

```java
// Non-Terminal Expression for Addition
class AddExpression implements Expression {
    private Expression leftExpression;
    private Expression rightExpression;

    public AddExpression(Expression left, Expression right) {
        this.leftExpression = left;
        this.rightExpression = right;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() + rightExpression.interpret();
    }
}

// Non-Terminal Expression for Subtraction
class SubtractExpression implements Expression {
    private Expression leftExpression;
    private Expression rightExpression;

    public SubtractExpression(Expression left, Expression right) {
        this.leftExpression = left;
        this.rightExpression = right;
    }

    @Override
    public int interpret() {
        return leftExpression.interpret() - rightExpression.interpret();
    }
}
```

#### Step 4: Client Code
The client builds the expression tree and invokes the `interpret()` method to evaluate the expression.

```java
public class InterpreterPatternDemo {
    public static void main(String[] args) {
        // Represent the expression: (3 + 5) - 2
        Expression three = new NumberExpression(3);
        Expression five = new NumberExpression(5);
        Expression two = new NumberExpression(2);

        // (3 + 5)
        Expression addExpression = new AddExpression(three, five);

        // (3 + 5) - 2
        Expression subtractExpression = new SubtractExpression(addExpression, two);

        // Interpret the expression and print the result
        System.out.println("(3 + 5) - 2 = " + subtractExpression.interpret());
    }
}
```

### Output

```
(3 + 5) - 2 = 6
```

### Explanation

- **Expression Interface (`Expression`)**: Defines the `interpret` method, which all concrete expressions must implement.
  
- **Terminal Expressions (`NumberExpression`)**: Represents individual numbers in the expression. These are the leaf nodes of the expression tree.

- **Non-Terminal Expressions (`AddExpression`, `SubtractExpression`)**: Represents more complex expressions that operate on other expressions (both terminal and non-terminal).

- **Context (Not explicitly used)**: A context can be passed to the `interpret()` method to share information needed during interpretation (e.g., variable values, environment settings).

### When to Use the Interpreter Pattern

- **Script Languages**: When you need to interpret or execute simple scripting languages or rules (e.g., mathematical expressions, Boolean expressions).
  
- **Configuration File Parsing**: When a system needs to evaluate expressions or configurations dynamically based on a set of rules.

- **Evaluating Grammars**: When a domain-specific language (DSL) is used, and you need to define how to interpret it.

### Benefits of the Interpreter Pattern

1. **Extendable**: New rules or operations can easily be added by creating new expression classes.
  
2. **Simple Grammar Parsing**: Useful for small languages where the grammar is simple, and parsing can be done efficiently.

3. **Decoupling**: The grammar structure is separated from the logic that processes or interprets it, making the code more modular and easier to maintain.

### Drawbacks of the Interpreter Pattern

1. **Inefficiency**: The pattern can become inefficient when the grammar is complex, as the process of building and traversing the abstract syntax tree becomes expensive.

2. **Complexity for Larger Grammars**: As the grammar becomes larger, the number of classes required to represent the grammar grows significantly, leading to increased complexity.

### Real-World Examples of the Interpreter Pattern

1. **SQL Query Interpreters**: Systems that dynamically build and evaluate SQL queries based on user input.
  
2. **Mathematical Expression Evaluators**: Calculators that evaluate user-defined formulas at runtime.

3. **Regular Expression Engines**: Regular expressions often follow a grammar that is interpreted and matched against text patterns.

The **Interpreter pattern** is ideal for interpreting sentences of a simple grammar, where the pattern of interpretation needs to be extendable and flexible. It’s most useful for small language processing, parsing, and configuration-based tasks.

------------------------------------------------------------------------------------------

## Iterator Design Pattern

The **Iterator design pattern** is a behavioral design pattern that provides a way to access the elements of an aggregate object (like a collection) sequentially without exposing its underlying representation. It separates the iteration logic from the collection logic, allowing you to traverse through the collection elements using a standard interface.

### Key Components of the Iterator Pattern

1. **Iterator**: An interface that defines the methods for iterating over the collection (e.g., `hasNext()`, `next()`).

2. **Concrete Iterator**: Implements the `Iterator` interface and maintains the current position within the iteration of the collection.

3. **Aggregate**: An interface that defines a method to create an iterator (e.g., `createIterator()`).

4. **Concrete Aggregate**: Implements the `Aggregate` interface and returns an instance of the `Concrete Iterator`. It holds the collection of objects.

### When to Use the Iterator Pattern

- **Accessing Elements**: When you need to traverse or iterate through the elements of a collection.
  
- **Avoiding Exposure of Internal Representation**: When you want to provide access to the elements of a collection without exposing the underlying data structure.

- **Multiple Iterators**: When you need to support multiple iterators on the same collection, allowing for different traversal strategies.

### Example of Iterator Pattern

Let's say we have a collection of `Book` objects and we want to iterate over them without exposing the internal representation of the collection. We'll implement the Iterator pattern to achieve this.

### Java Implementation of Iterator Pattern

#### Step 1: Iterator Interface
Define the `Iterator` interface with methods for traversing the collection.

```java
// Iterator Interface
interface Iterator {
    boolean hasNext();
    Object next();
}
```

#### Step 2: Aggregate Interface
Define the `Aggregate` interface with a method to create an iterator.

```java
// Aggregate Interface
interface Aggregate {
    Iterator createIterator();
}
```

#### Step 3: Concrete Iterator
Implement the `ConcreteIterator` that knows how to iterate over the collection.

```java
// Concrete Iterator
class BookIterator implements Iterator {
    private BookCollection collection;
    private int index;

    public BookIterator(BookCollection collection) {
        this.collection = collection;
        this.index = 0;
    }

    @Override
    public boolean hasNext() {
        return index < collection.getSize();
    }

    @Override
    public Object next() {
        return collection.getBookAt(index++);
    }
}
```

#### Step 4: Concrete Aggregate
Implement the `ConcreteAggregate` which holds the collection and provides an iterator.

```java
// Concrete Aggregate
class BookCollection implements Aggregate {
    private List<String> books;

    public BookCollection() {
        books = new ArrayList<>();
    }

    public void addBook(String book) {
        books.add(book);
    }

    public String getBookAt(int index) {
        return books.get(index);
    }

    public int getSize() {
        return books.size();
    }

    @Override
    public Iterator createIterator() {
        return new BookIterator(this);
    }
}
```

#### Step 5: Client Code
The client uses the iterator to traverse the collection.

```java
public class IteratorPatternDemo {
    public static void main(String[] args) {
        // Create and populate the collection
        BookCollection bookCollection = new BookCollection();
        bookCollection.addBook("The Catcher in the Rye");
        bookCollection.addBook("To Kill a Mockingbird");
        bookCollection.addBook("1984");

        // Get the iterator and traverse the collection
        Iterator iterator = bookCollection.createIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

### Output

```
The Catcher in the Rye
To Kill a Mockingbird
1984
```

### Explanation

- **Iterator Interface (`Iterator`)**: Declares the `hasNext()` and `next()` methods for iterating over the collection elements.
  
- **Concrete Iterator (`BookIterator`)**: Implements the `Iterator` interface and provides the logic for iterating through the `BookCollection`.

- **Aggregate Interface (`Aggregate`)**: Declares the method `createIterator()` for creating an iterator.

- **Concrete Aggregate (`BookCollection`)**: Implements the `Aggregate` interface and manages the collection of books. It also provides the `createIterator()` method to return a new iterator.

### When to Use the Iterator Pattern

1. **Accessing Collection Elements**: When you need to iterate through the elements of a collection without exposing the internal structure of the collection.

2. **Simplifying Traversal**: When you want a standard way to access elements of a collection, allowing clients to traverse through the collection in a consistent manner.

3. **Multiple Traversals**: When you need to support multiple traversal strategies or need multiple iterators over the same collection.

4. **Separating Concerns**: When you want to separate the iteration logic from the collection logic to adhere to the Single Responsibility Principle.

### Benefits of the Iterator Pattern

1. **Encapsulation**: Hides the internal representation of the collection and provides a standard way to traverse its elements.

2. **Flexibility**: Allows for different types of iteration over the same collection without changing the collection itself.

3. **Consistency**: Provides a consistent interface for traversing different types of collections, making the code more uniform and easier to understand.

4. **Separation of Concerns**: Separates the logic for iterating through a collection from the collection logic, leading to better maintainability.

### Drawbacks of the Iterator Pattern

1. **Complexity**: For simple collections, implementing the Iterator pattern may introduce unnecessary complexity.

2. **Performance**: Additional overhead of creating iterator objects and managing their state might impact performance in some cases.

### Real-World Examples of Iterator Pattern

1. **Java Collections Framework**: The `Iterator` interface in Java's Collections Framework provides a standard way to iterate over various types of collections (e.g., `ArrayList`, `HashSet`).

2. **Navigation Systems**: Iterating through items in a navigation menu or toolbar, where each item needs to be accessed sequentially.

3. **Database Result Sets**: Iterating through rows in a database result set, where each row represents a record in the database.

The **Iterator pattern** is a powerful tool for traversing elements of a collection while maintaining encapsulation and providing a uniform interface for iteration. It's widely used in various programming scenarios where access to collection elements is required without exposing the underlying data structure.


----------------------------------------------------------------------------------------

## Mediator Design Pattern

The **Mediator design pattern** is a behavioral design pattern that defines an object that encapsulates how a set of objects interact. This pattern is used to reduce the complexity of communication between multiple objects or classes by centralizing the communication logic in a single mediator object. It promotes loose coupling and easier maintenance by preventing objects from referring to each other explicitly.

### Key Components of the Mediator Pattern

1. **Mediator**: An interface that defines the methods for communicating with different colleagues. It centralizes the communication between different components.

2. **Concrete Mediator**: Implements the `Mediator` interface and coordinates the interactions between the colleague objects. It knows all the colleague objects and handles their communication.

3. **Colleague**: An interface or abstract class for the components that interact with each other through the mediator. It has a reference to the mediator and sends requests through it.

4. **Concrete Colleague**: Implements the `Colleague` interface and communicates with other colleagues through the mediator.

### When to Use the Mediator Pattern

- **Complex Communication**: When you have multiple objects that interact with each other in complex ways, and you want to simplify their communication.

- **Loose Coupling**: When you want to decouple components, allowing them to interact without knowing about each other.

- **Centralized Control**: When you want to centralize control over communication and interaction between different components.

### Example of Mediator Pattern

Let's consider an example where we have a chat room application. The chat room (mediator) handles communication between different users (colleagues). Users send messages to the chat room, which then distributes the messages to other users.

### Java Implementation of Mediator Pattern

#### Step 1: Mediator Interface
Define the `Mediator` interface with methods for communicating with colleagues.

```java
// Mediator Interface
interface ChatMediator {
    void sendMessage(String message, User user);
    void addUser(User user);
}
```

#### Step 2: Concrete Mediator
Implement the `ConcreteMediator` which handles communication between users.

```java
// Concrete Mediator
class ChatRoom implements ChatMediator {
    private List<User> users;

    public ChatRoom() {
        users = new ArrayList<>();
    }

    @Override
    public void sendMessage(String message, User user) {
        for (User u : users) {
            // Message should not be sent to the user who sent it
            if (u != user) {
                u.receive(message);
            }
        }
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}
```

#### Step 3: Colleague Interface
Define the `Colleague` interface with a method to receive messages and a reference to the mediator.

```java
// Colleague Interface
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(ChatMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    public abstract void send(String message);
    public abstract void receive(String message);
}
```

#### Step 4: Concrete Colleague
Implement `ConcreteColleague` which uses the mediator to send and receive messages.

```java
// Concrete Colleague
class ConcreteUser extends User {

    public ConcreteUser(ChatMediator mediator, String name) {
        super(mediator, name);
    }

    @Override
    public void send(String message) {
        System.out.println(name + " is sending message: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receive(String message) {
        System.out.println(name + " received message: " + message);
    }
}
```

#### Step 5: Client Code
The client code sets up the chat room and users, and demonstrates communication.

```java
public class MediatorPatternDemo {
    public static void main(String[] args) {
        // Create the mediator
        ChatMediator chatRoom = new ChatRoom();

        // Create users
        User john = new ConcreteUser(chatRoom, "John");
        User jane = new ConcreteUser(chatRoom, "Jane");
        User mike = new ConcreteUser(chatRoom, "Mike");

        // Add users to the chat room
        chatRoom.addUser(john);
        chatRoom.addUser(jane);
        chatRoom.addUser(mike);

        // Send messages
        john.send("Hello everyone!");
        jane.send("Hi John!");
    }
}
```

### Output

```
John is sending message: Hello everyone!
John received message: Hello everyone!
Jane received message: Hello everyone!
Mike received message: Hello everyone!
Jane is sending message: Hi John!
John received message: Hi John!
Mike received message: Hi John!
```

### Explanation

- **Mediator Interface (`ChatMediator`)**: Defines methods for sending messages and adding users to the chat room.

- **Concrete Mediator (`ChatRoom`)**: Implements the `ChatMediator` interface. It manages the list of users and handles message distribution between them.

- **Colleague Interface (`User`)**: Declares methods for sending and receiving messages and maintains a reference to the mediator.

- **Concrete Colleague (`ConcreteUser`)**: Implements the `User` interface. It uses the mediator to send and receive messages.

### When to Use the Mediator Pattern

1. **Complex Interactions**: When multiple objects interact in complex ways and you want to simplify and manage these interactions.

2. **Centralized Control**: When you want to centralize control and coordination of interactions between multiple objects, making the system easier to manage.

3. **Decoupling**: When you want to reduce the dependencies between components, making the system more flexible and maintainable.

### Benefits of the Mediator Pattern

1. **Simplified Communication**: Centralizes communication logic, making it easier to manage and understand.

2. **Loose Coupling**: Reduces dependencies between objects, leading to a more modular and maintainable system.

3. **Single Responsibility**: Keeps the responsibility of communication and coordination in one place, adhering to the Single Responsibility Principle.

### Drawbacks of the Mediator Pattern

1. **Complexity**: Can introduce complexity if the mediator becomes too large or handles too many interactions.

2. **Overhead**: Centralizing communication in a mediator may add an overhead in terms of performance and management.

### Real-World Examples of Mediator Pattern

1. **GUI Systems**: In graphical user interfaces (GUIs), a mediator can be used to manage interactions between various UI components (e.g., buttons, text fields).

2. **Chat Applications**: A chat room or messaging system where a mediator manages communication between different users.

3. **Air Traffic Control**: An air traffic control system where the mediator manages communication and coordination between different aircraft.

The **Mediator pattern** is valuable for managing complex interactions between multiple objects by centralizing communication logic and promoting loose coupling. It's particularly useful in scenarios where components need to interact in a controlled manner without being tightly coupled.


-----------------------------------------------------------------------------------------

## Memento Design Pattern

The **Memento design pattern** is a behavioral design pattern that allows an object to capture and externalize its internal state without violating encapsulation, so that the object can be restored to that state later. This pattern is useful for implementing undo/redo functionality, saving the state of an object at a given point in time, or for managing checkpoints.

### Key Components of the Memento Pattern

1. **Memento**: An object that stores the internal state of the `Originator`. It typically has no methods to alter its state and is designed to be immutable.

2. **Originator**: The object whose state needs to be saved and restored. It creates a `Memento` object to store its state and can use a `Memento` to restore its state.

3. **Caretaker**: Manages the `Memento` objects. It holds onto the `Memento` and can request the `Originator` to restore its state from a `Memento`, but it does not modify or examine the content of the `Memento`.

### When to Use the Memento Pattern

- **Undo/Redo Functionality**: When you need to provide undo and redo capabilities in your application.

- **State Restoration**: When you want to save and restore the state of an object without exposing its internal structure.

- **Checkpointing**: When you need to take snapshots of an object’s state to revert to at a later time.

### Example of Memento Pattern

Consider a text editor where you want to implement undo functionality. The text editor can create snapshots of its content, which can later be used to revert to a previous state.

### Java Implementation of Memento Pattern

#### Step 1: Memento Class
Define the `Memento` class that holds the state of the `Originator`.

```java
// Memento Class
class Memento {
    private String content;

    public Memento(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }
}
```

#### Step 2: Originator Class
Define the `Originator` class that creates and restores `Memento` objects.

```java
// Originator Class
class TextEditor {
    private String content;

    public void setContent(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }

    // Create a Memento with the current state
    public Memento createMemento() {
        return new Memento(content);
    }

    // Restore the state from a Memento
    public void restoreMemento(Memento memento) {
        this.content = memento.getContent();
    }
}
```

#### Step 3: Caretaker Class
Define the `Caretaker` class that manages `Memento` objects.

```java
// Caretaker Class
class Caretaker {
    private List<Memento> mementoList = new ArrayList<>();

    public void addMemento(Memento memento) {
        mementoList.add(memento);
    }

    public Memento getMemento(int index) {
        return mementoList.get(index);
    }
}
```

#### Step 4: Client Code
Demonstrate how to use the `Memento` pattern with the `TextEditor`, `Caretaker`, and `Memento` classes.

```java
public class MementoPatternDemo {
    public static void main(String[] args) {
        // Create the originator
        TextEditor textEditor = new TextEditor();
        Caretaker caretaker = new Caretaker();

        // Set content and create mementos
        textEditor.setContent("Version 1");
        caretaker.addMemento(textEditor.createMemento());

        textEditor.setContent("Version 2");
        caretaker.addMemento(textEditor.createMemento());

        textEditor.setContent("Version 3");
        System.out.println("Current content: " + textEditor.getContent());

        // Restore to a previous state
        textEditor.restoreMemento(caretaker.getMemento(1));
        System.out.println("Restored content: " + textEditor.getContent());

        textEditor.restoreMemento(caretaker.getMemento(0));
        System.out.println("Restored content: " + textEditor.getContent());
    }
}
```

### Output

```
Current content: Version 3
Restored content: Version 2
Restored content: Version 1
```

### Explanation

- **Memento Class**: Stores the state of the `TextEditor` (i.e., its content). It provides no methods to alter the state once it is set.

- **Originator Class (`TextEditor`)**: The `TextEditor` can create a `Memento` to save its current state and restore its state from a `Memento`.

- **Caretaker Class**: Manages the list of `Memento` objects. It adds new `Memento` instances and retrieves them as needed but does not manipulate or access their content.

### When to Use the Memento Pattern

1. **Undo/Redo Functionality**: Implementing undo/redo features in applications where reverting to previous states is required.

2. **State Preservation**: When you need to save the state of an object and restore it later without exposing its internal structure.

3. **Checkpoints**: In applications where you need to create checkpoints or snapshots of an object’s state to revert to if necessary.

### Benefits of the Memento Pattern

1. **Encapsulation**: Protects the internal state of the object and only allows state restoration through the `Memento` class.

2. **Separation of Concerns**: Separates the responsibility of managing state (in the `Memento`) from the `Originator` and `Caretaker`.

3. **Flexible State Restoration**: Allows for flexible and efficient state restoration without exposing or modifying the internal structure of the `Originator`.

### Drawbacks of the Memento Pattern

1. **Memory Overhead**: Storing multiple states can lead to increased memory usage, especially if many states are stored.

2. **Complexity**: Can introduce additional complexity in managing and handling `Memento` objects.

### Real-World Examples of Memento Pattern

1. **Text Editors**: Implementing undo/redo functionality where each action or change is saved as a `Memento`.

2. **Version Control Systems**: Saving different versions or states of files, allowing users to revert to previous versions.

3. **Game Save Systems**: Saving the state of a game at various points so that players can return to those points.

The **Memento pattern** is a powerful tool for managing object states and implementing undo/redo functionality, preserving encapsulation while allowing state restoration. It is particularly useful in scenarios where state management is complex and needs to be handled with care.

-----------------------------------------------------------------------------------

## Observer Design Pattern

The **Observer design pattern** is a behavioral pattern that defines a one-to-many dependency between objects. This allows one object (the **subject**) to notify multiple dependent objects (the **observers**) of any state changes, usually by calling one of their methods. This pattern is useful for implementing distributed event-handling systems and is commonly used in scenarios where changes in one part of a system need to be automatically propagated to other parts.

### Key Components of the Observer Pattern

1. **Subject**: The object that maintains a list of observers and provides methods to attach, detach, and notify observers. It is responsible for updating all registered observers when its state changes.

2. **Observer**: An interface or abstract class defining the update method that gets called by the `Subject` when its state changes. Observers are notified of changes in the `Subject`.

3. **Concrete Subject**: A specific implementation of the `Subject` that holds the state and notifies observers of state changes.

4. **Concrete Observer**: A specific implementation of the `Observer` that updates itself based on notifications from the `Concrete Subject`.

### When to Use the Observer Pattern

- **Event Handling**: When you need to implement a system where changes to one object should be reflected in other objects automatically.

- **Decoupling**: When you want to decouple the sender of a notification from the receivers.

- **Distributed Systems**: When you have a system where multiple components need to react to changes in another component.

### Example of Observer Pattern

Let's consider an example where we have a weather station (subject) that notifies multiple display elements (observers) about changes in weather data.

### Java Implementation of Observer Pattern

#### Step 1: Observer Interface
Define the `Observer` interface with a method to update the observer.

```java
// Observer Interface
interface Observer {
    void update(float temperature, float humidity, float pressure);
}
```

#### Step 2: Subject Interface
Define the `Subject` interface with methods for attaching, detaching, and notifying observers.

```java
// Subject Interface
interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}
```

#### Step 3: Concrete Subject
Implement the `ConcreteSubject` class that maintains a list of observers and notifies them of changes.

```java
// Concrete Subject
class WeatherData implements Subject {
    private List<Observer> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherData() {
        observers = new ArrayList<>();
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }

    // Set new weather data and notify observers
    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        notifyObservers();
    }
}
```

#### Step 4: Concrete Observer
Implement the `ConcreteObserver` class that reacts to changes in the subject.

```java
// Concrete Observer
class CurrentConditionsDisplay implements Observer {
    private float temperature;
    private float humidity;

    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        display();
    }

    public void display() {
        System.out.println("Current conditions: " + temperature + "F degrees and " + humidity + "% humidity");
    }
}
```

#### Step 5: Client Code
Demonstrate how to use the `Observer` pattern with the `WeatherData` and `CurrentConditionsDisplay` classes.

```java
public class ObserverPatternDemo {
    public static void main(String[] args) {
        // Create the subject
        WeatherData weatherData = new WeatherData();

        // Create observers
        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay();

        // Register observers
        weatherData.registerObserver(currentDisplay);

        // Update weather data
        weatherData.setMeasurements(80, 65, 30.4f);
        weatherData.setMeasurements(82, 70, 29.2f);
    }
}
```

### Output

```
Current conditions: 80.0F degrees and 65.0% humidity
Current conditions: 82.0F degrees and 70.0% humidity
```

### Explanation

- **Observer Interface**: Defines the `update` method that observers use to receive updates.

- **Subject Interface**: Defines methods for registering, removing, and notifying observers.

- **Concrete Subject (`WeatherData`)**: Maintains the state (weather data) and notifies registered observers when the state changes.

- **Concrete Observer (`CurrentConditionsDisplay`)**: Implements the `Observer` interface and updates its display based on the latest weather data.

### When to Use the Observer Pattern

1. **Event Handling**: When you need to handle events or changes in one part of a system and update multiple other parts of the system.

2. **Decoupling Components**: When you want to decouple components so that the subject does not need to know about the details of its observers.

3. **Multiple Dependent Objects**: When you have multiple objects that need to be updated in response to changes in another object.

### Benefits of the Observer Pattern

1. **Loose Coupling**: Reduces dependencies between the subject and observers, making the system more flexible and easier to maintain.

2. **Dynamic Relationships**: Allows observers to be added or removed dynamically at runtime.

3. **Centralized Notification**: Provides a centralized mechanism for notifying multiple observers of changes.

### Drawbacks of the Observer Pattern

1. **Performance Issues**: If there are many observers, the performance of the notification system may be affected.

2. **Complexity**: The pattern can add complexity to the design, especially if there are many interdependent observers.

### Real-World Examples of Observer Pattern

1. **User Interface Events**: GUI frameworks where UI components (like buttons, sliders) notify listeners (observers) about user actions.

2. **Messaging Systems**: Notification systems where subscribers (observers) receive messages or updates from a publisher (subject).

3. **Stock Market Applications**: Applications where various displays or components update in response to stock price changes.

The **Observer pattern** is a powerful tool for implementing distributed event-handling systems, managing updates in a decoupled manner, and maintaining flexibility in your application's design.

------------------------------------------------------------------------------------------

## The State Design Pattern

The **State design pattern** is a behavioral pattern that allows an object to change its behavior when its internal state changes. The pattern encapsulates state-specific behavior in separate state classes, making it easier to manage and modify state-dependent behavior without changing the context (the object that maintains the state).

### Key Components of the State Pattern

1. **Context**: The class that maintains a reference to the current state and delegates state-specific behavior to the current state object. It may have methods to change the state.

2. **State**: An interface or abstract class that defines state-specific methods. Concrete state classes implement these methods to handle behavior specific to that state.

3. **Concrete States**: Classes that implement the `State` interface and provide specific behavior for different states of the context.

### When to Use the State Pattern

- **State-Dependent Behavior**: When an object’s behavior changes based on its internal state, and you want to avoid large conditional statements.

- **State Transition Management**: When you need to manage complex state transitions and encapsulate state-specific logic.

- **Complex State Management**: When you have multiple states and transitions that need to be managed in a structured way.

### Example of State Pattern

Let’s consider a simple example of a **traffic light** system. The traffic light can be in one of three states: Green, Yellow, or Red. Each state will handle the behavior of the traffic light differently.

### Java Implementation of State Pattern

#### Step 1: State Interface
Define the `State` interface with methods that represent state-specific behavior.

```java
// State Interface
interface TrafficLightState {
    void handle(TrafficLightContext context);
}
```

#### Step 2: Concrete State Classes
Implement concrete state classes for each state of the traffic light.

```java
// Concrete State: Green
class GreenLightState implements TrafficLightState {
    @Override
    public void handle(TrafficLightContext context) {
        System.out.println("Green Light: Go!");
        context.setState(new YellowLightState());
    }
}

// Concrete State: Yellow
class YellowLightState implements TrafficLightState {
    @Override
    public void handle(TrafficLightContext context) {
        System.out.println("Yellow Light: Caution!");
        context.setState(new RedLightState());
    }
}

// Concrete State: Red
class RedLightState implements TrafficLightState {
    @Override
    public void handle(TrafficLightContext context) {
        System.out.println("Red Light: Stop!");
        context.setState(new GreenLightState());
    }
}
```

#### Step 3: Context Class
Define the `TrafficLightContext` class that maintains the current state and delegates behavior to it.

```java
// Context Class
class TrafficLightContext {
    private TrafficLightState state;

    public TrafficLightContext() {
        // Initial state
        state = new GreenLightState();
    }

    public void setState(TrafficLightState state) {
        this.state = state;
    }

    public void change() {
        state.handle(this);
    }
}
```

#### Step 4: Client Code
Demonstrate how to use the State pattern with the `TrafficLightContext` and state classes.

```java
public class StatePatternDemo {
    public static void main(String[] args) {
        TrafficLightContext trafficLight = new TrafficLightContext();

        // Simulate traffic light changes
        trafficLight.change(); // Green Light: Go!
        trafficLight.change(); // Yellow Light: Caution!
        trafficLight.change(); // Red Light: Stop!
        trafficLight.change(); // Green Light: Go!
    }
}
```

### Output

```
Green Light: Go!
Yellow Light: Caution!
Red Light: Stop!
Green Light: Go!
```

### Explanation

- **State Interface**: Defines the `handle` method for state-specific behavior.

- **Concrete States**: Implement `TrafficLightState` and provide specific behavior for each state of the traffic light.

- **Context Class (`TrafficLightContext`)**: Maintains the current state and delegates the `handle` method to the current state. It changes the state by calling `setState`.

### When to Use the State Pattern

1. **State-Dependent Behavior**: When the behavior of an object varies significantly with its state and you want to avoid cluttering the context with conditional logic.

2. **Complex State Management**: When you have multiple states and transitions that need to be managed systematically.

3. **Encapsulation of State-Specific Behavior**: When you want to encapsulate state-specific behavior in separate classes to improve maintainability and readability.

### Benefits of the State Pattern

1. **Improved Maintainability**: Encapsulates state-specific behavior in separate classes, making the code easier to maintain and extend.

2. **Simplified Context**: Reduces complexity in the context class by delegating state-specific logic to state classes.

3. **Flexible State Transitions**: Allows for easy addition of new states and transitions without modifying existing code.

### Drawbacks of the State Pattern

1. **Increased Number of Classes**: May result in a large number of classes if there are many states.

2. **Complexity**: Can add complexity to the design if not used judiciously.

### Real-World Examples of State Pattern

1. **State Machines**: Systems where the behavior depends on discrete states and transitions, such as workflow engines or process managers.

2. **Game Development**: Games where entities have different behaviors based on their state (e.g., characters in different states like idle, attacking, or defending).

3. **User Interfaces**: UI components that behave differently based on their state (e.g., a button that changes appearance based on whether it’s enabled or disabled).

The **State pattern** is a powerful tool for managing state-dependent behavior in an organized and maintainable manner, providing a structured approach to handle complex state transitions and behavior changes.


----------------------------------------------------------------------------------------

## Strategy Design Pattern

The **Strategy design pattern** is a behavioral pattern that defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable. This allows the algorithm to vary independently from clients that use it. The Strategy pattern is used to enable selecting an algorithm's implementation at runtime, making it easier to switch between different strategies without altering the client code.

### Key Components of the Strategy Pattern

1. **Strategy**: An interface or abstract class that defines a common interface for all supported algorithms. Each concrete strategy implements this interface.

2. **Concrete Strategies**: Classes that implement the `Strategy` interface, providing specific implementations of the algorithm.

3. **Context**: The class that uses a `Strategy` object to perform some operation. The context may have a method to set or change the strategy dynamically.

### When to Use the Strategy Pattern

- **Algorithm Variability**: When you have multiple algorithms for a specific task, and you want to be able to switch between them dynamically.

- **Open/Closed Principle**: When you want to extend functionality with new algorithms without modifying existing code.

- **Encapsulation of Algorithms**: When you need to encapsulate different algorithms in separate classes, making it easier to manage and understand.

### Example of Strategy Pattern

Let’s consider an example of a **payment system** where different payment methods (credit card, PayPal, bank transfer) are implemented as different strategies. The payment method can be selected and applied at runtime.

### Java Implementation of Strategy Pattern

#### Step 1: Strategy Interface
Define the `PaymentStrategy` interface with a method for processing payments.

```java
// Strategy Interface
interface PaymentStrategy {
    void pay(int amount);
}
```

#### Step 2: Concrete Strategies
Implement concrete strategy classes for different payment methods.

```java
// Concrete Strategy: Credit Card Payment
class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card: " + cardNumber);
    }
}

// Concrete Strategy: PayPal Payment
class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using PayPal: " + email);
    }
}

// Concrete Strategy: Bank Transfer Payment
class BankTransferPayment implements PaymentStrategy {
    private String accountNumber;

    public BankTransferPayment(String accountNumber) {
        this.accountNumber = accountNumber;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Bank Transfer: " + accountNumber);
    }
}
```

#### Step 3: Context Class
Define the `ShoppingCart` class that uses a `PaymentStrategy` to process payments.

```java
// Context Class
class ShoppingCart {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(int amount) {
        if (paymentStrategy == null) {
            System.out.println("No payment method selected.");
        } else {
            paymentStrategy.pay(amount);
        }
    }
}
```

#### Step 4: Client Code
Demonstrate how to use the Strategy pattern with the `ShoppingCart` and payment strategy classes.

```java
public class StrategyPatternDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        // Pay using Credit Card
        cart.setPaymentStrategy(new CreditCardPayment("1234-5678-9876-5432"));
        cart.checkout(100);

        // Pay using PayPal
        cart.setPaymentStrategy(new PayPalPayment("user@example.com"));
        cart.checkout(200);

        // Pay using Bank Transfer
        cart.setPaymentStrategy(new BankTransferPayment("9876543210"));
        cart.checkout(300);
    }
}
```

### Output

```
Paid 100 using Credit Card: 1234-5678-9876-5432
Paid 200 using PayPal: user@example.com
Paid 300 using Bank Transfer: 9876543210
```

### Explanation

- **Strategy Interface**: Defines a common interface (`pay` method) for all payment strategies.

- **Concrete Strategies**: Implement the `PaymentStrategy` interface with specific payment methods (Credit Card, PayPal, Bank Transfer).

- **Context Class (`ShoppingCart`)**: Uses a `PaymentStrategy` to process payments. The strategy can be set or changed dynamically.

### When to Use the Strategy Pattern

1. **Multiple Algorithms**: When you have multiple algorithms or strategies for a specific task, and you want to switch between them at runtime.

2. **Avoiding Conditional Statements**: When you want to avoid complex conditional statements in your code that choose different algorithms.

3. **Open/Closed Principle**: When you want to add new strategies without modifying existing code.

### Benefits of the Strategy Pattern

1. **Flexibility**: Allows dynamic switching between different algorithms or strategies at runtime.

2. **Encapsulation**: Encapsulates algorithms in separate classes, making the code easier to understand and maintain.

3. **Adherence to Open/Closed Principle**: Supports the addition of new strategies without changing existing code.

### Drawbacks of the Strategy Pattern

1. **Increased Number of Classes**: Can lead to a proliferation of classes, especially if there are many strategies.

2. **Complexity**: May add complexity to the design if not used judiciously.

### Real-World Examples of Strategy Pattern

1. **Sorting Algorithms**: Different sorting algorithms (e.g., quicksort, mergesort) that can be selected based on the data being sorted.

2. **Compression Algorithms**: Different compression algorithms (e.g., ZIP, GZIP) used for data compression.

3. **Route Calculation**: Different route-finding algorithms in GPS systems (e.g., shortest path, fastest route) that can be selected based on user preferences.

The **Strategy pattern** is a versatile and powerful tool for managing different algorithms or behaviors in a flexible and maintainable way, allowing you to easily switch between different strategies and extend functionality without altering existing code.