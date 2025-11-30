**Overfitting** happens when a machine learning model learns the **training data too well**, including its **noise, random fluctuations, or outliers**, instead of learning the general pattern that applies to new, unseen data.

Think of it like a student who **memorizes** answers to past exam questions instead of **understanding the concepts** — they score high on practice tests but fail when the questions change.

---

### 🔍 Example:

Let’s say you’re training a model to predict house prices.

- **Underfitting:**  
    Model is too simple — predicts every house has the same price.  
    → Poor performance on both training and test data.
    
- **Good fit:**  
    Model learns meaningful patterns like “bigger houses cost more” or “location matters.”  
    → Performs well on both training and test data.
    
- **Overfitting:**  
    Model memorizes the exact training examples (e.g., remembers specific house IDs and their prices).  
    → Excellent training accuracy, terrible test accuracy.
    

---

### 📈 Symptoms:

- Very **low training error**
    
- Very **high validation/test error**
    
- Model performance drops sharply on unseen data
    

---

### 🛠️ Common Ways to Prevent Overfitting:

1. **Train–Test Split** / **Cross-Validation** – Always test on unseen data.
    
2. **Regularization** – Add penalties for overly complex models (e.g., L1/L2 regularization).
    
3. **Simplify the Model** – Fewer layers or parameters.
    
4. **Dropout** (in neural networks) – Randomly ignore neurons during training.
    
5. **Early Stopping** – Stop training when validation loss stops improving.
    
6. **Data Augmentation** – Make more varied training examples.
    
7. **Increase Training Data** – The more real examples, the better the model generalizes.