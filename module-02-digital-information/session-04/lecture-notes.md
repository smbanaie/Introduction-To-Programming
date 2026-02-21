# Session 4: Number Systems

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will understand multiple number systems and their conversions
**Materials**: Whiteboard, base conversion charts, number system comparison table

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How many values can 1 byte represent?
- **Hook Activity**: Count to 10 using fingers, then demonstrate counting to 10 in binary using fingers
- **Question**: "Why do programmers use different number systems?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Understand decimal, binary, and hexadecimal systems
- Convert between different number bases
- Explain why hexadecimal is useful for programmers
- Apply number systems to real programming scenarios

### Agenda Overview (5 minutes)
1. Understanding different bases
2. Decimal and binary review
3. Hexadecimal system
4. Conversion techniques and applications

---

## II. Main Content (50 minutes)

### A. Number Base Fundamentals (15 minutes)

#### What is a Base?
- **Base**: How many digits a number system uses
- **Position Value**: Each position represents a power of the base
- **Example**: Decimal (base 10) uses digits 0-9

#### Base Comparison Table

| Number System | Base | Digits Used | Example | Use Case |
|---------------|------|-------------|---------|----------|
| **Decimal** | 10 | 0-9 | 42 | Human counting |
| **Binary** | 2 | 0-1 | 101010 | Computer storage |
| **Hexadecimal** | 16 | 0-9, A-F | 2A | Memory addresses |

#### Position Value Concept
```
For any base B:  d₂ d₁ d₀ . d₋₁ d₋₂  =  d₂×B² + d₁×B¹ + d₀×B⁰ + d₋₁×B⁻¹ + d₋₂×B⁻²

Decimal (42₁₀): 4×10¹ + 2×10⁰ = 40 + 2 = 42
Binary (1010₂):  1×2³ + 0×2² + 1×2¹ + 0×2⁰ = 8 + 0 + 2 + 0 = 10
```

### B. Hexadecimal System (20 minutes)

#### Why Hexadecimal?
- **Binary is verbose**: 8 binary digits = 1 hex digit
- **Memory addresses**: Computers use hex for memory locations
- **Color codes**: Web colors use hex (#FF0000 = red)
- **Compact representation**: Shorter than binary for same information

#### Hexadecimal Digits
```
0-9: Standard digits
A = 10, B = 11, C = 12, D = 13, E = 14, F = 15
```

#### Hex Examples
```
Decimal 15 = Hex F
Decimal 16 = Hex 10
Decimal 255 = Hex FF (8-bit maximum)
Decimal 4096 = Hex 1000
```

#### Binary-Hex Conversion
```
Binary:  1111 1010 1100 1111
Hex:       F    A    C    F

Each 4 binary bits = 1 hex digit
8 binary bits = 2 hex digits (1 byte)
```

### C. Conversion Techniques (15 minutes)

#### Decimal to Binary
- **Method**: Repeated division by 2, keep remainders
- **Example**: Convert 42₁₀ to binary
  ```
  42 ÷ 2 = 21 remainder 0
  21 ÷ 2 = 10 remainder 1
  10 ÷ 2 = 5 remainder 0
  5 ÷ 2 = 2 remainder 1
  2 ÷ 2 = 1 remainder 0
  1 ÷ 2 = 0 remainder 1
  Result: 101010₂ (read remainders bottom to top)
  ```

#### Binary to Hexadecimal
- **Method**: Group binary in 4-bit chunks, convert each to hex
- **Example**: 101010₂ to hex
  ```
  0010 1010₂ = 2A₁₆
  (0010 = 2, 1010 = A)
  ```

#### Hex to Decimal
- **Method**: Expand using place values
- **Example**: 2A₁₆ to decimal
  ```
  2×16¹ + A×16⁰ = 2×16 + 10×1 = 32 + 10 = 42₁₀
  ```

---

## III. Interactive Activities (15 minutes)

### Base Conversion Relay (10 minutes)
- **Team Activity**: Divide class into teams
- **Challenge**: Convert numbers between bases
- **Examples**: Decimal ↔ Binary ↔ Hexadecimal
- **Scoring**: Fastest accurate team wins

### Real-World Applications (5 minutes)
- **Memory addresses**: Show hex memory locations
- **Color picker**: Demonstrate hex color codes
- **File permissions**: Unix style (rwxr-xr-x)

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Multiple bases serve different purposes**: Decimal for humans, binary for computers, hex for programmers
2. **Hexadecimal compresses binary**: 4 bits = 1 hex digit
3. **Conversion follows patterns**: Position values and grouping rules
4. **Context matters**: Choose the right base for the task

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Convert binary 1010 to hexadecimal
2. Why do programmers prefer hex over binary for memory addresses?
3. Convert hex 1F to decimal

### Preview of Next Session (2 minutes)
"Next time we'll learn binary arithmetic - how computers add, subtract, multiply, and divide!"

---

## Additional Resources
- **Visual Aid**: Number base conversion flowchart
- **Handout**: Hexadecimal digit reference
- **Homework**: Convert your house number to binary and hex

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes