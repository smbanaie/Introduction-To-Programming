# Exception Handling: Managing Errors Gracefully

## Introduction to Exceptions

Exceptions are events that occur during program execution that disrupt the normal flow of instructions. Python uses exceptions to signal that something unexpected happened, allowing programs to respond appropriately rather than crashing.

## Basic Exception Handling

### try-except Block
```python
try:
    # Code that might raise an exception
    result = 10 / 0
    print("This line won't execute")
except ZeroDivisionError:
    # Code to handle the exception
    print("Cannot divide by zero!")

print("Program continues after exception handling")
```

### Catching Multiple Exceptions
```python
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    except TypeError:
        return "Both arguments must be numbers"
    except Exception as e:
        return f"An unexpected error occurred: {e}"

print(safe_divide(10, 2))      # 5.0
print(safe_divide(10, 0))      # "Cannot divide by zero"
print(safe_divide(10, "2"))    # "Both arguments must be numbers"
```

### Generic Exception Handling
```python
try:
    # Risky operations
    with open("file.txt", "r") as f:
        data = f.read()
    result = int(data.strip())
except Exception as e:
    # Catch any exception
    print(f"An error occurred: {e}")
    result = None

print(f"Result: {result}")
```

## Exception Hierarchy

### Built-in Exception Types
```python
# Common exceptions you'll encounter:

# ValueError - Invalid value for operation
int("not_a_number")  # ValueError

# TypeError - Operation on incompatible types
"string" + 5         # TypeError

# KeyError - Dictionary key not found
my_dict = {}
my_dict["missing"]   # KeyError

# IndexError - List index out of range
my_list = [1, 2, 3]
my_list[10]          # IndexError

# FileNotFoundError - File doesn't exist
open("nonexistent.txt")  # FileNotFoundError

# ZeroDivisionError - Division by zero
10 / 0               # ZeroDivisionError

# AttributeError - Object doesn't have attribute
obj = "string"
obj.some_method()    # AttributeError
```

### Custom Exceptions
```python
class InsufficientFundsError(Exception):
    """Raised when account has insufficient funds."""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Insufficient funds: balance ${balance}, needed ${amount}")

class InvalidAmountError(Exception):
    """Raised when transaction amount is invalid."""
    pass

def withdraw_money(account, amount):
    if amount <= 0:
        raise InvalidAmountError("Withdrawal amount must be positive")

    if amount > account.balance:
        raise InsufficientFundsError(account.balance, amount)

    account.balance -= amount
    return account.balance

# Usage
account = type('Account', (), {'balance': 100})()

try:
    withdraw_money(account, 150)
except InsufficientFundsError as e:
    print(f"Transaction failed: {e}")
except InvalidAmountError as e:
    print(f"Invalid amount: {e}")
```

## Exception Handling Patterns

### finally Block
```python
def read_file_with_cleanup(filename):
    file = None
    try:
        file = open(filename, "r")
        content = file.read()
        return content
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
    finally:
        # This always executes, even if exception occurs
        if file:
            file.close()
            print("File closed")

# Better approach using context manager
def read_file_context_manager(filename):
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
    # File automatically closed here
```

### else Block
```python
def process_data(data):
    try:
        # Try to process
        result = int(data)
    except ValueError:
        print("Invalid number format")
        return None
    else:
        # Only executes if no exception occurred
        print(f"Successfully processed: {result}")
        return result * 2
    finally:
        # Always executes
        print("Processing complete")

process_data("42")      # Success path
process_data("invalid") # Error path
```

### Exception Chaining
```python
def process_user_data(raw_data):
    try:
        # Parse JSON
        import json
        data = json.loads(raw_data)

        # Validate required fields
        if "name" not in data:
            raise ValueError("Missing required field: name")

        if "age" not in data:
            raise ValueError("Missing required field: age")

        # Validate age
        age = data["age"]
        if not isinstance(age, int) or age < 0:
            raise ValueError("Age must be a positive integer")

        return data

    except json.JSONDecodeError as e:
        raise ValueError(f"Invalid JSON format: {e}") from e
    except KeyError as e:
        raise ValueError(f"Missing required field: {e}") from e
```

## Context Managers and Resources

### Manual Resource Management
```python
def risky_file_operation(filename):
    file_handle = None
    try:
        file_handle = open(filename, "r")
        content = file_handle.read()
        # Process content...
        return len(content)
    except FileNotFoundError:
        print(f"File {filename} not found")
        return 0
    except PermissionError:
        print(f"Permission denied for {filename}")
        return 0
    finally:
        # Ensure file is closed even if exception occurs
        if file_handle:
            file_handle.close()
```

### Context Manager Pattern
```python
class DatabaseConnection:
    def __init__(self, config):
        self.config = config
        self.connection = None

    def __enter__(self):
        # Setup - acquire resource
        self.connection = self._connect()
        return self.connection

    def __exit__(self, exc_type, exc_val, exc_tb):
        # Cleanup - release resource
        if self.connection:
            self.connection.close()

    def _connect(self):
        # Simulate database connection
        print(f"Connecting to database: {self.config}")
        return "database_connection_object"

# Usage
config = {"host": "localhost", "port": 5432}

try:
    with DatabaseConnection(config) as conn:
        # Use connection
        print(f"Using connection: {conn}")
        # Perform database operations...
except Exception as e:
    print(f"Database operation failed: {e}")
# Connection automatically closed here
```

### Built-in Context Managers
```python
# File operations
try:
    with open("data.txt", "r") as file:
        data = file.read()
        # Process data...
except FileNotFoundError:
    print("File not found")

# Multiple resources
try:
    with open("input.txt", "r") as input_file, \
         open("output.txt", "w") as output_file:

        for line in input_file:
            # Process line
            processed = line.upper()
            output_file.write(processed)

except IOError as e:
    print(f"File operation failed: {e}")
```

## Exception Handling Best Practices

### Specific Exception Types
```python
# Bad - catches everything
try:
    risky_operation()
except Exception:
    print("Something went wrong")

# Good - catches specific exceptions
try:
    risky_operation()
except ValueError:
    print("Invalid value provided")
except ConnectionError:
    print("Network connection failed")
except Exception as e:
    print(f"Unexpected error: {e}")
```

### Avoid Bare except Clauses
```python
# Bad - catches system exit and keyboard interrupt
try:
    do_something()
except:
    print("Error occurred")

# Better - be specific
try:
    do_something()
except ValueError:
    handle_value_error()
except (IOError, OSError):
    handle_io_error()

# If you must catch everything, be explicit
try:
    do_something()
except Exception:
    handle_general_error()
```

### Preserve Exception Information
```python
# Bad - loses original exception
try:
    risky_call()
except ValueError:
    raise RuntimeError("Something failed")

# Good - chains exceptions
try:
    risky_call()
except ValueError as e:
    raise RuntimeError("Something failed") from e

# Even better - re-raise with context
try:
    risky_call()
except ValueError as e:
    raise RuntimeError(f"Something failed while processing: {e}") from e
```

### Resource Management
```python
# Bad - resource leak possible
file = open("data.txt", "r")
try:
    data = file.read()
finally:
    file.close()  # Might not execute if exception in try

# Good - use context manager
with open("data.txt", "r") as file:
    data = file.read()  # Automatically closed
```

## Common Error Scenarios and Solutions

### Network Operations
```python
import requests
from requests.exceptions import RequestException, Timeout, ConnectionError

def fetch_user_data(user_id):
    try:
        response = requests.get(f"https://api.example.com/users/{user_id}", timeout=5)
        response.raise_for_status()  # Raise for HTTP error codes
        return response.json()
    except Timeout:
        print("Request timed out")
        return None
    except ConnectionError:
        print("Network connection failed")
        return None
    except requests.exceptions.HTTPError as e:
        print(f"HTTP error: {e}")
        return None
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return None
```

### Database Operations
```python
import sqlite3

def get_user_balance(user_id):
    try:
        conn = sqlite3.connect("bank.db")
        cursor = conn.cursor()

        cursor.execute("SELECT balance FROM accounts WHERE id = ?", (user_id,))
        result = cursor.fetchone()

        if result is None:
            raise ValueError(f"User {user_id} not found")

        return result[0]

    except sqlite3.OperationalError as e:
        print(f"Database operation failed: {e}")
        raise
    except sqlite3.IntegrityError as e:
        print(f"Data integrity error: {e}")
        raise
    finally:
        if 'conn' in locals():
            conn.close()
```

### Mathematical Operations
```python
def safe_calculate(expression):
    """Safely evaluate mathematical expression."""
    try:
        # Only allow safe operations
        allowed_names = {
            "abs": abs, "round": round, "min": min, "max": max,
            "__builtins__": {}  # Disable built-ins for security
        }

        result = eval(expression, allowed_names)
        return result

    except ZeroDivisionError:
        return "Division by zero"
    except NameError:
        return "Invalid function or variable name"
    except (TypeError, SyntaxError):
        return "Invalid expression syntax"
    except Exception as e:
        return f"Calculation error: {e}"

print(safe_calculate("10 / 2"))        # 5.0
print(safe_calculate("10 / 0"))        # "Division by zero"
print(safe_calculate("import os"))     # "Invalid function or variable name"
print(safe_calculate("10 + 'text'"))   # "Invalid expression syntax"
```

## Testing Exception Handling

### Unit Testing Exceptions
```python
import pytest

def test_safe_divide():
    """Test safe_divide function."""
    from my_module import safe_divide

    # Normal cases
    assert safe_divide(10, 2) == 5.0
    assert safe_divide(10, 5) == 2.0

    # Error cases
    assert safe_divide(10, 0) == "Cannot divide by zero"
    assert safe_divide("10", 2) == "Both arguments must be numbers"

def test_exceptions_with_pytest():
    """Test that exceptions are raised correctly."""

    def risky_function(value):
        if value < 0:
            raise ValueError("Value must be non-negative")
        return value * 2

    # Test normal operation
    assert risky_function(5) == 10

    # Test exception is raised
    with pytest.raises(ValueError, match="must be non-negative"):
        risky_function(-1)
```

### Integration Testing
```python
def test_file_processing_integration():
    """Test file processing with various error conditions."""
    import tempfile
    import os

    # Test with valid file
    with tempfile.NamedTemporaryFile(mode='w', delete=False) as f:
        f.write("test data")
        temp_filename = f.name

    try:
        result = process_file(temp_filename)
        assert result is not None
    finally:
        os.unlink(temp_filename)

    # Test with missing file
    result = process_file("nonexistent_file.txt")
    assert result is None or isinstance(result, str)  # Should handle gracefully
```

## Performance Considerations

### Exception Handling Overhead
```python
# Exceptions have performance cost - use for exceptional cases only
def find_item(items, target):
    """Find item in list."""
    try:
        return items.index(target)
    except ValueError:
        return -1

# For frequent operations, use conditional checks instead
def find_item_efficient(items, target):
    """Find item in list efficiently."""
    for i, item in enumerate(items):
        if item == target:
            return i
    return -1
```

### Logging vs Raising Exceptions
```python
import logging

def process_data(data):
    """Process data with appropriate error handling."""
    try:
        # Attempt processing
        result = risky_operation(data)
        return result
    except ValueError as e:
        # Log and continue for recoverable errors
        logging.warning(f"Data validation failed: {e}")
        return get_default_value()
    except Exception as e:
        # Re-raise for serious errors
        logging.error(f"Critical error in data processing: {e}")
        raise
```

## Key Takeaways

1. **Exceptions handle unexpected events** without crashing programs
2. **Specific exception types** provide better error handling than generic catching
3. **finally blocks** ensure cleanup code always runs
4. **Context managers** automatically handle resource cleanup
5. **Custom exceptions** provide meaningful error messages
6. **Testing exception handling** ensures robust error recovery

## Further Reading
- Python exception hierarchy documentation
- Context manager protocol
- Logging best practices
- Error handling patterns in different programming paradigms
- Defensive programming techniques