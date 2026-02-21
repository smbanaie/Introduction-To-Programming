# Session 10: Python Environment & First Steps

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will set up Python and write their first programs
**Materials**: Computers with Python installed, IDLE/text editor, Python cheat sheet

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What is pseudocode?
- **Hook Demonstration**: Live Python code execution
- **Question**: "Ready to turn algorithms into real programs?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Set up and use Python environment
- Write and run basic Python programs
- Understand Python syntax basics
- Debug simple Python errors

### Agenda Overview (5 minutes)
1. Python installation and setup
2. Interactive Python (REPL)
3. Writing and running programs
4. Basic syntax and errors

---

## II. Main Content (50 minutes)

### A. Python Environment Setup (15 minutes)

#### What is Python?
- **High-level language**: Human-readable syntax
- **Interpreted**: Code runs directly (no compilation needed)
- **Cross-platform**: Works on Windows, Mac, Linux
- **Beginner-friendly**: Simple syntax, clear error messages

#### Installation Options

| Method | Best For | Setup Time |
|--------|----------|------------|
| **Official Python** | Most control | 10 minutes |
| **Anaconda** | Data science, includes packages | 15 minutes |
| **Online IDEs** | Quick start, no installation | 2 minutes |

#### Development Environments
- **IDLE**: Built-in Python editor (simple, good for beginners)
- **VS Code**: Professional editor with extensions
- **PyCharm**: Full IDE for Python development
- **Jupyter**: Interactive notebooks for experimentation

#### First Steps Verification
```python
# Open terminal/command prompt and type:
python --version
# Should show Python 3.x.x

# Or in Python REPL:
>>> print("Hello, Python!")
Hello, Python!
```

### B. Interactive Python (REPL) (15 minutes)

#### What is REPL?
- **Read-Eval-Print Loop**: Interactive Python interpreter
- **Immediate feedback**: Type code, see results instantly
- **Experimentation**: Test ideas quickly
- **Learning tool**: Perfect for beginners

#### Basic REPL Commands
```python
# Start Python (type 'python' in terminal)
>>> 2 + 2          # Math operations
4

>>> "Hello" + " " + "World"  # String concatenation
'Hello World'

>>> print("Hi!")   # Function calls
Hi!

>>> name = "Alice" # Variable assignment
>>> name
'Alice'
```

#### REPL Best Practices
- **Test small pieces**: Break problems into testable parts
- **Use for learning**: Experiment with syntax
- **Check results**: Verify each step works
- **Exit with Ctrl+D** (Linux/Mac) or **Ctrl+Z** (Windows)

### C. Writing Python Programs (20 minutes)

#### Script Files vs Interactive
- **Scripts**: Saved .py files for complete programs
- **Interactive**: REPL for quick tests and learning
- **Combination**: Use both in development

#### First Python Program
```python
# hello.py
print("Hello, World!")
print("Welcome to Python programming!")
```

#### Running Python Scripts
```bash
# Method 1: Command line
python hello.py

# Method 2: Double-click (if associated)
# Method 3: IDE run button
```

#### Basic Syntax Rules
- **Statements**: One per line (usually)
- **Comments**: Start with # (ignored by Python)
- **Case sensitive**: Print ≠ print
- **Indentation**: Important for code structure

#### Common Beginner Errors
```python
# Error examples:
print("Hello)          # Missing quote
Print("Hello")         # Wrong case
print(Hello)           # Missing quotes for string
```

---

## III. Interactive Activities (15 minutes)

### Python REPL Exploration (10 minutes)
- **Individual**: Experiment with basic operations
- **Try**: Math, strings, variables, print statements
- **Challenge**: Create a simple calculator in REPL

### First Script Creation (5 minutes)
- **Pairs**: Write and run "Hello, World!" program
- **Modify**: Add personal greeting
- **Debug**: Fix any syntax errors together

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Python is accessible**: Easy installation and setup
2. **REPL for learning**: Interactive environment for experimentation
3. **Scripts for programs**: Save code in .py files
4. **Syntax matters**: Pay attention to quotes, case, and punctuation

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. How do you start Python REPL?
2. What's the difference between a script and REPL?
3. Write a Python statement to print your name

### Preview of Next Session (2 minutes)
"Next time we'll learn about variables and data types - how Python stores information!"

---

## Additional Resources
- **Visual Aid**: Python installation guide
- **Handout**: Common Python commands
- **Homework**: Install Python and write 3 different print statements

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes