
# 📅 Summer Training - Daily Diary: Day 12
## 1. Introduction to Exploratory Data Analysis (EDA)
Today, we performed **Exploratory Data Analysis (EDA)** using a real-world case file of over **21,000 houses** in King County, USA. EDA acts like "detective work" where we use Python libraries to inspect data characteristics, uncover statistical distributions, detect outliers, and study feature correlations before machine learning modeling.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
df = pd.read_csv("kc_house_data.csv")

```
## 2. Simplifying the Case File (Feature Selection)
To keep our analysis focused and intuitive, we filtered our dataset to retain only the most critical, easily understandable features related to house pricing:
 * **price**: The price of the house (Target value)
 * **bedrooms**: Number of bedrooms
 * **bathrooms**: Number of bathrooms
 * **sqft_living**: Living space size in square feet
 * **floors**: Number of floors/stories
 * **waterfront**: Waterfront view indicator (1 = \text{Yes}, 0 = \text{No})
 * **yr_built**: Year the house was built
 * **condition**: Maintenance condition rating (1 = \text{Poor}, 5 = \text{Excellent})
```python
friendly_cols = ['price', 'bedrooms', 'bathrooms', 'sqft_living', 'floors', 'waterfront', 'yr_built', 'condition']
df = df[friendly_cols]
df.head()

```
## 3. Detective Statistics (.describe())
Using .describe(), we extracted quick statistical summaries to understand minimums, maximums, means, and standard deviations across our housing features.
```python
df.describe()

```
## 4. Univariate Analysis: The Price Mountain
We plotted a histogram with a Kernel Density Estimation (KDE) curve to analyze the distribution of house prices.
```python
plt.figure(figsize=(10, 5))
sns.histplot(data=df, x="price", kde=True, color="teal", bins=40)
plt.title("The Price Mountain: How House Prices are Distributed", fontsize=16)
plt.xlabel("Price ($)", fontsize=12)
plt.ylabel("Number of Houses", fontsize=12)
plt.show()

print("Right-skewed distribution indicates the presence of high-end price outliers.")

```
 * **Observation:** The price mountain is right-skewed, showing that while most houses fall into standard price ranges, a few luxury homes skew the tail toward multi-million-dollar values.
## 5. Bivariate & Outlier Analysis
### A. Bedroom Counts & Extreme Outliers
Using a countplot, we checked the frequency of bedroom counts across properties and searched for anomalies.
```python
plt.figure(figsize=(10, 5))
sns.countplot(data=df, x="bedrooms", hue="bedrooms", palette='Set2', legend=False)
plt.title('Bedroom Counts: How many rooms do people want?', fontsize=14)
plt.xlabel("Number of bedrooms", fontsize=12)
plt.ylabel("Number of Houses", fontsize=12)
plt.show()

# Find houses with extreme/abnormal number of bedrooms
giant_outlier = df[df['bedrooms'] > 10]
print(giant_outlier)

```
 * **Discovery:** Our data hygiene check successfully flagged bizarre data anomalies, such as a property with **33 bedrooms** packed into a 1,620 sqft living space—highlighting why outlier scrubbing is critical before model training.
### B. Size vs. Price (Living Area Impact)
We checked whether larger houses command higher prices by constructing a scatter plot, using waterfront as a hue modifier.
```python
plt.figure(figsize=(10, 6))
sns.scatterplot(data=df, x="sqft_living", y='price', hue="waterfront", palette='coolwarm')
plt.title('Size vs Price: Does a larger house cost more?', fontsize=16, color="red")
plt.xlabel("House Size (Square Feet)", fontsize=12)
plt.ylabel("Price ($)", fontsize=12)
plt.show()

```
### C. Waterfront Living Impact
Using a box plot, we evaluated how waterfront access alters property valuation.
```python
plt.figure(figsize=(10, 5))
sns.boxplot(x="waterfront", y="price", data=df, hue='waterfront', palette='pastel', legend=False)
plt.title('Waterfront View vs Price: Is lake-side living expensive?', fontsize=16)
plt.xticks([0, 1], ['No waterfront', 'Waterfront'])
plt.xlabel("House Location", fontsize=12)
plt.ylabel("Price ($)", fontsize=12)
plt.ticklabel_format(style='plain', axis='y')
plt.show()

```
### D. House Condition vs. Average Price
We grouped data by the condition rating to observe if cleaner, well-maintained homes command higher average prices.
```python
plt.figure(figsize=(8, 5))
sns.barplot(x="condition", y="price", data=df, hue='condition', palette='coolwarm', legend=False)
plt.title('House Condition vs Price: Do cleaner houses sell for more?', fontsize=16)
plt.xlabel("House Condition Rating (1 to 5)", fontsize=12)
plt.ylabel("Average Price ($)", fontsize=12)
plt.ticklabel_format(style='plain', axis='y')
plt.show()

```
## 6. The Connection Matrix (Correlation Heatmap)
To map out relationships among all numerical variables simultaneously, we generated a correlation matrix visualized via a Seaborn heatmap.
```python
plt.figure(figsize=(10, 8))
correlation_map = df.corr()
sns.heatmap(correlation_map, annot=True, cmap='coolwarm', linewidths=0.5, vmin=-1, vmax=1)
plt.title('The Magic Connection Map (Correlation Heatmap)', fontsize=16)
plt.show()

```
### 💡 Key Takeaways from Day 12:
 1. **Size Matters Most:** sqft_living displays the strongest positive correlation with house prices among standard structural attributes.
 2. **Waterfront Premium:** Waterfront properties exhibit significantly higher median prices and wider valuation spreads.
 3. **Data Cleaning Need:** EDA successfully isolates abnormal data points (e.g., 33 bedrooms), proving that raw datasets require preprocessing before building predictive models.
```python
# Saving our filtered dataset for upcoming training steps
df.to_csv('kc_house_filtered.csv', index=False)

```
A single relevant follow-up question to guide our progress: Would you like to dive into data cleaning routines to handle those extreme bedroom and price outliers next?
