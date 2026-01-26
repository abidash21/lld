- Instead of creating objects directly all over your code, creational design patterns provides a smart,
  controlled and organized way to handle the object creation process.
- Creational pattern centralize and streamline object creation, making system more flexible and easier to maintain


Types of Creational Design Patterns:

1. SINGLETON DESIGN PATTERN
- It ensures that there is only one instance of a class throughout the entire system
- Prevents resource wastage & ensures consistent behaviour
- Factory Manager, one person in charge of making the most important product
- ex: A single database connection shared across the whole system

2. FACTORY METHOD PATTERN
- Instead of specifying the exact product type, simply call the factory method to handle it
- Automatic assembly line, factory knows how to produce different types of products
- ex: CarFactory creates different car models dynamically

3. ABSTRACT FACTORY PATTERN
- It's a Mega Factory. The factory produces multiple related products
- Instead of creating a single product , it creates families of objects
- ex: FurnitureFactory creates chairs, tables and sofas together

4. BUILDER PATTERN
- It's like a custom order system
- While creating a complex products, you don't want to handle it in one go
- The builder pattern lets you break down the creation process into steps
- ex: Building luxuary cars with step by step features

5. PROTOTYPE PATTERN
- Copying a ready-made product
- Instead of creating objects from scratch, clone an existing one
- Save time and resources
- ex: Creating clones of gaming characters


Advantags:
- Simplifies object creation: No scattered object creation logic, everything is organized
- Flexibility: Add a new type of object without changin the entire codebase
- Maintainability: If need to change how object is created, only need to at one place instead of modifying multiple parts