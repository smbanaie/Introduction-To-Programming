# Python Lists: Ordered, Mutable Collections

## Introduction to Lists

Lists are ordered, mutable sequences that can store heterogeneous data types. They are one of Python's most versatile and commonly used data structures.

## Creating Lists

### Basic List Creation
```python
# Empty list
empty_list = []
empty_list = list()

# List with initial values
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "hello", 3.14, True, [1, 2, 3]]

# List from range
even_numbers = list(range(0, 10, 2))  # [0, 2, 4, 6, 8]

# List from string
chars = list("hello")  # ['h', 'e', 'l', 'l', 'o']
```

### List Comprehensions
```python
# Basic comprehension
squares = [x**2 for x in range(1, 6)]  # [1, 4, 9, 16, 25]

# With condition
even_squares = [x**2 for x in range(1, 11) if x % 2 == 0]  # [4, 16, 36, 64, 100]

# Nested comprehensions
matrix = [[i*j for j in range(1, 4)] for i in range(1, 4)]
# [[1, 2, 3], [2, 4, 6], [3, 6, 9]]

# Conditional expressions
results = ["even" if x % 2 == 0 else "odd" for x in range(1, 6)]
# ['odd', 'even', 'odd', 'even', 'odd']
```

## Accessing List Elements

### Indexing
```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

# Positive indexing
print(fruits[0])   # 'apple'
print(fruits[2])   # 'cherry'

# Negative indexing
print(fruits[-1])  # 'elderberry'
print(fruits[-2])  # 'date'

# Out of bounds (causes IndexError)
# print(fruits[10])  # IndexError
```

### Slicing
```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Basic slicing
print(numbers[2:7])   # [2, 3, 4, 5, 6]
print(numbers[:5])    # [0, 1, 2, 3, 4]
print(numbers[5:])    # [5, 6, 7, 8, 9]

# With step
print(numbers[::2])   # [0, 2, 4, 6, 8] (every other)
print(numbers[1::2])  # [1, 3, 5, 7, 9] (every other, starting from index 1)

# Reverse
print(numbers[::-1])  # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

# Advanced slicing
print(numbers[1:8:2]) # [1, 3, 5, 7] (start:end:step)
```

## Modifying Lists

### Adding Elements
```python
fruits = ["apple", "banana"]

# Append (add to end)
fruits.append("cherry")
print(fruits)  # ['apple', 'banana', 'cherry']

# Insert at specific position
fruits.insert(1, "avocado")
print(fruits)  # ['apple', 'avocado', 'banana', 'cherry']

# Extend with another list
fruits.extend(["date", "elderberry"])
print(fruits)  # ['apple', 'avocado', 'banana', 'cherry', 'date', 'elderberry']

# Concatenation (creates new list)
more_fruits = fruits + ["fig", "grape"]
print(more_fruits)  # ['apple', 'avocado', 'banana', 'cherry', 'date', 'elderberry', 'fig', 'grape']
```

### Removing Elements
```python
numbers = [1, 2, 3, 4, 5, 2, 3]

# Remove by value (first occurrence)
numbers.remove(2)
print(numbers)  # [1, 3, 4, 5, 2, 3]

# Remove by index
del numbers[0]  # Remove first element
print(numbers)  # [3, 4, 5, 2, 3]

# Pop (remove and return)
last = numbers.pop()  # Remove last element
print(last)     # 3
print(numbers)  # [3, 4, 5, 2]

# Pop specific index
second = numbers.pop(1)  # Remove index 1
print(second)   # 4
print(numbers)  # [3, 5, 2]

# Clear all elements
numbers.clear()
print(numbers)  # []
```

### Modifying Elements
```python
fruits = ["apple", "banana", "cherry"]

# Direct assignment
fruits[1] = "blueberry"
print(fruits)  # ['apple', 'blueberry', 'cherry']

# Modify slice
fruits[1:3] = ["blackberry", "cranberry", "dragonfruit"]
print(fruits)  # ['apple', 'blackberry', 'cranberry', 'dragonfruit']

# Replace multiple elements
fruits[:2] = ["apricot"]
print(fruits)  # ['apricot', 'cranberry', 'dragonfruit']
```

## List Operations and Methods

### Searching and Counting
```python
numbers = [1, 2, 3, 4, 5, 2, 3, 2]

# Find index of element
print(numbers.index(2))     # 1 (first occurrence)
print(numbers.index(2, 2))  # 5 (search from index 2)

# Count occurrences
print(numbers.count(2))     # 3
print(numbers.count(6))     # 0

# Check membership
print(3 in numbers)         # True
print(6 in numbers)         # False
```

### Sorting
```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

# Sort in place
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 4, 5, 6, 9]

# Sort descending
numbers.sort(reverse=True)
print(numbers)  # [9, 6, 5, 4, 3, 2, 1, 1]

# Create sorted copy
original = [3, 1, 4, 1, 5]
sorted_copy = sorted(original)
print(original)    # [3, 1, 4, 1, 5] (unchanged)
print(sorted_copy) # [1, 1, 3, 4, 5]

# Sort strings
fruits = ["banana", "Apple", "cherry"]
fruits.sort()  # Case-sensitive: ['Apple', 'banana', 'cherry']
fruits.sort(key=str.lower)  # Case-insensitive: ['Apple', 'banana', 'cherry']
```

### Reversing
```python
numbers = [1, 2, 3, 4, 5]

# Reverse in place
numbers.reverse()
print(numbers)  # [5, 4, 3, 2, 1]

# Create reversed copy
original = [1, 2, 3, 4, 5]
reversed_copy = list(reversed(original))
print(original)      # [1, 2, 3, 4, 5] (unchanged)
print(reversed_copy) # [5, 4, 3, 2, 1]
```

### Copying Lists
```python
original = [1, 2, [3, 4]]

# Shallow copy
shallow = original.copy()
shallow = list(original)  # Alternative
shallow = original[:]      # Alternative

# Modify shallow copy
shallow[0] = 999
print(original)  # [1, 2, [3, 4]] (unchanged)
print(shallow)   # [999, 2, [3, 4]]

# But nested objects are shared!
shallow[2][0] = 888
print(original)  # [1, 2, [888, 4]] (nested list changed!)
print(shallow)   # [999, 2, [888, 4]]

# Deep copy for nested structures
import copy
deep = copy.deepcopy(original)
deep[2][0] = 777
print(original)  # [1, 2, [888, 4]] (unchanged)
print(deep)      # [1, 2, [777, 4]]
```

## List Comprehensions Advanced

### Multiple Iterables
```python
# Cartesian product
colors = ["red", "blue"]
sizes = ["small", "large"]
combinations = [f"{color} {size}" for color in colors for size in sizes]
print(combinations)  # ['red small', 'red large', 'blue small', 'blue large']

# Zip in comprehension
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
people = [f"{name} ({age})" for name, age in zip(names, ages)]
print(people)  # ['Alice (25)', 'Bob (30)', 'Charlie (35)']
```

### Conditional Logic
```python
# Complex conditions
numbers = range(1, 21)
result = [
    "fizzbuzz" if x % 15 == 0 else
    "fizz" if x % 3 == 0 else
    "buzz" if x % 5 == 0 else
    str(x)
    for x in numbers
]
print(result)
# ['1', '2', 'fizz', '4', 'buzz', 'fizz', '7', '8', 'fizz', 'buzz', '11', 'fizz', '13', '14', 'fizzbuzz', ...]
```

## Common List Patterns

### Filtering
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter manually
evens = []
for num in numbers:
    if num % 2 == 0:
        evens.append(num)

# Filter with comprehension
evens = [num for num in numbers if num % 2 == 0]

# Filter with built-in
evens = list(filter(lambda x: x % 2 == 0, numbers))

print(evens)  # [2, 4, 6, 8, 10]
```

### Mapping/Transformation
```python
numbers = [1, 2, 3, 4, 5]

# Transform manually
squares = []
for num in numbers:
    squares.append(num ** 2)

# Transform with comprehension
squares = [num ** 2 for num in numbers]

# Transform with built-in
squares = list(map(lambda x: x ** 2, numbers))

print(squares)  # [1, 4, 9, 16, 25]
```

### Accumulation
```python
numbers = [1, 2, 3, 4, 5]

# Sum manually
total = 0
for num in numbers:
    total += num

# Sum with built-in
total = sum(numbers)

# Custom accumulation
running_total = []
current = 0
for num in numbers:
    current += num
    running_total.append(current)

print(running_total)  # [1, 3, 6, 10, 15]
```

## List Performance Considerations

### Time Complexity
```python
# O(1) operations - constant time
my_list = [1, 2, 3, 4, 5]
len(my_list)        # Length lookup
my_list[0]          # Index access
my_list.append(6)   # Add to end

# O(n) operations - linear time
my_list.insert(0, 0)    # Insert at beginning (shifts all elements)
5 in my_list            # Membership test
my_list.remove(3)       # Remove by value (searches list)
my_list.index(4)        # Find index (searches list)

# O(n log n) operations
my_list.sort()          # Sorting
```

### Memory Usage
```python
# Lists have overhead for each element
# Empty list: 64 bytes (on 64-bit system)
# List with 1 element: ~100 bytes
# List with 10 elements: ~200 bytes

# Pre-allocating can improve performance for large lists
large_list = [None] * 10000  # Pre-allocate space
# vs
large_list = []
for i in range(10000):
    large_list.append(None)  # Resizes repeatedly
```

### Choosing the Right Approach
```python
# For simple transformations: list comprehensions
squares = [x**2 for x in range(10)]

# For complex logic: traditional loops
result = []
for item in data:
    if complex_condition(item):
        processed = complex_transformation(item)
        result.append(processed)

# For filtering: comprehensions with conditions
valid_items = [item for item in data if is_valid(item)]

# For mapping + filtering: comprehensions
processed = [transform(item) for item in data if condition(item)]
```

## Advanced List Techniques

### List Unpacking
```python
# Unpack list into variables
first, *middle, last = [1, 2, 3, 4, 5]
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5

# Ignore unwanted values
_, second, *_ = [1, 2, 3, 4, 5]
print(second)  # 2
```

### List as Stack/Queue
```python
# Stack (LIFO - Last In, First Out)
stack = []
stack.append(1)  # Push
stack.append(2)
stack.append(3)
print(stack.pop())  # 3 (pop last)
print(stack)        # [1, 2]

# Queue (FIFO - First In, First Out)
from collections import deque
queue = deque([1, 2, 3])
queue.append(4)     # Enqueue
print(queue.popleft())  # 1 (dequeue first)
print(list(queue))  # [2, 3, 4]
```

### List Flattening
```python
# Flatten nested lists
nested = [[1, 2], [3, 4], [5, 6]]

# Method 1: nested comprehension
flattened = [item for sublist in nested for item in sublist]

# Method 2: itertools.chain
from itertools import chain
flattened = list(chain.from_iterable(nested))

# Method 3: sum (works for numbers)
# flattened = sum(nested, [])  # [1, 2, 3, 4, 5, 6]

print(flattened)  # [1, 2, 3, 4, 5, 6]
```

## Key Takeaways

1. **Lists are mutable, ordered sequences** that can store any data type
2. **List comprehensions** provide concise ways to create and transform lists
3. **Indexing and slicing** allow flexible element access
4. **Methods like append, insert, remove** modify list contents
5. **Sorting and searching** are built-in operations
6. **Performance matters** - choose the right method for your use case

## Further Reading
- Python list documentation
- Time complexity analysis
- Advanced data structures (collections module)
- List vs array performance comparisons
- Memory optimization techniques