#MLmodels #ML #Classification #supervised
## What is Classification?

- Classification is a **supervised learning** method used to assign **labels** (classes) to input data.
- It predicts **discrete categories** instead of continuous values.

E.g., Spam vs Not Spam, Dog vs Cat, Pass vs Fail

---

## Types of Classification

- **Binary Classification** – Two classes (Yes/No, 0/1).
- **Multiclass Classification** – More than two classes (e.g., digits 0–9).
- **Multilabel Classification** – Multiple labels per instance (e.g., tags on a blog post).

---

## Key Concepts

- **Decision Boundary**: Divides different class regions in the feature space.
- **Confusion Matrix**: Visualizes true vs predicted labels.
- **Precision, Recall, F1 Score**: Measures model performance.

---

## Algorithms Used

- Logistic Regression
- Decision Trees
- Random Forest
- Support Vector Machine (SVM)
- Neural Networks (Softmax output)

---

## Real-World Analogy

> A teacher predicting whether a student will **pass or fail** based on study hours and attendance.

---

## To create a Classification model, we need:

- Labeled data with class categories
- Feature representation
- Loss function (e.g., cross-entropy)
- Classifier algorithm
```
python
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers

# Sample binary data (X: hours studied, y: pass=1, fail=0)
X = np.array([[1], [2], [3], [4], [5], [6]], dtype=float)
y = np.array([[0], [0], [0], [1], [1], [1]], dtype=float)

# Build model
model = keras.Sequential([
    layers.Dense(units=1, activation='sigmoid', input_shape=[1])
])

# Compile
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])

# Train
model.fit(X, y, epochs=500, verbose=0)

# Predict
print(model.predict([[2.5], [5.5]]))
```