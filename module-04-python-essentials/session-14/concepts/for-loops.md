# For Loops: Iterating Over Collections

## Introduction to For Loops

For loops in Python iterate over sequences (like lists, strings, tuples) or other iterable objects. They automatically handle the iteration process, making them safer and more convenient than manual indexing.

## Basic For Loop Syntax

### Iterating Over Lists
```python
# Basic for loop
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(f"I like {fruit}")

# Output:
# I like apple
# I like banana
# I like cherry
```

### Iterating Over Strings
```python
# Strings are sequences of characters
message = "Hello"
for char in message:
    print(char)

# Output:
# H
# e
# l
# l
# o
```

### Iterating Over Ranges
```python
# Using range() for numbers
for i in range(5):  # 0, 1, 2, 3, 4
    print(f"Count: {i}")

# Range with start and end
for num in range(2, 6):  # 2, 3, 4, 5
    print(num)

# Range with step
for even in range(0, 10, 2):  # 0, 2, 4, 6, 8
    print(f"Even: {even}")
```

## Working with Indices

### Using enumerate()
```python
# Get both index and value
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: apple
# 1: banana
# 2: cherry

# Start enumeration from 1
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")

# Output:
# 1. apple
# 2. banana
# 3. cherry
```

### Manual Indexing (Not Recommended)
```python
# Less Pythonic, but possible
fruits = ["apple", "banana", "cherry"]
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# Same output as enumerate example
```

## Iterating Over Dictionaries

### Keys Only
```python
person = {"name": "Alice", "age": 25, "city": "New York"}

for key in person:
    print(f"Key: {key}")

# Output:
# Key: name
# Key: age
# Key: city
```

### Keys and Values
```python
for key, value in person.items():
    print(f"{key}: {value}")

# Output:
# name: Alice
# age: 25
# city: New York
```

### Values Only
```python
for value in person.values():
    print(f"Value: {value}")

# Output:
# Value: Alice
# Value: 25
# Value: New York
```

## Nested For Loops

### Basic Nesting
```python
# Multiplication table
for i in range(1, 4):  # 1, 2, 3
    for j in range(1, 4):  # 1, 2, 3
        print(f"{i} * {j} = {i * j}")
    print()  # Empty line after each row

# Output:
# 1 * 1 = 1
# 1 * 2 = 2
# 1 * 3 = 3
#
# 2 * 1 = 2
# etc.
```

### Iterating Over 2D Lists
```python
# Matrix (list of lists)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for element in row:
        print(element, end=" ")
    print()  # New line after each row

# Output:
# 1 2 3
# 4 5 6
# 7 8 9
```

## List Comprehensions

### Basic Comprehension
```python
# Traditional approach
numbers = [1, 2, 3, 4, 5]
squares = []
for num in numbers:
    squares.append(num ** 2)

print(squares)  # [1, 4, 9, 16, 25]

# List comprehension
squares = [num ** 2 for num in numbers]
print(squares)  # Same result
```

### Comprehension with Conditions
```python
# Filter even numbers
numbers = [1, 2, 3, 4, 5, 6]
evens = [num for num in numbers if num % 2 == 0]
print(evens)  # [2, 4, 6]

# Transform with condition
result = [num * 2 if num > 3 else num for num in numbers]
print(result)  # [1, 2, 3, 8, 10, 12]
```

### Nested Comprehensions
```python
# Flatten a matrix
matrix = [[1, 2], [3, 4], [5, 6]]
flattened = [num for row in matrix for num in row]
print(flattened)  # [1, 2, 3, 4, 5, 6]

# Create a multiplication table
table = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(table)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

## Iterating Over Files

### Reading Lines
```python
# Read all lines
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # Remove newline characters

# Process line by line with line numbers
with open("data.txt", "r") as file:
    for line_num, line in enumerate(file, start=1):
        print(f"Line {line_num}: {line.strip()}")
```

### Processing CSV-like Data
```python
# Simple CSV processing
data = [
    "Alice,25,Engineer",
    "Bob,30,Designer",
    "Charlie,35,Manager"
]

for row in data:
    name, age, job = row.split(",")
    print(f"{name} is {age} years old and works as {job}")
```

## Advanced Iteration Patterns

### Iterating with zip()
```python
# Parallel iteration
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

for name, age, city in zip(names, ages, cities):
    print(f"{name} ({age}) lives in {city}")

# Output:
# Alice (25) lives in NYC
# Bob (30) lives in LA
# Charlie (35) lives in Chicago
```

### Iterating in Reverse
```python
# Reverse iteration
fruits = ["apple", "banana", "cherry"]
for fruit in reversed(fruits):
    print(fruit)

# Output:
# cherry
# banana
# apple

# Reverse with indices
for i in reversed(range(len(fruits))):
    print(f"{i}: {fruits[i]}")
```

### Iterating with Step
```python
# Every other element
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# Using slice notation
for num in numbers[::2]:  # Start:0, End:len, Step:2
    print(num, end=" ")  # 0 2 4 6 8

print()

# Using range
for i in range(0, len(numbers), 2):
    print(numbers[i], end=" ")  # Same result
```

## Performance Considerations

### Avoid Modifying Lists During Iteration
```python
# Problematic - modifying while iterating
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)  # Modifying list during iteration

print(numbers)  # [1, 3, 5] - 4 was skipped!

# Better - create new list
numbers = [1, 2, 3, 4, 5]
odds = [num for num in numbers if num % 2 != 0]
print(odds)  # [1, 3, 5]
```

### Use Appropriate Data Structures
```python
# For membership testing, use sets
lookup_items = {"apple", "banana", "cherry"}  # Set for O(1) lookup
fruits = ["apple", "grape", "banana", "orange", "cherry"]

for fruit in fruits:
    if fruit in lookup_items:  # Fast lookup
        print(f"Found: {fruit}")
```

## Common For Loop Patterns

### Accumulator Pattern
```python
# Sum all numbers
numbers = [1, 2, 3, 4, 5]
total = 0
for num in numbers:
    total += num
print(f"Sum: {total}")  # 15

# Count occurrences
text = "hello world"
letter_counts = {}
for char in text:
    if char != " ":  # Skip spaces
        letter_counts[char] = letter_counts.get(char, 0) + 1

print(letter_counts)  # {'h': 1, 'e': 1, 'l': 3, 'o': 2, 'w': 1, 'r': 1, 'd': 1}
```

### Find Pattern
```python
# Find maximum
numbers = [3, 7, 2, 9, 5]
maximum = numbers[0] if numbers else None

for num in numbers[1:]:
    if num > maximum:
        maximum = num

print(f"Maximum: {maximum}")  # 9

# Find first match
fruits = ["apple", "banana", "cherry", "date"]
target = "cherry"
found_index = None

for i, fruit in enumerate(fruits):
    if fruit == target:
        found_index = i
        break  # Stop searching after first match

print(f"Found {target} at index {found_index}")
```

### Transform Pattern
```python
# Convert to uppercase
words = ["hello", "world", "python"]
upper_words = []

for word in words:
    upper_words.append(word.upper())

print(upper_words)  # ['HELLO', 'WORLD', 'PYTHON']

# Or using list comprehension
upper_words = [word.upper() for word in words]
print(upper_words)  # Same result
```

## Iterables vs Iterators

### Understanding Iterables
```python
# Lists are iterables
fruits = ["apple", "banana", "cherry"]
fruit_iter = iter(fruits)  # Create iterator

print(next(fruit_iter))  # "apple"
print(next(fruit_iter))  # "banana"
print(next(fruit_iter))  # "cherry"
# print(next(fruit_iter))  # StopIteration exception

# For loops handle this automatically
for fruit in fruits:  # Creates new iterator each time
    print(fruit)
```

### Creating Custom Iterables
```python
class Countdown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        return CountdownIterator(self.start)

class CountdownIterator:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1

# Usage
for num in Countdown(5):
    print(num, end=" ")  # 5 4 3 2 1
```

## Key Takeaways

1. **For loops iterate over sequences** automatically handling the iteration process
2. **Use enumerate()** for accessing both indices and values
3. **List comprehensions** provide concise ways to create new lists
4. **Nested loops** work with multi-dimensional data
5. **Be careful modifying collections** during iteration
6. **Choose the right iteration pattern** for your use case

## Further Reading
- Python iterator protocol and generators
- Advanced iteration patterns
- Performance optimization for loops
- Functional programming alternatives (map, filter, reduce)