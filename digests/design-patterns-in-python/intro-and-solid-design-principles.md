# Design Patterns in Python

Gang of Four book, translated to Python.

- End-of-section coding exercise.
- One Python file per demo.
- "Latest" version of Python (as of when?)
  - liberal use of decorators, metaclasses where applicable
  - external packages will also be used if valuable

## Author

- Dmitri Nesteruk, quant finance professional
- Course author on: Pluralsight, Udemy, Elsewhere
  - Design patterns in: C#, Java, C++, Swift, Python

## Other Topics

- Sequence processing (streams/Rx)
- Concurrency
- Dependency injection

## Languages picked up these design patterns already

- C# implementation of observer pattern
- Python implementation of decorator
- third party libraries

## Three Categories of Design Patterns

All from the book.

- Creational
  - Builder
  - Factories (two patterns): Abstract Factory, Factory Method
  - Prototype
  - Singleton
- Structural
  - Adapter
  - Bridge
  - Composite
  - Decorator
  - Facade
  - Flyweight
  - Proxy
- Behavioral
  - Chain of Responsibility
  - Command
  - Interpreter
  - Iterator
  - Mediator
  - Memento
  - Observer
  - State
  - Strategy
  - Template Method
  - Visitor


## Solid Design Principles

- Introduced by "uncle Bob", Robert C. Martin
    - Multiple books, plus blog
    - There are a rather large number of design principles
      - 5 selected SOLID

1. Single Responsibility Principle (SRP): "Separation of Concerns"
2. Open-Closed Principle

### 1. Single Responsibility Principle (SRP): "Separation of Concerns"

Example: Journal class that also has persistence (save, load)

> Journal class stores and allows manipulating entries, but then also gets functionality for persistence. This is a bad idea for a number of reasons. Persistence would go in its own class. Instead write a `PersistenceManager` class with a static `save_to_file(j, filename)` method.

- Antipattern: 'God Object', everything into a single class.

### 2. Open-Closed Principle: "Open for Extension, Closed for Modification."

Example: Product  has some properties, size, color.

> How do you filter product by color? Use a for loop to filter by color. But now we want to filter by size. When you add new functionality, add by extension, not modification. Now try filter by color and size... you add a third function for color AND size. This approach is combinatorial. You are also causing a `state-space explosion`. Add weight and for 3 params you need summation(3) filters: 3+2+1




### 3. Liskov Substitution Principle







