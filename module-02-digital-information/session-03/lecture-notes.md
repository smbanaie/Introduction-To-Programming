# Session 3: Bits, Bytes, and Data

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will understand how all digital information is stored using binary
**Materials**: Whiteboard, binary number cards, data size comparison chart

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How does source code become machine code?
- **Hook Demonstration**: Show a digital photo on screen, then zoom in to show pixels
- **Question**: "How can a computer store photos, videos, text, and numbers using only electricity?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Explain what bits and bytes are
- Understand binary representation
- Convert between decimal and binary
- Describe how different data types are stored

### Agenda Overview (5 minutes)
1. The binary system foundation
2. Bits, bytes, and data sizes
3. Real-world data representation
4. Binary conversion practice

---

## II. Main Content (50 minutes)

### A. The Binary Foundation (15 minutes)

#### Why Binary?
- **Electrical Reality**: Computers use electricity (on/off, high/low voltage)
- **Reliability**: Only two states reduces errors
- **Logic Gates**: Binary enables digital logic circuits
- **Scalability**: Can represent any information with patterns of 0s and 1s

#### Bits and Bytes Defined

| Unit | Size | What It Represents | Example |
|------|------|-------------------|---------|
| **Bit** | 1 binary digit | Single on/off value | 0 or 1 |
| **Byte** | 8 bits | Smallest addressable unit | 256 possible values (0-255) |
| **Kilobyte (KB)** | 1,000 bytes | Small text file | ~1 paragraph |
| **Megabyte (MB)** | 1,000 KB | Photo or song | ~1 minute MP3 |
| **Gigabyte (GB)** | 1,000 MB | Movie or large app | ~2 hours video |
| **Terabyte (TB)** | 1,000 GB | Large storage | ~500 hours video |

#### Data Size Visualization
```
1 Bit = 1 binary digit (0 or 1)
1 Byte = 8 bits = 256 possibilities
1 KB = 1,000 bytes = ~1,000 characters
1 MB = 1,000 KB = ~1 million characters
1 GB = 1,000 MB = ~1 billion characters
```

### B. Binary Number System (20 minutes)

#### Binary vs Decimal Comparison

| Decimal (Base 10) | Binary (Base 2) |
|------------------|-----------------|
| Digits: 0-9 | Digits: 0-1 |
| 10¹ = 10 | 2¹ = 2 |
| 10² = 100 | 2² = 4 |
| 10³ = 1,000 | 2³ = 8 |

#### Binary Place Values
```
Binary:  1  0  1  0  1  0  1  0
Places: 128 64 32 16 8  4  2  1
Value:  128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170
```

#### Common Binary Patterns
- **1 byte (8 bits)**: 0-255 range
- **4 bits (nibble)**: 0-15 range (used in hex conversion)
- **Word**: Typically 32 or 64 bits (computer word size)

### C. Data Representation Examples (15 minutes)

#### Numbers
- **Integers**: Direct binary representation
- **Example**: Decimal 42 = Binary 101010

#### Text (Characters)
- **ASCII**: 7 bits per character (128 characters)
- **Unicode**: 16+ bits per character (global languages)
- **Example**: 'A' = Binary 01000001 (ASCII)

#### Colors (Images)
- **RGB**: 24 bits per pixel (8 bits each for Red, Green, Blue)
- **Example**: Pure red = 11111111 00000000 00000000

#### Multimedia
- **Sound**: Binary samples of audio waves
- **Video**: Series of images played rapidly

---

## III. Interactive Activities (15 minutes)

### Binary Conversion Practice (10 minutes)
- **Individual**: Convert small decimal numbers (1-31) to binary
- **Pairs**: Convert binary back to decimal
- **Group Challenge**: Create binary representations for class data (ages, favorite numbers)

### Data Size Estimation Game (5 minutes)
- **Activity**: Estimate file sizes for common items
- **Examples**: Tweet length, photo sizes, music files
- **Reality Check**: Compare estimates with actual sizes

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **All digital data is binary**: Everything stored as 0s and 1s
2. **Bits and bytes are building blocks**: Small units combine for complex data
3. **Binary is electrical**: On/off states represent information
4. **Size matters**: Data grows exponentially with bits

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Convert decimal 13 to binary
2. How many values can 1 byte represent?
3. Name one type of data and how it's stored in binary

### Preview of Next Session (2 minutes)
"Next time we'll explore number systems beyond binary - decimal, hexadecimal, and why we use them!"

---

## Additional Resources
- **Visual Aid**: Binary place value chart
- **Handout**: Data size conversion table
- **Homework**: Find file sizes of 5 items on your computer

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes