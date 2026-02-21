# String Operations: Manipulating Text Data

## Strings as Sequences

In programming, strings are sequences of characters. Each character has a position (index) and can be accessed individually or manipulated as a group.

## Basic String Operations

### Creating Strings
```python
# Single quotes
text1 = 'Hello'

# Double quotes
text2 = "World"

# Multi-line strings
poem = """Roses are red
Violets are blue"""

# Escape sequences
path = "C:\\Users\\file.txt"
quote = "He said \"Hello\""
```

### String Concatenation
```python
# Using + operator
full_name = first_name + " " + last_name

# Using join() for efficiency
words = ["Hello", "world", "from", "Python"]
sentence = " ".join(words)  # "Hello world from Python"

# String multiplication
divider = "=" * 50  # "=================================================="
```

## String Indexing and Slicing

### Character Access
```python
text = "Python"
print(text[0])    # 'P' (first character)
print(text[5])    # 'n' (last character)
print(text[-1])   # 'n' (negative indexing)
```

### String Slicing
```python
text = "Hello World"

# Basic slicing: string[start:end]
print(text[0:5])   # 'Hello'
print(text[6:])    # 'World'
print(text[:5])    # 'Hello'

# With step: string[start:end:step]
print(text[::2])   # 'HloWrd' (every other character)
print(text[::-1])  # 'dlroW olleH' (reversed)
```

## String Methods

### Case Conversion
```python
text = "Hello World"

text.upper()       # 'HELLO WORLD'
text.lower()       # 'hello world'
text.capitalize()  # 'Hello world'
text.title()       # 'Hello World'
text.swapcase()    # 'hELLO wORLD'
```

### Searching and Finding
```python
text = "Python programming is fun"

text.find("pro")          # 7 (index where found)
text.find("xyz")          # -1 (not found)
text.index("pro")         # 7 (raises error if not found)
text.count("i")           # 2 (count occurrences)
text.startswith("Python") # True
text.endswith("fun")      # True
```

### Modification Methods
```python
text = "  Hello World  "

text.strip()              # 'Hello World' (remove whitespace)
text.lstrip()             # 'Hello World  ' (left strip)
text.rstrip()             # '  Hello World' (right strip)

text.replace("World", "Python")  # '  Hello Python  '
text.split()              # ['Hello', 'World'] (split on spaces)
text.split("l")           # ['  He', '', 'o Wor', 'd  ']
```

### Testing Methods
```python
text = "Hello123"

text.isalpha()     # False (contains numbers)
text.isdigit()     # False (contains letters)
text.isalnum()     # True (letters and numbers)
text.islower()     # False (mixed case)
text.isupper()     # False (not all upper)
text.isspace()     # False (not all whitespace)
```

## Advanced String Formatting

### F-Strings (Python 3.6+)
```python
name = "Alice"
age = 25
height = 1.68

# Basic f-string
message = f"Hello, {name}!"

# With expressions
message = f"Next year you will be {age + 1} years old."

# With formatting
message = f"Height: {height:.2f} meters"
message = f"Age: {age:03d}"  # Zero-padded
```

### Format Method
```python
# Positional formatting
template = "{} is {} years old".format(name, age)
# "Alice is 25 years old"

# Named formatting
template = "{name} is {age} years old and {height:.1f}m tall".format(
    name=name, age=age, height=height)

# Format specifications
f"Value: {42:04d}"    # 'Value: 0042'
f"Float: {3.14159:.2f}"  # 'Float: 3.14'
```

### Old Style Formatting
```python
# % formatting (legacy)
template = "%s is %d years old" % (name, age)
# "Alice is 25 years old"
```

## String Comparison and Sorting

### Lexicographic Comparison
```python
"apple" < "banana"     # True (a < b)
"Apple" < "apple"      # True (A < a in ASCII)
"10" < "2"            # True (1 < 2, lexicographic not numeric)
```

### Case-Insensitive Comparison
```python
text1 = "Hello"
text2 = "hello"

text1.lower() == text2.lower()  # True
text1.casefold() == text2.casefold()  # True (better for internationalization)
```

### Sorting Strings
```python
words = ["zebra", "apple", "Banana", "cherry"]
sorted(words)  # ['Banana', 'apple', 'cherry', 'zebra'] (ASCII order)

# Case-insensitive sort
sorted(words, key=str.lower)  # ['apple', 'Banana', 'cherry', 'zebra']
```

## Regular Expressions

### Pattern Matching
```python
import re

text = "The email is user@example.com and phone is 555-1234"

# Find email
email = re.search(r'\w+@\w+\.\w+', text)
print(email.group())  # 'user@example.com'

# Find phone
phone = re.search(r'\d{3}-\d{4}', text)
print(phone.group())  # '555-1234'

# Replace
cleaned = re.sub(r'\d{3}-\d{4}', '[PHONE]', text)
print(cleaned)  # 'The email is user@example.com and phone is [PHONE]'
```

### Common Patterns
```python
# Email
r'[\w\.-]+@[\w\.-]+\.\w+'

# Phone (US)
r'\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}'

# URL
r'https?://(?:[-\w.])+(?:[:\d]+)?(?:/(?:[\w/_.])*(?:\?(?:[\w&=%.])*)?(?:#(?:\w*))?)?'

# Date (MM/DD/YYYY)
r'\d{1,2}/\d{1,2}/\d{4}'
```

## Text Processing Algorithms

### String Reversal
```python
def reverse_string(text):
    return text[::-1]

# Or using recursion
def reverse_recursive(text):
    if len(text) <= 1:
        return text
    return reverse_recursive(text[1:]) + text[0]
```

### Palindrome Check
```python
def is_palindrome(text):
    clean_text = ''.join(c.lower() for c in text if c.isalnum())
    return clean_text == clean_text[::-1]

print(is_palindrome("A man, a plan, a canal: Panama"))  # True
```

### Word Frequency Count
```python
def word_frequency(text):
    words = text.lower().split()
    frequency = {}
    for word in words:
        # Remove punctuation
        word = ''.join(c for c in word if c.isalnum())
        if word:
            frequency[word] = frequency.get(word, 0) + 1
    return frequency
```

### String Compression
```python
def compress_string(text):
    if not text:
        return ""
    compressed = []
    count = 1
    for i in range(1, len(text)):
        if text[i] == text[i-1]:
            count += 1
        else:
            compressed.append(text[i-1] + str(count))
            count = 1
    compressed.append(text[-1] + str(count))
    result = ''.join(compressed)
    return result if len(result) < len(text) else text

print(compress_string("aabcccccaaa"))  # "a2b1c5a3"
```

## Unicode and International Text

### Unicode Operations
```python
# Unicode normalization
import unicodedata

text = "café"
normalized = unicodedata.normalize('NFC', text)

# Unicode categories
for char in text:
    print(f"{char}: {unicodedata.category(char)}")
```

### Handling Different Scripts
```python
# Arabic text (right-to-left)
arabic = "مرحبا بالعالم"

# Mixed scripts
mixed = "Hello 世界 Привет"

# Length considerations
len(mixed)  # 15 (character count)
len(mixed.encode('utf-8'))  # 21 (byte count)
```

## Performance Considerations

### String Immutability
```python
# Strings are immutable - each operation creates new string
text = "hello"
text = text.upper()  # Creates new string
text = text + " world"  # Creates another new string

# For many operations, use lists then join
parts = []
for i in range(1000):
    parts.append(str(i))
result = ''.join(parts)  # Efficient
```

### String Interning
```python
# Python interns short strings for efficiency
a = "hello"
b = "hello"
a is b  # True (same object)

# But not for longer or dynamically created strings
a = "a" * 1000
b = "a" * 1000
a is b  # False (different objects)
```

## Common String Problems

### Encoding Issues
```python
# Wrong encoding leads to errors
text = "café"
try:
    text.encode('ascii')  # Will fail
except UnicodeEncodeError:
    print("Cannot encode with ASCII")
```

### Index Errors
```python
text = "hello"
# text[10]  # IndexError
# Use slicing safely
chunk = text[2:10]  # No error, just truncated
```

### Case Sensitivity Issues
```python
# Case-sensitive by default
"Apple" == "apple"  # False

# Use lower() for case-insensitive
"Apple".lower() == "apple".lower()  # True
```

## Key Takeaways

1. **Strings are sequences**: Characters can be accessed by index
2. **Rich method library**: 40+ methods for text manipulation
3. **Formatting options**: f-strings, format(), % formatting
4. **Unicode support**: Handle text in any language
5. **Performance matters**: Consider immutability and interning

## Further Reading
- Study string algorithms (KMP, Boyer-Moore)
- Learn about text compression techniques
- Explore natural language processing
- Understand collation and internationalization