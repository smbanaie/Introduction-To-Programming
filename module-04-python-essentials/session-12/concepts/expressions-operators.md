# Expressions and Operators: Making Calculations

## What You'll Learn
- How to do math in Python
- How to compare values
- How to combine multiple conditions
- Common beginner mistakes

---

## What Are Operators?

Operators are special symbols that tell Python to perform specific operations. Think of them like buttons on a calculator.

```
5 + 3    →  The + button adds
10 - 2   →  The - button subtracts
5 > 3    →  The > button compares
```

---

## Arithmetic Operators: Basic Math

### The Four Basic Operations

```python
# Addition (+)
result = 5 + 3       # 8
print(f"5 + 3 = {result}")

# Subtraction (-)
result = 10 - 4      # 6
print(f"10 - 4 = {result}")

# Multiplication (*)
result = 6 * 7       # 42
print(f"6 * 7 = {result}")

# Division (/)
result = 15 / 3      # 5.0
print(f"15 / 3 = {result}")
```

### More Math Operators

```python
# Integer Division (//) - drops the decimal
result = 17 // 5     # 3 (not 3.4!)
print(f"17 // 5 = {result}")

# Modulo (%) - gives the remainder
result = 17 % 5      # 2 (17 = 3*5 + 2)
print(f"17 % 5 = {result}")

# Exponentiation (**)
result = 2 ** 3      # 8 (2*2*2)
print(f"2 ** 3 = {result}")

# Square root
result = 16 ** 0.5   # 4.0
print(f"Square root of 16 = {result}")
```

### ASCII Diagram: Math Operations

```
Integer Division (//)          Modulo (%)
17 ÷ 5 = 3 R 2               17 ÷ 5 = 3 R 2
┌──────────┐                 ┌──────────┐
│  17 // 5 │                 │  17 % 5  │
│     ↓    │                 │     ↓    │
│    3     │                 │    2     │
│ (quotient)│                │ (remainder)│
└──────────┘                 └──────────┘
```

---

## Comparison Operators: Comparing Values

These operators compare two values and return `True` or `False`.

### Basic Comparisons

```python
age = 25

# Equal to (==)
print(age == 25)     # True
print(age == 30)     # False

# Not equal to (!=)
print(age != 30)     # True
print(age != 25)     # False

# Greater than (>)
print(age > 20)      # True
print(age > 30)      # False

# Less than (<)
print(age < 30)      # True
print(age < 20)      # False

# Greater than or equal (>=)
print(age >= 25)     # True
print(age >= 30)     # False

# Less than or equal (<=)
print(age <= 25)     # True
print(age <= 20)     # False
```

### Comparison Table

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `7 > 5` | `True` |
| `<` | Less than | `3 < 5` | `True` |
| `>=` | Greater or equal | `5 >= 5` | `True` |
| `<=` | Less or equal | `5 <= 7` | `True` |

---

## Logical Operators: Combining Conditions

Sometimes you need to check multiple things at once.

### AND (both must be True)

```python
age = 25
has_license = True

# Both conditions must be true
if age >= 18 and has_license:
    print("You can drive!")

# Visual:
# age >= 18    →  True
# has_license  →  True
#               AND
# Result       →  True ✓
```

**AND Truth Table:**
```
True  and True   → True ✓
True  and False  → False
False and True   → False
False and False  → False
```

### OR (at least one must be True)

```python
day = "Saturday"

# Either condition can be true
if day == "Saturday" or day == "Sunday":
    print("It's the weekend!")

# Visual:
# day == "Saturday"  →  True
# day == "Sunday"    →  False
#                     OR
# Result             →  True ✓
```

**OR Truth Table:**
```
True  or True   → True ✓
True  or False  → True ✓
False or True   → True ✓
False or False  → False
```

### NOT (reverses the value)

```python
is_raining = False

if not is_raining:
    print("You don't need an umbrella")

# Visual:
# is_raining  →  False
# not False   →  True ✓
```

---

## Operator Precedence: Order of Operations

Just like in math, Python follows an order when there are multiple operations.

### The Order (Highest to Lowest)

1. **Parentheses** `()`
2. **Exponentiation** `**`
3. **Multiplication/Division** `* / // %`
4. **Addition/Subtraction** `+ -`
5. **Comparisons** `== != > < >= <=`
6. **Logical NOT** `not`
7. **Logical AND** `and`
8. **Logical OR** `or`

### Examples

```python
# Without parentheses
result = 2 + 3 * 4      # 14 (not 20!)
# Because: 3 * 4 = 12, then 2 + 12 = 14

# With parentheses
result = (2 + 3) * 4    # 20
# Because: 2 + 3 = 5, then 5 * 4 = 20

# Complex example
result = 10 + 5 * 2 ** 2 - 8 / 4
# Step 1: 2 ** 2 = 4
# Step 2: 5 * 4 = 20
# Step 3: 8 / 4 = 2.0
# Step 4: 10 + 20 - 2.0 = 28.0
```

### Pro Tip: Use Parentheses!

```python
# Even if you know the order, use parentheses for clarity
# Good:
total = (price + tax) * quantity

# Not as clear:
total = price + tax * quantity  # Different result!
```

---

## Augmented Assignment: Shortcuts

When you want to update a variable with an operation.

```python
score = 10

# Instead of: score = score + 5
score += 5      # score is now 15

# Instead of: score = score - 3
score -= 3      # score is now 12

# Instead of: score = score * 2
score *= 2      # score is now 24

# Instead of: score = score / 4
score /= 4      # score is now 6.0
```

| Long Way | Shortcut | Meaning |
|----------|----------|---------|
| `x = x + 5` | `x += 5` | Add 5 to x |
| `x = x - 3` | `x -= 3` | Subtract 3 from x |
| `x = x * 2` | `x *= 2` | Multiply x by 2 |
| `x = x / 2` | `x /= 2` | Divide x by 2 |

---

## Common Beginner Mistakes

### Mistake 1: Using = Instead of ==

```python
# ❌ Wrong (= is for assignment)
if age = 18:
    print("You're 18")

# ✅ Correct (== is for comparison)
if age == 18:
    print("You're 18")
```

### Mistake 2: String vs Number Comparison

```python
# ❌ Wrong - comparing text to number
age = "25"  # This is text!
if age > 18:  # ERROR! Can't compare text to number
    print("Adult")

# ✅ Correct
age = 25  # This is a number
if age > 18:
    print("Adult")
```

### Mistake 3: Integer Division Confusion

```python
# ❌ Wrong - expecting decimal
result = 5 / 2      # Gives 2.5 (in Python 3)

# Integer division gives whole number
result = 5 // 2     # Gives 2
```

### Mistake 4: Floating Point Comparisons

```python
# ❌ Wrong - floating point is imprecise
price = 0.1 + 0.2
if price == 0.3:    # Might be False!
    print("Equal")

# ✅ Correct - use tolerance
if abs(price - 0.3) < 0.0001:
    print("Approximately equal")
```

### Mistake 5: Chaining Comparisons Incorrectly

```python
# ❌ Wrong - this doesn't work like math
if 5 < age < 10:   # This actually works in Python!
    pass

# But this is confusing:
if 5 < 10 > 3:     # True (5 < 10 is True, 10 > 3 is True)
    pass
```

---

## Try It Yourself: Exercises

### Exercise 1: Temperature Converter

Convert Celsius to Fahrenheit: `F = (C × 9/5) + 32`

```python
celsius = float(input("Enter temperature in Celsius: "))
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C = {fahrenheit}°F")
```

### Exercise 2: Shopping Calculator

Calculate total with tax and discount.

```python
price = float(input("Item price: $"))
quantity = int(input("Quantity: "))
tax_rate = 0.08  # 8% tax

subtotal = price * quantity
tax = subtotal * tax_rate
total = subtotal + tax

print(f"\nSubtotal: ${subtotal:.2f}")
print(f"Tax ({tax_rate*100}%): ${tax:.2f}")
print(f"Total: ${total:.2f}")
```

### Exercise 3: Check Voting Eligibility

Check if someone can vote (18+ and citizen).

```python
age = int(input("Enter your age: "))
is_citizen = input("Are you a citizen? (yes/no): ").lower() == "yes"

if age >= 18 and is_citizen:
    print("You are eligible to vote!")
else:
    if age < 18:
        print(f"You need to wait {18 - age} more years.")
    if not is_citizen:
        print("You must be a citizen to vote.")
```

### Exercise 4: Fix the Errors

Find and fix the errors in this code:

```python
# Buggy code
num1 = input("First number: ")
num2 = input("Second number: ")
sum = num1 + num2
average = sum / 2

if average > 50
    print("Above average")
else
    print("Below average")
```

<details>
<summary>Click to see the answer</summary>

```python
# Fixed code
num1 = float(input("First number: "))  # Convert to number
num2 = float(input("Second number: "))
sum_result = num1 + num2               # 'sum' is a built-in function!
average = sum_result / 2

if average > 50:                      # Missing colon
    print("Above average")
else:                                 # Missing colon
    print("Below average")
```
</details>

---

## Quick Reference

| Type | Operators | Example |
|------|-----------|---------|
| Math | `+ - * / // % **` | `5 + 3 = 8` |
| Compare | `== != > < >= <=` | `5 > 3 → True` |
| Logical | `and or not` | `True and False → False` |
| Assignment | `= += -= *= /=` | `x += 5` |

---

## Key Takeaways

1. **Math operators** work like a calculator: `+ - * / // % **`
2. **Comparison operators** give `True` or `False`: `== != > < >= <=`
3. **Logical operators** combine conditions: `and`, `or`, `not`
4. **Parentheses** control the order of operations
5. **`=` assigns**, **`==` compares** - don't confuse them!

---

## What's Next?

Now you know how to calculate! Next, we'll learn:
- How to control what code runs (conditions)
- How to repeat code (loops)
- How to organize code (functions)
