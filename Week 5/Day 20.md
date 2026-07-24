

# Summer Training Diary – Day 20


# 📚 Topics Covered

## 1. BGR vs RGB

### Theory

OpenCV stores color images in **BGR** format.

Most other libraries like Matplotlib use **RGB**.

If an image is displayed without conversion, colors may appear incorrect.

---

## 2. Image Resizing

### Theory

Resizing changes the dimensions of an image.

Applications:

- Better visualization
- Standard input size
- Image preprocessing

---

## 3. Grayscale to BGR Conversion

### Code

```python
color_digit = cv2.cvtColor(
    gray_image,
    cv2.COLOR_GRAY2BGR
)
```

### Explanation

Converts a grayscale image into a three-channel color image.

### Learning

Learned how OpenCV represents color images.

---

## 4. Image Resizing

### Code

```python
digit_resized = cv2.resize(
    digit_small,
    (32,32),
    interpolation=cv2.INTER_CUBIC
)
```

### Explanation

Resizes an image from **8×8** to **32×32** pixels.

### Learning

Resizing improves image visibility without changing the original content.

---

## 5. Image Thresholding

### Theory

Thresholding converts a grayscale image into a binary image.

Rule:

- Pixel > Threshold → White
- Pixel ≤ Threshold → Black

Applications:

- OCR
- Document Scanning
- Object Detection

---

## 6. Binary Threshold

### Code

```python
_, thresh = cv2.threshold(
    image,
    100,
    255,
    cv2.THRESH_BINARY
)
```

### Explanation

Converts the grayscale image into a black-and-white image.

### Learning

Thresholding simplifies image analysis.

---

## 7. Contour Detection

### Theory

Contours are the boundaries of objects present inside an image.

Applications:

- Shape Detection
- Character Recognition
- Object Counting

---

## 8. Find Contours

### Code

```python
contours, _ = cv2.findContours(
    thresh,
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)
```

### Explanation

Finds the outline of the handwritten digit.

### Learning

Contours help identify objects inside an image.

---

## 9. Feature Extraction

### Code

```python
X_features = X_raw.reshape(len(X_raw), -1)
```

### Explanation

Converts every **8×8** image into a **64-dimensional feature vector**.

### Learning

Machine learning algorithms require numerical feature vectors instead of image matrices.

---

## 10. K-Nearest Neighbors (KNN)

### Theory

KNN is a supervised machine learning algorithm.

Working:

1. Store training data.
2. Find the K nearest neighbors.
3. Predict the majority class.

---

## 11. Train KNN Model

### Code

```python
model = KNeighborsClassifier()
model.fit(X_train, y_train)
```

### Explanation

Trains the classifier using the training dataset.

### Learning

The model learns patterns from handwritten digits.

---

## 12. Predict Handwritten Digit

### Code

```python
prediction = model.predict(test_image)
```

### Explanation

Predicts the digit present in the given image.

### Learning

Combined image preprocessing and machine learning to recognize handwritten digits.

---

# ✅ Learning Outcome

By the end of Day 20, I learned:

- BGR vs RGB color formats
- Image resizing
- Thresholding
- Contour detection
- Feature extraction
- K-Nearest Neighbors (KNN)
- Handwritten digit recognition using OpenCV and Scikit-learn

The session provided practical experience in integrating image processing with machine learning to build a simple computer vision application.
