---
title: "Ch 17: Interview Questions & Answers"
weight: 17
---

# Interview Questions & Answers

## Learning Objectives

After reading this chapter, you will be able to:
- Answer common Python interview questions with confidence
- Understand the reasoning behind each answer
- Demonstrate best practices and Pythonic thinking
- Handle both theoretical and coding questions

---

## 17.1 Python Fundamentals

### Q1: What is the difference between a list and a tuple?

**Answer:**
- **List**: Mutable (`[]`), slower, supports item assignment
- **Tuple**: Immutable (`()`), faster, hashable (can be dict key)

```python
# List — modifiable
lst = [1, 2, 3]
lst[0] = 10  # OK

# Tuple — fixed
tpl = (1, 2, 3)
# tpl[0] = 10  # TypeError!

# Tuple as dict key (hashable)
d = {(1, 2): "point"}  # OK
# d = {[1, 2]: "point"}  # TypeError!
```

### Q2: Explain Python's `__init__` and `__new__` methods.

**Answer:**
- `__new__` creates the instance (called first, returns the new object)
- `__init__` initializes the instance (called after, returns None)
- `__new__` is rarely overridden unless implementing singletons or metaclasses

```python
class Singleton:
    _instance = None
    
    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
    
    def __init__(self, value):
        self.value = value
```

### Q3: What is the difference between `is` and `==`?

**Answer:**
- `==` checks **value equality** (are values the same?)
- `is` checks **identity equality** (are they the same object in memory?)

```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)  # True (same values)
print(a is b)  # False (different objects)

# Small integers are cached (-5 to 256)
x = 256
y = 256
print(x is y)  # True (cached)

x = 257
y = 257
print(x is y)  # False (not cached)

# Always use "is" for None comparison
if result is None:
    print("No result")
```

### Q4: How does Python manage memory?

**Answer:**
- Python uses **reference counting** and a **garbage collector**
- Objects are freed when their reference count reaches zero
- The GC handles circular references (cycles)
- `gc` module provides manual control

```python
import sys
import gc

x = []
print(sys.getrefcount(x))  # 2 (x + argument)

y = x
print(sys.getrefcount(x))  # 3

del y  # Decrements ref count
print(sys.getrefcount(x))  # 2

# Force garbage collection
gc.collect()

# Disable GC (for performance-critical code)
gc.disable()
```

### Q5: What are decorators and how do they work?

**Answer:**
Decorators wrap functions to add behavior. They're syntactic sugar for `func = decorator(func)`.

```python
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.time()-start:.2f}s")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done"
```

---

## 17.2 Data Structures & Algorithms

### Q6: How do you reverse a linked list in Python?

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverse_list(head):
    prev = None
    current = head
    while current:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    return prev
```

### Q7: Find the first non-repeating character in a string.

```python
from collections import Counter

def first_non_repeating(s):
    counts = Counter(s)
    for i, char in enumerate(s):
        if counts[char] == 1:
            return i
    return -1
```

### Q8: Check if parentheses are balanced.

```python
def is_balanced(s):
    stack = []
    pairs = {")": "(", "]": "[", "}": "{"}
    for char in s:
        if char in "([{":
            stack.append(char)
        elif char in ")]}":
            if not stack or stack.pop() != pairs[char]:
                return False
    return len(stack) == 0
```

### Q9: Find all anagrams in a list of strings.

```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)
    for word in words:
        key = "".join(sorted(word))
        groups[key].append(word)
    return list(groups.values())
```

---

## 17.3 OOP & Design

### Q10: Explain inheritance vs composition.

**Answer:**
- **Inheritance**: "is-a" relationship (e.g., `Dog` is an `Animal`)
- **Composition**: "has-a" relationship (e.g., `Car` has an `Engine`)
- Favor composition over inheritance (more flexible, less coupling)

```python
# Inheritance (is-a)
class Animal:
    def breathe(self): ...

class Dog(Animal):
    def bark(self): ...

# Composition (has-a)
class Engine:
    def start(self): ...

class Car:
    def __init__(self):
        self.engine = Engine()  # Car has an Engine
    
    def start(self):
        self.engine.start()
```

### Q11: What is the MRO and how does it work?

**Answer:**
**MRO** (Method Resolution Order) determines which method is called in inheritance hierarchies. Python uses C3 linearization.

```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass

print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)
```

---

## 17.4 Advanced Topics

### Q12: What is the GIL and how does it affect threading?

**Answer:**
The **GIL** (Global Interpreter Lock) allows only one thread to execute Python bytecode at a time. This means:
- **CPU-bound tasks**: Threads don't help (use multiprocessing)
- **I/O-bound tasks**: Threads do help (GIL is released during I/O)

### Q13: How do `*args` and `**kwargs` work?

```python
def func(*args, **kwargs):
    print(f"Positional: {args}")   # Tuple
    print(f"Keyword: {kwargs}")     # Dict

func(1, 2, 3, a=4, b=5)
# Positional: (1, 2, 3)
# Keyword: {'a': 4, 'b': 5}

# Unpacking
items = [1, 2, 3]
d = {"a": 4, "b": 5}
func(*items, **d)
```

### Q14: Explain generators and the `yield` keyword.

```python
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci()
first_5 = [next(fib) for _ in range(5)]  # [0, 1, 1, 2, 3]
```

### Q15: What are context managers?

```python
# Using with statement
with open("file.txt") as f:
    content = f.read()

# Custom context manager using class
class ManagedFile:
    def __enter__(self):
        self.file = open("file.txt")
        return self.file
    def __exit__(self, *args):
        self.file.close()

# Using contextlib
from contextlib import contextmanager

@contextmanager
def managed_file(name):
    f = open(name)
    try:
        yield f
    finally:
        f.close()
```

---

## 17.5 Coding Problems

### Q16: Two Sum

```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

### Q17: Merge sorted arrays

```python
def merge_sorted(arr1, arr2):
    i = j = 0
    result = []
    while i < len(arr1) and j < len(arr2):
        if arr1[i] < arr2[j]:
            result.append(arr1[i])
            i += 1
        else:
            result.append(arr2[j])
            j += 1
    result.extend(arr1[i:])
    result.extend(arr2[j:])
    return result
```

### Q18: LRU Cache

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cache = OrderedDict()
        self.capacity = capacity
    
    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]
    
    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

---

## Key Takeaways

- Understand **data structures** (list, tuple, dict, set) and when to use each
- Know **decorators**, **generators**, and **context managers** inside out
- Practice **coding problems** (Two Sum, reverse linked list, LRU cache)
- Understand **GIL**, **MRO**, and memory management
- Write **Pythonic code** — use comprehensions, `with` statements, truthiness
- Be ready to explain **tradeoffs** between different approaches

---

## Next Steps

→ Continue to [Chapter 18: Real-World Scenarios & Coding Problems]({{< relref "18-real-world-scenarios-and-coding-problems" >}})
