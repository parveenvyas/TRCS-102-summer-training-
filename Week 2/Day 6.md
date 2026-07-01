Here is the clean, professional, and beautifully structured Markdown version of your **Day 6** notes on **NumPy Fundamentals**, processed directly from your uploaded notebook. It's ready to be copied and pasted straight into your GitHub training diary!

---

# 📅 Summer Training - Daily Diary: Day 6

## 1. Introduction to NumPy

**NumPy** (Numerical Python) is an open-source library that provides support for large, multi-dimensional arrays and matrices, along with a collection of high-level mathematical functions to operate on them.

### Why NumPy over Standard Python Lists?

While Python lists are flexible because they store mixed data types, this flexibility makes them slow and memory-heavy. NumPy arrays (`ndarray`) solve this by enforcing homogeneity and optimizing memory.

| Feature | Python Lists | NumPy Arrays (`ndarray`) |
| --- | --- | --- |
| **Data Type** | Heterogeneous (mixed types allowed) | Homogeneous (all elements must be the same type) |
| **Memory Layout** | Non-contiguous (pointers scattered in memory) | Contiguous (elements stored right next to each other) |
| **Speed** | Slower (requires type checking & pointer dereferencing) | Extremely fast (processed close to hardware/CPU speeds) |
| **Operations** | Element-wise changes require explicit loops | Supports vectorized operations (no loops needed) |

---

## 2. Creating Arrays & Inspecting Attributes

### 2.1 Array Creation

NumPy arrays can be initialized from standard Python lists or generated using built-in functions.

* `np.array()`: Converts a list or nested list into an `ndarray`.
* `np.zeros(shape)`: Creates an array filled entirely with `0`s.
* `np.ones(shape)`: Creates an array filled entirely with `1`s.
* `np.arange(start, stop, step)`: Generates values within a given range and step size.
* `np.linspace(start, stop, num)`: Generates `num` evenly spaced values over a specified interval.
* `np.eye(n)`: Creates an $n \times n$ identity matrix.

```python
import numpy as np

# Creating 1D and 2D arrays from lists
arr_1d = np.array([10, 20, 40, 50])
matrix_2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# Standard built-in array initializations
zeros = np.zeros((3, 4))        # 3 rows, 4 columns
ones = np.ones((2, 3))          # 2 rows, 3 columns
even_arr = np.arange(0, 100, 2) # Even numbers from 0 to 98
linspace_arr = np.linspace(1, 5, 10)
identity_matrix = np.eye(4)

```

### 2.2 Core Array Attributes

Every `ndarray` possesses specific structural properties:

* `.ndim`: The total number of dimensions (axes).
* `.shape`: A tuple representing the dimensions (rows, columns).
* `.size`: The total count of elements inside the array.
* `.dtype`: The specific data type of the elements (e.g., `int32`, `float64`).
* `.itemsize`: The memory size of a single array element in bytes.

```python
my_matrix = np.array([[1, 2, 3], [4, 5, 6]], dtype=np.int32)

print("Dimensions (ndim):", my_matrix.ndim)     # Output: 2
print("Shape (shape):     ", my_matrix.shape)    # Output: (2, 3)
print("Total size (size):  ", my_matrix.size)     # Output: 6
print("Data Type (dtype):  ", my_matrix.dtype)    # Output: int32
print("Item size (bytes):  ", my_matrix.itemsize) # Output: 4

```

---

## 3. Indexing & Filtering Techniques

### 3.1 1D and 2D Indexing

Standard 1D arrays utilize basic index brackets. Multi-dimensional arrays can be cleanly targeted using comma-separated notation within a single set of brackets: `array[row, column]`.

```python
matrix = np.array([
    [10, 20, 30],
    [40, 50, 60],
    [70, 80, 90]
])

print("Element at row 0, col 1:", matrix[0, 1]) # 20
print("Element at row 2, col 2:", matrix[2, 2]) # 90
print("First row completely:   ", matrix[0, :]) # [10, 20, 30]
print("Second column completely:", matrix[:, 1]) # [20, 50, 80]

```

### 3.2 Boolean Indexing (Masking) 🌟

Boolean masking evaluates logical conditions across entire arrays without structural loops. It produces a logical mask of `True`/`False` entries which is then applied to extract or alter target values.

```python
data = np.array([5, 12, 8, 21, 3, 14, 7])

# Creating and applying a boolean mask
mask = data > 10
filtered_data = data[mask] 
print("Filtered Data:", filtered_data) # [12, 21, 14]

# Modifying elements matching a criteria directly
scores = np.array([45, 65, 30, 85, 92, 40])
scores[scores < 50] = 50 
print("Modified Scores (Baseline 50):", scores) # [50, 65, 50, 85, 92, 50]

```

---

## 4. Slicing: Memory Views vs. Copies ⚠️

Slicing pulls out segments of an array using the `[start:stop:step]` syntax.

> **Crucial Concept:** Unlike standard Python lists where a slice creates a new copy, **NumPy slicing creates a view**. A view simply points to the original array's memory address. Modifying a view **will alter** your original array! To prevent this, you must explicitly use the `.copy()` method.

```python
# The Danger of Views
original = np.array([10, 20, 30, 40, 50])
my_slice = original[1:4]
my_slice[0] = 999
print("Original Array (Mutated by slice!):", original) # [10, 999, 30, 40, 50]

# The Safe Copy Approach
original = np.array([10, 20, 30, 40, 50])
safe_copy = original[1:4].copy()
safe_copy[0] = 999
print("Original Array (Protected & Unchanged):", original) # [10, 20, 30, 40, 50]

```

---

## 5. Broadcasting & Vectorization

### 5.1 Broadcasting Rules

**Broadcasting** allows arithmetic math operations to be performed between arrays of completely different shapes. NumPy virtually "stretches" the smaller array across the larger one to make their dimensions compatible.

Dimensions are checked from **right to left**:

1. Are the dimensions equal?
2. Is one of the dimensions 1?

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
]) # Shape: (2, 3)

vector = np.array([10, 20, 30]) # Shape: (3,)

# Vector broadcasts across the rows of the matrix
result = matrix + vector
print("Broadcast Result:\n", result)
# [[11, 22, 33],
#  [14, 25, 36]]

```

### 5.2 Vectorization Efficiency

Vectorization replaces native Python loops with highly optimized element-wise computations run close to CPU hardware speed.

```python
# Squaring 1,000,000 numbers performance test
numbers = np.arange(1000000)

# Loop implementation: ~50-100ms depending on environment
# %timeit [x ** 2 for x in numbers]

# Vectorized implementation: ~1-2ms (Massively faster!)
# %timeit numbers ** 2

```

---

## 6. Practical Programming Exercises (Self-Solved)

### Exercise 6.1: Celsius to Fahrenheit Vectorized Converter

```python
celsius = np.array([0, 10, 20, 30, 40])
fahrenheit = (celsius * 9/5) + 32
print("Fahrenheit Equivalents:", fahrenheit)

```

### Exercise 6.2: Salary Filtering and Baseline Adjustments

```python
emp_sal = np.array([45000, 78000, 120000, 32000, 95000, 50000])

# Filter salaries >= 60000
high_salary = emp_sal[emp_sal >= 60000]
print("High Salaries:", high_salary)

# Adjust baseline floor to 40000
emp_sal[emp_sal < 40000] = 40000
print("Adjusted Salary Roll:", emp_sal)

```

### Exercise 6.3: Multi-Dimensional Slicing Matrix Challenge

```python
matrix = np.array([
    [5,  6,  7,  8],
    [9,  10, 11, 12],
    [14, 15, 16, 17],
    [18, 19, 20, 21]
])

# 1. Extract the inner 2x2 block
print("Inner 2x2 Block:\n", matrix[1:3, 2:4])

# 2. Extract the third row completely
print("Third Row:", matrix[2, :])

# 3. Extract the first two elements of the last column
print("Partial Last Column:", matrix[0:2, -1])

```

### Exercise 6.4: Safe View Protection Validation

```python
array = np.array([1, 2, 3, 4, 5])
safe_copy = array[0:3].copy()
safe_copy *= 2

print("Modified Copy:", safe_copy) # [2, 4, 6]
print("Original Array (Verified Unchanged):", array) # [1, 2, 3, 4, 5]

```
---
