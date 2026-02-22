# Basic Python Syntax: Writing Your First Code

## Python Syntax Principles

Python's syntax is designed to be readable and intuitive. It uses English-like keywords and relies on indentation rather than braces or semicolons.

## Basic Program Structure

### Hello World Program
```python
# This is a comment - ignored by Python
print("Hello, World!")
```

**Output:**
```
Hello, World!
```

### Multi-line Program
```python
# Program to greet user
name = input("What's your name? ")
print("Hello, " + name + "!")
print("Welcome to Python programming!")
```

## Statements and Expressions

### Statements
Statements are complete instructions that perform actions:
```python
# Assignment statement
x = 5

# Function call statement
print("Hello")

# Control flow statement
if x > 3:
    print("Big number")
```

### Expressions
Expressions evaluate to values:
```python
# Arithmetic expression
result = 2 + 3 * 4

# Function call expression
length = len("hello")

# Comparison expression
is_large = x > 10
```

## Variables and Assignment

### Variable Names
```python
# Valid names
my_variable = 5
user_name = "Alice"
total_count = 100
is_active = True

# Invalid names (would cause errors)
# 2variable = 5      # Can't start with number
# my-variable = 10   # No hyphens
# class = "Python"   # Reserved keyword
```

### Assignment Operators
```python
# Basic assignment
x = 5

# Compound assignment
x += 3    # x = x + 3
x -= 2    # x = x - 2
x *= 4    # x = x * 4
x /= 2    # x = x / 2
x %= 3    # x = x % 3
```

## Data Types and Literals

### Numbers
```python
# Integers
age = 25
year = 2024

# Floating point
pi = 3.14159
price = 19.99

# Scientific notation
avogadro = 6.022e23
microsecond = 1e-6
```

### Strings
```python
# Single quotes
name = 'Alice'

# Double quotes
message = "Hello, World!"

# Multi-line strings
poem = """Roses are red
Violets are blue"""

# Escape sequences
path = "C:\\Users\\file.txt"
quote = "He said \"Hello\""
newline = "Line 1\nLine 2"
```

### Booleans
```python
# Boolean values
is_student = True
has_license = False

# Boolean expressions
is_adult = age >= 18
is_even = number % 2 == 0
```

## Basic Operations

### Arithmetic Operators
```python
# Addition
sum = 5 + 3  # 8

# Subtraction
diff = 10 - 4  # 6

# Multiplication
product = 6 * 7  # 42

# Division
quotient = 15 / 4  # 3.75

# Integer division
whole = 15 // 4  # 3

# Modulo (remainder)
remainder = 15 % 4  # 3

# Exponentiation
power = 2 ** 3  # 8
```

### Comparison Operators
```python
# Equal to
x == y

# Not equal to
x != y

# Greater than
x > y

# Less than
x < y

# Greater than or equal
x >= y

# Less than or equal
x <= y
```

### Logical Operators
```python
# AND - both must be true
is_adult = age >= 18 and has_id

# OR - at least one must be true
can_enter = is_member or has_ticket

# NOT - reverses truth value
is_minor = not is_adult
```

## Control Flow

### Conditional Statements
```python
# Simple if
if age >= 18:
    print("You can vote")

# If-else
if temperature > 30:
    print("It's hot!")
else:
    print("It's not too hot")

# If-elif-else
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

### Loops
```python
# While loop
count = 1
while count <= 5:
    print(count)
    count += 1

# For loop with range
for i in range(1, 6):
    print(i)

# For loop with list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

## Functions

### Defining Functions
```python
def greet_user(name):
    """This function greets a user by name."""
    message = "Hello, " + name + "!"
    return message

# Calling functions
result = greet_user("Alice")
print(result)  # "Hello, Alice!"
```

### Function with Multiple Parameters
```python
def calculate_area(length, width):
    """Calculate rectangle area."""
    area = length * width
    return area

# Call with positional arguments
result = calculate_area(5, 3)  # 15

# Call with keyword arguments
result = calculate_area(length=5, width=3)  # 15
```

## Comments and Documentation

### Single-line Comments
```python
# This is a comment
x = 5  # This assigns 5 to x
```

### Multi-line Comments
```python
"""
This is a multi-line comment
It can span several lines
Used for function documentation
"""

# Or use multiple single-line comments
# This function calculates
# the area of a rectangle
def calculate_area(length, width):
    return length * width
```

### Docstrings
```python
def calculate_average(numbers):
    """
    Calculate the arithmetic mean of a list of numbers.

    Args:
        numbers (list): A list of numeric values

    Returns:
        float: The average value

    Example:
        >>> calculate_average([1, 2, 3, 4, 5])
        3.0
    """
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)
```

## Input and Output

### Console Output
```python
# Simple print
print("Hello")

# Print multiple items
print("Name:", name, "Age:", age)

# Formatted output
print(f"My name is {name} and I'm {age} years old")
print("Value: {:.2f}".format(3.14159))
```

### Console Input
```python
# Get string input
name = input("Enter your name: ")

# Get numeric input (with conversion)
age = int(input("Enter your age: "))
height = float(input("Enter your height: "))

# Handle input errors
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("That's not a valid number!")
```

## Common Syntax Errors

### Indentation Errors
```python
# Wrong - inconsistent indentation
if x > 5:
    print("Big")
   print("This will cause IndentationError")

# Correct
if x > 5:
    print("Big")
    print("This is fine")
```

### Missing Colons
```python
# Wrong
if x > 5
    print("Big")  # SyntaxError

# Correct
if x > 5:
    print("Big")
```

### Quote Mismatches
```python
# Wrong
message = "Hello, world!  # SyntaxError

# Wrong
message = 'Hello, world!"  # SyntaxError

# Correct
message = "Hello, world!"
message = 'Hello, world!'
```

## Code Style and Best Practices

### PEP 8 Guidelines
```python
# Good variable names
user_name = "Alice"
total_count = 10
is_valid = True

# Consistent spacing
x = 1 + 2
y = x * 3

# Line length (max 79 characters)
# Break long lines
result = some_function(argument1, argument2,
                      argument3, argument4)
```

### Readability
```python
# Hard to read
x=1+2;y=x*3;z=y-1

# Easy to read
x = 1 + 2
y = x * 3
z = y - 1
```

### Meaningful Names
```python
# Avoid single letters (except in loops)
# Bad
a = calculate_average(scores)
b = find_maximum(values)

# Good
average_score = calculate_average(scores)
highest_value = find_maximum(values)
```

## Running Python Programs

### From Command Line
```bash
# Run script
python3 my_program.py

# Run with arguments
python3 script.py arg1 arg2

# Access command line arguments
import sys
print("Arguments:", sys.argv)
```

### Shebang for Unix-like Systems
```python
#!/usr/bin/env python3
# This tells the system to use Python 3

print("This script can be run directly!")
```

### Making Scripts Executable
```bash
# Add execute permission
chmod +x my_script.py

# Run directly
./my_script.py
```

## Practice Exercises

### REPL Exploration
Try these exercises in the Python REPL:

1. **Basic Operations**: Try simple math operations
   ```python
   >>> 5 + 3
   >>> 10 * 2
   >>> 15 / 3
   ```

2. **String Operations**: Experiment with text
   ```python
   >>> "Hello" + " " + "World"
   >>> "Python".upper()
   >>> len("Hello")
   ```

3. **Variables**: Create and use variables
   ```python
   >>> name = "Alice"
   >>> age = 25
   >>> print(f"My name is {name} and I am {age} years old")
   ```

### Script Creation Challenges

1. **Hello World**: Create a script that prints "Hello, World!"
2. **Personal Greeting**: Modify the script to ask for the user's name and greet them personally
3. **Simple Calculator**: Write a script that asks for two numbers and prints their sum

### Error Debugging
Identify and fix these common errors:

```python
# Fix these errors:
print("Hello)          # Missing quote
Print("Hello")         # Wrong case
print(Hello)           # Missing quotes for string
print("Hello"          # Missing closing parenthesis
```

### Exit Ticket Questions
1. How do you start Python REPL?
2. What's the difference between a script and REPL?
3. Write a Python statement to print your name

## Key Takeaways

1. **Indentation matters**: Python uses indentation to define code blocks
2. **No semicolons needed**: Statements end with newlines
3. **Dynamic typing**: Variables don't need type declarations
4. **Readable syntax**: Python emphasizes human readability
5. **Batteries included**: Rich standard library built-in

## Further Reading
- PEP 8 Style Guide (python.org/dev/peps/pep-0008/)
- Python Language Reference
- Common Python pitfalls and gotchas
- Best practices for Python development