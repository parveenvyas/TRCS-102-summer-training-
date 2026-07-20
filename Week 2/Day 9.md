
# 📅 Summer Training - Daily Diary: Day 9

## 1. Advanced Indexing: `.loc` vs. `.iloc`

* **`.loc[row_labels, column_names]`**: Targets data using explicit row index labels and named columns. Range bounds are **inclusive**.


* **`.iloc[row_indices, column_indices]`**: Targets data using numerical positional indices. Range bounds are **exclusive** of the end index.



```python
import pandas as pd
df = pd.read_csv("data.csv")

# 1. Using .loc (Label-based)
# Selects rows from label 0 to 3 for 'CustomerID' and 'Income'
print("Using .loc:\n", df.loc[0:3, ["CustomerID", "Income"]])

# 2. Using .iloc (Position-based)
# Selects rows 1 to 3 (index 1:4) and columns 1 to 3 (index 1:4)
print("\nUsing .iloc:\n", df.iloc[1:4, 1:4])

```

---

## 2. Boolean Indexing & Conditional Filtering

Filtering datasets dynamically based on logical rules (`&` for AND, `|` for OR).

```python
# Filter rows where Income is greater than 50,000
high_income = df[df['Income'] > 50000]
print("Income > 50,000:\n", high_income)

# Multi-condition filtering: Females with Income > 45,000
female_high_income = df[(df["Income"] > 45000) & (df["Gender"] == "F")]
print("\nFemales with Income > 45,000:\n", female_high_income)

```

---

## 3. Data Preprocessing & Cleaning Missing Values (`NaN`s)

Real-world datasets contain missing gaps (`NaN` — Not a Number). Machine Learning models cannot process missing entries, so they must be scrubbed or filled.

1. **Detecting Nulls**: `df.isnull().sum()` lists missing entry counts per column.


2. **Imputation (`.fillna()`)**: Fills missing values with standard metrics like `mean` or `median`.


3. **Deletion (`.dropna()`)**: Drops rows containing missing values in key columns.



```python
# Check missing value counts
print("Missing values before cleaning:\n", df.isnull().sum())

# Strategy A: Imputing missing numerical values with column mean
age_mean = df["Age"].mean()
df["Age"] = df["Age"].fillna(age_mean)

income_mean = df["Income"].mean()
df["Income"] = df["Income"].fillna(income_mean)

# Strategy B: Dropping rows where critical categorical entries (like Gender) are NaN
df = df.dropna(subset=["Gender"])

print("\nMissing values after cleaning:\n", df.isnull().sum())

```

---

## 4. Hands-On Practice Exercises (Titanic Dataset)

### Exercise 9.1: Dataset Inspection & Selection

```python
titanic_df = pd.read_csv("train.csv")

# 1. Verify Series data type
print("Fare type:", type(titanic_df["Fare"]))

# 2. Display specific columns
print(titanic_df[["Name", "Sex", "Age"]].head())

# 3. Positional slicing: Rows 10-14, First 5 columns
print(titanic_df.iloc[10:15, 0:5])

```

### Exercise 9.2: Titanic Filtering & Preprocessing

```python
# Count total survivors
survived_count = len(titanic_df[titanic_df["Survived"] == 1])
print("Total Survivors:", survived_count)

# Impute missing Age entries with median
median_age = titanic_df["Age"].median()
titanic_df["Age"] = titanic_df["Age"].fillna(median_age)

# Drop missing 'Embarked' rows
titanic_df = titanic_df.dropna(subset=["Embarked"])
print("Remaining null values:\n", titanic_df.isnull().sum())

```

---

