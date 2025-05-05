# N-Queens Problem: Backtracking vs Branch and Bound

## Intuition and Mental Models

### Backtracking Approach
**Think of it like:** Trying on outfits one piece at a time, and when something doesn't fit, you backtrack to try a different combination.

**Key Characteristics:**
- Systematically explores all possibilities
- Abandons a path as soon as it determines it can't lead to a solution ("pruning")
- Uses recursion naturally to explore and backtrack

### Branch and Bound Approach
**Think of it like:** A smart shopper who estimates the total cost while filling their cart, and abandons paths that can't possibly beat the best solution found so far.

**Key Characteristics:**
- Uses a priority queue to explore most promising nodes first
- Maintains bounds to eliminate unpromising branches early
- Often more efficient than pure backtracking for optimization problems

## Backtracking Implementation (C++ and Java)

### C++ Implementation
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(vector<int>& board, int row, int col) {
    // Check if a queen can be placed at (row,col)
    for (int i = 0; i < row; i++) {
        // Same column or diagonal check
        if (board[i] == col || abs(board[i] - col) == abs(i - row)) {
            return false;
        }
    }
    return true;
}

void solveNQueens(vector<int>& board, int row, int n, vector<vector<string>>& solutions) {
    if (row == n) {
        // Found a solution, convert to string representation
        vector<string> solution;
        for (int i = 0; i < n; i++) {
            string s(n, '.');
            s[board[i]] = 'Q';
            solution.push_back(s);
        }
        solutions.push_back(solution);
        return;
    }

    for (int col = 0; col < n; col++) {
        if (isSafe(board, row, col)) {
            board[row] = col;
            solveNQueens(board, row + 1, n, solutions);
            board[row] = -1; // Backtrack
        }
    }
}

vector<vector<string>> solveNQueens(int n) {
    vector<vector<string>> solutions;
    vector<int> board(n, -1);
    solveNQueens(board, 0, n, solutions);
    return solutions;
}

int main() {
    int n = 4;
    auto solutions = solveNQueens(n);
    for (auto& sol : solutions) {
        for (auto& row : sol) {
            cout << row << endl;
        }
        cout << endl;
    }
    return 0;
}
```

### Java Implementation
```java
import java.util.ArrayList;
import java.util.List;

public class NQueensBacktracking {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> solutions = new ArrayList<>();
        int[] board = new int[n];
        solve(board, 0, n, solutions);
        return solutions;
    }

    private void solve(int[] board, int row, int n, List<List<String>> solutions) {
        if (row == n) {
            solutions.add(createSolution(board));
            return;
        }

        for (int col = 0; col < n; col++) {
            if (isSafe(board, row, col)) {
                board[row] = col;
                solve(board, row + 1, n, solutions);
                board[row] = -1; // Backtrack
            }
        }
    }

    private boolean isSafe(int[] board, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (board[i] == col || Math.abs(board[i] - col) == Math.abs(i - row)) {
                return false;
            }
        }
        return true;
    }

    private List<String> createSolution(int[] board) {
        List<String> solution = new ArrayList<>();
        for (int row = 0; row < board.length; row++) {
            StringBuilder sb = new StringBuilder();
            for (int col = 0; col < board.length; col++) {
                sb.append(board[row] == col ? "Q" : ".");
            }
            solution.add(sb.toString());
        }
        return solution;
    }

    public static void main(String[] args) {
        NQueensBacktracking solver = new NQueensBacktracking();
        List<List<String>> solutions = solver.solveNQueens(4);
        for (List<String> sol : solutions) {
            for (String row : sol) {
                System.out.println(row);
            }
            System.out.println();
        }
    }
}
```

## Branch and Bound Implementation (C++ and Java)

### C++ Implementation
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Node {
    int level;
    vector<int> path;
    int cost; // Lower bound on number of conflicts
};

bool compareNodes(const Node& a, const Node& b) {
    return a.cost < b.cost;
}

int calculateCost(vector<int>& path, int n) {
    int conflicts = 0;
    for (int i = 0; i < path.size(); i++) {
        for (int j = i + 1; j < path.size(); j++) {
            if (path[i] == path[j] || abs(path[i] - path[j]) == abs(i - j)) {
                conflicts++;
            }
        }
    }
    return conflicts;
}

vector<vector<string>> solveNQueensBB(int n) {
    vector<vector<string>> solutions;
    vector<Node> pq; // Priority queue

    // Initialize with root node
    Node root{-1, {}, 0};
    pq.push_back(root);
    make_heap(pq.begin(), pq.end(), compareNodes);

    while (!pq.empty()) {
        pop_heap(pq.begin(), pq.end(), compareNodes);
        Node current = pq.back();
        pq.pop_back();

        if (current.level == n - 1) {
            // Found a solution with 0 conflicts
            vector<string> solution;
            for (int row = 0; row < n; row++) {
                string s(n, '.');
                s[current.path[row]] = 'Q';
                solution.push_back(s);
            }
            solutions.push_back(solution);
            continue;
        }

        int nextLevel = current.level + 1;
        for (int col = 0; col < n; col++) {
            vector<int> newPath = current.path;
            newPath.push_back(col);
            int newCost = calculateCost(newPath, n);

            if (newCost == 0) { // Only proceed if no conflicts
                Node child{nextLevel, newPath, newCost};
                pq.push_back(child);
                push_heap(pq.begin(), pq.end(), compareNodes);
            }
        }
    }

    return solutions;
}

int main() {
    int n = 4;
    auto solutions = solveNQueensBB(n);
    for (auto& sol : solutions) {
        for (auto& row : sol) {
            cout << row << endl;
        }
        cout << endl;
    }
    return 0;
}
```

### Java Implementation
```java
import java.util.*;

public class NQueensBranchAndBound {
    static class Node implements Comparable<Node> {
        int level;
        List<Integer> path;
        int cost;

        public Node(int level, List<Integer> path, int cost) {
            this.level = level;
            this.path = new ArrayList<>(path);
            this.cost = cost;
        }

        @Override
        public int compareTo(Node other) {
            return Integer.compare(this.cost, other.cost);
        }
    }

    public List<List<String>> solveNQueens(int n) {
        List<List<String>> solutions = new ArrayList<>();
        PriorityQueue<Node> pq = new PriorityQueue<>();

        // Initialize with root node
        pq.add(new Node(-1, new ArrayList<>(), 0));

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            if (current.level == n - 1) {
                solutions.add(createSolution(current.path));
                continue;
            }

            int nextLevel = current.level + 1;
            for (int col = 0; col < n; col++) {
                List<Integer> newPath = new ArrayList<>(current.path);
                newPath.add(col);
                int newCost = calculateCost(newPath);

                if (newCost == 0) { // Only proceed if no conflicts
                    pq.add(new Node(nextLevel, newPath, newCost));
                }
            }
        }

        return solutions;
    }

    private int calculateCost(List<Integer> path) {
        int conflicts = 0;
        for (int i = 0; i < path.size(); i++) {
            for (int j = i + 1; j < path.size(); j++) {
                if (path.get(i).equals(path.get(j)) || 
                    Math.abs(path.get(i) - path.get(j)) == Math.abs(i - j)) {
                    conflicts++;
                }
            }
        }
        return conflicts;
    }

    private List<String> createSolution(List<Integer> board) {
        List<String> solution = new ArrayList<>();
        for (int row = 0; row < board.size(); row++) {
            StringBuilder sb = new StringBuilder();
            for (int col = 0; col < board.size(); col++) {
                sb.append(board.get(row) == col ? "Q" : ".");
            }
            solution.add(sb.toString());
        }
        return solution;
    }

    public static void main(String[] args) {
        NQueensBranchAndBound solver = new NQueensBranchAndBound();
        List<List<String>> solutions = solver.solveNQueens(4);
        for (List<String> sol : solutions) {
            for (String row : sol) {
                System.out.println(row);
            }
            System.out.println();
        }
    }
}
```

## Key Differences and When to Use Each

| Aspect          | Backtracking                          | Branch and Bound                     |
|----------------|---------------------------------------|---------------------------------------|
| **Approach**   | Depth-first with pruning              | Best-first search with bounding      |
| **Memory**     | Uses recursion stack (less memory)    | Uses priority queue (more memory)    |
| **Order**      | Finds solutions in arbitrary order    | Tends to find better solutions first |
| **Best for**   | Finding all solutions                 | Optimization problems                |
| **Complexity** | O(N!) time                           | O(N!) time but often faster in practice|

**Pro Tip:** For N-Queens where we want all solutions, backtracking is often simpler and sufficient. Branch and Bound shines when we need the "best" solution according to some metric (like minimum conflicts).