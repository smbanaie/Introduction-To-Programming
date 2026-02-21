# Session 17: Functions

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will create reusable functions to organize and modularize code
**Materials**: Whiteboard, function flowchart examples, code organization demonstrations

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What's the difference between a list and dictionary?
- **Hook Activity**: Show repetitive code vs clean functions
- **Question**: "How can we avoid writing the same code over and over?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Define and call functions in Python
- Pass parameters and return values
- Understand scope and variable lifetime
- Create modular, reusable code

### Agenda Overview (5 minutes)
1. Function basics and syntax
2. Parameters and return values
3. Scope and variable lifetime
4. Function design principles

---

## II. Main Content (50 minutes)

### A. Function Basics (15 minutes)

#### Defining Functions
```python
# Function definition syntax
def function_name():
    # Code block
    statement1
    statement2
    return  # Optional

# Simple function example
def greet():
    print("Hello, World!")
    print("Welcome to programming!")

# Calling functions
greet()  # Execute the function
```

#### Function Naming Conventions
- **Descriptive names**: Use verbs for actions
- **snake_case**: lowercase with underscores
- **Examples**: calculate_total(), validate_email(), print_report()

#### Function Documentation
```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle

    Returns:
        float: The area of the rectangle
    """
    return length * width
```

### B. Parameters and Arguments (15 minutes)

#### Function Parameters
```python
# Function with parameters
def greet_person(name):
    print(f"Hello, {name}!")
    print("Nice to meet you!")

# Calling with arguments
greet_person("Alice")    # name = "Alice"
greet_person("Bob")      # name = "Bob"

# Multiple parameters
def add_numbers(a, b):
    result = a + b
    print(f"{a} + {b} = {result}")
    return result

sum_result = add_numbers(5, 3)  # 8
```

#### Parameter Types
```python
# Positional parameters (required)
def power(base, exponent):
    return base ** exponent

power(2, 3)  # 8

# Default parameters (optional)
def power(base, exponent=2):
    return base ** exponent

power(2, 3)  # 8
power(2)     # 4 (exponent defaults to 2)

# Keyword arguments
power(base=2, exponent=3)  # 8
power(exponent=3, base=2)  # 8 (order doesn't matter)
```

#### Return Values
```python
# Functions can return values
def get_full_name(first, last):
    return f"{first} {last}"

name = get_full_name("John", "Doe")  # "John Doe"

# Multiple return values (using tuple)
def get_user_info():
    name = "Alice"
    age = 25
    return name, age

user_name, user_age = get_user_info()  # Unpacking

# Early return
def divide(a, b):
    if b == 0:
        return "Error: Division by zero"
    return a / b
```

### C. Scope and Variable Lifetime (10 minutes)

#### Local vs Global Scope
```python
# Global variable
message = "Hello"

def greet():
    # Local variable (only exists inside function)
    local_msg = "Hi there!"
    print(message)      # Can access global
    print(local_msg)    # Can access local

def change_message():
    # This creates a local variable, doesn't change global
    message = "Goodbye"
    print(message)      # "Goodbye" (local)

greet()
change_message()
print(message)  # "Hello" (global unchanged)
```

#### Scope Rules
- **Local scope**: Variables defined inside function
- **Global scope**: Variables defined outside functions
- **LEGB Rule**: Local → Enclosing → Global → Built-in
- **Local variables**: Created when function called, destroyed when function ends

#### Modifying Global Variables
```python
counter = 0

def increment_counter():
    global counter  # Declare we're using global variable
    counter += 1

increment_counter()
print(counter)  # 1
```

### D. Function Design Principles (10 minutes)

#### Single Responsibility Principle
```python
# Good: One clear purpose
def calculate_tax(amount, rate):
    return amount * rate

def print_receipt(items, tax):
    # Print logic here
    pass

# Bad: Multiple responsibilities
def process_order(items, tax_rate):
    # Calculate tax
    tax = sum(items) * tax_rate
    # Print receipt
    print("Receipt:")
    for item in items:
        print(f"- {item}")
    # Save to database (too many responsibilities!)
    # ...
```

#### Function Length
- **Aim for 10-20 lines**: Longer functions should be broken down
- **Extract helper functions**: Complex logic into separate functions
- **Clear naming**: Function name should describe what it does

#### Error Handling in Functions
```python
def safe_divide(a, b):
    """Divide a by b safely."""
    try:
        return a / b
    except ZeroDivisionError:
        return None

def validate_age(age):
    """Check if age is valid."""
    if not isinstance(age, (int, float)):
        return False, "Age must be a number"
    if age < 0 or age > 150:
        return False, "Age must be between 0 and 150"
    return True, "Valid age"
```

---

## III. Interactive Activities (15 minutes)

### Function Creation Workshop (10 minutes)
- **Individual**: Write functions for common tasks
- **Examples**: Temperature conversion, string formatting, list operations
- **Requirements**: Include docstrings, proper parameters, return values

### Code Refactoring Challenge (5 minutes)
- **Pairs**: Take repetitive code and convert to functions
- **Before**: Lots of duplicated code
- **After**: Clean functions with calls
- **Discuss**: Benefits of the refactored version

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Functions modularize code**: Break programs into reusable pieces
2. **Parameters pass data**: Functions receive input through parameters
3. **Return values output results**: Functions can send back computed values
4. **Scope controls access**: Variables have defined lifetimes and visibility

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Write a function that adds two numbers
2. What are parameters used for?
3. What's the difference between local and global variables?

### Preview of Next Session (2 minutes)
"Next time we'll learn error handling - making programs robust and user-friendly!"

---

## Additional Resources
- **Visual Aid**: Function call flow diagram
- **Handout**: Function design checklist
- **Homework**: Create a calculator program with functions

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes