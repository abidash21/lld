DRY(Don't Repeat Yourself)
- Avoid duplication of code in a system
- Create reusable components, functions or modules that can be utilized in various parts of the codebase
- Code reusablity, Readability, Maintenance and updates, Consistency, Reduced Development time, Facilitates        collaboration, Avoidance of copy-paste errors, Testability


How to implement DRY principles
1. Use Functions and Methods - Encapsulate repetitive code into reusable functions or methods.
2. Leverage Object-Oriented Principles - Use inheritance, polymorphism, and interfaces to share behavior between classes.
3. Use constants and configuration files - Avoid hardcoding values by defining them in a single location.


Advantages:
- Efficiency
- Maintainability
- Scalability
- Consistency
- Collaboration

Disadvantages:
- Over-Abstraction Risks: Too much abstraction can make code harder to read and debug.
- Initial Time Investment: Writing reusable code often requires more upfront planning and effort.
- Misuse: Applying DRY inappropriately to unrelated functionalities can lead to tight coupling and reduced flexibility.
- Complex Refactoring: Refactoring legacy code to adhere to DRY can be time-consuming and error-prone.
