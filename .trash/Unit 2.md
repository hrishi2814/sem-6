### __A* Algorithm 

The **A*** algorithm is a **graph/tree search algorithm** used to find the **shortest path** from a start node to a goal node. It is widely used in **AI, game development, robotics, and pathfinding problems**.

---

## __🔹 How A* Works?_

A* uses two functions to evaluate the cost of each node:

1. **`g(n)`** → The cost from the start node to the current node.
2. **`h(n)`** → The estimated cost from the current node to the goal (heuristic).

The total cost function is:

f(n)=g(n)+h(n)f(n) = g(n) + h(n)

- `g(n)`: Actual distance traveled so far.
- `h(n)`: Estimated distance to the goal (heuristic).
- `f(n)`: The total estimated cost to reach the goal.

---

## **🔹 Properties of A***

✔ **Optimal**: Finds the shortest path if `h(n)` is admissible (does not overestimate).  
✔ **Complete**: Will always find a solution if one exists.  
✔ **Efficient**: Uses heuristics to speed up the search.

---

## __🔹 Steps of A*  Algorithm

1️⃣ **Initialize**:

- Add the start node to the **open list**.
- The **open list** contains nodes to be explored.
- The **closed list** contains nodes that have already been explored.

2️⃣ **Loop Until Goal is Found**:

- Pick the node with the **lowest `f(n)` value** from the open list.
- Move it to the closed list.

3️⃣ **Expand the Node**:

- Generate its neighbors (connected nodes).
- Compute `g(n)`, `h(n)`, and `f(n)`.
- If the neighbor is not in the open list, add it.
- If it’s already in the open list with a **higher cost**, update it with a lower cost.

4️⃣ **Repeat Until Goal is Reached**.

---

## **🔹 Example: Finding the Shortest Path**

Imagine a **grid-based pathfinding problem**, where we move from **Start (S) → Goal (G)**.

```
S → A → B → G
```

|Node|g(n)|h(n)|f(n)|
|---|---|---|---|
|S|0|6|6|
|A|1|4|5|
|B|2|2|4|
|G|3|0|3|

Here, A* will always pick the **lowest f(n) node** to explore next.

---

## __🔹 Python Implementation of A* Algorithm

```python
import heapq

class Node:
    def __init__(self, name, g, h):
        self.name = name
        self.g = g  # Cost from start
        self.h = h  # Heuristic (estimated cost to goal)
        self.f = g + h  # Total cost
    def __lt__(self, other):
        return self.f < other.f

def a_star_algorithm(graph, start, goal, heuristic):
    open_list = []
    closed_list = set()
    heapq.heappush(open_list, (0, start))  # (f, node)

    g_scores = {node: float('inf') for node in graph}
    g_scores[start] = 0

    while open_list:
        _, current = heapq.heappop(open_list)

        if current == goal:
            return f"Reached {goal} with cost {g_scores[goal]}"

        closed_list.add(current)

        for neighbor, cost in graph[current].items():
            if neighbor in closed_list:
                continue
            
            new_g = g_scores[current] + cost
            if new_g < g_scores[neighbor]:  # Found a better path
                g_scores[neighbor] = new_g
                f = new_g + heuristic[neighbor]
                heapq.heappush(open_list, (f, neighbor))

    return "No path found"

# Example Graph (Adjacency List)
graph = {
    'S': {'A': 1, 'B': 4},
    'A': {'B': 2, 'G': 5},
    'B': {'G': 1},
    'G': {}
}

# Heuristic Estimates (Straight-line distance to goal)
heuristic = {'S': 6, 'A': 4, 'B': 2, 'G': 0}

print(a_star_algorithm(graph, 'S', 'G', heuristic))
```

---

## __🔹 Why A* is Better than Dijkstra?

- **Dijkstra’s Algorithm** considers only `g(n)` (actual distance), making it slower.
- **A*** considers both `g(n)` and `h(n)`, making it much more efficient.

---

## **🔹 Applications of A* 

✅ **Google Maps & GPS Navigation** (Finding the shortest path).  
✅ **Game AI (Pathfinding in Games like Pac-Man, Chess)**.  
✅ **Robotics (Autonomous vehicle navigation)**.  
✅ **Network Routing Algorithms**.

---
---
# **Hill Climbing Algorithm – Explained 🚀**

Hill Climbing is a **heuristic search algorithm** used to find an optimal solution by continuously moving towards the **higher-valued (better) state**. It is commonly used in **AI, optimization problems, and machine learning**.

---

## **🔹 How Hill Climbing Works?**

1. **Start at an Initial State**
2. **Evaluate Neighboring States**
3. **Move to the Best Neighbor**
4. **Repeat Until No Better Neighbor Exists**

It is called **"Hill Climbing"** because it continuously tries to **increase (maximize) the value**—just like climbing a hill!

---

## **🔹 Types of Hill Climbing**

1️⃣ **Simple Hill Climbing** → Moves to the first better neighbor it finds.  
2️⃣ **Steepest-Ascent Hill Climbing** → Looks at all neighbors and picks the best one.  
3️⃣ **Stochastic Hill Climbing** → Picks a random neighbor with some probability.

---

## **🔹 Example: Hill Climbing to Maximize a Function**

Let’s say we want to **maximize** the function:

f(x)=−(x−3)2+9f(x) = -(x-3)^2 + 9

This is a **parabolic function** with a peak at `x = 3, f(3) = 9`.

---

## **🔹 Python Implementation of Hill Climbing**

```python
import random

def hill_climb(f, x_start, step_size=0.1, max_iterations=100):
    x = x_start  # Start point
    for _ in range(max_iterations):
        next_x = x + random.choice([-step_size, step_size])  # Move left or right
        if f(next_x) > f(x):  # Move only if the new position is better
            x = next_x
    return x, f(x)

# Function to maximize: f(x) = -(x-3)^2 + 9
def objective_function(x):
    return -(x - 3) ** 2 + 9

best_x, best_y = hill_climb(objective_function, x_start=random.uniform(0, 6))
print(f"Best x: {best_x:.2f}, Best y: {best_y:.2f}")
```

---

## **🔹 Why Hill Climbing Can Fail?**

1️⃣ **Local Maxima** → The algorithm may stop at a suboptimal peak.  
2️⃣ **Plateau** → A flat area where no improvement is seen.  
3️⃣ **Ridges & Valleys** → Some paths may be difficult to climb.

### **🛠 Solution:**

✔ **Random Restarts** → Run the algorithm multiple times with different starting points.  
✔ **Simulated Annealing** → Introduce some randomness to escape local maxima.  
✔ **Genetic Algorithms** → Use population-based search instead.

---

## **🔹 Applications of Hill Climbing**

✅ **Route Optimization (GPS, Logistics, AI)**  
✅ **Game AI (Enemy Movement, Strategy Planning)**  
✅ **Feature Selection in Machine Learning**  
✅ **Tuning Hyperparameters in Deep Learning**

---

### __🔹 Hill Climbing vs. A_ Algorithm_*

|Feature|Hill Climbing|A* Algorithm|
|---|---|---|
|**Type**|Greedy Local Search|Best-First Search|
|**Uses Heuristic?**|Yes|Yes|
|**Can Backtrack?**|No|Yes|
|**Guarantees Optimal Solution?**|No|Yes (if heuristic is admissible)|
|**Best For**|Optimization Problems|Pathfinding Problems|

---
---
## **🔍 Contrast: Depth First Search (DFS) vs. Best First Search (BFS) 🚀**

DFS and Best-First Search (BFS) are both **graph traversal algorithms**, but they differ in how they explore nodes.

|Feature|**Depth-First Search (DFS)**|**Best-First Search (BFS)**|
|---|---|---|
|**Search Strategy**|Explores **deepest** node first (LIFO)|Explores **most promising** node first (heuristic-based)|
|**Data Structure**|**Stack** (Recursive or Explicit)|**Priority Queue** (Min-Heap)|
|**Path Finding**|**Not optimal** (may get stuck in deep paths)|**Can be optimal** (depends on heuristic)|
|**Backtracking?**|Yes|No (Only selects best heuristic node)|
|**Time Complexity**|O(V + E)|O(E log V) (depends on heuristic)|
|**Memory Usage**|Low (only stores path)|High (stores all frontier nodes)|
|**When to Use?**|When searching an **entire space** (e.g., maze)|When you have a **good heuristic** for guidance|

---

### **🔹 How They Work**

1️⃣ **Depth-First Search (DFS)**:

- Uses **LIFO** (Last-In, First-Out) approach (Stack).
- Goes **deep** into one path before backtracking.
- Can get stuck in loops (if not handled properly).

2️⃣ **Best-First Search (BFS)**:

- Uses **Priority Queue** and selects the **best node** based on a heuristic.
- Always expands the most promising node first.
- Works well when an **accurate heuristic is available**.

---

## **🔹 Example: DFS vs. BFS**

Consider a graph where we need to find a path from `A` to `G`:

```
       A
      / \
     B   C
    / \   \
   D   E   F
      /     \
     G       G
```

### **1️⃣ DFS Traversal (A → B → D → E → G ✅)**

- **Explores deep first**.
- Can get **stuck in loops** if not careful.

### **2️⃣ BFS Traversal (A → C → F → G ✅)**

- **Chooses the best heuristic path**.
- **Faster when heuristic is good**.

---

## **🔹 Python Code for DFS vs. Best-First Search**

```python
import heapq

graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['G'],
    'F': ['G'],
    'G': []
}

# DFS Implementation
def dfs(graph, start, goal, path=[]):
    path = path + [start]
    if start == goal:
        return path
    for neighbor in graph.get(start, []):
        if neighbor not in path:
            new_path = dfs(graph, neighbor, goal, path)
            if new_path:
                return new_path
    return None

# Best-First Search Implementation
def best_first_search(graph, start, goal, heuristic):
    pq = []
    heapq.heappush(pq, (heuristic[start], start, [start]))

    while pq:
        _, node, path = heapq.heappop(pq)
        if node == goal:
            return path
        for neighbor in graph.get(node, []):
            heapq.heappush(pq, (heuristic[neighbor], neighbor, path + [neighbor]))

    return None

# Example Heuristic (Estimated Cost to Goal G)
heuristic = {'A': 3, 'B': 2, 'C': 1, 'D': 4, 'E': 1, 'F': 1, 'G': 0}

print("DFS Path:", dfs(graph, 'A', 'G'))
print("Best-First Search Path:", best_first_search(graph, 'A', 'G', heuristic))
```

---

## **🔹 Key Takeaways**

✔ **Use DFS when**: The search space is large but memory is a concern.  
✔ **Use Best-First Search when**: A heuristic can guide the search efficiently.

---
---
## **🔍 Blind Search vs. Heuristic Search – Key Differences** 🚀

Blind search and heuristic search are two types of search strategies used in AI and graph traversal. Let’s break them down:

| Feature              | **Blind Search (Uninformed Search)**                                       | **Heuristic Search (Informed Search)**                          |
| -------------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Definition**       | Searches the entire space without prior knowledge.                         | Uses additional problem-specific knowledge to guide the search. |
| **Knowledge Used?**  | No heuristic information is used.                                          | Uses a heuristic function to estimate the best path.            |
| **Efficiency**       | Less efficient; explores many unnecessary nodes.                           | More efficient; intelligently selects nodes to explore.         |
| **Optimality**       | May not always find the best solution.                                     | Can find optimal solutions if the heuristic is well-defined.    |
| **Examples**         | BFS (Breadth-First Search), DFS (Depth-First Search), Uniform Cost Search. | A* Algorithm, Best-First Search, Hill Climbing.                 |
| **Time Complexity**  | Higher (O(b^d) in worst cases).                                            | Lower (depends on heuristic quality).                           |
| **Space Complexity** | High (stores many nodes in memory).                                        | Lower (stores only promising nodes).                            |

---

## **🔹 Examples**

### **1️⃣ Blind Search Example (Breadth-First Search - BFS)**

- Explores **all nodes** level by level.
- Doesn't prioritize **the goal**.

### __2️⃣ Heuristic Search Example (A_ Algorithm)_*

- Uses `f(n) = g(n) + h(n)`, where:
    - `g(n)` = Actual cost from start to current node.
    - `h(n)` = Estimated cost from current node to goal.
- Prioritizes paths that seem promising.

---

## **🔹 When to Use?**

✔ **Use Blind Search when** you have **no prior knowledge** of the problem space.  
✔ **Use Heuristic Search when** you can estimate **which paths are better** to explore.

---
---
## **🔍 Local Search & Optimization Problem – Explained 🚀**

### **🔹 What is Local Search?**

Local Search is an **optimization technique** used to find a **satisfactory solution** by iteratively improving an initial solution. Unlike global search algorithms that explore the entire space, **local search focuses on neighboring solutions** and moves towards a better solution.

✅ **Best for problems where an optimal solution is difficult to compute globally.**

---

## **🔹 Characteristics of Local Search**

1. **Starts with an Initial Solution**
2. **Explores Neighboring Solutions**
3. **Moves to a Better Neighbor (if found)**
4. **Repeats Until a Stopping Condition is Met**

🚀 **Examples:**

- **Hill Climbing** (moves to the best local neighbor)
- **Simulated Annealing** (accepts worse solutions sometimes to escape local optima)
- **Genetic Algorithms** (uses mutation and selection to evolve solutions)

---

## **🔹 What is an Optimization Problem?**

An **optimization problem** is a problem where the goal is to find the **best solution** (maximum or minimum) based on a given objective function.

💡 **Example:**

- **Traveling Salesman Problem (TSP)** → Find the shortest route covering all cities.
- **Job Scheduling** → Assign jobs to minimize processing time.
- **Neural Network Training** → Optimize weights to minimize error.

### **🔹 Types of Optimization Problems**

1️⃣ **Maximization Problem** → Find the highest possible value (e.g., profit maximization).  
2️⃣ **Minimization Problem** → Find the lowest possible value (e.g., cost minimization).

---

## **🔹 Local Search vs. Global Search**

|Feature|**Local Search**|**Global Search**|
|---|---|---|
|**Exploration**|Focuses on a small region (local neighbors).|Explores the entire search space.|
|**Efficiency**|Faster but may get stuck in local optima.|Slower but more likely to find the best solution.|
|**Examples**|Hill Climbing, Simulated Annealing.|Genetic Algorithms, A* Search.|

Here's a **simple Python implementation** of **Local Search using Hill Climbing** to find the maximum of a function.

### **🔹 Problem:**

We want to maximize the function:

f(x)=−(x−3)2+9f(x) = -(x - 3)^2 + 9

This is a **parabola** with a peak at x=3x = 3, where f(3)=9f(3) = 9.

---

### **🔹 Simple Hill Climbing Algorithm**

```python
import random

# Objective function to maximize
def objective_function(x):
    return -(x - 3) ** 2 + 9  # Parabolic function with peak at x = 3

# Simple Hill Climbing
def hill_climb(start_x, step_size=0.1, max_iterations=100):
    x = start_x  # Start at a random point
    for _ in range(max_iterations):
        # Generate a small step left or right
        next_x = x + random.choice([-step_size, step_size])

        # Move only if the new position has a better value
        if objective_function(next_x) > objective_function(x):
            x = next_x
    
    return x, objective_function(x)

# Run the algorithm from a random start point
start_x = random.uniform(0, 6)  # Start anywhere in range [0, 6]
best_x, best_y = hill_climb(start_x)

print(f"Best x: {best_x:.2f}, Best y: {best_y:.2f}")
```

---

### **🔹 How it Works**

1. **Starts at a random position** between 0 and 6.
2. **Moves left or right in small steps** (`step_size=0.1`).
3. **If the new position is better**, it moves there.
4. **Stops when no better move is found**.

---

### **🔹 Output Example**

```
Best x: 3.00, Best y: 9.00
```

🎯 It correctly finds **x = 3**, where the function reaches its maximum!

---
---

![](data:image/png;base64,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)

## **🔍 Problem-Solving Agent – Explained 🚀**

### **🔹 What is a Problem-Solving Agent?**

A **problem-solving agent** is an **AI-based system** that **decides and executes actions** to achieve a **specific goal** by searching for an optimal solution. It **analyzes the current state, applies search algorithms, and finds the best action sequence** to reach the goal.

---

### **🔹 Key Components of a Problem-Solving Agent**

1️⃣ **Initial State** → The starting point of the problem.  
2️⃣ **Goal State** → The desired outcome or solution.  
3️⃣ **Actions** → A set of valid moves to transition between states.  
4️⃣ **Transition Model** → Defines how an action changes the current state.  
5️⃣ **Path Cost** → The cost of reaching a state (e.g., distance, time, resources).  
6️⃣ **Search Algorithm** → A method for finding the best sequence of actions.

---

### **🔹 How a Problem-Solving Agent Works**

1. **Receives a problem (Initial State & Goal State).**
2. **Explores possible actions & applies a search algorithm.**
3. **Finds the best sequence of actions to reach the goal.**
4. **Executes the actions & reaches the goal efficiently.**

---

### **🔹 Example: A Problem-Solving Agent in Action**

#### **🛣️ Example: Pathfinding Agent (Self-Driving Car)**

- **Initial State:** Car at Location A.
- **Goal State:** Reach Location B.
- **Actions:** Move Left, Move Right, Move Forward, Stop.
- **Transition Model:** Defines how each move affects the car’s position.
- **Path Cost:** Distance traveled or fuel used.
- **Search Algorithm:** A* Search (shortest path algorithm).

🔹 **Output:** The agent finds the **shortest path** to reach the destination.

---

### **🔹 Types of Problem-Solving Approaches**

|**Type**|**Description**|**Example**|
|---|---|---|
|**Uninformed Search**|No prior knowledge, explores blindly.|BFS, DFS, Uniform Cost Search|
|**Informed Search**|Uses heuristics to guide search.|A* Search, Best-First Search|
|**Local Search**|Focuses on improving a single solution iteratively.|Hill Climbing, Simulated Annealing|

---

### **🔹 Summary**

✅ **A Problem-Solving Agent:**

- **Finds an optimal sequence of actions to reach a goal.**
- __Uses search algorithms (BFS, A_, etc.)._*
- **Can be applied to AI, robotics, gaming, and real-world problems.**

---

## **What is Local Search? 

- Local search are used to deal with problems where only solution state configuration is important example 8-queen,factory floor layout speech handwriting recognition 
    
- Local search is a search algorithm used to find a good solution without exploring the entire search space. 
    
- It starts from a solution and gradually improves it by making small changes. 
    
- It does not store paths, only the current state and its neighboring states. 
    

🔹 Example: 

- Imagine finding the highest mountain peak in a range. You start climbing and always move to a higher point until you reach the top. 
    

  ---

### **What is an Optimization Problem? 

- An optimization problem is about finding the best possible solution from many choices. 
    
- The goal is to maximize or minimize a function. 
    
- Examples:  
    
    - Finding the shortest route between two cities. 
        
    - Minimizing delivery costs for a company. 
        

  
---
### **How Local Search Solves Optimization Problems? 

Local search is used to find the best solution efficiently. 

- It starts with a random solution. 
    
- It modifies it slightly to check if it improves. 
    
- It continues until no further improvement is possible. 
    

🔹 Example: 

- Suppose a company wants to schedule shifts to minimize costs. 
    
- It starts with a random schedule and gradually swaps shifts to reduce expenses. 
    

  
---
### **Types of Local Search Algorithms 

|                     |                                                                          |                                                       |
| ------------------- | ------------------------------------------------------------------------ | ----------------------------------------------------- |
| Algorithm           | How It Works                                                             | Example                                               |
| Hill Climbing       | Always moves to a better solution until no improvement is possible.      | Finding the highest mountain peak.                    |
| Simulated Annealing | Sometimes accepts a worse solution to escape local optima.               | Avoiding getting stuck on a small hill when climbing. |
| Genetic Algorithm   | Uses natural selection (mutation, crossover) to evolve better solutions. | Optimizing robot movement.                            |

  ---

### ***Summary 

- Local Search: Searches for a solution without exploring all possibilities. 
    
- Optimization Problem: Finds the best solution by maximizing or minimizing a function. 
    
- Examples: Finding shortest paths, reducing costs, scheduling tasks.

---
---

## **🔍 Heuristic Function in AI – Explained 🚀**

### **🔹 What is a Heuristic Function?**

A **heuristic function** h(n)h(n) is used in **informed search algorithms** to estimate the **cost from the current state to the goal state**. It **guides the search** toward the most promising path and helps **improve efficiency**.

✅ **Heuristics make search algorithms faster by prioritizing good paths instead of exploring all possibilities.**

---

## **🔹 Types of Heuristic Functions**

| **Type**                             | **Description**                                                             | **Example**                       |
| ------------------------------------ | --------------------------------------------------------------------------- | --------------------------------- |
| **Admissible Heuristic**             | Never overestimates the actual cost to reach the goal (ensures optimality). | Manhattan Distance in A* Search.  |
| **Consistent (Monotonic) Heuristic** | The estimated cost never decreases along a path.                            | Euclidean Distance in Navigation. |
| **Relaxed Heuristic**                | Derived by relaxing problem constraints (simplifies the problem).           | Ignoring walls in a maze.         |
| **Inadmissible Heuristic**           | May overestimate, leading to a non-optimal solution but faster search.      | Weighted A* Search.               |

---

## **🔹 Example of Heuristic Functions**
### **🔹 Real-Life Problem: Finding the Shortest Route to a Coffee Shop ☕**

#### **📌 Problem Statement:**

Imagine you are at **Home** and want to go to a **Coffee Shop** in your city. There are multiple roads, but some are longer than others. Your goal is to find the **shortest possible route** to the Coffee Shop.

---

### **🔹 Heuristic Function: Straight-Line Distance**

💡 A simple heuristic to estimate the remaining distance to the Coffee Shop is the **Straight-Line Distance** between your current position and the Coffee Shop.

h(n)=Straight-line distance from current location to the Coffee Shoph(n) = \text{Straight-line distance from current location to the Coffee Shop}

This heuristic **ignores obstacles like traffic lights or turns**, but it still gives a rough idea of which direction to go.

---

### **🔹 Example Locations (Simplified Map)**

|Location|Coordinates (x, y)|
|---|---|
|🏠 **Home**|(0, 0)|
|🏫 **School**|(2, 4)|
|🏢 **Office**|(5, 2)|
|☕ **Coffee Shop**|(6, 6)|

---

### **🔹 Applying Heuristic Values**

| Location                | Real Distance to Coffee Shop | Heuristic (Straight-Line) |
| ----------------------- | ---------------------------- | ------------------------- |
| 🏠 **Home (0,0)**       | 10 steps                     | 8.5 (estimated)           |
| 🏫 **School (2,4)**     | 5 steps                      | 4.5                       |
| 🏢 **Office (5,2)**     | 6 steps                      | 5                         |
| ☕ **Coffee Shop (6,6)** | **0 (Goal Reached)**         | 0                         |

✅ **The heuristic helps prioritize locations closer to the goal** instead of checking every path randomly.

---
### **🔹 Key Takeaways**

✔ **Heuristic functions provide an estimate to guide search.**  
✔ **Straight-line distance is a simple and intuitive heuristic.**  
✔ **Real-world applications:** GPS navigation, Google Maps, self-driving cars, etc.
✔ **Heuristic functions improve search efficiency.**  
✔ **Good heuristics (admissible & consistent) guarantee optimal solutions.**  
✔ __A_ Search is one of the best search algorithms using heuristics._*

---
## __🔍 Comparison Between Depth-First Search (DFS) & Best-First Search (BFS_)_*

|**Feature**|**Depth-First Search (DFS)**|__Best-First Search (BFS_)_*|
|---|---|---|
|**Search Strategy**|Explores **deepest nodes first** (LIFO - Stack).|Explores **most promising nodes first** based on heuristic.|
|**Data Structure Used**|**Stack** (or recursion).|**Priority Queue** (sorted by heuristic function).|
|**Completeness**|❌ **Not always complete** (may go in infinite loops).|✅ **Complete** if heuristic is good.|
|**Optimality**|❌ **Not optimal** (may find suboptimal paths).|✅ **Can be optimal** if heuristic is admissible.|
|**Time Complexity**|**O(b^d)** (exponential, bad for deep trees).|**O(b^d)** (depends on heuristic).|
|**Space Complexity**|**O(d)** (better than BFS).|**O(b^d)** (stores all nodes in priority queue).|
|**Use Cases**|**Solving puzzles, maze solving** when deep paths matter.|__Pathfinding (A_), GPS navigation, AI in games._*|

---

### **🔹 Example**

#### **🎯 Problem: Finding a Path to a Treasure Chest**

Imagine a pirate is navigating an island to find a **hidden treasure**.

- **DFS**: Moves **deep into one path first**, might take wrong routes before backtracking.
- **Best-First Search**: Uses a **heuristic (distance to treasure)** to choose the best path first.

---

### **🔹 Key Takeaways**

✔ **DFS is useful when memory is limited but may go down the wrong path.**  
✔ **Best-First Search is better for pathfinding due to heuristic guidance.**  
✔ **Best-First Search is often used in AI, while DFS is common in puzzles & graphs.**

---
