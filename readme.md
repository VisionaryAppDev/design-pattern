Design Pattern
==============

References:
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)


# Table of Content
## [Creational Patterns](#creational-patterns-2)
1. [Factory Method](#factory-method) 
2. [Abstact Factory]() 
3. [Builder]() 
4. [Prototype]() 
5. [Singleton]() 


## [Structural Patterns](#structural-patterns-2)
1. [Adapter]()
2. [Bridge]()
3. [Composite]()
4. [Decorator]()
5. [Facade]()
6. [Flyweight]()
7. [Proxy]()


## [Behavioral Patterns](#)
1. [Chian of Responsibility]()
2. [Command]()
3. [Iterator]()
4. [Mediator]()
5. [Memeto]()
6. [Observer]()
7. [State]()
8. [Strategy]()
9. [Template Method]()
10. [Visitor]()

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

