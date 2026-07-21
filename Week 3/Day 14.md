Here is the structured and comprehensive daily diary entry for **Day 14** based on your notebooks covering **Train/Test Splitting, Linear Regression (Simple & Multiple), Model Evaluation, and Polynomial Regression**.
You can copy and paste this entry directly into your GitHub training diary repository!
# 📅 Summer Training - Daily Diary: Day 14
## 1. Splitting the Work (Train / Test Split)
Before training our machine learning models, we split our preprocessed dataset into two parts to evaluate performance fairly:
 1. **Training Set (80%):** The data our model studies to learn patterns and relationships.
 2. **Testing Set (20%):** The unseen data used to evaluate how accurately the model generalizes to new information.
> **The Math Exam Analogy:** If you study using practice questions and are given those *exact same* questions on the exam, memorizing them doesn't prove you understand math. To test real understanding, a teacher must give you *unseen questions*.
> 
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, r2_score

df = pd.read_csv("kc_house_preprocessed.csv")

# Separate features (X) from the target (y)
x = df.drop(columns=['price'])
y = df['price']

# Perform the 80/20 train/test split
X_train, X_test, Y_train, Y_test = train_test_split(x, y, test_size=0.20, random_state=42)

print(f"Training set rows: {X_train.shape[0]}")
print(f"Testing set rows: {X_test.shape[0]}")

```
## 2. Simple Linear Regression
We started simple by training a linear regression model using just **one clue**: Scaled_size (house size) to predict the house price.
```python
X_train_simple = X_train[['Scaled_size']]
X_test_simple = X_test[['Scaled_size']]

simple_model = LinearRegression()
simple_model.fit(X_train_simple, Y_train)

# Visualizing the predictions against test data
y_pred_simple = simple_model.predict(X_test_simple)

plt.figure(figsize=(10, 6))
plt.scatter(X_test_simple['Scaled_size'], Y_test, color='royalblue', alpha=0.3, label='Actual Test Houses')
plt.plot(X_test_simple['Scaled_size'], y_pred_simple, color="crimson", linewidth=3, label="Robot Prediction Line")
plt.xlabel("House Size (Scaled)")
plt.ylabel("Price ($)")
plt.title("House Prediction: Actual vs Best Fit Line")
plt.legend()
plt.show()

```
## 3. Multiple Linear Regression
Next, we scaled up our robot's training capabilities by feeding it **all available clues** (bedrooms, bathrooms, size, condition, location tiers, etc.) using Multiple Linear Regression.
```python
multiple_model = LinearRegression()
multiple_model.fit(X_train, Y_train)

y_pred_multiple = multiple_model.predict(X_test)
print("Multiple Linear Regression model trained successfully!")

```
### Making Predictions for a Custom House
We tested our multiple regression model with a custom hypothetical property profile:
```python
custom_house = pd.DataFrame([{
    'bedrooms': 3.0,
    'bathrooms': 2.0,
    'Scaled_size': 0.35,   # 35% of max house size
    'floors': 2.0,
    'waterfront': 0,
    'sqft_living': 1800.0, 
    'condition': 4,
    'Loc_Budget': 0, 
    'Loc_Mid-range': 1,
    'Loc_Premium': 0
}])

custom_house = custom_house[X_train.columns]
predicted_price = multiple_model.predict(custom_house)[0]
print(f"Predicted price for our custom house: ${predicted_price:,.2f}")

```
## 4. Model Evaluation & Comparison
To determine how accurately our models perform, we evaluated them using **Mean Absolute Error (MAE)** and the **R² Score**:
 * **MAE:** Represents the average dollar amount our model's predictions miss by (lower is better).
 * **R² Score:** Represents the proportion of variance in the target variable explained by the model (closer to 1.0 or 100% is better).
```python
mae_simple = mean_absolute_error(Y_test, y_pred_simple)
r2_simple = r2_score(Y_test, y_pred_simple)

mae_multiple = mean_absolute_error(Y_test, y_pred_multiple)
r2_multiple = r2_score(Y_test, y_pred_multiple)

print("==== Model Performance Comparison ====")
print(f"Simple Model (Size only): MAE = ${mae_simple:,.2f} | R2 Score = {r2_simple:.4f}")
print(f"Multiple Model (All Clues): MAE = ${mae_multiple:,.2f} | R2 Score = {r2_multiple:.4f}")

```
## 5. Teaching Our Robot to Curve (Polynomial Regression)
Because linear models draw straight lines, they might miss non-linear relationships. We built a **Polynomial Regression** pipeline (Degree 2) to fit a "bendy line" to our data patterns.
```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline

# Sample a subset for polynomial demonstration
df_sample = df.sample(n=80, random_state=42)
X_poly = df_sample.drop(columns="price")
y_poly = df_sample['price']

X_tr, X_te, y_tr, y_te = train_test_split(X_poly, y_poly, test_size=0.20, random_state=42)

# Create our "Bendy Line" pipeline (Degree 2)
poly_model = make_pipeline(PolynomialFeatures(degree=2), LinearRegression())
poly_model.fit(X_tr, y_tr)

# Evaluate performance
y_pred_poly = poly_model.predict(X_te)
y_train_pred_poly = poly_model.predict(X_tr)

mae_poly = mean_absolute_error(y_te, y_pred_poly)
r2_poly_test = r2_score(y_te, y_pred_poly)
r2_poly_train = r2_score(y_tr, y_train_pred_poly)

print("---- Robot Performance Summary (Polynomial) ----")
print(f"Average Miss (MAE): ${mae_poly:,.2f}")
print(f"Test Accuracy Score (R2): {r2_poly_test:.2%}")
print(f"Train Accuracy Score (R2): {r2_poly_train:.2%}")

```
### 💡 Key Takeaways from Day 14:
 1. **Train/Test Split:** Essential for mimicking real-world exams to check if a model genuinely learns patterns rather than just memorizing data.
 2. **Multiple vs. Simple Regression:** Feeding multiple structured features generally decreases error metrics (MAE) and increases explanatory power (R² score).
 3. **Polynomial Features:** Introducing polynomial degrees allows regression models to map curved, non-linear relationships in complex data distributed?
