# Session 16: Collections (lists, dicts, etc.)

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will use Python collections to store and manipulate multiple values
**Materials**: Whiteboard, collection type comparison, data structure examples

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you convert a string to uppercase?
- **Hook Activity**: Show organizing data with lists vs individual variables
- **Question**: "How can programs store collections of related data efficiently?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Create and manipulate lists for ordered data
- Use dictionaries for key-value data
- Work with tuples for immutable sequences
- Choose appropriate collection types for different scenarios

### Agenda Overview (5 minutes)
1. Lists: ordered, mutable sequences
2. Dictionaries: key-value mappings
3. Tuples and other collections
4. Collection operations and methods

---

## II. Main Content (50 minutes)

### A. Lists (20 minutes)

#### List Basics
```python
# Creating lists
empty_list = []
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "hello", True, 3.14]

# List length
len(numbers)  # 5

# Accessing elements (same as strings)
numbers[0]    # 1 (first element)
numbers[-1]   # 5 (last element)
numbers[1:3]  # [2, 3] (slicing)
```

#### List Modification
```python
fruits = ["apple", "banana", "cherry"]

# Add elements
fruits.append("date")        # ["apple", "banana", "cherry", "date"]
fruits.insert(1, "apricot")  # ["apple", "apricot", "banana", "cherry", "date"]

# Remove elements
fruits.remove("banana")      # ["apple", "apricot", "cherry", "date"]
last = fruits.pop()          # Remove and return last element ("date")
first = fruits.pop(0)        # Remove and return first element ("apple")

# Modify elements
fruits[1] = "blueberry"      # ["apricot", "blueberry", "cherry"]
```

#### List Operations
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# Concatenation
combined = list1 + list2     # [1, 2, 3, 4, 5, 6]

# Repetition
repeated = list1 * 3         # [1, 2, 3, 1, 2, 3, 1, 2, 3]

# Membership
2 in list1                   # True
7 in list1                   # False

# Finding
numbers = [10, 20, 30, 20]
numbers.index(20)            # 1 (first occurrence)
numbers.count(20)            # 2 (number of occurrences)
```

#### List Methods
```python
numbers = [3, 1, 4, 1, 5]

# Sorting
numbers.sort()               # [1, 1, 3, 4, 5] (modifies original)
sorted_nums = sorted(numbers) # [1, 1, 3, 4, 5] (returns new list)

# Reversing
numbers.reverse()            # [5, 4, 3, 1, 1]

# Clearing
numbers.clear()              # []

# Copying
original = [1, 2, 3]
copy_list = original.copy()  # [1, 2, 3] (shallow copy)
```

### B. Dictionaries (15 minutes)

#### Dictionary Basics
```python
# Creating dictionaries
empty_dict = {}
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Alternative syntax
person2 = dict(name="Bob", age=30, city="London")

# Accessing values
person["name"]     # "Alice"
person["age"]      # 25
person.get("city") # "New York"
person.get("salary", "Not specified")  # Default value
```

#### Dictionary Modification
```python
person = {"name": "Alice", "age": 25}

# Add/update items
person["city"] = "Boston"      # Add new key-value pair
person["age"] = 26             # Update existing value

# Remove items
del person["age"]              # Remove specific key
city = person.pop("city")      # Remove and return value
person.clear()                 # Remove all items
```

#### Dictionary Operations
```python
person = {"name": "Alice", "age": 25, "city": "Boston"}

# Check membership
"name" in person              # True (checks keys)
"Alice" in person             # False (doesn't check values)

# Get all keys/values
person.keys()                 # dict_keys(['name', 'age', 'city'])
person.values()               # dict_values(['Alice', 25, 'Boston'])
person.items()                # dict_items([('name', 'Alice'), ('age', 25), ('city', 'Boston')])

# Length
len(person)                   # 3
```

#### Dictionary Use Cases
```python
# Student grades
grades = {"Alice": 95, "Bob": 87, "Charlie": 92}
grades["Alice"]  # 95

# Configuration settings
config = {
    "debug": True,
    "max_users": 100,
    "timeout": 30
}

# Word frequency counter
text = "hello world hello python world"
word_count = {}
for word in text.split():
    word_count[word] = word_count.get(word, 0) + 1
# {"hello": 2, "world": 2, "python": 1}
```

### C. Tuples and Other Collections (15 minutes)

#### Tuples (Immutable Lists)
```python
# Creating tuples
empty_tuple = ()
single_item = (42,)           # Note the comma!
coordinates = (10, 20)
colors = ("red", "green", "blue")

# Tuple operations (similar to lists)
len(coordinates)              # 2
coordinates[0]                # 10
coordinates[1:]               # (20,)

# Tuples are immutable
# coordinates[0] = 15  # Error!
```

#### Tuple Use Cases
```python
# Returning multiple values from functions
def get_user_info():
    return ("Alice", 25, "Engineer")

name, age, job = get_user_info()

# Dictionary keys (lists can't be keys)
locations = {
    (40.7128, -74.0060): "New York",
    (34.0522, -118.2437): "Los Angeles"
}

# Unpacking
x, y = coordinates
first, *rest = [1, 2, 3, 4]  # first=1, rest=[2,3,4]
```

#### Sets (Unique Collections)
```python
# Creating sets
empty_set = set()
fruits = {"apple", "banana", "cherry"}
numbers = set([1, 2, 2, 3, 3, 3])  # {1, 2, 3} (duplicates removed)

# Set operations
fruits.add("date")            # Add item
fruits.remove("banana")       # Remove item
fruits.discard("grape")       # Remove if exists (no error)

# Mathematical set operations
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
set1 | set2  # Union: {1, 2, 3, 4, 5, 6}
set1 & set2  # Intersection: {3, 4}
set1 - set2  # Difference: {1, 2}
```

#### Choosing the Right Collection
- **List**: Ordered, mutable, allows duplicates
- **Dictionary**: Key-value pairs, fast lookup
- **Tuple**: Ordered, immutable, allows duplicates
- **Set**: Unordered, unique elements, fast membership tests

---

## III. Interactive Activities (15 minutes)

### Collection Builder Challenge (10 minutes)
- **Individual**: Create collections for different scenarios
- **Examples**: Shopping list (list), contact book (dict), coordinates (tuple)
- **Operations**: Add, remove, search, modify elements

### Data Structure Selection (5 minutes)
- **Groups**: Choose appropriate collections for real problems
- **Discuss**: Why one collection over another?
- **Present**: Defend collection choices

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Lists**: Ordered, mutable sequences for collections of items
2. **Dictionaries**: Key-value pairs for associative data
3. **Tuples**: Immutable sequences for fixed data
4. **Choose wisely**: Each collection type serves different purposes

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Create a list with 3 colors
2. How do you add an item to a list?
3. What's the difference between a list and tuple?

### Preview of Next Module (2 minutes)
"Next module we'll dive into software development - functions, error handling, and complete programs!"

---

## Additional Resources
- **Visual Aid**: Collection type comparison chart
- **Handout**: Common collection operations
- **Homework**: Create a student grade management system

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes