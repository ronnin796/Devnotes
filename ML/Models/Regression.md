#MLmodels #ML #Regression #supervised

## What is Regression?

- Regression is a **supervised learning technique** used to predict **continuous** numeric values.
- It models the relationship between a **dependent variable (target)** and one or more **independent variables (features)**.
- The goal is to **fit a function** to the data to **minimize error** between predicted and actual values.

E.g., Predicting house prices, temperature, or salary.

---

## Types of Regression

- **Linear Regression** – Predicts using a straight line.
- **Polynomial Regression** – Models curved relationships.
- **Ridge / Lasso Regression** – Regularized linear models to prevent overfitting.
- **Logarithmic / Exponential Regression** – Non-linear relationships.

---

## Key Concepts

- **Loss Function**: Typically uses **Mean Squared Error (MSE)** to measure prediction accuracy.
- **Overfitting**: When the model learns noise; solved via regularization or more data.
- **R² Score**: Measures how well the model explains the variance in the data (1.0 is perfect).

---

## Real-World Analogy

> Predicting the **height of a plant** based on the number of days it has been growing.

---

## To create a Regression model, we need:

- Labeled data with numeric targets
- A hypothesis function (e.g., `y = mx + b`)
- A loss function (e.g., MSE)
- An optimizer (e.g., gradient descent)
```
python
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers

# Sample Data (X: size in sq ft, y: price in $1000s)
X = np.array([500, 750, 1000, 1250, 1500], dtype=float)
y = np.array([150, 200, 250, 300, 350], dtype=float)

# Build model
model = keras.Sequential([
    layers.Dense(units=1, input_shape=[1])
])

# Compile model
model.compile(optimizer='adam', loss='mean_squared_error')

# Train model
model.fit(X, y, epochs=500, verbose=0)

# Predict
print(model.predict([1600]))
```