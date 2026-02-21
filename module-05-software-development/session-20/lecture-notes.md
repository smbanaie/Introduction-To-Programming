# Session 20: Modules & Multi-file Programs

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will organize code into modules and create multi-file programs
**Materials**: Whiteboard, module structure examples, import demonstrations

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you safely read from a file?
- **Hook Activity**: Show single massive file vs organized modules
- **Question**: "How can we organize large programs into manageable pieces?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Create and import custom modules
- Organize code into logical components
- Use Python's standard library modules
- Build multi-file applications

### Agenda Overview (5 minutes)
1. Understanding modules and imports
2. Creating custom modules
3. Python standard library
4. Multi-file program organization

---

## II. Main Content (50 minutes)

### A. Modules and Imports (15 minutes)

#### What are Modules?
- **Modules**: Python files containing code (functions, classes, variables)
- **Packages**: Directories containing multiple modules
- **Benefits**: Code organization, reusability, maintainability

#### Import Methods
```python
# Method 1: Import entire module
import math
result = math.sqrt(16)  # Use module.function

# Method 2: Import specific items
from math import sqrt, pi
result = sqrt(16)  # Use function directly

# Method 3: Import with alias
import math as m
result = m.sqrt(16)  # Shorter name

# Method 4: Import all (generally avoid)
from math import *
result = sqrt(16)  # Everything available
```

#### Import Best Practices
- **Import at top**: All imports at file beginning
- **Standard library first**: Built-in modules before custom
- **Group imports**: Related imports together
- **Use descriptive aliases**: import pandas as pd

### B. Creating Custom Modules (15 minutes)

#### Basic Module Structure
```python
# calculator.py - A simple calculator module

def add(a, b):
    """Add two numbers."""
    return a + b

def subtract(a, b):
    """Subtract b from a."""
    return a - b

def multiply(a, b):
    """Multiply two numbers."""
    return a * b

def divide(a, b):
    """Divide a by b."""
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

# Module-level variables
PI = 3.14159
AUTHOR = "Student Programmer"
```

#### Using Custom Modules
```python
# main.py - Main program using calculator module

import calculator

# Use functions from module
result1 = calculator.add(5, 3)
result2 = calculator.multiply(4, 7)

print(f"5 + 3 = {result1}")
print(f"4 × 7 = {result2}")

# Use module constants
print(f"PI is approximately {calculator.PI}")
print(f"Module by {calculator.AUTHOR}")
```

#### Module Execution Context
```python
# test_module.py

print("This always prints when module is imported")

if __name__ == "__main__":
    print("This only prints when module is run directly")
    # Test code here
else:
    print("This prints when module is imported")

# When run with: python test_module.py
# Output: "This always prints when module is imported"
#         "This only prints when module is run directly"

# When imported: import test_module
# Output: "This always prints when module is imported"
#         "This prints when module is imported"
```

### C. Python Standard Library (10 minutes)

#### Essential Standard Modules
```python
# Math operations
import math
print(math.sqrt(25))    # 5.0
print(math.pi)          # 3.141592653589793

# Random numbers
import random
print(random.randint(1, 10))    # Random integer 1-10
print(random.choice(['a', 'b', 'c']))  # Random choice

# Date and time
import datetime
now = datetime.datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # Formatted time

# Operating system interface
import os
print(os.getcwd())      # Current working directory
print(os.listdir('.'))  # List files in current directory

# JSON data handling
import json
data = {"name": "Alice", "age": 25}
json_str = json.dumps(data)  # Convert to JSON string
parsed = json.loads(json_str)  # Parse JSON string
```

#### Commonly Used Modules
- **sys**: System-specific parameters and functions
- **os**: Operating system interface
- **re**: Regular expressions
- **collections**: Specialized container datatypes
- **itertools**: Functions creating iterators
- **functools**: Higher-order functions

### D. Multi-file Program Organization (10 minutes)

#### Project Structure
```
my_program/
├── main.py              # Entry point
├── utils.py             # Utility functions
├── data_handler.py      # Data processing
├── ui.py               # User interface
├── config.py           # Configuration settings
└── tests/
    ├── test_utils.py
    └── test_data.py
```

#### Example Multi-file Program
```python
# config.py - Configuration settings
APP_NAME = "Student Manager"
VERSION = "1.0.0"
DEFAULT_FILE = "students.json"

# utils.py - Utility functions
def validate_email(email):
    """Check if email is valid."""
    return "@" in email and "." in email

def calculate_average(grades):
    """Calculate average of grades."""
    if not grades:
        return 0
    return sum(grades) / len(grades)

# data_handler.py - Data management
import json
import config

def load_students():
    """Load students from file."""
    try:
        with open(config.DEFAULT_FILE, 'r') as f:
            return json.load(f)
    except FileNotFoundError:
        return []

def save_students(students):
    """Save students to file."""
    with open(config.DEFAULT_FILE, 'w') as f:
        json.dump(students, f, indent=2)

# main.py - Main program
import data_handler
import utils

def main():
    print(f"Welcome to {data_handler.config.APP_NAME}")

    students = data_handler.load_students()

    # Program logic here
    while True:
        print("\n1. Add student")
        print("2. List students")
        print("3. Exit")

        choice = input("Choose option: ")

        if choice == "1":
            # Add student logic
            pass
        elif choice == "2":
            # List students logic
            pass
        elif choice == "3":
            break

if __name__ == "__main__":
    main()
```

---

## III. Interactive Activities (15 minutes)

### Module Creation Workshop (10 minutes)
- **Individual**: Create a custom module with related functions
- **Examples**: Math utilities, string helpers, data validators
- **Test**: Import and use the module in another file

### Program Refactoring Challenge (5 minutes)
- **Pairs**: Take single-file program and split into modules
- **Goal**: Logical separation of concerns
- **Result**: Clean, organized multi-file structure

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Modules organize code**: Break large programs into manageable pieces
2. **Imports bring functionality**: Access code from other files
3. **Standard library provides tools**: Built-in modules for common tasks
4. **Structure matters**: Good organization improves maintainability

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. How do you import a custom module?
2. What's the difference between import math and from math import sqrt?
3. Why should you organize code into modules?

### Preview of Next Session (2 minutes)
"Next time we'll build a mini-project - putting everything together!"

---

## Additional Resources
- **Visual Aid**: Module import flow diagram
- **Handout**: Standard library module reference
- **Homework**: Create a multi-file calculator program

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes