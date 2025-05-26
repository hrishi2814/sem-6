# DFS and BFS in Java and C++ with Intuitive Explanations

Let me break this down in a way that will stick in your mind, with both Java and C++ implementations.

## The Core Intuition

Imagine you're exploring a maze:

- **DFS (Depth-First Search)**: Like putting your hand on the right wall and following it. You go as deep as possible down one path before backtracking.
- **BFS (Breadth-First Search)**: Like throwing a pebble in water - it explores all nodes at the same "depth level" before moving deeper.

## Java Implementation

### Graph Representation

```java
import java.util.*;

class Graph {
    private Map<Integer, List<Integer>> adjList;

    public Graph() {
        adjList = new HashMap<>();
    }

    public void addEdge(int u, int v) {
        adjList.putIfAbsent(u, new ArrayList<>());
        adjList.putIfAbsent(v, new ArrayList<>());
        adjList.get(u).add(v);
        adjList.get(v).add(u); // Undirected graph
    }

    public List<Integer> getNeighbors(int node) {
        return adjList.getOrDefault(node, new ArrayList<>());
    }
}
```

### DFS in Java

```java
// Recursive DFS - like diving deep first
void dfsRecursive(Graph graph, int node, Set<Integer> visited) {
    visited.add(node);
    System.out.print(node + " "); // Process node
    
    for (int neighbor : graph.getNeighbors(node)) {
        if (!visited.contains(neighbor)) {
            dfsRecursive(graph, neighbor, visited);
        }
    }
}

// Iterative DFS - uses stack (LIFO)
void dfsIterative(Graph graph, int start) {
    Set<Integer> visited = new HashSet<>();
    Stack<Integer> stack = new Stack<>();
    stack.push(start);
    
    while (!stack.isEmpty()) {
        int node = stack.pop();
        if (!visited.contains(node)) {
            visited.add(node);
            System.out.print(node + " ");
            
            // Push neighbors in reverse order for correct traversal
            List<Integer> neighbors = graph.getNeighbors(node);
            for (int i = neighbors.size() - 1; i >= 0; i--) {
                int neighbor = neighbors.get(i);
                if (!visited.contains(neighbor)) {
                    stack.push(neighbor);
                }
            }
        }
    }
}
```

### BFS in Java

```java
// BFS - uses queue (FIFO)
void bfs(Graph graph, int start) {
    Set<Integer> visited = new HashSet<>();
    Queue<Integer> queue = new LinkedList<>();
    queue.add(start);
    visited.add(start);
    
    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");
        
        for (int neighbor : graph.getNeighbors(node)) {
            if (!visited.contains(neighbor)) {
                visited.add(neighbor);
                queue.add(neighbor);
            }
        }
    }
}
```

## C++ Implementation

### Graph Representation

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <unordered_set>
#include <queue>
#include <stack>
using namespace std;

class Graph {
    unordered_map<int, vector<int>> adjList;
    
public:
    void addEdge(int u, int v) {
        adjList[u].push_back(v);
        adjList[v].push_back(u); // Undirected graph
    }
    
    const vector<int>& getNeighbors(int node) {
        return adjList[node];
    }
};
```

### DFS in C++

```cpp
// Recursive DFS
void dfsRecursive(Graph& graph, int node, unordered_set<int>& visited) {
    visited.insert(node);
    cout << node << " "; // Process node
    
    for (int neighbor : graph.getNeighbors(node)) {
        if (visited.find(neighbor) == visited.end()) {
            dfsRecursive(graph, neighbor, visited);
        }
    }
}

// Iterative DFS
void dfsIterative(Graph& graph, int start) {
    unordered_set<int> visited;
    stack<int> st;
    st.push(start);
    
    while (!st.empty()) {
        int node = st.top();
        st.pop();
        
        if (visited.find(node) == visited.end()) {
            visited.insert(node);
            cout << node << " ";
            
            // Push neighbors in reverse order
            vector<int> neighbors = graph.getNeighbors(node);
            for (auto it = neighbors.rbegin(); it != neighbors.rend(); ++it) {
                if (visited.find(*it) == visited.end()) {
                    st.push(*it);
                }
            }
        }
    }
}
```

### BFS in C++

```cpp
void bfs(Graph& graph, int start) {
    unordered_set<int> visited;
    queue<int> q;
    q.push(start);
    visited.insert(start);
    
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";
        
        for (int neighbor : graph.getNeighbors(node)) {
            if (visited.find(neighbor) == visited.end()) {
                visited.insert(neighbor);
                q.push(neighbor);
            }
        }
    }
}
```

## Mental Models That Stick

### DFS (Depth-First Search)
- **Think**: "Go deep first, then wide"
- **Analogy**: Like exploring a cave - you go as far down one tunnel as possible before checking others
- **Key Structures**: 
  - Recursive: Uses the call stack
  - Iterative: Explicit stack (LIFO)
- **When to use**: Finding connected components, topological sorting, solving puzzles

### BFS (Breadth-First Search)
- **Think**: "Explore all neighbors first"
- **Analogy**: Like ripples in water - expands uniformly in all directions
- **Key Structure**: Queue (FIFO)
- **When to use**: Shortest path in unweighted graphs, web crawling, social networks

## Memory Aid Table

| Feature        | DFS                          | BFS                          |
|---------------|-----------------------------|-----------------------------|
| **Structure** | Stack (LIFO)                | Queue (FIFO)                |
| **Memory**    | Less memory (depth)         | More memory (breadth)       |
| **Order**     | Vertically deep             | Horizontally wide           |
| **Use Case**  | Maze solving, cycle detect  | Shortest path, peer networks|

Remember: 
- DFS is like a **vertical** line going down the graph
- BFS is like a **horizontal** line expanding outward

This contrast should help you remember which to use when!