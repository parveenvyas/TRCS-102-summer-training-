
# 📅 Summer Training - Daily Diary: Day 16
## 1. Introduction to Decision Trees and Random Forests
Today, we extended our Titanic survival prediction project by moving beyond linear classification models into non-linear, tree-based machine learning algorithms: **Decision Trees** and **Random Forests**.
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Machine learning modules from scikit-learn
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report, ConfusionMatrixDisplay

# Load and preprocess dataset
df = pd.read_csv('train.csv')
df['Age'] = df['Age'].fillna(df['Age'].median())
df['Embarked'] = df['Embarked'].fillna(df['Embarked'].mode()[0])
df['IsFemale'] = df['Sex'].map({'female': 1, 'male': 0})

features = ['Pclass', 'Age', 'Fare', 'SibSp', 'Parch', 'IsFemale']
X = df[features]
y = df['Survived']

# Stratified split to maintain class balance
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)

```
## 2. How Decision Trees Split Data (Gini Impurity)
A decision tree splits data by finding partitions that maximize the purity of the child nodes. This is measured using **Gini Impurity**:

 * **Gini = 0:** Perfect purity (all samples in a node belong to a single class).
 * **Gini = 0.5:** Maximum impurity (even 50/50 distribution).
## 3. Training an Unconstrained Decision Tree
When a decision tree is allowed to grow without limits (max_depth=None), it completely memorizes the training data, leading to severe overfitting.
```python
model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)

train_acc = accuracy_score(y_train, model.predict(X_train))
test_acc = accuracy_score(y_test, model.predict(X_test))

print(f"Tree Depth: {model.get_depth()}")
print(f"Number of Leaves: {model.get_n_leaves()}")
print(f"Train Accuracy: {train_acc*100:.2f}% (Overfitted / Memorized)")
print(f"Test Accuracy: {test_acc*100:.2f}%")

```
## 4. Tuning Tree Hyperparameters & Preventing Overfitting
To control overfitting, we regularized the tree by sweeping through values of max_depth to find the optimal balance between bias and variance.
```python
depths = range(1, 16)
train_scores = []
test_scores = []

for d in depths:
    dt = DecisionTreeClassifier(max_depth=d, random_state=42)
    dt.fit(X_train, y_train)
    train_scores.append(accuracy_score(y_train, dt.predict(X_train)))
    test_scores.append(accuracy_score(y_test, dt.predict(X_test)))

best_depth = depths[np.argmax(test_scores)]
print(f"Optimal Depth by Test Accuracy: {best_depth} (Accuracy: {max(test_scores)*100:.2f}%)")

# Visualizing Accuracy vs. Max Depth
plt.figure(figsize=(9, 5))
plt.plot(depths, train_scores, 'o-', color='#6366f1', label='Train Accuracy')
plt.plot(depths, test_scores, 's-', color='#ef4444', label='Test Accuracy')
plt.axvline(best_depth, color='grey', linestyle='--', label=f'Best Depth = {best_depth}')
plt.title("Decision Tree: Accuracy vs max_depth", fontsize=13, fontweight='bold')
plt.xlabel('max_depth')
plt.ylabel('Accuracy')
plt.xticks(depths)
plt.legend()
plt.grid()
plt.tight_layout()
plt.show()

```
## 5. Random Forests (Ensemble Methods)
A single decision tree often suffers from high variance. **Random Forests** solve this by building an ensemble of many decision trees using **Bagging** (Bootstrap Aggregating) and feature subspace sampling, then averaging their collective votes.
```python
rf = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42, n_jobs=-1)
rf.fit(X_train, y_train)

y_pred_rf = rf.predict(X_test)
rf_train_acc = accuracy_score(y_train, rf.predict(X_train))
rf_test_acc = accuracy_score(y_test, y_pred_rf)
rf_cv = cross_val_score(rf, X_train, y_train, cv=5, scoring='accuracy')

print(f"Random Forest Train Accuracy: {rf_train_acc*100:.2f}%")
print(f"Random Forest Test Accuracy: {rf_test_acc*100:.2f}%")
print(f"5-fold CV Mean Accuracy: {rf_cv.mean()*100:.2f}% (+/- {rf_cv.std()*100:.2f}%)")

print('\nRandom Forest Classification Report:')
print(classification_report(y_test, y_pred_rf, target_names=['Died', 'Survived']))

```
## 6. Grand Classifier Comparison
We compared the performance of **Logistic Regression**, the **Tuned Decision Tree**, and the **Random Forest** classifier using test accuracy and cross-validation scores.
```python
classifiers = {
    'Logistic Regression': LogisticRegression(max_iter=1000, random_state=42).fit(X_train, y_train),
    'Decision Tree (tuned)': DecisionTreeClassifier(max_depth=best_depth, random_state=42).fit(X_train, y_train),
    'Random Forest': RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42, n_jobs=-1).fit(X_train, y_train)
}

summary = []
for name, clf in classifiers.items():
    pred = clf.predict(X_test)
    acc = accuracy_score(y_test, pred)
    cv = cross_val_score(clf, X_train, y_train, cv=5, scoring='accuracy').mean()
    summary.append({'Model': name, 'Test Accuracy': acc, 'CV Accuracy': cv})

summary_df = pd.DataFrame(summary)
print('Classifier Performance Comparison:')
print('=' * 55)
print(summary_df.to_string(index=False))
print('=' * 55)

# Bar chart comparison
plt.figure(figsize=(8, 4))
colors = ['#94a3b8', '#f59e0b', '#6366f1']
bars = plt.bar(summary_df['Model'], summary_df['Test Accuracy'], color=colors, width=0.45, edgecolor='white')

for bar in bars:
    plt.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.005, 
             f'{bar.get_height()*100:.2f}%', ha='center', va='bottom', fontsize=10, fontweight='bold')

plt.title('Classifier Performance Comparison (Test Accuracy)', fontsize=13, fontweight='bold')
plt.ylabel('Accuracy')
plt.ylim(0.65, 0.85)
plt.tight_layout()
plt.show()

```
### 💡 Key Takeaways from Day 16:
 1. **Decision Trees:** Intuitive and easy to interpret via visualization, but prone to high variance and overfitting if left unconstrained.
 2. **Hyperparameter Tuning:** Restricting max_depth regularizes tree models, cutting down on memorization noise and improving generalization on unseen test data.
 3. **Random Forests:** Combines multiple bootstrapped trees via ensemble voting to stabilize predictions and enhance robustness across cross-validation splits.
