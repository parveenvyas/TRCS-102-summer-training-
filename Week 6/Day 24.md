# Summer Training Daily Dairy: Day 24 
## Email Spam Detection using NLP and Naive Bayes

## Topics Covered

### 1. Introduction to Natural Language Processing (NLP)

Natural Language Processing (NLP) enables computers to understand, process, and analyze human language.

Applications include:

- Spam Detection
- Sentiment Analysis
- Chatbots
- Language Translation
- Text Classification

<details>
<summary><strong>Program 1: Installing NLTK</strong></summary>

<div markdown="1">

```python
%pip install nltk
```

</div>

</details>

<details>
<summary><strong>Program 2: Importing Required Libraries</strong></summary>

<div markdown="1">

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
from nltk.stem import PorterStemmer

from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import classification_report, confusion_matrix, accuracy_score, ConfusionMatrixDisplay

import os
import string
import warnings
warnings.filterwarnings('ignore')
```

</div>

</details>

---

### 2. Text Preprocessing

Before training a machine learning model, text must be cleaned.

The preprocessing pipeline includes:

- Lowercasing
- Tokenization
- Removing Punctuation
- Removing Stop Words
- Stemming
- Lemmatization

<details>
<summary><strong>Program 3: Downloading NLTK Resources</strong></summary>

<div markdown="1">

```python
nltk.download('stopwords')
nltk.download('punkt')
nltk.download('punkt_tab')
```

</div>

</details>

<details>
<summary><strong>Program 4: Demonstrating Text Preprocessing Steps</strong></summary>

<div markdown="1">

```python
sample_text = "Hello World! We are learning text preprocessing today!"

text_lower = sample_text.lower()

tokens = word_tokenize(text_lower)

tokens_no_punct = [
    word for word in tokens
    if word not in string.punctuation
]

stop_words = set(stopwords.words('english'))

tokens_no_stopwords = [
    word for word in tokens_no_punct
    if word not in stop_words
]

stemmer = PorterStemmer()

tokens_stemmed = [
    stemmer.stem(word)
    for word in tokens_no_stopwords
]

cleaned_text = " ".join(tokens_stemmed)

print(cleaned_text)
```

</div>

</details>

<details>
<summary><strong>Program 7: Text Cleaning Pipeline</strong></summary>

<div markdown="1">

```python
def preprocess_text(text):

    text = text.lower()

    tokens = word_tokenize(text)

    tokens = [
        word
        for word in tokens
        if word not in string.punctuation
    ]

    stop_words = set(stopwords.words("english"))

    tokens = [
        word
        for word in tokens
        if word not in stop_words
    ]

    stemmer = PorterStemmer()

    tokens = [
        stemmer.stem(word)
        for word in tokens
    ]

    return " ".join(tokens)

df["clean_text"] = df["text"].apply(preprocess_text)
```

</div>

</details>

---

### 3. Lowercasing

Converts all text into lowercase to avoid treating the same word differently.

Example:

```python
"Hello" → "hello"
```

---

### 4. Tokenization

Splits sentences into individual words (tokens).

Example:

```python
"I love AI"

↓

["I", "love", "AI"]
```

---

### 5. Stop Word Removal

Common words such as:

- the
- is
- and
- are

are removed because they usually do not contribute meaningful information.

---

### 6. Stemming

Reduces words to their root form.

Example:

```python
learning
learned
learner

↓

learn
```

---

### 7. Lemmatization

Converts words into meaningful dictionary words.

Example:

```python
better

↓

good
```

Lemmatization generally produces cleaner words than stemming.

<details>
<summary><strong>Program 12: Lemmatization Pipeline and Performance Comparison</strong></summary>

<div markdown="1">

```python
from nltk.stem import WordNetLemmatizer

nltk.download("wordnet")
nltk.download("omw-1.4")

def preprocess_with_lemmatizer(text):

    text = text.lower()

    tokens = word_tokenize(text)

    tokens = [
        word
        for word in tokens
        if word not in string.punctuation
    ]

    stop_words = set(stopwords.words("english"))

    tokens = [
        word
        for word in tokens
        if word not in stop_words
    ]

    lemmatizer = WordNetLemmatizer()

    tokens = [
        lemmatizer.lemmatize(word)
        for word in tokens
    ]

    return " ".join(tokens)

df["clean_lem"] = df["text"].apply(
    preprocess_with_lemmatizer
)

X_train_lem, X_test_lem, y_train_lem, y_test_lem = train_test_split(
    df["clean_lem"],
    df["is_spam"],
    test_size=0.20,
    random_state=42,
    stratify=df["is_spam"]
)

tfidf_lem = TfidfVectorizer(
    max_features=2500
)

X_train_tfidf_lem = tfidf_lem.fit_transform(
    X_train_lem
)

X_test_tfidf_lem = tfidf_lem.transform(
    X_test_lem
)

nb_lem = MultinomialNB()

nb_lem.fit(
    X_train_tfidf_lem,
    y_train_lem
)

y_pred_lem = nb_lem.predict(
    X_test_tfidf_lem
)

acc_lem = accuracy_score(
    y_test_lem,
    y_pred_lem
)

print(acc_lem)
```

</div>

</details>

---

### 8. Text Vectorization

Machine Learning models cannot understand text directly.

Text is converted into numbers using:

- Bag of Words (CountVectorizer)
- TF-IDF (Term Frequency-Inverse Document Frequency)

<details>
<summary><strong>Program 5: Bag of Words and TF-IDF Demonstration</strong></summary>

<div markdown="1">

```python
toy_corpus = [
    "The cat chased the Mouse.",
    "The dog chased the cat.",
    "The bird sang in the tree."
]

count_vect = CountVectorizer()

bow_matrix = count_vect.fit_transform(toy_corpus)

df_bow = pd.DataFrame(
    bow_matrix.toarray(),
    columns=count_vect.get_feature_names_out()
)

display(df_bow)

tfidf_vect = TfidfVectorizer()

tfidf_matrix = tfidf_vect.fit_transform(toy_corpus)

df_tfidf = pd.DataFrame(
    tfidf_matrix.toarray(),
    columns=tfidf_vect.get_feature_names_out()
)

display(df_tfidf.round(3))
```

</div>

</details>

---

### 9. Naive Bayes Classifier

Multinomial Naive Bayes is commonly used for text classification because it works efficiently with word frequencies.

Applications:

- Spam Detection
- News Classification
- Sentiment Analysis

<details>
<summary><strong>Program 6: Loading Spam Dataset</strong></summary>

<div markdown="1">

```python
df = pd.read_csv(
    "spam.csv",
    encoding="latin-1"
)

df = df[
    ["v1", "v2"]
].rename(
    columns={
        "v1": "label",
        "v2": "text"
    }
)

df["is_spam"] = df["label"].map(
    {
        "ham": 0,
        "spam": 1
    }
)

display(df.head())
```

</div>

</details>

<details>
<summary><strong>Program 9: Training Naive Bayes Model</strong></summary>

<div markdown="1">

```python
nb_classifier = MultinomialNB()

nb_classifier.fit(
    X_train_tfidf,
    y_train
)

y_pred = nb_classifier.predict(
    X_test_tfidf
)

accuracy = accuracy_score(
    y_test,
    y_pred
)

print(accuracy)
```

</div>

</details>

<details>
<summary><strong>Program 10: Confusion Matrix and Classification Report</strong></summary>

<div markdown="1">

```python
cm = confusion_matrix(
    y_test,
    y_pred
)

disp = ConfusionMatrixDisplay(
    confusion_matrix=cm,
    display_labels=["Ham", "Spam"]
)

disp.plot(cmap="Blues")

plt.grid(False)

plt.show()

print(
    classification_report(
        y_test,
        y_pred,
        target_names=[
            "Ham",
            "Spam"
        ]
    )
)
```

</div>

</details>

<details>
<summary><strong>Program 11: Predicting Custom Messages</strong></summary>

<div markdown="1">

```python
custom_texts = [
    "Hey, are we still meeting today?",
    "Congratulations! You won $1000.",
    "Call me back.",
    "Reset your password immediately."
]

cleaned_custom = [
    preprocess_text(text)
    for text in custom_texts
]

custom_tfidf = tfidf.transform(
    cleaned_custom
)

predictions = nb_classifier.predict(
    custom_tfidf
)

for msg, pred in zip(
    custom_texts,
    predictions
):
    print(msg)
    print(
        "SPAM"
        if pred == 1
        else "HAM"
    )
```

</div>

</details>

---

### 10. TF-IDF

TF-IDF assigns higher importance to words that appear frequently within one document but not across every document.

<details>
<summary><strong>Program 8: TF-IDF Feature Extraction</strong></summary>

<div markdown="1">

```python
X_train, X_test, y_train, y_test = train_test_split(
    df["clean_text"],
    df["is_spam"],
    test_size=0.20,
    random_state=42,
    stratify=df["is_spam"]
)

tfidf = TfidfVectorizer(
    max_features=2500
)

X_train_tfidf = tfidf.fit_transform(X_train)

X_test_tfidf = tfidf.transform(X_test)
```

</div>

</details>

---

## Key Learnings

- Learned the complete NLP preprocessing pipeline.
- Understood tokenization, stop-word removal, stemming, and lemmatization.
- Learned Bag of Words and TF-IDF vectorization.
- Built a Naive Bayes spam detection model.
- Evaluated the model using confusion matrix and classification report.
- Predicted spam for custom messages.
- Compared stemming and lemmatization approaches.

---

## Conclusion

Day 24 focused on applying Natural Language Processing techniques to email/SMS spam detection. The workflow included text preprocessing, TF-IDF feature extraction, Naive Bayes classification, custom message prediction, and comparing stemming with lemmatization to understand different approaches to text normalization.
