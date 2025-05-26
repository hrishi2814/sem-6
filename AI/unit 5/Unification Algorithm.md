### 🔗 Unification Algorithm (AI / Logic Programming)

**Unification** is a process in logic and AI (especially in **Prolog**, **automated reasoning**, and **theorem proving**) that **makes two logical expressions identical** by finding a suitable substitution for their variables.

---

### 📌 What is Unification?

It is used to:

- **Match terms** (constants, variables, compound terms).
    
- **Find a substitution** (called a **unifier**) that makes two expressions equal.
    

If such a substitution exists, the expressions are **unifiable**.

---

### 📚 Basic Terms

- **Variable:** `X`, `Y`, etc.
    
- **Constant:** `john`, `apple`, `3`
    
- **Compound Term:** `likes(john, X)`
    

---

### 🔧 Unification Algorithm (Steps)

1. **Compare the terms**:
    
    - If both are constants:
        
        - Succeed if equal.
            
        - Fail otherwise.
            
    - If one is a variable:
        
        - Replace the variable with the other term (if no circular substitution).
            
    - If both are compound:
        
        - Unify the function symbols and their arguments recursively.
            
2. **Occurs check** (optional): Prevent a variable from being unified with a term that contains it (e.g., `X = f(X)` → infinite recursion).
    

---

### ✅ Example

Unify:

```prolog
likes(john, X)  and  likes(Y, apple)
```

**Step-by-step:**

- Both are compound terms: `likes(...)`
    
- Check function symbols: ✔️ both `likes`
    
- Now unify arguments:
    
    - `john` with `Y` → Substitution: `{Y → john}`
        
    - `X` with `apple` → Substitution: `{X → apple}`
        

👉 **Final substitution (unifier):**

```prolog
{X → apple, Y → john}
```

This makes both expressions become:

```prolog
likes(john, apple)
```

✅ **Unified successfully.**

---

### ❌ Non-Unifiable Example

Unify:

```prolog
f(X, b)  and  f(a, X)
```

Try:

- First args: `X` and `a` → `{X → a}`
    
- Now: Second args: `b` and `X` → `b` and `a` → ❌ Not same
    

So, no single substitution works → **Not unifiable**.

---

### 🔁 Real Use

Unification is **core to Prolog** execution:

```prolog
likes(john, X).     % Fact
?- likes(john, apple).  % Query
```

→ Prolog uses unification to match query with the fact.

---

Let me know if you want the algorithm in code or more complex examples!