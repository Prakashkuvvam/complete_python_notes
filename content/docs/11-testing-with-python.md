---
title: "Ch 11: Testing with Python"
weight: 11
---

# Testing with Python

## Learning Objectives

After reading this chapter, you will be able to:
- Write unit tests using `unittest` and `pytest`
- Use test fixtures, parametrization, and mocking
- Understand test-driven development (TDD)
- Measure code coverage
- Write doctests for documentation and testing

---

## 11.1 Why Testing Matters

**Benefits of automated testing:**
- Catches bugs early
- Enables refactoring with confidence
- Documents expected behavior
- Prevents regression
- Improves code design (testable code is usually better code)

### Testing Levels

| Level | What It Tests | Tools |
|-------|---------------|-------|
| **Unit tests** | Individual functions/classes | `unittest`, `pytest` |
| **Integration tests** | How components work together | `pytest` + fixtures |
| **Functional tests** | Complete features from user perspective | `selenium`, `playwright` |
| **End-to-end tests** | Full application workflow | `cypress`, `playwright` |

---

## 11.2 Testing with `unittest`

`unittest` is Python's built-in test framework:

```python
# File: test_calculator.py
import unittest
from calculator import add, divide

class TestCalculator(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)
    
    def test_add_floats(self):
        self.assertAlmostEqual(add(0.1, 0.2), 0.3)
    
    def test_divide(self):
        self.assertEqual(divide(10, 2), 5)
        self.assertEqual(divide(7, 2), 3.5)
    
    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)
    
    def test_divide_negative(self):
        self.assertEqual(divide(-10, 2), -5)

if __name__ == "__main__":
    unittest.main()
```

Run with:
```bash
python3 -m unittest test_calculator.py
python3 -m unittest discover  # Discover all tests
```

### Common `unittest` Assertions

```python
self.assertEqual(a, b)       # a == b
self.assertNotEqual(a, b)    # a != b
self.assertTrue(x)           # bool(x) is True
self.assertFalse(x)          # bool(x) is False
self.assertIs(a, b)          # a is b
self.assertIsNone(x)         # x is None
self.assertIn(a, b)          # a in b
self.assertNotIn(a, b)       # a not in b
self.assertAlmostEqual(a, b) # Floating point
self.assertRaises(Error, func, *args, **kwargs)
self.assertIsInstance(obj, cls)
```

### Test Fixtures — setUp and tearDown

```python
class TestDatabase(unittest.TestCase):
    def setUp(self):
        """Run before each test."""
        self.db = Database(":memory:")
        self.db.create_tables()
    
    def tearDown(self):
        """Run after each test."""
        self.db.close()
    
    @classmethod
    def setUpClass(cls):
        """Run once before all tests."""
        print("Starting database tests...")
    
    @classmethod
    def tearDownClass(cls):
        """Run once after all tests."""
        print("All database tests complete.")
    
    def test_insert(self):
        self.db.insert("users", {"name": "Alice"})
        result = self.db.query("SELECT * FROM users")
        self.assertEqual(len(result), 1)
```

---

## 11.3 Testing with `pytest`

`pytest` is a third-party testing framework (install with `pip install pytest`):

```python
# File: test_math_utils.py
from math_utils import add, is_prime, fibonacci

# Simple test functions (no class needed!)
def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0

def test_add_strings():
    assert add("Hello, ", "World") == "Hello, World"

# Test class (optional)
class TestPrime:
    def test_prime_numbers(self):
        assert is_prime(2) == True
        assert is_prime(17) == True
        assert is_prime(97) == True
    
    def test_non_prime(self):
        assert is_prime(1) == False
        assert is_prime(4) == False
        assert is_prime(100) == False
```

Run with:
```bash
pytest                  # Auto-discover tests
pytest -v               # Verbose
pytest test_file.py     # Specific file
pytest -k "prime"       # Filter by test name
pytest -x               # Stop on first failure
pytest --tb=short       # Short traceback
```

### pytest Fixtures

```python
import pytest

# Define fixture
@pytest.fixture
def sample_data():
    """Provide test data."""
    return {"name": "Alice", "age": 30, "items": [1, 2, 3]}

# Use fixture
class TestDataProcessing:
    def test_name(self, sample_data):
        assert sample_data["name"] == "Alice"
    
    def test_item_count(self, sample_data):
        assert len(sample_data["items"]) == 3

# Fixture with cleanup (using yield)
@pytest.fixture
def database():
    db = Database(":memory:")
    db.create_tables()
    yield db
    db.close()  # Cleanup

# Fixture scope
def test_using_db(database):
    database.insert("test", {"value": 1})
    assert database.count("test") == 1
```

### Fixture Scopes

```python
@pytest.fixture(scope="function")  # Default — ran per test function
@pytest.fixture(scope="class")      # Once per test class
@pytest.fixture(scope="module")     # Once per module
@pytest.fixture(scope="session")    # Once per test session
```

### Parametrized Tests

```python
import pytest

@pytest.mark.parametrize("a, b, expected", [
    (1, 2, 3),
    (0, 0, 0),
    (-1, 1, 0),
    (100, -50, 50),
])
def test_add(a, b, expected):
    assert add(a, b) == expected

# Multiple parameters
@pytest.mark.parametrize("value", [0, 1, 2, 3])
@pytest.mark.parametrize("multiplier", [1, 2])
def test_multiply(value, multiplier):
    assert multiply(value, multiplier) == value * multiplier
```

### pytest Markers

```python
import pytest

@pytest.mark.slow
def test_heavy_computation():
    # Slow test
    pass

@pytest.mark.skip(reason="Feature not implemented yet")
def test_future_feature():
    pass

@pytest.mark.skipif(sys.version_info < (3, 10), reason="Requires Python 3.10+")
def test_new_feature():
    pass

@pytest.mark.xfail(reason="Known bug")
def test_buggy_feature():
    assert broken_function() == 42

# Run: pytest -m slow
# Run: pytest -m "not slow"
```

---

## 11.4 Mocking

Mock objects replace real dependencies during testing:

```python
from unittest.mock import Mock, patch, MagicMock

# Simple mock
mocked_function = Mock(return_value=42)
assert mocked_function() == 42

# Mock with side effects
mocked_db = Mock()
mocked_db.query.side_effect = [
    [{"id": 1, "name": "Alice"}],  # First call
    [],  # Second call
]

# Verify interactions
mocked_function(1, 2, key="value")
mocked_function.assert_called_once()
mocked_function.assert_called_with(1, 2, key="value")

# Patching with decorator
@patch("my_module.external_api_call")
def test_get_data(mock_api_call):
    mock_api_call.return_value = {"status": "ok"}
    result = my_module.get_data()
    assert result["status"] == "ok"
    mock_api_call.assert_called_once()

# Patching with context manager
def test_file_operations():
    with patch("builtins.open") as mock_open:
        mock_open.return_value.__enter__.return_value.read.return_value = "test"
        result = process_file("dummy.txt")
        assert result == "test"

# Mocking time (useful for testing)
from unittest.mock import patch

@patch("time.time")
def test_timeout(mock_time):
    mock_time.side_effect = [0, 30, 60, 61]  # Elapsed seconds
    # Test timeout logic
```

### Mock Best Practices

```python
# DON'T mock what you don't own — mock your interface to the external system

# GOOD: Mock at the boundary
@patch("my_app.database.connection.execute")
def test_save_user(mock_execute):
    mock_execute.return_value = 1
    result = save_user({"name": "Alice"})
    assert result == 1

# BAD: Mock internal details
# @patch("my_app.database.connection._conn.cursor.execute")
```

---

## 11.5 Test-Driven Development (TDD)

**Red-Green-Refactor cycle:**

1. **Red**: Write a failing test
2. **Green**: Write minimal code to make it pass
3. **Refactor**: Improve code while keeping tests green

```python
# Step 1: Write test first
class TestFizzBuzz:
    def test_returns_number(self):
        assert fizzbuzz(1) == "1"
        assert fizzbuzz(2) == "2"
    
    def test_fizz(self):
        assert fizzbuzz(3) == "Fizz"
        assert fizzbuzz(6) == "Fizz"
    
    def test_buzz(self):
        assert fizzbuzz(5) == "Buzz"
        assert fizzbuzz(10) == "Buzz"
    
    def test_fizzbuzz(self):
        assert fizzbuzz(15) == "FizzBuzz"
        assert fizzbuzz(30) == "FizzBuzz"

# Step 2: Implement to pass tests
def fizzbuzz(n):
    result = ""
    if n % 3 == 0:
        result += "Fizz"
    if n % 5 == 0:
        result += "Buzz"
    return result or str(n)
```

---

## 11.6 Code Coverage

```bash
# Install coverage
pip install coverage

# Run with coverage
coverage run -m pytest
coverage report           # Terminal report
coverage html             # HTML report
coverage report -m        # Show missing lines

# Coverage configuration (.coveragerc)
# [run]
# source = my_project
# 
# [report]
# exclude_lines =
#     pragma: no cover
#     def __repr__
```

---

## 11.7 Doctests

Tests embedded in docstrings:

```python
import doctest

def add(a, b):
    """
    Add two numbers together.
    
    >>> add(2, 3)
    5
    >>> add(-1, 1)
    0
    >>> add(0, 0)
    0
    >>> add(0.1, 0.2)  # doctest: +ELLIPSIS
    0.3...
    """
    return a + b

def celsius_to_fahrenheit(celsius):
    """
    Convert Celsius to Fahrenheit.
    
    >>> celsius_to_fahrenheit(0)
    32.0
    >>> celsius_to_fahrenheit(100)
    212.0
    >>> celsius_to_fahrenheit(-40)
    -40.0
    """
    return (celsius * 9/5) + 32

if __name__ == "__main__":
    doctest.testmod(verbose=True)
```

---

## Key Takeaways

- **`unittest`** is built-in and great for standard testing
- **`pytest`** is more concise with simpler syntax (`assert` instead of `self.assertEqual`)
- **Fixtures** provide test setup and teardown with built-in dependency injection
- **Mocking** isolates code from external dependencies
- **Parametrization** tests multiple cases without code duplication
- **TDD** is a development practice, not a testing tool
- **Coverage** tools show untested code paths
- **Doctests** are great for simple examples in documentation

---

## Exercises

1. **Calculator tests**: Write `unittest` and `pytest` tests for a calculator module
2. **Mock an API**: Write tests for a function that calls an external API
3. **TDD exercise**: Implement a shopping cart using TDD (write tests first)
4. **Parametrize**: Write parametrized tests for a date validation function
5. **Mock file I/O**: Write tests for a CSV processor without creating actual files
6. **Coverage**: Measure coverage for a module and bring it to 100%

---

## Next Steps

→ Continue to [Chapter 12: Working with APIs & Web Scraping]({{< relref "12-apis-and-web-scraping" >}})
