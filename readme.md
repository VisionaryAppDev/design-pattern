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


## [Behavioral Patterns](#behavioral-patterns-2)
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

### Decorator
The decorator pattern is a design pattern that allows behavior to be added to an individual object dynamically, without affecting the behavior of other objects from the same class. It is one of the structural design patterns.

The decorator pattern involves a set of decorator classes that are used to wrap concrete components. These decorator classes are used to add new functionality to an existing object dynamically. The original object can be decorated with one or more decorator classes, each adding new behavior to the original object.

One example of the decorator pattern is a coffee shop where customers can order a cup of coffee with various toppings such as whipped cream, caramel, or sprinkles. In this scenario, the base coffee represents the component and the toppings represent the decorators. Customers can choose to add one or more toppings to their coffee, and each topping can be combined in any order.

The decorator pattern is useful when:
- You want to add behavior to an object dynamically without affecting other objects of the same class.
- You want to add behavior to an object that is not possible or feasible to extend using inheritance.
- You want to be able to remove the added behavior dynamically.

Some use cases of the decorator pattern include:
- Adding additional functionality to a graphical user interface (GUI) component, such as adding a border or a tooltip.
- Adding functionality to a text editor, such as adding spell checking or auto-complete.
- Adding security checks or logging to an existing system.

Overall, the decorator pattern provides a flexible way to add new behavior to an existing object, without affecting the behavior of other objects of the same class.

![img](resources/decorator-1.png)

Imagine that you’re working on a notification library which lets other programs notify their users about important events. At some point, you realize that users of the library expect more than just email notifications. Many of them would like to receive an SMS about critical issues. Others would like to be notified on Facebook and, of course, the corporate users would love to get Slack notifications. And now people want use several notification type at once.

![img](resources/decorator-3.png)


By using the decorator pattern in this case could be a good decision because it allows for dynamic behavior and flexibility in adding or modifying the behavior of objects at runtime. Each notification type can be represented as a decorator that adds the necessary behavior to the base notification object. This makes it easy to add new notification types without having to modify the existing code, and it also makes it easy to combine different notification types to create composite notifications. Additionally, it can also help to reduce code duplication and improve maintainability.
![img](resources/decorator-5.png)

Example 1:
```
public interface Notification {
    void send(String message);
}
```

```
public class EmailNotification implements Notification {
    @Override
    public void send(String message) {
        System.out.println("Sending email notification: " + message);
    }
}
```

```
public class SmsNotificationDecorator implements Notification {
    private final Notification notification;

    public SmsNotificationDecorator(Notification notification) {
        this.notification = notification;
    }

    @Override
    public void send(String message) {
        notification.send(message);


        /// Sending SMS Notification Implementation
        System.out.println("Sending SMS notification: " + message);
    }
}
```

```
Notification emailNotification = new EmailNotification();
Notification smsNotification = new SmsNotificationDecorator(emailNotification);
```

Example 2:
```
public interface TextFormatter {
    String format(String text);
}
```

```
public class PlainTextFormatter implements TextFormatter {
    @Override
    public String format(String text) {
        return text;
    }
}
```

```
public abstract class TextDecorator implements TextFormatter {
    private TextFormatter textFormatter;

    public TextDecorator(TextFormatter textFormatter) {
        this.textFormatter = textFormatter;
    }

    @Override
    public String format(String text) {
        return textFormatter.format(text);
    }
}
```

```
public class BoldTextDecorator extends TextDecorator {
    public BoldTextDecorator(TextFormatter textFormatter) {
        super(textFormatter);
    }

    @Override
    public String format(String text) {
        return "<b>" + super.format(text) + "</b>";
    }
}
```

```
public class ItalicTextDecorator extends TextDecorator {
    public ItalicTextDecorator(TextFormatter textFormatter) {
        super(textFormatter);
    }

    @Override
    public String format(String text) {
        return "<i>" + super.format(text) + "</i>";
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

### Proxy
The Proxy pattern is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. In other words, a proxy acts as a middleman between a client and the real object, handling all requests and performing additional tasks such as caching, logging, or authentication.

The main purpose of the Proxy pattern is to provide a level of indirection between a client and a real object, enabling greater flexibility and control over how the client interacts with the object. The Proxy pattern is particularly useful when working with remote or expensive resources that should be accessed through a local object that can handle caching, authentication, or other tasks.

Imagine you are the CEO of a big company and you have a personal assistant who manages all of your scheduling and meetings. Your assistant is the Proxy in this scenario, as they act as an intermediary between you and the people you are meeting with.When someone wants to schedule a meeting with you, they go through your assistant, who checks your availability and schedules the meeting accordingly. Similarly, when you attend a meeting, your assistant will be present to take notes and make sure everything goes smoothly. In this case, your personal assistant is acting as a proxy, representing you and your schedule to the outside world. This allows you to focus on your work without being constantly interrupted by meeting requests and scheduling details.

Some sample use cases for the Proxy pattern include:
1. Caching: The proxy can cache results from a remote or expensive operation, improving performance by reducing the number of requests to the real object.
2. Remote access: The proxy can provide a local interface to a remote object, allowing clients to access the object over a network.
3. Security: The proxy can handle authentication and authorization for the real object, ensuring that only authorized clients can access it.
4. Virtual proxy: The proxy can create a placeholder for an expensive object until it is actually needed, allowing the application to start up faster and reducing memory usage.

In terms of implementation, the Proxy pattern can be implemented using either a static or dynamic proxy. A static proxy is created at compile time and requires a separate proxy class for each real object. A dynamic proxy is created at runtime and can handle multiple real objects using reflection.

In Spring, the Proxy pattern is often used to implement AOP (Aspect-Oriented Programming), where a proxy is used to intercept method calls and apply additional behavior such as logging, caching, or transaction management. Spring also provides support for creating dynamic proxies using either JDK or CGLIB, allowing for flexible and efficient implementation of proxies.

![img](resources/proxy-1.png)

Suppose you have a web application that accesses a remote API to fetch data. However, the remote API has a limit on the number of requests that can be made in a certain time period. To avoid exceeding this limit, you can use a proxy pattern to cache the results of previous requests and serve them from the cache when the same request is made again within a certain time period.
```
public interface RemoteApi {
    String getData(String key);
}
```

```
public class RealRemoteApi implements RemoteApi {
    public String getData(String key) {
        // make the actual request to the remote API and return the data
    }
}
```

```
public class RemoteApiProxy implements RemoteApi {
    private RealRemoteApi realRemoteApi;
    private Map<String, String> cache = new HashMap<>();
    private long cacheExpiryTime = 60000; // 1 minute

    public RemoteApiProxy(RealRemoteApi realRemoteApi) {
        this.realRemoteApi = realRemoteApi;
    }

    public String getData(String key) {
        String data = cache.get(key);
        if (data == null || System.currentTimeMillis() > cacheExpiryTime) {
            // data not in cache or cache has expired, make request to real remote API
            data = realRemoteApi.getData(key);
            cache.put(key, data);
            cacheExpiryTime = System.currentTimeMillis() + 60000; // set cache expiry time to 1 minute from now
        }
        return data;
    }
}
```
In this example, RealRemoteApi is the actual implementation of the remote API interface, and RemoteApiProxy is a proxy that caches the results of previous requests. When a request is made to RemoteApiProxy, it first checks if the data is in the cache and if the cache has not expired. If the data is in the cache and the cache has not expired, the data is returned from the cache. Otherwise, the proxy makes a request to the real remote API to fetch the data, caches the data, and returns it to the caller.




## Behavioral Patterns
### Chain of Responsibility
The Chain of Responsibility pattern is a behavioral pattern that allows you to pass requests through a chain of handlers until one of them handles the request. Each handler has a reference to the next handler in the chain, forming a linked list of handlers. The request is passed through the chain until one handler can handle it or until the end of the chain is reached.

The Chain of Responsibility pattern is useful when you have a set of handlers that can handle a request, but you don't know which one to use until runtime. It's also useful when you want to decouple the sender of a request from its receiver.

A common example of the Chain of Responsibility pattern is in a web application that has multiple filters to process a request. Each filter checks the request for certain criteria and either handles the request or passes it to the next filter in the chain.

Another example is in a customer service system, where customer complaints are handled by different levels of support personnel. A complaint is first handled by a lower level support agent, and if they can't resolve the issue, it's passed up the chain to a higher level support agent.

An analogy for the Chain of Responsibility pattern is a customer support phone system, where the customer's request is routed through a series of prompts and menus until it reaches the appropriate support agent who can handle the request.

In terms of implementation, each handler in the chain must have a method for handling the request and a reference to the next handler in the chain. The client code that creates the chain of handlers only needs to know about the first handler in the chain. The handler can either handle the request or pass it on to the next handler in the chain.

Overall, the Chain of Responsibility pattern provides a flexible and extensible way to handle requests that can be handled by multiple handlers in a dynamic and efficient way.

![img](resources/chain-of-responsibility-1.png)

Imagine you're building a software for a bank. The bank has different levels of approval for loan applications based on the loan amount. If the loan amount is less than $10,000, it can be approved by the bank manager alone. If the amount is between $10,000 and $50,000, it needs approval from the bank manager as well as the regional manager. If it's more than $50,000, it needs approval from the bank manager, regional manager, and the head office.

In this case, you can use the Chain of Responsibility pattern to create a chain of approvers. Each approver in the chain will check if they have the authority to approve the loan based on the loan amount. If they do, they will approve it and pass it on to the next approver in the chain. If they don't, they will simply pass it on to the next approver.
```
public abstract class LoanApprover {
    protected LoanApprover nextApprover;

    public void setNextApprover(LoanApprover nextApprover) {
        this.nextApprover = nextApprover;
    }

    public abstract void processLoan(Loan loan);
}
```

```
public class BankManager extends LoanApprover {
    public void processLoan(Loan loan) {
        if (loan.getAmount() < 10000) {
            System.out.println("Loan approved by Bank Manager");
        } else if (nextApprover != null) {
            nextApprover.processLoan(loan);
        }
    }
}
```

```
public class RegionalManager extends LoanApprover {
    public void processLoan(Loan loan) {
        if (loan.getAmount() < 50000) {
            System.out.println("Loan approved by Regional Manager");
        } else if (nextApprover != null) {
            nextApprover.processLoan(loan);
        }
    }
}
```

```
public class HeadOffice extends LoanApprover {
    public void processLoan(Loan loan) {
        if (loan.getAmount() >= 50000) {
            System.out.println("Loan approved by Head Office");
        } else if (nextApprover != null) {
            nextApprover.processLoan(loan);
        }
    }
}
```

```
public class Loan {
    private double amount;

    public Loan(double amount) {
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }
}
```

```
public class LoanApprovalChain {
    public static void main(String[] args) {
        LoanApprover bankManager = new BankManager();
        LoanApprover regionalManager = new RegionalManager();
        LoanApprover headOffice = new HeadOffice();
        
        /// Setup chain of approval.
        /// Start from the lower to higher (manager -> regional -> HQ)
        bankManager.setNextApprover(regionalManager);
        regionalManager.setNextApprover(headOffice);

        Loan loan1 = new Loan(5000);
        bankManager.processLoan(loan1);

        Loan loan2 = new Loan(25000);
        bankManager.processLoan(loan2);

        Loan loan3 = new Loan(75000);
        bankManager.processLoan(loan3);
    }
}
```
In this example, we have three different LoanApprovers - BankManager, RegionalManager, and HeadOffice. We create a chain of approvers by setting the next approver for each approver. Finally, we create three different loans and pass them to the BankManager to be processed. The BankManager will check if they have the authority to approve the loan based on the loan amount, and if not, pass it on to the next approver in the chain.



### Command
The Command pattern is a behavioral design pattern that encapsulates a request as an object, by letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

The main idea behind the Command pattern is to separate the requester of an action from the object that performs the action. This separation provides greater flexibility and allows you to design a system that can handle multiple types of requests, while still keeping it simple and easy to use.

A good example of the Command pattern is a restaurant order system. A waiter takes orders from customers and sends them to the kitchen for processing. In this scenario, the waiter acts as the invoker, and the kitchen acts as the receiver. Each order is a command object that contains all the necessary information to prepare the food, such as the type of dish, the ingredients, and the cooking instructions.

Another example of the Command pattern is a remote control for a TV. The remote control is the invoker, and the TV is the receiver. Each button on the remote control is a command object that sends a specific request to the TV, such as changing the channel, adjusting the volume, or turning the TV on or off.

The Command pattern is useful in situations where you want to decouple the requester of an action from the object that performs the action. It is especially useful in situations where you need to support undoable or redoable operations, as each command object can keep track of its own state and provide an undo or redo method.

In Spring Boot, the Command pattern can be used to encapsulate and execute database transactions. Each command object represents a database operation, such as creating a new record, updating an existing record, or deleting a record. The invoker can then execute the command object, which will perform the database operation and return the result. This allows you to decouple the business logic of your application from the database access layer, making it easier to maintain and test your code.


### [Example](https://refactoring.guru/design-patterns/command)
Imagine that you’re working on a new text-editor app. Your current task is to create a toolbar with a bunch of buttons for various operations of the editor. You created a very neat Button class that can be used for buttons on the toolbar, as well as for generic buttons in various dialogs.

![example](resources/command-1.png)

While all of these buttons look similar, they’re all supposed to do different things. Where would you put the code for the various click handlers of these buttons? The simplest solution is to create tons of subclasses for each place where the button is used. These subclasses would contain the code that would have to be executed on a button click.
Lots of button subclasses

![example](resources/command-2.png)

Before long, you realize that this approach is deeply flawed. First, you have an enormous number of subclasses, and that would be okay if you weren’t risking breaking the code in these subclasses each time you modify the base Button class. Put simply, your GUI code has become awkwardly dependent on the volatile code of the business logic.

![example](resources/command-3.png)

And here’s the ugliest part. Some operations, such as copying/pasting text, would need to be invoked from multiple places. For example, a user could click a small “Copy” button on the toolbar, or copy something via the context menu, or just hit Ctrl+C on the keyboard.

#### Solution
Good software design is often based on the principle of separation of concerns, which usually results in breaking an app into layers. The most common example: a layer for the graphical user interface and another layer for the business logic. The GUI layer is responsible for rendering a beautiful picture on the screen, capturing any input and showing results of what the user and the app are doing. However, when it comes to doing something important, like calculating the trajectory of the moon or composing an annual report, the GUI layer delegates the work to the underlying layer of business logic.

In the code it might look like this: a GUI object calls a method of a business logic object, passing it some arguments. This process is usually described as one object sending another a request.
![example](resources/command-4.png)

The Command pattern suggests that GUI objects shouldn’t send these requests directly. Instead, you should extract all of the request details, such as the object being called, the name of the method and the list of arguments into a separate command class with a single method that triggers this request.

Command objects serve as links between various GUI and business logic objects. From now on, the GUI object doesn’t need to know what business logic object will receive the request and how it’ll be processed. The GUI object just triggers the command, which handles all the details.
![example](resources/command-5.png)

The next step is to make your commands implement the same interface. Usually it has just a single execution method that takes no parameters. This interface lets you use various commands with the same request sender, without coupling it to concrete classes of commands. As a bonus, now you can switch command objects linked to the sender, effectively changing the sender’s behavior at runtime.

You might have noticed one missing piece of the puzzle, which is the request parameters. A GUI object might have supplied the business-layer object with some parameters. Since the command execution method doesn’t have any parameters, how would we pass the request details to the receiver? It turns out the command should be either pre-configured with this data, or capable of getting it on its own.
![example](resources/command-6.png)

#### Coding
```
public interface Command {
    void execute();
    void undo();
}
```

```
public class CopyCommand implements Command {
    private final TextEditor editor;

    public CopyCommand(TextEditor editor) {
        this.editor = editor;
    }

    @Override
    public void execute() {
        editor.copy();
    }

    @Override
    public void undo() {
        editor.clearSelection();
    }
}
```

```
public class PasteCommand implements Command {
    private final TextEditor editor;

    public PasteCommand(TextEditor editor) {
        this.editor = editor;
    }

    @Override
    public void execute() {
        editor.paste();
    }

    @Override
    public void undo() {
        editor.clearSelection();
    }
}
```

```
public class UndoCommand implements Command {
    private final TextEditor editor;

    public UndoCommand(TextEditor editor) {
        this.editor = editor;
    }

    @Override
    public void execute() {
        editor.undo();
    }

    @Override
    public void undo() {
        editor.redo();
    }
}

// ... other command classes for different operations
```

```
public class TextEditorInvoker {
    private final List<Command> commandHistory = new ArrayList<>();
    private final TextEditor editor;

    public TextEditorInvoker(TextEditor editor) {
        this.editor = editor;
    }

    public void executeCommand(Command command) {
        command.execute();
        commandHistory.add(command);
    }

    public void undoLastCommand() {
        if (!commandHistory.isEmpty()) {
            Command lastCommand = commandHistory.remove(commandHistory.size() - 1);
            lastCommand.undo();
        }
    }
}
```

```
TextEditor editor = new TextEditor();
TextEditorInvoker invoker = new TextEditorInvoker(editor);

Command copyCommand = new CopyCommand(editor);
Command pasteCommand = new PasteCommand(editor);
Command undoCommand = new UndoCommand(editor);

invoker.executeCommand(copyCommand);
invoker.executeCommand(pasteCommand);
invoker.executeCommand(undoCommand);

invoker.undoLastCommand();
```

#### Note
The Invoker class in the Command pattern acts as a client for the Command object. It is responsible for invoking the command object's execute() method at the appropriate time. The Invoker typically doesn't know anything about the Command object or what operation it performs. Instead, it simply calls the execute() method on the Command object when needed.

The reason for having an Invoker class is to separate the responsibility of invoking an operation from the operation itself. By doing this, we can decouple the objects that invoke the operation from the objects that perform the operation. This makes the system more flexible and easier to maintain because we can change the way operations are invoked without affecting the objects that perform the operations.

In a Spring Boot application, the Invoker class can be implemented as a service or a controller, depending on the context in which the Command pattern is being used. For example, if the Command pattern is being used to implement an undo/redo functionality, the Invoker class might be implemented as a controller that listens to user input and executes the appropriate Command object's execute() method. On the other hand, if the Command pattern is being used to perform some long-running background operation, the Invoker class might be implemented as a Spring service that runs the command asynchronously.


### State
The state pattern is a behavioral design pattern that allows an object to change its behavior when its internal state changes. It involves encapsulating different behaviors into separate state classes, and the context object can delegate to the current state object to perform the appropriate behavior based on its internal state.

The state pattern is useful when you have an object that behaves differently based on its internal state, and when adding new states or behaviors can be done easily without affecting the existing code. It is also useful when you have a large conditional block that depends on the internal state of an object, as it can be refactored into separate state classes.

A good example for the state pattern is a traffic light. A traffic light changes its behavior based on its current state (red, yellow, green). Each state (red, yellow, green) has its own behavior (stop, prepare to stop, go), and the traffic light delegates to the current state to perform the appropriate behavior.

Some sample use cases for the state pattern include:
- A vending machine that behaves differently based on its current state (e.g. no money inserted, money inserted but no selection made, selection made but no change given)
- A game character that has different behaviors based on its current state (e.g. standing, walking, running, jumping)
- An ATM machine that behaves differently based on the user's current state (e.g. idle, card inserted, PIN entered, transaction in progress)
- When the phone is unlocked, pressing buttons leads to executing various functions.
- When the phone is locked, pressing any button leads to the unlock screen.
- When the phone’s charge is low, pressing any button shows the charging screen.


Imagine that we have a Document class. A document can be in one of three states: Draft, Moderation and Published. The publish method of the document works a little bit differently in each state:
- In Draft, it moves the document to moderation.
- In Moderation, it makes the document public, but only if the current user is an administrator.
-  In Published, it doesn’t do anything at all.
![img](resources/state-1.png)

In Java, the state pattern can be implemented using interfaces or abstract classes to represent the different states, and a context class that maintains a reference to the current state object. The context class can delegate to the current state object to perform the appropriate behavior. Here's a simple example using Java:


```
public interface State {
    void handle(Context context);
}
```

```
public class StateA implements State {
    @Override
    public void handle(Context context) {
        // Behavior for state A
        // Do sth (eg, stop music and then update the state) and then toggle state to B
        context.setState(new StateB());
    }
}

```

```
public class StateB implements State {
    @Override
    public void handle(Context context) {
        // Behavior for state B
        // Do sth (eg, start music and then update the state) and then toggle state to A
        context.setState(new StateA());
    }
}

```

```
public class Context {
    private State currentState;

    public Context(State initialState) {
        this.currentState = initialState;
    }

    public void setState(State newState) {
        this.currentState = newState;
    }

    // The Action button that will perform specific task based on current state
    public void handleRequest() {
        this.currentState.handle(this);
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
