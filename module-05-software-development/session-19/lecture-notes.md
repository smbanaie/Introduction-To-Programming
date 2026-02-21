# Session 19: File Input/Output

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will read from and write to files to persist program data
**Materials**: Whiteboard, sample data files, file operation examples

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you handle errors with try/except?
- **Hook Activity**: Show data disappearing when program ends vs saving to file
- **Question**: "How can programs remember data between runs?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Open, read, and write text files
- Handle file operations safely
- Work with different file formats
- Manage file system operations

### Agenda Overview (5 minutes)
1. File operations basics
2. Reading from files
3. Writing to files
4. File management and safety

---

## II. Main Content (50 minutes)

### A. File Operations Basics (10 minutes)

#### Opening and Closing Files
```python
# Open a file for reading (default mode)
file = open("data.txt", "r")

# Always close files when done
file.close()

# Better: Use 'with' statement (auto-closes)
with open("data.txt", "r") as file:
    # File operations here
    pass
# File automatically closed here
```

#### File Modes
- **"r"**: Read (default) - File must exist
- **"w"**: Write - Creates new file or overwrites existing
- **"a"**: Append - Adds to end of existing file or creates new
- **"x"**: Exclusive create - Fails if file exists

#### File Paths
```python
# Relative paths (from current directory)
"data.txt"
"folder/data.txt"

# Absolute paths (full path)
"/Users/username/Documents/data.txt"  # Mac/Linux
"C:\\Users\\username\\Documents\\data.txt"  # Windows

# Current directory
import os
current_dir = os.getcwd()  # Get current working directory
```

### B. Reading from Files (15 minutes)

#### Reading Entire Files
```python
# Read entire file as string
with open("story.txt", "r") as file:
    content = file.read()
    print(content)

# Read all lines into a list
with open("names.txt", "r") as file:
    lines = file.readlines()
    print(lines)  # ['Alice\n', 'Bob\n', 'Charlie\n']

# Read line by line
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # Remove newline characters
```

#### Reading with Different Methods
```python
with open("numbers.txt", "r") as file:
    # Read specific number of characters
    first_10 = file.read(10)

    # Read one line
    line1 = file.readline()

    # Read remaining lines
    rest = file.readlines()
```

#### Processing File Data
```python
# Read numbers from file and calculate sum
total = 0
count = 0

with open("numbers.txt", "r") as file:
    for line in file:
        try:
            number = float(line.strip())
            total += number
            count += 1
        except ValueError:
            print(f"Skipping invalid number: {line.strip()}")

if count > 0:
    average = total / count
    print(f"Average: {average}")
```

#### Working with CSV-like Data
```python
# Simple CSV processing
with open("students.csv", "r") as file:
    for line in file:
        parts = line.strip().split(",")
        if len(parts) >= 2:
            name, grade = parts[0], parts[1]
            print(f"{name}: {grade}")
```

### C. Writing to Files (15 minutes)

#### Writing Text Files
```python
# Write to new file (overwrites if exists)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a test file.\n")

# Append to existing file
with open("log.txt", "a") as file:
    file.write(f"Program started at {time.ctime()}\n")
```

#### Writing Lists and Data
```python
# Write list of names to file
names = ["Alice", "Bob", "Charlie", "Diana"]

with open("names.txt", "w") as file:
    for name in names:
        file.write(name + "\n")

# Write dictionary data
student_grades = {
    "Alice": 95,
    "Bob": 87,
    "Charlie": 92
}

with open("grades.txt", "w") as file:
    file.write("Name,Grade\n")  # Header
    for name, grade in student_grades.items():
        file.write(f"{name},{grade}\n")
```

#### Safe File Writing
```python
import os

def safe_write(filename, content):
    """Write content to file safely."""
    # Create backup if file exists
    if os.path.exists(filename):
        backup = filename + ".backup"
        os.rename(filename, backup)

    try:
        with open(filename, "w") as file:
            file.write(content)
        # Remove backup on success
        if os.path.exists(backup):
            os.remove(backup)
    except Exception as e:
        # Restore backup on failure
        if os.path.exists(backup):
            os.rename(backup, filename)
        raise e
```

### D. File Management and Safety (10 minutes)

#### File Existence and Properties
```python
import os

filename = "data.txt"

# Check if file exists
if os.path.exists(filename):
    print("File exists")
else:
    print("File does not exist")

# Get file size
if os.path.exists(filename):
    size = os.path.getsize(filename)
    print(f"File size: {size} bytes")

# Check if it's a file or directory
if os.path.isfile(filename):
    print("It's a file")
elif os.path.isdir(filename):
    print("It's a directory")
```

#### Directory Operations
```python
import os

# Create directory
os.makedirs("data_folder", exist_ok=True)

# List files in directory
files = os.listdir(".")
print("Files in current directory:")
for file in files:
    if os.path.isfile(file):
        print(f"  {file}")

# Get file extension
filename = "document.pdf"
name, extension = os.path.splitext(filename)
print(f"Name: {name}, Extension: {extension}")
```

#### Error Handling for Files
```python
def read_file_safely(filename):
    """Read file with comprehensive error handling."""
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
        return None
    except PermissionError:
        print(f"Error: No permission to read '{filename}'")
        return None
    except UnicodeDecodeError:
        print(f"Error: File '{filename}' is not a text file")
        return None
    except Exception as e:
        print(f"Unexpected error reading file: {e}")
        return None
```

---

## III. Interactive Activities (15 minutes)

### File Processing Workshop (10 minutes)
- **Individual**: Create programs that read/write files
- **Examples**: Todo list manager, grade book, simple database
- **Features**: Add, list, search, save data

### Data Import/Export Challenge (5 minutes)
- **Pairs**: Convert between data formats
- **Task**: Read CSV-like data, process it, write to different format
- **Discuss**: File format choices and trade-offs

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Files persist data**: Save information between program runs
2. **Context managers**: Use 'with' for safe file operations
3. **Read vs write modes**: Different modes for different operations
4. **Error handling**: Files can fail - handle gracefully

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. How do you safely open a file for reading?
2. What's the difference between "w" and "a" modes?
3. Why should you use 'with' for file operations?

### Preview of Next Session (2 minutes)
"Next time we'll learn modules - organizing code into reusable components!"

---

## Additional Resources
- **Visual Aid**: File operation flow diagram
- **Handout**: File mode reference
- **Homework**: Create a contact list program with file storage

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes