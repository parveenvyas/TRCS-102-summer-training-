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

Here is the clean, professional, and structured Markdown entry for **Days 10, 11, and 12** based on your Matplotlib and Seaborn visualization notebook.

You can copy and paste each day's entry into your GitHub training diary repo!

---

## 3. Introduction to Data Visualization

Today, we transitioned to visual data analysis using **Matplotlib** and **Seaborn**. Data visualization allows us to identify trends, distributions, outliers, and feature correlations much faster than raw numbers.

```python
import matplotlib.pyplot as plt 
import seaborn as sns
import numpy as np
import pandas as pd

```

---

## 4. Line Charts (Trend Tracking)

Line charts are best used for continuous numerical values to track changes or trends over a sequence (e.g., time).

```python
# Sample Data: Speed over days
days = [1, 2, 3, 4, 5]
speed = [10, 25, 45, 70, 95]

plt.figure(figsize=(7, 4))
plt.plot(days, speed, color="red", marker='*', linestyle='--', linewidth=2, label='speed')

# Chart annotations
plt.title("Speed over Days")
plt.xlabel("Time (Days)")
plt.ylabel("Speed (km/h)")
plt.legend()
plt.grid(True)
plt.show()

```

---

## 5. Bar Plots (Categorical Comparisons)

Bar plots excel at comparing discrete categorical groups.

```python
treats = ['Chocolates', 'Gummy Bears', 'Cookies', 'Ice Cream']
count = [15, 8, 22, 12]

plt.figure(figsize=(7, 4))
plt.bar(treats, count, color='skyblue', edgecolor='yellow')

plt.title("Treats Eaten by Friends This Week", fontsize=12)
plt.xlabel("Types of Treats", fontsize=12)
plt.ylabel("Total Eaten Count", fontsize=12)
plt.show()

```

---

## 6. Scatter Plots (Relationship & Pattern Analysis)

Scatter plots display individual data points across two continuous axes to uncover relationships or spatial distributions.

```python
east_coords = [2, 4, 1, 5, 3, 2.5, 4.5, 1.5]
north_coords = [3, 1, 4, 2, 5, 3.5, 1.5, 4.2]

plt.figure(figsize=(7, 4))
plt.scatter(east_coords, north_coords, color="gold", marker='o', s=100, edgecolor='darkgoldenrod')

plt.title("Treasure Chest Locations on Map", fontsize=14, color='orange')
plt.xlabel("East-West Coordinates")
plt.ylabel("North-South Coordinates")
plt.grid(True)
plt.show()

```


---

