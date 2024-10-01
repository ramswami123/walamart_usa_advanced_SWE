<h> **Task -2 Software Architecture**</h>

<p>After much deliberation amongst your team, you have been trusted to design part of a new data processing pipeline. You will be responsible for coming up with the architecture for a dynamically reconfigurable data processor. The processor will have several different modes, each of which treats incoming data in a different way. Some modes will pass the result along to a database, and others will additionally validate the data against the database. To further complicate matters, there are several databases in play, and the processor needs the ability to toggle between them on the fly. The system needs to be extendable - your team has every intention of adding additional modes and databases in the future - so take extra care to ensure the system isn’t rigid. Adhere to good design principles, use design patterns where they make sense, and remember your SOLID principles. Your project lead will use this to assess your ability to design clean code, so be sure to show off what you know. Success here could mean a promotion, don’t squander the chance!</p>

<div>
  . Object-Oriented Design (OOD) and Principles
a) Encapsulation, Inheritance, and Polymorphism
Encapsulation: Group related data and methods into a single unit, i.e., a class. It helps protect the internal state of objects and ensures only specific methods can modify it.

Example: A Database class might have private methods for connecting to the database, while publicly exposing an insert method.
Inheritance: Allows one class to inherit behavior from another, promoting code reuse.

Example: A PostgresDatabase class can inherit from a generic Database class and implement the database-specific insert and validate methods.
Polymorphism: Means "many forms." It allows different classes to be treated as instances of the same superclass, particularly useful in implementing different database behaviors (Postgres, Redis, Elastic).

Example: insert(data) in different database classes (Postgres, Redis) behaves differently but can be used through the same interface.
b) SOLID Principles (Key design principles that improve maintainability and flexibility)
S: Single Responsibility Principle (SRP): A class should have one and only one reason to change. For instance, your processor class should focus on processing data, and database classes should focus on interacting with their respective databases.
O: Open/Closed Principle (OCP): Classes should be open for extension but closed for modification. For example, you could extend a base Database class for new databases without changing existing code.
L: Liskov Substitution Principle (LSP): Subclasses should be able to replace their base classes without altering the correct functioning of the program.
I: Interface Segregation Principle (ISP): Instead of having a single, large interface, create smaller, specific ones.
D: Dependency Inversion Principle (DIP): Depend on abstractions, not concrete classes. Use interfaces or abstract classes for your databases.
2. Design Patterns
a) Strategy Pattern
The Strategy Pattern is perfect when you need to define a family of algorithms or behaviors (modes in your case) and make them interchangeable. Each mode (Dump, Passthrough, Validate) can be its own strategy, and the processor can switch between them dynamically.
Example: The processor could have a modeStrategy attribute that can be set to DumpMode, PassthroughMode, or ValidateMode.
b) Factory Pattern
The Factory Pattern is used to create objects without exposing the instantiation logic to the client. It can help you manage which Database class to instantiate based on the DatabaseIdentifier.
Example: A DatabaseFactory class could have a createDatabase() method that returns the appropriate database object (Postgres, Redis, or Elastic) based on the passed identifier.
c) State Pattern
The State Pattern is used to allow an object to change its behavior when its internal state changes. You can apply this to manage transitions between different processor modes.
Example: The processor could have a state object representing its current mode, which dynamically alters its process(data) method.
d) Dependency Injection
Dependency Injection allows the processor to receive a database object (dependency) from outside, making it flexible and easier to test.
Example: Instead of the processor class creating database objects internally, you inject the appropriate database instance through the constructor or setter methods.
3. UML Diagrams
a) Class Diagrams
In a UML class diagram, classes are represented with boxes that show their name, attributes, and methods. Relationships like inheritance, composition, or aggregation between classes are represented with different types of arrows.
Example: Draw classes for Processor, Database, PostgresDatabase, RedisDatabase, etc., and show inheritance relationships.
b) State Diagrams
A state diagram shows the different states an object can be in and the transitions between them. This would be useful for visualizing how the processor moves between DumpMode, PassthroughMode, and ValidateMode.
Example: States are shown as circles, and transitions (like a mode switch) are arrows connecting these states.
4. Enum and Switch Statements
Enums (Enumerations) are special data types that define a set of named values. In your case, you can use them to represent processor modes (Dump, Passthrough, Validate) and databases (Postgres, Redis, Elastic).
In some programming languages (e.g., Java, C++), enums are used with switch statements to change behavior based on the enum value.
Example: The process(data) method could use a switch statement or if-else chain to change its behavior based on the current mode or database.
5. Database Abstraction
You need to define a common interface or abstract class for all databases. This will ensure the processor can use any database implementation without worrying about specific details.
Example: A Database interface could have methods like connect(), insert(data), and validate(data) which each specific database class (PostgresDatabase, RedisDatabase, etc.) will implement.
6. Testing Strategies
Learn how to write unit tests for your system:
Mocking: Use mocks to simulate the database connections and test how the processor handles different databases and modes without actually needing a live database.
Test different modes: You could write tests for process(data) in DumpMode, PassthroughMode, and ValidateMode to ensure it behaves as expected.
Test database switching: Ensure that switching databases works correctly and that the correct methods are called for the respective database.
Suggested Learning Path
Object-Oriented Principles: Start by reading about OOP principles and trying out basic examples to understand encapsulation, inheritance, and polymorphism. You could follow courses on OOP in Python, Java, or C++ depending on your preferred language.
Design Patterns: Study the most commonly used patterns (like Strategy, Factory, State) through books like Design Patterns: Elements of Reusable Object-Oriented Software or online courses on platforms like Udemy or Coursera.
UML Diagrams: Practice drawing class and state diagrams using tools like Lucidchart, Draw.io, or UML design software.
Enums and Switch Statements: Understand how enums work in your programming language and experiment with them using if-else or switch-case structures.
Database Abstraction: Look for tutorials on creating abstract classes and interfaces, especially for interacting with different databases.
Unit Testing and Mocking: Learn unit testing techniques, especially how to mock dependencies. For Python, look into libraries like unittest and pytest.
</div>
