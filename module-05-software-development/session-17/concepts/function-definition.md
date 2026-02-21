# Function Definition: Creating Reusable Code Blocks

## Introduction to Functions

Functions are reusable blocks of code that perform specific tasks. They allow you to break complex programs into smaller, manageable pieces, making code more organized, readable, and maintainable.

## Basic Function Definition

### Function Syntax
```python
def function_name():
    """Optional docstring describing what the function does."""
    # Function body - the code that executes
    print("Hello from inside the function!")
    return  # Optional return statement
```

### Calling Functions
```python
# Define the function
def greet_user():
    print("Hello, welcome to our program!")

# Call the function
greet_user()  # Output: Hello, welcome to our program!
greet_user()  # Can be called multiple times
```

## Function Parameters

### Positional Parameters
```python
def greet_person(name):
    """Greet a person by name."""
    print(f"Hello, {name}!")

# Call with argument
greet_person("Alice")   # Output: Hello, Alice!
greet_person("Bob")     # Output: Hello, Bob!
```

### Multiple Parameters
```python
def introduce_person(name, age, city):
    """Introduce a person with their details."""
    print(f"This is {name}, who is {age} years old and lives in {city}.")

introduce_person("Alice", 25, "New York")
introduce_person("Bob", 30, "London")
```

### Default Parameter Values
```python
def greet_with_time(name, time_of_day="morning"):
    """Greet someone with time of day."""
    print(f"Good {time_of_day}, {name}!")

greet_with_time("Alice")                    # Good morning, Alice!
greet_with_time("Bob", "afternoon")         # Good afternoon, Bob!
greet_with_time("Charlie", "evening")       # Good evening, Charlie!
```

### Keyword Arguments
```python
def create_profile(name, age, city, profession=None):
    """Create a user profile."""
    profile = {
        "name": name,
        "age": age,
        "city": city
    }
    if profession:
        profile["profession"] = profession
    return profile

# Using positional arguments
profile1 = create_profile("Alice", 25, "NYC", "Engineer")

# Using keyword arguments (more readable)
profile2 = create_profile(
    name="Bob",
    age=30,
    city="London",
    profession="Designer"
)

# Mixing positional and keyword
profile3 = create_profile("Charlie", 35, city="Paris", profession="Artist")
```

## Return Values

### Returning Single Values
```python
def calculate_square(number):
    """Return the square of a number."""
    return number ** 2

result = calculate_square(5)  # result = 25
print(result)                 # Output: 25
```

### Returning Multiple Values
```python
def get_user_info():
    """Return multiple pieces of information."""
    name = "Alice"
    age = 25
    city = "New York"
    return name, age, city

# Unpack the returned tuple
user_name, user_age, user_city = get_user_info()
print(f"{user_name} is {user_age} and lives in {user_city}")

# Or receive as a single tuple
info = get_user_info()
print(info)  # ('Alice', 25, 'New York')
```

### Early Returns
```python
def divide_numbers(a, b):
    """Divide two numbers with error checking."""
    if b == 0:
        return "Error: Cannot divide by zero"

    if not isinstance(a, (int, float)) or not isinstance(b, (int, float)):
        return "Error: Both arguments must be numbers"

    return a / b

print(divide_numbers(10, 2))      # 5.0
print(divide_numbers(10, 0))      # Error: Cannot divide by zero
print(divide_numbers(10, "2"))    # Error: Both arguments must be numbers
```

## Function Scope and Variables

### Local vs Global Scope
```python
# Global variable
global_counter = 0

def increment_counter():
    """Increment a global counter."""
    global global_counter  # Declare we're using the global variable
    global_counter += 1
    print(f"Counter is now: {global_counter}")

increment_counter()  # Counter is now: 1
increment_counter()  # Counter is now: 2

print(global_counter)  # 2 (accessible globally)
```

### Local Variables
```python
def calculate_area(length, width):
    """Calculate rectangle area."""
    # Local variables only exist inside this function
    area = length * width
    perimeter = 2 * (length + width)

    print(f"Area: {area}")
    print(f"Perimeter: {perimeter}")

    return area

result = calculate_area(5, 3)
# Inside function: Area: 15, Perimeter: 16

# These variables are not accessible here
# print(area)  # NameError: name 'area' is not defined
```

### Nested Functions and Closures
```python
def create_multiplier(factor):
    """Create a function that multiplies by a specific factor."""
    def multiplier(number):
        return number * factor
    return multiplier

# Create specialized multiplier functions
double = create_multiplier(2)
triple = create_multiplier(3)

print(double(5))  # 10
print(triple(5))  # 15

# The factor variable is "closed over" and remembered
print(double(10)) # 20
```

## Function Arguments Advanced

### Variable-Length Arguments (*args)
```python
def sum_all(*numbers):
    """Sum any number of arguments."""
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))        # 6
print(sum_all(10, 20, 30, 40)) # 100
print(sum_all())               # 0 (no arguments)
```

### Keyword Variable-Length Arguments (**kwargs)
```python
def create_person(**info):
    """Create a person dictionary from keyword arguments."""
    person = {}
    for key, value in info.items():
        person[key] = value
    return person

person1 = create_person(name="Alice", age=25, city="NYC")
person2 = create_person(name="Bob", profession="Engineer", salary=75000)

print(person1)  # {'name': 'Alice', 'age': 25, 'city': 'NYC'}
print(person2)  # {'name': 'Bob', 'profession': 'Engineer', 'salary': 75000}
```

### Combining All Parameter Types
```python
def complex_function(required, *args, default="value", **kwargs):
    """Function with all parameter types."""
    print(f"Required: {required}")
    print(f"Args: {args}")
    print(f"Default: {default}")
    print(f"Kwargs: {kwargs}")

complex_function("hello", 1, 2, 3, default="changed", extra="data")
# Required: hello
# Args: (1, 2, 3)
# Default: changed
# Kwargs: {'extra': 'data'}
```

## Function Documentation

### Docstrings
```python
def calculate_bmi(weight_kg, height_m):
    """
    Calculate Body Mass Index (BMI).

    Args:
        weight_kg (float): Weight in kilograms
        height_m (float): Height in meters

    Returns:
        float: BMI value

    Raises:
        ValueError: If weight or height are not positive numbers

    Example:
        >>> calculate_bmi(70, 1.75)
        22.857142857142858
    """
    if weight_kg <= 0 or height_m <= 0:
        raise ValueError("Weight and height must be positive numbers")

    return weight_kg / (height_m ** 2)

# Access docstring
print(calculate_bmi.__doc__)

# Use the function
bmi = calculate_bmi(70, 1.75)
print(f"BMI: {bmi:.1f}")
```

## Function Annotations (Type Hints)

### Basic Type Hints
```python
def greet_user(name: str, age: int) -> str:
    """Greet a user with type hints."""
    return f"Hello {name}, you are {age} years old!"

# Function still works normally
result = greet_user("Alice", 25)
print(result)  # "Hello Alice, you are 25 years old!"
```

### Advanced Type Hints
```python
from typing import List, Dict, Optional, Union

def process_data(data: List[Union[int, float]], config: Dict[str, any] = None) -> Optional[Dict[str, float]]:
    """
    Process a list of numbers and return statistics.

    Args:
        data: List of numbers to process
        config: Optional configuration dictionary

    Returns:
        Dictionary with statistics or None if data is empty
    """
    if not data:
        return None

    return {
        "count": len(data),
        "sum": sum(data),
        "average": sum(data) / len(data),
        "min": min(data),
        "max": max(data)
    }

# Usage
result = process_data([1, 2, 3, 4, 5])
print(result)
# {'count': 5, 'sum': 15, 'average': 3.0, 'min': 1, 'max': 5}
```

## Function Best Practices

### Single Responsibility Principle
```python
# Good - one clear purpose
def validate_email(email: str) -> bool:
    """Check if email address is valid."""
    # Email validation logic
    pass

def send_welcome_email(email: str) -> bool:
    """Send welcome email to user."""
    # Email sending logic
    pass

def register_user(email: str, password: str) -> bool:
    """Register a new user."""
    if not validate_email(email):
        return False

    # Registration logic
    # ...

    send_welcome_email(email)
    return True

# Bad - multiple responsibilities
def register_user_bad(email, password):
    """This function does too many things."""
    # Validate email
    # Hash password
    # Save to database
    # Send email
    # Log activity
    pass
```

### Meaningful Names and Parameters
```python
# Good - clear and descriptive
def calculate_monthly_payment(principal: float, annual_rate: float, years: int) -> float:
    """Calculate monthly mortgage payment."""

# Bad - unclear
def calc(x, y, z):
    """What does this calculate?"""
```

### Error Handling
```python
def safe_divide(dividend: float, divisor: float) -> Union[float, str]:
    """Safely divide two numbers."""
    try:
        if divisor == 0:
            raise ZeroDivisionError("Cannot divide by zero")
        return dividend / divisor
    except ZeroDivisionError as e:
        return f"Error: {e}"
    except TypeError:
        return "Error: Both arguments must be numbers"

print(safe_divide(10, 2))     # 5.0
print(safe_divide(10, 0))     # Error: Cannot divide by zero
print(safe_divide(10, "2"))   # Error: Both arguments must be numbers
```

## Function Testing and Debugging

### Unit Testing Functions
```python
def is_even(number: int) -> bool:
    """Check if a number is even."""
    return number % 2 == 0

def test_is_even():
    """Test the is_even function."""
    assert is_even(2) == True
    assert is_even(3) == False
    assert is_even(0) == True
    assert is_even(-2) == True
    print("All tests passed!")

test_is_even()
```

### Debugging Functions
```python
def factorial(n: int) -> int:
    """Calculate factorial with debugging."""
    print(f"Calculating factorial of {n}")

    if n < 0:
        raise ValueError("Factorial is not defined for negative numbers")

    result = 1
    for i in range(1, n + 1):
        print(f"  Multiplying by {i}: {result} * {i} = {result * i}")
        result *= i

    print(f"Final result: {result}")
    return result

# factorial(5)
```

## Function Composition

### Chaining Functions
```python
def clean_text(text: str) -> str:
    """Clean and normalize text."""
    return text.lower().strip()

def extract_words(text: str) -> List[str]:
    """Extract words from text."""
    import re
    return re.findall(r'\b\w+\b', text)

def remove_stop_words(words: List[str]) -> List[str]:
    """Remove common stop words."""
    stop_words = {"the", "a", "an", "and", "or", "but", "in", "on", "at"}
    return [word for word in words if word not in stop_words]

# Compose functions
def process_text(text: str) -> List[str]:
    """Process text through multiple transformations."""
    cleaned = clean_text(text)
    words = extract_words(cleaned)
    filtered = remove_stop_words(words)
    return filtered

text = "The quick brown fox jumps over the lazy dog"
result = process_text(text)
print(result)  # ['quick', 'brown', 'fox', 'jumps', 'lazy', 'dog']
```

## Key Takeaways

1. **Functions are reusable code blocks** that perform specific tasks
2. **Parameters allow functions to accept input** in various forms
3. **Return values provide function output** to calling code
4. **Scope controls variable accessibility** within and outside functions
5. **Documentation and type hints** improve code readability and maintainability
6. **Single responsibility principle** keeps functions focused and testable

## Further Reading
- Python function documentation
- Functional programming concepts
- Advanced parameter patterns
- Testing strategies for functions
- Performance optimization techniques