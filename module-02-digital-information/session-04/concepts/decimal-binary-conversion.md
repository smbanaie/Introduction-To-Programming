# Decimal-Binary Conversion: Bridging Two Worlds

## The Conversion Challenge

Humans think in decimal (base 10), but computers work in binary (base 2). Converting between these systems is fundamental to understanding how computers represent and process numbers.

## Decimal to Binary Conversion

### Method 1: Repeated Division by 2
**Algorithm**: Divide by 2, keep remainders, read bottom to top

Example: Convert 42₁₀ to binary
```
42 ÷ 2 = 21 remainder 0
21 ÷ 2 = 10 remainder 1
10 ÷ 2 = 5  remainder 0
5 ÷ 2 = 2   remainder 1
2 ÷ 2 = 1   remainder 0
1 ÷ 2 = 0   remainder 1

Remainders (bottom to top): 1 0 1 0 1 0
Binary result: 101010₂
```

### Method 2: Place Value Method
**Algorithm**: Find largest power of 2, subtract, repeat

Example: Convert 42₁₀ to binary
```
32 (2⁵) ≤ 42, so bit 5 = 1, subtract: 42 - 32 = 10
16 (2⁴) > 10, so bit 4 = 0
8 (2³) ≤ 10, so bit 3 = 1, subtract: 10 - 8 = 2
4 (2²) > 2, so bit 2 = 0
2 (2¹) ≤ 2, so bit 1 = 1, subtract: 2 - 2 = 0
1 (2⁰) > 0, so bit 0 = 0

Binary result: 101010₂
```

### Practice Examples
```
13₁₀ = 1101₂     (8+4+1=13)
27₁₀ = 11011₂    (16+8+2+1=27)
64₁₀ = 1000000₂  (64=2⁶)
100₁₀ = 1100100₂ (64+32+4=100)
```

## Binary to Decimal Conversion

### Method: Place Value Expansion
**Algorithm**: Multiply each bit by its place value (power of 2)

Example: Convert 101010₂ to decimal
```
1×2⁵ + 0×2⁴ + 1×2³ + 0×2² + 1×2¹ + 0×2⁰
= 32 + 0 + 8 + 0 + 2 + 0
= 42₁₀
```

### Alternative Method: Doubling
**Algorithm**: Start with 0, double and add each bit

Example: Convert 101010₂ to decimal
```
Start: 0
Bit 5 (1): 0×2 + 1 = 1
Bit 4 (0): 1×2 + 0 = 2
Bit 3 (1): 2×2 + 1 = 5
Bit 2 (0): 5×2 + 0 = 10
Bit 1 (1): 10×2 + 1 = 21
Bit 0 (0): 21×2 + 0 = 42
Result: 42₁₀
```

### Practice Examples
```
1101₂ = 13₁₀    (8+4+1=13)
11011₂ = 27₁₀   (16+8+2+1=27)
1000000₂ = 64₁₀ (64=2⁶)
1100100₂ = 100₁₀ (64+32+4=100)
```

## Working with Different Bit Sizes

### 4-Bit Binary (Nibble)
```
0000₂ = 0₁₀
0101₂ = 5₁₀
1010₂ = 10₁₀
1111₂ = 15₁₀
```

### 8-Bit Binary (Byte)
```
00000000₂ = 0₁₀
01010101₂ = 85₁₀
10101010₂ = 170₁₀
11111111₂ = 255₁₀
```

### 16-Bit Binary (Word)
```
0000000000000000₂ = 0₁₀
1000000000000000₂ = 32768₁₀
1111111111111111₂ = 65535₁₀
```

## Fractional Numbers

### Binary Fractions
Binary can represent fractions using negative powers of 2:

```
0.1₂ = 1×2⁻¹ = 0.5₁₀
0.01₂ = 1×2⁻² = 0.25₁₀
0.11₂ = 1×2⁻¹ + 1×2⁻² = 0.75₁₀
```

### Converting Decimal Fractions
Example: Convert 0.625₁₀ to binary
```
0.625 × 2 = 1.25 → 1, remainder 0.25
0.25 × 2 = 0.5   → 0, remainder 0.5
0.5 × 2 = 1.0    → 1, remainder 0.0

Binary: 0.101₂
```

## Signed Numbers

### Sign-Magnitude Representation
Leftmost bit represents sign:
- 0 = positive, 1 = negative
- Example: +5 = 0101, -5 = 1101

### Two's Complement (Standard)
Modern computers use two's complement:
- Positive: normal binary
- Negative: invert all bits, add 1

Example: -5 in 4-bit two's complement
```
5 = 0101₂
Invert: 1010₂
Add 1: 1011₂ = -5
```

## Hexadecimal as Bridge

### Binary ↔ Hex Conversion
4 binary bits = 1 hex digit:
```
1010 1111 0010 1100₂ = AF2C₁₆
```

### Decimal ↔ Hex via Binary
```
42₁₀ = 101010₂ = 2A₁₆
255₁₀ = 11111111₂ = FF₁₆
```

## Programming Examples

### Python Conversion Functions
```python
# Built-in functions
bin(42)    # '0b101010'  (decimal to binary)
int('101010', 2)  # 42        (binary to decimal)
hex(42)    # '0x2a'      (decimal to hex)
int('2a', 16)  # 42        (hex to decimal)
```

### Manual Conversion Functions
```python
def decimal_to_binary(n):
    """Convert decimal to binary string."""
    if n == 0:
        return '0'
    binary = ''
    while n > 0:
        binary = str(n % 2) + binary
        n = n // 2
    return binary

def binary_to_decimal(binary_str):
    """Convert binary string to decimal."""
    decimal = 0
    for i, bit in enumerate(reversed(binary_str)):
        if bit == '1':
            decimal += 2 ** i
    return decimal
```

## Common Conversion Patterns

### Powers of 2
```
2⁰ = 1₁₀ = 1₂
2¹ = 2₁₀ = 10₂
2² = 4₁₀ = 100₂
2³ = 8₁₀ = 1000₂
2⁴ = 16₁₀ = 10000₂
```

### Round Numbers
```
10₁₀ = 1010₂
20₁₀ = 10100₂
50₁₀ = 110010₂
100₁₀ = 1100100₂
```

### Bit Patterns
```
Even numbers: end with 0
Odd numbers: end with 1
Powers of 2: single 1, rest 0s
```

## Applications

### Computer Memory
```
Address 1024₁₀ = 10000000000₂
Address 4096₁₀ = 10000000000000₂
```

### Network Addresses
```
IP: 192.168.1.1
Binary: 11000000.10101000.00000001.00000001
```

### Color Values
```
Red: 255₁₀ = 11111111₂
Green: 128₁₀ = 10000000₂
Blue: 0₁₀ = 00000000₂
```

## Key Takeaways

1. **Repeated division**: Decimal to binary conversion method
2. **Place value expansion**: Binary to decimal conversion method
3. **Practice required**: Conversion becomes easier with practice
4. **Bit size matters**: Different applications use different bit widths
5. **Hexadecimal helps**: Provides compact binary representation

## Practice Exercises

### Easy Conversions
```
5₁₀ = ?₂     101₂ = ?₁₀
10₁₀ = ?₂    111₂ = ?₁₀
16₁₀ = ?₂    10000₂ = ?₁₀
```

### Medium Conversions
```
25₁₀ = ?₂    11001₂ = ?₁₀
50₁₀ = ?₂    110010₂ = ?₁₀
100₁₀ = ?₂   1100100₂ = ?₁₀
```

### Advanced Conversions
```
Fraction: 0.5₁₀ = ?₂
Negative: -8₁₀ = ?₂ (8-bit two's complement)
Hex: 2A₁₆ = ?₁₀ = ?₂
```

## Further Reading
- Study binary arithmetic and overflow conditions
- Learn about floating-point binary representation
- Explore binary-coded decimal (BCD) systems
- Understand one's complement and two's complement