# 📅 Summer Training Diary – Day 19


# 📚 Topics Covered

## 1. Introduction to OpenCV

OpenCV (Open Source Computer Vision Library) is an open-source library developed for computer vision and image processing. It provides a large collection of functions that help in reading, processing, analyzing, and displaying images and videos.

### Applications of OpenCV
- Face Detection
- Object Detection
- Image Filtering
- Medical Image Analysis
- Self-driving Cars
- OCR (Optical Character Recognition)
- Robotics

---

## 2. Installing OpenCV

### Code

```python
%pip install opencv-python
```

### Explanation

This command installs the OpenCV library in the Python environment.

### Learning

Learned how to install external Python libraries using pip.

---

## 3. Importing Required Libraries

### Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_digits
```

### Explanation

- `cv2` → OpenCV library
- `numpy` → Numerical operations
- `matplotlib` → Display images
- `load_digits()` → Loads handwritten digits dataset

### Learning

Different libraries are combined to perform image processing and machine learning tasks.

---

## 4. Loading the Dataset

### Code

```python
digits = load_digits()

X_raw = digits.images
y_raw = digits.target
```

### Explanation

The handwritten digits dataset is loaded.

- `X_raw` stores images.
- `y_raw` stores labels (0–9).

### Theory

A dataset is a collection of data used for training and testing machine learning models.

---

## 5. Understanding Image Representation

### Theory

A digital image is represented as a matrix of numbers.

Each number represents one pixel.

Example:

```
0  5  10
8 12 15
0  6  14
```

Each value represents the brightness of that pixel.

---

## 6. Pixel Intensity

Pixel intensity determines how bright a pixel appears.

For grayscale images:

- 0 → Black
- Higher values → Brighter pixels
- Maximum value → White

Understanding pixel values is the foundation of image processing.

---

## 7. Display Dataset Information

### Code

```python
print(len(X_raw))
print(X_raw[0].shape)
```

### Explanation

Displays

- Total number of images
- Size of each image

### Output

```
1797
(8,8)
```

### Learning

Each handwritten digit is stored as an 8×8 matrix.

---

## 8. Display Pixel Matrix

### Code

```python
sample_digit = X_raw[500]
print(sample_digit.astype(int))
```

### Explanation

Prints all pixel values of one handwritten digit.

### Learning

Images are actually matrices containing numerical pixel values.

---
