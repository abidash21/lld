Design Principle
-To maintain, scalable and easy to understand, to achieve this foundational guideline to achieve this is SOLID Principle
- Scalability: adding new features becomes straight forward
- Maintainability: changes in one part of the system has minimal impact on others
- Testability: Decoupled design makes unit testing stronger
- Readability: Clear separation of concerns improves code comprehensions

SOLID Principles
* SRP - Single Responsibility Principle
* OCP - Open Closed Principle
* LSP - Liskov Substitution Principle
* ISP - Interface Segregation Principle
* DIP - Dependency Inversion Principle

1. SINGLE RESPONSIBILITY PRINCIPLE
- A class should have only one reason to change

********* bad code *********

```java
class BreadBaker {
 public
  void bakeBread() { System.out.println("Baking high-quality bread..."); }

 public
  void manageInventory() { System.out.println("Managing inventory..."); }

 public
  void orderSupplies() { System.out.println("Ordering supplies..."); }

 public
  void serveCustomer() { System.out.println("Serving customers..."); }

 public
  void cleanBakery() { System.out.println("Cleaning the bakery..."); }

 public
  static void main(String[] args) {
    BreadBaker baker = new BreadBaker();
    baker.bakeBread();
    baker.manageInventory();
    baker.orderSupplies();
    baker.serveCustomer();
    baker.cleanBakery();
  }
}



******** good code *******


class BreadBaker {
    public void bakeBread() {
        System.out.println("Baking high-quality bread...");
    }
}

class InventoryManager {
    public void manageInventory() {
        System.out.println("Managing inventory...");
    }
}

class SupplyOrder {
    public void orderSupplies() {
        System.out.println("Ordering supplies...");
    }
}

class CustomerService {
    public void serveCustomer() {
        System.out.println("Serving customers...");
    }
}

class BakeryCleaner {
    public void cleanBakery() {
        System.out.println("Cleaning the bakery...");
    }
}

public class Bakery {
    public static void main(String[] args) {
        BreadBaker baker = new BreadBaker();
        InventoryManager inventoryManager = new InventoryManager();
        SupplyOrder supplyOrder = new SupplyOrder();
        CustomerService customerService = new CustomerService();
        BakeryCleaner cleaner = new BakeryCleaner();

        baker.bakeBread();
        inventoryManager.manageInventory();
        supplyOrder.orderSupplies();
        customerService.serveCustomer();
        cleaner.cleanBakery();
    }
}

- The code becomes more maintainable
- Easier to understand
- Changes in one class doesn't affect unrelated parts
- Enhances readability and reduces complexity
- Each class has a clear and focused Responsibility
- The system is more modular and easy to manage


2. OPEN CLOSED PRINCIPLE
- Open for extension but closed for modification


********* bad code *********

class Shape {
 private
  String type;
 public
  double calculateArea() {
    if (type.equals("circle")) {
      // Circle area calculation
    } else if (type.equals("rectangle")) {
      // Rectangle area calculation
    }
  }
}


******** good code *******

abstract class Shape {
    abstract double calculateArea();
}

class Circle extends Shape {
    private double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;

    Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}

class Triangle extends Shape {
    private double height;
    private double base;

    Triangle(double height, double base) {
        this.height = height;
        this.base = base;
    }

    @Override
    public double calculateArea() {
        return 0.5 * height * base;
    }
}


- Prevents breaking existing code
- Encourages reusable components
- Code is more maintainable
- Adding new shape doesn't require modification in existingcode

3. LISKOV SUBSTITUTION PRINCIPLE

- Any class that is child of a parent class should be usable in place of its parent without any 
  any unexpected behaviour.

********* bad code *********

class Vehicle {
 public
  void startEngine() {
   
  }
}

class Car extends Vehicle {
  @Override public void startEngine() {
    
  }
}

class Bicycle extends Vehicle {
  @Override public void startEngine() {
    throw new UnsupportedOperationException("Bicycles don't have engines");
  }
}

public class Main {
 public
  static void main(String[] args) {
    Vehicle car = new Car();
    Vehicle bicycle = new Bicycle();
    System.out.println("Car:");
    car.startEngine();  
    System.out.println("nBicycle:");
    try {
      bicycle.startEngine(); 
    } catch (UnsupportedOperationException e) {
      System.out.println("Error: " + e.getMessage());
    }
  }
}


******** good code *******

- When a subclass can not fulfill the contract of the parent class, it leads to a a breakdown in polymorphism
- If new vehicles types are added that do not have engines, they too would be forced to implement startEngine() method
- The tight coupling between vehicle class and its subclasses reduces the modularily and reusablity of the code


abstract class Vehicle {
    public
    void move(){

    }
}

abstract class EngineVehicle extends Vehicle {
    public
    void startEngine(){ }
}

abstract class NonEngineVehicle extends Vehicle {

}

abstract class Car extends EngineVehicle {
    @Override public void startEngine() {

    }
}

abstract class Bicycle extends NonEngineVehicle {

}

public class Main(){
    public
     static void main(String[] args){
        EngineVehicle car = new Car();
        car.startEngine();  
        car.move();      

        NonEngineVehicle bicycle = new Bicycle();
        bicycle.move();  
     }
}

- Each subtype fully satisfies the behavioural contract of its parent type
- Client code can interact with either vehicle type without unexpected behaviour
- The inheritance hierarchy accurately models the real world domain

4. INTERFACE SEGREGATION PRINCIPLE

- This is the first principle that is applied to interface rather than classes.
- It is similar to single responsibility principle.
- Do not force any client to implement an interface which is irrelevant to them.


****** bad code *******

interface Machine {
  void print();
  void scan();
  void fax();
}

class AllInOnePrinter implements Machine {
  @Override public void print() {
  }
  @Override public void scan() {
  }
  @Override public void fax() {
  }
}

class BasicPrinter implements Machine {
  @Override public void print() {
  }
  @Override public void scan() {
    throw new UnsupportedOperationException("Cannot scan");
  }
  @Override public void fax() {
    throw new UnsupportedOperationException("Cannot fax");
  }
}

******** good code ********

interface Printer {
  void print();
}

interface Scanner {
  void scan();
}

interface FaxMachine {
  void fax();
}

class BasicPrinter implements Printer {
  @Override
  public void print() {
  }
}

class AllInOnePrinter implements Printer, Scanner, FaxMachine {
  @Override
  public void print() {
  }
  @Override
  public void scan() {
  }
  @Override
  public void fax() {
  }
}


- Follows the principle of "interface cohesion": Each interface has a specific responsibility , leading to better cohesion and separation of concerns
- By segregating interfaces, we ensure that classes only implement methods that are relevant to their functionality,


5. DEPENDENCY INVERSION PRINCIPLE

- High level modules should not depend on low level modules. Both should depend on abstraction.
- Abstraction should not depend on details. Details should depend on abstraction.
- Class should rely on abstractions (interface or abstract classes) rather than concrete implementations.
- This allows for more flexible and decoupled code, making it easier to change implementation without affecting
  other part of the codebase.


********* bad code ********

class EmailNotifier {
  public void sendEmail(String message) {
  }
}

class OrderService {
  private EmailNotifier emailNotifier;
  private DatabaseLogger logger;
  private InventorySystem inventory;
  public OrderService() {
    // Direct dependencies on concrete implementations
    this.emailNotifier = new EmailNotifier();
    this.logger = new DatabaseLogger();
    this.inventory = new InventorySystem();
  }
  public void placeOrder(Order order) {
    // Process order
    inventory.updateStock(order);
    emailNotifier.sendEmail("Order #" + order.getId() + " placed successfully");
    logger.logTransaction("Order placed: " + order.getId());
  }
}



******* good code ********

interface NotificationService {
    public void sendNotification(String message);
}

interface LoggingService {
    void logMessage(String message);
    void logError(String error);
}

interface InventoryService {
    void updateStock(Order order);
    boolean checkAvailability(Product product);
}

class EmailNotifier extends NotificationService {
    @override
    public void sendNotification(String message){
    }
}

class SMSNotifier implements NotificationService {
  @Override
  public void sendNotification(String message){
  }
}

class PushNotifier implements NotificationService {
  @Override
  public void sendNotification(String message){
  }
}

class DatabaseLogger implements LoggingService {
  @Override
  public void logMessage(String message) 
  }
  @Override
  public void logError(String error){
  }
}

class OrderService {
  private final NotificationService notificationService;
  private final LoggingService loggingService;
  private final InventoryService inventoryService;

  public OrderService(
    NotificationService notificationService,
    LoggingService loggingService, 
    InventoryService inventoryService) {
        this.notificationService = notificationService;
        this.loggingService = loggingService;
        this.inventoryService = inventoryService;
  }

  public void placeOrder(Order order) {
    try {
      // Check inventory
      if (inventoryService.checkAvailability(order.getProduct())) {
        // Process order
        inventoryService.updateStock(order);
        // Send notification
        notificationService.sendNotification(
            "Order #" + order.getId() + " placed successfully");
        // Log success
        loggingService.logMessage(
            "Order processed successfully: " + order.getId());
      }
    } catch (Exception e) {
      loggingService.logError(
          "Error processing order: " + order.getId() + " - " + e.getMessage());
      throw e;
    }
  }
}

NotificationService emailNotifier = new EmailNotifier();
LoggingService logger = new DatabaseLogger();
InventoryService inventory = new WarehouseInventoryService();
OrderService orderService = new OrderService(emailNotifier, logger, inventory);