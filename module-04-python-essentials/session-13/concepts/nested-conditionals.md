# Nested Conditionals: Complex Decision Trees

## Introduction to Nested Conditions

Nested conditionals occur when one conditional statement is placed inside another. They create decision trees that handle complex logic by evaluating multiple conditions in sequence.

## Basic Nested Structures

### Simple Nesting
```python
age = 25
has_license = True

if age >= 18:
    print("You are an adult.")
    if has_license:
        print("You can drive.")
    else:
        print("You need a license to drive.")
else:
    print("You are a minor.")
```

### Multiple Levels
```python
temperature = 75
weather = "sunny"
is_weekend = True

if temperature > 70:
    print("It's warm outside.")
    if weather == "sunny":
        print("Perfect weather!")
        if is_weekend:
            print("Time for outdoor activities.")
        else:
            print("Enjoy after work.")
    else:
        print("Warm but not sunny.")
else:
    print("It's cool outside.")
```

## Common Patterns and Anti-Patterns

### The Arrow Anti-Pattern
```python
# Avoid - hard to read and maintain
if condition1:
    if condition2:
        if condition3:
            if condition4:
                do_something()
            else:
                handle_case_4()
        else:
            handle_case_3()
    else:
        handle_case_2()
else:
    handle_case_1()
```

### Guard Clauses (Early Returns)
```python
# Better - handle error cases first
def process_user(user):
    if user is None:
        return "No user provided"

    if not user.is_active:
        return "User is inactive"

    if not user.is_verified:
        return "User not verified"

    # Main logic here
    return f"Welcome, {user.name}!"

# Usage
result = process_user(user)
print(result)
```

### Return Early Pattern
```python
def validate_age(age):
    if age < 0:
        return False, "Age cannot be negative"

    if age > 150:
        return False, "Age seems unrealistic"

    if not isinstance(age, int):
        return False, "Age must be a whole number"

    return True, "Age is valid"

is_valid, message = validate_age(25)
print(f"Valid: {is_valid}, Message: {message}")
```

## Complex Decision Trees

### User Access Control
```python
def check_access(user, resource, action):
    # Level 1: Authentication
    if not user.is_authenticated:
        return False, "User not authenticated"

    # Level 2: Account status
    if not user.is_active:
        return False, "Account is inactive"

    # Level 3: Resource permissions
    if resource.owner_id == user.id:
        return True, "Access granted (owner)"

    # Level 4: Role-based permissions
    if user.role == "admin":
        return True, "Access granted (admin)"
    elif user.role == "moderator":
        if action in ["read", "edit"]:
            return True, "Access granted (moderator)"
        else:
            return False, "Moderators cannot delete"
    elif user.role == "user":
        if action == "read":
            return True, "Access granted (read-only)"
        else:
            return False, "Users have read-only access"

    return False, "Access denied"

# Test different scenarios
user_admin = type('User', (), {'is_authenticated': True, 'is_active': True, 'role': 'admin', 'id': 1})()
resource = type('Resource', (), {'owner_id': 2})()

granted, message = check_access(user_admin, resource, "delete")
print(message)  # "Access granted (admin)"
```

### E-commerce Pricing Logic
```python
def calculate_price(base_price, customer_type, quantity, promo_code=None):
    # Base price validation
    if base_price <= 0:
        raise ValueError("Price must be positive")

    final_price = base_price * quantity

    # Customer type discounts
    if customer_type == "premium":
        final_price *= 0.8  # 20% discount
    elif customer_type == "regular":
        if quantity >= 10:
            final_price *= 0.9  # 10% discount for bulk
    else:  # guest
        final_price *= 1.05  # 5% surcharge

    # Promo code handling
    if promo_code:
        if promo_code == "SAVE10":
            if customer_type in ["premium", "regular"]:
                final_price *= 0.9  # Additional 10% off
            else:
                final_price *= 0.95  # 5% off for guests
        elif promo_code == "FREESHIP":
            # Shipping discount handled elsewhere
            pass
        else:
            raise ValueError("Invalid promo code")

    return round(final_price, 2)

# Test pricing scenarios
price = calculate_price(10.0, "regular", 15, "SAVE10")
print(f"Final price: ${price}")  # $10 * 15 * 0.9 * 0.9 = $121.50
```

## Logical Operators vs Nested Conditions

### Using Logical Operators
```python
# Flat structure with logical operators
def can_drive(age, has_license, has_permit, accompanied):
    return (age >= 18 and has_license) or \
           (age >= 16 and has_permit and accompanied)

# Test cases
print(can_drive(20, True, False, False))   # True (adult with license)
print(can_drive(17, False, True, True))    # True (minor with permit and adult)
print(can_drive(15, False, True, False))   # False (too young, not accompanied)
```

### Equivalent Nested Structure
```python
def can_drive_nested(age, has_license, has_permit, accompanied):
    if age >= 18:
        if has_license:
            return True
        else:
            return False
    elif age >= 16:
        if has_permit and accompanied:
            return True
        else:
            return False
    else:
        return False

# Same results as logical version
print(can_drive_nested(20, True, False, False))   # True
print(can_drive_nested(17, False, True, True))    # True
print(can_drive_nested(15, False, True, False))   # False
```

### When to Use Which Approach
```python
# Use logical operators for:
# - Simple conditions
# - Performance-critical code (short-circuit evaluation)
# - Mathematical or business rules

# Use nested conditions for:
# - Complex validation with different error messages
# - Different actions for different failure reasons
# - Step-by-step decision processes
```

## Error Handling with Nested Conditions

### Validation Chains
```python
def validate_user_data(name, email, age):
    errors = []

    # Name validation
    if not name:
        errors.append("Name is required")
    elif len(name.strip()) < 2:
        errors.append("Name must be at least 2 characters")
    elif not name.replace(" ", "").isalpha():
        errors.append("Name can only contain letters and spaces")

    # Email validation
    if not email:
        errors.append("Email is required")
    elif "@" not in email:
        errors.append("Email must contain @ symbol")
    elif "." not in email.split("@")[1]:
        errors.append("Email must have a valid domain")

    # Age validation
    if age is None:
        errors.append("Age is required")
    elif not isinstance(age, int):
        errors.append("Age must be a number")
    elif age < 0:
        errors.append("Age cannot be negative")
    elif age > 150:
        errors.append("Age seems unrealistic")

    return len(errors) == 0, errors

# Test validation
valid, error_list = validate_user_data("Alice", "alice@email.com", 25)
print(f"Valid: {valid}")  # True

valid, error_list = validate_user_data("", "invalid", -5)
print(f"Valid: {valid}, Errors: {error_list}")
# Valid: False, Errors: ['Name is required', 'Email must have a valid domain', 'Age cannot be negative']
```

## State Machines with Nested Conditions

### Simple State Machine
```python
def process_order(order_status, payment_received, items_in_stock):
    if order_status == "pending":
        if payment_received:
            if items_in_stock:
                return "shipped", "Order shipped successfully"
            else:
                return "backordered", "Items temporarily out of stock"
        else:
            return "pending", "Waiting for payment"
    elif order_status == "shipped":
        return "shipped", "Order already shipped"
    elif order_status == "cancelled":
        return "cancelled", "Order was cancelled"
    else:
        return "unknown", "Unknown order status"

# Test different states
status, message = process_order("pending", True, True)
print(f"Status: {status}, Message: {message}")  # "shipped", "Order shipped successfully"

status, message = process_order("pending", True, False)
print(f"Status: {status}, Message: {message}")  # "backordered", "Items temporarily out of stock"
```

## Performance Considerations

### Short-Circuit Evaluation
```python
# Order conditions by likelihood/cost
def is_valid_user(user):
    # Check cheap conditions first
    return (user is not None and
            hasattr(user, 'id') and
            user.is_active and
            user.email_confirmed and
            complex_database_check(user.id))  # Expensive check last
```

### Avoiding Deep Nesting
```python
# Deep nesting - hard to read
def calculate_tax(income, state, filing_status):
    if state == "CA":
        if filing_status == "single":
            if income < 10000:
                return income * 0.05
            elif income < 50000:
                return income * 0.08
            else:
                return income * 0.10
        elif filing_status == "married":
            # More nested conditions...
    # More states...

# Flattened with early returns
def calculate_tax_better(income, state, filing_status):
    if state != "CA":
        return 0  # Simplified

    base_rate = 0.08 if filing_status == "married" else 0.10

    if income < 10000:
        rate = 0.05
    elif income < 50000:
        rate = base_rate
    else:
        rate = base_rate + 0.02

    return income * rate
```

## Testing Nested Conditions

### Test Case Coverage
```python
def test_calculate_tax():
    # Test all branches
    assert calculate_tax_better(5000, "CA", "single") == 250    # < 10000, single
    assert calculate_tax_better(30000, "CA", "single") == 2400  # 10000-50000, single
    assert calculate_tax_better(70000, "CA", "single") == 7200  # > 50000, single
    assert calculate_tax_better(30000, "CA", "married") == 1920 # 10000-50000, married
    assert calculate_tax_better(5000, "NY", "single") == 0      # Non-CA state

    print("All tests passed!")

test_calculate_tax()
```

### Boundary Testing
```python
def test_boundaries():
    # Test edge cases
    assert calculate_tax_better(9999, "CA", "single") == 499.95   # Just under 10000
    assert calculate_tax_better(10000, "CA", "single") == 800     # Exactly 10000
    assert calculate_tax_better(10001, "CA", "single") == 801     # Just over 10000

test_boundaries()
```

## Refactoring Nested Conditions

### Extract Method
```python
# Before: nested conditions in one method
def process_payment(amount, card_type, is_international):
    if amount > 0:
        if card_type in ["visa", "mastercard"]:
            if is_international:
                fee = amount * 0.03
            else:
                fee = amount * 0.02
            return amount + fee
        else:
            raise ValueError("Unsupported card type")
    else:
        raise ValueError("Amount must be positive")

# After: extracted helper methods
def calculate_fee(amount, card_type, is_international):
    if card_type not in ["visa", "mastercard"]:
        raise ValueError("Unsupported card type")

    rate = 0.03 if is_international else 0.02
    return amount * rate

def process_payment_refactored(amount, card_type, is_international):
    if amount <= 0:
        raise ValueError("Amount must be positive")

    fee = calculate_fee(amount, card_type, is_international)
    return amount + fee
```

### Use Dictionaries for Complex Logic
```python
# Replace nested conditions with lookup tables
def get_shipping_cost(region, weight, expedited):
    # Define shipping rates
    rates = {
        "domestic": {
            False: {  # standard
                "light": 5.99,
                "medium": 8.99,
                "heavy": 12.99
            },
            True: {   # expedited
                "light": 12.99,
                "medium": 18.99,
                "heavy": 24.99
            }
        },
        "international": {
            False: {  # standard
                "light": 15.99,
                "medium": 22.99,
                "heavy": 32.99
            },
            True: {   # expedited
                "light": 25.99,
                "medium": 35.99,
                "heavy": 49.99
            }
        }
    }

    # Determine weight category
    if weight <= 1:
        weight_cat = "light"
    elif weight <= 5:
        weight_cat = "medium"
    else:
        weight_cat = "heavy"

    return rates[region][expedited][weight_cat]

# Usage
cost = get_shipping_cost("international", 2.5, True)
print(f"Shipping cost: ${cost}")  # $35.99
```

## Key Takeaways

1. **Nested conditionals create complex decision trees** but can become hard to maintain
2. **Guard clauses and early returns** can simplify nested logic
3. **Logical operators** often provide cleaner alternatives to deep nesting
4. **Test coverage** is crucial for complex conditional logic
5. **Refactoring** can improve readability and maintainability
6. **Performance and clarity** should guide the choice between approaches

## Further Reading
- Design patterns for conditional logic
- State machines and automata theory
- Refactoring techniques for complex code
- Test-driven development for conditional logic