# 📅 Summer Training - Daily Diary: Day 23

# 📚 Topics Covered

## 1. Introduction to Natural Language Processing (NLP)

Natural Language Processing (NLP) is a branch of Artificial Intelligence (AI) that enables computers to understand, analyze, process, and generate human language.

### Applications of NLP

- Email Spam Detection
- Sentiment Analysis
- Chatbots
- Machine Translation
- Text Summarization
- Search Engines
- Voice Assistants

---

## 2. Installing NLTK

### Code

```python
%pip install nltk
```

### Explanation

Installs the **Natural Language Toolkit (NLTK)** library, which provides tools for text processing.

### Learning

Learned how to install an NLP library in Python.

---

## 3. Importing Required Libraries

### Code

```python
import nltk
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Explanation

- **NLTK** → Text processing
- **Pandas** → Data handling
- **NumPy** → Numerical operations
- **Matplotlib & Seaborn** → Visualization

### Learning

Different libraries work together to perform NLP and machine learning tasks.

---

## 4. Downloading NLTK Resources

### Code

```python
nltk.download('stopwords')
nltk.download('punkt')
```

### Explanation

Downloads:

- Tokenizer
- Stopword dictionary

These resources are required for text preprocessing.

---

# Text Preprocessing

Text preprocessing converts raw text into a clean format suitable for machine learning.

---

## 5. Lowercasing

### Theory

Converts all characters into lowercase.

Example:

```
"Hello World"
```

↓

```
"hello world"
```

### Benefit

Treats "Hello" and "hello" as the same word.

---

## 6. Tokenization

### Theory

Tokenization splits a sentence into individual words.

Example

```
Hello World
```

↓

```
["hello", "world"]
```

### Learning

Machine learning models process tokens rather than complete sentences.

---

## 7. Removing Punctuation

### Theory

Removes punctuation marks such as:

```
.,!?;:
```

This reduces unnecessary information.

---

## 8. Removing Stopwords

### Theory

Stopwords are very common words that usually do not carry important meaning.

Examples

- the
- is
- am
- are
- of
- in

Removing them improves model efficiency.

---

## 9. Stemming

### Theory

Stemming converts words to their root form.

Examples

- playing → play
- running → run
- studies → studi

This reduces vocabulary size.

---

## 10. Complete Text Preprocessing Pipeline

### Code

```python
def preprocess_text(text):
```

### Explanation

The preprocessing function performs:

1. Lowercasing
2. Tokenization
3. Removing punctuation
4. Removing stopwords
5. Stemming

### Learning

Learned how raw text is transformed into clean text for machine learning.

---

# Text Vectorization

Machine learning algorithms cannot understand text directly.

Therefore, text is converted into numerical vectors.

---

## 11. Bag of Words (BoW)

### Theory

Bag of Words counts the number of times each word appears in a document.

Example

Sentence 1:

```
The cat chased the mouse
```

Sentence 2:

```
The dog chased the cat
```

Each sentence is represented using word frequencies.

### Advantages

- Simple
- Easy to implement

### Limitation

Does not consider word importance.

---

## 12. TF-IDF

### Theory

TF-IDF (Term Frequency–Inverse Document Frequency) gives higher importance to unique words and lower importance to very common words.

Advantages

- Better than Bag of Words
- Reduces the impact of common words

---

## 13. Bag of Words Code

### Code

```python
CountVectorizer()
```

### Explanation

Creates numerical vectors using word counts.

### Learning

Converted text into machine-readable numerical features.

---

## 14. TF-IDF Code

### Code

```python
TfidfVectorizer()
```

### Explanation

Creates weighted numerical vectors.

### Learning

Learned an advanced text vectorization technique.

---


# ✅ Learning Outcome

By the end of Day 23, I learned:

- Fundamentals of Natural Language Processing (NLP)
- Text preprocessing pipeline
- Lowercasing
- Tokenization
- Stopword removal
- Punctuation removal
- Stemming
- Bag of Words
- TF-IDF Vectorization

