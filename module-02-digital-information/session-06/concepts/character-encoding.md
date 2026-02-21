# Character Encoding: How Text Becomes Digital

## The Text Storage Problem

Computers work with numbers, but humans communicate with text. Character encoding bridges this gap by assigning numeric codes to letters, symbols, and characters.

## ASCII: The Foundation

### What is ASCII?
American Standard Code for Information Interchange - the original character encoding standard.

- **Created**: 1960s for teleprinter communication
- **Size**: 7 bits (128 characters)
- **Coverage**: English letters, numbers, basic symbols

### ASCII Table
```
32-47:  !"#$%&'()*+,-./
48-57: 0123456789
65-90: ABCDEFGHIJKLMNOPQRSTUVWXYZ
97-122: abcdefghijklmnopqrstuvwxyz
```

### ASCII in Binary
```
'A' = 01000001 (decimal 65)
'B' = 01000010 (decimal 66)
'Hello' = 01001000 01100101 01101100 01101100 01101111
```

## Extended ASCII

### 8-Bit ASCII
- **Size**: 8 bits (256 characters)
- **Extra characters**: Accented letters, symbols, box drawing
- **Compatibility**: First 128 characters same as 7-bit ASCII
- **Problems**: Different code pages for different languages

### Code Page Confusion
Different regions used different extended ASCII variants:
- **CP1252**: Western European (Windows)
- **ISO-8859-1**: Western European (Linux/Unix)
- **KOI8-R**: Cyrillic (Russian)

## Unicode: The Universal Solution

### Unicode Goals
- **Universal**: Represent every character in every language
- **Unique**: Each character has exactly one code point
- **Consistent**: Same code for same character everywhere

### Unicode Code Points
- **Notation**: U+ followed by hexadecimal number
- **Range**: U+0000 to U+10FFFF (1,114,112 possible characters)
- **Examples**:
  - U+0041: Latin Capital Letter A
  - U+0627: Arabic Letter Alef
  - U+1F600: Grinning Face Emoji

## UTF-8: Unicode in Bytes

### Variable-Length Encoding
UTF-8 uses 1-4 bytes per character:
- **1 byte**: Standard ASCII (U+0000 to U+007F)
- **2 bytes**: Latin, Greek, Arabic (U+0080 to U+07FF)
- **3 bytes**: Basic multilingual (U+0800 to U+FFFF)
- **4 bytes**: Rare characters, emojis (U+10000 to U+10FFFF)

### UTF-8 Benefits
- **ASCII compatible**: Existing ASCII files work unchanged
- **Space efficient**: Common characters use fewer bytes
- **Self-synchronizing**: Can find character boundaries anywhere

### UTF-8 Examples
```
A:     01000001 (1 byte, same as ASCII)
á:     11000011 10100001 (2 bytes)
中:   11100100 10111000 10101101 (3 bytes)
😀:  11110000 10011111 10011000 10000000 (4 bytes)
```

## Other Unicode Encodings

### UTF-16
- **Fixed/variable**: 2 or 4 bytes per character
- **BOM**: Byte Order Mark to detect endianness
- **Usage**: Windows internally, Java strings

### UTF-32
- **Fixed size**: 4 bytes per character
- **Simple**: Direct mapping from code points
- **Wasteful**: Uses 4 bytes even for ASCII characters

## Encoding Detection

### Byte Order Mark (BOM)
Special bytes at file start:
- **UTF-8**: EF BB BF
- **UTF-16 BE**: FE FF
- **UTF-16 LE**: FF FE
- **UTF-32 BE**: 00 00 FE FF

### Content Analysis
- **Statistical methods**: Character frequency analysis
- **Heuristics**: Pattern matching for encoding signatures

## Programming with Encodings

### Python Encoding Examples
```python
# Encode string to bytes
text = "Hello, 世界"
utf8_bytes = text.encode('utf-8')
print(utf8_bytes)  # b'Hello, \xe4\xb8\x96\xe7\x95\x8c'

# Decode bytes to string
decoded = utf8_bytes.decode('utf-8')
print(decoded)  # "Hello, 世界"

# Handle encoding errors
try:
    bad_bytes.decode('ascii')
except UnicodeDecodeError:
    print("Cannot decode with ASCII")
```

### File I/O with Encoding
```python
# Write with specific encoding
with open('file.txt', 'w', encoding='utf-8') as f:
    f.write("Hello, 世界")

# Read with encoding detection
with open('file.txt', 'r', encoding='utf-8') as f:
    content = f.read()
```

## Common Encoding Issues

### Mojibake (Garbled Text)
When wrong encoding is used to decode:
```
Original: "café" (UTF-8: c3 a9)
Wrong decode (Latin-1): "cÃ©"
```

### Character Corruption
```
UTF-8 bytes interpreted as Latin-1:
UTF-8:     c3 a9 (é)
Latin-1:  Ã ©  (two characters)
```

### Truncation Issues
Cutting multi-byte characters:
```
"café" in UTF-8: 63 61 66 c3 a9
Cut at 4 bytes: 63 61 66 c3 → "cafÃ" (invalid)
```

## Normalization

### Unicode Equivalence
Different byte sequences for same visual character:
- **NFC**: Composed (single code point where possible)
- **NFD**: Decomposed (separate combining characters)
- **NFKC/NFKD**: Compatibility forms

### Example
```
é can be represented as:
- Single code point: U+00E9 (NFC)
- Base + combining: U+0065 U+0301 (NFD)
```

## Text Processing Considerations

### String Length
```python
text = "café"
print(len(text))  # 4 characters
print(len(text.encode('utf-8')))  # 5 bytes
```

### Substring Operations
```python
text = "café"
# Be careful with slicing multi-byte strings
print(text[3])  # 'é'
print(text[3:4])  # 'é'
```

### Regular Expressions
```python
import re
text = "café résumé naïve"
# Unicode-aware matching
matches = re.findall(r'\w+', text, re.UNICODE)
```

## Internationalization (I18N)

### Locale Support
- **Language codes**: en, es, zh, ar
- **Country codes**: US, MX, CN, SA
- **Script codes**: Latn, Cyrl, Hans

### Text Direction
- **LTR**: Left-to-right (English, Spanish)
- **RTL**: Right-to-left (Arabic, Hebrew)
- **BiDi**: Bidirectional text mixing

### Cultural Formatting
- **Numbers**: 1,234.56 vs 1.234,56
- **Dates**: MM/DD/YYYY vs DD/MM/YYYY
- **Currency**: $ vs € vs ¥

## Best Practices

### Always Specify Encoding
```python
# Good
with open('file.txt', 'r', encoding='utf-8') as f:
    content = f.read()

# Bad - uses system default
with open('file.txt', 'r') as f:
    content = f.read()
```

### Use Unicode Strings
```python
# Python 3: strings are Unicode by default
text = "Hello, 世界"  # Unicode string

# Convert to bytes when needed
data = text.encode('utf-8')
```

### Handle Errors Gracefully
```python
try:
    with open('file.txt', 'r', encoding='utf-8') as f:
        content = f.read()
except UnicodeDecodeError:
    print("File encoding issue")
    # Try different encoding or handle error
```

## Key Takeaways

1. **ASCII was the start**: 7-bit encoding for basic English text
2. **Unicode provides universality**: Every character in every language
3. **UTF-8 is the standard**: Efficient, backward-compatible encoding
4. **Encoding matters**: Wrong encoding leads to corrupted text
5. **Always specify encoding**: Prevents platform-dependent issues

## Further Reading
- Study Unicode standard documentation
- Learn about internationalization libraries
- Explore text processing algorithms
- Understand collation and sorting for different languages