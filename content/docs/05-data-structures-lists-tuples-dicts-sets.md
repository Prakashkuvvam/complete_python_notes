---
title: "Ch 5: Data Structures — Lists, Tuples, Dicts & Sets"
weight: 5
---

# Data Structures — Lists, Tuples, Dictionaries & Sets

## Learning Objectives

After reading this chapter, you will be able to:
- Create and manipulate lists with various methods
- Understand tuples and when to use them over lists
- Use dictionaries for key-value mappings
- Work with sets for unique collections and set operations
- Choose the right data structure for different scenarios
- Use advanced patterns like slicing, unpacking, and comprehensions

---

## 5.1 Lists

Lists are **ordered**, **mutable** sequences of elements.

### Creating Lists

```python
# Empty list
empty = []
empty = list()

# With elements
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True, None]
nested = [[1, 2], [3, 4], [5, 6]]

# From other iterables
chars = list("Python")  # ['P', 'y', 't', 'h', 'o', 'n']
range_list = list(range(5))  # [0, 1, 2, 3, 4]
```

### Accessing Elements

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

print(fruits[0])    # apple
print(fruits[-1])   # elderberry (negative indexing)
print(fruits[-2])   # date

# Slicing [start:stop:step]
print(fruits[1:3])     # ['banana', 'cherry']
print(fruits[:3])      # ['apple', 'banana', 'cherry']
print(fruits[::2])     # ['apple', 'cherry', 'elderberry']
print(fruits[::-1])    # ['elderberry', 'date', 'cherry', 'banana', 'apple']
```

### Modifying Lists

```python
fruits = ["apple", "banana", "cherry"]

# Modify by index
fruits[1] = "blueberry"
print(fruits)  # ['apple', 'blueberry', 'cherry']

# Append
fruits.append("date")
print(fruits)  # ['apple', 'blueberry', 'cherry', 'date']

# Insert at position
fruits.insert(1, "avocado")
print(fruits)  # ['apple', 'avocado', 'blueberry', 'cherry', 'date']

# Extend with another list
fruits.extend(["fig", "grape"])
print(fruits)  # ['apple', 'avocado', 'blueberry', 'cherry', 'date', 'fig', 'grape']

# Remove by value (first occurrence)
fruits.remove("avocado")

# Remove and return by index
removed = fruits.pop(2)  # Removes 'blueberry'
print(removed)  # blueberry

# Delete by index or slice
del fruits[0]       # Remove first element
del fruits[1:3]     # Remove slice

# Clear all elements
fruits.clear()
```

### List Methods

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]

# Sort in place
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]

# Sort descending
numbers.sort(reverse=True)

# Sorted returns new sorted list
unsorted = [3, 1, 4, 1, 5]
sorted_list = sorted(unsorted)
print(sorted_list)  # [1, 1, 3, 4, 5]

# Reverse in place
numbers.reverse()

# Count occurrences
print(numbers.count(5))  # 3

# Find index of first occurrence
print(numbers.index(4))  # 5 (after sorting)

# Copy
copy = numbers.copy()

# Length
print(len(numbers))  # 11

# Check membership
print(5 in numbers)   # True
print(99 in numbers)  # False
```

### List Operations

```python
# Concatenation
print([1, 2] + [3, 4])  # [1, 2, 3, 4]

# Repetition
print(["ha"] * 3)  # ['ha', 'ha', 'ha']

# Unpacking
first, second, *rest = [1, 2, 3, 4, 5]
print(first, second, rest)  # 1 2 [3, 4, 5]

first, *middle, last = [1, 2, 3, 4, 5]
print(first, middle, last)  # 1 [2, 3, 4] 5
```

---

## 5.2 Tuples

Tuples are **ordered**, **immutable** sequences.

```python
# Creating tuples
empty = ()
single = (1,)  # Trailing comma is required!
coords = (3, 4)
person = ("Alice", 30, "Engineer")

# Without parentheses (tuple packing)
point = 3, 4
print(type(point))  # <class 'tuple'>

# Accessing elements
a, b, c = person  # Unpacking
print(a)  # Alice
print(person[0])  # Alice
print(person[-1])  # Engineer

# Tuples are immutable
# person[0] = "Bob"  # TypeError!

# Tuple methods — only two!
numbers = (1, 2, 3, 2, 4, 2)
print(numbers.count(2))  # 3
print(numbers.index(3))  # 2

# Return multiple values (tuples)
def min_max(numbers):
    return min(numbers), max(numbers)

low, high = min_max([3, 1, 4, 1, 5])
print(low, high)  # 1 5
```

### When to Use Tuples vs Lists

| Use Case | Tuple | List |
|----------|-------|------|
| Fixed data (e.g., coordinates) | ✅ | ❌ |
| Dictionary keys | ✅ | ❌ |
| Heterogeneous data | ✅ | Sometimes |
| Need to modify | ❌ | ✅ |
| Large collections | ✅ (slightly more memory efficient) | ✅ |
| API design (prevent modification) | ✅ | ❌ |

---

## 5.3 Dictionaries

Dictionaries store **key-value pairs** with **unique keys**.

```python
# Creating dicts
empty = {}
person = {"name": "Alice", "age": 30, "city": "NYC"}

# Using dict() constructor
person = dict(name="Bob", age=25, role="admin")

# From pairs
pairs = dict([("a", 1), ("b", 2), ("c", 3)])

# Dict comprehension
squares = {x: x**2 for x in range(5)}
```

### Accessing and Modifying

```python
person = {"name": "Alice", "age": 30, "city": "NYC"}

# Access
print(person["name"])  # Alice
print(person.get("name"))  # Alice
print(person.get("phone", "N/A"))  # N/A (default)

# Safe access with get()
# print(person["phone"])  # KeyError!

# Membership
print("name" in person)   # True
print("phone" in person)  # False

# Modify/add
person["age"] = 31       # Update
person["phone"] = "555"  # Add new

# Remove
del person["phone"]
age = person.pop("age")  # Remove and return
last = person.popitem()    # Remove and return last inserted (Python 3.7+)
```

### Dictionary Methods

```python
person = {"name": "Alice", "age": 30, "city": "NYC"}

# All keys, values, items
print(person.keys())    # dict_keys(['name', 'age', 'city'])
print(person.values())  # dict_values(['Alice', 30, 'NYC'])
print(person.items())   # dict_items([('name', 'Alice'), ('age', 30), ('city', 'NYC')])

# Iteration
for key, value in person.items():
    print(f"{key}: {value}")

# Update with another dict
more = {"age": 31, "phone": "555-0123"}
person.update(more)
print(person)  # {'name': 'Alice', 'age': 31, 'city': 'NYC', 'phone': '555-0123'}

# Set default
person.setdefault("role", "user")  # Only sets if key doesn't exist

# Merge (Python 3.9+)
defaults = {"role": "user", "active": True}
merged = defaults | person  # Later keys override earlier ones

# Copy
copy = person.copy()
```

### Advanced Dictionary Patterns

```python
# defaultdict — automatic default values
from collections import defaultdict

# List defaultdict
word_groups = defaultdict(list)
words = ["apple", "banana", "apricot", "blueberry", "avocado"]
for word in words:
    word_groups[word[0]].append(word)

print(dict(word_groups))
# {'a': ['apple', 'apricot', 'avocado'], 'b': ['banana', 'blueberry']}

# Counter — count occurrences
from collections import Counter
text = "mississippi"
count = Counter(text)
print(count)  # Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
print(count.most_common(2))  # [('i', 4), ('s', 4)]

# OrderedDict (Python <3.7 — now regular dicts are ordered)
from collections import OrderedDict
```

---

## 5.4 Sets

Sets are **unordered** collections of **unique** elements.

```python
# Creating sets
empty = set()  # NOT {} — that's an empty dict!
numbers = {1, 2, 3, 4, 5}

# From iterable
unique = set([1, 2, 2, 3, 3, 3, 4])
print(unique)  # {1, 2, 3, 4}

chars = set("hello")
print(chars)  # {'h', 'e', 'l', 'o'} (l only appears once)
```

### Set Operations

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

# Union
print(a | b)  # {1, 2, 3, 4, 5, 6, 7, 8}
print(a.union(b))

# Intersection
print(a & b)  # {4, 5}
print(a.intersection(b))

# Difference (in a but not b)
print(a - b)  # {1, 2, 3}
print(a.difference(b))

# Symmetric difference (in a or b but not both)
print(a ^ b)  # {1, 2, 3, 6, 7, 8}
print(a.symmetric_difference(b))

# Subset/superset
print({1, 2}.issubset(a))    # True
print(a.issuperset({1, 2}))  # True

# Disjoint (no common elements)
print({1, 2}.isdisjoint({3, 4}))  # True
```

### Modifying Sets

```python
numbers = {1, 2, 3}

numbers.add(4)
print(numbers)  # {1, 2, 3, 4}

numbers.update([5, 6, 7])
print(numbers)  # {1, 2, 3, 4, 5, 6, 7}

numbers.remove(3)  # KeyError if not found
numbers.discard(10)  # No error if not found

removed = numbers.pop()  # Remove and return arbitrary element
print(removed)  # 1 (or any)

numbers.clear()  # Empty the set
```

### Frozenset — Immutable Set

```python
# Frozenset can be used as dictionary key or set element
fs = frozenset([1, 2, 3])
print(fs)  # frozenset({1, 2, 3})

# Supports all read-only set operations
print(fs | frozenset([3, 4, 5]))  # frozenset({1, 2, 3, 4, 5})
```

---

## 5.5 Choosing the Right Data Structure

| Need | Use |
|------|-----|
| Ordered, mutable collection | `List` |
| Ordered, immutable collection | `Tuple` |
| Fixed, heterogeneous data | `Tuple` (namedtuple for labels) |
| Key-value lookups | `Dict` |
| Unique elements | `Set` |
| Count elements | `Counter` (collections) |
| Queue | `deque` (collections) |
| Default values | `defaultdict` (collections) |
| Immutable mapping | `MappingProxyType` |

---

## Key Takeaways

- **Lists**: Ordered, mutable — use for sequences you'll modify
- **Tuples**: Ordered, immutable — use for fixed data, dict keys
- **Dicts**: Unordered (ordered in 3.7+), key-value mapping — fast lookups
- **Sets**: Unordered, unique — great for deduplication and set operations
- Use `get()` for safe dictionary access, `defaultdict` for grouping
- Prefer tuple unpacking for clean multiple returns
- Use `Counter` for counting, `set` for deduplication

---

## Exercises

1. **List operations**: Given `[1, 2, 3, 4, 5]`, reverse it in-place, slice it, find max/min
2. **Tuple unpacking**: Swap two variables without a temporary variable
3. **Word counter**: Count word frequencies in a string using a dictionary
4. **Set operations**: Find common elements, unique elements, and differences between two lists
5. **Group by**: Group a list of people by their age using `defaultdict`
6. **Shopping list**: Implement a shopping list with add/remove/view/search using lists
7. **Invert dict**: Write a function that swaps keys and values in a dictionary

---

## Next Steps

→ Continue to [Chapter 6: Strings & String Manipulation]({{< relref "06-strings-and-string-manipulation" >}})
