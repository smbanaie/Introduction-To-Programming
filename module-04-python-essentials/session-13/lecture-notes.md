# Session 13: Decision Making (if/elif/else)

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will use conditional statements to create decision-making programs
**Materials**: Whiteboard, flowchart templates, decision tree examples

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you get user input in Python?
- **Hook Scenario**: "Should I bring an umbrella?" decision process
- **Question**: "How can programs make choices like humans do?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Write if/elif/else conditional statements
- Create decision trees with multiple conditions
- Use comparison and logical operators in conditions
- Debug conditional logic

### Agenda Overview (5 minutes)
1. Introduction to conditional statements
2. if/elif/else syntax and structure
3. Complex conditions and nested decisions
4. Real-world decision-making examples

---

## II. Main Content (50 minutes)

### A. Basic Conditional Statements (15 minutes)

#### If Statement Structure
```python
if condition:
    # Code to execute if condition is True
    statement1
    statement2
```

#### Simple If Examples
```python
# Basic if statement
age = 18
if age >= 18:
    print("You are an adult!")

# With user input
temperature = float(input("Enter temperature: "))
if temperature > 30:
    print("It's hot outside!")

# String condition
name = input("Enter your name: ")
if name == "Alice":
    print("Hello, Alice!")
```

#### If-Else Statement
```python
if condition:
    # Code for True condition
    statements
else:
    # Code for False condition
    statements
```

#### If-Else Examples
```python
# Age check
age = int(input("Enter your age: "))
if age >= 18:
    print("You can vote!")
else:
    print("You cannot vote yet.")

# Even/odd check
number = int(input("Enter a number: "))
if number % 2 == 0:
    print("Even number")
else:
    print("Odd number")
```

### B. Multiple Conditions (elif) (15 minutes)

#### If-Elif-Else Structure
```python
if condition1:
    # Code for condition1 True
    statements
elif condition2:
    # Code for condition2 True (only if condition1 False)
    statements
elif condition3:
    # Code for condition3 True (only if previous conditions False)
    statements
else:
    # Code if all conditions False
    statements
```

#### Grade Calculator Example
```python
score = int(input("Enter your score (0-100): "))

if score >= 90:
    grade = "A"
    message = "Excellent work!"
elif score >= 80:
    grade = "B"
    message = "Good job!"
elif score >= 70:
    grade = "C"
    message = "Satisfactory"
elif score >= 60:
    grade = "D"
    message = "Needs improvement"
else:
    grade = "F"
    message = "Try harder next time"

print(f"Your grade is {grade}: {message}")
```

#### Temperature Advisor
```python
temp = float(input("Enter temperature in Celsius: "))

if temp >= 30:
    print("Wear light clothes and stay hydrated!")
elif temp >= 20:
    print("Perfect weather for outdoor activities!")
elif temp >= 10:
    print("Wear a light jacket.")
elif temp >= 0:
    print("Wear warm clothes and a coat.")
else:
    print("Very cold! Stay inside if possible.")
```

### C. Complex Conditions and Nesting (20 minutes)

#### Logical Operators in Conditions
```python
# AND operator (both conditions must be True)
age = 25
has_license = True
if age >= 18 and has_license:
    print("You can drive!")

# OR operator (at least one condition must be True)
is_weekend = True
is_holiday = False
if is_weekend or is_holiday:
    print("No school today!")

# NOT operator (reverses condition)
is_raining = False
if not is_raining:
    print("Go for a walk!")
```

#### Nested If Statements
```python
# Decision inside decision
age = int(input("Enter age: "))
has_ticket = input("Do you have a ticket? (y/n): ").lower() == "y"

if age >= 18:
    if has_ticket:
        print("Welcome to the concert!")
    else:
        print("You need a ticket to enter.")
else:
    print("This event is for adults only.")
```

#### Common Patterns
```python
# Range checking
number = int(input("Enter a number: "))
if number > 0:
    if number < 10:
        print("Single digit positive number")
    else:
        print("Multi-digit positive number")
else:
    print("Non-positive number")

# Multiple criteria
grade = int(input("Enter grade (0-100): "))
attendance = float(input("Enter attendance %: "))

if grade >= 70 and attendance >= 80:
    print("Passed!")
elif grade >= 60 and attendance >= 90:
    print("Passed on probation")
else:
    print("Failed")
```

#### Boolean Variables in Conditions
```python
# Using boolean flags
is_logged_in = True
is_admin = False
has_permission = True

if is_logged_in and (is_admin or has_permission):
    print("Access granted")
else:
    print("Access denied")
```

---

## III. Interactive Activities (15 minutes)

### Decision Tree Creation (10 minutes)
- **Groups**: Create decision trees for real scenarios
- **Examples**: Restaurant ordering, travel planning, shopping decisions
- **Implement**: Turn decision trees into Python if/elif/else code

### Bug Hunt Challenge (5 minutes)
- **Pairs**: Find and fix errors in conditional code
- **Examples**: Wrong indentation, missing colons, incorrect logic
- **Discuss**: Why each error matters

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **If statements control flow**: Execute code based on conditions
2. **Elif handles multiple choices**: Chain conditions for complex decisions
3. **Else covers remaining cases**: Default action when no conditions met
4. **Logical operators combine conditions**: AND, OR, NOT for complex logic

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Write an if statement to check if x > 10
2. What does elif stand for?
3. When does the else block execute?

### Preview of Next Session (2 minutes)
"Next time we'll learn loops - making programs repeat actions automatically!"

---

## Additional Resources
- **Visual Aid**: Decision tree flowchart
- **Handout**: Conditional statement patterns
- **Homework**: Create a grading program with if/elif/else

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes