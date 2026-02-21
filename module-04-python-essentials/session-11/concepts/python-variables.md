# Python Variables: Storing and Managing Data

## What Are Variables?

Variables are named storage locations in memory that hold data values. They allow programs to store, retrieve, and manipulate information during execution.

## Variable Declaration and Assignment

### Basic Assignment
```python
# Variable assignment
age = 25
name = "Alice"
is_student = True
height = 1.75

# Multiple assignment
x, y, z = 1, 2, 3

# Same value to multiple variables
a = b = c = 0
```

### Dynamic Typing
Python variables don't need type declarations:
```python
# Variable can change type
x = 5        # integer
x = "hello"  # string
x = [1, 2, 3]  # list

# Type is determined at runtime
print(type(x))  # <class 'list'>
```

## Variable Naming Rules

### Valid Names
```python
# Good variable names
user_name = "Alice"
total_count = 10
is_valid = True
max_value = 100
user_age = 25

# Single character (for loops/counters)
for i in range(5):
    for j in range(3):
        print(f"i={i}, j={j}")
```

### Invalid Names
```python
# Cannot start with number
# 2variable = 5  # SyntaxError

# No spaces or special characters (except underscore)
# user-name = "Alice"  # SyntaxError
# user.name = "Alice"  # SyntaxError

# Cannot use Python keywords
# class = "Python"  # SyntaxError
# if = 5           # SyntaxError
```

### Naming Conventions

#### PEP 8 Standards
```python
# Variables: snake_case (lowercase with underscores)
user_name = "Alice"
total_count = 10
is_active = True

# Constants: UPPERCASE_WITH_UNDERSCORES
MAX_CONNECTIONS = 100
DEFAULT_TIMEOUT = 30
PI = 3.14159

# Classes: PascalCase
class UserAccount:
    pass

class DataProcessor:
    pass
```

#### Descriptive Names
```python
# Bad: unclear purpose
x = 25
y = "Alice"
z = True

# Good: self-documenting
student_age = 25
student_name = "Alice"
is_enrolled = True
```

## Variable Scope

### Local Variables
Variables defined inside functions:
```python
def calculate_area(length, width):
    # Local variables
    area = length * width
    return area

# area is not accessible here
# print(area)  # NameError
```

### Global Variables
Variables defined at module level:
```python
# Global variable
counter = 0

def increment_counter():
    global counter  # Declare we're using global
    counter += 1
    return counter

increment_counter()  # 1
increment_counter()  # 2
print(counter)       # 2
```

### Nonlocal Variables (Nested Functions)
```python
def outer_function():
    count = 0

    def inner_function():
        nonlocal count  # Access outer function variable
        count += 1
        return count

    return inner_function

counter = outer_function()
print(counter())  # 1
print(counter())  # 2
```

### Variable Resolution (LEGB Rule)
Python follows LEGB (Local, Enclosing, Global, Built-in) for name resolution:
```python
# Built-in: len, print, etc.
# Global: module-level variables
# Enclosing: variables in outer functions
# Local: variables in current function

len = "not the built-in"  # Shadows built-in
print(len([1, 2, 3]))     # Uses our variable, not built-in
```

## Variable Memory Management

### Reference Counting
Python tracks how many references exist to each object:
```python
x = [1, 2, 3]  # Reference count = 1
y = x          # Reference count = 2
z = x          # Reference count = 3

del y          # Reference count = 2
x = None       # Reference count = 1
# When z goes out of scope, reference count = 0, object deleted
```

### Garbage Collection
Automatic cleanup of unused objects:
```python
# Circular references handled by garbage collector
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

# Create circular reference
node1 = Node(1)
node2 = Node(2)
node1.next = node2
node2.next = node1

# Without garbage collector, this would leak memory
del node1
del node2  # Objects still reference each other
# Garbage collector will eventually clean up
```

## Variable Operations

### Copying Variables
```python
# Shallow copy (references same object)
list1 = [1, 2, 3]
list2 = list1  # Both point to same list

list1.append(4)
print(list2)  # [1, 2, 3, 4] - both changed!

# Deep copy (creates new object)
import copy
list3 = copy.deepcopy(list1)  # Creates completely separate copy
list1.append(5)
print(list3)  # [1, 2, 3, 4] - unchanged
```

### Swapping Variables
```python
# Traditional swap (needs temp variable)
a = 5
b = 10
temp = a
a = b
b = temp

# Python swap (tuple unpacking)
a = 5
b = 10
a, b = b, a  # Elegant!

# Multiple swap
x, y, z = 1, 2, 3
x, y, z = z, x, y  # Rotate values
```

## Special Variable Types

### Constants (Convention)
```python
# Constants are just variables (by convention)
PI = 3.14159
MAX_USERS = 100
DEFAULT_PORT = 8080

# Don't change constants
# PI = 3.14  # Technically allowed, but bad practice
```

### Private Variables (Convention)
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # "Private" variable

    def get_balance(self):
        return self.__balance

# Name mangling makes it harder to access
account = BankAccount(1000)
# print(account.__balance)  # AttributeError
print(account._BankAccount__balance)  # Still accessible, but discouraged
```

## Variable Inspection and Debugging

### Inspecting Variables
```python
# Check variable type
x = 42
print(type(x))  # <class 'int'>

# Check variable identity (memory address)
print(id(x))    # Unique identifier

# Check if variables reference same object
a = [1, 2, 3]
b = a
c = [1, 2, 3]
print(a is b)   # True (same object)
print(a is c)   # False (different objects, same value)
```

### Variable Scope Inspection
```python
def test_function():
    local_var = "local"
    print("Local:", local_var)

    # Access global
    global global_var
    print("Global:", global_var)

global_var = "global"
test_function()
# print(local_var)  # NameError - not accessible here
```

### Memory Usage
```python
import sys

# Check object sizes
x = 42
print(sys.getsizeof(x))  # Size in bytes

y = "hello"
print(sys.getsizeof(y))  # String size

z = [1, 2, 3, 4, 5]
print(sys.getsizeof(z))  # List size (not including elements)
```

## Variable Best Practices

### Clear Naming
```python
# Use descriptive names
def calculate_total_price(items):
    total = 0
    for item in items:
        total += item.price * item.quantity
    return total

# Avoid single letters (except obvious cases)
# Bad
def calc(t):
    s = 0
    for i in t:
        s += i.p * i.q
    return s
```

### Consistent Style
```python
# Follow PEP 8
user_name = "Alice"     # snake_case for variables
UserAccount = "class"   # PascalCase for classes
MAX_CONNECTIONS = 100   # UPPERCASE for constants
```

### Minimize Global Variables
```python
# Bad - global state
total_sales = 0

def add_sale(amount):
    global total_sales
    total_sales += amount

# Better - encapsulate state
class SalesTracker:
    def __init__(self):
        self.total_sales = 0

    def add_sale(self, amount):
        self.total_sales += amount

    def get_total(self):
        return self.total_sales
```

### Use Meaningful Defaults
```python
# Good defaults
def connect_database(host="localhost", port=5432, timeout=30):
    # Implementation
    pass

# Bad defaults
def process_data(data=None, flag=True, count=-1):
    # -1 might be confused with valid count
    pass
```

## Common Variable Mistakes

### Uninitialized Variables
```python
# Error
print(unknown_variable)  # NameError

# Fix
unknown_variable = "now defined"
print(unknown_variable)
```

### Variable Shadowing
```python
total = 100

def calculate_total(items):
    total = 0  # Shadows global variable
    for item in items:
        total += item.price
    return total

print(total)  # Still 100 (global unchanged)
```

### Mutable Default Arguments
```python
# Problematic
def add_item(item, shopping_list=[]):
    shopping_list.append(item)
    return shopping_list

# Unexpected behavior
list1 = add_item("apple")
list2 = add_item("banana")
print(list1)  # ['apple', 'banana'] - both lists affected!

# Fix
def add_item(item, shopping_list=None):
    if shopping_list is None:
        shopping_list = []
    shopping_list.append(item)
    return shopping_list
```

## Key Takeaways

1. **Variables are named storage** for data values in memory
2. **Dynamic typing** allows variables to change types
3. **Scope controls accessibility** of variables
4. **Naming conventions** improve code readability
5. **Memory management** is automatic in Python
6. **Best practices** prevent common mistakes

## Further Reading
- Python data model and object system
- Variable scoping in different languages
- Memory management techniques
- Best practices for variable naming and organization