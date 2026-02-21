# Session 18: Error Handling & Debugging

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will handle errors gracefully and debug programs systematically
**Materials**: Whiteboard, error message examples, debugging checklist

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What are function parameters used for?
- **Hook Scenario**: Show program crashing vs handling errors gracefully
- **Question**: "What happens when programs encounter problems, and how can we fix them?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Use try/except for error handling
- Debug programs systematically
- Understand common error types
- Write robust, user-friendly code

### Agenda Overview (5 minutes)
1. Understanding errors and exceptions
2. Try/except error handling
3. Debugging techniques
4. Best practices for robust code

---

## II. Main Content (50 minutes)

### A. Understanding Errors (15 minutes)

#### Types of Errors

##### Syntax Errors
```python
# Invalid Python syntax
if x > 5  # Missing colon
    print("Big number")

# Will show: SyntaxError: invalid syntax
```

##### Runtime Errors (Exceptions)
```python
# Code is syntactically correct but fails during execution
x = 5 / 0                    # ZeroDivisionError
name = "Alice"
print(name[10])              # IndexError
int("hello")                 # ValueError
open("nonexistent.txt")      # FileNotFoundError
```

##### Logic Errors
```python
# Code runs but produces wrong results
def calculate_average(numbers):
    total = 0
    for num in numbers:
        total += num
    return total / len(numbers)  # Works for non-empty lists

# But what if numbers is empty?
average = calculate_average([])  # ZeroDivisionError at runtime
```

#### Common Python Exceptions
- **ValueError**: Invalid value for operation
- **TypeError**: Wrong data type for operation
- **IndexError**: List/string index out of range
- **KeyError**: Dictionary key not found
- **ZeroDivisionError**: Division by zero
- **FileNotFoundError**: File doesn't exist
- **AttributeError**: Object doesn't have requested attribute

### B. Try/Except Error Handling (15 minutes)

#### Basic Try/Except
```python
try:
    # Code that might cause an error
    result = 10 / 0
    print("This won't print")
except ZeroDivisionError:
    # Code to run if error occurs
    print("Cannot divide by zero!")

print("Program continues...")
```

#### Handling Multiple Exceptions
```python
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Error: Division by zero"
    except TypeError:
        return "Error: Invalid data types"
    except Exception as e:  # Catch any other error
        return f"Unexpected error: {e}"

print(safe_divide(10, 2))    # 5.0
print(safe_divide(10, 0))    # "Error: Division by zero"
print(safe_divide("10", 2))  # "Error: Invalid data types"
```

#### Try/Except/Else/Finally
```python
def read_file(filename):
    try:
        file = open(filename, 'r')
        content = file.read()
    except FileNotFoundError:
        print(f"File '{filename}' not found")
        return None
    else:
        # Runs only if no exception occurred
        print("File read successfully")
        return content
    finally:
        # Always runs (even if exception occurred)
        try:
            file.close()
            print("File closed")
        except NameError:
            # file was never opened
            pass
```

#### Raising Exceptions
```python
def validate_age(age):
    if not isinstance(age, (int, float)):
        raise TypeError("Age must be a number")
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age seems too high")
    return age

# Usage
try:
    validate_age(-5)
except ValueError as e:
    print(f"Validation error: {e}")
```

### C. Debugging Techniques (20 minutes)

#### Systematic Debugging Process
1. **Reproduce the error**: Can you make it happen consistently?
2. **Identify the error**: Read the error message carefully
3. **Isolate the problem**: Find exactly where the error occurs
4. **Check assumptions**: Verify your understanding of the code
5. **Fix and test**: Make changes and verify the fix

#### Print Debugging
```python
def calculate_total(prices, tax_rate):
    print(f"Input prices: {prices}")  # Debug print
    print(f"Tax rate: {tax_rate}")    # Debug print

    subtotal = sum(prices)
    print(f"Subtotal: {subtotal}")    # Debug print

    tax = subtotal * tax_rate
    print(f"Tax amount: {tax}")      # Debug print

    total = subtotal + tax
    print(f"Final total: {total}")   # Debug print

    return total

# Test with debugging
result = calculate_total([10, 20, 30], 0.08)
```

#### Using Python Debugger (pdb)
```python
import pdb

def problematic_function(x, y):
    pdb.set_trace()  # Program pauses here for debugging
    result = x / y
    return result

# At breakpoint, you can:
# - Print variables: p x, p y
# - Execute code: result = x + y
# - Continue: c
# - Step to next line: n
# - Quit: q
```

#### Common Debugging Strategies
```python
# Check data types
age = input("Enter age: ")
print(f"Age type: {type(age)}, value: {repr(age)}")

# Check variable values at key points
def complex_calculation(data):
    print(f"Function called with: {data}")

    # Process data
    if not data:
        print("Warning: empty data received")
        return 0

    result = sum(data) / len(data)
    print(f"Calculation result: {result}")
    return result
```

#### Rubber Duck Debugging
- **Explain your code**: Describe what each line should do
- **Talk through logic**: "This line should calculate X, but..."
- **Find inconsistencies**: Where your explanation doesn't match the code

---

## III. Interactive Activities (15 minutes)

### Error Handling Workshop (10 minutes)
- **Individual**: Add error handling to existing code
- **Examples**: File operations, user input validation, calculations
- **Test**: Try to break the code with bad inputs

### Bug Hunt Challenge (5 minutes)
- **Pairs**: Find and fix bugs in provided code samples
- **Types**: Logic errors, runtime errors, edge cases
- **Strategy**: Use systematic debugging approach

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Errors are inevitable**: All programs encounter problems
2. **Handle gracefully**: Use try/except to manage errors
3. **Debug systematically**: Follow a process to find and fix issues
4. **Prevention is best**: Write robust code that anticipates problems

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. What does try/except do?
2. Name two common Python exceptions
3. What's the first step in debugging?

### Preview of Next Session (2 minutes)
"Next time we'll learn file input/output - reading and writing data to disk!"

---

## Additional Resources
- **Visual Aid**: Error handling flow diagram
- **Handout**: Common errors and solutions
- **Homework**: Add error handling to calculator program

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes