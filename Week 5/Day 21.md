# 📅 Summer Training Diary – Day 21


# 📚 Topics Covered

## 1. Introduction to Customer Churn

Customer churn refers to customers who stop using a company's product or service. Predicting churn helps businesses identify customers who are likely to leave so that they can take preventive actions.

### Applications
- Telecom Companies
- Banks
- OTT Platforms
- Insurance
- E-commerce

---

## 2. Importing Required Libraries

### Code

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Explanation

- **Pandas** → Data loading and manipulation
- **NumPy** → Numerical computations
- **Matplotlib** → Data visualization
- **Seaborn** → Statistical visualization

### Learning

Learned how different Python libraries work together for data analysis and visualization.

---

## 3. Loading the Dataset

### Code

```python
df = pd.read_csv("customer_churn_nlp.csv")
```

### Explanation

Loads the customer churn dataset into a Pandas DataFrame.

### Learning

Learned how to import datasets from CSV files.

---

## 4. Exploratory Data Analysis (EDA)

### Theory

EDA is the process of exploring and understanding a dataset before building a machine learning model.

It helps to:
- Understand data distribution
- Detect missing values
- Find relationships between variables
- Identify patterns and outliers

---

## 5. Churn Distribution

### Code

```python
sns.countplot(data=df, x="Churn")
```

### Explanation

Displays the number of churned and retained customers.

### Learning

Understood whether the dataset is balanced or imbalanced.

---

## 6. Tenure Analysis

### Code

```python
sns.boxplot(data=df, x="Churn", y="Tenure")
```

### Explanation

Compares customer tenure with churn status.

### Learning

Observed how customer loyalty affects churn.

---

## 7. Monthly Charges Analysis

### Code

```python
sns.boxplot(data=df, x="Churn", y="MonthlyCharges")
```

### Explanation

Shows the relationship between monthly charges and customer churn.

### Learning

Higher monthly charges may increase the probability of churn.

---

## 8. Support Tickets Analysis

### Code

```python
sns.countplot(data=df, x="SupportTickets", hue="Churn")
```

### Explanation

Compares the number of support tickets raised by churned and retained customers.

### Learning

Customers with more complaints are more likely to leave.

---

## 9. Contract Type Analysis

### Code

```python
sns.countplot(data=df, x="Contract", hue="Churn")
```

### Explanation

Analyzes churn based on contract type.

### Learning

Long-term contracts usually have lower churn rates.

---

## 10. NLP (Natural Language Processing)

### Theory

Natural Language Processing (NLP) enables computers to understand and process human language.

In this project, customer feedback text is analyzed to understand customer satisfaction and behavior.

### Applications

- Sentiment Analysis
- Chatbots
- Text Classification
- Spam Detection
- Review Analysis

---

## 11. Display Customer Feedback

### Code

```python
for text in df[df["Churn"]==0]["CustomerFeedback"].head(3):
    print(text)
```

### Explanation

Displays sample feedback from retained customers.

### Learning

Learned how customer reviews provide useful insights for predicting churn.

---

## 12. Data Preprocessing

### Theory

Machine learning models require clean numerical data.

Preprocessing includes:
- Encoding categorical variables
- Handling missing values
- Feature engineering

---

## 13. One-Hot Encoding

### Code

```python
pd.get_dummies(df["Contract"], drop_first=True)
```

### Explanation

Converts categorical contract values into numerical columns.

### Learning

Machine learning algorithms cannot directly process text categories.

---

# ✅ Learning Outcome

By the end of Day 21, I learned:

- Customer churn prediction concepts
- Exploratory Data Analysis (EDA)
- Customer behavior analysis
- Data visualization
- Natural Language Processing basics
- Data preprocessing
- One-Hot Encoding

---
