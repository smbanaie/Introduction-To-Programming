# Session 15: Working with Strings

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will master string manipulation and text processing in Python
**Materials**: Whiteboard, string method examples, text processing scenarios

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What's the difference between for and while loops?
- **Hook Activity**: Show text transformation examples (uppercase, search/replace)
- **Question**: "How can programs manipulate and analyze text like word processors do?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Access and slice string characters
- Use string methods for manipulation
- Format and combine strings effectively
- Process text for real-world applications

### Agenda Overview (5 minutes)
1. String basics and indexing
2. String methods and operations
3. String formatting techniques
4. Text processing applications

---

## II. Main Content (50 minutes)

### A. String Basics and Indexing (15 minutes)

#### String Creation and Properties
```python
# String literals
text1 = "Hello World"
text2 = 'Python Programming'
text3 = """Multi-line
string"""

# Empty string
empty = ""

# String length
len(text1)  # 11

# Strings are immutable (cannot change individual characters)
# text1[0] = "h"  # This would cause an error
```

#### String Indexing
```python
text = "Python"
# Index:  0  1  2  3  4  5
# Char:   P  y  t  h  o  n
# Index: -6 -5 -4 -3 -2 -1

print(text[0])   # 'P' (first character)
print(text[5])   # 'n' (last character)
print(text[-1])  # 'n' (last character, negative index)
print(text[-2])  # 'o' (second to last)
```

#### String Slicing
```python
text = "Python Programming"

# Slice syntax: string[start:end:step]
print(text[0:6])    # 'Python' (characters 0-5)
print(text[7:])     # 'Programming' (from index 7 to end)
print(text[:6])     # 'Python' (from start to index 5)
print(text[::2])    # 'Pto rgamn' (every other character)
print(text[::-1])   # 'gnimmargorP nohtyP' (reversed)
```

### B. String Methods (20 minutes)

#### Case Conversion
```python
text = "Hello World"

text.upper()        # 'HELLO WORLD'
text.lower()        # 'hello world'
text.capitalize()   # 'Hello world'
text.title()        # 'Hello World'
text.swapcase()     # 'hELLO wORLD'
```

#### Searching and Finding
```python
text = "Python is amazing"

text.find("is")           # 7 (index where "is" starts)
text.find("not")          # -1 (not found)
text.index("is")          # 7 (same as find, but raises error if not found)
text.count("i")           # 2 (count occurrences)
text.startswith("Python") # True
text.endswith("amazing")  # True
```

#### Modification Methods
```python
text = "  Hello World  "

text.strip()              # 'Hello World' (remove whitespace)
text.lstrip()             # 'Hello World  ' (left strip)
text.rstrip()             # '  Hello World' (right strip)

text.replace("World", "Python")  # '  Hello Python  '
text.split()              # ['Hello', 'World'] (split on spaces)
text.split("l")           # ['  He', '', 'o Wor', 'd  '] (split on 'l')
```

#### Testing Methods
```python
text = "Hello123"

text.isalpha()     # False (contains numbers)
text.isdigit()     # False (contains letters)
text.isalnum()     # True (letters and numbers)
text.islower()     # False (mixed case)
text.isupper()     # False (not all upper)
text.isspace()     # False (not all whitespace)
```

#### Join and Split
```python
# Join: combine strings with separator
words = ["Hello", "World", "Python"]
" ".join(words)           # 'Hello World Python'
"-".join(words)           # 'Hello-World-Python'

# Split: break string into list
text = "apple,banana,cherry"
text.split(",")           # ['apple', 'banana', 'cherry']
```

### C. String Formatting and Operations (15 minutes)

#### String Concatenation
```python
# Using + operator
first = "Hello"
last = "World"
full = first + " " + last  # 'Hello World'

# Using join (more efficient for many strings)
parts = ["Hello", "beautiful", "world"]
" ".join(parts)  # 'Hello beautiful world'
```

#### F-String Formatting (Modern)
```python
name = "Alice"
age = 25
height = 1.68

# Basic f-string
f"Hello, {name}!"  # 'Hello, Alice!'

# With expressions
f"Next year you will be {age + 1} years old."

# With formatting
f"Height: {height:.2f} meters"  # 'Height: 1.68 meters'
f"Age: {age:03d}"              # 'Age: 025' (zero-padded)
```

#### Format Method
```python
# Positional formatting
"{} is {} years old".format(name, age)  # 'Alice is 25 years old'

# Named formatting
"{name} is {age} years old and {height:.1f}m tall".format(
    name=name, age=age, height=height)
```

#### String Operations
```python
# Repetition
"Ha" * 3        # 'HaHaHa'

# Membership
"a" in "banana" # True
"z" in "banana" # False

# Comparison
"apple" < "banana"  # True (alphabetical order)
"Apple" < "apple"   # True (ASCII order: 'A' < 'a')
```

---

## III. Interactive Activities (15 minutes)

### String Manipulation Workshop (10 minutes)
- **Individual**: Apply string methods to transform text
- **Examples**: Case conversion, finding substrings, replacing text
- **Challenge**: Create a text cleaner (remove extra spaces, fix case)

### Text Processing Scenarios (5 minutes)
- **Groups**: Solve real problems with string operations
- **Examples**: Parse names, validate emails, format addresses
- **Present**: Share solutions and discuss approaches

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Strings are sequences**: Access with indexing and slicing
2. **Rich method library**: 40+ methods for text manipulation
3. **Formatting options**: f-strings, format(), concatenation
4. **Immutable but changeable**: Create new strings from operations

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. How do you get the first character of "Hello"?
2. What does "hello".upper() return?
3. Write an f-string with name and age variables

### Preview of Next Session (2 minutes)
"Next time we'll learn collections - storing multiple values together!"

---

## Additional Resources
- **Visual Aid**: String method reference chart
- **Handout**: Common string operation patterns
- **Homework**: Create a name formatter program

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes