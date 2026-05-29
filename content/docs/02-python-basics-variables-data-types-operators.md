---
title: "Ch 2: Variables, Data Types & Operators"
weight: 2
---

# Variables, Data Types & Operators

## Learning Objectives

After reading this chapter, you will be able to:
- Create and use variables in Python
- Understand Python's primitive data types
- Perform operations with numbers, strings, and booleans
- Convert between data types
- Write expressions using operators
- Understand dynamic typing and type hints

---

## 2.1 Variables in Python

Variables are names that refer to values stored in memory.

```python
# Assigning variables
name = "Alice"
age = 30
height = 1.75
is_student = True

# Variables can be reassigned
age = 31

# Multiple assignment
x, y, z = 1, 2, 3

# Same value to multiple variables
a = b = c = 0
```

### Variable Naming Rules

```python
# ✅ Valid names
my_var = 1
myVar = 2
my_variable_2 = 3
MY_CONSTANT = 3.14
camelCaseVariant = 4

# ❌ Invalid names
# 1var = 1      # Can't start with a number
# my-var = 1    # Hyphens not allowed
# my var = 1    # Spaces not allowed
# class = 1     # Reserved keyword
```

### Python Keywords

These words are reserved and cannot be used as variable names:

```python
import keyword
print(keyword.kwlist)
# ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await',
#  'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except',
#  'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is',
#  'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return',
#  'try', 'while', 'with', 'yield']
```

---

## 2.2 Dynamic Typing

Python is **dynamically typed** — variables can change type:

```python
value = 42          # int
print(type(value))  # <class 'int'>

value = "hello"     # now it's a str
print(type(value))  # <class 'str'>

value = [1, 2, 3]   # now it's a list
print(type(value))  # <class 'list'>
```

### Type Hints (Python 3.5+)

Type hints are optional but recommended for better code quality:

```python
# Without type hints
def greet(name):
    return f"Hello, {name}"

# With type hints
def greet(name: str) -> str:
    return f"Hello, {name}"

# Variable type hints
age: int = 30
name: str = "Alice"
```

---

## 2.3 Primitive Data Types

### Integers (`int`)

```python
# Integer literals
a = 42           # Positive
b = -5           # Negative
c = 0            # Zero
large = 1_000_000  # Underscores for readability (1 million)

# Different bases
binary = 0b1010    # 10 in decimal
octal = 0o12       # 10 in decimal
hexadecimal = 0xA   # 10 in decimal

# Integer operations
print(10 + 3)    # 13
print(10 - 3)    # 7
print(10 * 3)    # 30
print(10 / 3)    # 3.333... (float result!)
print(10 // 3)   # 3 (integer division)
print(10 % 3)    # 1 (modulo)
print(10 ** 3)   # 1000 (exponentiation)
```

### Floating Point (`float`)

```python
# Float literals
pi = 3.14159
avogadro = 6.022e23  # Scientific notation
small = 1e-10        # 0.0000000001

# Float precision issues
print(0.1 + 0.2)  # 0.30000000000000004 (not exactly 0.3!)

# Use round() for financial calculations
print(round(0.1 + 0.2, 1))  # 0.3
```

### Strings (`str`)

```python
# String literals
single = 'Hello'
double = "Hello"
multi = '''This is a
multi-line string'''

# String concatenation
print("Hello" + " " + "World")  # Hello World

# String repetition
print("Ha" * 3)  # HaHaHa

# String length
print(len("Python"))  # 6

# f-strings (Python 3.6+)
name = "Alice"
age = 30
print(f"{name} is {age} years old")  # Alice is 30 years old

# Expression in f-strings
print(f"{2 + 2}")  # 4
print(f"{name.upper()}")  # ALICE
```

### Booleans (`bool`)

```python
# Boolean literals
is_valid = True
is_done = False

# Booleans are integers underneath
print(True + True)    # 2
print(True * 10)      # 10
print(False + 1)      # 1

# Truthy and falsy values
print(bool(1))        # True
print(bool(0))        # False
print(bool("hello"))  # True
print(bool(""))       # False
print(bool([]))       # False (empty list)
print(bool(None))     # False
```

### None Type (`NoneType`)

```python
# Represents the absence of a value
result = None

def no_return():
    pass

print(no_return())  # None

# Check for None
if result is None:
    print("No result yet")
```

---

## 2.4 Type Conversion

```python
# Implicit conversion (automatic)
print(10 + 3.0)  # 13.0 (int → float)

# Explicit conversion (casting)
print(int(3.14))      # 3
print(float(10))      # 10.0
print(str(42))        # "42"
print(int("42"))      # 42
print(float("3.14"))  # 3.14

# Careful with conversions
# int("hello")  # ValueError!
# int("3.14")   # ValueError! (must be int string first)

# Bool conversion
print(bool(1))       # True
print(bool(0))       # False
print(bool(""))      # False
print(bool("text"))  # True
```

---

## 2.5 Operators

### Arithmetic Operators

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `5 / 3` | `1.666...` |
| `//` | Floor Division | `5 // 3` | `1` |
| `%` | Modulus | `5 % 3` | `2` |
| `**` | Exponentiation | `5 ** 3` | `125` |

### Comparison Operators

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater or equal | `5 >= 5` | `True` |
| `<=` | Less or equal | `5 <= 3` | `False` |

### Logical Operators

```python
print(True and True)    # True
print(True and False)   # False
print(True or False)    # True
print(False or False)   # False
print(not True)         # False

# Short-circuit evaluation
def risky():
    return 1 / 0  # Never called

x = False and risky()  # Safe — risky() never runs

# Chained comparisons
age = 25
print(18 <= age <= 65)  # True (Python-specific!)
```

### Assignment Operators

```python
x = 5
x += 3    # x = x + 3 = 8
x -= 2    # x = x - 2 = 6
x *= 4    # x = x * 4 = 24
x /= 3    # x = x / 3 = 8.0
x //= 2   # x = x // 2 = 4.0
x %= 3    # x = x % 3 = 1.0
x **= 2   # x = x ** 2 = 1.0
```

### Identity Operators

```python
# is vs ==
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (same value)
print(a is b)  # False (different objects)
print(a is c)  # True (same object)

# is checks identity, == checks equality
# Use is for None, True, False
def get_value():
    return None

result = get_value()
if result is None:
    print("No value")
```

### Membership Operators

```python
print("a" in "hello")     # False
print("e" in "hello")     # True
print("x" not in "hello")  # True

print(3 in [1, 2, 3])     # True
print("key" in {"key": 1})  # True
```

### Operator Precedence

From highest to lowest precedence:

```python
# 1. () — Parentheses
# 2. ** — Exponentiation
# 3. +x, -x — Unary operators
# 4. *, /, //, % — Multiplication/Division
# 5. +, - — Addition/Subtraction
# 6. ==, !=, >, <, >=, <= — Comparisons
# 7. not — Logical NOT
# 8. and — Logical AND
# 9. or — Logical OR

result = 2 + 3 * 4 ** 2  # 2 + 3 * 16 = 2 + 48 = 50
result = (2 + 3) * 4 ** 2  # 5 * 16 = 80
```

---

## Key Takeaways

- Python is dynamically typed — variables can change type freely
- Use type hints for better code clarity (optional but recommended)
- Python has `int`, `float`, `str`, `bool`, and `NoneType` as primitive types
- f-strings (`f"..."`) are the best way to format strings
- Use `is` for `None` comparison, `==` for value comparison
- Python supports chained comparisons like `18 <= age <= 65`

---

## Exercises

1. **Swap two variables** without using a third variable: `a, b = b, a`
2. **Calculate compound interest**: A = P(1 + r/n)^(nt)
3. **Write expressions** using all arithmetic operators and verify results
4. **Practice type conversion**: Convert a string number to int, float, and back
5. **Check if a number** is even or odd using the modulo operator

---

## Next Steps

→ Continue to [Chapter 3: Control Flow — Conditionals & Loops]({{< relref "03-control-flow-conditionals-and-loops" >}})
