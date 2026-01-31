Structural Design Pattern:
- While building a large application, dozens of components needs work together
- Without proper system to manage, code become a tangled web of dependencies
- Making changes may break multiple components because tightly coupled relationships


Structural design patterns helps in establish well-defined, flexible connection between components,
reducing dependencies and making the system easier to understand, extend and maintain.

Types of Structural Design Pattern:

1. Adapter Pattern: The Universal Translator
Acts as a bridge between two incompatible interfaces, allowing them to work together 
without altering their underlying code.

ex: Integrating a third-party API that has different data format than your application's internal structure

2. Bridge Pattern: Separation of concerns
Helps to split a large class into two separate hierarchies-abstraction and implementation which can be developed independently of eachother.

ex: Designing a cross platform UI framework that separates platform specific implementations from shared abstraction

3. Composite Pattern: Building a hierarchy
Treats individual objects and group of objects uniformly making it easier to work with complex hierarchies.

ex: Representing a folder structure in a operating system, where files and folders are treated uniformly

4. Decorator Pattern: Customizing on the Fly
Allows dynamically add new new behaviours or responsibilities to objects without modifying their structure

ex: Adding features to a text editor, such as spell check or auto-format, without modifying the core editor functionality

5. Facade Pattern: Simplifying complexity
Simplified interface to a complex subsystem, making it easier to interact with, without dealing 
with all the underlying details

ex: Simplifying access to a complex video player library, by providing single play/pause interface

6. Flyweight Pattern: Sharing resources efficiently
Minimizes memory uses by sharing common parts of objects while allowing unique details for each instance.

ex: Managing characters in a word processor by processing fonts and styles across repeated characters

7. Proxy Pattern: The Middleman
Provides a placeholder or surrogate for another object, controlling access to it or adding extra behaviour

ex: Controlling access to a remote database by using a proxy class to cache data locally

advantage:
- Organized code
- Reduced dependencies
- Reusability
- Simplified maintenance


