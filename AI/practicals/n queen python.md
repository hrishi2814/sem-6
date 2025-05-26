Alright!  
Let's implement the **N-Queens problem** using both:

- **Backtracking** (the standard way)
    
- **Branch and Bound** (which improves backtracking by pruning more efficiently)
    

---

I'll first give you a clean **Backtracking** solution, then **Branch and Bound** after that.  
I'll write them both in **Python**, cleanly side-by-side.

---

# 1. N-Queens — Backtracking (Standard)

```python
def solve_n_queens_backtracking(n):
    def is_safe(board, row, col):
        # Check same column
        for i in range(row):
            if board[i] == col:
                return False
            # Check diagonals
            if abs(board[i] - col) == abs(i - row):
                return False
        return True

    def solve(board, row):
        if row == n:
            solutions.append(board[:])
            return
        for col in range(n):
            if is_safe(board, row, col):
                board[row] = col
                solve(board, row + 1)
                board[row] = -1  # backtrack

    solutions = []
    board = [-1] * n
    solve(board, 0)
    return solutions

def print_solutions(solutions, n):
    for sol in solutions:
        for i in range(n):
            line = ['.'] * n
            line[sol[i]] = 'Q'
            print(' '.join(line))
        print()

# Example
n = 4
solutions = solve_n_queens_backtracking(n)
print(f"Total Solutions (Backtracking) for {n}-Queens: {len(solutions)}")
print_solutions(solutions, n)
```

---

# 2. N-Queens — Branch and Bound (Optimized Backtracking)

**Branch and Bound** uses 3 boolean arrays:

- `columns[col]` — whether a column is occupied
    
- `diag1[row - col + n - 1]` — major diagonals ( \ )
    
- `diag2[row + col]` — minor diagonals ( / )
    

```python
def solve_n_queens_branch_and_bound(n):
    def solve(row):
        if row == n:
            solutions.append(board[:])
            return
        for col in range(n):
            if not columns[col] and not diag1[row - col + n - 1] and not diag2[row + col]:
                board[row] = col
                columns[col] = diag1[row - col + n - 1] = diag2[row + col] = True
                solve(row + 1)
                columns[col] = diag1[row - col + n - 1] = diag2[row + col] = False
                board[row] = -1

    solutions = []
    board = [-1] * n
    columns = [False] * n
    diag1 = [False] * (2 * n - 1)
    diag2 = [False] * (2 * n - 1)
    solve(0)
    return solutions

# Example
n = 4
solutions_bb = solve_n_queens_branch_and_bound(n)
print(f"Total Solutions (Branch and Bound) for {n}-Queens: {len(solutions_bb)}")
print_solutions(solutions_bb, n)
```

---

# ✨ Summary:

|Method|Time Complexity|Space Complexity|Notes|
|:--|:--|:--|:--|
|Backtracking|O(N!)|O(N)|Simple, but slower|
|Branch and Bound|O(N!) (but faster in practice)|O(N)|Faster by pruning|

---

