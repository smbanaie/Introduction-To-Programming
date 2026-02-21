# Expressions and Operators: Building Computations

## What Are Expressions?

Expressions are combinations of values, variables, and operators that Python evaluates to produce a result. They are the building blocks of computations in programming.

## Arithmetic Operators

### Basic Math Operations
```python
# Addition
result = 5 + 3  # 8

# Subtraction
result = 10 - 4  # 6

# Multiplication
result = 6 * 7   # 42

# Division (floating point)
result = 15 / 4  # 3.75

# Integer division (floor division)
result = 15 // 4 # 3

# Modulo (remainder)
result = 15 % 4  # 3

# Exponentiation
result = 2 ** 3  # 8
result = 2 ** 0.5  # 1.4142135623730951 (square root)
```

### Operator Precedence
Python follows mathematical order of operations:

```python
# PEMDAS: Parentheses, Exponents, Multiplication/Division, Addition/Subtraction
result = 2 + 3 * 4       # 14 (multiplication first)
result = (2 + 3) * 4     # 20 (parentheses force addition first)
result = 2 ** 3 * 2      # 16 (exponentiation before multiplication)
result = 10 - 5 + 2      # 7 (left to right for same precedence)
```

### Augmented Assignment Operators
```python
x = 5

x += 3   # x = x + 3 → 8
x -= 2   # x = x - 2 → 6
x *= 4   # x = x * 4 → 24
x /= 2   # x = x / 2 → 12.0
x //= 3  # x = x // 3 → 4.0
x %= 3   # x = x % 3 → 1.0
x **= 2  # x = x ** 2 → 1.0
```

## Comparison Operators

### Basic Comparisons
```python
# Equal to
result = 5 == 5      # True
result = 5 == 6      # False

# Not equal to
result = 5 != 6      # True
result = 5 != 5      # False

# Greater than
result = 7 > 5       # True
result = 5 > 7       # False

# Less than
result = 3 < 8       # True
result = 8 < 3       # False

# Greater than or equal
result = 5 >= 5      # True
result = 5 >= 3      # True

# Less than or equal
result = 4 <= 4      # True
result = 4 <= 6      # True
```

### String Comparisons
```python
# Lexicographic comparison (dictionary order)
result = "apple" < "banana"    # True ('a' comes before 'b')
result = "Apple" < "apple"     # True (uppercase before lowercase)
result = "apple" == "Apple"    # False (case sensitive)
```

### Chaining Comparisons
```python
# Multiple comparisons
x = 5
result = 3 < x < 10   # True (equivalent to 3 < x and x < 10)
result = x < 10 > 7   # True (equivalent to x < 10 and 10 > 7)

# More complex chains
age = 25
result = 18 <= age <= 65  # True (valid working age)
```

## Logical Operators

### Boolean Logic
```python
# AND: both conditions must be true
result = True and True    # True
result = True and False   # False
result = (5 > 3) and (10 < 20)  # True

# OR: at least one condition must be true
result = True or False    # True
result = False or False   # False
result = (5 < 3) or (10 > 5)  # True

# NOT: reverses the truth value
result = not True         # False
result = not False        # True
result = not (5 > 3)      # False
```

### Short-Circuit Evaluation
Python stops evaluating as soon as the result is known:

```python
# AND short-circuit
def check_condition():
    print("Checking condition...")
    return True

# If first part is False, second part isn't evaluated
result = False and check_condition()  # Doesn't print "Checking condition..."

# OR short-circuit
result = True or check_condition()    # Doesn't print "Checking condition..."
```

### Complex Logical Expressions
```python
# User validation
age = 25
has_id = True
is_student = False

# Complex condition with parentheses
can_enter = (age >= 18 and has_id) or is_student
print(can_enter)  # True

# Nested conditions
is_eligible = age >= 18 and (has_id or is_student)
print(is_eligible)  # True
```

## Bitwise Operators

### Binary Operations
```python
# AND (&): 1 only where both bits are 1
result = 5 & 3   # 1 (binary: 101 & 011 = 001)

# OR (|): 1 where either bit is 1
result = 5 | 3   # 7 (binary: 101 | 011 = 111)

# XOR (^): 1 where bits are different
result = 5 ^ 3   # 6 (binary: 101 ^ 011 = 110)

# NOT (~): Flip all bits
result = ~5      # -6 (two's complement)

# Left shift (<<): Move bits left
result = 5 << 1  # 10 (binary: 101 → 1010)

# Right shift (>>): Move bits right
result = 10 >> 1 # 5 (binary: 1010 → 101)
```

### Practical Bitwise Applications
```python
# Check if number is even
is_even = (number & 1) == 0

# Check if number is power of 2
is_power_of_2 = (number & (number - 1)) == 0 and number > 0

# Extract individual bits
bit_0 = number & 1
bit_1 = (number >> 1) & 1
bit_2 = (number >> 2) & 1
```

## Membership and Identity Operators

### Membership Operators
```python
# in: check if value exists in collection
result = 5 in [1, 2, 3, 4, 5]        # True
result = "a" in "banana"              # True
result = "z" in "banana"              # False
result = "key" in {"key": "value"}    # True (checks keys)

# not in: opposite of in
result = 6 not in [1, 2, 3, 4, 5]    # True
```

### Identity Operators
```python
# is: check if two variables reference the same object
a = [1, 2, 3]
b = a
c = [1, 2, 3]

result = a is b     # True (same object)
result = a is c     # False (different objects, same content)

# is not: opposite of is
result = a is not c # True

# Important: Don't use == with None, use is
result = None is None     # True
result = value is None    # Correct way to check for None
```

## Expression Evaluation Order

### Complete Precedence Table
From highest to lowest precedence:

```python
# 1. Parentheses
result = (2 + 3) * 4   # 20

# 2. Exponentiation
result = 2 ** 3 ** 2   # 512 (right to left)

# 3. Unary operators (+, -, ~)
result = -2 ** 2       # -4 (not (-2)**2)

# 4. Multiplication, division, modulo
result = 10 * 2 + 5    # 25 (not 10*(2+5))

# 5. Addition, subtraction
result = 10 + 5 * 2    # 20

# 6. Bitwise shifts
result = 1 << 2 + 1    # 8 (1 << (2 + 1))

# 7. Bitwise AND
result = 5 & 3 | 2     # 2 ((5 & 3) | 2)

# 8. Bitwise XOR
# 9. Bitwise OR

# 10. Comparison operators
result = 5 < 10 == True  # False ((5 < 10) == True)

# 11. Identity operators (is, is not)

# 12. Membership operators (in, not in)

# 13. Logical NOT

# 14. Logical AND

# 15. Logical OR
```

### Associativity
```python
# Left-associative (most operators)
result = 10 - 5 - 2   # (10 - 5) - 2 = 3

# Right-associative (exponentiation, assignment)
result = 2 ** 3 ** 2  # 2 ** (3 ** 2) = 512
x = y = z = 5        # All variables become 5
```

## Conditional Expressions

### Ternary Operator
```python
# condition ? true_value : false_value (other languages)
# Python syntax: true_value if condition else false_value

age = 25
status = "adult" if age >= 18 else "minor"
print(status)  # "adult"

# More complex example
x = 10
y = 20
maximum = x if x > y else y
print(maximum)  # 20

# Nested ternary
score = 85
grade = "A" if score >= 90 else ("B" if score >= 80 else "C")
print(grade)  # "B"
```

## Lambda Expressions

### Anonymous Functions
```python
# Regular function
def add(x, y):
    return x + y

# Lambda equivalent
add_lambda = lambda x, y: x + y

# Usage
result = add_lambda(3, 5)  # 8

# Common use cases
numbers = [1, 2, 3, 4, 5]

# Sort by custom key
sorted_numbers = sorted(numbers, key=lambda x: -x)  # [5, 4, 3, 2, 1]

# Filter with condition
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]

# Transform elements
squared = list(map(lambda x: x ** 2, numbers))  # [1, 4, 9, 16, 25]
```

## Expression Best Practices

### Readability
```python
# Clear and readable
if age >= 18 and has_license:
    can_drive = True

# Less readable (but equivalent)
can_drive = age >= 18 and has_license

# Even less readable
can_drive = 18 <= age and has_license
```

### Avoiding Common Mistakes
```python
# Wrong: assignment instead of comparison
if x = 5:  # SyntaxError in Python (unlike C/C++)
    print("This won't work")

# Correct
if x == 5:
    print("Equal to 5")

# Careful with floating point
if abs(a - b) < 0.0001:  # Use epsilon for float comparison
    print("Approximately equal")

# None checking
if value is None:  # Use 'is' for None
    print("No value")
```

### Complex Expressions
```python
# Break complex expressions into parts
is_valid_user = (
    user is not None and
    user.age >= 18 and
    user.is_active and
    user.email_verified
)

# Or use intermediate variables
user_exists = user is not None
is_adult = user.age >= 18 if user_exists else False
is_active = user.is_active if user_exists else False
is_verified = user.email_verified if user_exists else False

is_valid_user = user_exists and is_adult and is_active and is_verified
```

## Performance Considerations

### Short-Circuit Evaluation Benefits
```python
# Avoid expensive operations when possible
if user_exists and user_has_permission():  # Second function not called if user doesn't exist
    perform_action()
```

### Expression Optimization
```python
# Python optimizes some expressions
x = 5
y = x * 2 + 10  # Calculated efficiently

# But don't over-optimize prematurely
# Readable code is better than micro-optimized code
```

## Key Takeaways

1. **Expressions combine values and operators** to produce results
2. **Operator precedence** determines evaluation order
3. **Logical operators** enable complex conditions
4. **Comparison operators** work with different data types
5. **Bitwise operators** manipulate binary representations
6. **Clarity matters** more than clever expressions

## Further Reading
- Python operator precedence documentation
- Boolean logic and truth tables
- Bit manipulation techniques
- Functional programming with lambda expressions
- Expression optimization strategies