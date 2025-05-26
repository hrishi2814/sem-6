## 📘 What is K-Fold Cross Validation?

**K-Fold Cross Validation** is a model validation technique used to assess how a machine learning model will generalize to an independent dataset. It is especially useful when data is limited.

---

## 🔄 How It Works:

1. The dataset is randomly divided into **k equal-sized subsets** called _folds_.
    
2. The model is trained and tested **k times**, each time:
    
    - Using **k−1 folds** for **training**
        
    - Using the **remaining 1 fold** for **testing**
        
3. Each fold gets a chance to be the test set **exactly once**.
    
4. The performance scores (e.g., accuracy, F1-score) from all k trials are **averaged** to get the final evaluation metric.
    

---

### 📌 Example with `k = 5`:

Suppose we have 100 data points:

- Split into 5 folds → 20 points in each fold
    
- Round 1: Train on folds 2–5, Test on fold 1
    
- Round 2: Train on folds 1,3–5, Test on fold 2
    
- ...
    
- Round 5: Train on folds 1–4, Test on fold 5
    

→ Final score = Average of the 5 test scores

---

## ✅ Advantages:

- **Better generalization estimate** than a single train-test split
    
- **Efficient use of data**: Every observation is used for both training and testing
    
- **Reduces overfitting** risk
    

---

## ❌ Disadvantages:

- **Computationally expensive** (train k times)
    
- **Not ideal for time-series data** (because of temporal dependency)
    

---

## 🛠 Python Example using `sklearn`

```python
from sklearn.model_selection import KFold
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris
from sklearn.metrics import accuracy_score
import numpy as np

# Load dataset
X, y = load_iris(return_X_y=True)

kf = KFold(n_splits=5, shuffle=True, random_state=42)
model = LogisticRegression()

scores = []

for train_index, test_index in kf.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)
    acc = accuracy_score(y_test, y_pred)
    scores.append(acc)

print(f"Scores: {scores}")
print(f"Average Accuracy: {np.mean(scores):.2f}")
```

---

## 🧠 Summary Table

|Feature|Description|
|---|---|
|Goal|Evaluate model's performance|
|Input|Dataset + number of folds (k)|
|Output|Average metric across k folds|
|Best for|Small or medium-sized datasets|
|Common values of k|5 or 10 (standard practice)|

---

## 🧭 When to Use K-Fold Cross Validation?

- When you want a **robust performance estimate**
    
- When the dataset is **not too large**
    
- When you want to **minimize bias** from a single data split
    

---

Let me know if you want a visual diagram or a comparison with other validation techniques like **Leave-One-Out (LOO)** or **Stratified K-Fold**!