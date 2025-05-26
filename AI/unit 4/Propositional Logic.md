
Certainly! Here's a complete explanation of **Propositional Logic**, including its **syntax**, **semantics**, **inference rules**, and the **algorithm for deciding entailment**.

---

## 💡 What is Propositional Logic?

**Propositional Logic** (also called **Sentential Logic**) is the most basic form of logic. It deals with **propositions** — statements that can be **true** or **false** — and uses **logical connectives** to form complex expressions.

Unlike First Order Logic, it **does not** handle relationships between objects or use quantifiers.

---

## 🧠 1. **Syntax of Propositional Logic**

### ✅ **Basic Components**:

|Component|Description|Example|
|---|---|---|
|**Propositions**|Atomic statements|`P`, `Q`, `R` (e.g., "It is raining")|
|**Logical Connectives**|Used to build complex statements|`¬`, `∧`, `∨`, `→`, `↔`|
|**Well-Formed Formulas (WFFs)**|Formed by applying connectives to atomic propositions|`P ∧ Q`, `¬P ∨ (Q → R)`|

### ✅ **Connectives Summary**:

|Symbol|Name|Meaning|
|---|---|---|
|`¬P`|Negation|Not P|
|`P ∧ Q`|Conjunction|P and Q|
|`P ∨ Q`|Disjunction|P or Q|
|`P → Q`|Implication|If P, then Q|
|`P ↔ Q`|Biconditional|P if and only if Q|

---

## 📖 2. **Semantics of Propositional Logic**

Semantics define how we **interpret** and assign **truth values** to formulas.

### ✅ **Truth Assignments**:

Each proposition is assigned **true (T)** or **false (F)**.

Example:

```text
Let: P = true, Q = false

Then:
¬P       = false
P ∧ Q    = false
P ∨ Q    = true
P → Q    = false
P ↔ Q    = false
```

---

## 🧩 3. **Inference in Propositional Logic**

### ✅ **Entailment (`⊨`)**

A set of sentences **KB (knowledge base)** **entails** a sentence `α` if in **every model** where KB is true, `α` is also true.

> Notation:  
> `KB ⊨ α`

---

## 🧠 4. **Common Inference Rules**

|Rule|Form|Meaning|
|---|---|---|
|**Modus Ponens**|`P → Q`, `P` ⟹ `Q`|If P implies Q and P is true, then Q must be true|
|**Modus Tollens**|`P → Q`, `¬Q` ⟹ `¬P`|If P implies Q and Q is false, then P must be false|
|**And-Elimination**|`P ∧ Q` ⟹ `P`, `Q`|If both P and Q are true, then P is true (and Q is too)|
|**And-Introduction**|`P`, `Q` ⟹ `P ∧ Q`|Combine P and Q|
|**Or-Introduction**|`P` ⟹ `P ∨ Q`|If P is true, then P or Q is true|
|**Resolution**|`P ∨ Q`, `¬Q ∨ R` ⟹ `P ∨ R`|Resolve on common literal Q|

---

## 🛠️ 5. **Algorithm for Deciding Entailment**

We determine if `KB ⊨ α` (i.e., if α logically follows from KB). A common method is **Truth Table Checking**.

---

### ✅ **Truth Table Entailment Algorithm**:

**Goal**: Check whether every model that satisfies `KB` also satisfies `α`.

### **Steps**:

1. **List all atomic propositions** in `KB` and `α`.
    
2. **Generate all possible truth assignments** (2ⁿ for n variables).
    
3. For each assignment:
    
    - If **KB is true**, check if **α is also true**.
        
    - If KB is true **and α is false**, then **KB ⊭ α**.
        
4. If **α is true in all models** where KB is true, then **KB ⊨ α**.
    

---

### 🧪 Example:

Let `KB = P → Q`, and check if `KB ⊨ ¬P ∨ Q`.

|P|Q|P → Q|¬P ∨ Q|Entailment|
|---|---|---|---|---|
|T|T|T|T|OK|
|T|F|F|F|Ignore|
|F|T|T|T|OK|
|F|F|T|T|OK|

✅ All rows where `KB` is true → `¬P ∨ Q` is true  
➡️ So, `KB ⊨ ¬P ∨ Q`

---

## 🧮 Other Methods for Entailment

1. **Resolution Algorithm**:
    
    - Convert all formulas into **CNF (Conjunctive Normal Form)**.
        
    - Apply resolution rules repeatedly.
        
    - If you derive an empty clause `□`, then `KB ⊨ α`.
        
2. **Forward/Backward Chaining** (for Horn clauses).
    
3. **Model Checking**:
    
    - Generate truth tables (brute force).
        
    - Practical for small sets.
        

---

## ✅ Summary

|Topic|Description|
|---|---|
|**Propositional Logic**|Uses atomic statements and connectives. No quantifiers or objects.|
|**Syntax**|Propositions and logical connectives.|
|**Semantics**|Truth values (T/F) assigned to propositions.|
|**Inference Rules**|Used to derive conclusions (Modus Ponens, Resolution, etc.).|
|**Entailment Algorithm**|Truth table, resolution, or chaining methods.|

---

Would you like an example of entailment using **Resolution** too?