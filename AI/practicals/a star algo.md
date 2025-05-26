# A* Algorithm for 8-Puzzle Problem (C++ and Java)

## Strong Intuition First (Mental Model)

Imagine the 8-puzzle as a sliding tile game where you need to arrange numbered tiles in order. The A* algorithm is like having:
1. A **foresight** (heuristic) that estimates how close you are to the solution
2. A **memory** of the exact steps taken so far (path cost)

**Key Components Visualized:**
```
Current State    Heuristic (h)    Path Cost (g)    Priority (f = g + h)
[1 2 3]          h=0 (solved)     g=3 moves        f=0+3=3
[4 5 6]
[7 8 0]
```

## C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_set>
#include <cmath>
using namespace std;

// Puzzle state representation
struct Node {
    vector<vector<int>> state;
    int g, h; // g = path cost, h = heuristic
    int zero_row, zero_col; // Position of empty tile (0)
    string path; // Moves taken (U,D,L,R)

    // Priority comparison
    bool operator>(const Node& other) const {
        return (g + h) > (other.g + other.h);
    }
};

// Calculate Manhattan distance heuristic
int manhattanDistance(const vector<vector<int>>& state) {
    int distance = 0;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            int val = state[i][j];
            if (val != 0) {
                int target_row = (val - 1) / 3;
                int target_col = (val - 1) % 3;
                distance += abs(i - target_row) + abs(j - target_col);
            }
        }
    }
    return distance;
}

// A* Algorithm
string solvePuzzle(vector<vector<int>> initial) {
    priority_queue<Node, vector<Node>, greater<Node>> pq; // Min-heap
    unordered_set<string> visited;
    
    // Find initial empty position
    int zr, zc;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (initial[i][j] == 0) {
                zr = i;
                zc = j;
            }
        }
    }
    
    Node start{initial, 0, manhattanDistance(initial), zr, zc, ""};
    pq.push(start);
    
    // Possible moves (up, down, left, right)
    int dr[] = {-1, 1, 0, 0};
    int dc[] = {0, 0, -1, 1};
    char moves[] = {'U', 'D', 'L', 'R'};
    
    while (!pq.empty()) {
        Node current = pq.top();
        pq.pop();
        
        // Check if solved
        if (current.h == 0) {
            return current.path;
        }
        
        // Generate unique state identifier
        string state_id;
        for (auto &row : current.state) {
            for (int num : row) {
                state_id += to_string(num);
            }
        }
        
        if (visited.count(state_id)) continue;
        visited.insert(state_id);
        
        // Generate neighbors
        for (int i = 0; i < 4; i++) {
            int new_row = current.zero_row + dr[i];
            int new_col = current.zero_col + dc[i];
            
            if (new_row >= 0 && new_row < 3 && new_col >= 0 && new_col < 3) {
                vector<vector<int>> new_state = current.state;
                swap(new_state[current.zero_row][current.zero_col], 
                     new_state[new_row][new_col]);
                
                Node neighbor{
                    new_state,
                    current.g + 1,
                    manhattanDistance(new_state),
                    new_row, new_col,
                    current.path + moves[i]
                };
                
                pq.push(neighbor);
            }
        }
    }
    
    return "No solution";
}

int main() {
    vector<vector<int>> puzzle = {
        {1, 2, 3},
        {4, 0, 6},
        {7, 5, 8}
    };
    
    string solution = solvePuzzle(puzzle);
    cout << "Solution path: " << solution << endl;
    return 0;
}
```

## Java Implementation

```java
import java.util.*;

class Node implements Comparable<Node> {
    int[][] state;
    int g, h;
    int zeroRow, zeroCol;
    String path;

    public Node(int[][] state, int g, int h, int zeroRow, int zeroCol, String path) {
        this.state = new int[3][3];
        for (int i = 0; i < 3; i++) {
            System.arraycopy(state[i], 0, this.state[i], 0, 3);
        }
        this.g = g;
        this.h = h;
        this.zeroRow = zeroRow;
        this.zeroCol = zeroCol;
        this.path = path;
    }

    @Override
    public int compareTo(Node other) {
        return Integer.compare(this.g + this.h, other.g + other.h);
    }
}

public class EightPuzzleAStar {
    private static int manhattanDistance(int[][] state) {
        int distance = 0;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                int val = state[i][j];
                if (val != 0) {
                    int targetRow = (val - 1) / 3;
                    int targetCol = (val - 1) % 3;
                    distance += Math.abs(i - targetRow) + Math.abs(j - targetCol);
                }
            }
        }
        return distance;
    }

    public static String solvePuzzle(int[][] initial) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        Set<String> visited = new HashSet<>();

        // Find initial empty position
        int zr = 0, zc = 0;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (initial[i][j] == 0) {
                    zr = i;
                    zc = j;
                }
            }
        }

        pq.add(new Node(initial, 0, manhattanDistance(initial), zr, zc, ""));

        int[] dr = {-1, 1, 0, 0};
        int[] dc = {0, 0, -1, 1};
        char[] moves = {'U', 'D', 'L', 'R'};

        while (!pq.isEmpty()) {
            Node current = pq.poll();

            if (current.h == 0) {
                return current.path;
            }

            String stateId = Arrays.deepToString(current.state);
            if (visited.contains(stateId)) continue;
            visited.add(stateId);

            for (int i = 0; i < 4; i++) {
                int newRow = current.zeroRow + dr[i];
                int newCol = current.zeroCol + dc[i];

                if (newRow >= 0 && newRow < 3 && newCol >= 0 && newCol < 3) {
                    int[][] newState = new int[3][3];
                    for (int r = 0; r < 3; r++) {
                        System.arraycopy(current.state[r], 0, newState[r], 0, 3);
                    }

                    // Swap tiles
                    int temp = newState[current.zeroRow][current.zeroCol];
                    newState[current.zeroRow][current.zeroCol] = newState[newRow][newCol];
                    newState[newRow][newCol] = temp;

                    Node neighbor = new Node(
                        newState,
                        current.g + 1,
                        manhattanDistance(newState),
                        newRow, newCol,
                        current.path + moves[i]
                    );

                    pq.add(neighbor);
                }
            }
        }

        return "No solution";
    }

    public static void main(String[] args) {
        int[][] puzzle = {
            {1, 2, 3},
            {4, 0, 6},
            {7, 5, 8}
        };

        String solution = solvePuzzle(puzzle);
        System.out.println("Solution path: " + solution);
    }
}
```

## Deep Intuition Breakdown

1. **Heuristic Function (Manhattan Distance)**
   - For each tile, calculate how many moves it needs to reach its correct position
   - Sum this for all tiles (except 0)
   - Example: Tile 5 in position (2,1) needs to go to (1,1) → distance = 1

2. **Priority Queue**
   - Always expands the most promising node first (lowest f = g + h)
   - g = exact cost so far (number of moves)
   - h = estimated cost to goal (heuristic)

3. **Visited States**
   - Prevents revisiting the same configuration
   - Uses string representation of the board as key

4. **Neighbor Generation**
   - For each move (Up, Down, Left, Right):
     - Check if move is valid (within bounds)
     - Swap empty tile (0) with adjacent tile
     - Calculate new heuristic
     - Add to priority queue

## Visualization of Algorithm Flow

```
Initial State:    After 1 move:     After 2 moves:
[1 2 3]          [1 2 3]           [1 2 3]
[4 0 6]   → D    [4 5 6]   → R     [4 5 6]
[7 5 8]          [7 0 8]           [7 8 0]
f=1+3=4          f=2+1=3           f=3+0=3 (solved)
```

**Key Insight:** A* smartly balances between:
- Exploiting known information (g)
- Exploring promising paths (h)

This combination makes it optimally efficient for pathfinding problems like the 8-puzzle!