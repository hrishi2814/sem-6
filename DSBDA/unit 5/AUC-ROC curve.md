## 📈 What is the ROC Curve?

**ROC (Receiver Operating Characteristic) Curve** is a graph that shows the performance of a **binary classification model** at different threshold settings.

### 📊 What It Plots:

- **X-axis:** False Positive Rate (FPR)
    
    FPR=FPFP+TN\text{FPR} = \frac{FP}{FP + TN}
- **Y-axis:** True Positive Rate (TPR) a.k.a **Recall**
    
    TPR=TPTP+FN\text{TPR} = \frac{TP}{TP + FN}

### ✅ Goal:

Show how the **true positives** increase while trying to avoid **false positives** as the classification threshold changes.

---

## 🔹 What is AUC?

**AUC (Area Under the Curve)** is the **area under the ROC curve**.

- **Range:** 0 to 1
    
- **Higher AUC = Better model performance**
    

|AUC Score|Interpretation|
|---|---|
|1.0|Perfect model|
|0.9–1.0|Excellent|
|0.8–0.9|Good|
|0.7–0.8|Fair|
|0.6–0.7|Poor|
|0.5|No skill (random guessing)|

---

## 🧠 Why Use ROC-AUC?

- Works well even with **imbalanced datasets**
    
- Tells how well the model can **distinguish between classes**
    
- Doesn't depend on a fixed threshold like accuracy does
    

---

## 🎯 Example

Suppose a model outputs the following **probability scores** for a spam email (1 = spam):

|Email|Actual|Predicted Probability|
|---|---|---|
|1|1|0.95|
|2|0|0.70|
|3|1|0.60|
|4|0|0.40|

By changing the threshold (e.g., 0.5, 0.6, 0.7...), we get different TPR and FPR values, and we plot them on the ROC curve.

---

## 🛠 Python Code to Plot ROC Curve and AUC

```python
from sklearn.metrics import roc_curve, roc_auc_score
import matplotlib.pyplot as plt

y_true = [1, 0, 1, 0]  # actual labels
y_scores = [0.95, 0.70, 0.60, 0.40]  # predicted probabilities

fpr, tpr, thresholds = roc_curve(y_true, y_scores)
auc_score = roc_auc_score(y_true, y_scores)

plt.plot(fpr, tpr, label=f'AUC = {auc_score:.2f}')
plt.plot([0, 1], [0, 1], 'k--')  # diagonal line for random model
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve')
plt.legend()
plt.grid(True)
plt.show()
```

---

## 🧾 Summary

- **ROC Curve** shows TPR vs FPR at various thresholds.
    
- **AUC** measures the overall ability of the model to discriminate between classes.
    
- Higher AUC = better model.
    
- Especially useful when **class distribution is imbalanced**.
    

---

Let me know if you want the same concept explained for **multi-class classification** or **precision-recall curves**!