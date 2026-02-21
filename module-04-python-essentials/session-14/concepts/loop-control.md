# Loop Control: Managing Loop Execution

## Introduction to Loop Control

Loop control statements allow you to modify the normal flow of loop execution. They provide flexibility to skip iterations, exit early, or handle special conditions within loops.

## Break Statement

### Basic Break Usage
```python
# Exit loop immediately when condition met
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for num in numbers:
    if num == 7:
        print("Found 7! Stopping search.")
        break
    print(f"Checking: {num}")

# Output:
# Checking: 1
# Checking: 2
# Checking: 3
# Checking: 4
# Checking: 5
# Checking: 6
# Found 7! Stopping search.
```

### Break in While Loops
```python
# Game loop with exit condition
while True:
    command = input("Enter command (quit to exit): ").lower()
    if command == "quit":
        print("Goodbye!")
        break
    print(f"Executing: {command}")

print("Program ended")
```

### Break in Nested Loops
```python
# Find first occurrence in 2D list
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

target = 5
found = False

for i, row in enumerate(matrix):
    for j, value in enumerate(row):
        if value == target:
            print(f"Found {target} at position ({i}, {j})")
            found = True
            break  # Break inner loop
    if found:
        break  # Break outer loop

if not found:
    print(f"{target} not found")
```

## Continue Statement

### Basic Continue Usage
```python
# Skip even numbers
for num in range(1, 11):
    if num % 2 == 0:
        continue  # Skip rest of this iteration
    print(f"Odd number: {num}")

# Output:
# Odd number: 1
# Odd number: 3
# Odd number: 5
# Odd number: 7
# Odd number: 9
```

### Continue with Filtering
```python
# Process only valid data
data = ["apple", "", "banana", None, "cherry", ""]

for item in data:
    if not item:  # Skip empty or None values
        continue
    print(f"Processing: {item.upper()}")

# Output:
# Processing: APPLE
# Processing: BANANA
# Processing: CHERRY
```

### Continue in While Loops
```python
# Input validation loop
valid_numbers = []

while len(valid_numbers) < 5:
    try:
        num = float(input("Enter a number: "))
        if num < 0:
            print("Negative numbers not allowed, try again.")
            continue
        valid_numbers.append(num)
        print(f"Added {num}. Need {5 - len(valid_numbers)} more.")
    except ValueError:
        print("Please enter a valid number.")
        continue

print(f"Collected numbers: {valid_numbers}")
```

## Else Clause with Loops

### For Loop Else
```python
# Else executes if loop completes normally (no break)
def find_in_list(target, items):
    for item in items:
        if item == target:
            print(f"Found {target}!")
            break
    else:
        print(f"{target} not found in the list")

# Test cases
find_in_list(5, [1, 2, 3, 4, 5, 6])    # Found 5!
find_in_list(10, [1, 2, 3, 4, 5, 6])   # 10 not found in the list
```

### While Loop Else
```python
# Else executes if loop exits normally (not via break)
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    password = input("Enter password: ")
    if password == "secret":
        print("Access granted!")
        break
    attempts += 1
    print(f"Wrong password. {max_attempts - attempts} attempts remaining.")
else:
    print("Maximum attempts exceeded. Access denied.")

# If password is correct: "Access granted!"
# If max attempts reached: "Maximum attempts exceeded. Access denied."
```

## Pass Statement

### Placeholder in Loops
```python
# Pass as placeholder for future code
for num in range(10):
    if num % 2 == 0:
        pass  # TODO: Handle even numbers
    else:
        print(f"Odd: {num}")

# Pass in empty control blocks
numbers = []
if not numbers:
    pass  # Nothing to do for empty list
else:
    for num in numbers:
        print(num)
```

## Advanced Control Patterns

### Conditional Break with Flag
```python
# Using flag to control nested loop exit
found = False
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        if matrix[i][j] == 5:
            print(f"Found 5 at ({i}, {j})")
            found = True
            break
    if found:
        break

# Cleaner with function and return
def find_value(matrix, target):
    for i in range(len(matrix)):
        for j in range(len(matrix[i])):
            if matrix[i][j] == target:
                return i, j
    return None

result = find_value(matrix, 5)
if result:
    print(f"Found 5 at {result}")
```

### Loop with Retry Logic
```python
import time

def process_with_retry(data, max_retries=3):
    for attempt in range(max_retries):
        try:
            # Simulate processing that might fail
            if attempt < 2:  # Fail first two attempts
                raise Exception(f"Attempt {attempt + 1} failed")
            return f"Successfully processed: {data}"
        except Exception as e:
            print(f"Attempt {attempt + 1} failed: {e}")
            if attempt < max_retries - 1:
                print("Retrying in 1 second...")
                time.sleep(1)
            continue
    return "All attempts failed"

result = process_with_retry("important data")
print(result)
```

### Early Exit with Validation
```python
def validate_and_process(items):
    # Validate all items first
    for item in items:
        if not isinstance(item, (int, float)):
            print(f"Invalid item: {item} (not a number)")
            return False
        if item < 0:
            print(f"Invalid item: {item} (negative)")
            return False

    # Process valid items
    total = 0
    for item in items:
        total += item
        print(f"Processed: {item}")

    print(f"Total: {total}")
    return True

# Test cases
validate_and_process([1, 2, 3, 4])        # Valid
validate_and_process([1, "invalid", 3])    # Invalid type
validate_and_process([1, -2, 3])           # Negative value
```

## Loop Control in Different Contexts

### File Processing
```python
def process_file_until_error(filename):
    try:
        with open(filename, 'r') as file:
            for line_num, line in enumerate(file, 1):
                line = line.strip()
                if not line:  # Skip empty lines
                    continue
                if line.startswith('#'):  # Skip comments
                    continue
                if 'ERROR' in line:
                    print(f"Error found at line {line_num}: {line}")
                    break
                print(f"Processing line {line_num}: {line}")
    except FileNotFoundError:
        print(f"File {filename} not found")

process_file_until_error("data.txt")
```

### User Interface Loops
```python
def interactive_menu():
    items = []

    while True:
        print("\n=== Shopping List ===")
        print("1. Add item")
        print("2. Remove item")
        print("3. Show list")
        print("4. Clear list")
        print("5. Exit")

        choice = input("Choose option (1-5): ").strip()

        if choice == '1':
            item = input("Enter item to add: ").strip()
            if item:
                items.append(item)
                print(f"Added: {item}")
            else:
                print("Item cannot be empty")

        elif choice == '2':
            if not items:
                print("List is empty")
                continue
            print("Current items:")
            for i, item in enumerate(items, 1):
                print(f"{i}. {item}")
            try:
                index = int(input("Enter item number to remove: ")) - 1
                removed = items.pop(index)
                print(f"Removed: {removed}")
            except (ValueError, IndexError):
                print("Invalid item number")

        elif choice == '3':
            if not items:
                print("Shopping list is empty")
            else:
                print("Shopping list:")
                for i, item in enumerate(items, 1):
                    print(f"{i}. {item}")

        elif choice == '4':
            items.clear()
            print("List cleared")

        elif choice == '5':
            if items:
                print(f"Final shopping list has {len(items)} items")
            print("Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")

interactive_menu()
```

## Best Practices for Loop Control

### Clear Intent
```python
# Good - clear break condition
for item in items:
    if item.is_expired():
        break
    process_item(item)

# Less clear - multiple exit points
for item in items:
    if not item.is_valid():
        continue
    if item.is_special():
        break
    process_item(item)
```

### Avoid Deep Nesting
```python
# Avoid deeply nested loops with multiple breaks
# Use functions or early returns instead

def process_matrix(matrix):
    for i, row in enumerate(matrix):
        for j, value in enumerate(row):
            if value == target:
                return i, j
    return None
```

### Consistent Control Flow
```python
# Consistent pattern: validate, then process
for data in data_stream:
    if not is_valid(data):
        log_error(data)
        continue
    process_data(data)
```

## Common Loop Control Mistakes

### Multiple Breaks in Nested Loops
```python
# Problematic - unclear which loop exits
for i in range(10):
    for j in range(10):
        if some_condition(i, j):
            break  # Which loop breaks?
    # Code here might still execute

# Better - use flags or restructure
def find_coordinates():
    for i in range(10):
        for j in range(10):
            if some_condition(i, j):
                return i, j
    return None
```

### Forgetting to Update Loop Variables
```python
# Infinite loop
i = 0
while i < 10:
    if some_condition():
        continue  # i not incremented!
    i += 1

# Fix
i = 0
while i < 10:
    if some_condition():
        i += 1  # Update before continue
        continue
    i += 1
```

### Using Break in Comprehensions
```python
# Can't use break in list comprehensions
# Wrong
numbers = [x for x in range(100) if x > 50 break]  # SyntaxError

# Use traditional loop instead
numbers = []
for x in range(100):
    if x > 50:
        break
    numbers.append(x)
```

## Performance Considerations

### Break vs Complete Iteration
```python
# Break can improve performance for early exit
large_list = list(range(1000000))
target = 500

# Fast - stops at target
for num in large_list:
    if num == target:
        print("Found early")
        break

# Slow - always checks entire list
found = target in large_list  # Checks all elements
```

### Continue vs If-Else
```python
# Continue can be clearer for skipping
for item in items:
    if not item.is_valid():
        continue
    process_item(item)

# Equivalent but less clear
for item in items:
    if item.is_valid():
        process_item(item)
```

## Key Takeaways

1. **Break exits the loop immediately** - use for early termination
2. **Continue skips current iteration** - use for filtering or special cases
3. **Else clause executes if no break** - use for "not found" scenarios
4. **Pass is a placeholder** - use when no action is needed
5. **Clear control flow** prevents bugs and improves readability
6. **Functions can simplify** complex nested loop control

## Further Reading
- Control flow patterns in different programming paradigms
- Exception handling vs loop control for error management
- Refactoring techniques for complex loop logic
- Performance implications of different control strategies