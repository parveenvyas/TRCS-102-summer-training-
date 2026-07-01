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
