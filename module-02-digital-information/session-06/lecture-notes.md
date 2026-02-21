# Session 6: Text Representation

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will understand how text characters are encoded in binary
**Materials**: Whiteboard, ASCII table handout, Unicode examples from different languages

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: Add binary 101 + 011
- **Hook Activity**: Type a message and show its binary representation
- **Question**: "How can computers store letters, emojis, and text from any language?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Explain ASCII and Unicode encoding systems
- Convert text to binary and back
- Understand character encoding evolution
- Apply text representation to programming scenarios

### Agenda Overview (5 minutes)
1. Character encoding basics
2. ASCII system
3. Unicode and modern text
4. Encoding in programming

---

## II. Main Content (50 minutes)

### A. Character Encoding Fundamentals (10 minutes)

#### Why Encoding Matters
- **Digital storage**: All data must be binary
- **Standardization**: Everyone must agree on representations
- **Compatibility**: Different systems must understand each other
- **Internationalization**: Support for all world languages

#### Encoding vs Encryption
- **Encoding**: Converting to binary representation (reversible)
- **Encryption**: Securing data (requires key to reverse)
- **Example**: ASCII encoding vs AES encryption

### B. ASCII Character Set (20 minutes)

#### ASCII Overview
- **American Standard Code for Information Interchange**
- **7 bits per character**: 128 possible characters
- **Created in 1963**: For teleprinter communication
- **Still widely used**: Foundation of computing

#### ASCII Table Structure

| Decimal | Binary | Character | Description |
|---------|--------|-----------|-------------|
| 32 | 00100000 | [space] | Space character |
| 48 | 00110000 | '0' | Digit zero |
| 65 | 01000001 | 'A' | Uppercase A |
| 97 | 01100001 | 'a' | Lowercase a |
| 127 | 01111111 | DEL | Delete character |

#### ASCII Patterns
- **Digits 0-9**: 48-57 (00110000 to 00111001)
- **Uppercase A-Z**: 65-90 (01000001 to 01011010)
- **Lowercase a-z**: 97-122 (01100001 to 01111010)
- **Control characters**: 0-31 (formatting, device control)

#### Text to Binary Conversion
```
"Hello" in ASCII:
H = 01001000
e = 01100101
l = 01101100
l = 01101100
o = 01101111
```

### C. Unicode System (20 minutes)

#### Unicode Evolution
- **ASCII limitation**: Only English and basic symbols
- **Unicode goal**: Represent every character in every language
- **UTF-8**: Most common Unicode encoding (variable length)

#### Unicode vs ASCII Comparison

| Feature | ASCII | Unicode (UTF-8) |
|---------|-------|-----------------|
| **Characters** | 128 | 1,112,064+ |
| **Languages** | English + symbols | All world languages |
| **Bytes per char** | 1 byte | 1-4 bytes |
| **Backward compatible** | N/A | Yes with ASCII |

#### Unicode Examples
```
English 'A' = U+0041 (same as ASCII)
Arabic 'ا' = U+0627
Emoji 😀 = U+1F600
Chinese '中' = U+4E2D
```

#### UTF-8 Encoding
- **1 byte**: Standard ASCII (0-127)
- **2 bytes**: Latin, Greek, Arabic (128-2047)
- **3 bytes**: Basic multilingual (2048-65535)
- **4 bytes**: Rare characters, emojis (65536+)

---

## III. Interactive Activities (15 minutes)

### ASCII Decoder Challenge (10 minutes)
- **Groups**: Decode binary strings to text
- **Examples**: Famous quotes, names, messages
- **Competition**: Fastest accurate decoding wins

### Unicode Explorer (5 minutes)
- **Activity**: Show characters from different writing systems
- **Discussion**: How many bytes for each character?
- **Real-world**: Search for Unicode characters online

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Text needs encoding**: Characters must be converted to binary for computers
2. **ASCII is foundational**: 128 characters for basic English communication
3. **Unicode enables globalization**: Support for all world languages and symbols
4. **UTF-8 is efficient**: Variable length encoding balances space and compatibility

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. What is the ASCII code for 'A'?
2. How many bytes can Unicode characters use?
3. Why was Unicode created?

### Preview of Next Module (2 minutes)
"Next module we'll learn algorithmic thinking - how to design step-by-step solutions before writing code!"

---

## Additional Resources
- **Visual Aid**: ASCII table poster
- **Handout**: Unicode character examples
- **Homework**: Find ASCII codes for your name

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes