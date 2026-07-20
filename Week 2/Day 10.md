# 📅 Summer Training - Daily Diary: Day 10

## 1. Grouping & Aggregations (`groupby`)

Categorical aggregations allow evaluating group-level statistics (e.g., comparing metrics across demographic segments). We use **`.groupby()`** combined with aggregation methods like `.mean()`, `.sum()`, or `.count()`.

```python
import pandas as pd

df = pd.read_csv("data.csv")

# Impute missing values for clean aggregation
df["Age"] = df["Age"].fillna(df["Age"].mean())
df["Income"] = df["Income"].fillna(df["Income"].mean())
df = df.dropna(subset=["Gender"])

# Group by Gender and calculate mean Age and Income
gender_summary = df.groupby("Gender")[["Age", "Income"]].mean()
print("Groupby Gender Summary:\n", gender_summary)

# Group by Purchased status and calculate mean metrics
purchase_summary = df.groupby("Purchased")[["Income", "Age"]].mean()
print("\nGroupby Purchased Summary:\n", purchase_summary)

```

---

## 2. Practical Data Exploration Exercises

### Exercise 10.1: Titanic Survival Aggregations

```python
titanic_df = pd.read_csv("train.csv")

# Fill missing age with median
titanic_df["Age"] = titanic_df["Age"].fillna(titanic_df["Age"].median())

# 1. Average age by Sex
print("Average Age by Sex:\n", titanic_df.groupby("Sex")["Age"].mean())

# 2. Average Fare by Passenger Class (Pclass)
print("\nAverage Fare by Pclass:\n", titanic_df.groupby("Pclass")["Fare"].mean())

# 3. Average Age and Fare grouped by Survival status
print("\nAverage Age & Fare by Survival:\n", titanic_df.groupby("Survived")[["Age", "Fare"]].mean())

```

### Exercise 10.2: House Prices Feature Extraction Pipeline

```python
house_df = pd.read_csv("house_data.csv")

# Extract relevant model features
features = ["price", "bedrooms", "bathrooms", "sqft_living", "floors", "waterfront", "yr_built", "condition"]
clean_house_df = house_df[features]

print("Dataset Shape:", clean_house_df.shape)
print("\nMissing values check:\n", clean_house_df.isnull().sum())

# Subset slicing examples
print("\nLabel-based Slice (.loc):\n", clean_house_df.loc[0:5, ["price", "bedrooms", "floors"]])
print("\nPositional Slice (.iloc):\n", clean_house_df.iloc[0:3, 0:6])

```

---

