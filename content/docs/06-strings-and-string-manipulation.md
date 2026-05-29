---
title: "Ch 6: Strings & String Manipulation"
weight: 6
---

# Strings & String Manipulation

## Learning Objectives

After reading this chapter, you will be able to:
- Create and manipulate strings using various methods
- Format strings with f-strings, `.format()`, and `%` formatting
- Use regular expressions for pattern matching
- Work with Unicode and encoding
- Understand string immutability and slicing

---

## 6.1 String Basics

### Creating Strings

```python
# Single quotes
single = 'Hello'

# Double quotes
double = "Hello"

# Triple quotes for multiline
multi = '''This is a
multi-line string'''

multi2 = """Also works
with double quotes"""

# Raw strings (no escape processing)
path = r'C:\Users\Name\Documents'
regex = r'\d+\.\d+'

# f-strings (formatted strings)
name = "Alice"
greeting = f"Hello, {name}!"
```

### Escape Sequences

```python
print("Line1\nLine2")      # Newline
print("Tab\tseparated")    # Tab
print("Backslash: \\")      # Backslash
print("Quote: \"")         # Double quote
print("Quote: '")          # Single quote
print("Unicode: \u2764")   # Unicode heart: ❤
print("Hex: \x41")         # ASCII 'A'
```

---

## 6.2 String Immutability

Strings in Python are **immutable** — they cannot be changed in place.

```python
name = "Python"
# name[0] = "J"  # TypeError: 'str' object does not support item assignment

# Instead, create a new string
name = "J" + name[1:]
print(name)  # Jython

# Every string operation returns a new string
original = "Hello"
upper = original.upper()
print(original)  # Hello (unchanged)
print(upper)     # HELLO
```

---

## 6.3 String Methods

### Case Conversion

```python
text = "Hello World"

print(text.upper())          # HELLO WORLD
print(text.lower())          # hello world
print(text.title())          # Hello World
print(text.capitalize())     # Hello world
print(text.swapcase())       # hELLO wORLD
print(text.casefold())       # hello world (aggressive lowercasing)

# Case-insensitive comparison
print("Straße".lower() == "strasse".lower())   # False
print("Straße".casefold() == "strasse".casefold())  # True
```

### Checking String Properties

```python
print("Hello".isalpha())     # True
print("123".isdigit())       # True
print("abc123".isalnum())    # True
print("   ".isspace())       # True
print("Hello".isupper())     # False
print("hello".islower())     # True
print("Hello World".istitle())  # True
print("123".isnumeric())     # True
print("Ⅷ".isnumeric())       # True (Roman numeral)
```

### Searching and Finding

```python
text = "Hello, welcome to Python programming"

print(text.find("Python"))   # 18 (index of first occurrence)
print(text.find("Java"))     # -1 (not found)
print(text.index("Python"))  # 18 (raises ValueError if not found)
print(text.rfind("o"))       # 24 (last occurrence)
print(text.count("o"))       # 4
print("Python" in text)      # True
print("Java" not in text)    # True
print(text.startswith("Hello"))  # True
print(text.endswith("ing"))      # True
```

### Modifying Strings

```python
text = "  Hello, World!  "

# Remove whitespace
print(text.strip())       # "Hello, World!"
print(text.lstrip())      # "Hello, World!  "
print(text.rstrip())      # "  Hello, World!"

# Replace
print(text.replace("World", "Python"))  #   Hello, Python!

# Split and join
print("a,b,c".split(","))           # ['a', 'b', 'c']
print("one two three".split())       # ['one', 'two', 'three']
print("1-2-3-4".split("-", 2))      # ['1', '2', '3-4'] (maxsplit)
print("\n".join(["a", "b", "c"]))    # "a\nb\nc"

# Padding and alignment
text = "Python"
print(text.center(20))       # '      Python       '
print(text.ljust(20, '-'))   # 'Python--------------'
print(text.rjust(20, '-'))   # '--------------Python'
print(text.zfill(10))        # '0000Python'

# Remove prefixes/suffixes (Python 3.9+)
print("test.py").removeprefix("test")  # ".py"
print("test.py").removesuffix(".py")   # "test"
```

---

## 6.4 String Formatting

### f-Strings (Python 3.6+) — **Preferred Method**

```python
name = "Alice"
age = 30

# Basic
print(f"Name: {name}, Age: {age}")

# Expressions
print(f"2 + 2 = {2 + 2}")
print(f"Uppercase: {name.upper()}")

# Format specifiers
pi = 3.14159265
print(f"Pi: {pi:.2f}")            # Pi: 3.14
print(f"Pi: {pi:.4f}")            # Pi: 3.1416
print(f"Pi: {pi:10.2f}")          # Pi:       3.14 (right-aligned)

# Number formatting
print(f"{1000000:,}")             # 1,000,000
print(f"{0.25:.1%}")              # 25.0%
print(f"{255:#x}")               # 0xff (hex)
print(f"{255:#o}")               # 0o377 (octal)
print(f"{255:#b}")               # 0b11111111 (binary)

# Alignment
print(f"{name:>10}")              # '     Alice' (right)
print(f"{name:<10}")              # 'Alice     ' (left)
print(f"{name:^10}")              # '  Alice   ' (center)

# Debugging (Python 3.8+)
print(f"{name=}, {age=}")         # name='Alice', age=30
```

### `.format()` Method

```python
# Positional
print("{} is {} years old".format("Alice", 30))

# Indexed
print("{0} {1} {0}".format("a", "b"))  # a b a

# Named
print("{name} is {age} years old".format(name="Bob", age=25))

# Dict unpacking
person = {"name": "Charlie", "age": 35}
print("{name} is {age}".format(**person))
```

### `%` Formatting (Old Style)

```python
print("%s is %d years old" % ("Alice", 30))
print("Pi = %.2f" % 3.14159)
print("Hex: %x" % 255)

# Specifiers: %s (string), %d (int), %f (float), %x (hex)
```

---

## 6.5 String Slicing

```python
text = "Python Programming"

print(text[0:6])      # 'Python'
print(text[7:])       # 'Programming'
print(text[:6])       # 'Python'
print(text[-11:])     # 'Programming'
print(text[::-1])     # 'gnimmargorP nohtyP' (reverse)
print(text[::2])      # 'Pto rgamn' (every other)
print(text[1::2])     # 'yh rorai' (every other, starting at 1)
```

### Slicing Idioms

```python
# Palindrome check
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    return s == s[::-1]

print(is_palindrome("racecar"))      # True
print(is_palindrome("A man a plan a canal panama"))  # True
```

---

## 6.6 Regular Expressions

The `re` module provides powerful pattern matching:

```python
import re

text = "Contact: alice@email.com or bob@test.org"

# Search — find first match
match = re.search(r'\w+@\w+\.\w+', text)
if match:
    print(match.group())  # alice@email.com

# Find all matches
emails = re.findall(r'\w+@\w+\.\w+', text)
print(emails)  # ['alice@email.com', 'bob@test.org']

# Match at beginning
print(re.match(r'Contact', text))  # Match object
print(re.match(r'Email', text))     # None

# Split by pattern
print(re.split(r'[,;\s]+', "a,b;c d"))  # ['a', 'b', 'c', 'd']

# Replace
print(re.sub(r'\d+', '###', 'Order: 123, Item: 456'))
# Order: ###, Item: ###

# Compile for reuse
email_pattern = re.compile(r'([\w.]+)@([\w.]+)\.(\w+)')
match = email_pattern.search("user@example.com")
if match:
    print(match.groups())  # ('user', 'example', 'com')
    print(match.group(1))  # user
```

### Common Regex Patterns

| Pattern | Matches | Example |
|---------|---------|---------|
| `\d+` | One or more digits | `123` |
| `\w+` | One or more word chars | `hello_123` |
| `\s+` | One or more whitespace | `   ` |
| `[A-Za-z]+` | Letters only | `Python` |
| `^...` | Start of string | — |
| `...$` | End of string | — |
| `[abc]` | Any of a, b, or c | `a` |
| `[^abc]` | Not a, b, or c | `d` |
| `a|b` | Either a or b | — |
| `a{3}` | Exactly 3 a's | `aaa` |
| `a{2,4}` | 2 to 4 a's | `aa`, `aaa` |

---

## 6.7 Unicode and Encoding

```python
# String to bytes (encoding)
text = "Hello, 世界"
bytes_utf8 = text.encode('utf-8')
print(bytes_utf8)  # b'Hello, \xe4\xb8\x96\xe7\x95\x8c'

# Bytes to string (decoding)
decoded = bytes_utf8.decode('utf-8')
print(decoded)  # Hello, 世界

# Different encodings
print(text.encode('utf-16'))  # Different byte sequence
print(text.encode('ascii', errors='ignore'))  # b'Hello, '
print(text.encode('ascii', errors='replace'))  # b'Hello, ??'

# Unicode code points
print(ord('A'))    # 65
print(ord('世'))   # 19990
print(chr(65))     # 'A'
print(chr(19990))  # '世'
```

---

## Key Takeaways

- Strings are **immutable** — all operations return new strings
- **f-strings** are the preferred formatting method (Python 3.6+)
- String methods like `.strip()`, `.split()`, `.join()`, `.replace()` are essential
- Regular expressions (`re` module) handle complex pattern matching
- Use `.casefold()` for aggressive case-insensitive comparison
- Slicing syntax `[start:stop:step]` works on strings too
- Always specify encoding when reading/writing files (`utf-8`)

---

## Exercises

1. **String reversal**: Reverse a string in three different ways
2. **Palindrome detector**: Check if a string is a palindrome (ignore case, spaces, punctuation)
3. **Email extractor**: Use regex to extract all email addresses from a block of text
4. **CSV parser**: Parse a CSV line into fields (handle quoted fields)
5. **Password validator**: Check password meets criteria: 8+ chars, upper, lower, digit, special
6. **URL parser**: Extract protocol, domain, and path from a URL
7. **Format converter**: Convert "snake_case" to "camelCase" and back

---

## Next Steps

→ Continue to [Chapter 7: File I/O & Exception Handling]({{< relref "07-file-io-and-exception-handling" >}})
