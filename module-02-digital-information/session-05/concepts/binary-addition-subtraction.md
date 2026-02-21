# Binary Addition and Subtraction: How Computers Do Math

## Binary Addition

### Basic Rules
Computers add binary numbers using simple rules:
- 0 + 0 = 0
- 0 + 1 = 1
- 1 + 0 = 1
- 1 + 1 = 0 (carry 1 to next position)

### Addition Example
```
  1 1 1  (carry bits)
    1 0 1  (5 in decimal)
  + 0 1 1  (3 in decimal)
  -------
  1 0 0 0  (8 in decimal)
```

**Step by step:**
1. Rightmost: 1 + 1 = 0, carry 1
2. Middle: 0 + 1 + 1(carry) = 0, carry 1
3. Leftmost: 1 + 0 + 1(carry) = 0, carry 1
4. Final carry: 1 (extends number)

### Multi-byte Addition
```
   1111  (15)
 + 0001  (1)
 -------
 10000  (16)
```

## Binary Subtraction

### Basic Rules
- 0 - 0 = 0
- 1 - 0 = 1
- 1 - 1 = 0
- 0 - 1 = 1 (borrow 1 from next position)

### Subtraction Example
```
  1 0  (borrow bits)
    1 0 1  (5 in decimal)
  - 0 0 1  (1 in decimal)
  -------
    0 1 0  (4 in decimal)
```

**Step by step:**
1. Rightmost: 1 - 1 = 0
2. Middle: 0 - 0 = 0
3. Leftmost: 1 - 0 = 1

### Subtraction with Borrowing
```
  1 1 0  (borrow bits)
    1 0 0  (4 in decimal)
  - 0 1 1  (3 in decimal)
  -------
    0 0 1  (1 in decimal)
```

## Two's Complement Subtraction

### Modern Method
Computers use two's complement for efficient subtraction:
1. Convert subtrahend to negative (two's complement)
2. Add the numbers
3. Result is correct

### Two's Complement Steps
To negate a number:
1. Invert all bits (one's complement)
2. Add 1

### Example: 5 - 3
```
5 in binary:  0101
3 in binary:  0011
3 negated:   1101 (invert 0011 = 1100, add 1 = 1101)

  0101  (5)
+ 1101  (-3)
------
10010  (2, ignore carry)
```

## Overflow and Underflow

### Addition Overflow
When result is too large for bit width:
```
4-bit addition: 8 + 8
  1000  (8)
+ 1000  (8)
------
 10000  (16, but only 4 bits available)
Result: 0000 (overflow!)
```

### Subtraction Underflow
When result is too small for signed representation:
```
4-bit subtraction: -8 - 1
  1000  (-8)
- 0001  (1)
------
  0111  (7, but should be -9)
Result: 0111 (underflow!)
```

## Carry and Borrow Flags

### CPU Flags
Modern CPUs track operation results:
- **Carry Flag**: Set when addition produces carry
- **Borrow Flag**: Set when subtraction needs borrow
- **Zero Flag**: Set when result is zero
- **Overflow Flag**: Set when signed overflow occurs

### Flag Usage
```
Addition: 255 + 1 (8-bit)
Result: 0, Carry Flag = 1 (overflow occurred)

Subtraction: 0 - 1 (8-bit)
Result: 255, Borrow Flag = 1 (underflow occurred)
```

## Binary Multiplication

### Basic Multiplication
Same as decimal, but simpler:
```
    101  (5)
  × 011  (3)
  ------
    101
  101
------
  1111  (15)
```

### Shift and Add Method
Computers multiply by shifting and adding:
```
5 × 3 = 5 × (2¹ + 2⁰) = 5×2 + 5×1 = 10 + 5 = 15

In binary:
  101 × 011 = 101 × (010 + 001) = (101×10) + (101×01) = 1010 + 0101 = 1111
```

## Binary Division

### Division Algorithm
Similar to decimal long division:
```
  10  (quotient)
------
101 | 1010  (dividend)
     101   (multiply quotient by divisor)
     ---
      010  (remainder, bring down next bit)
```

### Integer Division
```
10 ÷ 3 = 3 remainder 1
In binary:
1010 ÷ 11 = 11 remainder 01
```

## Bitwise Operations

### Logical Operations
```
AND (&): 1 only if both bits are 1
OR (|): 1 if either bit is 1
XOR (^): 1 if bits are different
NOT (~): Flip the bit
```

### Examples
```
  1010  (10)
& 1100  (12)
------
  1000  (8)

  1010  (10)
| 1100  (12)
------
  1110  (14)

  1010  (10)
^ 1100  (12)
------
  0110  (6)
```

## Shift Operations

### Left Shift (<<)
Move bits left, fill with zeros:
```
5 << 1 = 1010 (10)  // 5 × 2
5 << 2 = 10100 (20) // 5 × 4
```

### Right Shift (>>)
Move bits right, lose rightmost bits:
```
10 >> 1 = 101 (5)   // 10 ÷ 2
20 >> 2 = 101 (5)   // 20 ÷ 4
```

### Arithmetic vs Logical Shift
- **Logical**: Fill with zeros
- **Arithmetic**: Preserve sign bit

## Floating Point Arithmetic

### IEEE 754 Format
32-bit float: sign(1) + exponent(8) + mantissa(23)

### Special Values
- **Zero**: All bits zero
- **Infinity**: Exponent all 1s, mantissa zero
- **NaN**: Exponent all 1s, mantissa non-zero

### Precision Limits
Floating point has limited precision:
```
0.1 + 0.2 = 0.30000000000000004 (not exactly 0.3!)
```

## Computer Implementation

### ALU (Arithmetic Logic Unit)
The CPU component that performs calculations:
- **Adder**: For addition/subtraction
- **Shifter**: For multiplication/division by powers of 2
- **Logic Unit**: For bitwise operations
- **Flags**: Status indicators

### Pipeline Execution
Modern CPUs execute multiple operations simultaneously:
1. **Fetch**: Get instruction from memory
2. **Decode**: Interpret the instruction
3. **Execute**: Perform the calculation
4. **Store**: Save the result

## Programming Examples

### Python Bitwise Operations
```python
# Bitwise AND
result = 10 & 12  # 8 (1010 & 1100 = 1000)

# Bitwise OR
result = 10 | 12  # 14 (1010 | 1100 = 1110)

# Bitwise XOR
result = 10 ^ 12  # 6 (1010 ^ 1100 = 0110)

# Left shift
result = 5 << 1   # 10 (101 << 1 = 1010)

# Right shift
result = 10 >> 1  # 5 (1010 >> 1 = 101)
```

### Checking Bits
```python
# Check if number is even
if (number & 1) == 0:
    print("Even")

# Check if bit 3 is set
if (number & (1 << 3)) != 0:
    print("Bit 3 is set")
```

## Key Takeaways

1. **Binary arithmetic uses simple rules**: Addition and subtraction with carry/borrow
2. **Two's complement enables efficient subtraction**: Convert to addition problem
3. **Overflow occurs when results exceed bit width**: Important for error handling
4. **Bitwise operations enable efficient computations**: Direct bit manipulation
5. **Shift operations provide fast multiplication/division**: By powers of 2

## Common Pitfalls

### Ignoring Overflow
```python
# 8-bit addition
255 + 1 = 0 (with overflow)
```

### Signed vs Unsigned Confusion
```python
# 8-bit: 10000000
# Signed: -128
# Unsigned: 128
```

### Floating Point Precision
```python
# Never test floating point equality
if abs(a - b) < 0.0001:  # Use epsilon comparison
    print("Approximately equal")
```

## Further Reading
- Study computer architecture and ALU design
- Learn about floating-point arithmetic standards
- Explore arbitrary-precision arithmetic libraries
- Understand saturation arithmetic for embedded systems