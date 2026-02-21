# Common Errors: Preventing and Handling Programming Mistakes

## Introduction to Common Programming Errors

Programming errors are inevitable, but understanding common patterns allows developers to write more robust code. This guide covers frequent mistakes and strategies for prevention and handling.

## Syntax Errors

### Common Syntax Mistakes
```python
# Missing colon
if x > 5
    print("Big")  # SyntaxError: invalid syntax

# Incorrect indentation (Python requires consistency)
def function():
print("Hello")  # IndentationError: expected an indented block

# Mismatched quotes
message = "Hello, world!  # SyntaxError: EOL while scanning string literal

# Incorrect operator usage
if x = 5:  # SyntaxError: invalid syntax (assignment instead of comparison)
    print("Equal")

# Missing parentheses in function calls
print "Hello"  # SyntaxError: Missing parentheses in call

# Incorrect dictionary syntax
my_dict = {"key1": "value1" "key2": "value2"}  # SyntaxError: invalid syntax
```

### Prevention Strategies
```python
# Use a linter (like flake8 or pylint)
# pip install flake8
# flake8 your_file.py

# Use an IDE with syntax highlighting
# Most modern editors catch syntax errors immediately

# Write code in small chunks and test frequently
# This makes it easier to isolate syntax errors

def validate_syntax():
    """Basic syntax validation patterns."""
    try:
        # Test code compilation
        code = """
def test_function(x, y):
    if x > y:
        return x
    else:
        return y
"""
        compile(code, '<string>', 'exec')
        print("Syntax is valid")
    except SyntaxError as e:
        print(f"Syntax error: {e}")
        print(f"Line {e.lineno}: {e.text}")
```

## Runtime Errors

### Type Errors
```python
# Adding incompatible types
result = "Hello" + 5  # TypeError: can only concatenate str (not "int") to str

# Calling method on wrong type
numbers = [1, 2, 3]
numbers.length()  # AttributeError: 'list' object has no attribute 'length'

# Incorrect function arguments
len(5)  # TypeError: object of type 'int' has no len()

# Accessing undefined variable
print(undefined_variable)  # NameError: name 'undefined_variable' is not defined
```

### Value Errors
```python
# Converting invalid values
int("not_a_number")  # ValueError: invalid literal for int()

# Accessing out-of-range indices
my_list = [1, 2, 3]
my_list[10]  # IndexError: list index out of range

# Dictionary key errors
my_dict = {"a": 1}
my_dict["missing_key"]  # KeyError: 'missing_key'
```

### Prevention and Handling
```python
def safe_operations():
    """Demonstrate safe operation patterns."""

    # Safe type conversion
    def safe_int(value, default=0):
        try:
            return int(value)
        except (ValueError, TypeError):
            return default

    # Safe list access
    def safe_list_get(lst, index, default=None):
        try:
            return lst[index]
        except IndexError:
            return default

    # Safe dictionary access
    def safe_dict_get(dct, key, default=None):
        return dct.get(key, default)

    # Usage
    print(safe_int("42"))          # 42
    print(safe_int("not_number"))  # 0 (default)
    print(safe_list_get([1,2,3], 5, "not found"))  # "not found"
    print(safe_dict_get({"a": 1}, "b", "missing"))  # "missing"
```

## Logical Errors

### Off-by-One Errors
```python
# Common loop mistakes
numbers = [1, 2, 3, 4, 5]

# Wrong: includes index 5 which doesn't exist
for i in range(len(numbers) + 1):  # range(6) -> 0,1,2,3,4,5
    print(numbers[i])  # IndexError on i=5

# Wrong: excludes last element
for i in range(len(numbers) - 1):  # range(4) -> 0,1,2,3
    print(numbers[i])  # Misses element at index 4

# Correct
for i in range(len(numbers)):  # range(5) -> 0,1,2,3,4
    print(numbers[i])

# Better: use enumerate or iterate directly
for number in numbers:
    print(number)
```

### Boundary Condition Errors
```python
def is_valid_age(age):
    """Check if age is valid (should be 0-120)."""
    if age > 0 and age < 120:  # Wrong: excludes 0 and 120
        return True
    return False

def is_valid_age_fixed(age):
    """Correct age validation."""
    return 0 <= age <= 120

# Test boundary cases
print(is_valid_age(0))      # False (should be True)
print(is_valid_age(120))    # False (should be True)
print(is_valid_age_fixed(0))    # True
print(is_valid_age_fixed(120))  # True
```

### Floating Point Precision Issues
```python
# Dangerous floating point comparisons
a = 0.1 + 0.2
b = 0.3

print(a == b)  # False! (0.30000000000000004 != 0.3)

# Correct approaches
def float_equal(a, b, tolerance=1e-9):
    """Check if two floats are approximately equal."""
    return abs(a - b) < tolerance

print(float_equal(a, b))  # True

# Or use decimal for precise calculations
from decimal import Decimal, getcontext

getcontext().prec = 10  # Set precision
a = Decimal('0.1') + Decimal('0.2')
b = Decimal('0.3')
print(a == b)  # True
```

## Resource Management Errors

### File Handling Mistakes
```python
# Dangerous: file not properly closed if exception occurs
def read_file_dangerous(filename):
    file = open(filename, "r")
    content = file.read()
    file.close()  # Never reached if exception above
    return content

# Better: use context manager
def read_file_safe(filename):
    with open(filename, "r") as file:
        return file.read()

# Or manual cleanup
def read_file_manual(filename):
    file = None
    try:
        file = open(filename, "r")
        return file.read()
    finally:
        if file:
            file.close()
```

### Memory Leaks
```python
# Accumulating references
class MemoryLeak:
    def __init__(self):
        self.data = []

    def add_data(self, item):
        self.data.append(item)

# Usage that creates memory issues
objects = []
for i in range(1000):
    obj = MemoryLeak()
    obj.add_data([i] * 1000)  # Large data kept in memory
    objects.append(obj)

# Solution: clear references when done
del objects  # Allow garbage collection
```

## Concurrency Issues

### Race Conditions (in multi-threaded code)
```python
import threading

counter = 0

def increment_counter():
    global counter
    for _ in range(100000):
        counter += 1  # Not atomic - race condition!

threads = []
for _ in range(10):
    thread = threading.Thread(target=increment_counter)
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()

print(counter)  # Likely not 1,000,000 due to race condition

# Solution: use locks
counter = 0
lock = threading.Lock()

def increment_counter_safe():
    global counter
    for _ in range(100000):
        with lock:  # Atomic operation
            counter += 1

# Or use atomic operations (not shown - would require different approach)
```

## Data Validation Errors

### Input Validation Problems
```python
def process_user_age(age_str):
    """Process user age from string input."""
    age = int(age_str)  # What if age_str is not numeric?

    if age < 0:
        raise ValueError("Age cannot be negative")

    return age

# Better validation
def process_user_age_safe(age_input):
    """Safely process user age."""
    try:
        age = int(age_input)
    except ValueError:
        raise ValueError(f"Invalid age format: {age_input}")

    if not 0 <= age <= 150:
        raise ValueError(f"Age must be between 0 and 150, got {age}")

    return age

# Usage
try:
    age = process_user_age_safe("25")
    print(f"Age: {age}")
except ValueError as e:
    print(f"Error: {e}")
```

### SQL Injection Vulnerabilities
```python
# Dangerous - SQL injection possible
def get_user_bad(username):
    query = f"SELECT * FROM users WHERE username = '{username}'"
    # If username is "'; DROP TABLE users; --"
    # This becomes: SELECT * FROM users WHERE username = ''; DROP TABLE users; --'
    return execute_query(query)

# Safe - use parameterized queries
def get_user_safe(username):
    query = "SELECT * FROM users WHERE username = ?"
    return execute_query(query, (username,))  # Parameters separate from SQL
```

## Algorithm Errors

### Incorrect Loop Logic
```python
# Finding maximum - common mistakes
def find_max_broken(numbers):
    """Broken implementation."""
    if not numbers:
        return None

    max_val = numbers[0]
    for num in numbers:  # Includes first element again
        if num > max_val:
            max_val = num
    return max_val  # Correct result, but inefficient

def find_max_correct(numbers):
    """Correct implementation."""
    if not numbers:
        return None

    max_val = numbers[0]
    for num in numbers[1:]:  # Skip first element
        if num > max_val:
            max_val = num
    return max_val
```

### Infinite Loops
```python
# Accidental infinite loop
def countdown_broken(n):
    while n > 0:
        print(n)
        # Forgot to decrement n!

# Fixed
def countdown_fixed(n):
    while n > 0:
        print(n)
        n -= 1

# Another common mistake
def process_list_broken(items):
    i = 0
    while i < len(items):
        if items[i] == "skip":
            continue  # i not incremented!
        print(items[i])
        i += 1

# Fixed
def process_list_fixed(items):
    i = 0
    while i < len(items):
        if items[i] == "skip":
            i += 1
            continue
        print(items[i])
        i += 1
```

## Import and Module Errors

### Circular Import Issues
```python
# module_a.py
from module_b import function_b

def function_a():
    return function_b()

# module_b.py
from module_a import function_a  # Circular import!

def function_b():
    return function_a()

# Solution: Import inside functions or restructure
# module_a.py
def function_a():
    from module_b import function_b
    return function_b()

# module_b.py
def function_b():
    from module_a import function_a
    return function_a()
```

### Name Collision Problems
```python
# Shadowing built-in functions
list = [1, 2, 3]  # Shadows built-in list()
my_list = list((4, 5, 6))  # TypeError: 'list' object is not callable

# Fixed
my_list_data = [1, 2, 3]
my_tuple = (4, 5, 6)
my_list = list(my_tuple)  # Use built-in list
```

## Testing and Validation Strategies

### Unit Testing for Error Prevention
```python
import pytest

def add_numbers(a, b):
    """Add two numbers."""
    return a + b

def test_add_numbers():
    """Test add_numbers function."""
    # Normal cases
    assert add_numbers(2, 3) == 5
    assert add_numbers(-1, 1) == 0
    assert add_numbers(0.5, 0.5) == 1.0

    # Edge cases
    assert add_numbers(0, 0) == 0

def test_add_numbers_errors():
    """Test error handling."""
    # This should work - dynamic typing allows it
    result = add_numbers("hello", "world")
    assert result == "helloworld"

# Run tests
if __name__ == "__main__":
    test_add_numbers()
    test_add_numbers_errors()
    print("All tests passed!")
```

### Defensive Programming
```python
def robust_divide(dividend, divisor):
    """Divide with comprehensive error checking."""
    # Type checking
    if not isinstance(dividend, (int, float)):
        raise TypeError("Dividend must be a number")
    if not isinstance(divisor, (int, float)):
        raise TypeError("Divisor must be a number")

    # Value checking
    if divisor == 0:
        raise ValueError("Cannot divide by zero")

    # Handle special cases
    if dividend == 0:
        return 0

    return dividend / divisor

def test_robust_divide():
    """Test robust_divide with various inputs."""
    # Normal cases
    assert robust_divide(10, 2) == 5.0

    # Error cases
    try:
        robust_divide(10, 0)
        assert False, "Should raise ValueError"
    except ValueError:
        pass

    try:
        robust_divide("10", 2)
        assert False, "Should raise TypeError"
    except TypeError:
        pass

test_robust_divide()
```

## Error Recovery Patterns

### Graceful Degradation
```python
def load_configuration(filename="config.json"):
    """Load configuration with fallback options."""
    import json
    import os

    # Try primary configuration file
    if os.path.exists(filename):
        try:
            with open(filename, 'r') as f:
                return json.load(f)
        except (json.JSONDecodeError, IOError) as e:
            print(f"Error loading {filename}: {e}")

    # Fallback to environment variables
    config = {}
    config['database_url'] = os.getenv('DATABASE_URL', 'sqlite:///default.db')
    config['debug'] = os.getenv('DEBUG', 'False').lower() == 'true'

    print("Using fallback configuration")
    return config
```

### Retry Mechanisms
```python
import time
import random

def unreliable_operation():
    """Simulate operation that might fail."""
    if random.random() < 0.7:
        raise Exception("Temporary failure")
    return "Success"

def retry_operation(operation, max_attempts=3, delay=1):
    """Retry operation with exponential backoff."""
    for attempt in range(max_attempts):
        try:
            return operation()
        except Exception as e:
            if attempt == max_attempts - 1:
                raise e
            print(f"Attempt {attempt + 1} failed: {e}")
            time.sleep(delay * (2 ** attempt))  # Exponential backoff

    raise Exception("All retry attempts failed")

# Usage
try:
    result = retry_operation(unreliable_operation)
    print(f"Operation succeeded: {result}")
except Exception as e:
    print(f"Operation failed: {e}")
```

## Key Takeaways

1. **Syntax errors** are caught by the parser before execution
2. **Runtime errors** occur during program execution and need handling
3. **Logical errors** produce incorrect results but don't crash the program
4. **Defensive programming** anticipates and handles potential errors
5. **Testing** helps catch errors before they reach production
6. **Graceful error handling** improves user experience

## Further Reading
- Python exception hierarchy
- Unit testing best practices
- Defensive programming techniques
- Error handling patterns in different languages
- Debugging and troubleshooting guides