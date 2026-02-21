# Binary Multiplication and Division: Advanced Binary Operations

## Binary Multiplication

### Basic Multiplication
Binary multiplication follows the same rules as decimal, but with only 0s and 1s:

```
    1 0 1  (5 in decimal)
  × 0 1 1  (3 in decimal)
  -------
    1 0 1  (5 × 1)
  1 0 1    (5 × 1, shifted left)
----------
  1 1 1 1  (15 in decimal)
```

### Multiplication Algorithm
1. **Partial products**: Multiply by each bit of multiplier
2. **Shifting**: Shift left for each position
3. **Addition**: Sum all partial products

### Booth's Algorithm
Advanced method for signed multiplication:
- Reduces number of additions needed
- Handles negative numbers efficiently
- Used in hardware multipliers

## Binary Division

### Division Algorithm
Similar to decimal long division:

```
   1 0  (quotient)
--------
1 1 | 1 0 1 0  (divisor = 3, dividend = 10)
     1 1      (3 × 1 = 3)
     ---
      1 1 0   (bring down next bit)
    - 1 1     (3 × 1 = 3)
      ---
        1 0   (remainder = 2)
```

### Restoring Division
Standard hardware division method:
1. **Compare**: Shift remainder left, compare with divisor
2. **Subtract**: If remainder ≥ divisor, subtract and set quotient bit
3. **Restore**: If remainder < 0, restore and clear quotient bit
4. **Repeat**: Continue until all bits processed

### Non-Restoring Division
Optimized version that avoids restoration steps.

## Shift and Add Algorithms

### Russian Peasant Multiplication
Ancient method that works perfectly in binary:
1. **Double the left number, halve the right** (integer division)
2. **Add left number to total when right number is odd**
3. **Repeat until right number becomes 1**

Example: 13 × 11
```
13  11  odd → add 13, total = 13
26   5  odd → add 26, total = 39
52   2 even → skip
104  1  odd → add 104, total = 143
```

### Binary Implementation
This is exactly how computers multiply!

## Fast Multiplication Techniques

### Karatsuba Algorithm
Divide and conquer approach:
- Split numbers into halves
- Compute three multiplications instead of four
- Reconstruct result

### FFT-based Multiplication
Using Fast Fourier Transform for very large numbers:
- Transform to frequency domain
- Multiply in frequency domain
- Transform back to get result

## Hardware Multipliers

### Array Multiplier
Simple but slow:
- AND gates for each bit combination
- Adders for each row
- Ripple carry between stages

### Wallace Tree Multiplier
Faster implementation:
- Carry-save adders reduce latency
- Tree structure allows parallel computation
- More complex but much faster

### Booth Multiplier
Signed multiplication:
- Detects runs of 1s for efficiency
- Reduces partial products needed
- Standard in modern CPUs

## Division Hardware

### SRT Division
Fast radix-2 division:
- Estimates quotient digits
- Uses lookup tables
- Iterative refinement

### Newton-Raphson Division
Uses multiplication for division:
- Converts division to multiplication problem
- Uses Newton's method for convergence
- Very fast for floating point

## Floating Point Operations

### IEEE 754 Arithmetic
Special handling for floating point:
- **Addition**: Align exponents, add mantissas
- **Multiplication**: Add exponents, multiply mantissas
- **Division**: Subtract exponents, divide mantissas

### Precision Issues
Floating point has limited precision:
- **Guard digits**: Extra bits for rounding
- **Rounding modes**: Different ways to handle precision loss
- **Exception handling**: Overflow, underflow, NaN

## Modular Arithmetic

### Clock Arithmetic
Numbers wrap around at modulus:
```
7 mod 3 = 1 (7 ÷ 3 = 2*3 + 1)
```

### Applications
- **Cryptography**: RSA, Diffie-Hellman
- **Hash functions**: Distribute values evenly
- **Error detection**: Checksums, CRC

### Binary Modular Operations
```
Multiplication mod 2ⁿ: AND with mask
Division mod 2ⁿ: Right shift
```

## Bit Manipulation Tricks

### Power of 2 Tests
```python
# Check if power of 2
if (n & (n-1)) == 0 and n > 0:
    print("Power of 2")

# Find next power of 2
next_pow2 = 1 << (n-1).bit_length()
```

### Bit Counting
```python
# Count set bits
def count_bits(n):
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count

# Fast method
def fast_count_bits(n):
    count = 0
    while n:
        n &= n - 1  # Clear least significant set bit
        count += 1
    return count
```

### Bit Reversal
```python
# Reverse bits in a byte
def reverse_bits(n):
    result = 0
    for i in range(8):
        result = (result << 1) | (n & 1)
        n >>= 1
    return result
```

## Computer Arithmetic Instructions

### x86 Assembly Examples
```asm
; Addition
add eax, ebx    ; EAX = EAX + EBX

; Subtraction
sub eax, ebx    ; EAX = EAX - EBX

; Multiplication
imul eax, ebx   ; EAX = EAX * EBX (signed)

; Division
idiv ebx        ; EAX = EDX:EAX / EBX (signed)
```

### SIMD Instructions
Single Instruction, Multiple Data:
```asm
; Add 4 pairs of numbers simultaneously
paddd xmm0, xmm1  ; 4 × 32-bit additions
```

## Performance Considerations

### Operation Costs
```
Addition: 1 cycle
Multiplication: 3-10 cycles
Division: 10-50 cycles
```

### Optimization Techniques
- **Strength reduction**: Replace expensive operations with cheaper ones
- **Constant folding**: Compute constants at compile time
- **Loop unrolling**: Reduce loop overhead
- **Vectorization**: Use SIMD instructions

## Arbitrary Precision Arithmetic

### Big Integer Libraries
For numbers larger than built-in types:
- **Java**: BigInteger class
- **Python**: Automatic arbitrary precision
- **C++**: Boost multiprecision library

### Applications
- **Cryptography**: Large prime numbers
- **Scientific computing**: High precision calculations
- **Financial calculations**: Exact decimal arithmetic

## Error Analysis

### Round-off Errors
Floating point precision limitations:
- **Accumulated errors**: Small errors compound
- **Cancellation**: Subtracting similar numbers loses precision
- **Ill-conditioned problems**: Input errors amplify

### Mitigation Strategies
- **Mixed precision**: Use double precision for critical calculations
- **Stable algorithms**: Rearrange computations to minimize errors
- **Interval arithmetic**: Track error bounds

## Key Takeaways

1. **Binary multiplication uses shift and add**: Efficient for hardware implementation
2. **Division is more complex**: Requires iterative algorithms
3. **Hardware optimizations improve speed**: Specialized circuits for arithmetic
4. **Bit manipulation enables clever tricks**: Efficient algorithms for common operations
5. **Precision limits affect calculations**: Understanding floating point behavior is crucial

## Common Algorithms

### Extended Euclidean Algorithm
For finding GCD and modular inverses:
```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    gcd, x1, y1 = extended_gcd(b, a % b)
    x = y1
    y = x1 - (a // b) * y1
    return gcd, x, y
```

### Montgomery Multiplication
Fast modular multiplication for cryptography:
- Avoids expensive division operations
- Used in RSA and ECC implementations
- Critical for secure communications

## Further Reading
- Study computer arithmetic textbooks
- Learn about cryptography algorithms
- Explore high-performance computing techniques
- Understand quantum computing arithmetic