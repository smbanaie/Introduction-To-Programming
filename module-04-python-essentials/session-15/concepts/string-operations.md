# String Operations: Manipulating Text

## String Basics Review

Strings are sequences of characters used to represent text. Python strings are immutable, meaning they cannot be changed after creation.

## Creating and Accessing Strings

### String Creation
```python
# Single quotes
name = 'Alice'

# Double quotes
message = "Hello, World!"

# Triple quotes for multi-line
poem = """Roses are red
Violets are blue"""

# Empty string
empty = ""
empty = str()

# Convert to string
age_str = str(25)
pi_str = str(3.14159)
```

### String Access
```python
text = "Python"

# Positive indexing (from start)
print(text[0])    # 'P'
print(text[1])    # 'y'

# Negative indexing (from end)
print(text[-1])   # 'n'
print(text[-2])   # 'o'

# Length
print(len(text))  # 6
```

## Basic String Operations

### Concatenation
```python
# Using + operator
first = "Hello"
second = "World"
result = first + " " + second  # "Hello World"

# Multiple concatenations
greeting = "Hi"
name = "Alice"
full = greeting + ", " + name + "!"  # "Hi, Alice!"

# Concatenating with other types (requires conversion)
age = 25
info = "Age: " + str(age)  # "Age: 25"
```

### Repetition
```python
# Repeat strings
line = "=" * 50
print(line)  # "=================================================="

# Create patterns
dots = "." * 10  # ".........."
stars = "*" * 5  # "*****"
```

### Membership Testing
```python
text = "Python programming"

# Check if substring exists
print("Python" in text)    # True
print("Java" in text)      # False
print("pro" in text)       # True (case sensitive)

# Check if not in string
print("Java" not in text)  # True
```

## String Slicing

### Basic Slicing
```python
text = "Python Programming"

# Get substring from index 0 to 5
print(text[0:6])   # "Python"

# From index 7 to end
print(text[7:])    # "Programming"

# From start to index 6
print(text[:6])    # "Python"

# Entire string
print(text[:])     # "Python Programming"
```

### Advanced Slicing
```python
# With step parameter
numbers = "0123456789"

# Every other character
print(numbers[::2])    # "02468"

# Reverse string
print(text[::-1])      # "gnimmargorP nohtyP"

# Every 3rd character
print(numbers[::3])    # "0369"

# Reverse every other character
print(numbers[::-2])   # "97531"
```

### Practical Slicing Examples
```python
filename = "document.pdf"

# Get file extension
extension = filename[-3:]  # "pdf"

# Get filename without extension
name_only = filename[:-4]  # "document"

# Extract domain from email
email = "user@example.com"
domain = email.split('@')[1]  # "example.com"

# Get first 10 characters
preview = text[:10] + "..." if len(text) > 10 else text
```

## String Methods

### Case Conversion
```python
text = "Hello World"

# Convert to uppercase
print(text.upper())       # "HELLO WORLD"

# Convert to lowercase
print(text.lower())       # "hello world"

# Capitalize first letter
print(text.capitalize())  # "Hello world"

# Title case
print(text.title())       # "Hello World"

# Swap case
print(text.swapcase())    # "hELLO wORLD"
```

### Searching and Finding
```python
text = "Python is powerful and Python is fun"

# Find first occurrence
print(text.find("Python"))    # 0
print(text.find("Java"))      # -1 (not found)

# Find from specific position
print(text.find("Python", 10)) # 23 (second occurrence)

# Count occurrences
print(text.count("Python"))   # 2
print(text.count("is"))       # 2

# Check start/end
print(text.startswith("Python"))  # True
print(text.endswith("fun"))       # True
```

### Replacing and Splitting
```python
text = "I like Python programming"

# Replace substrings
new_text = text.replace("Python", "Java")
print(new_text)  # "I like Java programming"

# Replace limited occurrences
new_text = text.replace("i", "I", 1)  # Only first occurrence
print(new_text)  # "I like Python programming"

# Split into list
words = text.split()  # ['I', 'like', 'Python', 'programming']

# Split on specific character
csv_data = "Alice,25,Engineer"
fields = csv_data.split(',')  # ['Alice', '25', 'Engineer']

# Join list into string
words = ['Hello', 'World']
sentence = ' '.join(words)  # "Hello World"

# Join with different separator
path = ['home', 'user', 'documents']
full_path = '/'.join(path)  # "home/user/documents"
```

### Testing and Validation
```python
# Check character types
print("123".isdigit())      # True
print("abc".isalpha())      # True
print("abc123".isalnum())   # True
print("hello".islower())    # True
print("HELLO".isupper())    # True
print("Hello".istitle())    # True
print("   ".isspace())      # True (all whitespace)

# Check string properties
print("".isspace())         # False (empty string)
print("Hello".isspace())    # False (contains non-space)
```

### Stripping Whitespace
```python
text = "   Hello World   "

# Remove leading/trailing whitespace
print(text.strip())    # "Hello World"

# Remove only leading whitespace
print(text.lstrip())   # "Hello World   "

# Remove only trailing whitespace
print(text.rstrip())   # "   Hello World"

# Remove specific characters
text2 = "xxxHelloxxx"
print(text2.strip('x'))  # "Hello"
```

## String Formatting

### Old Style Formatting (%)
```python
name = "Alice"
age = 25

# Basic formatting
print("My name is %s and I am %d years old" % (name, age))

# With precision
pi = 3.14159265359
print("Pi is approximately %.2f" % pi)

# Multiple values
print("Name: %s, Age: %d, Score: %.1f" % (name, age, 95.5))
```

### New Style Formatting (.format())
```python
# Positional arguments
print("My name is {} and I am {} years old".format(name, age))

# Indexed arguments
print("My name is {0} and I am {1} years old. {0} is a great name!".format(name, age))

# Named arguments
print("My name is {name} and I am {age} years old".format(name=name, age=age))

# Formatting options
print("Pi is approximately {:.2f}".format(pi))
print("Number with commas: {:,}".format(1234567))
```

### F-Strings (Python 3.6+)
```python
# Simple f-strings
print(f"My name is {name} and I am {age} years old")

# Expressions in f-strings
print(f"Next year I will be {age + 1} years old")

# Formatting in f-strings
print(f"Pi is approximately {pi:.2f}")
print(f"Binary of 10 is {10:b}")
print(f"Hex of 255 is {255:x}")

# Multi-line f-strings
message = f"""
Name: {name}
Age: {age}
Next year: {age + 1}
"""
print(message)
```

## Advanced String Operations

### String Translation
```python
# Create translation table
trans = str.maketrans('aeiou', '12345')
text = "hello world"

# Apply translation
result = text.translate(trans)
print(result)  # "h2ll4 w4rld"
```

### String Encoding/Decoding
```python
# Encode to bytes
text = "Hello, 世界"
utf8_bytes = text.encode('utf-8')
print(utf8_bytes)  # b'Hello, \xe4\xb8\x96\xe7\x95\x8c'

# Decode from bytes
decoded = utf8_bytes.decode('utf-8')
print(decoded)  # "Hello, 世界"
```

### Regular Expressions (regex)
```python
import re

text = "Email: user@example.com, Phone: 123-456-7890"

# Find email pattern
email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
emails = re.findall(email_pattern, text)
print(emails)  # ['user@example.com']

# Find phone pattern
phone_pattern = r'\d{3}-\d{3}-\d{4}'
phones = re.findall(phone_pattern, text)
print(phones)  # ['123-456-7890']

# Replace patterns
censored = re.sub(phone_pattern, "***-***-****", text)
print(censored)  # "Email: user@example.com, Phone: ***-***-****"
```

## String Performance Considerations

### String Concatenation in Loops
```python
# Inefficient - creates new string each time
result = ""
for i in range(1000):
    result += str(i) + " "  # Bad: O(n²) performance

# Better - use list then join
parts = []
for i in range(1000):
    parts.append(str(i))
result = " ".join(parts)  # O(n) performance

# Best - list comprehension
result = " ".join(str(i) for i in range(1000))
```

### String Interning
```python
# Python automatically interns short strings
a = "hello"
b = "hello"
print(a is b)  # True (same object in memory)

# Longer strings may not be interned
long_a = "a" * 1000
long_b = "a" * 1000
print(long_a is long_b)  # False (different objects)
```

## Common String Tasks

### Text Processing Examples
```python
def clean_text(text):
    """Clean and normalize text"""
    # Convert to lowercase
    text = text.lower()
    # Remove extra whitespace
    text = ' '.join(text.split())
    # Remove punctuation
    import string
    text = text.translate(str.maketrans('', '', string.punctuation))
    return text

def extract_words(text):
    """Extract words from text"""
    import re
    words = re.findall(r'\b\w+\b', text.lower())
    return words

def word_frequency(text):
    """Count word frequencies"""
    words = extract_words(text)
    frequency = {}
    for word in words:
        frequency[word] = frequency.get(word, 0) + 1
    return frequency

# Usage
text = "Hello, hello! How are you? Hello again."
print(clean_text(text))        # "hello hello how are you hello again"
print(extract_words(text))     # ['hello', 'hello', 'how', 'are', 'you', 'hello', 'again']
print(word_frequency(text))    # {'hello': 3, 'how': 1, 'are': 1, 'you': 1, 'again': 1}
```

### String Validation
```python
def is_valid_email(email):
    """Basic email validation"""
    import re
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return bool(re.match(pattern, email))

def is_strong_password(password):
    """Check password strength"""
    if len(password) < 8:
        return False
    has_upper = any(c.isupper() for c in password)
    has_lower = any(c.islower() for c in password)
    has_digit = any(c.isdigit() for c in password)
    return has_upper and has_lower and has_digit

# Usage
print(is_valid_email("user@example.com"))     # True
print(is_valid_email("invalid-email"))        # False
print(is_strong_password("StrongPass123"))    # True
print(is_strong_password("weak"))             # False
```

## Key Takeaways

1. **Strings are immutable sequences** of characters
2. **Use slicing** for extracting substrings efficiently
3. **String methods** provide powerful text manipulation tools
4. **Choose formatting method** based on Python version and needs
5. **Regular expressions** enable complex pattern matching
6. **Performance matters** in string operations, especially concatenation

## Further Reading
- Unicode and character encoding
- Regular expression patterns and best practices
- Text processing libraries (nltk, spaCy)
- String algorithms and data structures