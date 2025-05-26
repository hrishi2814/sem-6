### 🧠 What is First Order Logic (FOL)?

**First Order Logic (FOL)** is a powerful formal system used in mathematics, computer science, and artificial intelligence to represent and reason about **objects**, their **properties**, and **relationships** among them. It extends **propositional logic** by introducing **quantifiers** and **predicates**.

---

## 🔤 1. **Syntax of First Order Logic**

The **syntax** defines the valid symbols and the rules to form well-formed formulas.

### ✅ **Basic Elements:**

|Component|Description|Example|
|---|---|---|
|**Constants**|Represent specific objects|`john`, `3`, `earth`|
|**Variables**|Symbolic placeholders for objects|`x`, `y`, `z`|
|**Predicates**|Represent properties or relations|`Human(x)`, `Loves(john, x)`|
|**Functions**|Map input objects to output objects|`FatherOf(x)`, `Add(x, y)`|
|**Connectives**|Logical operators|`∧`, `∨`, `¬`, `→`, `↔`|
|**Quantifiers**|Express generality or existence|`∀x` (for all x), `∃x` (there exists an x)|
|**Terms**|Constants, variables, or function applications|`x`, `john`, `FatherOf(x)`|
|**Atomic Formulas**|Predicate applied to terms|`Human(x)`, `Loves(john, mary)`|
|**Well-Formed Formulas (WFFs)**|Built from atomic formulas using connectives and quantifiers|`∀x (Human(x) → Mortal(x))`|

---

## 📖 2. **Semantics of First Order Logic**

Semantics define **what formulas mean** — i.e., their **truth** in a model.

### A **Model** in FOL includes:

- A **domain (D)**: The set of all possible objects (e.g., people, numbers).
    
- **Interpretations**:
    
    - Assign meaning to **constants** (e.g., `john` → a person).
        
    - Assign meaning to **predicates** (e.g., `Human(x)` is true if x is a person).
        
    - Assign meaning to **functions** (e.g., `FatherOf(john)` returns john’s father).
        

---

### ✅ **Semantics of Main Components:**

|FOL Expression|Meaning|
|---|---|
|`P(a)`|Predicate `P` is **true** for object `a`|
|`¬P(x)`|Predicate `P` is **not true** for `x`|
|`P(x) ∧ Q(x)`|Both `P(x)` and `Q(x)` are true|
|`P(x) ∨ Q(x)`|Either `P(x)` or `Q(x)` (or both) are true|
|`P(x) → Q(x)`|If `P(x)` is true, then `Q(x)` must also be true|
|`∀x P(x)`|`P(x)` is true for **all** objects in the domain|
|`∃x P(x)`|There is **at least one** object for which `P(x)` is true|

---

## 🧪 Examples

### Example 1: All humans are mortal

```plaintext
∀x (Human(x) → Mortal(x))
```

- Meaning: For **every x**, if x is a human, then x is mortal.
    

### Example 2: Socrates is a human

```plaintext
Human(socrates)
```

### Example 3: Therefore, Socrates is mortal

```plaintext
Mortal(socrates)
```

> Using inference, you can deduce this from examples 1 and 2.

---

### Example 4: There exists someone who loves Mary

```plaintext
∃x (Loves(x, mary))
```

### Example 5: Everyone loves themselves

```plaintext
∀x (Loves(x, x))
```

---

## ✅ Summary

|Aspect|Description|
|---|---|
|**Syntax**|Rules for constructing valid FOL expressions|
|**Semantics**|Rules for interpreting the truth of those expressions in a given domain|
|**Power**|Can represent complex relationships and reason about them logically|

---

Would you like a solved example using a truth model or how FOL is applied in AI (e.g., Wumpus World)?