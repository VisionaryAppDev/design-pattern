Design Pattern
==============

References:
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)


# Table of Content
## [Creational Patterns](#creational-patterns-2)
1. [Factory Method](#factory-method) 
2. [Abstact Factory](#abstract-factory)
3. [Builder](#builder)
4. [Prototype](#prototype)
5. [Singleton](#singleton)


## [Structural Patterns](#structural-patterns-2)
1. [Adapter](#adapter)
2. [Bridge](#bridge)
3. [Composite](#composite)
4. [Decorator](#decorator)
5. [Facade](#facade)
6. [Flyweight](#flyweight)
7. [Proxy](#proxy)


## [Behavioral Patterns](#)
1. [Chain of Responsibility](#chain-of-responsibility)
2. [Command](#command)
3. [Iterator](#iterator)
4. [Mediator](#mediator)
5. [Memeto](#memeto)
6. [Observer](#observer)
7. [State](#state)
8. [Strategy](#stategy)
9. [Template Method](#template-method)
10. [Visitor](#visitor)

## Creational Patterns
### Factory Method

The Factory Method pattern is a creational design pattern that provides an interface for creating objects but lets subclasses decide which class to instantiate. In other words, the factory method pattern defines an interface for creating an object, but allows the subclasses to decide which class to instantiate based on the requirements.

The Factory Method pattern is useful when there are several classes that implement a common interface, and it is not known at compile time which implementation will be used. The factory method pattern allows for flexibility in creating objects and makes it easy to add new implementations without modifying existing code.

One analogy for the Factory Method pattern is a pizza restaurant. The pizza restaurant has a common interface, which is to make a pizza. However, the type of pizza made depends on the order. The restaurant has several options for pizza, such as pepperoni, cheese, and vegetarian. The order is the client in this scenario, and the pizza chef is the factory. The pizza chef creates the pizza based on the order and returns the appropriate type of pizza to the client.

A sample use case for the Factory Method pattern is in a shopping cart application. Suppose the shopping cart needs to create an object for each item added to the cart. The item may be a book, a toy, or a piece of clothing, and each item has different attributes and behaviors. Rather than having a single class to create objects, the Factory Method pattern can be used to create a separate factory class for each item. The factory class can create the appropriate object based on the item type, which allows for flexibility in adding new items to the cart without modifying existing code.

Another use case for the Factory Method pattern is in a game development application. The game may have several types of characters, such as warriors, mages, and archers. Each character type has different attributes and behaviors, and the appropriate character type needs to be created based on the user's choice. The Factory Method pattern can be used to create a separate factory class for each character type. The factory class can create the appropriate character object based on the user's choice, which allows for flexibility in adding new character types to the game without modifying existing code.

In summary, the Factory Method pattern provides flexibility in creating objects and allows for easy addition of new implementations without modifying existing code. It is useful when there are several classes that implement a common interface, and it is not known at compile time which implementation will be used.

![example](resources/factory-1.png)

---
![example](resources/factory-2.png)


Example 1:
```
public enum LogisticType {
    LAND("LAND"),
    SEA("SEA");

    private final String type;

    public LogisticType(String type) {
        this.type = type;
    }
}
```

```
public interface LogisticService {
    void deliver(String destination);
    LogisticType getType();
}
```

```
@Service
public class LandLogisticService implements LogisticService {
    public void deliver(String destination);
        // implementation for credit card payment
    }

    public LogisticType getType() {
        return LogisticType.Land;
    }
}
```

```
@Service
public class SeaLogisticService implements LogisticService {
    public void deliver(String destination);
        // implementation for credit card payment
    }

    public LogisticType getType() {
        return LogisticType.Sea;
    }
}
```

```
@Service
public class LogisticFactory {
    @Autowired
    private List<LogisticService> logisticServices;

    public LogsticService getLogisticService(LogisticType type) {
        return logisticServices.stream
        (
            .filter(logstic -> logistic.getType().equals(type.type))
            .findAny()
            .orElseThrow()-> {
                throw new IllegalArgumentException("Invalid logistic type: " + type);
            }
        );
    }
}
```


## Structural Patterns
### Bridge
The Bridge Design Pattern is a structural design pattern that decouples an abstraction from its implementation, allowing both to vary independently. It involves creating two separate abstraction and implementation hierarchies, and connecting them using a bridge interface. This allows the implementation to be changed or extended without affecting the abstraction, and vice versa.

The Bridge Design Pattern is useful when there are multiple variations in functionality, and the implementation details may change frequently. By separating the abstraction from the implementation, the Bridge pattern allows for more flexibility and scalability in the codebase.

A common use case for the Bridge Design Pattern is in graphical user interfaces (GUIs), where there are multiple types of controls that can be implemented in different ways. For example, a button control can be implemented as a standard button, a dropdown button, or a toggle button. The implementation of each type of button can vary, but the abstraction (the fact that it is a button control) remains the same.

Another use case for the Bridge Design Pattern is in database applications, where there are multiple database systems (such as MySQL, Oracle, or PostgreSQL) that can be used to store data. By separating the abstraction (the database interface) from the implementation (the specific database system), the application can support multiple database systems without needing to modify the codebase.

Suppose you have a music player application that can play different types of audio files such as MP3, WAV, and FLAC. You want to add support for different types of operating systems such as Windows, Linux, and macOS. You can use the bridge design pattern to decouple the abstraction of the music player from the implementation of the operating system. The music player can be the abstraction, and the operating system can be the implementation. The bridge between them can be the operating system interface. By using the bridge design pattern, you can add support for new operating systems without changing the music player code.

Suppose a person who wants to cross a river. They could choose to swim across, but that would be difficult and time-consuming. Instead, they could use a bridge to cross the river quickly and easily. The bridge provides a standardized interface (a path over the river) that can be used by different people (or objects) to cross the river in their own way. In software development, the bridge pattern can be thought of as a way to cross the gap between different abstractions or systems, just as a physical bridge crosses a gap between two points. It allows two or more different systems to work together by providing a standard interface that can be used by each system to communicate with the other.

![example](resources/bridge-1.png)
---
![example](resources/bridge-2.png)

Here is a sample code example in Java to illustrate the Bridge Design Pattern:
```
// Abstraction interface
public interface Shape {
    void draw();
}
```

```
// Concrete implementation
public class Rectangle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}
```

```
// Concrete implementation
public class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}
```

```
// Bridge interface
public interface Color {
    void fill();
}
```

```
// Concrete implementation
public class RedColor implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with red color");
    }
}
```

```
// Concrete implementation
public class BlueColor implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with blue color");
    }
}
```

```
// Abstraction class
public abstract class AbstractShape {
    protected Color color;
    
    public AbstractShape(Color color) {
        this.color = color;
    }
    
    public abstract void draw();
}
```

```
// Refined abstraction class
public class RectangleShape extends AbstractShape {
    public RectangleShape(Color color) {
        super(color);
    }
    
    @Override
    public void draw() {
        System.out.print("Drawing a rectangle shape. ");
        color.fill();
    }
}
```

```
// Refined abstraction class
public class CircleShape extends AbstractShape {
    public CircleShape(Color color) {
        super(color);
    }
    
    @Override
    public void draw() {
        System.out.print("Drawing a circle shape. ");
        color.fill();
    }
}
```

```
// Usage example
public class Main {
    public static void main(String[] args) {
        Color redColor = new RedColor();
        Color blueColor = new BlueColor();
        
        AbstractShape rectangleShape = new RectangleShape(redColor);
        AbstractShape circleShape = new CircleShape(blueColor);
        
        rectangleShape.draw(); // Output: Drawing a rectangle shape. Filling with red color
        circleShape.draw(); // Output: Drawing a circle shape. Filling with blue color
    }
}
```

### Facade
The Facade pattern is a software design pattern that provides a simplified interface to a complex system of classes, interfaces, and APIs. It hides the complexity of the system and provides a simpler interface that the client can use to interact with the system.

The Facade pattern is useful when you have a complex system that needs to be used by multiple clients or when you want to isolate the clients from the complexities of the system. It promotes loose coupling between the client and the system, which makes the system easier to modify and maintain.

The Facade pattern is similar to a concierge at a hotel. The concierge provides a simplified interface to the complex system of services available in the hotel. The guests can use the concierge to book a taxi, reserve a table at a restaurant, or order room service without having to interact with the individual services directly.

In software development, a Facade can be used to provide a simple interface to a complex system of objects or APIs. For example, in a web application, a Facade can be used to provide a simplified interface to a set of APIs that are used to access a database.

Some of the use cases for the Facade pattern include:
- Simplifying the interface to a complex system
- Providing a layer of abstraction between the client and the system
- Promoting loose coupling between the client and the system
- Improving the maintainability and extensibility of the system

An example of using the Facade pattern in a web application is to provide a simplified interface for accessing a database. Instead of exposing the full functionality of the database APIs to the client, the Facade can provide a set of simple CRUD (create, read, update, delete) operations that the client can use to interact with the database. This makes it easier for the client to use the database and also makes it easier to modify the database implementation without affecting the clients.

Another example is providing a simplified interface for a complex system of objects or APIs in a software development framework. For example, in the Spring framework, the Spring JDBC Template class provides a simplified interface for accessing a database. It encapsulates the complexity of the JDBC API and provides a simpler and more intuitive API for interacting with the database.

Suppose we have a complex system that includes several subsystems, each of which has its own set of classes and objects. To simplify the interaction with this system, we could create a facade class that provides a simplified interface to the subsystems.

![example](resources/facade.png)

```
public class SystemFacade {
    private SubsystemA subsystemA;
    private SubsystemB subsystemB;
    private SubsystemC subsystemC;

    public SystemFacade() {
        subsystemA = new SubsystemA();
        subsystemB = new SubsystemB();
        subsystemC = new SubsystemC();
    }

    public void doSomething() {
        subsystemA.doSomething();
        subsystemB.doSomething();
        subsystemC.doSomething();
    }
}
```






## READ
- [When to use the Bridge pattern and how is it different from the Adapter pattern?](https://stackoverflow.com/questions/319728/when-to-use-the-bridge-pattern-and-how-is-it-different-from-the-adapter-pattern)

The Bridge pattern is an application of the old advice, "prefer composition over inheritance". It becomes handy when you must subclass different times in ways that are orthogonal with one another. Say you must implement a hierarchy of colored shapes. You wouldn't subclass Shape with Rectangle and Circle and then subclass Rectangle with RedRectangle, BlueRectangle and GreenRectangle and the same for Circle, would you? You would prefer to say that each Shape has a Color and to implement a hierarchy of colors, and that is the Bridge Pattern. Well, I wouldn't implement a "hierarchy of colors", but you get the idea...
 
 When:
```

                   ----Shape---
                  /            \
         Rectangle              Circle
        /         \            /      \
BlueRectangle  RedRectangle BlueCircle RedCircle
```


Refactor to:
```

          ----Shape---                        Color
         /            \                       /   \
Rectangle(Color)   Circle(Color)           Blue   Red
```
