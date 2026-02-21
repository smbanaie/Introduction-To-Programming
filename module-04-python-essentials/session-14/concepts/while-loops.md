# While Loops: Conditional Iteration

## Introduction to While Loops

While loops execute a block of code repeatedly as long as a condition remains true. Unlike for loops that iterate over collections, while loops continue until a condition changes.

## Basic While Loop Syntax

### Simple While Loop
```python
# Basic counter
count = 1
while count <= 5:
    print(f"Count: {count}")
    count += 1

# Output:
# Count: 1
# Count: 2
# Count: 3
# Count: 4
# Count: 5
```

### While with Boolean Condition
```python
# Continue until user says stop
keep_going = True
while keep_going:
    response = input("Continue? (y/n): ").lower()
    if response == 'n':
        keep_going = False
    else:
        print("Continuing...")

print("Loop ended")
```

## Common While Loop Patterns

### Input Validation
```python
# Keep asking until valid input
def get_positive_number():
    while True:
        try:
            num = float(input("Enter a positive number: "))
            if num > 0:
                return num
            else:
                print("Number must be positive!")
        except ValueError:
            print("Please enter a valid number!")

number = get_positive_number()
print(f"You entered: {number}")
```

### Sentinel Values
```python
# Continue until special value entered
total = 0
print("Enter numbers to sum (enter 0 to finish):")

while True:
    num = float(input("Enter number: "))
    if num == 0:
        break  # Exit loop
    total += num

print(f"Total: {total}")
```

### Menu Systems
```python
def show_menu():
    print("\n=== Calculator Menu ===")
    print("1. Add")
    print("2. Subtract")
    print("3. Multiply")
    print("4. Divide")
    print("5. Exit")

def calculator():
    while True:
        show_menu()
        choice = input("Choose option (1-5): ")

        if choice == '5':
            print("Goodbye!")
            break

        if choice in ['1', '2', '3', '4']:
            try:
                a = float(input("First number: "))
                b = float(input("Second number: "))

                if choice == '1':
                    print(f"Result: {a + b}")
                elif choice == '2':
                    print(f"Result: {a - b}")
                elif choice == '3':
                    print(f"Result: {a * b}")
                elif choice == '4':
                    if b != 0:
                        print(f"Result: {a / b}")
                    else:
                        print("Cannot divide by zero!")
            except ValueError:
                print("Invalid number!")
        else:
            print("Invalid choice!")

calculator()
```

## Infinite Loops and How to Avoid Them

### Accidental Infinite Loops
```python
# Common mistake - condition never becomes false
counter = 1
while counter <= 5:
    print(counter)
    # Forgot to increment counter!

# This will loop forever!

# Fix
counter = 1
while counter <= 5:
    print(counter)
    counter += 1  # Don't forget this!
```

### Intentional Infinite Loops with Break
```python
# Game loop
while True:
    print("Game running...")
    command = input("Enter command (quit to exit): ")

    if command.lower() == 'quit':
        print("Thanks for playing!")
        break
    else:
        print(f"Executing: {command}")

print("Game ended")
```

### Controlled Infinite Loops
```python
# Server-like loop
import time

request_count = 0
while True:
    print(f"Processing request #{request_count + 1}")
    # Simulate work
    time.sleep(1)
    request_count += 1

    # Exit condition
    if request_count >= 10:
        print("Server shutting down after 10 requests")
        break
```

## While vs For Loops

### When to Use While
```python
# Unknown number of iterations
# Keep reading until end of file or special condition
lines = []
while True:
    line = input("Enter line (empty to finish): ")
    if not line:  # Empty string is falsy
        break
    lines.append(line)

print("You entered:")
for line in lines:
    print(line)
```

### When to Use For
```python
# Known number of iterations
# Iterating over collections
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(f"I like {fruit}")

# Equivalent while (less Pythonic)
i = 0
while i < len(fruits):
    print(f"I like {fruits[i]}")
    i += 1
```

### Converting Between Loop Types
```python
# For loop with manual index
items = ["a", "b", "c"]
for i in range(len(items)):
    print(f"Index {i}: {items[i]}")

# Equivalent while
i = 0
while i < len(items):
    print(f"Index {i}: {items[i]}")
    i += 1
```

## Loop Control Statements

### Break Statement
```python
# Exit loop immediately
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for num in numbers:
    if num == 7:
        print("Found 7, stopping search")
        break
    print(f"Checking: {num}")

# Output: Checking: 1, 2, 3, 4, 5, 6, Found 7, stopping search
```

### Continue Statement
```python
# Skip current iteration, continue with next
for num in range(1, 11):
    if num % 2 == 0:  # Skip even numbers
        continue
    print(f"Odd number: {num}")

# Output: Odd number: 1, 3, 5, 7, 9
```

### Else Clause with Loops
```python
# Else executes if loop completes normally (no break)
def find_number(target, numbers):
    for num in numbers:
        if num == target:
            print(f"Found {target}!")
            break
    else:
        print(f"{target} not found in list")

find_number(5, [1, 2, 3, 4, 5, 6])  # Found 5!
find_number(10, [1, 2, 3, 4, 5, 6]) # 10 not found in list
```

## Nested While Loops

### Multiplication Table
```python
# Nested while loops
i = 1
while i <= 3:
    j = 1
    while j <= 3:
        print(f"{i} * {j} = {i * j}")
        j += 1
    print()  # Empty line
    i += 1
```

### Input Validation with Multiple Fields
```python
def get_user_info():
    while True:
        name = input("Name: ").strip()
        if not name:
            print("Name cannot be empty")
            continue

        while True:
            try:
                age = int(input("Age: "))
                if age < 0:
                    print("Age cannot be negative")
                    continue
                elif age > 150:
                    print("Please enter a realistic age")
                    continue
                break  # Valid age entered
            except ValueError:
                print("Please enter a valid number for age")
                continue

        return name, age

name, age = get_user_info()
print(f"User: {name}, Age: {age}")
```

## Advanced While Loop Patterns

### Do-While Equivalent
```python
# Python doesn't have do-while, but we can simulate it
while True:
    # Always execute at least once
    response = input("Play again? (y/n): ").lower()
    if response != 'y':
        break
    # Game logic here
    print("Playing game...")
```

### Loop with Timeout
```python
import time

# Wait for user input with timeout
timeout = 10  # seconds
start_time = time.time()

while True:
    if time.time() - start_time > timeout:
        print("Timeout! No input received.")
        break

    user_input = input("Enter something (you have 10 seconds): ")
    if user_input:
        print(f"You entered: {user_input}")
        break
```

### Exponential Backoff
```python
import time
import random

def unreliable_operation():
    """Simulate an operation that might fail"""
    if random.random() < 0.7:  # 70% chance of failure
        raise Exception("Operation failed")
    return "Success!"

max_attempts = 5
attempt = 0
delay = 1

while attempt < max_attempts:
    try:
        result = unreliable_operation()
        print(f"Success after {attempt + 1} attempts: {result}")
        break
    except Exception as e:
        attempt += 1
        if attempt < max_attempts:
            print(f"Attempt {attempt} failed, retrying in {delay}s...")
            time.sleep(delay)
            delay *= 2  # Exponential backoff
        else:
            print(f"All {max_attempts} attempts failed: {e}")
```

## Common While Loop Mistakes

### Off-by-One Errors
```python
# Wrong - loop executes 11 times
count = 0
while count <= 10:  # 0 to 10 inclusive = 11 times
    print(count)
    count += 1

# Correct - 10 times
count = 1
while count <= 10:
    print(count)
    count += 1

# Or use range for known iterations
for count in range(1, 11):
    print(count)
```

### Infinite Loops from Floating Point
```python
# Dangerous - floating point precision
x = 0.0
while x != 1.0:  # May never be exactly 1.0 due to floating point errors
    print(x)
    x += 0.1

# Better - use integer counter or tolerance
x = 0.0
tolerance = 0.0001
while abs(x - 1.0) > tolerance:
    print(f"x = {x:.1f}")
    x += 0.1
```

### Modifying Loop Variables Incorrectly
```python
# Problematic
i = 0
while i < 10:
    print(i)
    if i == 5:
        i = 10  # Jump to end
    i += 1

# Better - use break
i = 0
while i < 10:
    print(i)
    if i == 5:
        break
    i += 1
```

## Performance Considerations

### While Loops vs For Loops
```python
# For large ranges, for loop is more efficient
import time

# While loop
start = time.time()
i = 0
while i < 1000000:
    i += 1
while_time = time.time() - start

# For loop
start = time.time()
for i in range(1000000):
    pass
for_time = time.time() - start

print(f"While: {while_time:.3f}s, For: {for_time:.3f}s")
```

### Memory Usage
```python
# While loops can accumulate memory if not careful
results = []
i = 0
while i < 1000000:
    results.append(i ** 2)  # List grows in memory
    i += 1

# Better - use generator or process in chunks
def generate_squares(n):
    i = 0
    while i < n:
        yield i ** 2
        i += 1

for square in generate_squares(1000000):
    # Process one at a time, low memory usage
    pass
```

## Key Takeaways

1. **While loops continue while condition is true** - perfect for unknown iterations
2. **Avoid infinite loops** by ensuring conditions eventually become false
3. **Use break and continue** for flow control within loops
4. **While loops excel at** input validation and event-driven scenarios
5. **Choose while over for** when iteration count is unknown
6. **Be careful with floating point** comparisons in loop conditions

## Further Reading
- Loop invariants and correctness proofs
- Event-driven programming patterns
- Asynchronous programming with loops
- Performance optimization techniques