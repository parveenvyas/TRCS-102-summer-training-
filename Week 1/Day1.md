## 📅 Summer Training - Daily Diary: Day 1

### 1. Python Basics & Variables

Today, I learned about variables, printing formats, and how Python manages memory.

* **F-strings:** Used for clean string formatting.
* **`id()` function:** Returns the unique memory address of an object.
* **Dynamic Typing:** Python automatically determines the data type of a variable based on the value assigned to it, and this can change dynamically.

```python
x = 43
print(x)                          # Prints the value: 43
print("x")                        # Prints the literal string: x
print(f"{x} is a number")         # F-string output

# Checking memory address
print(f"Memory address of x (id): {id(x)}")

# Demonstrating dynamic typing
my_var = 100
print(type(my_var))               # Output: <class 'int'>

my_var = "Now I am a string!"
print(type(my_var))               # Output: <class 'str'>

```

---

### 2. Built-in Data Types

### 2.1 Numeric Types

Python supports integers, floating-point numbers, and complex numbers.

* **Mutability Note:** Numeric types are **immutable** (their value cannot be changed in place; a new memory block is allocated instead).

```python
my_int = -10
my_float = 3.14159
my_complex = 2 + 3j

print(type(my_int))     # <class 'int'>
print(type(my_float))   # <class 'float'>
print(type(my_complex)) # <class 'complex'>

# Accessing real and imaginary parts of a complex number
print(my_complex.real, my_complex.imag) 

```

### 2.2 Text / String Type

Strings can be enclosed in single or double quotes.

```python
single_line = "Hi, I am Parveen"
multi_line = "I am Parveen. I am currently doing B.Tech in CSE from GNDEC."

print(single_line)
print(multi_line)

```

### 2.3 Boolean and None Type

* **Boolean:** Represents logical values: `True` or `False`.
* **NoneType:** Represents the absence of a value (`None`).

```python
it_is_raining = True
has_passed = False
empty_value = None

print(type(it_is_raining)) # <class 'bool'>
print(type(has_passed))    # <class 'bool'>
print(type(empty_value))   # <class 'NoneType'>

```

### 2.4 Type Casting (Changing Data Types)

We can explicitly convert one data type into another.

```python
num = 10
print(type(num))   # <class 'int'>

num = float(num)   # Converting int to float
print(type(num))   # <class 'float'>

```

---

### 3. Operators & Control Flow

### 3.1 Arithmetic Operators

Used to perform standard mathematical operations:

* `+` (Addition) : Returns the sum
* `-` (Subtraction) : Returns the difference
* `/` (Division) : Divide
* `//` (Floor Division): Divides and rounds down to the nearest whole integer.
* `%` (Modulus): Returns the remainder of a division.
* `` (Exponentiation): Power operator.

```python
a = 14
b = 8

print(f"Sum of a and b = {a + b}")
print(f"Difference of a and b = {a - b}")
print(f"Division: {a / b}")
print(f"Floor Division: {a // b}")
print(f"Remainder (Modulus): {a % b}")
print(f"Power: {a ** b}")

```

#### 🛠️ Practical Practice: Student Percentage Calculator

```python
eng = int(input("English: "))
hind = int(input("Hindi: "))
math = int(input("Math: "))
pun = int(input("Punjabi: "))
science = int(input("Science: "))

total_marks = eng + hind + math + pun + science
percentage = (total_marks * 100) / 500

print("Percentage:", percentage)

```

### 3.2 Comparison / Relational Operators

Used to compare two values. They always return a Boolean (`True` or `False`).

```python
x = int(input("X: "))
y = int(input("Y: "))

print("x == y:", x == y)
print("x != y:", x != y)

```

### 3.3 Logical Operators

Used to combine conditional statements:

* `and`: Returns `True` if **both** conditions are true.
* `or`: Returns `True` if **at least one** condition is true.
* `not`: Reverses the Boolean value.

```python
is_sunny = True
is_weekend = False

print(is_sunny and is_weekend) # False
print(is_sunny or is_weekend)  # True
print(not is_sunny)            # False

```

#### 🛠️ Practical Practice: Finding the Greatest of Three Numbers

```python
x = int(input("x: "))
y = int(input("y: "))
z = int(input("z: "))

if x > y and x > z:
    print("x is the greatest")
elif y > x and y > z:
    print("y is the greatest")
else:
    print("z is the greatest")

```

### 3.4 Assignment Operators

Used to assign values to variables, often combining an operation with an assignment shorthand (e.g., `x += 3` is equivalent to `x = x + 3`).

```python
num = 10

num += 5   # num = 10 + 5 -> 15
print(num)

num *= 2   # num = 15 * 2 -> 30
print(num)

num //= 3  # num = 30 // 3 -> 10
print(num)

```
