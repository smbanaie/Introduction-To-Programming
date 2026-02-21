# Session 11: Variables & Data Types

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will understand variables and Python's main data types
**Materials**: Whiteboard, data type examples, variable naming rules

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you print text in Python?
- **Hook Activity**: Show variables changing values in REPL
- **Question**: "How does Python remember information between operations?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Create and use variables in Python
- Understand Python's main data types
- Apply appropriate data types to different information
- Follow variable naming conventions

### Agenda Overview (5 minutes)
1. Introduction to variables
2. Python data types
3. Variable naming and best practices
4. Type conversion and operations

---

## II. Main Content (50 minutes)

### A. Variables Fundamentals (15 minutes)

#### What are Variables?
- **Storage containers**: Hold data values in memory
- **Named references**: Use names to access stored values
- **Changeable**: Can update variable contents
- **Abstraction**: Represent concepts with meaningful names

#### Variable Assignment
```python
# Basic assignment
age = 25
name = "Alice"
is_student = True

# Multiple assignment
x, y, z = 1, 2, 3

# Same value to multiple variables
a = b = c = 0
```

#### Variable Operations
```python
# Reading variables
print(name)      # Alice
print(age + 5)   # 30

# Updating variables
age = age + 1    # Increment
name = name + " Johnson"  # Concatenate
```

#### Variable Memory Model
```
name → "Alice"    (string in memory)
age  → 25         (integer in memory)
```

### B. Python Data Types (20 minutes)

#### Core Data Types

| Type | Description | Examples | Use Case |
|------|-------------|----------|----------|
| **int** | Whole numbers | 42, -17, 0 | Counting, ages, quantities |
| **float** | Decimal numbers | 3.14, -2.5, 1.0 | Measurements, prices, averages |
| **str** | Text strings | "Hello", 'Python' | Names, messages, labels |
| **bool** | True/False | True, False | Conditions, flags, switches |

#### Type Examples in Code
```python
# Integers
students = 25
temperature = -5
year = 2024

# Floats
pi = 3.14159
price = 19.99
weight = 65.5

# Strings
message = "Welcome to class!"
name = 'Python'
empty = ""

# Booleans
is_raining = False
has_passed = True
is_active = True
```

#### Type Checking
```python
# Check variable types
type(age)        # <class 'int'>
type(name)       # <class 'str'>
type(price)      # <class 'float'>
type(is_student) # <class 'bool'>
```

### C. Variable Naming & Best Practices (15 minutes)

#### Naming Rules
- **Letters, numbers, underscores**: No spaces or special characters
- **Start with letter or underscore**: Never start with number
- **Case sensitive**: age ≠ Age ≠ AGE
- **No Python keywords**: Don't use print, if, for, etc.

#### Naming Conventions
```python
# Good naming (descriptive and clear)
student_count = 25
user_name = "Alice"
total_price = 99.95
is_logged_in = True

# Bad naming (unclear)
x = 25
a = "Alice"
tp = 99.95
ili = True
```

#### Python Keywords (Avoid)
```
False, None, True, and, as, assert, async, await, break, class, continue, def, del, elif, else, except, finally, for, from, global, if, import, in, is, lambda, nonlocal, not, or, pass, raise, return, try, while, with, yield
```

#### Best Practices
- **Descriptive names**: Use full words, avoid abbreviations
- **Consistent style**: snake_case for variables (word_word)
- **Logical grouping**: Related variables together
- **Comments**: Explain complex variable purposes

---

## III. Interactive Activities (15 minutes)

### Variable Creation Challenge (10 minutes)
- **Individual**: Create variables for personal information
- **Requirements**: Use all 4 data types, good naming
- **Share**: Present variable choices and explain reasoning

### Type Exploration Game (5 minutes)
- **Groups**: Predict and check types of expressions
- **Examples**: 5 + 3.0, "Hello" + "World", 10 > 5
- **Discussion**: Why does Python choose certain types?

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Variables store data**: Named containers for information
2. **Four main types**: int, float, str, bool for different data
3. **Naming matters**: Clear, descriptive names following rules
4. **Type awareness**: Understanding data types prevents errors

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Create a variable named 'score' with value 95
2. What data type is "Hello World"?
3. Name one variable naming rule

### Preview of Next Session (2 minutes)
"Next time we'll learn input/output and expressions - making programs interactive!"

---

## Additional Resources
- **Visual Aid**: Data type comparison chart
- **Handout**: Variable naming rules
- **Homework**: Create 10 variables using different data types

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes