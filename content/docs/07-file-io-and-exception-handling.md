---
title: "Ch 7: File I/O & Exception Handling"
weight: 7
---

# File I/O & Exception Handling

## Learning Objectives

After reading this chapter, you will be able to:
- Read and write files using Python's built-in functions
- Use context managers (`with` statement) for resource management
- Handle exceptions with `try`/`except`/`finally`
- Create custom exceptions
- Work with different file formats (CSV, JSON)
- Understand file modes and binary vs text files

---

## 7.1 Opening and Closing Files

### The `open()` Function

```python
file = open("example.txt", "r")  # Open for reading
data = file.read()               # Read content
file.close()                      # Always close!
```

### File Modes

| Mode | Description |
|------|-------------|
| `'r'` | Read (default) — error if file doesn't exist |
| `'w'` | Write — creates file, overwrites if exists |
| `'a'` | Append — creates file if doesn't exist |
| `'x'` | Exclusive create — fails if file exists |
| `'r+'` | Read and write |
| `'b'` | Binary mode (add to other modes, e.g., `'rb'`, `'wb'`) |
| `'t'` | Text mode (default, e.g., `'rt'`) |

---

## 7.2 Context Managers (`with` Statement)

**Always use `with`** for file operations — it automatically closes the file:

```python
# Reading
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here

# Writing
with open("output.txt", "w") as file:
    file.write("Hello, World!")

# Multiple files
with open("input.txt") as infile, open("output.txt", "w") as outfile:
    outfile.write(infile.read().upper())
```

---

## 7.3 Reading Files

```python
with open("sample.txt", "r") as f:
    # Read entire file as string
    content = f.read()
    
    # Read first N characters
    first_100 = f.read(100)
    
    # Read all lines into a list
    lines = f.readlines()
    
    # Read one line at a time (memory efficient)
    for line in f:
        print(line.strip())
    
    # Read next line
    line = f.readline()
    print(line)
```

### Best Practices for Large Files

```python
# Memory-efficient — reads line by line
with open("large_file.txt", "r") as f:
    for line in f:
        process(line)

# Read in chunks (for binary files)
def read_in_chunks(file_path, chunk_size=1024):
    with open(file_path, "rb") as f:
        while chunk := f.read(chunk_size):
            yield chunk
```

---

## 7.4 Writing Files

```python
# Write string
with open("output.txt", "w") as f:
    f.write("First line\n")
    f.write("Second line\n")

# Write multiple lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w") as f:
    f.writelines(line + "\n" for line in lines)

# Append to file
with open("log.txt", "a") as f:
    f.write("New log entry\n")
```

---

## 7.5 Working with File Paths

```python
import os
from pathlib import Path  # Modern approach

# Using os.path
print(os.path.join("dir", "subdir", "file.txt"))
print(os.path.exists("file.txt"))
print(os.path.isfile("file.txt"))
print(os.path.isdir("mydir"))
print(os.path.basename("/path/to/file.txt"))  # file.txt
print(os.path.dirname("/path/to/file.txt"))   # /path/to
print(os.path.splitext("file.txt"))           # ('file', '.txt')

# Using pathlib (Python 3.4+)
p = Path("dir/subdir/file.txt")
print(p.parent)      # dir/subdir
print(p.name)        # file.txt
print(p.stem)        # file
print(p.suffix)      # .txt
print(p.exists())    # True/False
print(p.is_file())   # True/False

# Creating directories
Path("output/data").mkdir(parents=True, exist_ok=True)
```

---

## 7.6 Working with JSON

```python
import json

# Writing JSON
data = {
    "name": "Alice",
    "age": 30,
    "skills": ["Python", "SQL", "Docker"],
    "active": True
}

with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

# Reading JSON
with open("data.json", "r") as f:
    loaded = json.load(f)
    print(loaded["name"])  # Alice

# String conversions
json_str = json.dumps(data, indent=2)
parsed = json.loads(json_str)

# Handling custom objects
from datetime import datetime

def serialize(obj):
    if isinstance(obj, datetime):
        return obj.isoformat()
    raise TypeError(f"Cannot serialize {obj}")

with open("data.json", "w") as f:
    json.dump({"now": datetime.now()}, f, default=serialize)
```

---

## 7.7 Working with CSV

```python
import csv

# Reading CSV
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    header = next(reader)  # Skip header
    for row in reader:
        print(row)

# Using DictReader
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["name"], row["age"])

# Writing CSV
with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "age", "city"])
    writer.writerow(["Alice", 30, "NYC"])
    writer.writerows([
        ["Bob", 25, "LA"],
        ["Charlie", 35, "Chicago"]
    ])

# Using DictWriter
with open("output.csv", "w", newline="") as f:
    fieldnames = ["name", "age", "city"]
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({"name": "Alice", "age": 30, "city": "NYC"})
```

---

## 7.8 Exception Handling

### Basic `try`/`except`

```python
try:
    number = int(input("Enter a number: "))
    result = 10 / number
    print(f"Result: {result}")
except ValueError:
    print("That's not a valid number!")
except ZeroDivisionError:
    print("Can't divide by zero!")
```

### Catching Multiple Exceptions

```python
try:
    value = risky_function()
except (ValueError, TypeError, RuntimeError) as e:
    print(f"Error occurred: {e}")

# Catch all (use sparingly!)
try:
    value = risky_function()
except Exception as e:
    print(f"Unexpected error: {e}")
```

### `else` and `finally` Clauses

```python
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found!")
else:
    print(f"Read {len(content)} characters")
    # Only runs if no exception occurred
finally:
    file.close()  # Always runs — cleanup!
```

### Raising Exceptions

```python
def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError("Amount must be positive")
    if amount > balance:
        raise InsufficientFundsError("Insufficient balance")
    return balance - amount

# Re-raising
try:
    withdraw(100, 200)
except InsufficientFundsError:
    print("Logging error...")
    raise  # Re-raise the same exception
```

### Custom Exceptions

```python
class BankError(Exception):
    """Base exception for bank operations."""
    pass

class InsufficientFundsError(BankError):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Insufficient funds: balance={balance}, required={amount}")

class AccountLockedError(BankError):
    pass

# Usage
try:
    raise InsufficientFundsError(100, 200)
except BankError as e:
    print(f"Bank error: {e}")
```

### Common Built-in Exceptions

| Exception | Cause |
|-----------|-------|
| `ValueError` | Invalid argument value |
| `TypeError` | Operation on wrong type |
| `IndexError` | List/tuple index out of range |
| `KeyError` | Dictionary key not found |
| `FileNotFoundError` | File doesn't exist |
| `ZeroDivisionError` | Division by zero |
| `AttributeError` | Object has no such attribute |
| `ImportError` | Module not found |
| `StopIteration` | Iterator exhausted |

---

## 7.9 The `with` Statement and Context Managers

### Creating a Custom Context Manager

```python
# Using __enter__ and __exit__
class ManagedFile:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.file.close()
        # Return True to suppress exceptions, False to propagate
        return False

# Usage
with ManagedFile("test.txt", "w") as f:
    f.write("Hello!")

# Using contextlib
from contextlib import contextmanager

@contextmanager
def managed_file(filename, mode):
    f = open(filename, mode)
    try:
        yield f
    finally:
        f.close()

with managed_file("test.txt", "w") as f:
    f.write("Hello from generator!")
```

---

## Key Takeaways

- Always use `with open(...)` for file operations — automatic cleanup
- Use `'w'` for write, `'r'` for read, `'a'` for append, `'b'` for binary
- JSON and CSV modules handle structured data files
- `try`/`except` catches errors; `finally` ensures cleanup
- Create custom exceptions by inheriting from `Exception`
- `pathlib.Path` is the modern way to handle file paths
- The `with` statement works with any context manager (file, lock, database connection)

---

## Exercises

1. **File copy**: Write a function that copies a file character by character
2. **CSV analyzer**: Read a CSV file and print summary statistics of numeric columns
3. **JSON processor**: Read a JSON file, modify some values, and write it back
4. **Exception handling**: Write a calculator that gracefully handles all input errors
5. **Log parser**: Parse a log file and count errors/warnings/info messages
6. **Custom context**: Create a timer context manager that measures execution time
7. **File tree**: Use `pathlib` to recursively list all files in a directory

---

## Next Steps

→ Continue to [Chapter 8: Object-Oriented Programming (OOP)]({{< relref "08-oop-object-oriented-programming" >}})
