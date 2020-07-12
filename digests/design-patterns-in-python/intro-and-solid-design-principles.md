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

- Introduced by "Uncle Bob", Robert C. Martin
    - Multiple books, plus blog
    - There are a rather large number of design principles
      - 5 selected SOLID

1. Single Responsibility Principle (SRP): "Separation of Concerns"
2. Open-Closed Principle
3. Liskov Substitution Principle
4. Interface Segregation Principle
5. Dependency Inversion Principle


### 1. Single Responsibility Principle (SRP): "Separation of Concerns"

Example: Journal class that also has persistence (save, load)

> Journal class stores and allows manipulating entries, but then also gets functionality for persistence. This is a bad idea for a number of reasons. Persistence would go in its own class. Instead write a `PersistenceManager` class with a static `save_to_file(j, filename)` method.

- Antipattern: 'God Object', everything into a single class.

### 2. Open-Closed Principle: "Open for Extension, Closed for Modification."

Example: Product  has some properties, size, color.

> How do you filter product by color? Use a for loop to filter by color. But now we want to filter by size. When you add new functionality, add by extension, not modification. Now try filter by color and size... you add a third function for color AND size. This approach is combinatorial. You are also causing a `state-space explosion`. Add weight and for 3 params you need summation(3) filters: 3+2+1

Lets add the new filters through modification and use an "enterprise pattern".

"Enterprise patterns require a separate course."

#### Enterprise Pattern: "Specification"



```
class Product:
    def __init__(self, name, color, size):
        self.name = name
        self.color = color
        self.size = size

# OCP = open for extension, closed for modification

# see the course resources for the full implementation with some testing
class Specification:
    ''' determine if an item specifies a criteria

    This is a base class. You are intended to override the methods.
    '''
    def is_satisfied(self, item):
        pass
    # this is explained later, i think it's foolish and breaks expectations for the reader of the code...
    def __and__(self, other):
        return AndSpecification(self, other)


class Filter:
    ''' General method, doesn't specify any particular criteria.

    This is a base class. You are intended to override the methods.
    '''
    def filter(self, items, spec):
        pass

class ColorSpecification(Specification):
    def __init__(self, color):
        self.color = color
    def is_satisfied(self, item):
        return item.color == self.color

class SizeSpecification(Specification):
    def __init__(self, size):
        self.size = size
    def is_satisfied(self, item):
        return item.size == self.size

class BetterFilter(Filter):
    def filter(self, items, spec):
        for item in items:
            if spec.is_satisfied(item):
                yield item

# How do we implement the combinator `AND` with these?
class AndSpecification(Specification):
    ''' check that any number of specifications apply
    '''
    def __init__(self, *args):
        self.args = args

    def is_satisfied(self, item):
        # NB: all() returns True if empty, but false for e.g. [''] or [None]
        return all(map(
            lambda spec: spec.is_satisfied(item), self.args
        ))

# This is the combinator
large_and_blue = AndSpecification(SizeSpecification(Size.LARGE), ColorSpecification(Color.BLUE))
bf = BetterFilter()
for p in bf.filter(products, large_and_blue)

# we want to simplify large_and_blue though, we can overload the `binary and` operator, `&`
# lets do this in `Specification` above, are we breaking the open closed principle? no we would do this at the beginning (trent: not business realistic...)
# This is silly, breaks type expectation for reader. Just keep it simple, accumulate and explode a sequence or something
large_and_blue = SizeSpecification(Size.LARGE) & ColorSpecification(Color.BLUE)
```

### 3. Liskov Substitution Principle

- Named after Barbara Liskov.
- If you have an interface named after a base class you should be able to stick a derived class in and everything should work.
- Imagine a `Rectangle` class and a `Square` class that inherits from rectangle. Square should work wherever rectangle worked.
    - So maybe we expect `width*height=area`, where class rectangle has each `@property`: width, height.
    - so for square, lets just take one dimension, `size`, since width is height.
        - Now if we set width and height at the same time, both from `size`, "this looks very innocent"
    - now if we use `use_it`, it only works on a rectangle, because it sets width, height explicitly.
        - We can fix `use_it` a few ways: don't have a square class (doesn't solve use_it), don't allow the setters
            - trent: avoid square class is the right answer, we should still use `@property` in Python.
            - trent: **so this means that our descendants are constrained by our downstream implementations?  i don't love this...**
                - So uh... When we need to refactor, we need to enumerate downstream impelementation before we can subclass something? Well, alright...


### 4. Interface Segregation Principle

- If you have a "kitchen sink interface", then individual implementations have a bunch of NOOP methods.
- If someone makes an instance of a limited implementation, they try using the NOOP methods.



### 5. Dependency Inversion Principle


