## 📘 **MapReduce Summary**

**MapReduce** is a programming model introduced by Google for **processing large datasets in a distributed manner**. It works on the principle of **divide and conquer** using two key functions: **Map** and **Reduce**.

---

### 🔧 **Key Components**

1. **Map Function**
    
    - Takes input data and converts it into a set of key-value pairs.
        
    - Operates on **splits** of the input data in **parallel**.
        
    - Output: intermediate key-value pairs.
        
2. **Shuffle and Sort**
    
    - Intermediate data is shuffled and sorted by key.
        
    - This organizes the data for the Reduce phase.
        
3. **Reduce Function**
    
    - Takes grouped intermediate data and processes each group.
        
    - Produces the final output (aggregated or summarized data).
        

---

### 🧱 **How It Works**

1. **Input Split**: Input data is split into fixed-size blocks (default: 64MB or 128MB in Hadoop).
    
2. **Mapping**: Each split is processed by a Mapper to produce intermediate data (key-value pairs).
    
3. **Shuffling**: The system collects and redistributes the intermediate data so that all values for the same key are grouped together.
    
4. **Reducing**: Reducer functions process these key-value pairs to produce the final output.
    

---

### 📊 Example

**Word Count Problem**:

- **Input**: A large text document.
    
- **Map Output**: (word, 1) for every word in the text.
    
- **Reduce Output**: (word, total_count), summing up occurrences.
    

---

### ⚙️ **Working Phases**

1. **Splitting**
    
2. **Mapping**
    
3. **Shuffling and Sorting**
    
4. **Reducing**
    

---

### 📈 **Benefits of MapReduce**

- Scalable and fault-tolerant
    
- Handles large-scale data easily
    
- Parallel processing
    
- Simplifies complex data processing logic
    

---

### 📌 **Limitations**

- Not suitable for real-time processing
    
- High latency due to disk-based operations
    
- Difficult debugging and testing
    

---

### 🧠 **Real-World Use Cases**

- Web indexing (e.g., Google Search)
    
- Log file analysis
    
- Recommendation systems
    
- Data mining tasks
    

---
