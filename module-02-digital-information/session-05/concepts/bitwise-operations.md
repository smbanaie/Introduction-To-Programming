# Bitwise Operations: Manipulating Data at the Binary Level

## What Are Bitwise Operations?

Bitwise operations work on individual bits of binary numbers. They treat each bit as a separate switch that can be on (1) or off (0), allowing for powerful and efficient data manipulation.

## Basic Bitwise Operations

### AND (&)
Sets a bit to 1 only if both input bits are 1:
```
  1010  (10)
& 1100  (12)
------
  1000  (8)
```

**Truth table:**
- 0 & 0 = 0
- 0 & 1 = 0
- 1 & 0 = 0
- 1 & 1 = 1

### OR (|)
Sets a bit to 1 if either input bit is 1:
```
  1010  (10)
| 1100  (12)
------
  1110  (14)
```

**Truth table:**
- 0 | 0 = 0
- 0 | 1 = 1
- 1 | 0 = 1
- 1 | 1 = 1

### XOR (^)
Sets a bit to 1 if the input bits are different:
```
  1010  (10)
^ 1100  (12)
------
  0110  (6)
```

**Truth table:**
- 0 ^ 0 = 0
- 0 ^ 1 = 1
- 1 ^ 0 = 1
- 1 ^ 1 = 0

### NOT (~)
Flips all bits (one's complement):
```
~1010 = 0101 (in 4 bits)
```

**Note:** In two's complement systems, ~x = -x - 1

## Shift Operations

### Left Shift (<<)
Moves bits to the left, fills with zeros:
```
5 << 1 = 10  (101 → 1010)
5 << 2 = 20  (101 → 10100)
```

**Effect:** Multiplication by powers of 2

### Right Shift (>>)
Moves bits to the right, loses rightmost bits:
```
10 >> 1 = 5   (1010 → 101)
20 >> 2 = 5   (10100 → 101)
```

**Effect:** Division by powers of 2 (integer division)

### Arithmetic vs Logical Shift
- **Logical shift**: Always fills with zeros
- **Arithmetic shift**: Preserves sign bit for negative numbers

## Practical Applications

### Setting Bits
```python
# Set bit 2 (third bit from right)
flags = flags | (1 << 2)

# Set multiple bits
mask = (1 << 3) | (1 << 5) | (1 << 7)  # Bits 3, 5, 7
flags = flags | mask
```

### Clearing Bits
```python
# Clear bit 2
flags = flags & ~(1 << 2)

# Clear multiple bits
mask = (1 << 3) | (1 << 5) | (1 << 7)
flags = flags & ~mask
```

### Checking Bits
```python
# Check if bit 2 is set
if (flags & (1 << 2)) != 0:
    print("Bit 2 is set")

# Check if any of multiple bits are set
mask = (1 << 3) | (1 << 5)
if (flags & mask) != 0:
    print("At least one of bits 3 or 5 is set")
```

### Toggling Bits
```python
# Toggle bit 2
flags = flags ^ (1 << 2)

# Toggle multiple bits
mask = (1 << 3) | (1 << 5)
flags = flags ^ mask
```

## Advanced Techniques

### Bit Masks
Predefined patterns for common operations:
```python
# Extract lower 4 bits
value & 0x0F

# Extract bits 4-7
(value >> 4) & 0x0F

# Set bits 4-7 to specific value
value = (value & ~0xF0) | ((new_value << 4) & 0xF0)
```

### Bit Fields
Packing multiple small values into one integer:
```python
# Pack 3 values: red(5 bits), green(6 bits), blue(5 bits)
color = (red << 11) | (green << 5) | blue

# Extract values
red = (color >> 11) & 0x1F
green = (color >> 5) & 0x3F
blue = color & 0x1F
```

### Efficient Computations

#### Fast Multiplication/Division by Powers of 2
```python
# Instead of x * 8
result = x << 3

# Instead of x / 16
result = x >> 4
```

#### Checking Even/Odd
```python
# Even numbers end with 0
if (number & 1) == 0:
    print("Even")

# Odd numbers end with 1
if (number & 1) == 1:
    print("Odd")
```

#### Power of 2 Check
```python
# Power of 2 numbers have exactly one bit set
if (number & (number - 1)) == 0 and number > 0:
    print("Power of 2")
```

## Bit Manipulation Algorithms

### Count Set Bits
```python
def count_bits(n):
    """Count number of 1 bits in binary representation."""
    count = 0
    while n:
        count += n & 1  # Add least significant bit
        n >>= 1         # Shift right
    return count

# More efficient method
def count_bits_fast(n):
    """Count bits using bit manipulation."""
    count = 0
    while n:
        n &= n - 1  # Clear least significant set bit
        count += 1
    return count
```

### Find First Set Bit
```python
def lowest_set_bit(n):
    """Find position of lowest set bit (0-based)."""
    if n == 0:
        return -1
    return (n & -n).bit_length() - 1
```

### Bit Reversal
```python
def reverse_bits(n, bit_length=8):
    """Reverse bits in a number."""
    result = 0
    for i in range(bit_length):
        result = (result << 1) | (n & 1)
        n >>= 1
    return result
```

### Gray Code Conversion
```python
def binary_to_gray(n):
    """Convert binary to Gray code."""
    return n ^ (n >> 1)

def gray_to_binary(n):
    """Convert Gray code to binary."""
    mask = n
    while mask:
        mask >>= 1
        n ^= mask
    return n
```

## Hardware Implementation

### Logic Gates
Digital circuits implement bitwise operations:
- **AND gate**: Implements &
- **OR gate**: Implements |
- **XOR gate**: Implements ^
- **NOT gate**: Implements ~

### ALU Operations
Arithmetic Logic Unit performs:
- **Bitwise operations**: AND, OR, XOR, NOT
- **Shift operations**: Left/right shifts
- **Arithmetic**: Using bitwise operations as building blocks

### SIMD Instructions
Single Instruction, Multiple Data:
```asm
; Process 16 bytes simultaneously
pand xmm0, xmm1    ; 16 AND operations
por xmm0, xmm1     ; 16 OR operations
pxor xmm0, xmm1    ; 16 XOR operations
```

## Cryptography Applications

### XOR Cipher
Simple encryption using XOR:
```python
def xor_encrypt(plaintext, key):
    """Simple XOR encryption."""
    return bytes([p ^ k for p, k in zip(plaintext, key)])

# Encrypt and decrypt
key = b'secret'
encrypted = xor_encrypt(b'hello', key)
decrypted = xor_encrypt(encrypted, key)  # Same function decrypts
```

### Hash Functions
Bit operations create diffusion:
```python
# Simplified hash function
def simple_hash(data):
    hash_value = 0
    for byte in data:
        hash_value = ((hash_value << 5) + hash_value) ^ byte  # hash * 33 ^ byte
    return hash_value
```

## Performance Benefits

### Memory Efficiency
- **Bit flags**: Store 32 boolean values in one integer
- **Bit sets**: Efficient set operations
- **Bloom filters**: Space-efficient approximate membership

### Speed Advantages
- **No branches**: Bit operations avoid conditional jumps
- **Parallel processing**: Multiple bits processed simultaneously
- **Cache friendly**: Compact data structures

## Programming Language Support

### Python Bitwise Operators
```python
# Basic operations
a & b   # AND
a | b   # OR
a ^ b   # XOR
~a      # NOT
a << n  # Left shift
a >> n  # Right shift
```

### C/C++ Bitwise Operators
```c
// Same operators as Python
int result = a & b;
int shifted = value << 3;
```

### Java Bitwise Operators
```java
// Same operators
int result = a & b;
int shifted = value >>> 3;  // Unsigned right shift
```

## Common Pitfalls

### Signed vs Unsigned Issues
```python
# In Python (arbitrary precision)
-1 >> 1  # -1 (arithmetic shift preserves sign)

# In C (fixed width, undefined behavior for negative shifts)
```

### Endianness Considerations
```python
# Bit operations are endianness-independent
# But multi-byte values may need byte swapping on different architectures
```

### Overflow Handling
```python
# Python handles arbitrary precision
large_number = 1 << 1000  # Works fine

# C/C++ may overflow silently
```

## Real-World Examples

### Network Protocols
```
TCP flags: 8 bits for control information
  CWR | ECE | URG | ACK | PSH | RST | SYN | FIN
```

### File Permissions
```
Unix permissions: 9 bits (3×3)
  Owner: rwx (111)
  Group: r-x (101)
  Other: --x (001)
```

### Graphics
```
Alpha blending: Combine pixels with bitwise operations
Color masks: Extract RGBA components
```

## Key Takeaways

1. **Bitwise operations manipulate individual bits**: AND, OR, XOR, NOT provide fundamental operations
2. **Shift operations enable fast math**: Multiplication/division by powers of 2
3. **Bit masks control multiple flags**: Efficient boolean operations
4. **Cryptography relies on bit operations**: XOR for encryption, diffusion for security
5. **Performance benefits**: Faster, more memory-efficient than byte-level operations

## Further Reading
- Study digital logic and circuit design
- Learn cryptography and hash function design
- Explore compression algorithms
- Understand error-correcting codes