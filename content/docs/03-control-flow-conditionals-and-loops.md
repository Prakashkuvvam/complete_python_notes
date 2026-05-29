---
title: "Ch 3: Control Flow — Conditionals & Loops"
weight: 3
---

# Control Flow — Conditionals & Loops

## Learning Objectives

After reading this chapter, you will be able to:
- Use `if`, `elif`, and `else` for conditional logic
- Write `for` loops to iterate over sequences
- Use `while` loops for repeated execution
- Control loop flow with `break`, `continue`, and `else`
- Use list comprehensions for concise iteration
- Understand the `match` statement (Python 3.10+)

---

## 3.1 Conditional Statements (`if`/`elif`/`else`)

### Basic `if` Statement

```python
age = 18

if age >= 18:
    print("You are an adult")
```

### `if`/`else`

```python
age = 16

if age >= 18:
    print("You can vote")
else:
    print("You are too young to vote")
```

### `if`/`elif`/`else` Chain

```python
grade = 85

if grade >= 90:
    letter = "A"
elif grade >= 80:
    letter = "B"
elif grade >= 70:
    letter = "C"
elif grade >= 60:
    letter = "D"
else:
    letter = "F"

print(f"Grade: {letter}")
```

### Nested Conditionals

```python
x = 10

if x > 0:
    if x % 2 == 0:
        print("Positive even number")
    else:
        print("Positive odd number")
else:
    print("Non-positive number")
```

### Ternary Operator (Conditional Expression)

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)  # Adult

# Equivalent to:
if age >= 18:
    status = "Adult"
else:
    status = "Minor"
```

---

## 3.2 Truthy and Falsy Values

In Python, every value can be evaluated as `True` or `False` in a boolean context:

```python
# Falsy values (evaluate to False)
print(bool(False))      # False
print(bool(None))       # False
print(bool(0))          # False
print(bool(0.0))        # False
print(bool(""))         # False (empty string)
print(bool([]))         # False (empty list)
print(bool({}))         # False (empty dict)
print(bool(set()))      # False (empty set)
print(bool(()))         # False (empty tuple)

# Truthy values (everything else)
print(bool(1))          # True
print(bool(-1))         # True
print(bool("hello"))    # True
print(bool([1, 2]))     # True
print(bool({"a": 1}))   # True
```

### Using Truthiness in Conditionals

```python
# Idiomatic Python — avoid explicit comparisons
def process_user(name):
    if not name:  # Instead of: if name == "" or name is None
        print("No name provided")
        return
    print(f"Processing {name}")

items = []
if items:  # Instead of: if len(items) > 0
    print(f"Processing {len(items)} items")
else:
    print("No items to process")
```

---

## 3.3 The `match` Statement (Python 3.10+)

Structural pattern matching — a powerful alternative to long `if/elif` chains:

```python
# Basic match
status_code = 404

match status_code:
    case 200:
        print("OK")
    case 201:
        print("Created")
    case 404:
        print("Not Found")
    case _:
        print("Unknown status")
```

### Matching with Multiple Patterns

```python
def handle_command(command):
    match command.split():
        case ["quit"]:
            print("Goodbye!")
        case ["hello", name]:
            print(f"Hello, {name}!")
        case ["add", *numbers]:
            total = sum(int(n) for n in numbers)
            print(f"Sum: {total}")
        case _:
            print("Unknown command")

handle_command("hello Alice")   # Hello, Alice!
handle_command("add 1 2 3 4")   # Sum: 10
```

### Matching with Guards

```python
point = (5, -5)

match point:
    case (0, 0):
        print("Origin")
    case (x, 0) if x > 0:
        print(f"Positive X-axis: {x}")
    case (0, y) if y > 0:
        print(f"Positive Y-axis: {y}")
    case (x, y) if x > 0 and y > 0:
        print(f"First quadrant: ({x}, {y})")
    case _:
        print("Other location")
```

---

## 3.4 `for` Loops

### Iterating Over Sequences

```python
# List
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# String
for char in "Python":
    print(char, end=" ")  # P y t h o n

# Tuple
for item in (1, 2, 3):
    print(item)

# Dictionary
person = {"name": "Alice", "age": 30}
for key in person:
    print(key, person[key])

# With .items()
for key, value in person.items():
    print(f"{key}: {value}")
```

### Using `range()`

```python
# range(stop)
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# range(start, stop)
for i in range(2, 7):
    print(i)  # 2, 3, 4, 5, 6

# range(start, stop, step)
for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8

# Backwards
for i in range(10, 0, -1):
    print(i)  # 10, 9, 8, ..., 1
```

### The `enumerate()` Function

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
# 0: apple
# 1: banana
# 2: cherry

# Start from a different number
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}: {fruit}")
# 1: apple
# 2: banana
# 3: cherry
```

### The `zip()` Function

```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 92, 78]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
# Alice: 85
# Bob: 92
# Charlie: 78

# Unzip
pairs = [(1, 'a'), (2, 'b'), (3, 'c')]
numbers, letters = zip(*pairs)
print(numbers)  # (1, 2, 3)
print(letters)  # ('a', 'b', 'c')
```

---

## 3.5 `while` Loops

### Basic `while` Loop

```python
count = 0
while count < 5:
    print(count)
    count += 1
```

### Infinite Loops (with break)

```python
while True:
    response = input("Type 'quit' to exit: ")
    if response.lower() == "quit":
        break
    print(f"You typed: {response}")
```

### Sentinel-Controlled Loop

```python
# Sum numbers until negative
numbers = [10, 20, 30, -1, 40, 50]
total = 0
i = 0

while i < len(numbers) and numbers[i] >= 0:
    total += numbers[i]
    i += 1

print(f"Sum before negative: {total}")  # 60
```

---

## 3.6 Loop Control: `break`, `continue`, `pass`

### `break` — Exit the Loop

```python
# Find first even number
numbers = [1, 3, 5, 8, 11, 14]
for n in numbers:
    if n % 2 == 0:
        print(f"Found even: {n}")
        break

# Nested loop break only breaks inner loop
for i in range(3):
    for j in range(3):
        if i == j == 1:
            break
        print(i, j)
```

### `continue` — Skip to Next Iteration

```python
# Print only even numbers
for n in range(10):
    if n % 2 != 0:
        continue
    print(n)  # 0, 2, 4, 6, 8

# Skip vowels
word = "hello world"
vowels = "aeiou"
for char in word:
    if char in vowels:
        continue
    print(char, end="")  # hll wrld
```

### `pass` — Do Nothing (Placeholder)

```python
# Placeholder for future code
def to_implement():
    pass

class MyClass:
    pass

for i in range(5):
    if i == 3:
        pass  # Will handle later
    print(i)
```

### `else` Clause on Loops

The `else` block executes **only if** the loop completes normally (no `break`):

```python
# Search example
numbers = [1, 3, 5, 7, 9]
target = 4

for n in numbers:
    if n == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found")  # This runs

# Prime number check
num = 17
for i in range(2, int(num ** 0.5) + 1):
    if num % i == 0:
        print(f"{num} is not prime")
        break
else:
    print(f"{num} is prime")  # Runs if no factor found
```

---

## 3.7 List Comprehensions

A concise way to create lists:

```python
# Basic syntax: [expression for item in iterable]
squares = [x ** 2 for x in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With condition: [expression for item in iterable if condition]
even_squares = [x ** 2 for x in range(10) if x % 2 == 0]
print(even_squares)  # [0, 4, 16, 36, 64]

# With if-else (ternary inside)
labels = ["even" if x % 2 == 0 else "odd" for x in range(5)]
print(labels)  # ['even', 'odd', 'even', 'odd', 'even']

# Nested loop comprehension
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs)
# [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]

# Flatten a matrix
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [num for row in matrix for num in row]
print(flat)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Dict and Set Comprehensions

```python
# Dict comprehension: {key: value for item in iterable}
squares_dict = {x: x ** 2 for x in range(5)}
print(squares_dict)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Set comprehension: {expression for item in iterable}
numbers = [1, 2, 2, 3, 3, 3, 4]
unique_squares = {x ** 2 for x in numbers}
print(unique_squares)  # {1, 4, 9, 16}
```

---

## 3.8 Generator Expressions

Similar to list comprehensions but lazy (produce items on demand):

```python
# Generator expression (parentheses instead of brackets)
squares_gen = (x ** 2 for x in range(5))
print(squares_gen)  # <generator object at 0x...>

for s in squares_gen:
    print(s)  # 0, 1, 4, 9, 16

# Memory efficient for large sequences
# List comprehension creates full list in memory
# Generator expression produces items one by one
sum_of_squares = sum(x ** 2 for x in range(1000000))
print(sum_of_squares)  # 333332833333500
```

---

## Key Takeaways

- Use `if`/`elif`/`else` for conditional branching
- `for` loops iterate over any iterable; use `range()` for numeric ranges
- `match` (Python 3.10+) provides powerful pattern matching
- `break` exits a loop, `continue` skips to next iteration
- The `else` clause on loops runs only if no `break` occurred
- List comprehensions are concise but can be overused — keep them readable
- Generator expressions are memory-efficient for large datasets
- Use truthiness — it's more Pythonic than explicit comparisons

---

## Exercises

1. **FizzBuzz**: Print numbers 1-100. Multiples of 3 → "Fizz", 5 → "Buzz", both → "FizzBuzz"
2. **Prime numbers**: Write a loop to find all primes up to 100
3. **Fibonacci**: Generate the first 20 Fibonacci numbers using a loop
4. **List comprehension**: Create a list of (x, x², x³) for x in range(1, 11)
5. **Nested loops**: Print a multiplication table (1-10) using nested `for` loops
6. **Match statement**: Write a calculator that handles `add`, `sub`, `mul`, `div` commands
7. **Loop with else**: Find if a word is a palindrome using a loop with `else`

---

## Next Steps

→ Continue to [Chapter 4: Functions & Modules]({{< relref "04-functions-and-modules" >}})
