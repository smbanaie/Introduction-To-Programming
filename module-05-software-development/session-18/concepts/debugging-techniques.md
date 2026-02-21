# Debugging Techniques: Finding and Fixing Program Errors

## Introduction to Debugging

Debugging is the process of finding and fixing errors (bugs) in computer programs. Effective debugging involves systematic investigation, hypothesis testing, and careful analysis of program behavior.

## Understanding Program State

### Print Debugging
```python
def calculate_average(numbers):
    """Calculate average with debugging prints."""
    print(f"Input: {numbers}")
    print(f"Length: {len(numbers)}")

    if not numbers:
        print("Empty list, returning 0")
        return 0

    total = 0
    for i, num in enumerate(numbers):
        print(f"Adding number {i}: {num}")
        total += num
        print(f"Running total: {total}")

    average = total / len(numbers)
    print(f"Final average: {average}")
    return average

# Test with debugging
result = calculate_average([10, 20, 30])
print(f"Final result: {result}")
```

### Using Assertions
```python
def divide_and_round(a, b, decimals=2):
    """Divide a by b and round to specified decimals."""
    assert b != 0, "Cannot divide by zero"
    assert decimals >= 0, "Decimals must be non-negative"
    assert isinstance(a, (int, float)), "First argument must be a number"
    assert isinstance(b, (int, float)), "Second argument must be a number"

    result = a / b
    rounded = round(result, decimals)
    return rounded

# Assertions help catch errors early
try:
    result = divide_and_round(10, 3, 2)
    print(f"Result: {result}")  # 3.33
except AssertionError as e:
    print(f"Assertion failed: {e}")
```

### Logging for Debugging
```python
import logging

# Configure logging
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def process_data(data):
    """Process data with comprehensive logging."""
    logging.info(f"Starting data processing for {len(data)} items")

    try:
        # Validate input
        if not data:
            logging.warning("Empty data provided")
            return []

        # Process each item
        results = []
        for i, item in enumerate(data):
            logging.debug(f"Processing item {i}: {item}")

            processed = process_single_item(item)
            results.append(processed)

            if i % 10 == 0:  # Log progress for large datasets
                logging.info(f"Processed {i+1}/{len(data)} items")

        logging.info(f"Successfully processed {len(results)} items")
        return results

    except Exception as e:
        logging.error(f"Error processing data: {e}", exc_info=True)
        raise

def process_single_item(item):
    """Process single item (placeholder)."""
    return item.upper() if isinstance(item, str) else item
```

## Interactive Debugging

### Python Debugger (pdb)
```python
import pdb

def complex_calculation(x, y, z):
    """Complex calculation with debugging breakpoints."""
    # Set breakpoint
    pdb.set_trace()

    step1 = x + y
    step2 = step1 * z
    step3 = step2 / (x + y)

    return step3

# Run with debugging
result = complex_calculation(2, 3, 4)
print(result)

# At breakpoint, you can:
# n - next line
# s - step into function
# c - continue execution
# l - list code
# p variable - print variable value
# q - quit debugger
```

### Post-Mortem Debugging
```python
import pdb
import traceback

def risky_function():
    """Function that might fail."""
    data = [1, 2, 3]
    return data[10]  # IndexError

try:
    risky_function()
except Exception:
    # Start debugger at point of exception
    pdb.post_mortem()
```

### Conditional Breakpoints
```python
def find_duplicates(items):
    """Find duplicate items in list."""
    seen = set()
    duplicates = []

    for item in items:
        if item in seen:
            duplicates.append(item)
            # Conditional breakpoint
            if len(duplicates) >= 3:
                breakpoint()  # Python 3.7+ built-in debugger
        else:
            seen.add(item)

    return duplicates
```

## Systematic Debugging Process

### 1. Reproduce the Problem
```python
def test_function_with_bug():
    """Function with a subtle bug."""
    data = [1, 2, 3, 4, 5]

    # Bug: modifying list while iterating
    for item in data:
        if item % 2 == 0:
            data.remove(item)  # This causes items to be skipped!

    return data

# Reproduce the issue
print("Expected: [1, 3, 5]")
print(f"Actual: {test_function_with_bug()}")  # [1, 3, 5] - seems correct?
print("Wait, let's check with different data...")

# The bug becomes apparent with different data
print(f"With [1,2,3,4,5,6]: {test_function_with_bug()}")  # Skips some evens
```

### 2. Isolate the Problem
```python
def test_isolation():
    """Isolate the problematic code."""

    # Test individual components
    data = [1, 2, 3, 4, 5]
    print("Original data:", data)

    # Test the loop logic manually
    seen_items = []
    for i, item in enumerate(data):
        print(f"Iteration {i}: item={item}, data={data}")
        if item % 2 == 0:
            print(f"  Removing even number: {item}")
            data.remove(item)
            print(f"  Data after removal: {data}")
        seen_items.append(item)

    print("Items seen during iteration:", seen_items)
    print("Final data:", data)

test_isolation()
```

### 3. Identify Root Cause
```python
def correct_function(items):
    """Correct implementation that doesn't modify list during iteration."""

    # Method 1: Create new list
    odds = []
    for item in items:
        if item % 2 != 0:
            odds.append(item)
    return odds

    # Method 2: List comprehension
    # return [item for item in items if item % 2 != 0]

    # Method 3: Filter function
    # return list(filter(lambda x: x % 2 != 0, items))

def test_fix():
    """Test the corrected function."""
    test_cases = [
        [1, 2, 3, 4, 5],
        [2, 4, 6, 8, 10],
        [1, 3, 5, 7, 9],
        []
    ]

    for case in test_cases:
        result = correct_function(case)
        print(f"Input: {case} -> Output: {result}")

test_fix()
```

### 4. Implement and Test Fix
```python
def comprehensive_test():
    """Test the fix with edge cases."""
    test_cases = [
        ([], []),
        ([1], [1]),
        ([2], []),
        ([1, 2], [1]),
        ([1, 2, 3, 4, 5], [1, 3, 5]),
        ([2, 4, 6], []),
        (list(range(1, 11)), list(range(1, 11, 2))),  # 1,3,5,7,9
    ]

    for input_data, expected in test_cases:
        result = correct_function(input_data)
        status = "✓" if result == expected else "✗"
        print(f"{status} {input_data} -> {result} (expected {expected})")

        if result != expected:
            print(f"  ERROR: Expected {expected}, got {result}")

comprehensive_test()
```

## Common Debugging Tools

### IDE Debuggers
```python
# Most IDEs (PyCharm, VS Code, etc.) provide:
# - Step-by-step execution
# - Variable inspection
# - Call stack viewing
# - Breakpoint management
# - Watch expressions

def function_to_debug(a, b, c):
    """Function for IDE debugging demonstration."""
    x = a + b
    y = x * c
    z = y / (a + b)

    # Set breakpoint here in IDE
    return z  # Inspect variables at this point
```

### Profiling for Performance Issues
```python
import cProfile
import pstats

def slow_function():
    """Function with performance issues."""
    result = []
    for i in range(10000):
        result.append(i ** 2)  # Inefficient concatenation
    return result

# Profile the function
profiler = cProfile.Profile()
profiler.enable()
result = slow_function()
profiler.disable()

# Print statistics
stats = pstats.Stats(profiler)
stats.sort_stats('cumulative')
stats.print_stats(10)  # Top 10 functions
```

### Memory Debugging
```python
import tracemalloc

def memory_intensive_function():
    """Function that uses a lot of memory."""
    data = []
    for i in range(100000):
        data.append([i] * 1000)  # Creates large nested lists

    return len(data)

# Track memory usage
tracemalloc.start()

print(f"Memory before: {tracemalloc.get_traced_memory()[0] / 1024 / 1024:.2f} MB")

result = memory_intensive_function()

print(f"Memory after: {tracemalloc.get_traced_memory()[0] / 1024 / 1024:.2f} MB")

# Get top memory users
snapshot = tracemalloc.take_snapshot()
top_stats = snapshot.statistics('lineno')

print("Top memory users:")
for stat in top_stats[:5]:
    print(stat)
```

## Advanced Debugging Techniques

### Binary Search Debugging
```python
def binary_search_debug(code_lines):
    """Use binary search to isolate problematic code."""

    # Comment out half the code
    mid = len(code_lines) // 2

    print("Testing first half...")
    # Execute first half
    try:
        exec('\n'.join(code_lines[:mid]))
        print("First half works - bug in second half")
        # Debug second half
        binary_search_debug(code_lines[mid:])
    except Exception as e:
        print(f"First half fails: {e} - bug in first half")
        # Debug first half
        binary_search_debug(code_lines[:mid])

# Example usage (conceptual)
problematic_code = [
    "x = 1",
    "y = 2",
    "z = x / y",  # This will fail if y=0
    "print(z)"
]

# In practice, you'd modify the code to comment/uncomment sections
```

### Monkey Patching for Testing
```python
import random

def unreliable_function():
    """Function that sometimes fails."""
    if random.random() < 0.7:
        raise Exception("Random failure")
    return "Success"

def test_with_monkey_patch():
    """Test by controlling random behavior."""

    # Save original function
    original_random = random.random

    # Test success case
    random.random = lambda: 0.8  # Always return > 0.7
    try:
        result = unreliable_function()
        assert result == "Success"
        print("Success case: ✓")
    except Exception as e:
        print(f"Success case failed: {e}")

    # Test failure case
    random.random = lambda: 0.5  # Always return < 0.7
    try:
        result = unreliable_function()
        print(f"Failure case should have raised exception: {result}")
    except Exception:
        print("Failure case: ✓")

    # Restore original
    random.random = original_random

test_with_monkey_patch()
```

### Logging Decorators
```python
import functools
import time

def debug_log(func):
    """Decorator that logs function calls and results."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        func_name = func.__name__

        # Log function call
        arg_str = ', '.join([repr(arg) for arg in args] +
                          [f"{k}={v!r}" for k, v in kwargs.items()])
        print(f"Calling {func_name}({arg_str})")

        start_time = time.time()

        try:
            result = func(*args, **kwargs)
            end_time = time.time()

            print(f"{func_name} returned {result!r} in {end_time - start_time:.3f}s")
            return result

        except Exception as e:
            end_time = time.time()
            print(f"{func_name} raised {type(e).__name__}: {e} after {end_time - start_time:.3f}s")
            raise

    return wrapper

@debug_log
def calculate_fibonacci(n):
    """Calculate nth Fibonacci number."""
    if n <= 1:
        return n
    return calculate_fibonacci(n-1) + calculate_fibonacci(n-2)

# Test with debugging
result = calculate_fibonacci(5)
```

## Debugging Best Practices

### Rubber Duck Debugging
```python
def explain_to_rubber_duck():
    """
    Explain your code line by line to an inanimate object.
    This often reveals logical errors in your thinking.
    """
    print("Okay rubber duck, let me explain this code...")

    # Walk through the problematic code
    data = [1, 2, 3, 4, 5]
    print(f"We start with data: {data}")

    # Explain each step
    for i, item in enumerate(data):
        print(f"Looking at index {i}, item {item}")
        print(f"Is {item} even? {item % 2 == 0}")

        if item % 2 == 0:
            print(f"Yes, removing {item}")
            data.remove(item)
            print(f"Data is now: {data}")

    print("Final result:", data)
    print("Wait, this doesn't look right...")

explain_to_rubber_duck()
```

### Version Control for Debugging
```python
# Use git bisect to find when a bug was introduced
"""
git bisect start
git bisect bad     # Current version has the bug
git bisect good v1.0  # Version 1.0 was working
# Git will checkout a middle version
# Test if bug exists
git bisect bad     # or git bisect good
# Repeat until git finds the problematic commit
git bisect reset   # Return to original state
"""
```

### Creating Minimal Test Cases
```python
def create_minimal_reproduction():
    """Create the smallest possible code that reproduces the bug."""

    # Start with the full problematic code
    # Remove parts that aren't related to the bug
    # Simplify variable names and values
    # Keep removing until you have the minimal case

    # Example: Minimal reproduction of the list modification bug
    data = [1, 2]  # Minimal data that shows the problem

    print("Before:", data)
    for item in data:
        if item % 2 == 0:
            data.remove(item)  # This causes the bug
    print("After:", data)  # [1] - 2 was skipped!

    # Now you can clearly see and fix the issue
```

## Key Takeaways

1. **Systematic debugging** involves reproduction, isolation, identification, and fixing
2. **Print statements and logging** provide visibility into program execution
3. **Debuggers** allow step-by-step execution and state inspection
4. **Assertions** catch errors early in development
5. **Testing** with comprehensive test cases prevents regressions
6. **Rubber duck debugging** helps identify logical errors

## Further Reading
- Python debugger documentation
- Logging best practices
- Unit testing frameworks (pytest, unittest)
- Profiling and performance analysis tools
- Debugging techniques in different programming paradigms