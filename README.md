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

-------------------------------------------------------------------------------