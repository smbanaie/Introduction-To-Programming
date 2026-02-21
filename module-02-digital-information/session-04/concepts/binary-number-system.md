# Binary Number System: How Computers Count

## Why Binary?

Computers are electrical machines that work with two states: on and off, high voltage and low voltage. This fundamental electrical nature determines why computers use the binary number system - a system with only two digits: 0 and 1.

## Understanding Number Systems

### Decimal (Base 10)
Our everyday number system:
- **Digits**: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- **Base**: 10
- **Place values**: 10⁰, 10¹, 10², 10³...
- **Example**: 42 = 4×10¹ + 2×10⁰

### Binary (Base 2)
The computer's number system:
- **Digits**: 0, 1
- **Base**: 2
- **Place values**: 2⁰, 2¹, 2², 2³...
- **Example**: 1010₂ = 1×2³ + 0×2² + 1×2¹ + 0×2⁰ = 8 + 2 = 10

## Binary Place Values

### Powers of 2
Each position represents a power of 2:
```
2⁰ = 1
2¹ = 2
2² = 4
2³ = 8
2⁴ = 16
2⁵ = 32
2⁶ = 64
2⁷ = 128
2⁸ = 256
```

### Reading Binary Numbers
```
Binary:  1  0  1  0  1  0  1  0
Places: 128 64 32 16 8  4  2  1
Value:  128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170
```

## Converting Between Decimal and Binary

### Decimal to Binary
**Method**: Repeated division by 2

Example: Convert 42 to binary
```
42 ÷ 2 = 21 remainder 0
21 ÷ 2 = 10 remainder 1
10 ÷ 2 = 5  remainder 0
5 ÷ 2 = 2   remainder 1
2 ÷ 2 = 1   remainder 0
1 ÷ 2 = 0   remainder 1

Read remainders bottom to top: 101010₂
```

### Binary to Decimal
**Method**: Multiply each bit by its place value

Example: Convert 101010₂ to decimal
```
1×32 + 0×16 + 1×8 + 0×4 + 1×2 + 0×1 = 32 + 8 + 2 = 42
```

## Binary Arithmetic

### Addition
Rules:
- 0 + 0 = 0
- 0 + 1 = 1
- 1 + 0 = 1
- 1 + 1 = 0 (carry 1)

Example:
```
  1 1 1  (carries)
    1 0 1  (5)
  + 0 1 1  (3)
  -------
  1 0 0 0  (8)
```

### Subtraction
Rules:
- 0 - 0 = 0
- 1 - 0 = 1
- 1 - 1 = 0
- 0 - 1 = 1 (borrow 1)

Example:
```
  1 0  (borrows)
    1 0 1  (5)
  - 0 0 1  (1)
  -------
    0 1 0  (4)
```

### Multiplication
Same as decimal, but only 0s and 1s:
```
    1 0 1  (5)
  × 0 1 1  (3)
  -------
    1 0 1
  1 0 1
----------
  1 1 1 1  (15)
```

## Binary in Computer Architecture

### Data Sizes
```
1 bit = smallest unit
1 byte = 8 bits = 256 possible values
1 word = 32 or 64 bits (processor dependent)
```

### Memory Addressing
Each memory location has a binary address:
```
Address 0: 00000000
Address 1: 00000001
Address 255: 11111111
```

### Data Types
Different types need different bit patterns:
```
Boolean: 1 bit (true/false)
Byte: 8 bits (0-255)
Integer: 32 bits (-2 billion to +2 billion)
Float: 32 bits (decimal numbers)
```

## Hexadecimal: Binary's Friend

### Why Hexadecimal?
Binary numbers get long quickly. Hexadecimal (base 16) provides a compact representation:
- **Digits**: 0-9, A-F (A=10, B=11, C=12, D=13, E=14, F=15)
- **Conversion**: 4 binary bits = 1 hex digit

### Binary-Hex Conversion
```
Binary:  1111 1010 1100 1111
Hex:       F    A    C    F
```

### Memory Addresses
Hex is commonly used for memory addresses:
```
Address 0x1000 = 0001000000000000 in binary
Address 0xFFFF = 1111111111111111 in binary
```

## Binary Logic Operations

### Bitwise Operations
Computers perform logic on individual bits:

#### AND (&)
```
  1010
& 1100
------
  1000
```

#### OR (|)
```
  1010
| 1100
------
  1110
```

#### XOR (^)
```
  1010
^ 1100
------
  0110
```

### Applications
- **Graphics**: Color manipulation
- **Networking**: Error checking
- **Security**: Encryption algorithms
- **Compression**: Data encoding

## Signed Binary Numbers

### Sign-Magnitude
Leftmost bit represents sign:
- 0 = positive, 1 = negative
- Example: +5 = 0101, -5 = 1101

### Two's Complement (Modern Standard)
- Positive numbers: normal binary
- Negative numbers: invert all bits and add 1
- Example: -5 = 11111011 (invert 00000101 to 11111010, add 1)

## Floating Point Binary

### IEEE 754 Standard
32-bit float format:
- **Sign**: 1 bit
- **Exponent**: 8 bits (biased by 127)
- **Mantissa**: 23 bits

### Example: 3.14
```
Sign: 0 (positive)
Exponent: 10000000 (128 - 127 = 1)
Mantissa: 10010001111010111000011
Result: 1.570796... × 2¹ = 3.141592...
```

## Practical Applications

### Computer Graphics
```
Color RGB: Each component 0-255 (8 bits)
Pixel: 24 bits total (8+8+8)
Image: width × height × 24 bits
```

### Networking
```
IP Address: 32 bits (4 bytes)
MAC Address: 48 bits (6 bytes)
Port Numbers: 16 bits (0-65535)
```

### File Systems
```
Permissions: 9 bits (rwx for owner/group/others)
File size: 64 bits (up to 18 exabytes)
Timestamps: 64 bits (nanosecond precision)
```

## Common Binary Patterns

### Powers of 2
```
2⁰ = 1        = 0001
2¹ = 2        = 0010
2² = 4        = 0100
2³ = 8        = 1000
2⁴ = 16       = 00010000
```

### Bit Masks
```
Check bit 3: 00001000 (8)
Set bit 2:   00000100 (4)
Clear bit 1: 11111101 (253)
```

## Key Takeaways

1. **Binary matches computer hardware**: Electrical on/off states
2. **Place values determine magnitude**: Each position is a power of 2
3. **Conversion requires practice**: Decimal ↔ binary conversion
4. **Arithmetic works the same**: Just with different rules
5. **Hex makes binary manageable**: Compact representation for humans

## Common Mistakes

### Leading Zeros
- **Wrong**: 0010₂ = 2₁₀
- **Right**: 0010₂ = 2₁₀ (leading zeros don't change value)

### Bit Order
- **Wrong**: Reading right to left
- **Right**: Leftmost bit has highest place value

### Overflow
- **Problem**: 8-bit addition of 255 + 1 = 0 (with carry)
- **Solution**: Use larger data types to prevent overflow

## Further Reading
- Study binary arithmetic in detail
- Learn about different integer representations (signed/unsigned)
- Explore floating-point arithmetic and precision issues
- Understand binary-coded decimal (BCD) systems