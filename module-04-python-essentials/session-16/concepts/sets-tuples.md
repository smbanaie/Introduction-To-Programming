# Sets and Tuples: Specialized Collections

## Introduction to Additional Collections

Beyond lists and dictionaries, Python provides specialized collection types for specific use cases: sets for unique elements and tuples for immutable sequences.

## Tuples: Immutable Sequences

### Creating Tuples
```python
# Empty tuple
empty_tuple = ()
empty_tuple = tuple()

# Single element tuple (note the comma!)
single = (42,)
single = 42,  # Alternative

# Multiple elements
coordinates = (10, 20)
person = ("Alice", 25, "Engineer")

# Without parentheses
colors = "red", "green", "blue"

# From iterable
numbers = tuple([1, 2, 3, 4])
letters = tuple("hello")
```

### Tuple Operations
```python
point = (3, 4, 5)

# Length
print(len(point))     # 3

# Indexing (same as lists)
print(point[0])       # 3
print(point[-1])      # 5

# Slicing
print(point[1:])      # (4, 5)
print(point[::-1])    # (5, 4, 3)

# Membership
print(4 in point)     # True
print(6 in point)     # False

# Counting
print(point.count(4)) # 1
print(point.index(4)) # 1 (first occurrence)
```

### Tuple Unpacking
```python
# Basic unpacking
x, y = (10, 20)
print(x, y)  # 10 20

# Extended unpacking
first, *middle, last = (1, 2, 3, 4, 5)
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5

# Ignore values
name, _, age = ("Alice", "female", 25)
print(name, age)  # Alice 25

# Swap values
a, b = 1, 2
a, b = b, a
print(a, b)  # 2 1
```

### Tuple Methods and Operations
```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

# Concatenation (creates new tuple)
combined = tuple1 + tuple2
print(combined)  # (1, 2, 3, 4, 5, 6)

# Repetition
repeated = tuple1 * 3
print(repeated)  # (1, 2, 3, 1, 2, 3, 1, 2, 3)

# Comparison
print((1, 2) < (1, 3))    # True (lexicographic comparison)
print((2, 1) > (1, 5))    # True

# Iteration
for item in tuple1:
    print(item, end=" ")  # 1 2 3
```

### Named Tuples
```python
from collections import namedtuple

# Define named tuple class
Point = namedtuple('Point', ['x', 'y'])
Person = namedtuple('Person', 'name age city')

# Create instances
p1 = Point(10, 20)
person1 = Person("Alice", 25, "New York")

# Access by index
print(p1[0], p1[1])        # 10 20

# Access by name
print(p1.x, p1.y)          # 10 20
print(person1.name)        # "Alice"
print(person1.age)         # 25

# Convert to dictionary
print(person1._asdict())   # {'name': 'Alice', 'age': 25, 'city': 'New York'}

# Replace values
person2 = person1._replace(age=26)
print(person2)             # Person(name='Alice', age=26, city='New York')
```

## Sets: Collections of Unique Elements

### Creating Sets
```python
# Empty set
empty_set = set()

# Set with initial values
fruits = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 4, 5}

# From iterable (removes duplicates)
duplicates = [1, 2, 2, 3, 3, 3]
unique_numbers = set(duplicates)  # {1, 2, 3}

# From string
letters = set("hello")  # {'h', 'e', 'l', 'o'}
```

### Set Operations
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Union (elements in either set)
print(set1 | set2)          # {1, 2, 3, 4, 5, 6}
print(set1.union(set2))     # Same result

# Intersection (elements in both sets)
print(set1 & set2)          # {3, 4}
print(set1.intersection(set2))  # Same result

# Difference (elements in set1 but not set2)
print(set1 - set2)          # {1, 2}
print(set1.difference(set2))  # Same result

# Symmetric difference (elements in either set but not both)
print(set1 ^ set2)          # {1, 2, 5, 6}
print(set1.symmetric_difference(set2))  # Same result
```

### Set Methods
```python
fruits = {"apple", "banana", "cherry"}

# Add elements
fruits.add("date")
print(fruits)  # {'apple', 'banana', 'cherry', 'date'}

# Add multiple elements
fruits.update(["elderberry", "fig"])
print(fruits)  # {'apple', 'banana', 'cherry', 'date', 'elderberry', 'fig'}

# Remove elements
fruits.remove("banana")     # Raises KeyError if not found
print(fruits)

fruits.discard("grape")     # No error if not found
fruits.discard("apple")     # Removes if found
print(fruits)

# Pop random element
removed = fruits.pop()
print(f"Removed: {removed}")

# Clear set
fruits.clear()
print(fruits)  # set()
```

### Set Membership and Size
```python
numbers = {1, 2, 3, 4, 5}

# Membership testing (very fast O(1))
print(3 in numbers)      # True
print(6 in numbers)      # False

# Size
print(len(numbers))      # 5

# Check if empty
print(bool(numbers))     # True
print(len(numbers) == 0) # False
```

### Set Comprehensions
```python
# Basic set comprehension
squares = {x**2 for x in range(1, 6)}
print(squares)  # {1, 4, 9, 16, 25}

# With condition
even_squares = {x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # {4, 16, 36, 64, 100}

# String processing
words = ["hello", "world", "python"]
first_letters = {word[0] for word in words}
print(first_letters)  # {'h', 'w', 'p'}
```

### Frozen Sets
```python
# Immutable set
normal_set = {1, 2, 3}
frozen_set = frozenset([1, 2, 3])

# Normal set is mutable
normal_set.add(4)
print(normal_set)  # {1, 2, 3, 4}

# Frozen set is immutable
# frozen_set.add(4)  # AttributeError

# But can be used as dictionary keys
set_dict = {frozen_set: "value"}
print(set_dict[frozen_set])  # "value"

# Can contain mutable objects
complex_frozen = frozenset([1, 2, (3, 4)])  # OK
# complex_frozen = frozenset([1, 2, [3, 4]])  # TypeError (list not hashable)
```

## Collection Comparisons

### List vs Tuple
```python
# Lists are mutable, tuples are immutable
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)

my_list[0] = 999    # OK
# my_tuple[0] = 999 # TypeError

# Tuples are slightly more memory efficient
import sys
print(sys.getsizeof(my_list))   # ~104 bytes
print(sys.getsizeof(my_tuple))  # ~72 bytes

# Tuples can be dictionary keys (if hashable)
dict_with_tuple_key = {my_tuple: "value"}
# dict_with_list_key = {my_list: "value"}  # TypeError
```

### List vs Set
```python
# Lists maintain order, allow duplicates
my_list = [1, 2, 2, 3, 1]
print(my_list)       # [1, 2, 2, 3, 1]
print(len(my_list))  # 5

# Sets are unordered, unique elements only
my_set = {1, 2, 2, 3, 1}
print(my_set)        # {1, 2, 3} (order not guaranteed)
print(len(my_set))   # 3

# Performance: sets are faster for membership testing
large_list = list(range(10000))
large_set = set(range(10000))

import time
start = time.time()
9999 in large_list  # O(n)
list_time = time.time() - start

start = time.time()
9999 in large_set   # O(1)
set_time = time.time() - start

print(f"List lookup: {list_time:.6f}s")
print(f"Set lookup: {set_time:.6f}s")
```

## Practical Applications

### Removing Duplicates
```python
# From list
original = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4]
unique = list(set(original))
print(unique)  # [1, 2, 3, 4] (order may vary)

# Preserve order
seen = set()
ordered_unique = []
for item in original:
    if item not in seen:
        seen.add(item)
        ordered_unique.append(item)

print(ordered_unique)  # [1, 2, 3, 4] (order preserved)
```

### Finding Common Elements
```python
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
list3 = [4, 5, 6, 7, 8]

# Convert to sets for set operations
set1, set2, set3 = set(list1), set(list2), set(list3)

# Common to all three
common_all = set1 & set2 & set3
print(common_all)  # {4, 5}

# Common to at least two
common_two = (set1 & set2) | (set1 & set3) | (set2 & set3)
print(common_two)  # {3, 4, 5, 6, 7}

# Unique to each
unique1 = set1 - (set2 | set3)
unique2 = set2 - (set1 | set3)
unique3 = set3 - (set1 | set2)

print(f"Unique to list1: {unique1}")  # {1, 2}
print(f"Unique to list2: {unique2}")  # {3}
print(f"Unique to list3: {unique3}")  # {8}
```

### Data Validation
```python
# Valid options
valid_colors = {"red", "green", "blue", "yellow"}
valid_sizes = {"small", "medium", "large"}

# User selections
selected_colors = ["red", "purple", "green", "blue"]
selected_sizes = ["medium", "extra-large"]

# Find invalid selections
invalid_colors = set(selected_colors) - valid_colors
invalid_sizes = set(selected_sizes) - valid_sizes

print(f"Invalid colors: {invalid_colors}")    # {'purple'}
print(f"Invalid sizes: {invalid_sizes}")      # {'extra-large'}

# Check if all selections are valid
colors_valid = set(selected_colors).issubset(valid_colors)
sizes_valid = set(selected_sizes).issubset(valid_sizes)

print(f"All colors valid: {colors_valid}")    # False
print(f"All sizes valid: {sizes_valid}")      # False
```

### Configuration Management
```python
# Immutable configuration
DATABASE_CONFIG = (
    "localhost",  # host
    5432,         # port
    "myapp",      # database name
    "user",       # username
    "password"    # password
)

# Unpack configuration
host, port, dbname, user, password = DATABASE_CONFIG

# Cannot accidentally modify
# DATABASE_CONFIG[0] = "remote"  # TypeError

# For mutable config, use dict
APP_CONFIG = {
    "debug": True,
    "max_connections": 100,
    "timeout": 30
}

# Can modify
APP_CONFIG["timeout"] = 60
```

### Mathematical Set Operations
```python
# Students in different classes
math_class = {"Alice", "Bob", "Charlie", "David"}
science_class = {"Bob", "Charlie", "Eve", "Frank"}
history_class = {"Alice", "Charlie", "Eve", "George"}

# Students taking all three classes
takes_all_three = math_class & science_class & history_class
print(takes_all_three)  # {'Charlie'}

# Students taking math or science
takes_math_or_science = math_class | science_class
print(takes_math_or_science)  # {'Alice', 'Bob', 'Charlie', 'David', 'Eve', 'Frank'}

# Students taking only math
only_math = math_class - (science_class | history_class)
print(only_math)  # {'David'}

# Students taking exactly one class
all_students = math_class | science_class | history_class
takes_multiple = (math_class & science_class) | (math_class & history_class) | (science_class & history_class)
takes_one_class = all_students - takes_multiple
print(takes_one_class)  # {'David', 'Frank', 'George'}
```

## Performance Considerations

### Choosing the Right Collection
```python
# For ordered sequences with duplicates: list
shopping_list = ["milk", "bread", "eggs", "bread"]

# For ordered sequences without duplicates: tuple (if immutable)
coordinates = (10.5, 20.3)

# For unique unordered elements: set
unique_visitors = {"alice", "bob", "charlie"}

# For key-value mapping: dict
user_info = {"name": "Alice", "age": 25}

# For immutable key-value mapping: namedtuple or frozenset of pairs
Point = namedtuple('Point', ['x', 'y'])
point = Point(10, 20)
```

### Memory Usage
```python
import sys

# Compare memory usage
my_list = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)
my_set = {1, 2, 3, 4, 5}

print(f"List: {sys.getsizeof(my_list)} bytes")
print(f"Tuple: {sys.getsizeof(my_tuple)} bytes")
print(f"Set: {sys.getsizeof(my_set)} bytes")

# Tuples are most memory efficient for small collections
# Sets have overhead for hash table
```

### Operation Time Complexity
```python
# Lists: O(1) access by index, O(n) search
# Tuples: O(1) access by index, O(n) search (same as lists)
# Sets: O(1) membership test, O(1) add/remove
# Dicts: O(1) key access, O(1) key existence

# Choose based on your access patterns
```

## Key Takeaways

1. **Tuples are immutable sequences** - use for fixed data that shouldn't change
2. **Sets contain unique elements** - perfect for membership testing and removing duplicates
3. **Named tuples** provide readable access to tuple elements
4. **Frozen sets** are immutable sets that can be used as dictionary keys
5. **Choose collections** based on mutability, ordering, and performance needs
6. **Set operations** enable mathematical operations on collections

## Further Reading
- Python collections documentation
- collections module (namedtuple, defaultdict, Counter, deque)
- Set theory and mathematical operations
- Performance characteristics of different data structures
- Memory optimization techniques