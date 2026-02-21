# Algorithm Analysis: Measuring Performance and Efficiency

## Why Analyze Algorithms?

Different algorithms solve the same problem with different efficiency. Algorithm analysis helps us understand and compare performance characteristics before implementation.

## Time Complexity Analysis

### Big O Notation

**Definition**: Describes how algorithm performance grows as input size increases.

**Focus**: Worst-case asymptotic behavior (as input size approaches infinity).

**Common Complexities:**

| Complexity | Name | Example | Description |
|------------|------|---------|-------------|
| O(1) | Constant | Array access | Same time regardless of input size |
| O(log n) | Logarithmic | Binary search | Time doubles when input size doubles |
| O(n) | Linear | Linear search | Time proportional to input size |
| O(n log n) | Linearithmic | Merge sort | n × log n operations |
| O(n²) | Quadratic | Bubble sort | Time proportional to square of input size |
| O(2ⁿ) | Exponential | Subset generation | Time doubles for each additional input element |
| O(n!) | Factorial | Traveling salesman (brute force) | Extremely slow growth |

### Analyzing Basic Operations

```python
# O(1) - Constant time
def access_array_element(arr, index):
    return arr[index]  # Always takes same time

# O(n) - Linear time
def find_maximum(arr):
    max_val = arr[0]
    for num in arr:        # Loop runs n times
        if num > max_val:
            max_val = num
    return max_val

# O(n²) - Quadratic time
def bubble_sort(arr):
    for i in range(len(arr)):      # n times
        for j in range(len(arr)-1): # n times
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
```

### Analyzing Function Calls

```python
# O(n) - Single loop
def linear_search(arr, target):
    for item in arr:  # O(n)
        if item == target:
            return True
    return False

# O(n²) - Nested loops
def has_duplicates(arr):
    for i in range(len(arr)):      # O(n)
        for j in range(i+1, len(arr)):  # O(n)
            if arr[i] == arr[j]:
                return True
    return False

# O(log n) - Divide and conquer
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:  # O(log n) iterations
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

### Recursive Analysis

```python
# O(2ⁿ) - Exponential
def fibonacci_bad(n):
    if n <= 1:
        return n
    return fibonacci_bad(n-1) + fibonacci_bad(n-2)  # Two recursive calls

# O(n) - Linear with memoization
def fibonacci_good(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_good(n-1, memo) + fibonacci_good(n-2, memo)
    return memo[n]
```

## Space Complexity Analysis

### Space Complexity Definition

**Definition**: How much additional memory an algorithm uses relative to input size.

### Examples

```python
# O(1) - Constant space
def sum_array(arr):
    total = 0        # O(1) variables
    for num in arr:  # O(1) additional space
        total += num
    return total

# O(n) - Linear space
def copy_array(arr):
    copy = []         # O(n) space for copy
    for item in arr:
        copy.append(item)
    return copy

# O(n²) - Quadratic space
def create_matrix(n):
    matrix = []       # O(n²) space
    for i in range(n):
        row = []
        for j in range(n):
            row.append(0)
        matrix.append(row)
    return matrix
```

### In-Place Algorithms

```python
# O(1) extra space - in-place
def reverse_array(arr):
    left, right = 0, len(arr) - 1
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]  # Swap in place
        left += 1
        right -= 1
    # No additional space allocated

# O(n) space - not in-place
def reverse_array_copy(arr):
    result = []                    # O(n) additional space
    for i in range(len(arr)-1, -1, -1):
        result.append(arr[i])
    return result
```

## Best, Average, and Worst Case Analysis

### Understanding Different Cases

```python
# Linear search - different cases
def linear_search(arr, target):
    for i, item in enumerate(arr):
        if item == target:
            return i
    return -1

# Best case: O(1) - target is first element
# Average case: O(n) - target is in middle
# Worst case: O(n) - target not found or last element
```

### Binary Search Cases

```python
# Binary search is always O(log n) in all cases
# Best case: O(1) - target is middle element
# Average case: O(log n)
# Worst case: O(log n) - target not found
```

### Sorting Algorithms Cases

```python
# Bubble sort
# Best case: O(n) - already sorted
# Average case: O(n²)
# Worst case: O(n²) - reverse sorted

# Quick sort
# Best case: O(n log n) - balanced partitions
# Average case: O(n log n)
# Worst case: O(n²) - already sorted or reverse sorted
```

## Amortized Analysis

### Definition
**Amortized analysis**: Average performance over a sequence of operations, even if individual operations are expensive.

### Example: Dynamic Arrays

```python
class DynamicArray:
    def __init__(self):
        self.capacity = 1
        self.size = 0
        self.arr = [None] * self.capacity

    def append(self, value):
        if self.size == self.capacity:
            # Double capacity - O(n) operation
            self.capacity *= 2
            new_arr = [None] * self.capacity
            for i in range(self.size):
                new_arr[i] = self.arr[i]
            self.arr = new_arr

        self.arr[self.size] = value
        self.size += 1

# Individual append: O(1) amortized, O(n) worst case
# Sequence of n appends: O(n) total amortized time
```

## Practical Performance Measurement

### Benchmarking

```python
import time

def benchmark_algorithm(algorithm, *args, runs=10):
    times = []
    for _ in range(runs):
        start = time.time()
        result = algorithm(*args)
        end = time.time()
        times.append(end - start)

    avg_time = sum(times) / len(times)
    return avg_time, result

# Compare algorithms
arr = list(range(1000))

linear_time, _ = benchmark_algorithm(linear_search, arr, 999)
binary_time, _ = benchmark_algorithm(binary_search, sorted(arr), 999)

print(f"Linear search: {linear_time:.6f} seconds")
print(f"Binary search: {binary_time:.6f} seconds")
```

### Profiling Tools

```python
import cProfile

def profile_function(func, *args):
    profiler = cProfile.Profile()
    profiler.enable()
    result = func(*args)
    profiler.disable()
    profiler.print_stats(sort='cumulative')
    return result

# Profile a function
result = profile_function(my_algorithm, data)
```

## Comparing Algorithms

### Theoretical vs Practical Performance

```python
# Theoretical: O(n²) vs O(n log n)
# For n=1000:
# O(n²): 1,000,000 operations
# O(n log n): ~10,000 operations

# Practical: Constants matter
# O(n²) with small constant might beat O(n log n) with large constant
# for small n
```

### Choosing the Right Algorithm

**Factors to consider:**
- Input size and constraints
- Required time limits
- Available memory
- Ease of implementation
- Code maintainability

### Algorithm Selection Guide

| Problem Type | Small Input (n<100) | Medium Input (n<10,000) | Large Input (n>10,000) |
|--------------|---------------------|------------------------|----------------------|
| Search | Linear search | Binary search | Hash table |
| Sort | Insertion sort | Merge sort/Quick sort | External sort |
| Shortest path | Floyd-Warshall | Dijkstra | A* with heuristics |
| Matching | Brute force | Dynamic programming | Approximation |

## Common Complexity Classes

### P (Polynomial Time)
Problems solvable in polynomial time: O(n^k) for some constant k.

**Examples:** Sorting, searching, shortest paths in graphs.

### NP (Nondeterministic Polynomial)
Problems where solutions can be verified in polynomial time.

**Examples:** Traveling salesman, knapsack, boolean satisfiability.

### NP-Complete
Hardest problems in NP - if any can be solved in polynomial time, all can.

### NP-Hard
At least as hard as NP-complete problems, may not be in NP.

## Master Theorem for Divide and Conquer

### Formula
For recurrence: T(n) = aT(n/b) + f(n)

**Cases:**
1. If f(n) = O(n^(log_b a - ε)), then T(n) = Θ(n^log_b a)
2. If f(n) = Θ(n^log_b a), then T(n) = Θ(n^log_b a log n)
3. If f(n) = Ω(n^(log_b a + ε)), then T(n) = Θ(f(n))

### Examples

```python
# Merge sort: T(n) = 2T(n/2) + O(n)
# a=2, b=2, f(n)=n
# log_b a = log_2 2 = 1
# f(n) = Θ(n^1) = Θ(n^log_b a)
# Case 2: T(n) = Θ(n log n)

# Binary search tree: T(n) = T(n/2) + O(1)
# a=1, b=2, f(n)=1
# log_b a = log_2 1 = 0
# f(n) = Ω(n^0) = Ω(1)
# Case 3: T(n) = Θ(1)
```

## Performance Optimization Techniques

### Algorithm-Level Optimizations
- Choose better data structures
- Use more efficient algorithms
- Apply algorithmic improvements (memoization, pruning)

### Code-Level Optimizations
- Reduce constant factors
- Minimize memory allocations
- Use vectorized operations
- Employ compiler optimizations

### System-Level Optimizations
- Parallel processing
- Distributed computing
- Hardware acceleration (GPU, FPGA)
- Caching and memory hierarchy optimization

## Key Takeaways

1. **Big O describes growth rate**: Focus on how performance scales with input size
2. **Worst case usually matters**: Design for the most demanding scenarios
3. **Space-time trade-offs**: Sometimes use more memory to save time
4. **Constants can matter**: Theoretical analysis doesn't capture implementation details
5. **Benchmarking validates theory**: Real performance may differ from asymptotic analysis

## Further Reading
- Study "Algorithm Design" by Kleinberg and Tardos
- Learn about advanced analysis techniques (smoothed analysis, parameterized complexity)
- Explore competitive programming and performance optimization
- Understand cache behavior and memory hierarchy effects