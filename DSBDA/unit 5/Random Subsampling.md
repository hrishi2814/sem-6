
## 🎲 What is Random Subsampling?

**Random Subsampling** is a **model validation technique** used to evaluate the performance of a machine learning algorithm by **randomly splitting the dataset into training and testing sets multiple times**.

Unlike **k-fold cross-validation**, where the dataset is divided into _k_ fixed folds, random subsampling performs repeated random splits and evaluates the model on each.

---

## ⚙️ How It Works (Steps):

1. **Randomly split** the dataset into:
    
    - **Training set**
        
    - **Testing set**  
        (e.g., 70% train, 30% test)
        
2. **Train the model** on the training set.
    
3. **Evaluate** the model on the testing set.
    
4. **Repeat** this process **N times** (e.g., 10 or 100 times), each with a different random split.
    
5. **Average the results** (e.g., accuracy, F1-score) to get an overall performance estimate.
    

---

## 🔍 Key Features

|Feature|Description|
|---|---|
|Validation Technique|Supervised (used for model evaluation)|
|Type|Repeated Random Train-Test Splits|
|Splits|User-defined % for train/test (e.g., 80/20)|
|Repeats|User-defined number of repetitions|
|Test samples reused|Yes (test samples may repeat across iterations)|

---

## ✅ Advantages

- Simple to implement
    
- Allows flexibility in train-test split ratio
    
- Reduces variance in evaluation by averaging multiple results
    
- Less biased than a single train-test split
    

---

## ❌ Disadvantages

- Some data points might never be used for testing
    
- Some might be used multiple times
    
- Less efficient than **stratified k-fold**, especially with imbalanced data
    

---

## 🛠 Python Example using `sklearn`

```python
from sklearn.model_selection import ShuffleSplit
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris
from sklearn.metrics import accuracy_score

# Load dataset
X, y = load_iris(return_X_y=True)

# Define random subsampling strategy
ss = ShuffleSplit(n_splits=5, test_size=0.3, random_state=42)

model = LogisticRegression()

scores = []

for train_index, test_index in ss.split(X):
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
    
    model.fit(X_train, y_train)
    y_pred = model.predict(X_test)
    acc = accuracy_score(y_test, y_pred)
    scores.append(acc)

print(f"Accuracy over 5 iterations: {scores}")
print(f"Average Accuracy: {sum(scores)/len(scores):.2f}")
```

---

## 🎯 When to Use Random Subsampling?

- When you want a **quick, robust estimate** of model performance.
    
- When dataset size is **sufficiently large**.
    
- When **k-fold cross-validation** is too computationally expensive.
    

---

## 🧠 Summary

- **Random Subsampling** is a validation method using repeated random train-test splits.
    
- Useful for performance estimation while avoiding overfitting to a particular split.
    
- Results are averaged across multiple iterations to provide a **more stable evaluation**.
    

---

Let me know if you'd like a comparison table between random subsampling and k-fold cross-validation!