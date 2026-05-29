---
title: "Ch 9: Advanced Python — Decorators, Generators, Context Managers"
weight: 9
---

# Advanced Python — Decorators, Generators, Context Managers

## Learning Objectives

After reading this chapter, you will be able to:
- Create and use decorators for function enhancement
- Write generators for memory-efficient iteration
- Build custom context managers
- Understand closures and first-class functions
- Use `functools` utilities for advanced function behavior
- Master iterators and the iteration protocol

---

## 9.1 First-Class Functions and Closures

### Functions as First-Class Citizens

```python
def square(x):
    return x ** 2

# Assign to variable
f = square
print(f(5))  # 25

# Pass as argument
def apply(func, value):
    return func(value)

print(apply(square, 5))  # 25

# Return from function
def get_operation(op):
    if op == "square":
        return lambda x: x ** 2
    elif op == "cube":
        return lambda x: x ** 3

op = get_operation("cube")
print(op(3))  # 27
```

### Closures

A closure remembers variables from the enclosing scope:

```python
def make_multiplier(n):
    def multiplier(x):
        return x * n  # n is "captured" from outer scope
    return multiplier

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))  # 10
print(triple(5))  # 15

# Practical example — counter
def create_counter():
    count = 0
    def counter():
        nonlocal count
        count += 1
        return count
    return counter

counter_a = create_counter()
print(counter_a())  # 1
print(counter_a())  # 2
```

---

## 9.2 Decorators

A decorator is a function that wraps another function to extend its behavior.

### Basic Decorator

```python
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

# Equivalent to: say_hello = my_decorator(say_hello)

say_hello()
# Before function call
# Hello!
# After function call
```

### Decorator with Arguments

```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
# Hello, Alice!
# Hello, Alice!
# Hello, Alice!
```

### Preserving Function Metadata

```python
import functools

def my_decorator(func):
    @functools.wraps(func)  # Preserves func's metadata
    def wrapper(*args, **kwargs):
        """Wrapper docstring"""
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(a, b):
    """Add two numbers."""
    return a + b

print(add.__name__)  # 'add' (without @wraps, would be 'wrapper')
print(add.__doc__)   # 'Add two numbers.' (without @wraps, would be 'Wrapper docstring')
```

### Practical Decorator Examples

```python
import functools
import time

# Timing decorator
def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done"

# Logging decorator
def logger(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        args_repr = [repr(a) for a in args]
        kwargs_repr = [f"{k}={v!r}" for k, v in kwargs.items()]
        signature = ", ".join(args_repr + kwargs_repr)
        print(f"Calling {func.__name__}({signature})")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result!r}")
        return result
    return wrapper

@logger
def add(a, b):
    return a + b

add(3, 5)
# Calling add(3, 5)
# add returned 8

# Retry decorator
def retry(max_attempts=3, delay=1):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"Attempt {attempt} failed: {e}")
                    if attempt == max_attempts:
                        raise
                    time.sleep(delay)
        return wrapper
    return decorator

@retry(max_attempts=3, delay=0.5)
def unstable_network_call():
    import random
    if random.random() < 0.7:
        raise ConnectionError("Network timeout")
    return "Success!"
```

### Decorators on Class Methods

```python
def require_authentication(func):
    @functools.wraps(func)
    def wrapper(self, *args, **kwargs):
        if not self.is_authenticated:
            raise PermissionError("Authentication required")
        return func(self, *args, **kwargs)
    return wrapper

class API:
    def __init__(self):
        self.is_authenticated = False
    
    def login(self, password):
        if password == "secret":
            self.is_authenticated = True
    
    @require_authentication
    def get_data(self):
        return "Sensitive data"
```

### Class-Based Decorators

```python
class CountCalls:
    def __init__(self, func):
        functools.update_wrapper(self, func)
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Call {self.count} of {self.func.__name__}")
        return self.func(*args, **kwargs)

@CountCalls
def say_hello():
    print("Hello!")

say_hello()  # Call 1 of say_hello
say_hello()  # Call 2 of say_hello
print(say_hello.count)  # 2
```

---

## 9.3 Generators

Generators produce values lazily (one at a time), saving memory.

### Generator Functions

```python
def count_up_to(n):
    i = 1
    while i <= n:
        yield i  # Yields a value, pauses execution
        i += 1

# Returns a generator object
counter = count_up_to(5)
print(counter)  # <generator object at 0x...>

for num in counter:
    print(num)  # 1, 2, 3, 4, 5

# Manual iteration
gen = count_up_to(3)
print(next(gen))  # 1
print(next(gen))  # 2
print(next(gen))  # 3
# print(next(gen))  # StopIteration
```

### Generator vs List Comparison

```python
def squares_list(n):
    result = []
    for i in range(n):
        result.append(i ** 2)
    return result

def squares_generator(n):
    for i in range(n):
        yield i ** 2

# List — all in memory at once
big_list = squares_list(1000000)  # ~8MB for ints

# Generator — produces one at a time
big_gen = squares_generator(1000000)  # Negligible memory

# Memory efficient sum
print(sum(squares_generator(10000)))
```

### Generator Expressions

```python
# Generator expression (parentheses)
squares = (x ** 2 for x in range(10))
print(type(squares))  # <class 'generator'>

# Converting to list
squares_list = list(squares)

# Using in functions
print(sum(x ** 2 for x in range(10)))  # 285
print(max(len(word) for word in ["hello", "world", "python"]))  # 6
```

### The `yield from` Syntax

```python
def flatten(nested):
    for sublist in nested:
        yield from sublist  # Delegate to sub-iterable

nested = [[1, 2], [3, 4], [5, 6]]
flat = list(flatten(nested))
print(flat)  # [1, 2, 3, 4, 5, 6]

# Recursive flattener
def deep_flatten(nested):
    for item in nested:
        if isinstance(item, (list, tuple)):
            yield from deep_flatten(item)
        else:
            yield item

print(list(deep_flatten([1, [2, [3, 4]], 5])))  # [1, 2, 3, 4, 5]
```

### Infinite Generators

```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# Take first 10
fib = fibonacci()
first_10 = [next(fib) for _ in range(10)]
print(first_10)  # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

# Using itertools.islice
from itertools import islice
next_10 = list(islice(fibonacci(), 10, 20))
print(next_10)  # [55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181]
```

---

## 9.4 Iterators and Iterables

```python
# Every generator is an iterator
# But we can create custom iterators

class CountDown:
    def __init__(self, start):
        self.start = start
    
    def __iter__(self):
        # Return an iterator (usually self)
        self.current = self.start
        return self
    
    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        value = self.current
        self.current -= 1
        return value

# CountDown is both iterable (__iter__) and iterator (__next__)
for n in CountDown(5):
    print(n)  # 5, 4, 3, 2, 1
```

---

## 9.5 Context Managers

### Creating with `contextlib`

```python
from contextlib import contextmanager

@contextmanager
def temporary_change(file_path, new_content):
    """Context manager that modifies a file and restores it."""
    import shutil, tempfile
    
    # Save original content
    try:
        with open(file_path) as f:
            original = f.read()
    except FileNotFoundError:
        original = None
    
    # Write new content
    with open(file_path, "w") as f:
        f.write(new_content)
    
    try:
        yield  # Code inside the `with` block runs here
    finally:
        # Restore original
        if original is not None:
            with open(file_path, "w") as f:
                f.write(original)
        else:
            import os
            os.remove(file_path)

@contextmanager
def timed(name="block"):
    start = time.perf_counter()
    try:
        yield
    finally:
        end = time.perf_counter()
        print(f"{name} took {end - start:.4f}s")

# Usage
with timed("Data processing"):
    result = sum(x ** 2 for x in range(1000000))
```

---

## Key Takeaways

- **Decorators** wrap functions to add behavior (timing, logging, auth)
- Always use `@functools.wraps` to preserve metadata
- **Generators** use `yield` for lazy, memory-efficient iteration
- **Generator expressions** are like list comprehensions but lazy
- `yield from` delegates to a sub-generator
- **Context managers** use `__enter__`/`__exit__` or `@contextmanager`
- **Closures** capture variables from the enclosing scope
- The iteration protocol requires `__iter__` and `__next__`

---

## Exercises

1. **Timer decorator**: Create a decorator that measures and prints function execution time
2. **Cache decorator**: Implement an LRU cache decorator (like `@functools.lru_cache`)
3. **Fibonacci generator**: Write a generator that yields Fibonacci numbers indefinitely
4. **Chunk reader**: Create a generator that reads a large file in chunks
5. **Toggle context**: Create a context manager that temporarily changes a global setting
6. **Rate limiter**: Write a decorator that limits function calls to N per second
7. **Pipeline**: Chain multiple generators for a data processing pipeline

---

## Next Steps

→ Continue to [Chapter 10: The Python Standard Library]({{< relref "10-python-standard-library" >}})
