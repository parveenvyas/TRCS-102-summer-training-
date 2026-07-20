# 📅 Summer Training - Daily Diary: Day 11

## 1. Histograms & KDE (Distribution Analysis)

Histograms bin continuous numerical data to show its frequency distribution. Kernel Density Estimation (KDE) overlays a smooth probability density curve over the histogram.

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Generate simulated candy counts (Normal distribution centered at 20)
np.random.seed(42)
candies = np.random.normal(loc=20, scale=4, size=30).astype(int)
df_candy = pd.DataFrame({"Candies": candies})

# Plotting Histogram with KDE
sns.set_theme(style="whitegrid")
plt.figure(figsize=(7, 4))
sns.histplot(data=df_candy, x="Candies", kde=True, color="blue", bins=8)

plt.title("Candy Distribution Among Kids", fontsize=14)
plt.xlabel("Number of Candies", fontsize=12)
plt.ylabel("Number of Kids (Count)", fontsize=12)
plt.show()

```

---

## 2. Box Plots (Outlier Detection)

Box plots summarize data distributions using a 5-number summary (Minimum, Q1, Median, Q3, Maximum). They are the best tool for instantly spotting **outliers** (extreme anomaly values).

```python
frog_jumps = [5, 6, 4, 7, 5, 7, 6, 7, 5, 18, 20] # Note: 18 and 20 are outliers
df_frogs = pd.DataFrame({"JumpDistance": frog_jumps})

plt.figure(figsize=(7, 3.5))
sns.boxplot(data=df_frogs, x="JumpDistance", color="lightgreen")

plt.title("Frog Jump Distance & Outlier Detection", fontsize=14, color='darkgreen')
plt.xlabel("Jump Distance (Feet)", fontsize=12)
plt.show()

```

---

## 3. Correlation Heatmaps

Heatmaps provide a color-coded grid representing the linear relationship (correlation coefficients) between multiple numeric variables.

```python
df_game = pd.DataFrame({
    'PlayTime_Hours': [10, 50, 80, 20, 95],
    'Popularity_Score': [40, 85, 90, 30, 98],
    'Game_Difficulty': [8, 5, 3, 9, 2]
})

corr_matrix = df_game.corr()

plt.figure(figsize=(6, 4.5))
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", vmin=-1, vmax=1, linewidths=2)
plt.title("Video Game Features Correlation Grid", fontsize=14, color='darkgreen')
plt.show()

```

---

## 1. Titanic Dataset Visualization Exercises

Today, we applied Seaborn and Matplotlib to inspect the Titanic passenger dataset.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("train.csv")

```

### Exercise 12.1: Passenger Age Distribution (Histogram)

```python
plt.figure(figsize=(8, 5))
sns.histplot(data=df, x="Age", kde=True, color="green", bins=8)

plt.title("Age Distribution of Titanic Passengers", fontsize=14, color='darkgreen')
plt.xlabel("Age", fontsize=12)
plt.show()

```

### Exercise 12.2: Survival Count (Countplot)

```python
plt.figure(figsize=(8, 5))
sns.countplot(data=df, x="Survived", hue="Survived", palette="Set1", legend=False)

plt.title("Titanic Passengers Survival Count", fontsize=14, color='darkgreen')
plt.xlabel("Survived (0 = No, 1 = Yes)")
plt.ylabel("Count")
plt.show()

```

### Exercise 12.3: Demographic Gender Split

```python
plt.figure(figsize=(8, 5))
sns.countplot(data=df, x="Sex", hue="Sex", palette="Set1", legend=False)

plt.title("Titanic Passengers Gender Distribution", fontsize=14, color='darkgreen')
plt.xlabel("Gender")
plt.ylabel("Count")
plt.show()

```

### Exercise 12.4: Ticket Fare Outlier Analysis (Boxplot)

```python
plt.figure(figsize=(8, 5))
sns.boxplot(data=df, x="Fare", color="teal")

plt.title("Ticket Fare Distribution & Outliers", fontsize=14, color='darkgreen')
plt.xlabel("Fare")
plt.show()

```

### Exercise 12.5: Bivariate Analysis — Age vs. Fare by Survival (Scatter Plot)

```python
plt.figure(figsize=(8, 5))
sns.scatterplot(data=df, x="Age", y="Fare", hue="Survived", palette="coolwarm")

plt.title("Passenger Age vs Ticket Fare")
plt.xlabel("Age")
plt.ylabel("Fare")
plt.show()

```

### Exercise 12.6: Titanic Feature Correlation Matrix (Heatmap)

```python
# Selecting numerical columns only
num_cols = ["Survived", "Pclass", "Age", "Fare"]
titanic_corr = df[num_cols].corr()

plt.figure(figsize=(7, 5))
sns.heatmap(titanic_corr, annot=True, cmap="coolwarm", vmin=-1, vmax=1, linewidths=1)
plt.title("Relation Between Survival, Class, Age, and Fare", fontsize=12)
plt.show()

```

---

