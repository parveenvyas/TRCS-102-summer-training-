
# 📅 Summer Training - Daily Diary: Day 5
## Data Structures

## 2. Tuples

A tuple is an ordered, **immutable** collection type in Python. Once created, its elements cannot be altered, added, or removed.

### 2.1 Tuple Unpacking

Unpacking allows you to extract elements of a tuple directly into individual variables.

```python
tuple1 = (10, 20, 30)
l, b, h = tuple1 # Unpacking into separate variables
print(f"l: {l}")
print(f"Calculated value (l * b + h): {l * b + h}")

```

### 2.2 Wildcard Unpacking (`*`)

When you don't know the exact length or only want to isolate specific values, the `*` operator aggregates remaining elements into a list.

```python
tuple1 = (10, "simran", 80, 90, 30, 10, 12)

# age takes 10, name takes "simran", course takes 12, and *expenses grabs everything in between
age, name, *expenses, course = tuple1 

print("Age:", age)
print("Expenses (gathered as list):", expenses)
print("Course:", course)

```

### 2.3 Practical ML Layout: Multi-Level Tuple Unpacking

Tuples are frequently used to hold data matrix splits in Machine Learning validation pipelines.

```python
dataset_splits = (
    ([1, 2, 3, 4, 5.6, 7.8], [0, 1, 0, 1]), # Train: (X, y)
    ([2.1, 4, 3], [1, 0]),                  # Val:   (X, y)
    ([9.0], [1])                            # Test:  (X, y)
)

# Phase 1 Unpacking: Break splits apart
train, val, test = dataset_splits

# Phase 2 Unpacking: Isolate features (X) from labels (y)
x_train, y_train = train
x_val, y_val = val
x_test, y_test = test

print(f"Train samples count: {len(x_train)}")
print(f"Val samples count: {len(x_val)}")
print(f"Test samples count: {len(x_test)}")

```

### 2.4 Bypassing Immutability (Type Conversion)

Since tuples cannot be changed directly, you must convert them to a list to modify them, then convert them back.

```python
tuple1 = (10, 20, 30, 40, 50)

list1 = list(tuple1)    # Step 1: Convert to list
list1.insert(1, 100)    # Step 2: Modify
list1.append(60)
tuple1 = tuple(list1)   # Step 3: Convert back to tuple

print("Modified Tuple:", tuple1)

```

---

## 3. Dictionaries

Dictionaries store data in unordered, mutable **Key-Value** pairs. They provide highly optimized search speeds based on keys.

```python
student = {
    "Name": "sahil",
    "course": "B.tech",
    "rollno": 101
}

# Reading components using dictionary views
print("Keys:", student.keys())
print("Values:", student.values())
print("Items:", student.items())

# Iterating through a dictionary
print("\nReading dictionary entries:")
for key, value in student.items():
    print(f" - {key} : {value}")

# Accessing and modifying values
print("\nSelected Roll Number:", student["rollno"])
student["rollno"] = 103          # Updating value
student["school"] = "GNDEC"      # Appending a new key-value pair
print("Updated Student Dict:", student)

```

### 💡 Algorithmic Optimization: Frequency Counter

```python
data = [100, 300, 200, 300, 400]
count = {}

# Optimized O(n) Approach: Single pass incrementation
for item in data:
    if item in count:
        count[item] += 1
    else:
        count[item] = 1
print("Frequency Counter Output:", count)

```

---

## 4. Sets

Sets are unordered collections of **unique** elements. They automatically discard duplicate values and excel at mathematical group comparisons.

```python
# Eliminating duplicate items via set cast casting
list1 = [100, 200, 300, 400, 100, 200]
set1 = set(list1)
print("Unique Set Elements:", set1)

```

### 4.1 Set Operators & Methods

```python
train_classes = {"cat", "dog", "sheep"}
val_classes = {"dog", "horse", "sheep"}

# Union (|): Combines all unique items from both groups
print("UNION:", train_classes | val_classes)

# Intersection (&): Pulls only matching mutual items
print("INTERSECTION:", train_classes & val_classes)

# Difference (-): Items in the first set but NOT in the second
print("DIFFERENCE (Train - Val):", train_classes - val_classes)

# Symmetric Difference (^): Items unique to either set (removes overlap)
print("SYMMETRIC DIFFERENCE:", train_classes ^ val_classes)

```

---

## 5. Practical Programming Exercises

### Exercise 5.1: Machine Learning Dataset Label Validation

```python
train_labels = ["tumor", "healthy", "healthy", "tumor", "cyst", "tumor"]
test_labels = ["tumor", "healthy", "fibroid", "tumor"]

# Deduplicating classes via set conversion
train_set = set(train_labels)
test_set = set(test_labels)

print("Unique Train Classes:", train_set)
print("Unique Test Classes:", test_set)

# Finding structural anomalies / data leakage classes
print("Unseen Classes in Test Set:", test_set - train_set)
print("All Unique Dataset System Labels:", train_set | test_set)

```

### Exercise 5.2: Weather Array Temperature Filter

```python
temp = [28, 32, 18, 15, 30, 22, 17]
cold_days = []
hot_days = []

for t in temp:
    if t < 20:
        cold_days.append(t)
    else:
        hot_days.append(t)
        
print("Cold Days (<20°C):", cold_days)
print("Hot Days (>=20°C):", hot_days)

```

### Exercise 5.3: Student Information Unpacker

```python
student_record = ("S105", "Ananya", 20, "AI/ML")
student_id, name, age, course = student_record

print(f"Student {name} (ID: {student_id}) is {age} years old and is enrolled in {course}.")

```

### Exercise 5.4: Book Inventory Tracker

```python
inventory = {"Python Guide": 12, "Maths for ML": 5, "AI basics": 8}

# Add entry conditionally if it doesn't exist
if "Data Science Handbook" not in inventory:
    inventory["Data Science Handbook"] = 10

# Decrement a stock value
inventory["Maths for ML"] -= 3

# Bulk restocking: Incrementing all components by 10
for k in inventory.keys():
    inventory[k] += 10
    
print("Final Book Inventory:", inventory)

```

### Exercise 5.5: Cross-Workshop Student Registration Tracker

```python
python_workshop = ["dev@email.com", "raj@email.com", "amit@email.com", "dev@email.com"]
ai_workshop = ["amit@email.com", "priya@email.com", "raj@email.com"]

# Deduplicate profiles
python_attendees = set(python_workshop)
ai_attendees = set(ai_workshop)

# Find intersection: Students enrolled in BOTH classes
print("Students registered for both workshops:", python_attendees & ai_attendees)

```

---

