#ML #ModelEvaluation #accuracy #precision #recall #F1score
# 📊 Model Evaluation Metrics

Use these metrics to evaluate how well a classification model is performing.

---

## 📌 Confusion Matrix

|              | Predicted Positive | Predicted Negative |
|--------------|--------------------|--------------------|
| Actual Positive | ✅ True Positive (TP)  | ❌ False Negative (FN) |
| Actual Negative | ❌ False Positive (FP) | ✅ True Negative (TN)  |

---

## ✅ Accuracy

- **Formula**:  
  $$
  \text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}
  $$

- **Meaning**:  
  The proportion of total correct predictions.

- ✅ Good when: Classes are **balanced**.

- ❌ Bad when: Classes are **imbalanced** (e.g., 95% Negative, 5% Positive).

---

## 🎯 Precision

- **Formula**:  
  $$
  \text{Precision} = \frac{TP}{TP + FP}
  $$

- **Meaning**:  
  Out of all predicted positives, how many were actually correct?

- ✅ Useful when: **False positives** are costly (e.g., spam detection).

---

## 📥 Recall (Sensitivity / True Positive Rate)

- **Formula**:  
  $$
  \text{Recall} = \frac{TP}{TP + FN}
  $$

- **Meaning**:  
  Out of all actual positives, how many did we correctly identify?

- ✅ Useful when: **False negatives** are costly (e.g., disease detection).

---

## ⚖️ F1 Score

- **Formula**:  
  $$
  \text{F1} = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
  $$

- **Meaning**:  
  Harmonic mean of Precision and Recall. A balance between them.

- ✅ Use when: You need a **balance** between precision and recall.

---

## 🧠 Quick Summary Table

| Metric    | Formula                                         | Best for...                            |
| --------- | ----------------------------------------------- | -------------------------------------- |
| Accuracy  | (TP + TN) / (TP + TN + FP + FN)                 | Balanced datasets                      |
| Precision | TP / (TP + FP)                                  | Avoiding False Positives               |
| Recall    | TP / (TP + FN)                                  | Avoiding False Negatives               |
| F1 Score  | 2 × (Precision × Recall) / (Precision + Recall) | Trade-off between Precision and Recall |

---

## 📌 Bonus: Macro vs Micro Averages (for multi-class)

- **Micro**: Calculates metrics **globally** (total TP, FP, FN).
- **Macro**: Calculates metrics **per class**, then takes the average (equal weight to all classes).

