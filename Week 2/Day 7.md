# 📅 Summer Training - Daily Diary: Day 7

## 1. Advanced NumPy: Random Sampling & Distributions

In Machine Learning, random number generation is essential for initializing neural network weights, splitting datasets, and introducing stochastic variations in algorithms.

### 1.1 Uniform vs. Standard Normal Distributions

* **`np.random.rand(rows, cols)`**: Generates values uniformly distributed over the interval $[0, 1)$.


* **`np.random.randn(rows, cols)`**: Generates values from a Standard Normal Distribution (Mean = 0, Variance = 1). This is heavily utilized when initializing weights in deep learning neural networks.



```python
import numpy as np

# 1. Uniform Distribution (values strictly between 0 and 1)
uniform_arr = np.random.rand(2, 3)
print("Uniform Distribution Array:\n", uniform_arr)

# 2. Standard Normal Distribution (Mean = 0, Std Dev = 1)
normal_arr = np.random.randn(3, 2)
print("\nStandard Normal Distribution Array:\n", normal_arr)

```

---

## 2. Practical Algorithmic Coding Challenges

### Exercise 2.1: Label Frequency Counter Function

Creating an optimized function to count categorical occurrences (e.g., medical diagnoses).

```python
labels = ["tumor", "healthy", "tumor", "cyst", "tumor", "healthy"]

def count_frequencies(labels):
    count = {}
    for label in labels:
        if label not in count:
            count[label] = 1
        else:
            count[label] += 1
    return count

frequency_map = count_frequencies(labels)
print("Class Frequencies:", frequency_map)
# Output: {'tumor': 3, 'healthy': 2, 'cyst': 1}

```

### Exercise 2.2: Prime Range Generator

Creating helper functions to calculate and filter prime numbers within a specified numerical range.

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

def get_primes_in_range(start, end):
    return [n for n in range(start, end + 1) if is_prime(n)]

print("Primes between 10 and 50:\n", get_primes_in_range(10, 50))
# Output: [11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]

```

### Exercise 2.3: Recursive Power Function ($a^b$)

Solving exponential multiplication recursively by breaking the exponent down to a base case.

```python
def recursive_power(base, exponent):
    if exponent == 0:  # Base Case
        return 1
    else:               # Recursive Case
        return base * recursive_power(base, exponent - 1)

print("3^4 = ", recursive_power(3, 4)) # Output: 81

```


### Exercise 2.4: Recursive Sum of Digits

Extracting individual digits sequentially using floor division (`//`) and modulus (`%`) operations.

```python
def sum_of_digits(n):
    if n < 10:          # Base case: single-digit number
        return n
    else:               # Recursive case: last digit + sum of remaining
        return (n % 10) + sum_of_digits(n // 10)

print("Sum of digits for 12345:", sum_of_digits(12345)) # Output: 15

```
---

## 3. Evaluation Metrics in Machine Learning

Calculating performance metrics using vectorized NumPy operations.

### 3.1 Precision & Recall

* **True Positive (TP):** Model predicts positive (`1`), actual is positive (`1`).


* **False Positive (FP):** Model predicts positive (`1`), actual is negative (`0`).


* **False Negative (FN):** Model predicts negative (`0`), actual is positive (`1`).



$$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$$

$$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$$

```python
def calculate_precision_recall(actual, predicted):
    # Vectorized binary comparisons using boolean logic (&)
    TP = np.sum((actual == 1) & (predicted == 1))
    FP = np.sum((actual == 0) & (predicted == 1))
    FN = np.sum((actual == 1) & (predicted == 0))
    
    precision = TP / (TP + FP) if (TP + FP) > 0 else 0
    recall = TP / (TP + FN) if (TP + FN) > 0 else 0
    
    return precision, recall

actual    = np.array([1, 0, 1, 1, 0])
predicted = np.array([1, 1, 1, 0, 0])

precision, recall = calculate_precision_recall(actual, predicted)
print(f"Precision: {precision:.4f}") # Output: 0.6667
print(f"Recall:    {recall:.4f}")    # Output: 0.6667

```
