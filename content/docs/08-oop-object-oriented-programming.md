---
title: "Ch 8: Object-Oriented Programming (OOP)"
weight: 8
---

# Object-Oriented Programming (OOP)

## Learning Objectives

After reading this chapter, you will be able to:
- Define classes and create objects
- Understand instance methods, class methods, and static methods
- Use inheritance and composition effectively
- Leverage magic (dunder) methods for custom behavior
- Work with properties, descriptors, and slots
- Apply OOP principles (encapsulation, inheritance, polymorphism)

---

## 8.1 Classes and Objects

```python
class Dog:
    """A simple Dog class."""
    
    # Class attribute (shared by all instances)
    species = "Canis familiaris"
    
    # Constructor — called when creating a new instance
    def __init__(self, name, age):
        self.name = name  # Instance attribute
        self.age = age
    
    # Instance method
    def bark(self):
        return f"{self.name} says Woof!"
    
    def get_info(self):
        return f"{self.name} is {self.age} years old"

# Creating objects
buddy = Dog("Buddy", 3)
max_dog = Dog("Max", 5)

print(buddy.name)         # Buddy
print(buddy.species)      # Canis familiaris
print(buddy.bark())       # Buddy says Woof!
print(max_dog.get_info()) # Max is 5 years old

# Class attribute is shared
print(Dog.species)        # Canis familiaris
print(buddy.species)      # Canis familiaris

# Modifying class attribute affects all
Dog.species = "Canis lupus"
print(buddy.species)      # Canis lupus
```

---

## 8.2 Instance vs Class vs Static Methods

```python
class MathUtils:
    # Class attribute
    pi = 3.14159
    
    def __init__(self, name):
        self.name = name
    
    # Instance method — has access to self (instance)
    def greet(self):
        return f"Hello from {self.name}"
    
    # Class method — has access to cls (class)
    @classmethod
    def from_string(cls, data):
        name, _ = data.split(",")
        return cls(name)  # Creates instance
    
    # Class method to access/modify class state
    @classmethod
    def get_pi(cls):
        return cls.pi
    
    # Static method — no access to self or cls
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def validate_positive(value):
        return value > 0

# Usage
m = MathUtils("Calc")
print(m.greet())  # Hello from Calc

m2 = MathUtils.from_string("Advanced, v2")
print(m2.name)  # Advanced

print(MathUtils.get_pi())       # 3.14159
print(MathUtils.add(5, 3))      # 8
print(MathUtils.validate_positive(-5))  # False
```

---

## 8.3 Inheritance

```python
# Base class
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        raise NotImplementedError("Subclass must implement")
    
    def move(self):
        return f"{self.name} moves"

# Derived classes
class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

class Duck(Animal):
    def speak(self):
        return f"{self.name} says Quack!"

# Polymorphism
def make_sound(animal):
    print(animal.speak())

animals = [Dog("Buddy"), Cat("Whiskers"), Duck("Donald")]
for a in animals:
    make_sound(a)
# Buddy says Woof!
# Whiskers says Meow!
# Donald says Quack!
```

### The `super()` Function

```python
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
    
    def start(self):
        return f"{self.brand} {self.model} engine starting..."

class Car(Vehicle):
    def __init__(self, brand, model, doors):
        super().__init__(brand, model)  # Call parent constructor
        self.doors = doors
    
    def start(self):
        parent_start = super().start()
        return f"{parent_start} Doors: {self.doors}"

car = Car("Toyota", "Camry", 4)
print(car.start())  # Toyota Camry engine starting... Doors: 4
```

### Multiple Inheritance

```python
class Flyer:
    def fly(self):
        return "Flying..."

class Swimmer:
    def swim(self):
        return "Swimming..."

class Duck(Animal, Flyer, Swimmer):
    def speak(self):
        return "Quack!"

# MRO — Method Resolution Order
print(Duck.__mro__)
# (<class 'Duck'>, <class 'Animal'>, <class 'Flyer'>, <class 'Swimmer'>, <class 'object'>)
```

### Method Resolution Order (MRO)

```python
class A:
    def method(self):
        return "A"

class B(A):
    def method(self):
        return "B"

class C(A):
    def method(self):
        return "C"

class D(B, C):
    pass

print(D().method())  # "B" — follows D -> B -> C -> A order
print(D.__mro__)
```

---

## 8.4 Encapsulation and Name Mangling

Python uses naming conventions for access control (no true private members):

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner          # Public
        self._balance = balance     # Protected (convention: _prefix)
        self.__pin = "1234"         # Private (name mangling: _ClassName__attr)
    
    # Public method — the interface
    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount
            return True
        return False
    
    def get_balance(self):
        return self._balance
    
    # Property decorator for controlled access
    @property
    def balance(self):
        return self._balance

account = BankAccount("Alice", 1000)
print(account.owner)       # Alice (public)
print(account._balance)    # 1000 (accessible but "protected")
# print(account.__pin)     # AttributeError!
print(account._BankAccount__pin)  # '1234' (name mangled access)
```

---

## 8.5 Properties

Properties provide controlled access with attribute-like syntax:

```python
class Temperature:
    def __init__(self, celsius=0):
        self._celsius = celsius
    
    @property
    def celsius(self):
        """Getter — called as temp.celsius"""
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        """Setter — called as temp.celsius = 100"""
        if value < -273.15:
            raise ValueError("Below absolute zero!")
        self._celsius = value
    
    @celsius.deleter
    def celsius(self):
        """Deleter — called as del temp.celsius"""
        print("Deleting temperature...")
        del self._celsius
    
    @property
    def fahrenheit(self):
        """Computed property (no setter → read-only)"""
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self._celsius = (value - 32) * 5/9

t = Temperature(100)
print(t.celsius)              # 100 (getter)
print(t.fahrenheit)           # 212.0 (computed)

t.celsius = 0                 # setter
print(t.fahrenheit)           # 32.0

t.fahrenheit = 98.6           # fahrenheit setter
print(t.celsius)              # 37.0...

# t.celsius = -300            # ValueError!
```

---

## 8.6 Magic (Dunder) Methods

Special methods surrounded by double underscores:

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    # String representation
    def __str__(self):
        return f"'{self.title}' by {self.author}"
    
    # Developer representation (debugging)
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    # Equality
    def __eq__(self, other):
        if not isinstance(other, Book):
            return NotImplemented
        return self.title == other.title and self.author == other.author
    
    # Less-than (for sorting)
    def __lt__(self, other):
        if not isinstance(other, Book):
            return NotImplemented
        return self.pages < other.pages
    
    # Length
    def __len__(self):
        return self.pages
    
    # Callable
    def __call__(self):
        return f"Reading {self.title}..."
    
    # Iterator
    def __iter__(self):
        self._index = 0
        return self
    
    def __next__(self):
        chapters = ["Ch1", "Ch2", "Ch3"]
        if self._index >= len(chapters):
            raise StopIteration
        result = chapters[self._index]
        self._index += 1
        return result

book1 = Book("1984", "Orwell", 328)
book2 = Book("1984", "Orwell", 328)
book3 = Book("Brave New World", "Huxley", 311)

print(str(book1))   # '1984' by Orwell
print(repr(book1))  # Book('1984', 'Orwell', 328)
print(book1 == book2)  # True (uses __eq__)
print(len(book1))      # 328 (uses __len__)
print(book1())         # Reading 1984... (uses __call__)

books = [book1, book3]
print(sorted(books))  # Sorted by pages (uses __lt__)

for chapter in book1:
    print(chapter)
```

### Common Magic Methods

| Category | Methods |
|----------|---------|
| **Creation** | `__new__`, `__init__`, `__del__` |
| **String** | `__str__`, `__repr__`, `__format__` |
| **Comparison** | `__eq__`, `__ne__`, `__lt__`, `__le__`, `__gt__`, `__ge__` |
| **Arithmetic** | `__add__`, `__sub__`, `__mul__`, `__truediv__`, `__floordiv__`, `__mod__` |
| **Container** | `__len__`, `__getitem__`, `__setitem__`, `__delitem__`, `__contains__` |
| **Iteration** | `__iter__`, `__next__` |
| **Callable** | `__call__` |
| **Context** | `__enter__`, `__exit__` |

---

## 8.7 Abstract Base Classes

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass
    
    def description(self):
        return f"Area: {self.area()}, Perimeter: {self.perimeter()}"

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius ** 2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

# shape = Shape()  # TypeError! Can't instantiate abstract class
circle = Circle(5)
rect = Rectangle(4, 6)
print(circle.description())  # Area: 78.5..., Perimeter: 31.4...
```

---

## Key Takeaways

- Classes define blueprints; objects are instances
- `@classmethod` has access to class, `@staticmethod` has no access to class/instance
- `super()` calls parent class methods
- Properties (`@property`) provide controlled attribute access
- Magic methods (`__str__`, `__eq__`, `__len__`, etc.) customize behavior
- Name mangling (`__attr`) for pseudo-private attributes
- ABCs (`abc.ABC`) enforce interface contracts
- Composition over inheritance — prefer "has-a" over "is-a"

---

## Exercises

1. **Bank system**: Create `BankAccount`, `SavingsAccount`, `CheckingAccount` with inheritance
2. **Library system**: Create `Book`, `Library`, `Member` classes with borrowing functionality
3. **Vector class**: Implement a 2D Vector with `__add__`, `__sub__`, `__mul__`, `__eq__`, `__repr__`
4. **Property validator**: Create a `Person` class with `name`, `age` properties that validate
5. **Custom iterator**: Create an `EvenNumbers` class that iterates through even numbers up to N
6. **Singleton**: Implement a Singleton pattern using `__new__`
7. **Shape hierarchy**: Create abstract `Shape` with `Circle`, `Rectangle`, `Triangle`

---

## Next Steps

→ Continue to [Chapter 9: Advanced Python — Decorators, Generators, Context Managers]({{< relref "09-advanced-python-decorators-generators" >}})
