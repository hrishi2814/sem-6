## 📘 **What is the Apriori Algorithm?**

**Apriori** is a classic algorithm in **Association Rule Mining** used to **find frequent itemsets** in a dataset and derive **association rules** from them.  
It’s mainly used in **market basket analysis** — discovering which items are frequently bought together.

---

## ⚙️ **How Apriori Algorithm Works (Step-by-Step)**

1. **Set minimum thresholds** for:
    
    - **Support** (how frequently an itemset appears)
        
    - **Confidence** (how strong the rule is)
        
2. **Generate frequent itemsets**:
    
    - Start with **1-itemsets**, count how often each item appears (support).
        
    - Eliminate those below **min support**.
        
    - Use the **Apriori property**: _If an itemset is frequent, all of its subsets must also be frequent._
        
    - Use **joining and pruning** to generate 2-itemsets, 3-itemsets, etc.
        
    - Continue until no further frequent itemsets can be generated.
        
3. **Generate Association Rules** from frequent itemsets:
    
    - For each frequent itemset, generate rules in the form:  
        **If {A} then {B}**
        
    - Calculate **confidence** of each rule.
        
    - Keep rules above **min confidence**.
        

---

## 🧾 **Association Rules**

An **association rule** is an implication of the form:

A⇒BA \Rightarrow B

Where:

- AA: Antecedent (if A occurs)
    
- BB: Consequent (then B occurs)
    

**Example**:  
If `{Milk, Bread} => {Butter}`, it means customers who buy milk and bread often also buy butter.

---

## 📊 **Key Metrics in Apriori**

### 1. **Support**

- Frequency of itemset in all transactions.
    
- Formula:
    
$$
    Support(A)=Transactions containing A
    Total transactions\text{Support}(A) = \frac{\text{Transactions containing } A}{\text{Total transactions}}
$$
- Filters out **rare combinations**.
    

### 2. **Confidence**

- How often rule B is true when A is true.
    
- Formula:
    
$$
    Confidence(A⇒B)=Support(A∪B)Support(A)\text{Confidence}(A \Rightarrow B) = \frac{\text{Support}(A \cup B)}{\text{Support}(A)}
$$
- Measures **rule strength**.
    

### 3. **Lift** (optional)

- Measures how much more likely B is to occur with A than by chance.
    
- Formula:
    
    Lift(A⇒B)=Confidence(A⇒B)Support(B)\text{Lift}(A \Rightarrow B) = \frac{\text{Confidence}(A \Rightarrow B)}{\text{Support}(B)}

---

## 📦 **Example: Market Basket Analysis**

### 🛒 Transactions:

|Transaction ID|Items|
|---|---|
|T1|Milk, Bread, Butter|
|T2|Milk, Bread|
|T3|Bread, Butter|
|T4|Milk, Butter|
|T5|Bread|

### 📐 Step 1: Find Frequent Itemsets (min support = 40%)

|Itemset|Support Count|Support|
|---|---|---|
|{Milk}|3|60%|
|{Bread}|4|80%|
|{Butter}|3|60%|
|{Milk, Bread}|2|40%|
|{Milk, Butter}|2|40%|
|{Bread, Butter}|2|40%|
|{Milk, Bread, Butter}|1|20% ❌|

### ✅ Keep itemsets ≥ 40% support.

### 📐 Step 2: Generate Rules (min confidence = 70%)

From frequent itemset {Milk, Bread}:

- Rule: Milk ⇒ Bread  
    Confidence = 2/3 ≈ 66.7% ❌ (discarded)
    
- Rule: Bread ⇒ Milk  
    Confidence = 2/4 = 50% ❌
    

From {Bread, Butter}:

- Bread ⇒ Butter = 2/4 = 50% ❌
    
- Butter ⇒ Bread = 2/3 = 66.7% ❌
    

From {Milk, Butter}:

- Milk ⇒ Butter = 2/3 = 66.7% ❌
    

👉 No rule meets 70% confidence here.

---

## 🧠 **Why Apriori Works Well**

- Efficiently narrows down search space using the **Apriori property**.
    
- Works well with **discrete transactional data**.
    
- Can be extended to mine **interesting patterns** in large datasets.
    

---

## 💼 **Applications of Apriori Algorithm**

|Domain|Use Case|
|---|---|
|**Retail**|Market basket analysis (products often bought together)|
|**E-commerce**|Product recommendations|
|**Healthcare**|Finding co-occurrence of symptoms/diseases|
|**Banking**|Detecting fraud patterns|
|**Web Usage Mining**|Understanding user navigation patterns|

---

## 📊 Summary Table

|Aspect|Description|
|---|---|
|**Algorithm**|Apriori|
|**Type**|Association Rule Mining|
|**Key Steps**|Frequent itemset generation, rule mining|
|**Key Metrics**|Support, Confidence, (Lift)|
|**Input**|Transactional dataset|
|**Output**|Association rules|
|**Applications**|Retail, healthcare, fraud detection|

---

Let me know if you want the **Python implementation** using `mlxtend` or `apriori()` or a **diagram of the algorithm's flow**!