# Evaluation Order and Precedence: Expression Processing

## How Python Evaluates Expressions

Understanding how Python processes expressions is crucial for writing correct and predictable code. Expression evaluation follows strict rules of precedence and associativity.

## Operator Precedence Hierarchy

Python evaluates operators in a specific order, from highest to lowest precedence:

### 1. Parentheses (Grouping)
```python
# Parentheses override all other precedence
result = (2 + 3) * 4     # 20 (addition happens first)
result = 2 + (3 * 4)     # 14 (multiplication happens first)

# Nested parentheses
result = ((2 + 3) * 4) - 1  # 19
```

### 2. Function Calls and Attribute Access
```python
# Function calls have very high precedence
result = len("hello") + 5  # 10 (len("hello") = 5, then + 5)

# Method calls
result = "hello".upper().count('L')  # 2

# Attribute access
result = math.pi * 2  # Access pi first, then multiply
```

### 3. Exponentiation
```python
# Right-associative
result = 2 ** 3 ** 2      # 512 (2^(3^2) = 2^9 = 512)
result = (2 ** 3) ** 2    # 64 (8^2 = 64)

# Mixed with other operators
result = 2 * 3 ** 2       # 18 (3^2 = 9, then 2*9)
```

### 4. Unary Operators
```python
# Positive, negative, bitwise NOT
result = -2 ** 2          # -4 (not (-2)**2)
result = -(2 ** 2)        # -4 (same as above)
result = ~5 + 3           # -3 (bitwise NOT first, then add)

# Logical NOT
result = not True or False  # False (not first, then or)
```

### 5. Multiplication, Division, Modulo
```python
# Left-associative, same precedence level
result = 10 * 2 / 5       # 4.0 (10*2=20, 20/5=4.0)
result = 10 / 2 * 5       # 25.0 (10/2=5.0, 5.0*5=25.0)

# Integer division and modulo
result = 17 // 3 % 2      # 1 ((17//3)=5, 5%2=1)
```

### 6. Addition and Subtraction
```python
# Left-associative
result = 10 - 5 + 2       # 7 ((10-5)=5, 5+2=7)
result = 10 + 5 - 2       # 13 ((10+5)=15, 15-2=13)
```

### 7. Bitwise Shifts
```python
# Left and right shift
result = 8 >> 1 + 1       # 2 (1+1=2, then 8>>2)
result = (8 >> 1) + 1     # 5 (8>>1=4, 4+1=5)
```

### 8. Bitwise AND
```python
result = 5 & 3 | 2        # 2 ((5&3)=1, 1|2=2)
```

### 9. Bitwise XOR
```python
result = 5 ^ 3 | 2        # 7 ((5^3)=6, 6|2=7)
```

### 10. Bitwise OR
```python
result = 5 | 3 & 2        # 7 ((3&2)=2, 5|2=7)
```

### 11. Comparison Operators
```python
# All have same precedence, left-associative
result = 5 < 10 == True   # False ((5<10)=True, True==True, but chained differently)
result = 5 < 10 and 10 == 10  # True (comparison before logical)
```

### 12. Identity Operators (is, is not)
```python
# After comparisons
result = x is None or x == 0  # Check identity first
```

### 13. Membership Operators (in, not in)
```python
result = x in [1, 2, 3] and x > 0
```

### 14. Logical NOT
```python
result = not x > 5 and y < 10
```

### 15. Logical AND
```python
result = x > 5 and y < 10 or z == 0
```

### 16. Logical OR
```python
result = x or y and z  # Equivalent to x or (y and z)
```

## Associativity Rules

### Left-Associative Operators
Most operators group from left to right:
```python
# Addition/subtraction
result = 10 - 5 - 2     # (10 - 5) - 2 = 3

# Multiplication/division
result = 10 / 2 * 5     # (10 / 2) * 5 = 25.0

# Comparisons (chained)
result = 1 < 2 < 3      # (1 < 2) and (2 < 3) = True
```

### Right-Associative Operators
Few operators group from right to left:
```python
# Exponentiation
result = 2 ** 3 ** 2    # 2 ** (3 ** 2) = 512

# Assignment operators
x = y = z = 5          # z = 5, then y = z, then x = y
```

## Short-Circuit Evaluation

### Logical Operators
Python stops evaluating when result is certain:

```python
# AND: stops at first False
def expensive_check():
    print("Expensive operation!")
    return True

result = False and expensive_check()  # Doesn't call expensive_check()
result = True and expensive_check()   # Calls expensive_check()

# OR: stops at first True
result = True or expensive_check()    # Doesn't call expensive_check()
result = False or expensive_check()   # Calls expensive_check()
```

### Practical Applications
```python
# Safe division
def safe_divide(a, b):
    return b != 0 and a / b

result = safe_divide(10, 0)   # False (no division by zero)
result = safe_divide(10, 2)   # 5.0

# Null-safe attribute access
user = None
name = user and user.name  # None (doesn't access .name on None)
```

## Evaluation Context

### Eager vs Lazy Evaluation
```python
# Python uses eager evaluation (evaluates all arguments)
def add(a, b):
    return a + b

result = add(2 * 3, 4 + 5)  # Evaluates 6 and 9, then adds

# But logical operators are lazy
result = True or expensive_function()  # expensive_function not called
```

### List Comprehensions
```python
# All expressions evaluated eagerly
squares = [x**2 for x in range(1, 6)]  # [1, 4, 9, 16, 25]

# Generator expressions (lazy)
squares_gen = (x**2 for x in range(1, 6))  # Not evaluated yet
list(squares_gen)  # [1, 4, 9, 16, 25] - evaluated now
```

## Common Precedence Mistakes

### Mathematical Expressions
```python
# Common mistake
result = 3 + 4 * 2     # 11 (not 14)
# Correct understanding
result = 3 + (4 * 2)   # 11

# Another mistake
result = 10 / 2 * 3    # 15.0 (not 1.666...)
# Correct: (10 / 2) * 3 = 15.0
```

### Comparison Chains
```python
# Unexpected behavior
result = 5 < 10 == True  # False!
# Because: (5 < 10) == True → True == True → True
# But chained as: 5 < 10 and 10 == True → False

# Correct way
result = 5 < 10 and 10 == 10  # True
```

### Bitwise and Logical Operators
```python
# Bitwise has higher precedence than comparison
result = x & y == 0     # (x & y) == 0
result = x & (y == 0)   # Usually not what you want

# Logical AND has lower precedence than comparison
result = x > 5 and y < 10  # Correct
result = x > 5 & y < 10    # Bitwise AND! Probably wrong
```

## Best Practices for Expression Clarity

### Use Parentheses for Clarity
```python
# Clear intent
if (age >= 18) and (has_license or has_permit):
    can_drive = True

# Unclear (but equivalent)
if age >= 18 and has_license or has_permit:
    can_drive = True  # Wrong! OR has lower precedence
```

### Break Complex Expressions
```python
# Hard to read
if x > 0 and y > 0 and z > 0 and x + y + z < 100:

# Better
coordinates_valid = x > 0 and y > 0 and z > 0
sum_valid = x + y + z < 100
if coordinates_valid and sum_valid:
```

### Avoid Overly Complex Expressions
```python
# Too complex - hard to debug
result = (a if condition1 else b) + (c if condition2 else d) * (e if condition3 else f)

# Better - use intermediate variables
first_value = a if condition1 else b
second_value = c if condition2 else d
third_value = e if condition3 else f
result = first_value + second_value * third_value
```

## Performance Implications

### Expression Optimization
```python
# Python optimizes some expressions at compile time
x = 2 + 3  # Constant folding: becomes 5

# But dynamic expressions are evaluated at runtime
x = a + b  # Evaluated each time
```

### Short-Circuit Benefits
```python
# Avoid expensive operations
if user_exists and validate_user_permissions(user):
    grant_access()

# Better than
if user_exists:
    if validate_user_permissions(user):
        grant_access()
```

## Debugging Expression Evaluation

### Print Debugging
```python
# Debug complex expressions
x, y, z = 5, 10, 15
result = x + y * z / 2

# Add debug prints
print(f"x = {x}, y = {y}, z = {z}")
print(f"y * z = {y * z}")
print(f"(y * z) / 2 = {(y * z) / 2}")
print(f"x + ((y * z) / 2) = {result}")
```

### Using Python's AST
```python
import ast

# Parse expression to see structure
expression = "x + y * z / 2"
tree = ast.parse(expression, mode='eval')
print(ast.dump(tree, indent=2))
```

## Key Takeaways

1. **Precedence determines evaluation order** - higher precedence operators first
2. **Associativity** resolves same-precedence operators (usually left-to-right)
3. **Parentheses override precedence** - use for clarity
4. **Short-circuit evaluation** can improve performance
5. **Complex expressions** should be broken down for readability

## Further Reading
- Python language reference on expressions
- Compiler optimization techniques
- Functional programming evaluation strategies
- Expression parsing and abstract syntax trees