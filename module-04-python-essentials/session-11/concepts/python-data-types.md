# Python Data Types: Organizing Information

## What Are Data Types?

Data types define the kind of values a variable can hold and the operations that can be performed on those values. Python has several built-in data types, each suited for different kinds of data.

## Numeric Types

### Integers (int)
Whole numbers, positive or negative:
```python
# Basic integers
age = 25
temperature = -5
year = 2024

# Large integers (no size limit in Python 3)
very_large = 123456789012345678901234567890
print(type(very_large))  # <class 'int'>

# Different bases
decimal = 42        # Decimal (base 10)
binary = 0b101010   # Binary (base 2)
octal = 0o52        # Octal (base 8)
hexadecimal = 0x2A  # Hexadecimal (base 16)
```

### Floating-Point Numbers (float)
Numbers with decimal points:
```python
# Basic floats
pi = 3.14159
price = 19.99
weight = 65.5

# Scientific notation
avogadro = 6.022e23  # 6.022 × 10²³
microsecond = 1e-6   # 1 × 10⁻⁶

# Special float values
positive_infinity = float('inf')
negative_infinity = float('-inf')
not_a_number = float('nan')

# Precision limitations
print(0.1 + 0.2)  # 0.30000000000000004 (not exactly 0.3!)
```

### Complex Numbers (complex)
Numbers with real and imaginary parts:
```python
# Complex number creation
z1 = 3 + 4j      # Real: 3, Imaginary: 4
z2 = complex(2, 5)  # Using complex() function

# Complex operations
print(z1 + z2)   # (5+9j)
print(z1 * z2)   # (-14+23j)
print(z1.real)   # 3.0
print(z1.imag)   # 4.0
print(abs(z1))   # 5.0 (magnitude)
```

## Text Type

### Strings (str)
Sequences of characters:
```python
# String creation
name = "Alice"
message = 'Hello, World!'
multiline = """This is a
multiline string"""

# String properties
text = "Python"
print(len(text))      # 6 (length)
print(text[0])        # 'P' (first character)
print(text[-1])       # 'n' (last character)

# Strings are immutable
# text[0] = 'J'  # TypeError!
```

### String Operations
```python
text = "Hello, World!"

# Concatenation
greeting = "Hello" + " " + "Alice"  # "Hello Alice"

# Repetition
divider = "=" * 50  # "=================================================="

# Membership
print("Hello" in text)   # True
print("Python" in text)  # False

# Slicing
print(text[0:5])    # "Hello"
print(text[7:])     # "World!"
print(text[::-1])   # "!dlroW ,olleH" (reversed)
```

### String Methods
```python
text = "hello world"

# Case conversion
print(text.upper())       # "HELLO WORLD"
print(text.lower())       # "hello world"
print(text.capitalize())  # "Hello world"
print(text.title())       # "Hello World"

# Searching
print(text.find("world"))    # 6
print(text.count("l"))       # 3
print(text.startswith("hello"))  # True

# Modification
print(text.replace("world", "Python"))  # "hello Python"
words = text.split()        # ["hello", "world"]
joined = " ".join(words)    # "hello world"

# Testing
print(text.isalpha())   # False (contains space)
print(text.islower())   # True
print(text.isdigit())   # False
```

## Boolean Type

### Booleans (bool)
Truth values:
```python
# Boolean literals
is_active = True
is_deleted = False

# Boolean from comparisons
age = 25
is_adult = age >= 18      # True
is_senior = age >= 65     # False

# Boolean from other types
print(bool(0))        # False
print(bool(1))        # True
print(bool(""))       # False (empty string)
print(bool("hello"))  # True
print(bool([]))       # False (empty list)
print(bool([1, 2]))   # True
```

### Boolean Operations
```python
# Logical AND
result = True and False  # False
result = True and True   # True

# Logical OR
result = True or False   # True
result = False or False  # False

# Logical NOT
result = not True        # False
result = not False       # True

# Short-circuit evaluation
def expensive_operation():
    print("This is expensive!")
    return True

# AND stops at first False
result = False and expensive_operation()  # Doesn't call expensive_operation()

# OR stops at first True
result = True or expensive_operation()    # Doesn't call expensive_operation()
```

## Sequence Types

### Lists (list)
Ordered, mutable sequences:
```python
# List creation
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "hello", True, 3.14]

# Empty list
empty = []
empty = list()

# List operations
numbers.append(6)        # [1, 2, 3, 4, 5, 6]
numbers.insert(0, 0)     # [0, 1, 2, 3, 4, 5, 6]
numbers.remove(3)        # [0, 1, 2, 4, 5, 6]
last = numbers.pop()     # 6, list becomes [0, 1, 2, 4, 5]

# Indexing and slicing
print(numbers[0])        # 0
print(numbers[-1])       # 5
print(numbers[1:4])      # [1, 2, 4]

# List methods
numbers.sort()           # [0, 1, 2, 4, 5]
numbers.reverse()        # [5, 4, 2, 1, 0]
length = len(numbers)    # 5
```

### Tuples (tuple)
Ordered, immutable sequences:
```python
# Tuple creation
coordinates = (10, 20)
person = ("Alice", 25, "Engineer")

# Single element tuple
single = (42,)  # Note the comma!

# Empty tuple
empty = ()
empty = tuple()

# Tuple operations (similar to lists)
print(coordinates[0])    # 10
print(len(coordinates))  # 2

# Tuples are immutable
# coordinates[0] = 15  # TypeError!

# Unpacking
x, y = coordinates
name, age, job = person
```

### Ranges (range)
Immutable sequences of numbers:
```python
# Range creation
numbers = range(5)          # 0, 1, 2, 3, 4
even_numbers = range(0, 10, 2)  # 0, 2, 4, 6, 8

# Range to list
list(range(5))              # [0, 1, 2, 3, 4]
list(range(2, 8))           # [2, 3, 4, 5, 6, 7]
list(range(10, 0, -1))      # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

# Range properties
r = range(0, 100, 5)
print(r.start)     # 0
print(r.stop)      # 100
print(r.step)      # 5
print(len(r))      # 20
print(25 in r)     # True
```

## Mapping Type

### Dictionaries (dict)
Key-value pairs:
```python
# Dictionary creation
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Empty dictionary
empty = {}
empty = dict()

# Alternative creation
person2 = dict(name="Bob", age=30, city="London")

# Accessing values
print(person["name"])       # "Alice"
print(person.get("age"))    # 25
print(person.get("salary", "Not specified"))  # "Not specified"

# Modifying dictionaries
person["age"] = 26          # Update existing
person["job"] = "Engineer"  # Add new
del person["city"]          # Remove

# Dictionary methods
print(person.keys())        # dict_keys(['name', 'age', 'job'])
print(person.values())      # dict_values(['Alice', 26, 'Engineer'])
print(person.items())       # dict_items([('name', 'Alice'), ('age', 26), ('job', 'Engineer')])

# Membership testing
print("name" in person)     # True (key exists)
print("Alice" in person)    # False (value exists, but we check keys)
```

## Set Types

### Sets (set)
Unordered collections of unique elements:
```python
# Set creation
fruits = {"apple", "banana", "cherry"}
numbers = set([1, 2, 3, 3, 4])  # {1, 2, 3, 4} (duplicates removed)

# Empty set
empty = set()  # Not {} which creates dict!

# Set operations
fruits.add("date")          # {"apple", "banana", "cherry", "date"}
fruits.remove("banana")     # {"apple", "cherry", "date"}
fruits.discard("grape")     # No error if element doesn't exist

# Mathematical set operations
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

print(set1 | set2)  # Union: {1, 2, 3, 4, 5, 6}
print(set1 & set2)  # Intersection: {3, 4}
print(set1 - set2)  # Difference: {1, 2}
print(set1 ^ set2)  # Symmetric difference: {1, 2, 5, 6}
```

### Frozen Sets (frozenset)
Immutable sets:
```python
# Frozen set creation
immutable_set = frozenset([1, 2, 3, 4])

# Can be used as dictionary keys
coordinates = {(1, 2): "point A", (3, 4): "point B"}
# Lists can't be keys, but frozensets can
```

## None Type

### NoneType
Represents absence of value:
```python
# None literal
result = None

# Functions that don't return values
def print_message(message):
    print(message)
    # No return statement = returns None

result = print_message("Hello")
print(result)  # None

# Checking for None
if result is None:
    print("No value returned")

# None vs False vs 0 vs empty string
print(None == False)    # False
print(None == 0)        # False
print(None == "")       # False
print(None is None)     # True (use 'is' for None)
```

## Type Conversion

### Implicit Conversion (Coercion)
Python automatically converts types in some cases:
```python
# Numeric coercion
result = 5 + 3.2  # 8.2 (int + float = float)

# String concatenation
message = "Count: " + str(5)  # Must convert int to string
```

### Explicit Conversion (Casting)
Manually convert between types:
```python
# To string
str(42)        # "42"
str(3.14)      # "3.14"
str(True)      # "True"

# To integer
int("42")      # 42
int(3.14)      # 3 (truncates)
int(True)      # 1

# To float
float("3.14")  # 3.14
float(42)      # 42.0
float(True)    # 1.0

# To boolean
bool(0)        # False
bool(1)        # True
bool("")       # False
bool("hello")  # True
bool([])       # False
bool([1, 2])   # True

# To list/tuple
list("hello")  # ['h', 'e', 'l', 'l', 'o']
tuple([1, 2, 3])  # (1, 2, 3)

# To set
set([1, 2, 2, 3])  # {1, 2, 3}
```

### Safe Conversion
```python
# Handle conversion errors
def safe_int_conversion(value):
    try:
        return int(value)
    except ValueError:
        return None

print(safe_int_conversion("42"))    # 42
print(safe_int_conversion("hello")) # None
```

## Type Checking

### Runtime Type Checking
```python
# Check variable type
x = 42
print(type(x))        # <class 'int'>
print(isinstance(x, int))   # True
print(isinstance(x, str))   # False

# Check multiple types
def is_numeric(value):
    return isinstance(value, (int, float, complex))

print(is_numeric(42))      # True
print(is_numeric("42"))    # False
print(is_numeric(3.14))    # True
```

## Key Takeaways

1. **Python has built-in data types** for different kinds of information
2. **Data types determine** what operations are available
3. **Type conversion** allows working with different types
4. **Collections** (lists, tuples, dicts, sets) organize multiple values
5. **None represents** absence of value
6. **Type checking** ensures correct usage

## Further Reading
- Python data model documentation
- Object-oriented programming concepts
- Type hints and annotations (Python 3.5+)
- Advanced data structures (collections module)