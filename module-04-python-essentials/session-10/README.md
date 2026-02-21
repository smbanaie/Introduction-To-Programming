# Session 10: Getting Started with Python – Environment and First Steps

## Session Overview

Welcome to your first hands-on programming session! After nine weeks of building conceptual foundations, today we finally start writing and running Python code. We'll set up a Python environment, explore the interactive REPL, create our first script, and connect what we've learned about algorithms and data representation to actual Python syntax. This marks the transition from thinking about programming to doing programming.

## Key Terms

- **Python interpreter**: Program that reads and executes Python code
- **REPL (Read-Eval-Print Loop)**: Interactive Python environment for immediate code execution
- **Script**: A file containing Python code saved with .py extension
- **Python shell/IDLE**: Built-in development environment that comes with Python
- **Command line/Terminal**: Text-based interface for running programs

## What Is the Python Interpreter?

The Python interpreter is a program that:
- Reads your Python source code
- Translates it into bytecode (intermediate form)
- Executes the bytecode using the Python Virtual Machine (PVM)
- Handles memory management, I/O, and other low-level details

It's what makes your human-readable code runnable on a computer.

## Setting Up Python

### Option 1: Install Python Locally
1. Visit python.org and download the latest version
2. Run the installer (check "Add Python to PATH")
3. Open command prompt/terminal and type `python --version`

### Option 2: Use Online Environments
- Replit.com (free online coding environment)
- PythonAnywhere.com
- Google Colab (for data science, but works for basics)

### Option 3: Use IDLE (Comes with Python)
- Search for "IDLE" in your Start menu
- Built-in editor and interpreter

## Using the Python REPL

The REPL is perfect for experimenting:

1. Open command prompt/terminal
2. Type `python` and press Enter
3. You'll see `>>>` prompt
4. Type expressions and see immediate results:

```python
>>> 2 + 3
5
>>> "Hello" + " World"
'Hello World'
>>> print("Welcome to Python!")
Welcome to Python!
```

To exit: `Ctrl+D` (Linux/Mac) or `Ctrl+Z` then Enter (Windows)

## Your First Python Script

Let's create a simple program:

1. **Create a file** called `hello.py`
2. **Add this code**:
```python
print("Hello, World!")
name = input("What's your name? ")
print("Nice to meet you, " + name + "!")
```

3. **Run it**:
   - Command line: `python hello.py`
   - IDLE: Open file and press F5
   - Online: Use the run button

## Connecting to Pseudocode

Remember our pseudocode from Session 9? Here's how it translates:

**Pseudocode:**
```
DISPLAY "Hello, World!"
GET name FROM user
DISPLAY "Nice to meet you, " + name + "!"
```

**Python:**
```python
print("Hello, World!")
name = input("What's your name? ")
print("Nice to meet you, " + name + "!")
```

The concepts are the same - the syntax is just Python's way of expressing them.

## Basic Python Syntax Elements

### Comments
```python
# This is a comment - ignored by Python
print("Hello")  # Comments can go after code too
```

### Statements
Each line is typically one statement:
```python
print("First")
print("Second")
```

### Expressions
Code that evaluates to a value:
```python
2 + 3          # Arithmetic expression
"Hello" + "!"  # String concatenation
len("Python")  # Function call expression
```

## Common Beginner Issues

### File Saving Issues
- Make sure file ends with `.py`
- Save in a location you can find
- Check file encoding (usually UTF-8)

### Path Issues
- Use `cd` to navigate to your script's directory
- Or use full paths: `python C:\Users\YourName\hello.py`

### Python Not Found
- Check if Python is installed: `python --version`
- Try `python3` instead of `python`
- Reinstall if needed

### Case Sensitivity
Python is case-sensitive:
- `Print("hello")` ❌ (capital P)
- `print("hello")` ✅

## Summary and Checklist

### What We Covered Today
- ✅ Setting up a Python environment
- ✅ Using the interactive REPL
- ✅ Creating and running Python scripts
- ✅ Basic syntax and common pitfalls
- ✅ Connecting pseudocode to Python code

### Self-Check Questions
- What's the difference between the REPL and a script?
- How do you run a Python file from the command line?
- What does the `print()` function do?
- Why might `python hello.py` not work?

### Key Takeaway
You've just taken your first step from thinking about programming to actually programming! Python's clean syntax makes it perfect for beginners, and the immediate feedback helps you learn quickly.

## Next Steps

Now that you can run Python code, we'll explore variables and data types. In our next session, you'll learn how to store and manipulate different kinds of information in Python programs.

## Connection to Future Sessions

This session launches you into practical programming:
- **Session 11**: Variables and data types (int, float, bool, str)
- **Session 12**: Input/output and expressions
- **Session 13-16**: Control structures and collections
- **Session 17-22**: Functions, error handling, files, and projects

## Further Reading (Optional)

- "Python Crash Course" by Eric Matthes (Chapters 1-2)
- Automate the Boring Stuff with Python (Chapters 0-1)
- Official Python tutorial: docs.python.org/3/tutorial/