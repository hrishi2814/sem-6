## 📊 What is K-Means Clustering?

**K-Means** is a popular **unsupervised machine learning algorithm** used to **partition a dataset into K distinct, non-overlapping clusters** based on feature similarity.

> It groups data points so that points within a cluster are more similar to each other than to points in other clusters.

---

## 🎯 Purpose of K-Means

- **Automatically group** data points based on patterns.
    
- Find **natural clusters** in unlabeled data.
    
- Reduce data complexity.
    

---

## ⚙️ How K-Means Works (Step-by-Step)

1. **Choose K (number of clusters)**.
    
2. **Initialize K centroids randomly**.
    
3. **Assign each point to the nearest centroid** (based on Euclidean distance).
    
4. **Update centroids** by calculating the mean of the points assigned to each cluster.
    
5. **Repeat steps 3–4** until:
    
    - Centroids don’t change, OR
        
    - Max iterations reached.
        

> This is an iterative optimization technique to **minimize the sum of squared distances (inertia)** between points and their cluster center.

---

## 🔢 Example

Suppose you have customer data with two features: **Annual Income** and **Spending Score**.

K-Means will:

- Find clusters like **Low Income-Low Spender**, **High Income-High Spender**, etc.
    
- Place centroids in the center of these clusters.
    

---

## 🧪 Simple Python Example

```python
from sklearn.cluster import KMeans
import pandas as pd

# Sample data
data = pd.DataFrame({
    'Income': [45, 38, 90, 85, 30, 70, 75, 25],
    'SpendingScore': [20, 22, 80, 90, 25, 75, 85, 15]
})

# Create KMeans model
kmeans = KMeans(n_clusters=2, random_state=0)
data['Cluster'] = kmeans.fit_predict(data)

# Show results
print(data)
```

---

## 🧠 Choosing the Right Value of K

### 📉 **Elbow Method**:

- Plot number of clusters (K) vs. **inertia** (within-cluster sum of squares).
    
- Choose the K where the decrease in inertia starts to **flatten** — like an elbow.
    

```python
import matplotlib.pyplot as plt

inertias = []
for k in range(1, 10):
    km = KMeans(n_clusters=k, random_state=0)
    km.fit(data)
    inertias.append(km.inertia_)

plt.plot(range(1, 10), inertias, marker='o')
plt.xlabel('K')
plt.ylabel('Inertia')
plt.title('Elbow Method')
plt.show()
```

---

## 🧰 Applications of K-Means

|Field|Application|
|---|---|
|**Marketing**|Customer segmentation|
|**Retail**|Product recommendation groups|
|**Finance**|Credit risk clustering|
|**Healthcare**|Patient risk group detection|
|**Image Processing**|Image compression, color quantization|

---

## ✅ Advantages

- Simple to understand and implement.
    
- Fast and efficient on large datasets.
    
- Works well when clusters are spherical and balanced.
    

---

## ⚠️ Limitations

|Issue|Description|
|---|---|
|**Needs K as input**|Must specify number of clusters|
|**Sensitive to outliers**|Outliers can skew results|
|**Assumes spherical clusters**|Doesn’t work well with irregular shapes|
|**Random Initialization**|May converge to local minima|

> Solutions: Use `k-means++` for better initialization.

---

## 📌 Summary

|Feature|Description|
|---|---|
|**Type**|Unsupervised Learning|
|**Input**|Number of clusters (K), feature data|
|**Output**|Cluster labels for each data point|
|**Goal**|Minimize distance between points and centroids|

---

