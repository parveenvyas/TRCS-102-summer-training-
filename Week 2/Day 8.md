# 📅 Summer Training - Daily Diary: Day 8

## 1. Introduction to Pandas

**Pandas** is the core Python library used for data manipulation, structured data analysis, and tabular preprocessing in AI and Data Science.

```python
import pandas as pd
import numpy as np

print(f"Pandas Version: {pd.__version__}") # Checking installed version

```

## 2. Core Data Structures

Pandas introduces two main data structures for handling data:

1. **`Series`**: A 1D labeled array capable of holding any single data type.


2. **`DataFrame`**: A 2D tabular structure consisting of labeled rows and columns.



```python
# 1. Creating a Pandas Series
list1 = [1, 2, 3, 4, 5]
series1 = pd.Series(list1)
print("Pandas Series:\n", series1)

# 2. Creating a Pandas DataFrame
student_dict = {
    "Name": ["Ram", "Shyam", "Hari"],
    "Course": ["BCA", "BSc", "BBA"],
    "Rollno": [101, 102, 103]
}
df_student = pd.DataFrame(student_dict)
print("\nStudent DataFrame:\n", df_student)
print("Shape of DataFrame:", df_student.shape) # Returns (rows, columns)

```

## 3. Initial Data Inspection Tools

When loading a new dataset, standard inspection functions help analyze the structure:

* `df.head(n)`: Views the first `n` rows of the DataFrame.


* `df.tail(n)`: Views the last `n` rows of the DataFrame.


* `df.shape`: Returns a tuple representing total rows and columns.


* `df.dtypes`: Shows the data type of each column.


* `df.info()`: Summarizes memory usage, row count, and non-null values.


* `df.describe()`: Displays summary statistics (mean, std, min, max, quartiles) for numerical columns.



```python
# Reading customer dataset
df = pd.read_csv("data.csv")

print("--- Data Summary (info) ---")
df.info()

print("\n--- Statistical Overview (describe) ---")
print(df.describe())

```

---

## 4. Basic Slicing & Indexing

Accessing specific columns or subsets from a dataset:

```python
# Selecting a single column (returns a Series)
income_series = df["Income"]

# Selecting multiple columns (returns a DataFrame)
selected_cols = ["CustomerID", "Age", "Income"]
print(df[selected_cols])

```


---

