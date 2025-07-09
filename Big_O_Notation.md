# Big O Notation - Complete Guide

## What is Big O?

Big O answers one simple question: **"If I double my input size, how much more work does my algorithm do?"**

It's NOT about exact timing - it's about how performance scales with input size.

## The Core Concept

Think of Big O as describing the **relationship** between input size and work required:

- **O(1)**: Same work regardless of input size
- **O(n)**: Double input = double work  
- **O(n²)**: Double input = 4× work
- **O(log n)**: Double input = one extra step

## Common Big O Complexities (Best to Worst)

### O(1) - Constant Time
**"Same work every time"**

```python
def get_first_item(arr):
    return arr[0]  # Always 1 operation
```

**Examples:**
- Accessing array element by index: `arr[5]`
- Getting size of array: `len(arr)` 
- Hash table lookup: `dict[key]`

**Real world:** Opening a book to page 50. Same effort whether it's a 100-page or 1000-page book.

### O(log n) - Logarithmic Time
**"Double the input, add one more step"**

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Examples:**
- Binary search in sorted array
- Finding item in balanced binary search tree
- Some divide-and-conquer algorithms

**Real world:** Guessing a number 1-1000. Each guess eliminates half the possibilities.

### O(n) - Linear Time
**"Double the input, double the work"**

```python
def find_max(arr):
    max_val = arr[0]
    for item in arr[1:]:
        if item > max_val:
            max_val = item
    return max_val
```

**Examples:**
- Finding maximum value in unsorted array
- Printing all elements
- Linear search
- Single loop through data

**Real world:** Reading every page of a book to find a quote.

### O(n log n) - Linearithmic Time
**"Efficient sorting algorithms"**

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)
```

**Examples:**
- Merge sort
- Heap sort
- Quick sort (average case)
- Many efficient sorting algorithms

**Real world:** Organizing a deck of cards using an efficient method.

### O(n²) - Quadratic Time
**"Double the input, quadruple the work"**

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
```

**Examples:**
- Bubble sort, selection sort
- Nested loops over same data
- Comparing every pair of items

**Real world:** Comparing every person in a room with every other person.

### O(2ⁿ) - Exponential Time
**"Double the input, square the work"**

```python
def fibonacci_naive(n):
    if n <= 1:
        return n
    return fibonacci_naive(n-1) + fibonacci_naive(n-2)
```

**Examples:**
- Naive recursive algorithms
- Brute force solutions
- Some backtracking algorithms

**Real world:** Checking every possible combination of a password.

## Visual Comparison

|Input Size:  |   1  |  10  |  100 | 1,000 | 10,000 |
|------------ |------|------|------|-------|--------|
|O(1):     |     1   |  1   |  1   |   1   |    1   |
|O(log n):  |    1   |  3   |  7   |  10   |   13   |
|O(n):      |    1   |  10  |  100 | 1,000 |  10,000 |
|O(n log n):  |  1   |  33  |  664 |  9,966 | 132,877 |
|O(n²):    |     1   |  100 | 10,000 | 1,000,000 | 100,000,000 |
|O(2ⁿ):     |    2    | 1,024  |  2¹⁰⁰  |  2¹⁰⁰⁰  |  2¹⁰⁰⁰⁰ |

**Notice how dramatically they diverge!**

## Why Constants and Lower Terms Don't Matter

**These are all O(n):**
- `n` operations
- `5n` operations  
- `n + 100` operations
- `3n + 50` operations

**Why?** For large inputs, the growth pattern is the same:

```
n = 1,000:     5n = 5,000      vs    n² = 1,000,000
n = 10,000:    5n = 50,000     vs    n² = 100,000,000
```

The constant factor becomes irrelevant compared to the growth rate.

## Space Complexity

Big O also describes memory usage:

```python
def create_matrix(n):
    matrix = []
    for i in range(n):
        row = []
        for j in range(n):
            row.append(i * j)
        matrix.append(row)
    return matrix
```

**Time complexity:** O(n²) - nested loops
**Space complexity:** O(n²) - creating n×n matrix

## Best, Average, and Worst Case

**Example: Linear Search**
```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
```

- **Best case:** O(1) - target is first element
- **Average case:** O(n) - target is in the middle
- **Worst case:** O(n) - target not found

**When we say "linear search is O(n)", we usually mean worst case.**

## Common Patterns and Their Big O

### Single Loop
```python
for i in range(n):
    print(i)
```
**O(n)**

### Nested Loops
```python
for i in range(n):
    for j in range(n):
        print(i, j)
```
**O(n²)**

### Dividing Problem in Half
```python
while n > 1:
    n = n // 2
    print(n)
```
**O(log n)**

### Recursive Calls
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```
**O(n)** - makes n recursive calls

## Algorithm Comparison Example

**Problem:** Find duplicates in an array

**Approach 1: Nested loops**
```python
def find_duplicates_nested(arr):
    duplicates = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j]:
                duplicates.append(arr[i])
    return duplicates
```
**Time:** O(n²), **Space:** O(k) where k is number of duplicates

**Approach 2: Hash set**
```python
def find_duplicates_hash(arr):
    seen = set()
    duplicates = []
    for num in arr:
        if num in seen:
            duplicates.append(num)
        seen.add(num)
    return duplicates
```
**Time:** O(n), **Space:** O(n)

**For 1,000 elements:**
- Approach 1: ~1,000,000 operations
- Approach 2: ~1,000 operations

## Common Mistakes

### Mistake 1: Thinking O(n) is always better than O(n²)
**Reality:** For small inputs, O(n²) might be faster due to simpler operations.

### Mistake 2: Ignoring space complexity
**Reality:** Sometimes you trade time for space or vice versa.

### Mistake 3: Premature optimization
**Reality:** O(n²) might be fine for your use case. Profile first, optimize later.

### Mistake 4: Thinking Big O gives exact running time
**Reality:** Big O shows growth rate, not exact performance.

## When Big O Matters

**Big O is crucial when:**
- Working with large datasets
- Performance is critical
- Comparing algorithm alternatives
- Planning for scale

**Big O matters less when:**
- Working with small, fixed datasets
- Simplicity is more important than performance
- The algorithm runs infrequently

## Quick Reference

| Complexity | Name | Example |
|------------|------|---------|
| O(1) | Constant | Array access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Linear search |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Bubble sort |
| O(2ⁿ) | Exponential | Naive fibonacci |

## Key Takeaways

1. **Big O describes scalability, not speed**
2. **Focus on growth rate, not exact operations**
3. **Usually consider worst-case scenario**
4. **Constants and lower terms don't matter for large inputs**
5. **Use Big O to compare algorithms and make informed decisions**
6. **Consider both time and space complexity**

## Practice Questions

1. What's the Big O of accessing the middle element of an array?
2. What's the Big O of printing all pairs of elements in an array?
3. If an algorithm takes 5n + 100 operations, what's its Big O?
4. Why is binary search O(log n) instead of O(n)?
5. What's the space complexity of storing all substrings of a string?

**Remember:** Big O helps you predict how your code will behave as data grows. It's about making informed decisions.