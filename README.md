
### Daily report 
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


## 📅 Summer Training - Daily Diary: Day 2

### 1. Advanced Operators

### 1.1 Bitwise Operators

Bitwise operators perform operations directly on the binary representations of integers.

* `&` (AND): Sets each bit to `1` if both bits are `1`.
* `|` (OR): Sets each bit to `1` if one of the bits is `1`.
* `^` (XOR): Sets each bit to `1` if only one of the bits is `1` (0 if they are identical).
* `~` (NOT): Inverts all bits. Formula for integers: `~N = -(N + 1)`.
* `<<` (Left Shift): Shifts bits to the left by pushing zeros in from the right.
* `>>` (Right Shift): Shifts bits to the right.

```python
# Bitwise AND, OR, XOR
print("AND of 13 and 8:", 13 & 8) 
print("OR of 13 and 8:", 13 | 8)   
print("XOR of 13 and 8:", 13 ^ 8)  

# Bitwise Shifts
print("Left shift 1 step:", 13 << 1)  # Shifting left multiplies by 2
print("Left shift 2 steps:", 13 << 2) # Shifting left twice multiplies by 4
print("Left shift 3 steps:", 13 << 3)

print("Right shift 1 step:", 13 >> 1) # Shifting right divides by 2 (floor)
print("Right shift 4 steps:", 13 >> 4)

# Bitwise NOT (~N = -(N+1))
print("NOT of 13:", ~13) # Output: -14

```

### 1.2 Membership Operators

Used to test if a sequence (like a list, string, or tuple) contains a specific value.

* `in`: Returns `True` if the value is present.
* `not in`: Returns `True` if the value is not present.

```python
fruits = ["apple", "banana", "Grapes", "mango"]

print("Is 'kiwi' in fruits?", "kiwi" in fruits)
print("Is 'Grapes' in fruits?", "Grapes" in fruits)

```

### 1.3 Identity Operators

Used to compare objects, not just their values. It checks if they point to the exact same location in memory (`id`).

* `is`: Returns `True` if both variables point to the same object.
* `is not`: Returns `True` if variables point to different objects.

> 💡 **Key Difference:** `==` checks if the **values** are equal. `is` checks if the **memory addresses (IDs)** are equal.

```python
list_x = [1, 2, 3, 4]
list_y = [1, 2, 3, 4]

print("Memory address of list_x:", id(list_x))
print("Memory address of list_y:", id(list_y))

print("list_x is list_y:", list_x is list_y)   # False (different addresses)
print("list_x == list_y:", list_x == list_y)   # True (same values)

```

#### 🛠️ Quick Practice: Check Positive and Even

```python
num = 30
print(f"Is {num} positive AND even?")
if num > 0 and num % 2 == 0:
    print("Yes")
else:
    print("No")

```

---

### 2. Loops & Iteration

### 2.1 The `for` Loop and `range()`

The `range(start, stop, step)` function generates a sequence of numbers up to (but not including) the stop value.

```python
# Iterating with steps
for i in range(0, 20, 3):
    print(i, end=" ") # 0 3 6 9 12 15 18
print()

# Printing a math table for 5
for i in range(0, 11):
    print(f"5 X {i}: {5 * i}")

# Iterating over a list
languages = ["python", "SQL", "C++"]
for lang in languages:
    print(f"I am learning: {lang} (Length: {len(lang)} characters)")

# Counting down using a negative step
print("\nCounting down from 10 to 2 (even steps):")
for i in range(10, 0, -2):
    print(i, end=" ")
print()

```

#### 🛠️ Practice: Password Strength Checker

```python
passwords = ["abc123", "hifriend3", "are51", "father#+="]

for pwd in passwords:
    if len(pwd) >= 6:
        print(f"{pwd} is a Strong password")
    else:
        print(f"{pwd} is a Weak password")

```

### 2.2 The `while` Loop

Runs continuously as long as a specified conditional statement remains true.

```python
count = 1
while count <= 3:
    print(f"Count is: {count}")
    count += 1  # Increment to avoid an infinite loop

```

---

### 3. Loop Control Statements

### 3.1 `break` Statement

Terminates the loop entirely and jumps to the code outside the loop block.

```python
for num in range(1, 10):
    if num == 5:
        print(f"Found {num}! Exiting the loop early.")
        break
    print(f"Current number: {num}")
print("End of program!!")

```

### 3.2 `continue` Statement

Skips the rest of the current iteration and jumps directly to the next turn of the loop.

```python
for num in range(1, 10):
    if num == 5:
        print(f"Skipping {num}...")
        continue
    print(f"Current number: {num}")

```

### 3.3 `pass` Statement

A null statement acting as a syntax placeholder when a block of code is required but no logic is written yet.

```python
for num in range(0, 5):
    if num == 3:
        pass  # Will add future logic here
    else:
        print(f"Current number: {num}")

```

### 3.4 `for ... else` Blocks

The `else` block runs **only** if the `for` loop completes naturally without being terminated by a `break` statement.

```python
# Example: Searching for an item
fruits = ["apple", "banana", "orange"]
target = "orange"

for fruit in fruits:
    if fruit == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found in the list.")

```

#### 🛠️ Comprehensive Application: Password Security System

```python
correct_pass = "abc123"

# Simulating 5 maximum attempts
for i in range(1, 6):
    user_input = input(f"Attempt {i}/5 - Enter password: ")
    if user_input == correct_pass:
        print("Access Granted! Successful Login.")
        break
    else:
        print("Wrong password.")
else:
    # Executes only if the loop finishes all 5 attempts without a break
    print("Too many failed attempts. You cannot try again for 30 minutes.")

```

---

### 4. Conditional Control Flow (Age Classification)

Using structured `if-elif-else` branches to group conditions cleanly.

```python
age = int(input("Enter age: "))
print(f"Age is {age}")

if age < 13:
    print("Child")
elif age <= 19:   # Catches ages 13 to 19 inclusive
    print("Teenager")
elif age <= 59:   # Catches ages 20 to 59 inclusive
    print("Adult")
else:
    print("Senior")

```

Excellent! Day 3 covers a highly practical project (the ATM simulator), Python's essential built-in functions, and the fundamentals of user-defined functions (parameters, arguments, and the `return` statement).

There is a minor syntax/logic bug at the very end of your code regarding how you call your `is_prime` function and handle its output. I have refined and fixed that in the structured Markdown below so it's ready for your GitHub repository!

---

# 📅 Summer Training - Daily Diary: Day 3

### 1. ATM Simulator


```python
balance = 10000

while True:
    print("--- Welcome to ATM Simulator ---")
    print("1. Check Balance")
    print("2. Deposit Money")
    print("3. Withdraw Money")
    print("4. Exit")

    choice = int(input("Enter your choice: "))

    if choice == 1:
        print(f"Your balance is: {balance}\n")
    
    elif choice == 2:
        money = int(input("Enter amount to deposit: "))
        balance += money
        print(f"Deposit successful! Your updated balance is: {balance}\n")
        
    elif choice == 3:
        money_withdraw = int(input("Enter amount to withdraw: "))

        # Validation: Check if sufficient funds exist
        if balance >= money_withdraw:
            print("Processing transaction... Your money has been withdrawn.")
            balance -= money_withdraw
        else:
            print("Transaction declined: Insufficient balance.")
        
        print(f"Your available balance is: {balance}\n")
        
    elif choice == 4:
        print("Exiting application. Thank you for using our ATM!")
        break
    else:
        print("Invalid option selected. Please choose a valid option (1-4).\n")

```

---

### 2. Built-in Functions

Python provides highly optimized, built-in functions to handle common actions.

* `len(sequence)`: Returns the total number of items in an iterable or characters in a string.
* `sum(iterable)`: Adds up numerical collections.
* `max(iterable)`: Extracts the largest item.
* `abs(number)`: Returns the absolute value (converts negatives to positive).
* `round(number, digits)`: Rounds off a float to a specified number of decimal points.

```python
list_1 = [1, 2, 3, 4, 8, 10, 41, 12, 13]
string = "Terimerikahani"

print(f"Length of list_1: {len(list_1)}")
print(f"Length of string: {len(string)}")
print(f"Sum of list_1: {sum(list_1)}")
print(f"Maximum value in list_1: {max(list_1)}")

# Demonstrating absolute values
num = -5
print(f"Absolute value of {num} is {abs(num)}")

list1 = [10, -20, 30, -262]
print("Absolute values from list1:", [abs(a) for a in list1])

# Demonstrating round off
num_to_round = 3.14519
print(f"Rounded value (2 decimal places): {round(num_to_round, 2)}")
print(f"Value of Pi (22/7) to 4 decimal places: {round(22/7, 4)}")

```

---

### 3. Functions & Modular Programming

Functions help divide complex applications into smaller, reusable, organized, and modular blocks of code.

### 3.1 Parameters vs. Arguments

* **Parameter:** The placeholder variable listed inside the function definition parentheses.
* **Argument:** The actual data value dispatched to the function when calling it.

```python
# Definition with parameters (username, course)
def greet_user(username, course):
    print(f"Hello, {username}! Ready to train some models? Current course: {course}")

# Invocation with arguments ("Amit123", "Btech")
greet_user("Amit123", "BTech")
greet_user("Sandhya", "IT")

```

#### 🛠️ Practice: Custom Multi-Operation Calculator Function

```python
def cal(a, b, symbol):
    if symbol == "+":
        print(f"Sum of {a} and {b} is {a + b}")
    elif symbol == "-":
        print(f"Difference of {a} and {b} is {a - b}")
    elif symbol == "*":
        print(f"Product of {a} and {b} is {a * b}")
    elif symbol == "/":
        print(f"Division of {a} and {b} is {a / b}")

cal(12, 13, "+")
cal(12, 25, "*")

```

### 3.2 The `return` Statement

The `return` statement immediately passes execution control and a value back to the function caller. **Any lines written directly after a `return` statement in the same block are unreachable and will not run.**

```python
def cal_square(num):
    square_value = num * num
    return square_value
    print("This statement is unreachable and never runs!") # Dead code

result = cal_square(5)
print("Calculated result:", result)

# Reusing the returned output
adjusted_score = result + 10
print(f"Adjusted score (result + 10): {adjusted_score}")

```

---

## 4. Comprehensive Application: Prime Number Checker

Optimized by checking factors only up to the square root of the target number ($\sqrt{n}$), which vastly decreases time complexity for large numbers.

```python
def is_prime(n):
    if n <= 1:
        return False
    
    # Check factors from 2 up to the square root of n
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False # Found a factor, so it is not prime
    return True # No factors found, it is prime

# User Input Entry
user_num = int(input("Enter a number to check if it's Prime: "))

if is_prime(user_num):
    print(f"{user_num} is a Prime number.")
else:
    print(f"{user_num} is NOT a prime number.")

```

---
