# Loop Control: break, continue, and else

## What You'll Learn
- How to stop a loop early with `break`
- How to skip an iteration with `continue`
- How to use `else` with loops
- When to use `pass` as a placeholder
- Common beginner mistakes

---

## Controlling Loop Flow

Sometimes you need to change how a loop behaves:
- Stop a loop early when you find what you're looking for
- Skip over some items that don't match
- Run code when a loop finishes normally (not broken)

---

## break: Stop the Loop Immediately

`break` exits the loop right away, skipping any remaining iterations.

### Real-Life Analogy: Exit the Building

```
You're searching room by room for a key.
Found it in room 3! 🎉
No need to check rooms 4, 5, 6...
Exit the building immediately!
```

### Using break in a For Loop

```python
# Find the first even number and stop
numbers = [1, 3, 5, 8, 9, 10, 12]

for num in numbers:
    if num % 2 == 0:  # If even
        print(f"Found even number: {num}")
        break  # Stop immediately!

print("Done searching.")
```

**Output:**
```
Found even number: 8
Done searching.
```

Notice it didn't check 10 or 12 - it stopped at the first match!

### Using break in a While Loop

```python
# Keep guessing until correct
secret = 7

while True:  # Loop forever...
    guess = int(input("Guess the number (1-10): "))
    
    if guess == secret:
        print("Correct! 🎉")
        break  # Exit the loop
    
    print("Try again!")

print("Thanks for playing!")
```

---

## continue: Skip to the Next Iteration

`continue` skips the rest of the current iteration and moves to the next one.

### Real-Life Analogy: Skip a Step in Assembly Line

```
You're checking apples on a conveyor belt.
Good apple → Package it
Bad apple → Skip it (continue)
Move to next apple
```

### Using continue in a Loop

```python
# Print only even numbers, skip odd ones
for num in range(1, 11):
    if num % 2 != 0:  # If odd
        continue  # Skip this one
    
    print(f"Even number: {num}")

print("Done!")
```

**Output:**
```
Even number: 2
Even number: 4
Even number: 6
Even number: 8
Even number: 10
Done!
```

### Another Example: Skip Invalid Input

```python
# Process valid scores only
scores = [85, -5, 92, 0, 78, -3, 95]

for score in scores:
    if score < 0:
        print(f"Skipping invalid score: {score}")
        continue
    
    print(f"Valid score: {score}")

print("All scores processed.")
```

**Output:**
```
Valid score: 85
Skipping invalid score: -5
Valid score: 92
Valid score: 0
Valid score: 78
Skipping invalid score: -3
Valid score: 95
All scores processed.
```

---

## ASCII Diagram: How break and continue Work

```
Normal Loop Flow:
┌─────────────┐
│   Start     │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   Check     │
│  Condition  │
└──────┬──────┘
       │
   ┌───┴───┐
   │ True  │ False
   │       ├────────► Done
   ▼       │
┌─────────────┐
│ Loop Body   │
│   (work)    │
└──────┬──────┘
       │
       └──────────► Back to Check

With break:
Loop Body
   │
   ├───► if condition ──► break ────► Exit immediately!
   │         │
   │         │ False
   │         ▼
   └───► Continue work

With continue:
Loop Body
   │
   ├───► if condition ──► continue ──► Skip to next iteration
   │         │
   │         │ False
   │         ▼
   └───► Continue work
```

---

## else with Loops: Run When Loop Finishes Normally

The `else` block runs when the loop completes normally - meaning it didn't encounter a `break`.

### When else Runs vs When it Doesn't

```python
# Example 1: else runs because loop completed
for i in range(3):
    print(i)
else:
    print("Loop completed normally! ✅")

# Output:
# 0
# 1
# 2
# Loop completed normally! ✅
```

```python
# Example 2: else doesn't run because we broke
for i in range(3):
    print(i)
    if i == 1:
        break
else:
    print("Loop completed normally! ✅")

# Output:
# 0
# 1
# (else block never runs!)
```

### Real-Life Analogy: Treasure Hunt

```python
rooms = ["kitchen", "bedroom", "library"]
treasure_room = "library"

for room in rooms:
    print(f"Searching {room}...")
    if room == treasure_room:
        print(f"🏆 Found treasure in {room}!")
        break
else:
    # This only runs if we didn't find treasure!
    print("😢 No treasure found anywhere.")
```

**Output:**
```
Searching kitchen...
Searching bedroom...
Searching library...
🏆 Found treasure in library!
```

The `else` doesn't run because we found the treasure!

### Practical Use: Search with Not-Found Message

```python
# Search for a name in a list
names = ["Alice", "Bob", "Charlie"]
search_name = "David"

for name in names:
    if name == search_name:
        print(f"Found {name}!")
        break
else:
    print(f"{search_name} is not in the list.")

# Output: David is not in the list.
```

---

## pass: A Placeholder That Does Nothing

`pass` is a placeholder when you need to write code but don't want to do anything yet.

### When to Use pass

```python
# You're planning a function but haven't written it yet
def future_function():
    pass  # TODO: Implement this later

# In a loop where you might add code later
for item in items:
    if item.is_special():
        pass  # TODO: Handle special items
    else:
        print(item)
```

`pass` literally does nothing - it's just there so Python doesn't complain about empty blocks.

---

## Common Beginner Mistakes

### Mistake 1: Using break Instead of continue

```python
# ❌ Wrong - stops entirely instead of just skipping
for num in range(10):
    if num == 5:
        break  # Stops the whole loop!
    print(num)
# Only prints: 0, 1, 2, 3, 4

# ✅ Correct - skips just this number
for num in range(10):
    if num == 5:
        continue  # Just skips 5
    print(num)
# Prints: 0, 1, 2, 3, 4, 6, 7, 8, 9
```

### Mistake 2: Forgetting break in While True

```python
# ❌ Wrong - infinite loop!
while True:
    answer = input("Continue? (yes/no): ")
    if answer == "no":
        print("Goodbye!")
        # Forgot break! Loop runs forever!

# ✅ Correct - always break out
while True:
    answer = input("Continue? (yes/no): ")
    if answer == "no":
        print("Goodbye!")
        break  # Exit the loop
```

### Mistake 3: else Always Running After break

```python
# ❌ Wrong understanding
for i in range(5):
    if i == 3:
        break
else:
    print("Finished!")  # ❌ This won't print!

# ✅ The else only runs if loop completed without break
```

### Mistake 4: continue at the End of a Loop

```python
# ❌ Pointless - nothing comes after anyway
for i in range(5):
    print(i)
    continue  # Redundant - loop continues anyway!

# ✅ Only use continue to skip remaining code
for i in range(10):
    if i % 2 == 0:
        continue  # Skip even numbers
    print(i)  # Only prints odd numbers
```

### Mistake 5: Confusing break in Nested Loops

```python
# ⚠️ break only exits the innermost loop!
for i in range(3):
    for j in range(3):
        if j == 1:
            break  # Only exits inner loop!
        print(f"i={i}, j={j}")

# Output:
# i=0, j=0
# i=1, j=0
# i=2, j=0
```

---

## Practical Examples

### Example 1: Password with Maximum Attempts

```python
password = "secret123"
max_attempts = 3

for attempt in range(1, max_attempts + 1):
    guess = input(f"Attempt {attempt}/{max_attempts}: Enter password: ")
    
    if guess == password:
        print("✅ Access granted!")
        break
else:
    print("❌ Too many failed attempts. Account locked.")
```

### Example 2: Processing Data with Validation

```python
data = [10, 25, -5, 30, "invalid", 15, -3, 40]
valid_sum = 0
count = 0

for item in data:
    if not isinstance(item, int):  # Skip non-integers
        print(f"Skipping non-numeric: {item}")
        continue
    
    if item < 0:  # Skip negative numbers
        print(f"Skipping negative: {item}")
        continue
    
    valid_sum += item
    count += 1

print(f"Sum of {count} valid items: {valid_sum}")
```

### Example 3: Menu System with break

```python
while True:
    print("\n=== MENU ===")
    print("1. Add item")
    print("2. View items")
    print("3. Exit")
    
    choice = input("Choose (1-3): ")
    
    if choice == "1":
        print("Adding item...")
    elif choice == "2":
        print("Viewing items...")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Try again.")
```

---

## Try It Yourself: Exercises

### Exercise 1: Find First Divisible

Find the first number divisible by both 3 and 5 between 1 and 50.

```python
for num in range(1, 51):
    if num % 3 == 0 and num % 5 == 0:
        print(f"Found it: {num}")
        break
```

### Exercise 2: Sum with Skip

Sum all numbers from 1 to 10, but skip multiples of 3.

```python
total = 0
for num in range(1, 11):
    if num % 3 == 0:
        continue
    total += num

print(f"Sum (skipping multiples of 3): {total}")  # Should be 37
```

### Exercise 3: Search with else

Search for a number in a list. If not found, print a message.

```python
numbers = [10, 20, 30, 40, 50]
target = 25

# Write your code here
for num in numbers:
    if num == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found in the list.")
```

---

## Quick Reference

| Statement | What It Does | When to Use |
|-----------|--------------|-------------|
| `break` | Exits loop immediately | Found what you need, stop searching |
| `continue` | Skips to next iteration | Skip this item, continue with rest |
| `else` | Runs if loop finished normally (no break) | Do something if search failed |
| `pass` | Does nothing | Placeholder for future code |

---

## Key Takeaways

1. **`break`** - Stops the entire loop immediately
2. **`continue`** - Skips rest of current iteration, goes to next
3. **`else`** - Runs only if loop completed without breaking
4. **`pass`** - Does nothing, just a placeholder
5. Use `break` when you **found what you're looking for**
6. Use `continue` when you want to **skip certain items**
7. Use `else` to detect **when a search didn't find anything**

---

## What's Next?

Now you know how to control loops! Next, we'll learn about:
- List comprehensions (making lists with loops)
- Nested loops (loops inside loops)
- More complex loop patterns
