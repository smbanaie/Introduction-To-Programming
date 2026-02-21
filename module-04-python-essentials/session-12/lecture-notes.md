# Session 12: Input/Output & Expressions

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will create interactive programs with input/output and expressions
**Materials**: Whiteboard, input/output examples, expression evaluation practice

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What are Python's main data types?
- **Hook Demonstration**: Interactive program asking for name and age
- **Question**: "How can programs talk to users and perform calculations?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Get user input in Python programs
- Display formatted output
- Write and evaluate expressions
- Create simple interactive programs

### Agenda Overview (5 minutes)
1. User input and output
2. Expressions and operators
3. String formatting
4. Interactive program creation

---

## II. Main Content (50 minutes)

### A. Input and Output (20 minutes)

#### Getting User Input
```python
# Basic input
name = input("What is your name? ")
print("Hello, " + name + "!")

# Input with prompt
age = input("Enter your age: ")
print("You are " + age + " years old.")

# Numeric input (needs conversion)
age = int(input("Enter your age: "))
next_year = age + 1
print("Next year you will be", next_year)
```

#### Input Type Conversion
```python
# String input (default)
name = input("Name: ")  # Always returns string

# Convert to other types
age = int(input("Age: "))      # Convert to integer
height = float(input("Height: "))  # Convert to float
is_student = input("Student? (y/n): ").lower() == "y"  # Convert to boolean
```

#### Output Formatting
```python
# Multiple ways to print
print("Hello")                    # Simple string
print("Hello", "World")           # Multiple arguments
print("Hello " + name)            # String concatenation
print(f"Hello {name}")            # f-string (Python 3.6+)
print("Hello {}".format(name))    # format() method
```

#### Advanced Output
```python
# f-strings (modern, recommended)
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")

# Format with precision
pi = 3.14159
print(f"Pi is approximately {pi:.2f}")  # 3.14

# Multiple variables
print(f"Name: {name}, Age: {age}, Height: {height}m")
```

### B. Expressions and Operators (15 minutes)

#### Mathematical Expressions
```python
# Arithmetic operators
result = 5 + 3      # Addition: 8
result = 10 - 4     # Subtraction: 6
result = 6 * 7      # Multiplication: 42
result = 15 / 4     # Division: 3.75
result = 15 // 4    # Floor division: 3
result = 15 % 4     # Modulo: 3
result = 2 ** 3     # Exponentiation: 8
```

#### Operator Precedence
```
1. ** (exponentiation)
2. * / // % (multiplication, division, etc.)
3. + - (addition, subtraction)
```

```python
# Examples
result = 2 + 3 * 4     # 14 (3*4=12, then 2+12)
result = (2 + 3) * 4   # 20 (parentheses first)
result = 2 ** 3 * 2    # 16 (2^3=8, then 8*2)
```

#### Comparison Operators
```python
# Comparison results are boolean
5 > 3      # True
10 < 5     # False
7 >= 7     # True
4 <= 3     # False
5 == 5     # True (equal to)
3 != 4     # True (not equal to)
```

#### Logical Operators
```python
# Boolean logic
True and True    # True
True and False   # False
True or False    # True
not True         # False

# Combined with comparisons
age = 25
is_adult = age >= 18 and age < 65  # True
is_teen = age >= 13 and age <= 19  # False
```

### C. Building Interactive Programs (15 minutes)

#### Simple Calculator
```python
# Get two numbers
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

# Perform calculations
sum_result = num1 + num2
diff_result = num1 - num2
prod_result = num1 * num2
quot_result = num1 / num2 if num2 != 0 else "undefined"

# Display results
print(f"Sum: {sum_result}")
print(f"Difference: {diff_result}")
print(f"Product: {prod_result}")
print(f"Quotient: {quot_result}")
```

#### Temperature Converter
```python
# Fahrenheit to Celsius
fahrenheit = float(input("Enter temperature in Fahrenheit: "))
celsius = (fahrenheit - 32) * 5/9
print(f"{fahrenheit}°F is {celsius:.1f}°C")

# Celsius to Fahrenheit
celsius = float(input("Enter temperature in Celsius: "))
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}°C is {fahrenheit:.1f}°F")
```

#### Input Validation
```python
# Basic validation
age = input("Enter your age: ")
if age.isdigit():
    age = int(age)
    print(f"You are {age} years old.")
else:
    print("Please enter a valid number.")
```

---

## III. Interactive Activities (15 minutes)

### Expression Evaluator (10 minutes)
- **Individual**: Predict results of expressions, then test in Python
- **Examples**: Complex math, comparisons, logical operations
- **Challenge**: Create expressions that evaluate to specific values

### Interactive Program Creation (5 minutes)
- **Pairs**: Create a simple interactive program
- **Ideas**: Greeting program, age calculator, unit converter
- **Test**: Run and debug together

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Input gets data**: Use input() to read from users
2. **Output displays results**: print() and f-strings for formatting
3. **Expressions calculate**: Operators combine values
4. **Interactive programs**: Combine input, processing, output

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. How do you get a number from user input?
2. Write an expression for 5 squared plus 3
3. What does the f in f-strings stand for?

### Preview of Next Session (2 minutes)
"Next time we'll learn decision making with if/elif/else statements!"

---

## Additional Resources
- **Visual Aid**: Operator precedence chart
- **Handout**: Input/output examples
- **Homework**: Create an interactive calculator program

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes