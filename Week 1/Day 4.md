
# 📅 Summer Training - Daily Diary: Day 4

## 1. Types of Functional Arguments

Python allows different ways to pass arguments to a function based on position, names, or default configurations.

### 1.1 Positional, Keyword, and Default Arguments

* **Positional:** Arguments must be passed in the exact sequential order of the parameters.
* **Keyword:** Arguments are explicitly assigned using parameter names (`key=value`), making the order irrelevant.
* **Default:** Parameters are pre-assigned a value in the definition. If the caller omits them, the default value is used.

```python
def intro(name, age=18, course='12th'):
    print(f"{name} is {age} years old, studying in {course} class.")

# 1. Positional Arguments (Order matters)
intro("Sahil", 17, "11th")

# 2. Keyword Arguments (Order does not matter)
intro(course="9th", name="Sakshi", age=15)

# 3. Default Arguments (Omitting optional inputs defaults to age=18, course='12th')
intro("Priya") 

```

### 1.2 Variable-Length Arguments (`*args` and `kwargs`)

Used when the total number of arguments passed into the function is unknown beforehand.

* `*args`: Receives an arbitrary number of positional arguments as a **Tuple**.
* `kwargs`: Receives an arbitrary number of keyword arguments as a **Dictionary**.

```python
# *args Example: Collecting multiple numerical expense inputs
def cal_total_expenses(*expenses):
    print(f"Expenses received: {expenses} (Type: {type(expenses)})")
    return sum(expenses)

total = cal_total_expenses(12.5, 45.0, 100.25, 7.8)
print(f"Total Expenses: {total}\n")


# **kwargs Example: Collecting dynamically passed model hyperparameters
def print_model_parameters(**hyperparam):
    print(f"Hyperparameters received: {hyperparam} (Type: {type(hyperparam)})")
    for key, value in hyperparam.items():
        print(f"  - {key}: {value}")

print_model_parameters(learning_rate=0.001, batch_size=64, dropout=0.3)

```

---

## 2. Variable Scope and the `global` Keyword

* **Local Variables:** Created inside a function and accessible only within that function's block.
* **Global Variables:** Declared outside functions, accessible across the entire script.

```python
metric_name = "accuracy" # Global variable

def evaluate():
    score = 0.95         # Local variable
    print(f"Inside function: {metric_name} score is {score}")

evaluate()
print(f"Outside function: {metric_name}")

```

### Modifying Global Variables (The `global` Keyword)

To modify a global variable inside a local scope, you must explicitly declare it with the `global` keyword. Otherwise, Python simply creates a new local variable with the same name.

```python
a = 10 # Global variable

def change():
    global a # Pointing to the global variable
    a = 20
    print("Inside function (after modification):", a)

change()
print("Outside function (original global value altered):", a) # Output: 20

```

---

## 3. Recursive Functions

A recursive function is a function that calls itself to solve smaller instances of the same problem. It requires:

1. **Base Case:** A conditional exit branch that stops the recursion.
2. **Recursive Case:** The logical step where the function calls itself.

### 3.1 Factorial Calculation ($n!$)

```python
def calculate_factorial(n):
    if n == 0 or n == 1: # Base Case
        return 1
    else:                # Recursive Case
        return n * calculate_factorial(n - 1)

print("Factorial of 5:", calculate_factorial(5))
print("Factorial of 6:", calculate_factorial(6))

```

### 3.2 Fibonacci Sequence

An exercise to generate the sequence where each number is the sum of the preceding two values ($F_n = F_{n-1} + F_{n-2}$).

```python
def fibonacci(n):
    if n == 0:          # Base Case 1
        return 0
    elif n == 1:        # Base Case 2
        return 1
    else:               # Recursive Case
        return fibonacci(n - 1) + fibonacci(n - 2)

print("Fibonacci series up to index 5:")
for i in range(6):
    print(fibonacci(i), end=" ")
print()

```

---

## 4. Data Structures: Lists

Today, I explored lists—ordered, mutable collections in Python—and mastered their key operation mechanics.

### 4.1 Built-in List Methods

| Method | Description | Example |
| --- | --- | --- |
| `append(item)` | Adds a single element to the very end of the list. | `list1.append(70)` |
| `extend(iterable)` | Merges elements from another list/iterable into the current list. | `list1.extend(list2)` |
| `insert(index, item)` | Inserts an item at a specific target position index. | `list1.insert(1, "New")` |
| `remove(item)` | Deletes the first occurrence of a specific value. | `list1.remove(-99.0)` |
| `pop(index)` | Removes and returns the item at a given index (defaults to last item). | `list1.pop(0)` |

```python
list1 = [10, 20, 30, 40]
list2 = [10, 20, 30]

print(f"Data type: {type(list1)}")

# Append vs Extend
list1.append(70)
print("After append(70):", list1)

list1.extend(list2)
print("After extend(list2):", list1)

```

### 4.2 List Slicing & Sorting

Slicing allows you to access portions of a list using index syntax: `list[start:stop:step]`. Sorting can be done in-place using `.sort()` or non-destructively using `sorted()`.

```python
# Slicing example
my_list = [0, 1, 2, 3, 4, 5]
print("Slice [1:4]:", my_list[1:4]) # Elements at indices 1, 2, 3

```

---

## 5. Practical Data Applications with Lists

### 5.1 Applying Reductions (10% Tax Calculation)

```python
salary = [20000, 50000, 40000, 10000, 15000]
salary.sort(reverse=True) # Sorting data downward
print("Sorted Salaries:", salary)

# Deducting a 10% tax from each entry
for i in range(len(salary)):
    salary[i] -= salary[i] * 0.1

print("Updated Salaries (10% Tax Deducted):", salary)

```

### 5.2 Data Cleaning: Filtering Out Missing Values / Noise

A core requirement in machine learning dataset preprocessing is scrubbing placeholder data or noise values (e.g., `-99.0`).

```python
# Method A: Using a loop with while + .remove()
predictions = [0.15, -99.0, 0.82, 1.45, -99.0, -0.67, 2.1]
outlier = -99.0
while outlier in predictions:
    predictions.remove(outlier)
print("Scrubbed list (Method A):", predictions)

# Method B: Filtering into a fresh collection array (List Comprehension)
predictions = [0.15, -99.0, 0.82, 1.45, -99.0, -0.67, 2.1]
cleaned_list = [i for i in predictions if i != -99.0]
print("Scrubbed list (Method B):", cleaned_list)

```

### 5.3 Algorithmic Coding Challenge: The Two-Sum Problem

Finding unique pairs from an array that sum up to a specific targeted value.

```python
# Approach 1: Nested Loops (Brute Force - O(n²) time complexity)
list1 = [1, 8, 10, 10, 8, 8, 3, 5]
pairs = []
target = int(input("Enter targeted number: "))

for i in range(len(list1)):
    for j in range(i + 1, len(list1)):
        if list1[i] + list1[j] == target:
            pair = tuple(sorted((list1[i], list1[j])))
            if pair not in pairs:
                pairs.append(pair)
print("Unique pairs found (Brute Force):", pairs)


# Approach 2: Tracking Visited Elements (Optimized Lookups)
list1 = [1, 8, 10, 10, 8, 8, 3, 5]
target_val = 11  # Example tracking pair sum to 11
visited = []
result = []

for i in list1:
    diff = target_val - i
    if diff in visited:
        result.append((i, diff))
        visited.remove(diff) # Avoid duplicate combinations
    else:
        visited.append(i)
print("Targeted pairs matching 11 (Optimized):", result)

```

---
