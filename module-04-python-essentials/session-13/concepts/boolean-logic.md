# Boolean Logic: Foundation of Decision Making

## What is Boolean Logic?

Boolean logic deals with true/false values and operations. It's the foundation of all decision-making in programming, enabling computers to make choices based on conditions.

## Boolean Values

### True and False
```python
# Boolean literals
is_active = True
is_deleted = False

# Boolean type
print(type(True))    # <class 'bool'>
print(type(False))   # <class 'bool'>
```

### Creating Booleans from Other Types
```python
# From numbers
bool(0)        # False
bool(1)        # True
bool(-5)       # True (any non-zero)

# From strings
bool("")       # False (empty string)
bool("hello")  # True (non-empty string)

# From collections
bool([])       # False (empty list)
bool([1, 2])   # True (non-empty list)
bool({})       # False (empty dict)
bool({1: 2})   # True (non-empty dict)

# From None
bool(None)     # False
```

## Logical Operators

### NOT Operator
```python
# Reverses truth value
not True       # False
not False      # True

# Practical examples
is_logged_in = False
if not is_logged_in:
    print("Please log in")

# Double negative
not not True   # True (not common, but valid)
```

### AND Operator
```python
# True only if both operands are True
True and True    # True
True and False   # False
False and True   # False
False and False  # False

# Short-circuit evaluation
def expensive_check():
    print("Expensive operation!")
    return True

# Second operand not evaluated if first is False
False and expensive_check()  # Doesn't print, returns False

# Second operand evaluated if first is True
True and expensive_check()   # Prints, returns True
```

### OR Operator
```python
# True if at least one operand is True
True or True     # True
True or False    # True
False or True    # True
False or False   # False

# Short-circuit evaluation
False or expensive_check()   # Prints, returns True
True or expensive_check()    # Doesn't print, returns True
```

## Truth Tables

### NOT Truth Table
```
P     | NOT P
------|-------
True  | False
False | True
```

### AND Truth Table
```
P     | Q     | P AND Q
------|-------|---------
True  | True  | True
True  | False | False
False | True  | False
False | False | False
```

### OR Truth Table
```
P     | Q     | P OR Q
------|-------|--------
True  | True  | True
True  | False | True
False | True  | True
False | False | False
```

## Comparison Operators

### Equality and Inequality
```python
# Equal to
5 == 5        # True
5 == 6        # False
"hello" == "hello"  # True
"hello" == "Hello"  # False (case sensitive)

# Not equal to
5 != 6        # True
5 != 5        # False
```

### Ordering Comparisons
```python
# Greater than
7 > 5         # True
5 > 7         # False

# Less than
3 < 8         # True
8 < 3         # False

# Greater than or equal
5 >= 5        # True
5 >= 3        # True
3 >= 5        # False

# Less than or equal
4 <= 4        # True
4 <= 6        # True
6 <= 4        # False
```

### String Comparisons
```python
# Lexicographic (dictionary) order
"apple" < "banana"    # True ('a' before 'b')
"Apple" < "apple"     # True (uppercase before lowercase)
"abc" < "abcd"        # True (shorter before longer)
```

## Membership Operators

### in Operator
```python
# Check if item exists in collection
5 in [1, 2, 3, 4, 5]        # True
"apple" in ["apple", "banana"]  # True
"a" in "banana"              # True
"z" in "banana"              # False

# Dictionary membership (keys)
"key" in {"key": "value"}    # True
"value" in {"key": "value"}  # False
```

### not in Operator
```python
# Opposite of in
6 not in [1, 2, 3, 4, 5]    # True
"x" not in "hello"          # True
```

## Identity Operators

### is Operator
```python
# Check if two variables reference the same object
a = [1, 2, 3]
b = a
c = [1, 2, 3]

a is b      # True (same object)
a is c      # False (different objects, same content)

# Important for None checking
value = None
value is None     # True (correct way)
value == None     # True (also works, but 'is' is preferred)
```

### is not Operator
```python
a is not c        # True
value is not None # True
```

## Combining Boolean Expressions

### Complex Conditions
```python
age = 25
is_student = True
has_discount = False

# Multiple AND conditions
eligible = age >= 18 and is_student and not has_discount

# Multiple OR conditions
can_enter = age >= 21 or (age >= 18 and not is_student)

# Mixed operators
special_offer = (age < 18 or age > 65) and is_student
```

### Operator Precedence
```python
# NOT > AND > OR
not True and False or True    # ((not True) and False) or True = False

# Use parentheses for clarity
(not True) and (False or True)  # False and True = False
```

## Boolean Algebra Laws

### Commutative Laws
```python
# AND is commutative
True and False == False and True    # True

# OR is commutative
True or False == False or True      # True
```

### Associative Laws
```python
# AND is associative
(True and False) and True == True and (False and True)  # Both False

# OR is associative
(True or False) or True == True or (False or True)      # Both True
```

### Distributive Laws
```python
# AND distributes over OR
A and (B or C) == (A and B) or (A and C)

# OR distributes over AND
A or (B and C) == (A or B) and (A or C)
```

### De Morgan's Laws
```python
# not (A and B) == (not A) or (not B)
not (True and False) == (not True) or (not False)  # True == True

# not (A or B) == (not A) and (not B)
not (True or False) == (not True) and (not False)  # False == False
```

## Practical Applications

### User Authentication
```python
def can_access_admin(username, is_admin, is_logged_in):
    return is_logged_in and is_admin and username != "guest"

# Test cases
can_access_admin("alice", True, True)    # True
can_access_admin("bob", False, True)     # False
can_access_admin("guest", True, True)    # False
```

### Shopping Cart Logic
```python
def calculate_shipping(cost, is_premium, free_shipping_threshold=50):
    if is_premium or cost >= free_shipping_threshold:
        return 0.0  # Free shipping
    elif cost >= 25:
        return 5.99
    else:
        return 9.99

# Test different scenarios
calculate_shipping(60, False, 50)   # 0.0 (over threshold)
calculate_shipping(30, True, 50)    # 0.0 (premium)
calculate_shipping(30, False, 50)   # 5.99
calculate_shipping(10, False, 50)   # 9.99
```

### Form Validation
```python
def validate_registration(name, email, age, agree_to_terms):
    name_valid = bool(name.strip())  # Not empty after stripping whitespace
    email_valid = "@" in email and "." in email  # Basic email check
    age_valid = isinstance(age, int) and 13 <= age <= 120
    agreement_valid = agree_to_terms is True

    all_valid = name_valid and email_valid and age_valid and agreement_valid

    if not all_valid:
        issues = []
        if not name_valid:
            issues.append("Name is required")
        if not email_valid:
            issues.append("Valid email required")
        if not age_valid:
            issues.append("Age must be between 13 and 120")
        if not agreement_valid:
            issues.append("Must agree to terms")
        return False, issues

    return True, []

# Test validation
valid, errors = validate_registration("Alice", "alice@email.com", 25, True)
print(f"Valid: {valid}")  # True

valid, errors = validate_registration("", "invalid", 10, False)
print(f"Valid: {valid}, Errors: {errors}")
# Valid: False, Errors: ['Name is required', 'Valid email required', 'Age must be between 13 and 120', 'Must agree to terms']
```

## Boolean Flags and State

### Status Flags
```python
class UserAccount:
    def __init__(self, username):
        self.username = username
        self.is_active = True
        self.is_verified = False
        self.is_premium = False

    def can_post(self):
        return self.is_active and self.is_verified

    def can_access_premium(self):
        return self.can_post() and self.is_premium

user = UserAccount("alice")
user.is_verified = True

print(user.can_post())          # True
print(user.can_access_premium()) # False

user.is_premium = True
print(user.can_access_premium()) # True
```

### Configuration Flags
```python
class ApplicationConfig:
    def __init__(self):
        self.debug_mode = False
        self.enable_logging = True
        self.use_cache = True
        self.send_emails = False

    def should_log(self, level):
        return self.enable_logging and (
            self.debug_mode or level in ["ERROR", "WARNING"]
        )

config = ApplicationConfig()
config.debug_mode = True

print(config.should_log("DEBUG"))     # True
print(config.should_log("INFO"))      # False
print(config.should_log("ERROR"))     # True
```

## Common Boolean Mistakes

### Confusing = with ==
```python
# Wrong
if x = 5:      # Assignment, not comparison
    print("Equal")

# Correct
if x == 5:
    print("Equal")
```

### Incorrect None Checking
```python
# Works but not preferred
if user == None:
    pass

# Better - use 'is'
if user is None:
    pass
```

### Overly Complex Conditions
```python
# Hard to understand
if not (not a or not b):
    pass

# Simpler
if a and b:
    pass
```

### Floating Point Comparisons
```python
# Problematic
if price == 19.99:
    print("Exact match")

# Better
if abs(price - 19.99) < 0.01:
    print("Approximately $19.99")
```

## Boolean Expression Optimization

### Short-Circuit Benefits
```python
# Avoid expensive operations
if user_exists and validate_complex_permissions(user):
    grant_access()

# Better than always calling validate_complex_permissions
```

### Boolean Expression Simplification
```python
# Original
if not (x < 5 or y > 10):
    do_something()

# Simplified using De Morgan's law
if x >= 5 and y <= 10:
    do_something()
```

## Key Takeaways

1. **Boolean logic is fundamental** to all programming decisions
2. **True/False values** come from comparisons and type conversions
3. **Logical operators** (AND, OR, NOT) combine conditions
4. **Short-circuit evaluation** can improve performance
5. **Boolean algebra laws** help simplify complex expressions
6. **Clear boolean logic** makes code more maintainable

## Further Reading
- Boolean algebra and digital logic
- Fuzzy logic and multi-valued logic
- Circuit design with logic gates
- Formal verification of boolean expressions