Design Pattern
==============

References:
- [Refactoring Guru](https://refactoring.guru/design-patterns/factory-method)


# Table of Conten
## [Creational Patterns](#)
1. [Factory Method](#factory-method) 
2. [Abstact Factory]() 
3. [Builder]() 
4. [Prototype]() 
5. [Singleton]() 


## [Structural Patterns](#)
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

The Factory Method is a creational design pattern that defines an interface for creating objects, but lets subclasses decide which class to instantiate. In other words, it provides a way to delegate the instantiation logic to child classes.

A common use case for the Factory Method pattern is when you need to create objects that share a common interface or base class, but may differ in the specific implementation details. Instead of tightly coupling your code to these implementations, you can use a factory to create the objects based on some condition, parameter, or configuration.

![example](/home/norin/Desktop/design-pattern/resources/factory-1.png)

---
![example](/home/norin/Desktop/design-pattern/resources/factory-2.png)


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


