
# 📅 Summer Training - Daily Diary: Day 17
## 1. Introduction to Clustering (Unsupervised Learning)
Today, we started our journey into **Unsupervised Learning**. Unlike supervised learning where we feed a robot labeled answers (like "Is this house expensive?" or "Did this passenger survive?"), unsupervised learning gives the robot raw, unlabeled data and tells it: *"Figure out the patterns on your own!"*
 * **Project Focus:** Customer Segmentation for Retail Marketing using the Mall Customers dataset.
 * **Goal:** Group mall shoppers into natural segments based on their income and spending behavior so businesses can market to them effectively.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

import os
import warnings
warnings.filterwarnings("ignore")

sns.set_theme(style="whitegrid", palette='muted')
plt.rcParams['figure.dpi'] = 110
plt.rcParams['figure.figsize'] = (10, 6)

df = pd.read_csv('Mall_Customers.csv')
df.head()
df.columns

```
## 2. Exploratory Data Analysis & Visualization
We analyzed the dataset structure and created an initial scatter plot to visualize how customer annual income relates to their spending score.
```python
# Scatter Plot: Annual Income vs Spending Score
plt.figure(figsize=(8, 5.5))

sns.scatterplot(
    data=df,
    x='Annual Income (k$)',
    y='Spending Score (1-100)',
    s=70,
    color='#0a0653',
    alpha=0.8
)

plt.title('Customer Distribution : Annual Income vs Spending Score', fontsize=16, fontweight='bold')
plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score(1-100)')
plt.tight_layout()
plt.show()

```
## 3. Feature Scaling with Standard Scaler
Because **Annual Income** and **Spending Score** have different value ranges and units, distance-based algorithms like K-Means will give unfair weight to larger numbers. We used StandardScaler to put both features on the exact same scale.
```python
# 1. Selecting the features for clustering
X = df[["Annual Income (k$)", "Spending Score (1-100)"]]

# Standardize the features
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
X_scaled_df = pd.DataFrame(X_scaled, columns=X.columns)

print('=== First 5 rows of Scaled features ===')
print(X_scaled_df.head())

```
## 4. Applying K-Means Clustering
### How K-Means Works Step-by-Step 🚶‍♂️
 1. **Choose K:** Decide how many groups you want to find (we chose K = 5).
 2. **Place Centroids:** The algorithm places 5 starting anchors (called **centroids**) at random positions.
 3. **Assign Points:** Every customer point is assigned to its nearest centroid.
 4. **Update Centroids:** Each centroid moves to the exact center (average location) of all the points assigned to it.
 5. **Repeat:** The process repeats until the centroids stop shifting (the model converges).
```python
# n_init=10: the algorithm runs 10 times with different starting centroids
kmeans = KMeans(n_clusters=5, init='k-means++', n_init=10, random_state=42)

# Fit the model
kmeans.fit(X_scaled)

# Extract cluster assignments and centroid locations
labels = kmeans.labels_
centroids_scaled = kmeans.cluster_centers_

print("Model Training complete!")
print(f"First 10 customers are assigned to these clusters:\n{labels[:10]}")

```
## 5. Visualizing Final Clusters and Centroids
To interpret the results visually, we mapped the assigned cluster groups back to our dataset and converted the normalized centroids back to their original dollar/score scale.
```python
# Convert centroids back to original scale (k$ and 1-100 scale)
centroids_orig = scaler.inverse_transform(centroids_scaled)

# Add the cluster labels to our original DataFrame
df['Cluster'] = labels

plt.figure(figsize=(10, 6.5))
sns.scatterplot(
    data=df, x='Annual Income (k$)', y='Spending Score (1-100)',
    hue='Cluster', palette='Set1', s=70, alpha=0.5, edgecolor='w'
)

# Plot the centroids as large black stars
plt.scatter(
    centroids_orig[:, 0],  # X coordinates of centroids
    centroids_orig[:, 1],  # Y coordinates of centroids
    color='black', marker='*',
    s=300, edgecolor='white', linewidth=1.5, label='Centroids (Cluster Centers)'
)

plt.title('Mall Customer Segmentation (k = 5)', fontsize=15, fontweight='bold')
plt.xlabel('Annual Income (k$)')
plt.ylabel('Spending Score (1-100)')
plt.legend()
plt.tight_layout()
plt.show()

```

## 6. Interpreting the Customer Segments 📊
Based on the clusters, we can segment retail marketing strategies:
 1. **High Income, High Spending (Premium Shoppers):** Goldmine customers; target with luxury offers and VIP loyalty programs.
 2. **High Income, Low Spending (Conservative Spenders):** High earners who spend carefully; target with value propositions.
 3. **Average Income, Average Spending (Standard Shoppers):** Middle-class steady spenders.
 4. **Low Income, High Spending (Impulsive Buyers):** Spend heavily despite lower income; respond well to promotional discounts.
 5. **Low Income, Low Spending (Budget Shoppers):** Frugal and price-sensitive; focus on cost-saving product lines.
## 6. Choosing K mathematically: The Elbow Method 📐
When working with high-dimensional data where visual inspection fails, we use the **Elbow Method** to choose the optimal K:
 * Run K-Means for various values of K (e.g., 1 to 10).
 * Calculate **Inertia** (Within-Cluster Sum of Squares), which measures how tightly clustered the data points are relative to their centroids.
 * Plot Inertia against K. The "elbow" point on the curve marks the optimal number of clusters where adding more groups yields diminishing returns.
```python
inertias = []
k_values = range(1, 11)

for k in k_values:
    km = KMeans(n_clusters=k, init='k-means++', n_init=10, random_state=42)
    km.fit(X_scaled)
    inertias.append(km.inertia_)

# Plotting the Elbow Curve
plt.figure(figsize=(8.5, 5))
plt.plot(k_values, inertias, marker='o', color='#6366f1', linewidth=2.5)
plt.title('The Elbow Method for Finding Optimal K', fontsize=14, fontweight='bold')
plt.xlabel('Number of Clusters (K)')
plt.ylabel('Inertia (Within-Cluster Sum of Squares)')
plt.axvline(5, color='#ef4444', linestyle='--', label='Elbow Point (K = 5)')
plt.legend()
plt.tight_layout()
plt.show()

```
### 💡 Key Takeaways from Days 17:
 1. **Unsupervised Learning:** Uncovers hidden structures or segments in unlabeled data without predefined target outputs.
 2. **K-Means Clustering:** An iterative centroid-based technique that groups observations into distinct partitions.
 3. **Feature Scaling:** Mandatory for distance-centric algorithms to ensure all variables contribute equally.
 4. **The Elbow Method:** A reliable heuristic for identifying the optimal number of clusters by tracking drops in model inertia.



