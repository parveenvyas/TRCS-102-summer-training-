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
