## 📚 What are TF and IDF?

### 🔹 **TF (Term Frequency)**

It measures **how frequently** a term appears in a document.

$TF(t,d) = \frac{\text{Number of times term } t \text{ appears in document } d}{\text{Total number of terms in document } d}$

---

### 🔹 **IDF (Inverse Document Frequency)**

It measures **how important or unique** a term is across **all documents** in a collection. If a term appears in **many documents**, it’s considered less important.

$IDF(t)= \log\left(\frac{N}{1 + \text{Number of documents containing } t}\right)$

Where:

- N = Total number of documents
    
- $1+dft1 + \text{df}_t$ = Number of documents containing term tt (add 1 to avoid division by zero)
    

---

### 🔹 **TF-IDF Score**

$TF-IDF(t,d)=TF(t,d)×IDF(t)\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$

TF-IDF gives **high weight** to terms that:

- Appear **frequently** in a document (high TF),
    
- But appear in **fewer** documents overall (high IDF).
    

---

## 🧠 Simple Example

### Suppose you have 3 documents:

```text
Doc1: "the cat sat on the mat"  
Doc2: "the dog sat on the log"  
Doc3: "cats and dogs are friends"
```

---

### Step 1: Term Frequency (TF) for word **"sat"** in Doc1

- Frequency of "sat" = 1
    
- Total words in Doc1 = 6
    

$TF("sat",Doc1)=16≈0.167\text{TF}("sat", \text{Doc1}) = \frac{1}{6} \approx 0.167$

---

### Step 2: Document Frequency for "sat"

- "sat" appears in **Doc1 and Doc2** → 2 documents
    
- Total documents = 3
    

IDF("sat")=log⁡(31+2)=log⁡(1)=0\text{IDF}("sat") = \log\left(\frac{3}{1 + 2}\right) = \log(1) = 0

So "sat" has low importance due to its common appearance.

---

### Step 3: Now for word **"mat"**

- Appears only in Doc1
    
- TF = 16=0.167\frac{1}{6} = 0.167
    
- IDF = log⁡(31+1)=log⁡(1.5)≈0.176\log\left(\frac{3}{1 + 1}\right) = \log(1.5) \approx 0.176
    

TF-IDF("mat",Doc1)=0.167×0.176≈0.0294\text{TF-IDF}("mat", \text{Doc1}) = 0.167 \times 0.176 \approx 0.0294

"mat" is slightly more unique than "sat" across documents.

---

## 📌 Summary

|Term|TF (Doc1)|DF|IDF|TF-IDF|
|---|---|---|---|---|
|sat|0.167|2|0|0|
|mat|0.167|1|0.176|0.0294|

---

## 🛠 Real-World Use of TF-IDF

- **Search engines** (e.g., Google): Rank pages by relevance.
    
- **Text classification**: Feature extraction for spam filters, sentiment analysis.
    
- **Keyword extraction**: Highlighting important terms in articles or documents.
    

---

Would you like a Python code example using `sklearn` for this?