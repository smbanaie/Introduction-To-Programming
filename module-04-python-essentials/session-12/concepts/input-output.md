# Input and Output: Communicating with Python Programs

## Program Communication

Programs need to interact with users, files, and other systems. Input and output operations enable this communication, allowing programs to receive data and send results.

## Console Input

### Basic Input with input()
```python
# Get user input as string
name = input("Enter your name: ")
print(f"Hello, {name}!")

# Input with prompt
age = input("How old are you? ")
print(f"You are {age} years old.")
```

### Type Conversion for Input
```python
# Convert input to numbers
age = int(input("Enter your age: "))
height = float(input("Enter your height in meters: "))
weight = float(input("Enter your weight in kg: "))

# Calculate BMI
bmi = weight / (height ** 2)
print(f"Your BMI is: {bmi:.1f}")
```

### Handling Input Errors
```python
# Safe numeric input
def get_number(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Please enter a valid number.")

age = get_number("Enter your age: ")
print(f"You entered: {age}")
```

### Multiple Inputs
```python
# Get multiple values in one input
coordinates = input("Enter x,y coordinates: ")
x_str, y_str = coordinates.split(',')
x = float(x_str.strip())
y = float(y_str.strip())
print(f"Point: ({x}, {y})")
```

## Console Output

### Basic Output with print()
```python
# Simple text output
print("Hello, World!")

# Multiple arguments
name = "Alice"
age = 25
print("Name:", name, "Age:", age)

# Suppress newline
print("Hello", end="")
print(" World!")  # Output: "Hello World!"
```

### Formatted Output
```python
# f-strings (Python 3.6+)
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")

# format() method
print("My name is {} and I am {} years old.".format(name, age))

# Named placeholders
print("Hello {name}, you are {age}.".format(name="Bob", age=30))

# % formatting (older style)
print("My name is %s and I am %d years old." % (name, age))
```

### Advanced Formatting
```python
# Number formatting
pi = 3.14159265359
print(f"Pi to 2 decimal places: {pi:.2f}")
print(f"Pi in scientific notation: {pi:.2e}")

# Field width and alignment
names = ["Alice", "Bob", "Catherine"]
for name in names:
    print(f"{name:<10} | {len(name):>2} chars")
# Output:
# Alice      |  5 chars
# Bob        |  3 chars
# Catherine  | 10 chars
```

## File Input/Output

### Reading Files
```python
# Open and read entire file
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# Read line by line
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # Remove newline characters

# Read specific number of characters
with open("data.txt", "r") as file:
    chunk = file.read(100)  # Read first 100 characters
    print(chunk)
```

### Writing Files
```python
# Write to file (overwrites existing content)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a test file.\n")

# Append to file
with open("log.txt", "a") as file:
    file.write("Program started\n")

# Write multiple lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("lines.txt", "w") as file:
    for line in lines:
        file.write(line + "\n")
```

### File Modes
```python
# Read modes
"r"   # Read (default)
"rb"  # Read binary

# Write modes
"w"   # Write (overwrites)
"wb"  # Write binary
"a"   # Append
"ab"  # Append binary

# Universal modes
"r+"  # Read and write
"w+"  # Read and write (overwrites)
"a+"  # Read and append
```

### Handling File Errors
```python
def safe_read_file(filename):
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"File '{filename}' not found.")
        return None
    except PermissionError:
        print(f"No permission to read '{filename}'.")
        return None
    except Exception as e:
        print(f"Error reading file: {e}")
        return None

content = safe_read_file("myfile.txt")
if content:
    print(content)
```

## Working with File Paths

### Path Handling
```python
import os

# Current working directory
current_dir = os.getcwd()
print(f"Current directory: {current_dir}")

# Change directory
os.chdir("/path/to/directory")

# Join paths (cross-platform)
filepath = os.path.join("folder", "subfolder", "file.txt")
# Windows: folder\subfolder\file.txt
# Unix: folder/subfolder/file.txt

# Check if file exists
if os.path.exists("file.txt"):
    print("File exists")

# Get file information
file_size = os.path.getsize("file.txt")
print(f"File size: {file_size} bytes")
```

### pathlib Module (Python 3.4+)
```python
from pathlib import Path

# Create Path objects
file_path = Path("data") / "input.txt"
print(file_path)  # data/input.txt

# Check file properties
if file_path.exists():
    print(f"File size: {file_path.stat().st_size} bytes")
    print(f"Last modified: {file_path.stat().st_mtime}")

# Read and write easily
content = file_path.read_text()
file_path.write_text("New content")
```

## Binary File I/O

### Reading Binary Files
```python
# Read binary file
with open("image.jpg", "rb") as file:
    data = file.read()
    print(f"Read {len(data)} bytes")

# Process binary data
header = data[:10]  # First 10 bytes
print(f"Header: {header.hex()}")
```

### Writing Binary Files
```python
# Write binary data
binary_data = bytes([0x48, 0x65, 0x6C, 0x6C, 0x6F])  # "Hello" in bytes

with open("output.bin", "wb") as file:
    file.write(binary_data)
```

## String Encoding

### Text Encoding Basics
```python
# Write text with specific encoding
text = "Hello, 世界"

with open("utf8_file.txt", "w", encoding="utf-8") as file:
    file.write(text)

# Read text with encoding
with open("utf8_file.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

### Handling Encoding Errors
```python
# Specify error handling
with open("file.txt", "r", encoding="utf-8", errors="replace") as file:
    content = file.read()  # Replaces invalid chars with �

# Ignore encoding errors
with open("file.txt", "r", encoding="utf-8", errors="ignore") as file:
    content = file.read()  # Skips invalid characters
```

## Advanced I/O Techniques

### Reading Large Files
```python
# Process large file line by line
def process_large_file(filename):
    with open(filename, "r") as file:
        for line_number, line in enumerate(file, 1):
            # Process each line
            if "ERROR" in line:
                print(f"Error on line {line_number}: {line.strip()}")

process_large_file("large_log.txt")
```

### Context Managers
```python
# Custom context manager
class FileHandler:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

# Usage
with FileHandler("data.txt", "r") as file:
    content = file.read()
# File automatically closed
```

### Buffered I/O
```python
import io

# Buffered reading for performance
with open("large_file.txt", "r", buffering=8192) as file:
    for line in file:
        process_line(line)

# String buffer
string_buffer = io.StringIO()
string_buffer.write("Hello")
string_buffer.write(" World!")
content = string_buffer.getvalue()  # "Hello World!"
```

## Standard Streams

### stdin, stdout, stderr
```python
import sys

# Read from standard input
user_input = sys.stdin.read()

# Write to standard output
sys.stdout.write("Hello\n")

# Write to standard error
sys.stderr.write("Error: Something went wrong\n")

# Redirect output
original_stdout = sys.stdout
with open("output.txt", "w") as file:
    sys.stdout = file
    print("This goes to file")
sys.stdout = original_stdout
```

## Interactive Programs

### Menu-Driven Programs
```python
def show_menu():
    print("\n=== Calculator Menu ===")
    print("1. Add numbers")
    print("2. Subtract numbers")
    print("3. Multiply numbers")
    print("4. Divide numbers")
    print("5. Exit")

def get_numbers():
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    return a, b

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-5): ")

        if choice == "1":
            a, b = get_numbers()
            print(f"Result: {a + b}")
        elif choice == "2":
            a, b = get_numbers()
            print(f"Result: {a - b}")
        elif choice == "3":
            a, b = get_numbers()
            print(f"Result: {a * b}")
        elif choice == "4":
            a, b = get_numbers()
            if b != 0:
                print(f"Result: {a / b}")
            else:
                print("Error: Division by zero")
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

## Key Takeaways

1. **Input functions** like `input()` get data from users
2. **Output functions** like `print()` display information
3. **File operations** use `open()` with context managers for safety
4. **Error handling** prevents crashes from invalid input or files
5. **Encoding awareness** ensures proper text handling

## Further Reading
- Python I/O documentation
- File handling best practices
- Character encoding standards
- Command-line interface design
- Logging and output formatting