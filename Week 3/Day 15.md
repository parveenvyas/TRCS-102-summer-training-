
# 📅 Summer Training - Daily Diary: Day 15
## 1. Ridge and Lasso Regularization (Putting a Leash on our Robot)
When we train high-degree polynomial models (like a Degree 6 model), the robot can experience **overfitting**, creating wild, looping curves that memorize the training data rather than learning general patterns. To fix this, we apply regularization—acting as a leash on our model weights.
 * **1. Ridge Regression (L2 Penalty - "The Gentle Leash"):** Shrinks all the weights of the curve closer to zero, but doesn't make any of them exactly zero.
 * **2. Lasso Regression (L1 Penalty - "The Strict Leash"):** Can shrink weights completely down to zero, effectively performing feature selection.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression, Ridge, Lasso
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.metrics import mean_absolute_error, r2_score

df = pd.read_csv("kc_house_preprocessed.csv")
df_sample = df.sample(n=80, random_state=42)

X = df_sample[['Scaled_size']]
y = df_sample['price']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)

```
### Comparing Model Leashes:
```python
# 1. Wild Model (No Leash / Overfitting)
wild_model = make_pipeline(PolynomialFeatures(degree=6), LinearRegression())
wild_model.fit(X_train, y_train)
y_pred_wild = wild_model.predict(X_test)
print(f"Wild Robot R² Score: {r2_score(y_test, y_pred_wild):.2%}")

# 2. Ridge Regularization (Gentle Leash)
ridge_model = make_pipeline(PolynomialFeatures(degree=6), Ridge(alpha=0.1))
ridge_model.fit(X_train, y_train)
y_pred_ridge = ridge_model.predict(X_test)
print(f"Ridge Model R² Score: {r2_score(y_test, y_pred_ridge):.2%}")

# 3. Lasso Regularization (Strict Leash)
lasso_model = make_pipeline(PolynomialFeatures(degree=6), Lasso(alpha=0.1))
lasso_model.fit(X_train, y_train)
y_pred_lasso = lasso_model.predict(X_test)
print(f"Lasso Model R² Score: {r2_score(y_test, y_pred_lasso):.2%}")

```
## 2. Introduction to Classification: Logistic Regression
While regression predicts continuous numbers (like house prices), **Classification** predicts discrete categories or labels (like *Survived* vs. *Not Survived*). We used the famous Titanic dataset (train.csv) to build binary and multiclass logistic regression models.
### Data Preprocessing for Classification
```python
df = pd.read_csv('train.csv')

# Handle missing data & map categories to numeric values
df['Age'] = df['Age'].fillna(df['Age'].median())
most_common_embarked = df['Embarked'].mode()[0]
df['Embarked'] = df['Embarked'].fillna(most_common_embarked)
df['IsFemale'] = df['Sex'].map({'female': 1, 'male': 0})

features = ['Age', 'Fare', 'SibSp', 'Parch', 'IsFemale']

```
## 3. Binary Classification (Predicting Survival)
Our first classification task was predicting whether a passenger survived (0 or 1) based on attributes like age, fare, and gender.
```python
X = df[features]
y = df['Survived']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train the binary logistic model
binary_model = LogisticRegression(max_iter=1000)
binary_model.fit(X_train, y_train)

# Evaluate performance
y_pred = binary_model.predict(X_test)
print(f"Binary Classification Accuracy: {accuracy_score(y_test, y_pred):.2%}")
print(classification_report(y_test, y_pred, target_names=['Not Survived', 'Survived']))

```
## 4. Multiclass Classification (Predicting Passenger Class)
Instead of a binary outcome, we can predict multiple categories—such as passenger ticket class (Pclass: 1, 2, or 3).
```python
features_multi = ['Survived', 'Age', 'Fare', 'SibSp', 'Parch', 'IsFemale']

X_multi = df[features_multi]
y_multi = df['Pclass']

X_train_m, X_test_m, y_train_m, y_test_m = train_test_split(X_multi, y_multi, test_size=0.2, random_state=42)

# Train the multiclass logistic model
multiclass_model = LogisticRegression(max_iter=1000)
multiclass_model.fit(X_train_m, y_train_m)

# Evaluate performance
y_pred_multi = multiclass_model.predict(X_test_m)
print(f"Multiclass Classification Accuracy: {accuracy_score(y_test_m, y_pred_multi):.2%}")
print(classification_report(y_test_m, y_pred_multi, target_names=['Class 1', 'Class 2', 'Class 3']))

```
### 💡 Key Takeaways from Day 15:
 1. **Regularization (Ridge & Lasso):** Adds penalties to large coefficients, preventing complex polynomial models from overfitting noisy training trends.
 2. **Binary vs. Multiclass:** Logistic regression can seamlessly scale from predicting two outcomes (yes/no) to sorting items into multiple distinct buckets.
 3. **Evaluation Metrics:** Accuracy scores and classification reports (precision, recall, F1-score) provide deep insight into classification model reliability beyond simple guesswork.

