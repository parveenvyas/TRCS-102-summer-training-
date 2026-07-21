
# 📅 Summer Training - Daily Diary: Day 13
## 1. Introduction to Data Preprocessing
Today, we took our cleaned King County housing dataset and prepared it for machine learning models. Raw data often contains extreme outliers, features on drastically different measurement scales, and text-based categorical columns that machine learning models cannot interpret directly. To solve this, we applied **Outlier Capping (IQR Method)**, **Feature Scaling (MinMaxScaler & StandardScaler)**, and **One-Hot Encoding**.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Load the filtered dataset from Day 12
df = pd.read_csv('kc_house_filtered.csv')

```
## 2. Outlier Detection & Capping (IQR Method)
Outliers—such as extreme house prices, square footage, or abnormal bedroom counts—can skew machine learning algorithms. We used the **Interquartile Range (IQR)** method to detect and cap outliers, ensuring our data stays within logical boundaries without dropping valuable rows.
```python
# IQR represents the middle 50% of our data
def find_caps(column_data):
    Q1 = column_data.quantile(0.25)
    Q3 = column_data.quantile(0.75)
    IQR = Q3 - Q1
    lower_cap = Q1 - 1.5 * IQR
    upper_cap = Q3 + 1.5 * IQR
    return lower_cap, upper_cap

columns = ['price', 'sqft_living', 'bedrooms']
for col in columns:
    lower, upper = find_caps(df[col])
    outliers_count = ((df[col] < lower) | (df[col] > upper)).sum()
    
    # clip restricts values to stay between the lower and upper bounds
    df[col] = df[col].clip(lower=lower, upper=upper)
    print(f"Capped {outliers_count} outliers in '{col}'. New range: {df[col].min()} to {df[col].max()}")

```
## 3. Balancing the Scales (Feature Scaling)
Features like sqft_living (ranging up to thousands) and bedrooms (ranging from 1 to 5) have vastly different scales. If left unscaled, models might unfairly prioritize features with larger numerical values. We utilized two major scaling techniques:
 1. **MinMaxScaler (Normalization):** Scales values strictly between 0 and 1.
 2. **StandardScaler (Standardization):** Centers the distribution around a mean of 0 with a standard deviation of 1.
```python
# MinMax Scaler on house living size (0 to 1 scaling)
minmax_scaler = MinMaxScaler()
df['Scaled_size'] = minmax_scaler.fit_transform(df[['sqft_living']])

# Standard Scaler on year built (centered around mean)
std_scaler = StandardScaler()
df['Year_Scaled'] = std_scaler.fit_transform(df[['yr_built']])

```
## 4. Translating Categories to Numbers (One-Hot Encoding)
Machine learning models only understand numbers, not text labels. To handle categorical text data like neighborhood tiers (Budget, Mid-range, Premium), we applied **One-Hot Encoding** using pandas, creating binary flag columns (0 or 1) for each category.
```python
# Simulate a mock categorical column 'Neighbourhood'
np.random.seed(42)
neighbourhoods = ['Budget', 'Mid-range', 'Premium']
df['Neighbourhood'] = np.random.choice(neighbourhoods, size=len(df))

# One-Hot Encoding using pd.get_dummies
df_encoded = pd.get_dummies(df, columns=['Neighbourhood'], prefix="Loc", dtype=int)
df_encoded.head()

```
## 5. Final Review & Saving Preprocessed Data
After cleaning, scaling, and encoding our features, we selected our final modeling columns and exported the preprocessed dataset ready for machine learning ingestion.
```python
final_cols = [
    'price', 'bedrooms', 'bathrooms', 'Scaled_size', 'floors', 
    'waterfront', 'sqft_living', 'condition', 'Loc_Budget',
    'Loc_Mid-range', 'Loc_Premium'
]
df_final = df_encoded[final_cols]

# Save the final preprocessed dataset
df_final.to_csv('kc_house_preprocessed.csv', index=False)

```
### 💡 Key Takeaways from Day 13:
 1. **Outlier Capping:** Using the IQR clipping method protects models from being distorted by extreme values while retaining dataset size.
 2. **Feature Scaling:** Normalizing and standardizing variables ensures equal footing for multi-variable regression and machine learning algorithms.
 3. **One-Hot Encoding:** Translating text categories into binary indicator columns makes categorical data readable by mathematical models.

