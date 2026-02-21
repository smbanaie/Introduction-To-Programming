# Text Processing: Analyzing and Manipulating Strings

## Text Analysis Fundamentals

Text processing involves analyzing, transforming, and extracting information from strings. Python provides powerful tools for working with text data.

## String Searching and Finding

### Basic Search Methods
```python
text = "Python is a powerful programming language. Python is easy to learn."

# Find first occurrence (returns index)
print(text.find("Python"))        # 0
print(text.find("Java"))          # -1 (not found)

# Find from specific position
print(text.find("Python", 10))    # 43 (second occurrence)

# Check if substring exists
print("Python" in text)           # True
print("powerful" in text)         # True

# Count occurrences
print(text.count("Python"))       # 2
print(text.count("is"))           # 2
```

### Advanced Search with Regular Expressions
```python
import re

text = "Contact us at support@example.com or call 555-123-4567"

# Find email addresses
email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
emails = re.findall(email_pattern, text)
print(emails)  # ['support@example.com']

# Find phone numbers
phone_pattern = r'\d{3}-\d{3}-\d{4}'
phones = re.findall(phone_pattern, text)
print(phones)  # ['555-123-4567']

# Search with groups
date_text = "Meeting on 2024-01-15 and 2023-12-25"
date_pattern = r'(\d{4})-(\d{2})-(\d{2})'
matches = re.findall(date_pattern, date_text)
print(matches)  # [('2024', '01', '15'), ('2023', '12', '25')]
```

### Start and End Checking
```python
filenames = ["report.pdf", "data.csv", "script.py", "image.png"]

# Find PDF files
pdf_files = [f for f in filenames if f.endswith(".pdf")]
print(pdf_files)  # ['report.pdf']

# Find files starting with specific prefix
data_files = [f for f in filenames if f.startswith("data")]
print(data_files)  # ['data.csv']

# Check file extensions
for filename in filenames:
    if filename.endswith((".pdf", ".doc", ".docx")):
        print(f"{filename} is a document")
    elif filename.endswith((".csv", ".xlsx")):
        print(f"{filename} is a spreadsheet")
    elif filename.endswith((".py", ".js", ".java")):
        print(f"{filename} is a script")
```

## String Splitting and Joining

### Splitting Strings
```python
# Split on whitespace (default)
text = "Hello world, how are you?"
words = text.split()
print(words)  # ['Hello', 'world,', 'how', 'are', 'you?']

# Split on specific character
csv_line = "Alice,25,Engineer,New York"
fields = csv_line.split(',')
print(fields)  # ['Alice', '25', 'Engineer', 'New York']

# Split with max splits
sentence = "one:two:three:four:five"
parts = sentence.split(':', 2)  # Split only first 2 occurrences
print(parts)  # ['one', 'two', 'three:four:five']

# Split lines
multiline = "Line 1\nLine 2\nLine 3"
lines = multiline.split('\n')
print(lines)  # ['Line 1', 'Line 2', 'Line 3']

# Splitlines method (handles different line endings)
text_with_crlf = "Line 1\r\nLine 2\r\nLine 3"
lines = text_with_crlf.splitlines()
print(lines)  # ['Line 1', 'Line 2', 'Line 3']
```

### Joining Strings
```python
# Join list into string
words = ['Hello', 'world', 'how', 'are', 'you']
sentence = ' '.join(words)
print(sentence)  # "Hello world how are you"

# Join with different separators
path_parts = ['home', 'user', 'documents', 'file.txt']
file_path = '/'.join(path_parts)
print(file_path)  # "home/user/documents/file.txt"

# Join CSV data
data = ['Alice', '25', 'Engineer']
csv_line = ','.join(data)
print(csv_line)  # "Alice,25,Engineer"

# Join with formatting
numbers = [1, 2, 3, 4, 5]
formatted = ', '.join(str(n) for n in numbers)
print(formatted)  # "1, 2, 3, 4, 5"
```

## Text Transformation

### Case Conversion
```python
text = "Hello World"

print(text.upper())        # "HELLO WORLD"
print(text.lower())        # "hello world"
print(text.title())        # "Hello World"
print(text.capitalize())   # "Hello world"
print(text.swapcase())     # "hELLO wORLD"
```

### Character Replacement
```python
# Simple replacement
text = "I like Python programming"
new_text = text.replace("Python", "Java")
print(new_text)  # "I like Java programming"

# Replace limited occurrences
text = "one two one two one"
result = text.replace("one", "1", 2)  # Replace only first 2
print(result)  # "1 two 1 two one"

# Remove characters
text = "Hello, World!"
clean = text.replace(",", "").replace("!", "")
print(clean)  # "Hello World"

# Using translate for multiple replacements
trans_table = str.maketrans('aeiou', '12345')
text = "hello world"
result = text.translate(trans_table)
print(result)  # "h2ll4 w4rld"
```

### Whitespace Handling
```python
text = "   Hello   World   "

print(repr(text.strip()))     # "'Hello   World'"
print(repr(text.lstrip()))    # "'Hello   World   '"
print(repr(text.rstrip()))    # "'   Hello   World'"

# Remove all whitespace
no_spaces = ''.join(text.split())
print(no_spaces)  # "HelloWorld"

# Normalize whitespace
normalized = ' '.join(text.split())
print(repr(normalized))  # "'Hello World'"
```

## Text Validation and Cleaning

### Input Validation
```python
def validate_email(email):
    """Basic email validation"""
    if not email or '@' not in email:
        return False

    local, domain = email.split('@', 1)
    if not local or not domain or '.' not in domain:
        return False

    return True

def validate_phone(phone):
    """Basic phone number validation"""
    # Remove all non-digit characters
    digits = ''.join(c for c in phone if c.isdigit())

    # Check if we have 10 or 11 digits
    return len(digits) in (10, 11) and (len(digits) == 10 or digits[0] == '1')

print(validate_email("user@example.com"))    # True
print(validate_email("invalid-email"))       # False
print(validate_phone("555-123-4567"))        # True
print(validate_phone("123"))                 # False
```

### Text Cleaning Functions
```python
def clean_text(text):
    """Clean and normalize text"""
    if not text:
        return ""

    # Convert to lowercase
    text = text.lower()

    # Remove extra whitespace
    text = ' '.join(text.split())

    # Remove punctuation
    import string
    text = text.translate(str.maketrans('', '', string.punctuation))

    return text

def extract_words(text):
    """Extract alphanumeric words from text"""
    import re
    words = re.findall(r'\b\w+\b', text.lower())
    return words

# Usage
dirty_text = "  Hello, World!   How are you??  "
print(repr(clean_text(dirty_text)))     # "'hello world how are you'"
print(extract_words(dirty_text))         # ['hello', 'world', 'how', 'are', 'you']
```

## String Comparison and Sorting

### Natural String Comparison
```python
# ASCII comparison
print("apple" < "banana")     # True ('a' < 'b')
print("Apple" < "apple")      # True (uppercase before lowercase)
print("apple" < "Apple")      # False

# Case-insensitive comparison
text1, text2 = "Hello", "hello"
print(text1.lower() == text2.lower())  # True

# Using casefold for better Unicode support
print(text1.casefold() == text2.casefold())  # True
```

### String Sorting
```python
fruits = ["banana", "Apple", "cherry", "date"]

# Default sort (ASCII order)
sorted_fruits = sorted(fruits)
print(sorted_fruits)  # ['Apple', 'banana', 'cherry', 'date']

# Case-insensitive sort
sorted_fruits = sorted(fruits, key=str.lower)
print(sorted_fruits)  # ['Apple', 'banana', 'cherry', 'date']

# Sort by length
sorted_fruits = sorted(fruits, key=len)
print(sorted_fruits)  # ['date', 'Apple', 'banana', 'cherry']

# Reverse sort
sorted_fruits = sorted(fruits, key=str.lower, reverse=True)
print(sorted_fruits)  # ['date', 'cherry', 'banana', 'Apple']
```

## Text Statistics and Analysis

### Word Frequency Analysis
```python
def word_frequency(text):
    """Count word frequencies in text"""
    words = extract_words(text)
    frequency = {}

    for word in words:
        frequency[word] = frequency.get(word, 0) + 1

    return frequency

def most_common_words(text, n=5):
    """Find most common words"""
    freq = word_frequency(text)
    # Sort by frequency (descending), then by word (ascending)
    sorted_words = sorted(freq.items(), key=lambda x: (-x[1], x[0]))
    return sorted_words[:n]

text = """
Python is a programming language. Python is easy to learn.
Java is also a programming language. Java is widely used.
"""

freq = word_frequency(text)
print(freq)
# {'python': 2, 'is': 4, 'a': 2, 'programming': 2, 'language': 2, 'easy': 1, 'to': 1, 'learn': 1, 'java': 2, 'also': 1, 'widely': 1, 'used': 1}

common = most_common_words(text, 3)
print(common)  # [('is', 4), ('a', 2), ('language', 2)]
```

### Text Statistics
```python
def text_stats(text):
    """Calculate various text statistics"""
    words = extract_words(text)
    sentences = [s.strip() for s in text.split('.') if s.strip()]

    stats = {
        'characters': len(text),
        'words': len(words),
        'sentences': len(sentences),
        'avg_word_length': sum(len(word) for word in words) / len(words) if words else 0,
        'avg_sentence_length': len(words) / len(sentences) if sentences else 0
    }

    return stats

text = "Python is great. It is easy to learn. Many people love Python."
stats = text_stats(text)
for key, value in stats.items():
    if isinstance(value, float):
        print(f"{key}: {value:.1f}")
    else:
        print(f"{key}: {value}")
```

## Advanced Text Processing

### Text Tokenization
```python
import re

def tokenize(text):
    """Split text into meaningful tokens"""
    # Split on whitespace and punctuation
    pattern = r'\w+|[^\w\s]'
    tokens = re.findall(pattern, text)
    return tokens

def sentence_tokenize(text):
    """Split text into sentences"""
    # Simple sentence splitter
    sentences = re.split(r'[.!?]+', text)
    return [s.strip() for s in sentences if s.strip()]

text = "Hello, world! How are you? I'm fine."
print(tokenize(text))
# ['Hello', ',', 'world', '!', 'How', 'are', 'you', '?', 'I', "'m", 'fine', '.']

print(sentence_tokenize(text))
# ['Hello, world', 'How are you', "I'm fine"]
```

### Text Normalization
```python
def normalize_text(text):
    """Normalize text for consistent processing"""
    # Convert to lowercase
    text = text.lower()

    # Normalize whitespace
    text = ' '.join(text.split())

    # Handle contractions
    contractions = {
        "can't": "cannot",
        "won't": "will not",
        "i'm": "i am",
        "'re": " are",
        "'s": " is",
        "'ve": " have"
    }

    for contraction, expansion in contractions.items():
        text = text.replace(contraction, expansion)

    # Remove extra punctuation
    text = re.sub(r'[^\w\s]', '', text)

    return text.strip()

text = "I can't believe it's working! I'm so excited :)"
normalized = normalize_text(text)
print(normalized)  # "i cannot believe it is working i am so excited"
```

### Keyword Extraction
```python
def extract_keywords(text, min_length=4, max_words=10):
    """Extract important keywords from text"""
    words = extract_words(text)

    # Filter by length
    keywords = [word for word in words if len(word) >= min_length]

    # Count frequencies
    freq = {}
    for word in keywords:
        freq[word] = freq.get(word, 0) + 1

    # Sort by frequency and return top keywords
    sorted_keywords = sorted(freq.items(), key=lambda x: x[1], reverse=True)
    return [word for word, count in sorted_keywords[:max_words]]

text = """
Machine learning is a subset of artificial intelligence.
Machine learning algorithms learn from data.
Deep learning is part of machine learning.
"""

keywords = extract_keywords(text)
print(keywords)  # ['machine', 'learning', 'data', 'deep', 'part', 'algorithms', 'from', 'artificial', 'intelligence', 'subset']
```

## Performance Considerations

### Efficient String Operations
```python
# Avoid repeated string concatenation in loops
# Bad: O(n²) performance
result = ""
for word in words:
    result += word + " "  # Creates new string each time

# Good: O(n) performance
result = " ".join(words)

# Use list comprehension for filtering
# Good
long_words = [word for word in words if len(word) > 5]

# Avoid
long_words = []
for word in words:
    if len(word) > 5:
        long_words.append(word)
```

### Memory Usage with Large Texts
```python
# Process large files line by line
def process_large_file(filename):
    word_count = 0
    with open(filename, 'r') as file:
        for line in file:
            words = extract_words(line)
            word_count += len(words)
    return word_count

# Use generators for memory efficiency
def find_lines_with_word(filename, search_word):
    with open(filename, 'r') as file:
        for line_num, line in enumerate(file, 1):
            if search_word.lower() in line.lower():
                yield line_num, line.strip()
```

## Key Takeaways

1. **Regular expressions** enable powerful pattern matching and text analysis
2. **String methods** provide efficient text manipulation operations
3. **Splitting and joining** are fundamental for text processing
4. **Text normalization** ensures consistent processing
5. **Performance matters** when processing large amounts of text
6. **Combine multiple techniques** for comprehensive text analysis

## Further Reading
- Natural Language Processing (NLP) libraries
- Regular expression advanced patterns
- Unicode text processing
- Text mining and information extraction techniques