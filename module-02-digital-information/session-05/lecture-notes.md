# Session 5: Binary Arithmetic

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will understand how computers perform mathematical operations
**Materials**: Whiteboard, binary addition/subtraction charts, carry-over demonstration cards

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: Convert hex 2A to decimal
- **Hook Question**: "How does a computer add 2 + 2 when it only knows 0s and 1s?"
- **Demonstration**: Show binary addition with visual aids

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Perform binary addition and subtraction
- Understand carry and borrow operations
- Apply binary arithmetic to computer operations
- Explain overflow and underflow concepts

### Agenda Overview (5 minutes)
1. Binary addition fundamentals
2. Binary subtraction and borrowing
3. Multiplication and division concepts
4. Computer arithmetic limitations

---

## II. Main Content (50 minutes)

### A. Binary Addition (20 minutes)

#### Basic Rules
```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 0 (carry 1)
```

#### Addition with Carrying
```
Example: Add 5 + 3
  5 = 0101₂
  3 = 0011₂
      0101
    + 0011
    ------
      1000₂ = 8₁₀ ✓
```

#### Multi-bit Addition
```
  1 1 1 1  (carries)
    1 0 1 0  (10₂)
  + 0 1 1 1  (7₂)
  ---------
  1 0 0 0 1  (17₂)
```

#### Visual Carry Demonstration
```
Step-by-step: 1 + 1 + 1
Position 1: 1 + 1 = 0, carry 1
Position 2: 1 + 0 + 1(carry) = 0, carry 1
Position 3: 0 + 0 + 1(carry) = 1, carry 0
Result: 011₂ (but with carry would be 100₂)
```

### B. Binary Subtraction (15 minutes)

#### Basic Rules
```
0 - 0 = 0
1 - 0 = 1
1 - 1 = 0
0 - 1 = 1 (borrow 1)
```

#### Subtraction with Borrowing
```
Example: Subtract 3 - 1
  3 = 0011₂
  1 = 0001₂
      0011
    - 0001
    ------
      0010₂ = 2₁₀ ✓
```

#### Complex Subtraction
```
  1 0 0 0  (borrows)
    1 0 1 0  (10₂)
  - 0 0 1 1  (3₂)
  ---------
    0 1 1 1  (7₂)
```

### C. Advanced Operations (15 minutes)

#### Multiplication by Powers of 2
- **Left shift**: Multiply by 2 (add 0 on right)
- **Right shift**: Divide by 2 (remove rightmost bit)
- **Examples**:
  ```
  5₂ × 2 = 1010₂ (shift left)
  10₂ ÷ 2 = 101₂ (shift right)
  ```

#### Two's Complement (Negative Numbers)
- **Method**: Flip all bits and add 1
- **Example**: Represent -3
  ```
  3 = 0011₂
  Flip: 1100₂
  Add 1: 1101₂ (-3 in two's complement)
  ```

#### Overflow and Underflow
- **Overflow**: Result too large for bit space
- **Underflow**: Result too small for bit space
- **Example**: 4-bit addition: 15 + 1 = 0 (with overflow)

---

## III. Interactive Activities (15 minutes)

### Binary Calculator Game (10 minutes)
- **Pairs**: Students add binary numbers using cards
- **Challenge**: Race to solve addition problems
- **Extension**: Include subtraction and negative numbers

### Real Computer Scenarios (5 minutes)
- **Memory addresses**: Adding offsets
- **Color mixing**: RGB value calculations
- **Game scores**: Point arithmetic

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Binary arithmetic follows simple rules**: Addition and subtraction use carry/borrow
2. **Computers use binary for all math**: Foundation of all calculations
3. **Shifting enables fast multiplication/division**: Hardware-optimized operations
4. **Overflow creates challenges**: Bit limitations affect results

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. Add binary 101 + 011
2. Subtract binary 100 - 001
3. What happens when you add 1111₂ + 0001₂ in 4 bits?

### Preview of Next Session (2 minutes)
"Next time we'll explore how text and characters are represented in binary!"

---

## Additional Resources
- **Visual Aid**: Binary arithmetic rules chart
- **Handout**: Two's complement worksheet
- **Homework**: Calculate binary sums for decimal 1-20

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes