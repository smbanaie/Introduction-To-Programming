# Python Dictionaries: Key-Value Data Structures

## Introduction to Dictionaries

Dictionaries are mutable, unordered collections of key-value pairs. They provide fast lookups and are one of Python's most powerful data structures for organizing and accessing data.

## Creating Dictionaries

### Basic Dictionary Creation
```python
# Empty dictionary
empty_dict = {}
empty_dict = dict()

# Dictionary with initial values
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Using dict() constructor
person = dict(name="Alice", age=25, city="New York")

# From list of pairs
pairs = [("name", "Alice"), ("age", 25), ("city", "New York")]
person = dict(pairs)

# From keyword arguments
person = dict(name="Alice", age=25, city="New York")
```

### Dictionary Comprehensions
```python
# Basic comprehension
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With condition
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# Transform existing dictionary
original = {"a": 1, "b": 2, "c": 3}
doubled = {key: value * 2 for key, value in original.items()}
print(doubled)  # {'a': 2, 'b': 4, 'c': 6}

# Swap keys and values
swapped = {value: key for key, value in original.items()}
print(swapped)  # {1: 'a', 2: 'b', 3: 'c'}
```

## Accessing Dictionary Elements

### Key Access
```python
person = {"name": "Alice", "age": 25, "city": "New York"}

# Direct access
print(person["name"])   # "Alice"
print(person["age"])    # 25

# Using get() method (safer)
print(person.get("name"))        # "Alice"
print(person.get("salary"))      # None (key doesn't exist)
print(person.get("salary", 0))   # 0 (default value)
```

### Checking Keys
```python
person = {"name": "Alice", "age": 25}

# Check if key exists
print("name" in person)     # True
print("salary" in person)   # False

# Check if key doesn't exist
print("salary" not in person)  # True

# Safe access pattern
if "age" in person:
    age = person["age"]
    print(f"Age: {age}")
else:
    print("Age not specified")
```

### Handling Missing Keys
```python
person = {"name": "Alice"}

# Method 1: Check then access
if "age" in person:
    age = person["age"]
else:
    age = 18  # default

# Method 2: Use get()
age = person.get("age", 18)

# Method 3: setdefault() - get and set default
age = person.setdefault("age", 18)
print(person)  # {"name": "Alice", "age": 18}
```

## Modifying Dictionaries

### Adding and Updating
```python
person = {"name": "Alice", "age": 25}

# Add new key-value pair
person["city"] = "New York"
print(person)  # {'name': 'Alice', 'age': 25, 'city': 'New York'}

# Update existing value
person["age"] = 26
print(person)  # {'name': 'Alice', 'age': 26, 'city': 'New York'}

# Update multiple values
person.update({"age": 27, "job": "Engineer"})
print(person)  # {'name': 'Alice', 'age': 27, 'city': 'New York', 'job': 'Engineer'}

# Merge dictionaries
additional_info = {"hobby": "reading", "city": "Boston"}  # Overwrites city
person.update(additional_info)
print(person)  # {'name': 'Alice', 'age': 27, 'city': 'Boston', 'job': 'Engineer', 'hobby': 'reading'}
```

### Removing Elements
```python
person = {"name": "Alice", "age": 27, "city": "Boston", "job": "Engineer"}

# Remove by key (returns value)
removed_city = person.pop("city")
print(removed_city)  # "Boston"
print(person)        # {'name': 'Alice', 'age': 27, 'job': 'Engineer'}

# Remove with default (if key doesn't exist)
removed_hobby = person.pop("hobby", "Not specified")
print(removed_hobby)  # "Not specified"

# Remove last item (arbitrary in Python 3.7+)
last_item = person.popitem()
print(last_item)     # ('job', 'Engineer')
print(person)        # {'name': 'Alice', 'age': 27}

# Clear all items
person.clear()
print(person)        # {}
```

## Dictionary Views and Iteration

### Keys, Values, and Items
```python
person = {"name": "Alice", "age": 27, "city": "Boston"}

# Get all keys
keys = person.keys()
print(keys)          # dict_keys(['name', 'age', 'city'])
print(list(keys))    # ['name', 'age', 'city']

# Get all values
values = person.values()
print(values)        # dict_values(['Alice', 27, 'Boston'])

# Get all key-value pairs
items = person.items()
print(items)         # dict_items([('name', 'Alice'), ('age', 27), ('city', 'Boston')])

# Convert to lists
key_list = list(person.keys())
value_list = list(person.values())
item_list = list(person.items())
```

### Iterating Over Dictionaries
```python
person = {"name": "Alice", "age": 27, "city": "Boston"}

# Iterate over keys (default)
for key in person:
    print(f"{key}: {person[key]}")

# Iterate over keys explicitly
for key in person.keys():
    print(f"{key}: {person[key]}")

# Iterate over values
for value in person.values():
    print(f"Value: {value}")

# Iterate over key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")

# Unpacking in loop
for key, value in person.items():
    print(f"Key: {key}, Value: {value}")
```

## Dictionary Methods and Operations

### Copying Dictionaries
```python
original = {"a": 1, "b": [2, 3]}

# Shallow copy
shallow = original.copy()
shallow = dict(original)  # Alternative

# Modify shallow copy
shallow["c"] = 4
print(original)  # {'a': 1, 'b': [2, 3]} (unchanged)
print(shallow)   # {'a': 1, 'b': [2, 3], 'c': 4}

# But nested objects are shared!
shallow["b"].append(4)
print(original)  # {'a': 1, 'b': [2, 3, 4]} (nested list changed!)
print(shallow)   # {'a': 1, 'b': [2, 3, 4], 'c': 4}

# Deep copy for nested structures
import copy
deep = copy.deepcopy(original)
deep["b"].append(5)
print(original)  # {'a': 1, 'b': [2, 3, 4]} (unchanged)
print(deep)      # {'a': 1, 'b': [2, 3, 4, 5]}
```

### Dictionary Size and Information
```python
person = {"name": "Alice", "age": 27, "city": "Boston"}

# Get number of items
print(len(person))  # 3

# Check if empty
print(bool(person))     # True
print(len(person) == 0) # False

# Get value or set default
age = person.setdefault("age", 18)  # Returns existing value
print(age)  # 27

hobby = person.setdefault("hobby", "reading")  # Sets and returns default
print(hobby)  # "reading"
print(person)  # {'name': 'Alice', 'age': 27, 'city': 'Boston', 'hobby': 'reading'}
```

## Advanced Dictionary Techniques

### Dictionary Merging (Python 3.9+)
```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

# Merge with | operator
merged = dict1 | dict2
print(merged)  # {'a': 1, 'b': 3, 'c': 4}

# Update in place with |=
dict1 |= dict2
print(dict1)   # {'a': 1, 'b': 3, 'c': 4}
```

### Default Dictionaries
```python
from collections import defaultdict

# Regular dictionary
word_counts = {}
words = ["apple", "banana", "apple", "cherry", "banana"]

for word in words:
    if word in word_counts:
        word_counts[word] += 1
    else:
        word_counts[word] = 1

print(word_counts)  # {'apple': 2, 'banana': 2, 'cherry': 1}

# Default dictionary
word_counts = defaultdict(int)  # Default value is 0
for word in words:
    word_counts[word] += 1  # No need to check if key exists

print(dict(word_counts))  # {'apple': 2, 'banana': 2, 'cherry': 1}

# Other default types
list_dict = defaultdict(list)
list_dict["fruits"].append("apple")
list_dict["fruits"].append("banana")
print(dict(list_dict))  # {'fruits': ['apple', 'banana']}
```

### Ordered Dictionaries
```python
from collections import OrderedDict

# Regular dict maintains insertion order in Python 3.7+
regular = {"c": 3, "a": 1, "b": 2}
print(list(regular.keys()))  # ['c', 'a', 'b'] (insertion order)

# OrderedDict (for older Python versions or explicit ordering)
ordered = OrderedDict([("c", 3), ("a", 1), ("b", 2)])
print(list(ordered.keys()))  # ['c', 'a', 'b']

# Move item to end
ordered.move_to_end("a")
print(list(ordered.keys()))  # ['c', 'b', 'a']
```

## Dictionary Use Cases and Patterns

### Grouping Data
```python
# Group by category
data = [
    {"name": "Alice", "department": "Engineering"},
    {"name": "Bob", "department": "Sales"},
    {"name": "Charlie", "department": "Engineering"},
    {"name": "David", "department": "Sales"}
]

# Manual grouping
groups = {}
for item in data:
    dept = item["department"]
    if dept not in groups:
        groups[dept] = []
    groups[dept].append(item["name"])

print(groups)
# {'Engineering': ['Alice', 'Charlie'], 'Sales': ['Bob', 'David']}

# Using defaultdict
from collections import defaultdict
groups = defaultdict(list)
for item in data:
    groups[item["department"]].append(item["name"])

print(dict(groups))  # Same result
```

### Counting Frequencies
```python
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]

# Count manually
counts = {}
for word in words:
    counts[word] = counts.get(word, 0) + 1

# Using Counter (better)
from collections import Counter
counts = Counter(words)

print(counts)           # Counter({'apple': 3, 'banana': 2, 'cherry': 1})
print(counts.most_common(2))  # [('apple', 3), ('banana', 2)]
```

### Caching/Memoization
```python
# Simple cache
cache = {}

def fibonacci(n):
    if n in cache:
        return cache[n]

    if n <= 1:
        result = n
    else:
        result = fibonacci(n-1) + fibonacci(n-2)

    cache[n] = result
    return result

print(fibonacci(10))  # 55
print(cache)          # {0: 0, 1: 1, 2: 1, 3: 2, 4: 3, 5: 5, 6: 8, 7: 13, 8: 21, 9: 34, 10: 55}
```

### Configuration Management
```python
# Application configuration
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp"
    },
    "api": {
        "base_url": "https://api.example.com",
        "timeout": 30,
        "retries": 3
    },
    "logging": {
        "level": "INFO",
        "file": "app.log"
    }
}

# Access nested configuration
db_host = config["database"]["host"]
api_timeout = config["api"]["timeout"]

# Update configuration
config["api"]["timeout"] = 60
```

## Dictionary Performance

### Time Complexity
```python
# O(1) operations - average case
person = {"name": "Alice", "age": 25}
person["city"] = "New York"  # Add/update
value = person["name"]       # Access
"name" in person             # Membership test
del person["age"]            # Delete

# O(n) operations
len(person)                   # Size
list(person.keys())          # Convert to list
person.items()               # Get items view
```

### Hashable Keys
```python
# Valid keys (immutable/hashable)
valid_dict = {
    "string": "value",
    42: "number",
    (1, 2): "tuple",
    frozenset([1, 2]): "frozenset",
    True: "boolean"
}

# Invalid keys (mutable/unhashable)
# invalid_dict = {
#     [1, 2]: "list",        # TypeError: unhashable type: 'list'
#     {"a": 1}: "dict",      # TypeError: unhashable type: 'dict'
# }
```

### Memory Considerations
```python
# Dictionaries have memory overhead
# Empty dict: ~240 bytes
# Dict with 1 item: ~360 bytes
# Dict with 10 items: ~1,200 bytes

# Use appropriate data structures
# Dict for key lookups: O(1)
# List for ordered access: O(n) lookup
# Set for membership testing: O(1)
```

## Key Takeaways

1. **Dictionaries store key-value pairs** with fast O(1) lookups
2. **Keys must be immutable/hashable** (strings, numbers, tuples)
3. **Use get() and setdefault()** for safe key access
4. **Dictionary comprehensions** create dicts concisely
5. **Views (keys, values, items)** provide dynamic access to contents
6. **Choose dictionaries** when you need fast key-based access

## Further Reading
- Python dict documentation
- Hash table implementation details
- collections module (OrderedDict, defaultdict, Counter)
- Dictionary vs other data structures
- Memory optimization techniques