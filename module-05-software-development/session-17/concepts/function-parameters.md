# Function Parameters: Advanced Argument Handling

## Parameter Types and Passing Mechanisms

Python functions support various parameter types and argument passing mechanisms that provide flexibility in how functions can be called and used.

## Positional vs Keyword Arguments

### Positional Arguments
```python
def create_user(username, email, age):
    """Create a user with positional arguments."""
    return {
        "username": username,
        "email": email,
        "age": age
    }

# Must be called in exact order
user1 = create_user("alice123", "alice@email.com", 25)
user2 = create_user("bob456", "bob@email.com", 30)
```

### Keyword Arguments
```python
# Same function, called with keyword arguments
user3 = create_user(
    username="charlie789",
    email="charlie@email.com",
    age=35
)

# Order doesn't matter with keyword arguments
user4 = create_user(
    age=28,
    username="diana101",
    email="diana@email.com"
)

# Mix positional and keyword (positional first)
user5 = create_user("eve202", email="eve@email.com", age=32)
```

## Default Parameter Values

### Basic Default Values
```python
def send_email(to, subject, body="", priority="normal"):
    """Send an email with default values."""
    email = {
        "to": to,
        "subject": subject,
        "body": body,
        "priority": priority
    }
    print(f"Sending email: {email}")
    return True

# Use defaults
send_email("user@example.com", "Welcome!")

# Override some defaults
send_email("user@example.com", "Alert", "System maintenance tonight", "high")

# Override all
send_email("user@example.com", "Invoice", "Your bill is ready", "normal")
```

### Default Value Considerations
```python
# Problematic - mutable default argument
def add_item(item, shopping_list=[]):
    """Add item to shopping list (problematic version)."""
    shopping_list.append(item)
    return shopping_list

# Unexpected behavior
list1 = add_item("apples")
print(list1)  # ['apples']

list2 = add_item("bananas")
print(list2)  # ['apples', 'bananas'] - same list!

# Fixed version
def add_item_fixed(item, shopping_list=None):
    """Add item to shopping list (correct version)."""
    if shopping_list is None:
        shopping_list = []
    shopping_list.append(item)
    return shopping_list

list3 = add_item_fixed("apples")
list4 = add_item_fixed("bananas")
print(list3)  # ['apples']
print(list4)  # ['bananas']
```

### Default Values Evaluation
```python
import time

def log_message(message, timestamp=None):
    """Log a message with timestamp."""
    if timestamp is None:
        timestamp = time.time()  # Evaluated when function is called
    print(f"[{timestamp}] {message}")

# Each call gets different timestamp
log_message("Starting process")
time.sleep(1)
log_message("Process complete")

# Bad - evaluated only once when function is defined
def log_message_bad(message, timestamp=time.time()):
    """This is problematic."""
    print(f"[{timestamp}] {message}")

# Both calls use same timestamp
log_message_bad("First message")
log_message_bad("Second message")
```

## Variable-Length Arguments

### *args - Variable Positional Arguments
```python
def sum_numbers(*numbers):
    """Sum any number of arguments."""
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_numbers(1, 2, 3))           # 6
print(sum_numbers(10, 20, 30, 40))    # 100
print(sum_numbers())                  # 0

# Unpacking arguments
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
result = add(*numbers)  # Equivalent to add(1, 2, 3)
print(result)  # 6
```

### **kwargs - Variable Keyword Arguments
```python
def create_config(**settings):
    """Create configuration from keyword arguments."""
    config = {"debug": False, "timeout": 30}  # defaults
    config.update(settings)  # override with provided settings
    return config

config1 = create_config(host="localhost", port=8080)
config2 = create_config(debug=True, timeout=60, host="prod.example.com")

print(config1)  # {'debug': False, 'timeout': 30, 'host': 'localhost', 'port': 8080}
print(config2)  # {'debug': True, 'timeout': 60, 'host': 'prod.example.com'}
```

### Combining *args and **kwargs
```python
def flexible_function(required_arg, *args, default_param="default", **kwargs):
    """Function with all parameter types."""
    print(f"Required: {required_arg}")
    print(f"Args: {args}")
    print(f"Default: {default_param}")
    print(f"Kwargs: {kwargs}")

# Various calling styles
flexible_function("hello")
flexible_function("hello", 1, 2, 3)
flexible_function("hello", 1, 2, 3, default_param="changed")
flexible_function("hello", 1, 2, 3, extra="data", more="info")
```

## Argument Unpacking

### Unpacking Lists/Tuples
```python
def calculate_area(length, width):
    return length * width

# Direct call
area1 = calculate_area(5, 3)

# Unpack from sequence
dimensions = [5, 3]
area2 = calculate_area(*dimensions)  # Same as calculate_area(5, 3)

# Unpack with additional arguments
base_dimensions = [5, 3]
area3 = calculate_area(*base_dimensions)  # Still works
```

### Unpacking Dictionaries
```python
def configure_server(host, port, ssl=True, debug=False):
    return {
        "host": host,
        "port": port,
        "ssl": ssl,
        "debug": debug
    }

# Unpack dictionary
config = {"host": "localhost", "port": 8080, "ssl": False}
server_config = configure_server(**config)

print(server_config)
# {'host': 'localhost', 'port': 8080, 'ssl': False, 'debug': False}
```

## Parameter Validation and Type Checking

### Manual Validation
```python
def divide(a, b):
    """Divide two numbers with validation."""
    if not isinstance(a, (int, float)):
        raise TypeError("First argument must be a number")
    if not isinstance(b, (int, float)):
        raise TypeError("Second argument must be a number")
    if b == 0:
        raise ValueError("Cannot divide by zero")

    return a / b

try:
    result = divide(10, 2)
    print(f"Result: {result}")
except (TypeError, ValueError) as e:
    print(f"Error: {e}")
```

### Using Type Hints and Validation
```python
from typing import Union, Optional

def calculate_tax(income: Union[int, float], tax_rate: float = 0.2) -> float:
    """Calculate tax with type hints."""
    if not isinstance(income, (int, float)):
        raise TypeError("Income must be a number")
    if not isinstance(tax_rate, float):
        raise TypeError("Tax rate must be a float")
    if income < 0:
        raise ValueError("Income cannot be negative")
    if not 0 <= tax_rate <= 1:
        raise ValueError("Tax rate must be between 0 and 1")

    return income * tax_rate

try:
    tax = calculate_tax(50000, 0.25)
    print(f"Tax: ${tax}")
except (TypeError, ValueError) as e:
    print(f"Error: {e}")
```

## Function Overloading Patterns

### Parameter-Based Behavior
```python
def process_data(data, operation="sum"):
    """Process data based on operation parameter."""
    if operation == "sum":
        return sum(data)
    elif operation == "average":
        return sum(data) / len(data)
    elif operation == "max":
        return max(data)
    elif operation == "min":
        return min(data)
    else:
        raise ValueError(f"Unknown operation: {operation}")

numbers = [1, 2, 3, 4, 5]
print(process_data(numbers, "sum"))      # 15
print(process_data(numbers, "average"))  # 3.0
print(process_data(numbers, "max"))      # 5
```

### Union Types and Optional Parameters
```python
from typing import List, Union

def format_output(data: Union[str, List[str]], separator: str = ", ") -> str:
    """Format output as string."""
    if isinstance(data, str):
        return data
    elif isinstance(data, list):
        return separator.join(data)
    else:
        raise TypeError("Data must be string or list of strings")

print(format_output("Hello World"))              # "Hello World"
print(format_output(["apple", "banana", "cherry"]))  # "apple, banana, cherry"
print(format_output(["a", "b", "c"], " | "))     # "a | b | c"
```

## Advanced Parameter Patterns

### Callbacks and Function Parameters
```python
def apply_operation(data: List[int], operation) -> List[int]:
    """Apply an operation to each element."""
    return [operation(x) for x in data]

def double(x):
    return x * 2

def square(x):
    return x ** 2

numbers = [1, 2, 3, 4, 5]
doubled = apply_operation(numbers, double)
squared = apply_operation(numbers, square)

print(doubled)  # [2, 4, 6, 8, 10]
print(squared)  # [1, 4, 9, 16, 25]

# Using lambda functions
tripled = apply_operation(numbers, lambda x: x * 3)
print(tripled)  # [3, 6, 9, 12, 15]
```

### Factory Functions
```python
def create_multiplier(factor):
    """Create a function that multiplies by a specific factor."""
    def multiplier(number):
        return number * factor
    return multiplier

double = create_multiplier(2)
triple = create_multiplier(3)
quadruple = create_multiplier(4)

print(double(5))     # 10
print(triple(5))     # 15
print(quadruple(5))  # 20
```

### Parameter Dependency Injection
```python
def create_api_client(api_key: str, base_url: str = "https://api.example.com"):
    """Create an API client with configuration."""

    def make_request(endpoint: str, method: str = "GET", data: dict = None):
        """Make API request."""
        url = f"{base_url}/{endpoint}"
        headers = {"Authorization": f"Bearer {api_key}"}

        # Simulate API call
        return {
            "url": url,
            "method": method,
            "headers": headers,
            "data": data or {}
        }

    return make_request

# Create configured client
api_client = create_api_client("my-secret-key")

# Use the client
response1 = api_client("users")
response2 = api_client("posts", "POST", {"title": "New Post"})

print(response1["url"])  # "https://api.example.com/users"
print(response2["method"])  # "POST"
```

## Best Practices for Function Parameters

### Clear Parameter Names
```python
# Good - descriptive names
def calculate_payment(principal: float, annual_rate: float, months: int) -> float:
    pass

# Bad - unclear abbreviations
def calc_pmt(p: float, r: float, m: int) -> float:
    pass
```

### Consistent Parameter Ordering
```python
# Good - consistent order across related functions
def save_user(name: str, email: str, password: str):
    pass

def update_user(user_id: int, name: str = None, email: str = None):
    pass

# Bad - inconsistent order
def save_user(name, password, email):  # email last
    pass

def update_user(name, user_id, email):  # email first after name
    pass
```

### Avoid Too Many Parameters
```python
# Good - use data structure for many related parameters
def create_report(config: dict):
    """Create report with configuration."""
    title = config.get("title", "Report")
    date_range = config.get("date_range")
    filters = config.get("filters", {})
    # ...

# Bad - too many parameters
def create_report(title, start_date, end_date, filter_by_status,
                  filter_by_type, include_charts, export_format):
    pass

# Use a configuration object instead
```

### Parameter Documentation
```python
def process_payment(amount: float, currency: str = "USD",
                   description: str = "", metadata: dict = None) -> dict:
    """
    Process a payment.

    Args:
        amount: Payment amount (must be positive)
        currency: Three-letter currency code (e.g., 'USD', 'EUR')
        description: Optional payment description
        metadata: Optional additional data as key-value pairs

    Returns:
        Dictionary with payment details and status

    Raises:
        ValueError: If amount is not positive or currency is invalid
    """
    # Implementation...
    pass
```

## Parameter Testing Strategies

### Equivalence Classes
```python
def test_calculate_tax():
    """Test calculate_tax with different input classes."""

    # Valid inputs
    assert calculate_tax(50000, 0.2) == 10000
    assert calculate_tax(0, 0.2) == 0

    # Boundary values
    assert calculate_tax(0.01, 0.2) == 0.002

    # Invalid inputs (should raise exceptions)
    try:
        calculate_tax(-1000, 0.2)
        assert False, "Should raise ValueError for negative income"
    except ValueError:
        pass

def calculate_tax(income: float, rate: float) -> float:
    """Calculate tax."""
    if income < 0:
        raise ValueError("Income cannot be negative")
    if not 0 <= rate <= 1:
        raise ValueError("Rate must be between 0 and 1")
    return income * rate

test_calculate_tax()
print("All tests passed!")
```

## Key Takeaways

1. **Parameter types provide flexibility** in how functions can be called
2. **Default values make parameters optional** but require careful handling
3. **Variable-length arguments** (*args, **kwargs) handle arbitrary inputs
4. **Argument unpacking** allows passing collections as individual arguments
5. **Parameter validation** ensures function reliability
6. **Clear naming and documentation** improve code maintainability

## Further Reading
- Python parameter passing mechanisms
- Type hinting best practices
- Function composition patterns
- Testing strategies for parameterized functions