# Summer Training Daily Dairy: Day 23 

### 1. Introduction to Natural Language Processing (NLP)

Natural Language Processing (NLP) is a branch of Artificial Intelligence that enables computers to understand, process, and analyze human language.

Applications:

- Spam Detection
- Chatbots
- Sentiment Analysis
- Machine Translation
- Text Classification

<details>
<summary><strong>Program 1: Importing Required Libraries</strong></summary>

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
from sklearn.metrics import (
    accuracy_score,
    confusion_matrix,
    classification_report,
    ConfusionMatrixDisplay
)
```

</details>

---

### 2. Text Preprocessing

Raw text contains unnecessary information that must be cleaned before training Machine Learning models.

The preprocessing steps performed were:

- Lowercasing
- Tokenization
- Removing Punctuation
- Removing Stop Words
- Stemming

<details>
<summary><strong>Program 2: Downloading NLTK Resources</strong></summary>

```python
import os
import string
import warnings

warnings.filterwarnings('ignore')

nltk.download('stopwords')
nltk.download('punkt')
nltk.download('punkt_tab')

print("All libraries loaded and NLTK resources downloaded successfully!")
```

</details>

<details>
<summary><strong>Program 3: Demonstrating Text Preprocessing Steps</strong></summary>

```python
sample_text = "Hello World! We are learning text preprocessing today!"

print("Original Text:", sample_text)

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

stemmed_tokens = [
    stemmer.stem(word)
    for word in tokens_no_stopwords
]

clean_sentence = " ".join(stemmed_tokens)

print(clean_sentence)
```

</details>

<details>
<summary><strong>Program 6: Creating Text Preprocessing Function</strong></summary>

```python
def preprocess_text(text):

    text = text.lower()

    tokens = word_tokenize(text)

    tokens = [
        word
        for word in tokens
        if word not in string.punctuation
    ]

    stop_words = set(
        stopwords.words('english')
    )

    tokens = [
        word
        for word in tokens
        if word not in stop_words
    ]

    stemmer = PorterStemmer()

    stemmed = [
        stemmer.stem(word)
        for word in tokens
    ]

    return " ".join(stemmed)
```

</details>

<details>
<summary><strong>Program 7: Cleaning SMS Messages</strong></summary>

```python
print(
    "Cleaning all SMS messages..."
)

df['clean_text'] = df['text'].apply(
    preprocess_text
)

print("Preprocessing complete!")

print(df['clean_text'].head())
```

</details>

---

### 3. Lowercasing

All text is converted into lowercase to ensure consistency.

Example:

```text
Hello World
```

becomes

```text
hello world
```

---

### 4. Tokenization

Tokenization breaks a sentence into individual words called tokens.

Example:

```text
"I love AI"
```

becomes

```text
["I", "love", "AI"]
```

---

### 5. Removing Punctuation

Punctuation marks such as:

```text
. , ! ? : ; ( )
```

are removed because they usually do not contribute to text meaning.

---

### 6. Stop Word Removal

Common words such as:

- the
- is
- are
- of
- in

are removed to reduce unnecessary information.

---

### 7. Stemming

Stemming converts words into their root form.

Examples:

```text
running → run
playing → play
studies → studi
```

Used using:

```python
PorterStemmer()
```

---

### 8. Text Vectorization

Machine Learning algorithms cannot understand text directly.

Text must be converted into numerical vectors.

Methods covered:

- Bag of Words (Count Vectorizer)
- TF-IDF Vectorizer

<details>
<summary><strong>Program 4: Bag of Words and TF-IDF Representation</strong></summary>

```python
toy_corpus = [
    "The cat chased the mouse.",
    "The dog chased the cat.",
    "The bird sang in the tree."
]

count_vect = CountVectorizer()

bow_matrix = count_vect.fit_transform(
    toy_corpus
)

df_bow = pd.DataFrame(
    bow_matrix.toarray(),
    columns=count_vect.get_feature_names_out()
)

display(df_bow)

tfidf_vect = TfidfVectorizer()

tfidf_matrix = tfidf_vect.fit_transform(
    toy_corpus
)

df_tfidf = pd.DataFrame(
    tfidf_matrix.toarray(),
    columns=tfidf_vect.get_feature_names_out()
)

display(df_tfidf.round(3))
```

</details>

---

### 9. Bag of Words (BoW)

Bag of Words counts how many times each word appears in a document.

Used using:

```python
CountVectorizer()
```

---

### 10. TF-IDF

TF-IDF (Term Frequency-Inverse Document Frequency) gives higher importance to meaningful words while reducing the importance of very common words.

Used using:

```python
TfidfVectorizer()
```

---

### 11. SMS Spam Dataset

The SMS Spam Collection dataset contains two classes:

- Ham (Normal Message)
- Spam (Unwanted Message)

The labels were converted into binary values:

- Ham → 0
- Spam → 1

<details>
<summary><strong>Program 5: Loading SMS Spam Dataset</strong></summary>

```python
df = pd.read_csv(
    "spam.csv",
    encoding="latin-1"
)

df = df[
    ['v1','v2']
].rename(
    columns={
        'v1':'label',
        'v2':'text'
    }
)

df['is_spam'] = df['label'].map({
    'ham':0,
    'spam':1
})

print(df.head())
```

</details>

---

### 12. Train-Test Split

The dataset was divided into:

- 80% Training Data
- 20% Testing Data

The **stratify** parameter was used to maintain the same class distribution in both datasets.

<details>
<summary><strong>Program 8: Splitting Dataset and TF-IDF Vectorization</strong></summary>

```python
X_train, X_test, y_train, y_test = train_test_split(
    df['clean_text'],
    df['is_spam'],
    test_size=0.20,
    random_state=42,
    stratify=df['is_spam']
)

tfidf = TfidfVectorizer(
    max_features=2500
)

X_train_tfidf = tfidf.fit_transform(
    X_train
)

X_test_tfidf = tfidf.transform(
    X_test
)

print(
    f"Train size: {X_train.shape[0]}"
)

print(
    f"Test size: {X_test.shape[0]}"
)
```

</details>

---

## Key Learnings

- Learned the fundamentals of Natural Language Processing.
- Performed complete text preprocessing.
- Understood Lowercasing, Tokenization, Stop Word Removal, and Stemming.
- Learned Bag of Words and TF-IDF feature extraction.
- Loaded and explored the SMS Spam dataset.
- Converted text into numerical vectors for Machine Learning.
- Prepared the dataset for spam classification.

## Conclusion

Day 23 introduced Natural Language Processing (NLP) techniques used in Machine Learning. Raw text was cleaned using preprocessing techniques, transformed into numerical representations using Bag of Words and TF-IDF, and prepared for training an SMS Spam Detection model.
