# Conditional Statements: Making Decisions in Code

## Introduction to Decision Making

Conditional statements allow programs to execute different code paths based on conditions. They make programs intelligent and responsive to different situations.

## The if Statement

### Basic if Statement
```python
# Simple condition
age = 18
if age >= 18:
    print("You can vote!")
    print("You are an adult.")

print("This always executes")  # Not indented
```

### if-else Statement
```python
temperature = 25

if temperature > 30:
    print("It's hot!")
    print("Stay hydrated.")
else:
    print("It's not too hot.")
    print("Enjoy the weather.")
```

### if-elif-else Chain
```python
score = 85

if score >= 90:
    grade = "A"
    message = "Excellent work!"
elif score >= 80:
    grade = "B"
    message = "Good job!"
elif score >= 70:
    grade = "C"
    message = "Fair performance."
elif score >= 60:
    grade = "D"
    message = "Needs improvement."
else:
    grade = "F"
    message = "Failed."

print(f"Grade: {grade} - {message}")
```

## Truthy and Falsy Values

### What Python Considers True/False
```python
# Truthy values
if 5:                    # Non-zero numbers
    print("5 is truthy")

if "hello":              # Non-empty strings
    print("Non-empty string is truthy")

if [1, 2, 3]:           # Non-empty collections
    print("Non-empty list is truthy")

if {"key": "value"}:     # Non-empty dict
    print("Non-empty dict is truthy")

# Falsy values
if not 0:               # Zero
    print("0 is falsy")

if not "":              # Empty string
    print("Empty string is falsy")

if not []:              # Empty list
    print("Empty list is falsy")

if not {}:              # Empty dict
    print("Empty dict is falsy")

if not None:            # None
    print("None is falsy")
```

### Practical Applications
```python
# Check if variable has a value
name = input("Enter your name: ")
if name:  # Empty string is falsy
    print(f"Hello, {name}!")
else:
    print("You didn't enter a name.")

# Check if list has items
shopping_list = []
if shopping_list:
    print("You have items to buy.")
else:
    print("Your shopping list is empty.")
```

## Comparison Operators in Conditions

### Numeric Comparisons
```python
x = 10
y = 20

if x < y:
    print("x is less than y")

if x != y:
    print("x is not equal to y")

if x <= 10:
    print("x is 10 or less")
```

### String Comparisons
```python
name = "Alice"

if name == "Alice":
    print("Hello, Alice!")

if name.lower() == "alice":  # Case-insensitive
    print("Hello, alice!")

if len(name) > 3:
    print("Long name")
```

### Membership Tests
```python
fruits = ["apple", "banana", "cherry"]

if "apple" in fruits:
    print("Apple is in the list")

if "grape" not in fruits:
    print("Grape is not in the list")

# String membership
message = "Hello, World!"
if "World" in message:
    print("Found 'World' in message")
```

## Logical Operators in Conditions

### AND Conditions
```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("You can drive!")
else:
    print("You cannot drive.")

# Multiple AND conditions
if age >= 18 and has_license and age <= 80:
    print("You are eligible to drive.")
```

### OR Conditions
```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It's weekend!")
else:
    print("It's a weekday.")

# Multiple OR conditions
if day in ["Saturday", "Sunday", "Friday"]:
    print("Almost weekend or weekend!")
```

### NOT Conditions
```python
is_raining = False

if not is_raining:
    print("No umbrella needed.")
else:
    print("Take an umbrella!")

# Complex NOT conditions
user = None
if not user:
    print("Please log in.")
```

### Combining Logical Operators
```python
age = 25
is_student = True
has_discount = False

# Complex condition
if (age < 18 or age > 65) and is_student:
    print("Student discount available")
elif has_discount or age > 60:
    print("Senior discount available")
else:
    print("Full price")
```

## Nested Conditional Statements

### Basic Nesting
```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("You can enter the club.")
    else:
        print("You need ID to enter.")
else:
    print("You are too young to enter.")
```

### Multiple Levels of Nesting
```python
temperature = 25
weather = "sunny"
is_weekend = True

if temperature > 20:
    if weather == "sunny":
        if is_weekend:
            print("Perfect day for outdoor activities!")
        else:
            print("Nice weather for a walk after work.")
    else:
        print("Warm but not sunny.")
else:
    print("It's cold outside.")
```

### Avoiding Deep Nesting
```python
# Hard to read - deep nesting
if user is not None:
    if user.is_active:
        if user.age >= 18:
            if user.has_permission:
                perform_action()
            else:
                print("No permission")
        else:
            print("Too young")
    else:
        print("Inactive user")
else:
    print("No user")

# Better - early returns or guard clauses
if user is None:
    print("No user")
    return

if not user.is_active:
    print("Inactive user")
    return

if user.age < 18:
    print("Too young")
    return

if not user.has_permission:
    print("No permission")
    return

perform_action()
```

## Conditional Expressions (Ternary Operator)

### Basic Ternary
```python
# Traditional if-else
age = 20
if age >= 18:
    status = "adult"
else:
    status = "minor"

# Ternary equivalent
status = "adult" if age >= 18 else "minor"
print(status)
```

### Nested Ternary
```python
score = 85
grade = "A" if score >= 90 else ("B" if score >= 80 else ("C" if score >= 70 else "F"))
print(f"Grade: {grade}")

# More readable version
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

### Practical Ternary Examples
```python
# Function return
def get_discount_rate(age):
    return 0.5 if age < 18 or age > 65 else 0.0

# List comprehension with condition
numbers = [1, 2, 3, 4, 5]
result = ["even" if x % 2 == 0 else "odd" for x in numbers]
# ["odd", "even", "odd", "even", "odd"]
```

## Real-World Examples

### User Authentication
```python
def authenticate_user(username, password):
    # Simulate user database
    users = {
        "alice": "password123",
        "bob": "secret456"
    }

    if username in users:
        if users[username] == password:
            return "Login successful!"
        else:
            return "Incorrect password."
    else:
        return "User not found."

result = authenticate_user("alice", "password123")
print(result)  # "Login successful!"
```

### Shopping Cart Discount
```python
def calculate_discount(total, customer_type, first_time):
    discount = 0

    if customer_type == "premium":
        discount = 0.2  # 20% for premium
    elif customer_type == "regular":
        if total >= 100:
            discount = 0.1  # 10% for regular with big purchase
        elif first_time:
            discount = 0.05  # 5% for first-time regular
    else:
        if first_time and total >= 50:
            discount = 0.05  # 5% for first-time guest

    return total * discount

total = 120
discount = calculate_discount(total, "regular", True)
final_price = total - discount
print(f"Final price: ${final_price:.2f}")
```

### File Processing Decision
```python
def process_file(filename):
    if not filename:
        return "No filename provided"

    if not filename.endswith(('.txt', '.csv', '.json')):
        return "Unsupported file type"

    # Simulate file processing
    if filename.endswith('.txt'):
        return "Processed text file"
    elif filename.endswith('.csv'):
        return "Processed CSV file"
    else:
        return "Processed JSON file"

result = process_file("data.txt")
print(result)
```

## Best Practices

### Clear Condition Structure
```python
# Good - clear intent
if user.is_authenticated and user.has_permission:

# Less clear
if user.is_authenticated == True and user.has_permission == True:
```

### Consistent Indentation
```python
# Always use 4 spaces (PEP 8)
if condition:
    do_something()
    if nested_condition:
        do_more()
```

### Avoid Complex Conditions
```python
# Complex - hard to understand
if (age >= 18 and has_license) or (age >= 16 and has_permit and accompanied_by_adult):

# Better - use variables
can_drive_solo = age >= 18 and has_license
can_drive_with_permit = age >= 16 and has_permit and accompanied_by_adult

if can_drive_solo or can_drive_with_permit:
```

### Use elif for Mutually Exclusive Conditions
```python
# Good - only one condition can be true
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"

# Avoid - all conditions checked even if first is true
if score >= 90:
    grade = "A"
if score >= 80:  # This will execute even if score >= 90
    grade = "B"
```

## Common Mistakes

### Assignment vs Comparison
```python
# Wrong - assignment instead of comparison
if age = 18:  # SyntaxError in Python
    print("Adult")

# Correct
if age == 18:
    print("Exactly 18 years old")
```

### Floating Point Comparisons
```python
# Problematic
if price == 19.99:
    print("Exact price match")

# Better - use epsilon for floating point
if abs(price - 19.99) < 0.01:
    print("Approximately $19.99")
```

### None Comparisons
```python
# Wrong
if user == None:
    print("No user")

# Correct - use 'is' for None
if user is None:
    print("No user")
```

## Key Takeaways

1. **Conditional statements control program flow** based on conditions
2. **if-elif-else chains** handle multiple mutually exclusive cases
3. **Truthy/falsy values** determine condition evaluation
4. **Logical operators** combine multiple conditions
5. **Nested conditions** create complex decision trees
6. **Clarity matters** - write readable conditional logic

## Further Reading
- Boolean logic and truth tables
- Design patterns for conditional logic
- Testing strategies for conditional code
- Refactoring complex conditionals