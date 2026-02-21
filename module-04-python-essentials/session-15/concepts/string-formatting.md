# String Formatting: Creating Readable Output

## Introduction to String Formatting

String formatting allows you to create well-formatted text by inserting values into string templates. Python provides multiple ways to format strings, each with different capabilities and use cases.

## F-Strings (Python 3.6+)

### Basic F-String Usage
```python
name = "Alice"
age = 25
height = 1.68

# Simple variable insertion
message = f"My name is {name} and I am {age} years old."
print(message)  # "My name is Alice and I am 25 years old."

# Multiple variables
info = f"Name: {name}, Age: {age}, Height: {height}m"
print(info)  # "Name: Alice, Age: 25, Height: 1.68m"
```

### Expressions in F-Strings
```python
# Arithmetic expressions
a, b = 10, 3
result = f"Sum: {a + b}, Difference: {a - b}, Product: {a * b}"
print(result)  # "Sum: 13, Difference: 7, Product: 30"

# Function calls
text = "hello world"
formatted = f"Upper: {text.upper()}, Length: {len(text)}"
print(formatted)  # "Upper: HELLO WORLD, Length: 11"

# Conditional expressions
score = 85
status = f"Grade: {'Pass' if score >= 60 else 'Fail'}"
print(status)  # "Grade: Pass"
```

### Formatting Numbers in F-Strings
```python
pi = 3.14159265359
large_number = 1234567.89

# Decimal precision
print(f"Pi to 2 decimal places: {pi:.2f}")      # "Pi to 2 decimal places: 3.14"
print(f"Pi to 4 decimal places: {pi:.4f}")      # "Pi to 4 decimal places: 3.1416"

# Thousands separator
print(f"Large number: {large_number:,.2f}")     # "Large number: 1,234,567.89"

# Percentage
ratio = 0.85
print(f"Success rate: {ratio:.1%}")             # "Success rate: 85.0%"

# Scientific notation
small_number = 0.00001234
print(f"Scientific: {small_number:.2e}")        # "Scientific: 1.23e-05"
```

### Formatting Different Number Systems
```python
number = 42

# Binary
print(f"Binary: {number:b}")          # "Binary: 101010"

# Octal
print(f"Octal: {number:o}")           # "Octal: 52"

# Hexadecimal (lowercase)
print(f"Hex: {number:x}")             # "Hex: 2a"

# Hexadecimal (uppercase)
print(f"Hex: {number:X}")             # "Hex: 2A"

# With prefix
print(f"Binary: {number:#b}")         # "Binary: 0b101010"
print(f"Hex: {number:#x}")            # "Hex: 0x2a"
```

### String Formatting in F-Strings
```python
text = "hello"

# Minimum width
print(f"Right aligned: {text:>10}")    # "Right aligned:      hello"
print(f"Left aligned: {text:<10}")     # "Left aligned: hello      "
print(f"Centered: {text:^10}")         # "Centered:   hello   "

# Fill character
print(f"Fill with *: {text:*^10}")     # "Fill with *: **hello***"

# Truncation
long_text = "this is a very long text"
print(f"Truncated: {long_text:.10}")   # "Truncated: this is a v"
```

### DateTime Formatting in F-Strings
```python
from datetime import datetime

now = datetime.now()

# Date and time
print(f"Current date: {now:%Y-%m-%d}")           # "Current date: 2024-01-15"
print(f"Current time: {now:%H:%M:%S}")           # "Current time: 14:30:25"

# Full format
print(f"Full datetime: {now:%A, %B %d, %Y at %I:%M %p}")
# "Full datetime: Monday, January 15, 2024 at 02:30 PM"
```

## .format() Method

### Positional Arguments
```python
# Basic positional formatting
template = "Name: {}, Age: {}, City: {}"
result = template.format("Alice", 25, "New York")
print(result)  # "Name: Alice, Age: 25, City: New York"

# Reuse positional arguments
template = "Hello {0}, welcome to {1}. {0} is a great name!"
result = template.format("Alice", "Python")
print(result)  # "Hello Alice, welcome to Python. Alice is a great name!"
```

### Named Arguments
```python
# Named placeholders
template = "Hello {name}, you are {age} years old and live in {city}."
result = template.format(name="Bob", age=30, city="London")
print(result)  # "Hello Bob, you are 30 years old and live in London."

# Mix positional and named
template = "Hello {}, you are {age} years old."
result = template.format("Charlie", age=35)
print(result)  # "Hello Charlie, you are 35 years old."
```

### Format Specifications
```python
# Number formatting
price = 49.95
quantity = 3

# Currency style
print("Price: ${:.2f}".format(price))           # "Price: $49.95"
print("Total: ${:.2f}".format(price * quantity)) # "Total: $149.85"

# Thousands separator
large_num = 1234567
print("Number: {:,}".format(large_num))         # "Number: 1,234,567"

# Percentage
rate = 0.1567
print("Rate: {:.1%}".format(rate))              # "Rate: 15.7%"
```

### Alignment and Width
```python
# Field width and alignment
names = ["Alice", "Bob", "Catherine"]

for name in names:
    print("{:<10} | Length: {}".format(name, len(name)))
# Output:
# Alice      | Length: 5
# Bob        | Length: 3
# Catherine  | Length: 9

# Center alignment
print("{:^20}".format("Centered Text"))         # "    Centered Text    "

# Fill character
print("{:*^20}".format("Filled"))               # "*******Filled*******"
```

## Old Style % Formatting

### Basic % Formatting
```python
# String substitution
name = "Alice"
print("Hello, %s!" % name)                      # "Hello, Alice!"

# Multiple values
name = "Bob"
age = 25
print("My name is %s and I am %d years old." % (name, age))
# "My name is Bob and I am 25 years old."
```

### Format Specifiers
```python
# Integer formatting
number = 42
print("Decimal: %d" % number)                   # "Decimal: 42"
print("Hex: %x" % number)                       # "Hex: 2a"
print("Octal: %o" % number)                     # "Octal: 52"

# Float formatting
pi = 3.14159
print("Pi: %.2f" % pi)                          # "Pi: 3.14"
print("Scientific: %.2e" % pi)                  # "Scientific: 3.14e+00"

# Width and alignment
print("Right: %10s" % "text")                   # "Right:       text"
print("Left: %-10s" % "text")                   # "Left: text      "
```

### Dictionary Unpacking
```python
person = {"name": "Alice", "age": 25, "city": "New York"}

print("Name: %(name)s, Age: %(age)d, City: %(city)s" % person)
# "Name: Alice, Age: 25, City: New York"
```

## Template Strings

### Basic Template Usage
```python
from string import Template

# Create template
template = Template("Hello $name, welcome to $place!")
result = template.substitute(name="Alice", place="Python")
print(result)  # "Hello Alice, welcome to Python!"

# Dictionary substitution
data = {"name": "Bob", "place": "the party"}
result = template.substitute(data)
print(result)  # "Hello Bob, welcome to the party!"
```

### Safe Substitution
```python
template = Template("Hello $name, your score is $score.")

# Normal substitution
result = template.substitute(name="Alice", score=95)
print(result)  # "Hello Alice, your score is 95."

# Safe substitution (missing keys don't cause errors)
result = template.safe_substitute(name="Bob")  # score missing
print(result)  # "Hello Bob, your score is $score."
```

## Advanced Formatting Techniques

### Custom Format Classes
```python
class Currency:
    def __init__(self, amount):
        self.amount = amount

    def __format__(self, format_spec):
        # Custom formatting for currency
        if format_spec == "usd":
            return f"${self.amount:,.2f}"
        elif format_spec == "eur":
            return f"€{self.amount:,.2f}"
        else:
            return str(self.amount)

price = Currency(1234.56)
print(f"USD: {price:usd}")    # "USD: $1,234.56"
print(f"EUR: {price:eur}")    # "EUR: €1,234.56"
```

### Nested Formatting
```python
# Complex nested structures
data = {
    "users": [
        {"name": "Alice", "age": 25, "score": 95.5},
        {"name": "Bob", "age": 30, "score": 87.2}
    ]
}

for user in data["users"]:
    print(f"Name: {user['name']:<8} | Age: {user['age']:>2} | Score: {user['score']:.1f}")
# Output:
# Name: Alice    | Age: 25 | Score: 95.5
# Name: Bob      | Age: 30 | Score: 87.2
```

### Formatting with Regular Expressions
```python
import re

def format_phone_number(phone):
    """Format phone number as (XXX) XXX-XXXX"""
    # Remove all non-digits
    digits = re.sub(r'\D', '', phone)

    # Format if 10 digits
    if len(digits) == 10:
        return f"({digits[:3]}) {digits[3:6]}-{digits[6:]}"
    else:
        return phone  # Return original if not 10 digits

print(format_phone_number("123-456-7890"))     # "(123) 456-7890"
print(format_phone_number("1234567890"))       # "(123) 456-7890"
print(format_phone_number("(123) 456-7890"))   # "(123) 456-7890"
```

## Formatting Best Practices

### Choose the Right Method
```python
# F-strings for Python 3.6+ (most readable)
name, age = "Alice", 25
message = f"Hello {name}, you are {age} years old."

# .format() for complex templates or older Python
template = "Hello {name}, you are {age} years old."
message = template.format(name="Alice", age=25)

# % formatting for simple cases or C-style code
message = "Hello %s, you are %d years old." % ("Alice", 25)
```

### Consistent Number Formatting
```python
# Define format constants
DECIMAL_PLACES = ".2f"
CURRENCY_FORMAT = ":,.2f"

prices = [29.99, 149.50, 999.99]

for price in prices:
    print(f"Price: ${price:{DECIMAL_PLACES}}")
# Output:
# Price: $29.99
# Price: $149.50
# Price: $999.99
```

### Handle Edge Cases
```python
def format_percentage(value, decimals=1):
    """Safely format percentage with bounds checking"""
    if not isinstance(value, (int, float)):
        return "N/A"

    # Clamp to valid percentage range
    value = max(0.0, min(1.0, value))

    return f"{value:.{decimals}%}"

print(format_percentage(0.856))      # "85.6%"
print(format_percentage(1.5))        # "100.0%" (clamped)
print(format_percentage("invalid"))  # "N/A"
```

## Performance Comparison

### Formatting Method Performance
```python
import time

# Test data
name, age, salary = "Alice", 25, 75000.50
iterations = 100000

# F-string performance
start = time.time()
for _ in range(iterations):
    result = f"Name: {name}, Age: {age}, Salary: ${salary:,.2f}"
fstring_time = time.time() - start

# .format() performance
start = time.time()
template = "Name: {}, Age: {}, Salary: ${:,.2f}"
for _ in range(iterations):
    result = template.format(name, age, salary)
format_time = time.time() - start

# % formatting performance
start = time.time()
template = "Name: %s, Age: %d, Salary: $%s"
for _ in range(iterations):
    result = template % (name, age, f"{salary:,.2f}")
percent_time = time.time() - start

print(f"F-string: {fstring_time:.3f}s")
print(f".format(): {format_time:.3f}s")
print(f"%: {percent_time:.3f}s")
# F-strings are typically fastest in Python 3.6+
```

## Key Takeaways

1. **F-strings are the most readable** and often fastest formatting method
2. **Use .format()** for complex templates or older Python versions
3. **Format specifications** control number display and alignment
4. **Template strings** are safest for user-provided format strings
5. **Choose formatting method** based on readability and performance needs

## Further Reading
- Python format specification mini-language
- Internationalization and locale-aware formatting
- Custom formatting classes and __format__ method
- String formatting in web templates