# For Loops: Repeating Code for Each Item

## What You'll Learn
- How to repeat code for each item in a collection
- How to use for loops with lists, strings, and numbers
- How to count using range()
- Common beginner mistakes

---

## What is a For Loop?

A **for loop** lets you repeat code for each item in a group. Think of it like a robot going through a list of tasks:

```
Robot's list:
1. Wake up
2. Brush teeth
3. Eat breakfast

For each task in the list:
    Do the task ✓
```

---

## Basic For Loop Syntax

```python
for item in collection:
    # Do something with item
    print(item)
```

The loop goes through each item one by one and runs the indented code.

---

## Looping Over Lists

### Simple List Loop

```python
fruits = ["apple", "banana", "cherry", "date"]

for fruit in fruits:
    print(f"I like {fruit}")

print("Loop finished!")
```

**Output:**
```
I like apple
I like banana
I like cherry
I like date
Loop finished!
```

### How It Works (Step by Step)

```
fruits = ["apple", "banana", "cherry"]

Step 1: fruit = "apple"
        print("I like apple")
        
Step 2: fruit = "banana"
        print("I like banana")
        
Step 3: fruit = "cherry"
        print("I like cherry")
        
Done! Continue to next line
```

---

## ASCII Diagram: How For Loops Work

```
Collection: ["apple", "banana", "cherry"]

        Start
          │
          ▼
┌─────────────────┐
│ Get next item   │◄──────┐
│ (apple → banana │       │
│  → cherry)      │       │
└────────┬────────┘       │
         │                 │
    ┌────┴────┐            │
    │ More    │ No         │
    │ items?  ├──────────► Done
    └────┬────┘            │
      Yes│                  │
         ▼                  │
┌─────────────────┐         │
│ Do something    │         │
│ with the item   │         │
│ (print it)      │─────────┘
└─────────────────┘
```

---

## Looping Over Strings

Strings are just collections of characters!

```python
word = "Hello"

for letter in word:
    print(letter)
```

**Output:**
```
H
e
l
l
o
```

### Counting Vowels Example

```python
word = "banana"
vowel_count = 0

for letter in word:
    if letter in "aeiou":
        vowel_count += 1
        print(f"Found vowel: {letter}")

print(f"Total vowels: {vowel_count}")
```

**Output:**
```
Found vowel: a
Found vowel: a
Found vowel: a
Total vowels: 3
```

---

## Using range(): Counting Numbers

The `range()` function creates a sequence of numbers.

### Counting from 0 to N-1

```python
# Print numbers 0, 1, 2, 3, 4
for i in range(5):
    print(i)
```

**Output:**
```
0
1
2
3
4
```

**Important:** `range(5)` gives 0, 1, 2, 3, 4 (NOT 5!)

### Counting from Start to End

```python
# Print numbers 2, 3, 4, 5
for i in range(2, 6):
    print(i)
```

**Output:**
```
2
3
4
5
```

### Counting with Steps

```python
# Print even numbers: 0, 2, 4, 6, 8
for i in range(0, 10, 2):
    print(i)

# Print countdown: 5, 4, 3, 2, 1
for i in range(5, 0, -1):
    print(i)
```

### range() Quick Reference

| Code | Gives You | Use For |
|------|-----------|---------|
| `range(5)` | 0, 1, 2, 3, 4 | Repeat 5 times |
| `range(2, 6)` | 2, 3, 4, 5 | Numbers 2 to 5 |
| `range(0, 10, 2)` | 0, 2, 4, 6, 8 | Even numbers |
| `range(5, 0, -1)` | 5, 4, 3, 2, 1 | Countdown |

---

## Getting the Index with enumerate()

Sometimes you need to know the position (index) of each item.

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
```

**Output:**
```
0: apple
1: banana
2: cherry
```

### Starting from 1 Instead of 0

```python
fruits = ["apple", "banana", "cherry"]

for number, fruit in enumerate(fruits, start=1):
    print(f"{number}. {fruit}")
```

**Output:**
```
1. apple
2. banana
3. cherry
```

---

## Practical Examples

### Example 1: Shopping List Total

```python
prices = [10, 25, 5, 12, 8]
total = 0

for price in prices:
    total += price
    print(f"Added ${price}, total now: ${total}")

print(f"Final total: ${total}")
```

### Example 2: Finding the Maximum

```python
numbers = [45, 12, 78, 23, 67]
maximum = numbers[0]  # Start with first number

for num in numbers:
    if num > maximum:
        maximum = num
        print(f"New maximum found: {num}")

print(f"Maximum number: {maximum}")
```

### Example 3: Printing a Multiplication Table

```python
# Print 3 times table
print("3 times table:")
for i in range(1, 11):
    result = 3 * i
    print(f"3 × {i} = {result}")
```

**Output:**
```
3 times table:
3 × 1 = 3
3 × 2 = 6
3 × 3 = 9
...
3 × 10 = 30
```

---

## Common Beginner Mistakes

### Mistake 1: Modifying List While Looping

```python
# ❌ Wrong - don't modify while looping!
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:  # If even
        numbers.remove(num)  # DON'T DO THIS!

print(numbers)  # Unexpected result: [1, 3, 5] - 4 was skipped!

# ✅ Correct - create a new list
evens = []
for num in numbers:
    if num % 2 == 0:
        evens.append(num)
```

### Mistake 2: Forgetting Indentation

```python
# ❌ Wrong - no indentation
for i in range(3):
print(i)  # ERROR - must be indented!

# ✅ Correct
for i in range(3):
    print(i)
```

### Mistake 3: Variable Name Confusion

```python
# ❌ Confusing - using same name
for i in range(5):
    print(i)

for i in range(3):  # Reusing i - confusing!
    print(i)

# ✅ Better - descriptive names
for count in range(5):
    print(count)

for attempt in range(3):
    print(attempt)
```

### Mistake 4: Off-by-One Error with range()

```python
# ❌ Wrong - expects 1 to 5, but gets 1 to 4
for i in range(1, 5):
    print(i)
# Prints: 1, 2, 3, 4 (not 5!)

# ✅ Correct
for i in range(1, 6):  # 6 is exclusive, so we get 1-5
    print(i)
```

### Mistake 5: Forgetting to Initialize Variables

```python
# ❌ Wrong - total not initialized
for price in prices:
    total += price  # ERROR - total doesn't exist!

# ✅ Correct
total = 0  # Initialize first!
for price in prices:
    total += price
```

---

## When to Use For Loops

### Use for loops when:
- ✓ You have a list of items to process
- ✓ You know how many times to repeat
- ✓ You want to go through a collection
- ✓ You need to count from A to B

### Don't use for loops when:
- ✗ You don't know when to stop (use while)
- ✗ You're waiting for user input (use while)

---

## Try It Yourself: Exercises

### Exercise 1: Sum of Numbers

Calculate the sum of numbers 1 to 100.

```python
total = 0
for i in range(1, 101):
    total += i

print(f"Sum of 1 to 100: {total}")
# Answer should be 5050
```

### Exercise 2: Word Lengths

Print each word and its length.

```python
words = ["apple", "banana", "cherry", "date"]

for word in words:
    length = len(word)
    print(f"{word} has {length} letters")
```

### Exercise 3: Star Pattern

Print a triangle of stars.

```python
# Should print:
# *
# **
# ***
# ****
# *****

for i in range(1, 6):
    stars = "*" * i
    print(stars)
```

### Exercise 4: Fix the Code

Find and fix the bugs:

```python
# Buggy code
numbers = [10, 20, 30, 40, 50]

for num in numbers
    total = total + num
    print(f"Added {num}")

print(f"Total: {total}")
```

<details>
<summary>Click to see answer</summary>

```python
# Fixed code
numbers = [10, 20, 30, 40, 50]
total = 0  # Initialize total!

for num in numbers:  # Add colon
    total = total + num
    print(f"Added {num}")

print(f"Total: {total}")
```
</details>

---

## Quick Reference

| Task | Code Example |
|------|--------------|
| Loop through list | `for item in list:` |
| Loop through string | `for char in string:` |
| Count 0 to N-1 | `for i in range(N):` |
| Count A to B | `for i in range(A, B+1):` |
| Count with step | `for i in range(0, 10, 2):` |
| Get index and value | `for i, item in enumerate(list):` |

---

## Key Takeaways

1. **For loops** repeat code for each item in a collection
2. **`range(N)`** creates numbers 0, 1, 2, ..., N-1
3. **`enumerate()`** gives you both index and value
4. **Don't modify** the list you're looping through
5. **Initialize variables** (like `total = 0`) before the loop
6. **Indentation matters** - code inside loop must be indented

---

## What's Next?

Now you know how to repeat code! Next, we'll learn:
- While loops (when you don't know how many times)
- How to stop loops early
- How to skip iterations
