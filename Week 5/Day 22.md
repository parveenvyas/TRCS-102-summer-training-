
# 📅 Summer Training Diary – Day 22


# 📚 Topics Covered

## 1. Train-Test Split

### Theory

The dataset is divided into:

- **Training Set (80%)** → Used for training
- **Testing Set (20%)** → Used for evaluation

This ensures unbiased model performance.

---

## 2. Train-Test Split

### Code

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42,
    stratify=y
)
```

### Explanation

Splits the dataset into training and testing datasets while maintaining the same churn ratio.

### Learning

Learned why train-test splitting is important.

---

## 3. Machine Learning Model Training

### Theory

The Random Forest Classifier is an ensemble learning algorithm that combines multiple decision trees to improve prediction accuracy.

Advantages:

- High Accuracy
- Handles large datasets
- Reduces overfitting
- Works well with mixed features

---

## 4. Model Evaluation

### Theory

Model evaluation measures how well the trained model performs on unseen data.

Common metrics include:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

---

## 5. Confusion Matrix

### Code

```python
cm = confusion_matrix(y_test, y_pred_rf)
```

### Explanation

Displays correct and incorrect predictions made by the model.

### Learning

Learned how to evaluate classification performance.

---

## 6. Feature Importance

### Code

```python
feature_importance = pd.Series(
    model_rf.feature_importances_,
    index=X.columns
)
```

### Explanation

Calculates how much each feature contributes to customer churn prediction.

### Learning

Identified the most influential factors affecting customer churn.

---

## 7. Customer Churn Prediction Function

### Code

```python
def predict_customer_churn(
    tenure,
    monthly_charges,
    support_tickets,
    contract_type,
    feedback_text
):
```

### Explanation

Creates a function that accepts customer information and predicts whether the customer is likely to churn.

### Learning

Learned how to deploy a trained model for real-world predictions.

---

## 8. Saving the Model

### Code

```python
import pickle
```

### Explanation

Uses the **pickle** library to save the trained machine learning model.

### Learning

Saved models can be reused without retraining.

---

# ✅ Learning Outcome

By the end of Day 22, I learned:

- Train-test splitting
- Random Forest Classifier
- Model evaluation
- Confusion Matrix
- Feature Importance
- Customer churn prediction
- Model serialization using Pickle

