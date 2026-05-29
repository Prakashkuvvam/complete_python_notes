---
title: "Ch 4: Functions & Modules"
weight: 4
---

# Functions & Modules

## Learning Objectives

After reading this chapter, you will be able to:
- Define and call functions in Python
- Understand parameters, arguments, and return values
- Use positional, keyword, default, and variable-length arguments
- Create lambda (anonymous) functions
- Organize code into modules and packages
- Write proper docstrings and follow naming conventions

---

## 4.1 Defining Functions

Functions are reusable blocks of code defined with the `def` keyword:

```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Hello, Alice!
```

### Function Syntax

```python
def function_name(parameters):
    """Optional docstring explaining the function."""
    # Function body
    return value  # Optional
```

### Simple Examples

```python
def add(a, b):
    return a + b

def say_hello():
    print("Hello!")

def get_pi():
    return 3.14159

print(add(5, 3))    # 8
say_hello()          # Hello!
print(get_pi())     # 3.14159
```

---

## 4.2 Parameters and Arguments

### Positional Arguments

```python
def describe_person(name, age, city):
    return f"{name} is {age} years old and lives in {city}"

# Positional — order matters
print(describe_person("Alice", 30, "New York"))
```

### Keyword Arguments

```python
# Keyword — order doesn't matter
print(describe_person(city="London", name="Bob", age=25))

# Mixed — positional first, then keyword
def power(base, exponent):
    return base ** exponent

print(power(2, exponent=3))  # 8
```

### Default Parameters

```python
def greet(name, greeting="Hello", punctuation="!"):
    return f"{greeting}, {name}{punctuation}"

print(greet("Alice"))              # Hello, Alice!
print(greet("Bob", "Hi"))          # Hi, Bob!
print(greet("Charlie", "Hey", "."))  # Hey, Charlie.
```

### Mutable Default Arguments — Pitfall

```python
# BAD — mutable default is shared across calls
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(1))  # [1]
print(add_item(2))  # [1, 2] — Not expected!

# GOOD — use None and create new list
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

print(add_item(1))  # [1]
print(add_item(2))  # [2]
```

---

## 4.3 Variable-Length Arguments

### `*args` — Variable Positional Arguments

```python
def sum_all(*args):
    """Sum any number of arguments."""
    return sum(args)

print(sum_all(1, 2, 3, 4, 5))  # 15
print(sum_all(10, 20))          # 30

# *args is a tuple inside the function
def log(*args):
    for i, arg in enumerate(args):
        print(f"Arg {i}: {arg}")
```

### `**kwargs` — Variable Keyword Arguments

```python
def build_profile(**kwargs):
    """Build a profile from keyword arguments."""
    return kwargs  # Returns a dict

profile = build_profile(name="Alice", age=30, city="NYC")
print(profile)  # {'name': 'Alice', 'age': 30, 'city': 'NYC'}

# Common pattern — passing through arguments
def create_user(name, **kwargs):
    user = {"name": name}
    user.update(kwargs)
    return user

user = create_user("Bob", age=25, role="admin", active=True)
print(user)  # {'name': 'Bob', 'age': 25, 'role': 'admin', 'active': True}
```

### Combined Parameters (Order Matters!)

```python
def example(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
    """
    pos1, pos2: Positional-only (before /)
    pos_or_kwd: Positional or keyword (between / and *)
    kwd1, kwd2: Keyword-only (after *)
    """
    pass

# / = positional-only separator
# * = keyword-only separator

def divide(a, b, /):
    """Positional-only — can't call divide(a=10, b=2)"""
    return a / b

def safe_divide(a, b, *, precision=2):
    """Keyword-only after *."""
    return round(a / b, precision)

print(divide(10, 3))                     # 3.333...
print(safe_divide(10, 3, precision=4))    # 3.3333
```

---

## 4.4 Return Values

```python
# Single return value
def square(x):
    return x * x

# Multiple values (returns a tuple)
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([3, 1, 4, 1, 5, 9])
print(low, high)  # 1 9

# Early return
def divide(a, b):
    if b == 0:
        return None  # Guard clause
    return a / b

# Return None implicitly
def no_return():
    pass

print(no_return())  # None
```

---

## 4.5 Scope and Namespace

### LEGB Rule (Local, Enclosing, Global, Built-in)

```python
x = "global"  # Global scope

def outer():
    x = "enclosing"  # Enclosing scope
    
    def inner():
        x = "local"  # Local scope
        print(f"inner: {x}")
    
    inner()
    print(f"outer: {x}")

outer()
print(f"global: {x}")
# inner: local
# outer: enclosing
# global: global
```

### `global` Keyword

```python
counter = 0

def increment():
    global counter
    counter += 1

increment()
increment()
print(counter)  # 2
```

### `nonlocal` Keyword

```python
def make_counter():
    count = 0
    
    def increment():
        nonlocal count  # Modify enclosing scope variable
        count += 1
        return count
    
    return increment

counter = make_counter()
print(counter())  # 1
print(counter())  # 2
print(counter())  # 3
```

---

## 4.6 Lambda Functions

Small anonymous functions defined in a single expression:

```python
# Syntax: lambda arguments: expression
square = lambda x: x ** 2
print(square(5))  # 25

# Typically used with map(), filter(), sorted()
numbers = [1, 4, 2, 7, 3, 9, 5]
even = list(filter(lambda x: x % 2 == 0, numbers))
print(even)  # [4, 2]

pairs = [(1, 'one'), (3, 'three'), (2, 'two'), (4, 'four')]
sorted_pairs = sorted(pairs, key=lambda pair: pair[1])
print(sorted_pairs)  # [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
```

---

## 4.7 Docstrings

```python
def calculate_bmi(weight: float, height: float) -> float:
    """
    Calculate Body Mass Index (BMI).
    
    Args:
        weight: Weight in kilograms
        height: Height in meters
    
    Returns:
        BMI value rounded to 2 decimal places
    
    Raises:
        ValueError: If weight or height is not positive
    """
    if weight <= 0 or height <= 0:
        raise ValueError("Weight and height must be positive")
    
    bmi = weight / (height ** 2)
    return round(bmi, 2)

# Access docstring
print(calculate_bmi.__doc__)
print(help(calculate_bmi))
```

---

## 4.8 Modules and Imports

### Creating a Module

```python
# File: math_utils.py

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

PI = 3.14159
```

### Importing Modules

```python
# Import entire module
import math_utils
print(math_utils.add(5, 3))  # 8
print(math_utils.PI)         # 3.14159

# Import specific items
from math_utils import add, PI
print(add(5, 3))  # 8

# Import with alias
import math_utils as mu
print(mu.subtract(10, 3))  # 7

# Import all (avoid — pollutes namespace)
from math_utils import *
```

### Module Search Path

```python
import sys

# Python looks for modules in these locations
for path in sys.path:
    print(path)
```

### `if __name__ == "__main__"`

```python
# File: calculator.py

def add(a, b): return a + b
def sub(a, b): return a - b

# This code only runs when executed directly, not when imported
if __name__ == "__main__":
    print("Testing calculator...")
    assert add(2, 3) == 5
    assert sub(5, 3) == 2
    print("All tests passed!")
```

---

## 4.9 Packages

A package is a directory with an `__init__.py` file:

```
my_package/
    __init__.py
    module1.py
    module2.py
    sub_package/
        __init__.py
        module3.py
```

```python
# __init__.py — can be empty or run initialization code
# It's executed when the package is imported

# Import the package
import my_package
from my_package import module1
from my_package.sub_package import module3
```

---

## Key Takeaways

- Functions are defined with `def` and can return values with `return`
- Parameters can be positional, keyword, default, `*args`, or `**kwargs`
- Use `global` and `nonlocal` to modify enclosing scope variables
- Lambda functions are concise single-expression functions
- Modules organize related functions; packages organize modules
- Always include docstrings for non-trivial functions
- Use `if __name__ == "__main__"` for runnable scripts

---

## Exercises

1. **Calculator**: Create functions for add, subtract, multiply, divide with proper error handling
2. **Factorial**: Write both recursive and iterative factorial functions
3. **Decorator**: Write a function that accepts any args and logs them before execution
4. **Module**: Create a `string_utils.py` module with `reverse()`, `count_vowels()`, `is_palindrome()`
5. **Lambda + sort**: Sort a list of strings by their last character using a lambda
6. **Varargs**: Write a function `create_dict(**kwargs)` that returns a dict sorted by keys

---

## Next Steps

→ Continue to [Chapter 5: Data Structures — Lists, Tuples, Dictionaries & Sets]({{< relref "05-data-structures-lists-tuples-dicts-sets" >}})
