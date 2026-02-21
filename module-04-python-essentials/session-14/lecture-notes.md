# Session 14: Loops (while/for)

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will use loops to create repetitive program behavior
**Materials**: Whiteboard, loop flowchart examples, iteration counters

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What does elif do in conditional statements?
- **Hook Demonstration**: Count to 10 manually vs with a loop
- **Question**: "How can programs repeat actions without writing the same code over and over?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Write for loops for definite iteration
- Write while loops for conditional iteration
- Control loop execution with break and continue
- Avoid common loop pitfalls (infinite loops)

### Agenda Overview (5 minutes)
1. Introduction to loops and iteration
2. For loops with ranges and sequences
3. While loops with conditions
4. Loop control and common patterns

---

## II. Main Content (50 minutes)

### A. For Loops (20 minutes)

#### For Loop Basics
```python
# Basic for loop structure
for variable in sequence:
    # Code to repeat
    statement
```

#### Range-Based Loops
```python
# Count from 0 to 4
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4

# Count from 1 to 5
for i in range(1, 6):
    print(i)  # 1, 2, 3, 4, 5

# Count by 2s
for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8
```

#### Iterating Over Sequences
```python
# String iteration
name = "Python"
for letter in name:
    print(letter)  # P, y, t, h, o, n

# List iteration (we'll learn lists later)
colors = ["red", "green", "blue"]
for color in colors:
    print(color)
```

#### Accumulation Pattern
```python
# Sum numbers 1 to 10
total = 0
for i in range(1, 11):
    total = total + i
print(f"Sum: {total}")  # 55

# Count vowels in text
text = "Hello World"
vowel_count = 0
for char in text.lower():
    if char in "aeiou":
        vowel_count += 1
print(f"Vowels: {vowel_count}")  # 3
```

### B. While Loops (15 minutes)

#### While Loop Basics
```python
# While loop structure
while condition:
    # Code to repeat while condition is True
    statement
    # Don't forget to update condition!
```

#### While Loop Examples
```python
# Count to 5
count = 1
while count <= 5:
    print(count)
    count = count + 1  # Important: update condition variable

# Password prompt
password = ""
while password != "secret":
    password = input("Enter password: ")
print("Access granted!")
```

#### Sentinel-Controlled Loops
```python
# Keep asking until valid input
score = -1
while score < 0 or score > 100:
    score = int(input("Enter score (0-100): "))
print(f"Valid score: {score}")

# Sum until user enters 0
total = 0
number = int(input("Enter number (0 to stop): "))
while number != 0:
    total += number
    number = int(input("Enter number (0 to stop): "))
print(f"Total: {total}")
```

### C. Loop Control and Patterns (15 minutes)

#### Break and Continue
```python
# Break: exit loop immediately
for i in range(10):
    if i == 5:
        break  # Stop when i equals 5
    print(i)  # Prints 0, 1, 2, 3, 4

# Continue: skip to next iteration
for i in range(5):
    if i == 2:
        continue  # Skip when i equals 2
    print(i)  # Prints 0, 1, 3, 4
```

#### Common Loop Patterns
```python
# Finding maximum
numbers = [3, 7, 2, 9, 5]
maximum = numbers[0]
for num in numbers:
    if num > maximum:
        maximum = num
print(f"Maximum: {maximum}")  # 9

# Input validation with retry limit
attempts = 0
while attempts < 3:
    password = input("Enter password: ")
    if password == "secret":
        print("Access granted!")
        break
    attempts += 1
    print(f"Wrong password. {3-attempts} attempts left.")
else:
    print("Too many failed attempts!")
```

#### Avoiding Infinite Loops
```python
# Infinite loop (DANGER!)
# while True:
#     print("This never stops!")

# Safe version with exit condition
response = ""
while response != "quit":
    response = input("Type 'quit' to exit: ")
    print(f"You typed: {response}")
```

#### Nested Loops
```python
# Multiplication table
for i in range(1, 4):      # Outer loop
    for j in range(1, 4):  # Inner loop
        print(f"{i} × {j} = {i*j}")
    print("---")  # Separator after each row
```

---

## III. Interactive Activities (15 minutes)

### Loop Pattern Practice (10 minutes)
- **Individual**: Implement common loop patterns
- **Examples**: Sum a range, count characters, validate input
- **Challenge**: Combine patterns in creative ways

### Loop Debugging Workshop (5 minutes)
- **Pairs**: Identify and fix loop problems
- **Common issues**: Off-by-one errors, infinite loops, missing updates
- **Strategy**: Add print statements to trace execution

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **For loops**: Iterate over known sequences or ranges
2. **While loops**: Continue until condition becomes false
3. **Loop control**: Break and continue modify loop behavior
4. **Careful design**: Avoid infinite loops, update conditions properly

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Write a for loop to print numbers 1-3
2. What's wrong with: while True: print("loop")
3. When would you use break in a loop?

### Preview of Next Session (2 minutes)
"Next time we'll work with strings - Python's text manipulation power!"

---

## Additional Resources
- **Visual Aid**: Loop flowchart patterns
- **Handout**: Common loop pitfalls
- **Homework**: Create a number guessing game with loops

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes