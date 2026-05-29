---
title: "Ch 1: Introduction to Python & Setup"
weight: 1
---

# Introduction to Python & Setup

## Learning Objectives

After reading this chapter, you will be able to:
- Understand what Python is and why it's so popular
- Install Python on your machine
- Use the Python REPL for interactive coding
- Write and run your first Python script
- Set up a virtual environment and install packages
- Choose an IDE or code editor for Python development

---

## 1.1 What is Python?

**Python** is a high-level, interpreted, general-purpose programming language created by **Guido van Rossum** and first released in **1991**. It emphasizes **code readability** and **simplicity**, allowing developers to write clear, logical code for small and large-scale projects.

### Why Python?

| Reason | Description |
|--------|-------------|
| **Beginner-friendly** | Simple, readable syntax that reads like English |
| **Versatile** | Web development, data science, AI/ML, automation, scripting |
| **Huge ecosystem** | 200,000+ packages on PyPI (Python Package Index) |
| **Community** | One of the largest, most active programming communities |
| **Industry adoption** | Google, Netflix, Spotify, Instagram, NASA use Python |
| **Job market** | Consistently one of the most in-demand programming languages |

### Python's Design Philosophy

Python follows the "Zen of Python" (PEP 20), which includes principles like:

```python
# The Zen of Python — import this
import this
```

Key principles:
- **Beautiful is better than ugly**
- **Explicit is better than implicit**
- **Simple is better than complex**
- **Readability counts**

---

## 1.2 Python Versions

| Version | Status | When to Use |
|---------|--------|-------------|
| **Python 3.13+** | Latest | New projects, cutting-edge features |
| **Python 3.10–3.12** | Stable | Most production projects |
| **Python 3.9** | Maintenance | Legacy projects |
| **Python 3.8** | EOL (End of Life) | Migrate away |
| **Python 2.7** | Dead | Do NOT use |

> **Important:** Python 2 is officially dead since January 1, 2020. Always use Python 3!

---

## 1.3 Installing Python

### Option 1: Official Installer (All Platforms)

Go to [python.org/downloads](https://www.python.org/downloads/) and download the latest version for your OS.

### Option 2: Package Manager

```bash
# macOS (Homebrew)
brew install python@3.12

# Linux (Ubuntu/Debian)
sudo apt update
sudo apt install python3 python3-pip python3-venv

# Linux (RHEL/CentOS/Fedora)
sudo dnf install python3 python3-pip

# Windows (Chocolatey)
choco install python

# Windows (winget)
winget install Python.Python.3.12
```

### Verify Installation

```bash
python3 --version
# Python 3.12.0

pip3 --version
# pip 23.2.1 from ... (python 3.12)
```

On Windows, you may use `python` instead of `python3`.

---

## 1.4 The Python REPL

Python comes with an **interactive interpreter** (REPL — Read-Eval-Print Loop).

```bash
# Start the REPL
python3

# You'll see:
Python 3.12.0 (main, Oct 16 2023, 12:22:24)
[Clang 15.0.0 (clang-1500.0.40.1)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Try typing:

```python
>>> print("Hello, World!")
Hello, World!

>>> 2 + 2
4

>>> "Python" * 3
'PythonPythonPython'

>>> exit()
```

### Using the REPL Like a Pro

```python
# Get help on any function
>>> help(print)

# Check the type of any value
>>> type(42)
<class 'int'>

# Last expression result is stored in _
>>> 10 + 20
30
>>> _ * 2
60
```

---

## 1.5 Your First Python Script

Create a file called `hello.py`:

```python
# hello.py
print("Hello, World!")

# Ask for user input
name = input("What's your name? ")
print(f"Nice to meet you, {name}!")
```

Run it:

```bash
python3 hello.py
# Hello, World!
# What's your name? Alice
# Nice to meet you, Alice!
```

---

## 1.6 Virtual Environments

Virtual environments isolate project dependencies so different projects don't interfere with each other.

### Creating and Activating a Virtual Environment

```bash
# Create a virtual environment
python3 -m venv venv

# Activate it (macOS/Linux)
source venv/bin/activate

# Activate it (Windows)
.\\venv\\Scripts\\activate

# Your prompt changes to show (venv)
(venv) $

# Deactivate
(venv) $ deactivate
```

### Working with venv

```bash
# Activate first
source venv/bin/activate

# Check Python location — should be inside venv
which python3
# /Users/you/project/venv/bin/python3

# Install packages
pip install requests flask

# Freeze dependencies
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt
```

### Why Use Virtual Environments?

| Without venv | With venv |
|-------------|-----------|
| Project A needs Flask 2.0, Project B needs Flask 3.0 → conflict | Each project has its own dependencies |
| System-wide package installs may require sudo | User-level installation, no sudo needed |
| Can't reproduce exact dependencies | `requirements.txt` captures exact versions |

---

## 1.7 Package Management with pip

**pip** is Python's package installer. It downloads packages from PyPI (Python Package Index).

### Common pip Commands

```bash
# Install a package
pip install requests

# Install a specific version
pip install requests==2.31.0

# Install multiple packages
pip install flask pandas numpy

# Upgrade a package
pip install --upgrade requests

# Uninstall a package
pip uninstall requests

# List installed packages
pip list

# Show package info
pip show requests

# Install from requirements file
pip install -r requirements.txt
```

---

## 1.8 Choosing an IDE / Code Editor

| Editor | Best For | Features |
|--------|----------|----------|
| **VS Code** | General Python dev | Excellent Python extension, debugging, Git integration |
| **PyCharm** | Professional Python | Built-in debugger, test runner, database tools, refactoring |
| **Jupyter Lab** | Data science | Interactive notebooks, inline plots, data exploration |
| **vim/neovim** | Terminal purists | Lightweight, highly configurable, keyboard-driven |
| **Sublime Text** | Quick edits | Fast, minimal, great for small scripts |

### Recommended VS Code Extensions for Python

```
- Python (by Microsoft) — IntelliSense, linting, debugging
- Pylance — Fast, feature-rich language support
- Python Docstring Generator
- GitLens — Git blame annotations
- autoDocstring — Generate docstrings
```

---

## 1.9 Python Code Organization

### File Extensions

| Extension | Purpose |
|-----------|---------|
| `.py` | Standard Python source file |
| `.pyi` | Python stub file (type hints) |
| `.pyc` | Compiled Python file (bytecode) |
| `.ipynb` | Jupyter notebook |
| `.pyw` | Python script (Windows, no console) |

### Naming Conventions

```python
# Modules: short, lowercase, underscores
# File: my_module.py

# Classes: CapWords convention
class MyAwesomeClass:
    pass

# Functions and variables: lowercase_with_underscores
def calculate_average(numbers):
    total = sum(numbers)
    return total / len(numbers)

# Constants: ALL_CAPS
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 30
```

---

## Key Takeaways

- Python is a versatile, beginner-friendly language with a massive ecosystem
- Always use Python 3 (never Python 2)
- Use virtual environments to isolate project dependencies
- pip is the Python package manager — `pip install package_name`
- VS Code with the Python extension is a great starting setup
- The REPL is perfect for experimenting with code

---

## Exercises

1. **Install Python** and verify with `python3 --version`
2. **Create a virtual environment**, activate it, and install the `requests` package
3. **Write a script** that asks for the user's name and age, then prints a greeting
4. **Use the REPL** to experiment with `print()`, `type()`, and basic arithmetic
5. **Freeze your dependencies** with `pip freeze > requirements.txt`

---

## Next Steps

→ Continue to [Chapter 2: Variables, Data Types & Operators]({{< relref "02-python-basics-variables-data-types-operators" >}})
