# Nested Conditionals: Decisions Inside Decisions

## What You'll Learn
- How to put if statements inside other if statements
- When to use nested conditions vs. simple conditions
- How to avoid getting confused with many levels
- Common beginner mistakes

---

## What Are Nested Conditionals?

Nested conditionals are when you put an `if` statement **inside** another `if` statement. It's like having decisions within decisions.

### Real-Life Analogy: Going to a Movie

```
Decision 1: Do you want to see a movie?
    ↓ YES
Decision 2: Is the movie age-appropriate?
    ↓ YES
Decision 3: Do you have enough money?
    ↓ YES
Action: Buy ticket and enjoy!
```

### Simple Example

```python
age = 20
has_money = True

if age >= 18:
    print("You can enter the club.")
    if has_money:
        print("You can buy a drink!")
    else:
        print("Sorry, no money = no drink.")
else:
    print("You're too young to enter.")
```

**Output:**
```
You can enter the club.
You can buy a drink!
```

---

## ASCII Diagram: How Nesting Works

```
                    START
                      │
                      ▼
            ┌───────────────────┐
            │  age >= 18?       │
            │  (Check age)      │
            └─────────┬─────────┘
                      │
          ┌───────────┴───────────┐
       NO │                       │ YES
          ▼                       ▼
┌─────────────────┐    ┌───────────────────┐
│ "Too young"     │    │  has_money?       │
│ Skip club       │    │  (Check money)    │
└─────────────────┘    └─────────┬─────────┘
                                 │
                    ┌────────────┴────────────┐
                 NO │                         │ YES
                    ▼                         ▼
          ┌──────────────────┐    ┌──────────────────┐
          │ "No money =      │    │ "Enjoy your      │
          │  no drink"       │    │  drink!"         │
          └──────────────────┘    └──────────────────┘
```

---

## When to Use Nested Conditions

### Use Case 1: Checking Multiple Requirements Step by Step

```python
# Check if someone can rent a car
age = 25
has_license = True
has_credit_card = True

if age >= 21:  # First requirement
    print("✓ Age requirement met")
    
    if has_license:  # Second requirement (only if age passed)
        print("✓ License requirement met")
        
        if has_credit_card:  # Third requirement
            print("✓ Can rent a car!")
        else:
            print("✗ Need credit card")
    else:
        print("✗ Need driver's license")
else:
    print(f"✗ Must be 21+ (you need {21 - age} more years)")
```

### Use Case 2: Different Actions Based on Multiple Factors

```python
# Weather-based clothing advice
temperature = 75
is_raining = False
is_windy = True

if temperature > 70:
    if is_raining:
        print("☀️🌧️ Warm but raining - bring umbrella, wear light clothes")
    elif is_windy:
        print("☀️💨 Warm and windy - light jacket recommended")
    else:
        print("☀️ Perfect weather - enjoy!")
else:
    if is_raining:
        print("❄️🌧️ Cold and raining - wear warm waterproof jacket")
    else:
        print("❄️ Just cold - wear warm clothes")
```

---

## Avoiding Too Many Levels

### The Problem: Too Deep

```python
# ❌ Hard to read and understand (too many levels)
if user:
    if user.is_active:
        if user.age >= 18:
            if user.has_permission:
                print("Access granted!")
            else:
                print("No permission")
        else:
            print("Too young")
    else:
        print("Inactive user")
else:
    print("No user")
```

### Solution: Flatten with Early Returns

```python
# ✅ Better - easier to read
if not user:
    print("No user")
elif not user.is_active:
    print("Inactive user")
elif user.age < 18:
    print("Too young")
elif not user.has_permission:
    print("No permission")
else:
    print("Access granted!")
```

Or using functions:

```python
# ✅ Even better with guard clauses
def check_access(user):
    if not user:
        return "No user"
    if not user.is_active:
        return "Inactive user"
    if user.age < 18:
        return "Too young"
    if not user.has_permission:
        return "No permission"
    return "Access granted!"

result = check_access(user)
print(result)
```

---

## Comparing Nested vs. Flat Conditions

### Nested Version

```python
# Nested - more visual, but harder to follow
if age >= 18:
    if has_license:
        if not is_suspended:
            print("Can drive")
        else:
            print("License suspended")
    else:
        print("Need license")
else:
    print("Too young")
```

### Flat Version (Using and)

```python
# Flat - easier to read, same logic
if age >= 18 and has_license and not is_suspended:
    print("Can drive")
elif age < 18:
    print("Too young")
elif not has_license:
    print("Need license")
else:
    print("License suspended")
```

---

## Common Beginner Mistakes

### Mistake 1: Wrong Indentation

```python
# ❌ Wrong - second if not indented
if age >= 18:
if has_money:  # ERROR - needs to be indented!
    print("Can buy")

# ✅ Correct
if age >= 18:
    if has_money:
        print("Can buy")
```

### Mistake 2: Forgetting the else Matches the Closest if

```python
# ❌ Confusing - which if does the else match?
if age >= 18:
    if has_money:
        print("Can buy")
    else:  # This matches has_money check
        print("No money")
        
# What about when age < 18? Need another else!

# ✅ Clear with proper structure
if age >= 18:
    if has_money:
        print("Can buy")
    else:
        print("No money")
else:
    print("Too young")
```

### Mistake 3: Checking the Same Thing Twice

```python
# ❌ Redundant
if age >= 18:
    print("Adult")
    if age >= 21:  # We already know age >= 18!
        print("Can drink")

# ✅ Better
if age >= 21:
    print("Adult, can drink")
elif age >= 18:
    print("Adult, can't drink")
else:
    print("Minor")
```

### Mistake 4: Nested When Flat is Simpler

```python
# ❌ Nested when flat would be clearer
if temperature > 80:
    if is_humid:
        print("Hot and humid")
    else:
        print("Just hot")
else:
    if is_humid:
        print("Not hot but humid")
    else:
        print("Nice weather")

# ✅ Flat version
if temperature > 80 and is_humid:
    print("Hot and humid")
elif temperature > 80:
    print("Just hot")
elif is_humid:
    print("Not hot but humid")
else:
    print("Nice weather")
```

---

## Practical Example: Login System

```python
username = input("Username: ")
password = input("Password: ")

# Step-by-step validation
if username:  # Check if username is not empty
    if password:  # Check if password is not empty
        if username == "admin" and password == "secret":
            print("✅ Login successful!")
            
            # Nested check for admin features
            is_premium = True
            if is_premium:
                print("⭐ Premium features enabled")
            else:
                print("📋 Standard features only")
        else:
            print("❌ Wrong username or password")
    else:
        print("❌ Password required")
else:
    print("❌ Username required")
```

---

## Try It Yourself: Exercises

### Exercise 1: Club Entry with Multiple Checks

Create a club entry system that checks age, ID, and dress code.

```python
age = int(input("Age: "))
has_id = input("Have ID? (yes/no): ").lower() == "yes"
is_dressed_well = input("Dress code OK? (yes/no): ").lower() == "yes"

if age >= 21:
    print("✓ Age check passed")
    if has_id:
        print("✓ ID check passed")
        if is_dressed_well:
            print("🎉 Welcome to the club!")
        else:
            print("✗ Dress code violation")
    else:
        print("✗ ID required")
else:
    print(f"✗ Must be 21+ (need {21 - age} more years)")
```

### Exercise 2: Restaurant Recommendation

Recommend a restaurant based on budget and cuisine preference.

```python
budget = int(input("Your budget ($): "))
wants_fast_food = input("Want fast food? (yes/no): ").lower() == "yes"

if budget < 10:
    if wants_fast_food:
        print("🍔 Try the burger joint")
    else:
        print("🥪 Try the deli")
elif budget < 30:
    if wants_fast_food:
        print("🍕 Try the pizza place")
    else:
        print("🍝 Try the Italian restaurant")
else:
    print("🥂 Fancy dining - try the steakhouse!")
```

### Exercise 3: Fix the Structure

This code is too deeply nested. Flatten it:

```python
# Too nested - fix this!
if is_logged_in:
    if is_verified:
        if not is_banned:
            if has_credits:
                print("Can post")
            else:
                print("Need credits")
        else:
            print("Banned")
    else:
        print("Not verified")
else:
    print("Not logged in")
```

<details>
<summary>Click to see answer</summary>

```python
# Flattened version
if not is_logged_in:
    print("Not logged in")
elif not is_verified:
    print("Not verified")
elif is_banned:
    print("Banned")
elif not has_credits:
    print("Need credits")
else:
    print("Can post")
```
</details>

---

## Quick Reference

| Situation | Use |
|-----------|-----|
| Check requirements in order | Nested ifs |
| Different outcomes based on combinations | elif chain with `and`/`or` |
| Multiple independent conditions | Separate ifs |
| Too many levels (3+) | Flatten with early returns |

---

## Key Takeaways

1. **Nested conditions** are if statements inside other if statements
2. **Use nesting** when you need to check requirements step-by-step
3. **Avoid too many levels** (3+ is usually too many)
4. **Flatten with elif** when possible for cleaner code
5. **Indentation shows** which code belongs to which condition
6. **Early returns** (using functions) can make code clearer

---

## What's Next?

Now you know how to handle complex decisions! Next, we'll learn:
- How to repeat code with loops (for and while)
- How to handle multiple items with loops
- How to stop and skip iterations
