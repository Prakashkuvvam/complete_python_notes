---
title: "Ch 10: The Python Standard Library"
weight: 10
---

# The Python Standard Library

## Learning Objectives

After reading this chapter, you will be able to:
- Navigate and use Python's extensive standard library
- Work with common modules like `math`, `datetime`, `random`, `os`, `sys`
- Use `collections` for advanced data structures
- Use `itertools` for iterator manipulation
- Understand `typing` for type hints
- Work with `functools`, `re`, `json`, `csv`, `hashlib`

---

## 10.1 `math` — Mathematical Functions

```python
import math

# Constants
print(math.pi)       # 3.141592653589793
print(math.e)        # 2.718281828459045
print(math.inf)      # inf
print(math.nan)      # nan

# Rounding
print(math.ceil(3.2))    # 4
print(math.floor(3.8))   # 3
print(math.trunc(3.8))   # 3
print(round(3.5))        # 4 (built-in, bankers rounding)

# Powers and roots
print(math.sqrt(16))     # 4.0
print(math.pow(2, 10))   # 1024.0
print(math.exp(2))       # e² = 7.389...
print(math.log(100, 10)) # 2.0
print(math.log2(1024))   # 10.0

# Trigonometry
print(math.sin(math.pi/2))  # 1.0
print(math.cos(0))         # 1.0
print(math.degrees(math.pi))  # 180.0
print(math.radians(180))      # 3.1415...

# Combinatorial
print(math.factorial(5))  # 120
print(math.comb(5, 2))    # 10 (combinations)
print(math.perm(5, 2))    # 20 (permutations)

# GCD and LCM
print(math.gcd(48, 18))   # 6
print(math.lcm(4, 6))     # 12 (Python 3.9+)
```

---

## 10.2 `datetime` — Date and Time

```python
from datetime import date, time, datetime, timedelta, timezone

# Current date and time
now = datetime.now()
today = date.today()
print(now)   # 2026-05-29 10:30:45.123456
print(today) # 2026-05-29

# Creating specific dates
d = date(2025, 12, 25)
t = time(14, 30, 0)
dt = datetime(2025, 12, 25, 14, 30, 0)

# Accessing components
print(dt.year)   # 2025
print(dt.month)  # 12
print(dt.day)    # 25
print(dt.hour)   # 14

# Formatting
print(dt.strftime("%Y-%m-%d %H:%M:%S"))  # 2025-12-25 14:30:00
print(dt.strftime("%A, %B %d, %Y"))      # Thursday, December 25, 2025

# Parsing
parsed = datetime.strptime("2025-01-15", "%Y-%m-%d")
print(parsed)  # 2025-01-15 00:00:00

# Date arithmetic
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
one_hour = now + timedelta(hours=1)

# Difference between dates
future = datetime(2026, 1, 1)
delta = future - now
print(delta.days)       # Number of days
print(delta.total_seconds())  # Total seconds

# Time zones
from zoneinfo import ZoneInfo  # Python 3.9+
tz_ny = ZoneInfo("America/New_York")
tz_ldn = ZoneInfo("Europe/London")

utc_time = datetime.now(timezone.utc)
ny_time = utc_time.astimezone(tz_ny)
print(ny_time)
```

---

## 10.3 `random` — Random Numbers

```python
import random

# Basic random
print(random.random())       # 0.0 <= x < 1.0
print(random.randint(1, 6))  # Random integer between 1 and 6 (inclusive)
print(random.uniform(1, 10)) # Random float between 1 and 10

# Choices
fruits = ["apple", "banana", "cherry", "date"]
print(random.choice(fruits))          # Random element
print(random.choices(fruits, k=3))    # 3 elements with replacement
print(random.sample(fruits, k=2))     # 2 unique elements

# Shuffle
random.shuffle(fruits)  # In-place shuffle
print(fruits)

# Seed for reproducibility
random.seed(42)
print(random.randint(1, 100))  # Always 82
random.seed(42)
print(random.randint(1, 100))  # Always 82

# Gaussian distribution
print(random.gauss(0, 1))  # Mean=0, StdDev=1
```

---

## 10.4 `os` and `sys` — System Operations

### `os` Module

```python
import os

# Current directory
print(os.getcwd())  # Current working directory

# List directory
print(os.listdir("."))  # List files in current dir

# Create/remove directories
os.makedirs("a/b/c", exist_ok=True)  # Create nested dirs
os.rmdir("a")  # Remove single directory

# File operations
os.rename("old.txt", "new.txt")
os.remove("file.txt")  # Delete file

# Path operations (use pathlib instead for new code)
print(os.path.join("dir", "file.txt"))
print(os.path.exists("file.txt"))
print(os.path.isfile("file.txt"))

# Environment variables
print(os.environ.get("HOME"))
os.environ["MY_VAR"] = "value"

# Process
print(os.getpid())      # Process ID
print(os.cpu_count())   # Number of CPUs
```

### `sys` Module

```python
import sys

# Command line arguments
print(sys.argv)  # ['script.py', 'arg1', 'arg2']

# Python version
print(sys.version)       # '3.12.0 (main, ...)'
print(sys.version_info)  # sys.version_info(major=3, minor=12, micro=0)

# Module search path
for path in sys.path:
    print(path)

# Exit program
# sys.exit(1)  # Exit with status code

# Standard streams
sys.stdout.write("Hello\n")  # Like print
sys.stderr.write("Error!\n")  # Error output

# Memory size (for debugging)
print(sys.getsizeof([]))       # 56 bytes
print(sys.getsizeof([1,2,3]))  # 88 bytes

# Recursion limit
print(sys.getrecursionlimit())  # Usually 1000
# sys.setrecursionlimit(2000)
```

---

## 10.5 `collections` — Specialized Data Structures

```python
from collections import Counter, defaultdict, deque, OrderedDict, namedtuple

# Counter — count elements
colors = ["red", "blue", "red", "green", "blue", "blue"]
count = Counter(colors)
print(count)          # Counter({'blue': 3, 'red': 2, 'green': 1})
print(count.most_common(2))  # [('blue', 3), ('red', 2)]

# defaultdict — default values for missing keys
word_map = defaultdict(list)
words = ["hello", "world", "python", "hello"]
for word in words:
    word_map[word[0]].append(word)
print(dict(word_map))  # {'h': ['hello', 'hello'], 'w': ['world'], 'p': ['python']}

# deque — double-ended queue
queue = deque([1, 2, 3])
queue.append(4)       # [1, 2, 3, 4]
queue.appendleft(0)   # [0, 1, 2, 3, 4]
print(queue.popleft())   # 0
print(queue.pop())       # 4
queue.rotate(1)          # [4, 1, 2, 3]

# namedtuple — lightweight data objects
Point = namedtuple("Point", ["x", "y"])
p = Point(3, 4)
print(p.x, p.y)        # 3 4
print(p[0], p[1])      # 3 4 (indexable)
x, y = p               # Unpackable

# OrderedDict (Python <3.7 — now regular dicts remember insertion order)
od = OrderedDict()
od["a"] = 1
od["b"] = 2
print(list(od.keys()))  # ['a', 'b']
```

---

## 10.6 `itertools` — Iterator Tools

```python
from itertools import count, cycle, repeat, chain, product, permutations
from itertools import combinations, groupby, islice, accumulate

# Infinite iterators
for i in islice(count(10), 5):  # count(start=10)
    print(i)  # 10, 11, 12, 13, 14

for item in islice(cycle([1, 2, 3]), 7):  # cycle
    print(item)  # 1, 2, 3, 1, 2, 3, 1

for item in islice(repeat("A", 3), 5):  # repeat
    print(item)  # A, A, A (limited to 3)

# Chain iterables
print(list(chain([1, 2], [3, 4], [5, 6])))  # [1, 2, 3, 4, 5, 6]

# Cartesian product
print(list(product([1, 2], ["a", "b"])))
# [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]

# Permutations and combinations
print(list(permutations([1, 2, 3], 2)))
# [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]

print(list(combinations([1, 2, 3], 2)))
# [(1, 2), (1, 3), (2, 3)]

# Group by
items = [("fruit", "apple"), ("fruit", "banana"), ("veggie", "carrot")]
for key, group in groupby(items, key=lambda x: x[0]):
    print(key, list(group))
# fruit [('fruit', 'apple'), ('fruit', 'banana')]
# veggie [('veggie', 'carrot')]

# Accumulate
print(list(accumulate([1, 2, 3, 4, 5])))  # [1, 3, 6, 10, 15]
print(list(accumulate([1, 2, 3, 4], lambda a, b: a * b)))  # [1, 2, 6, 24]
```

---

## 10.7 `functools` — Higher-Order Functions

```python
import functools

# lru_cache — memoization
@functools.lru_cache(maxsize=128)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(50))  # 12586269025 (fast with caching!)
print(fibonacci.cache_info())  # Cache hits/misses

# partial — fix function arguments
import math

def power(base, exponent):
    return base ** exponent

square = functools.partial(power, exponent=2)
cube = functools.partial(power, exponent=3)

print(square(5))  # 25
print(cube(3))    # 27

# reduce — apply function cumulatively
numbers = [1, 2, 3, 4, 5]
product = functools.reduce(lambda a, b: a * b, numbers)
print(product)  # 120

# singledispatch — function overloading
from functools import singledispatch

@singledispatch
def process(value):
    raise NotImplementedError(f"Cannot process {type(value)}")

@process.register(int)
def _(value):
    return f"Processing integer: {value ** 2}"

@process.register(str)
def _(value):
    return f"Processing string: {value.upper()}"

@process.register(list)
def _(value):
    return f"Processing list with {len(value)} items"

print(process(5))       # Processing integer: 25
print(process("hello"))  # Processing string: HELLO
```

---

## 10.8 Other Essential Modules

### `hashlib` — Hashing

```python
import hashlib

password = "secret123"

# SHA-256 hash
hash_obj = hashlib.sha256(password.encode())
print(hash_obj.hexdigest())
# f5e5c0b...

# MD5 (insecure, use for checksums only)
print(hashlib.md5(b"data").hexdigest())
```

### `uuid` — Unique IDs

```python
import uuid

print(uuid.uuid4())  # Random UUID: 550e8400-e29b-41d4-a716-446655440000
```

### `argparse` — Command Line Arguments

```python
import argparse

parser = argparse.ArgumentParser(description="Process some integers.")
parser.add_argument("numbers", nargs="+", type=int, help="Numbers to process")
parser.add_argument("--sum", action="store_true", help="Sum the numbers")
parser.add_argument("--output", "-o", help="Output file")

args = parser.parse_args()
if args.sum:
    print(sum(args.numbers))
```

### `logging` — Logging

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s"
)

logger = logging.getLogger(__name__)
logger.debug("Detailed debug info")
logger.info("Program started")
logger.warning("Low disk space")
logger.error("An error occurred")
logger.critical("System failure")
```

---

## Key Takeaways

- Python's standard library is vast — "batteries included"
- `collections` provides `Counter`, `defaultdict`, `deque`, `namedtuple`
- `itertools` offers powerful iterator manipulation tools
- `functools` gives `lru_cache`, `partial`, `reduce`, `singledispatch`
- `datetime`, `math`, `random`, `os`, `sys` are daily drivers
- Use `hashlib` for hashing, `uuid` for IDs, `argparse` for CLI args
- Use `logging` instead of `print` for production applications
- Check the standard library first before installing third-party packages

---

## Exercises

1. **Data analysis**: Use `Counter` to find the most common words in a text
2. **Date arithmetic**: Calculate your exact age in years, months, days, hours, minutes
3. **Permutations**: Generate all permutations of a string's characters
4. **Memoization**: Use `@lru_cache` to speed up a recursive function
5. **CLI tool**: Build a simple CLI using `argparse` that processes files
6. **Logging**: Set up logging for a multi-module project
7. **Deque**: Implement a sliding window algorithm using `deque`

---

## Next Steps

→ Continue to [Chapter 11: Testing with Python]({{< relref "11-testing-with-python" >}})
