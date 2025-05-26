### 🧠 Wumpus World Environment (with PEAS Description)

The **Wumpus World** is a classic example of a simple, turn-based environment used in **Artificial Intelligence** to demonstrate agent behavior in uncertain environments. It was introduced in the book _"Artificial Intelligence: A Modern Approach"_ by Russell & Norvig.

---

### 🌍 **Wumpus World Overview**

- A 4x4 grid of rooms.
    
- The agent’s goal is to find gold and exit the world without dying.
    
- Hazards:
    
    - **Wumpus**: A deadly monster; entering its room means death.
        
    - **Pits**: Bottomless holes; falling into one is fatal.
        
- **Gold**: If found, the agent can grab it and escape for reward.
    
- **Walls**: The agent can't pass through them.
    

#### 🧠 Percepts (what the agent senses):

- **Stench**: Wumpus is in an adjacent square.
    
- **Breeze**: A pit is in an adjacent square.
    
- **Glitter**: Gold is in the same square.
    
- **Bump**: Agent hits a wall.
    
- **Scream**: Wumpus has been killed.
    

---

### 🧩 **PEAS Description (Performance, Environment, Actuators, Sensors)**

|**Component**|**Description**|
|---|---|
|**P** (Performance Measure)|- Find gold- Exit safely- Minimize actions taken- Avoid death (from pits or Wumpus)|
|**E** (Environment)|- 4x4 grid of rooms- Rooms may contain pits, the Wumpus, or gold- Agent starts in (1,1)|
|**A** (Actuators)|- Move forward- Turn left/right- Grab (to take gold)- Shoot (arrow to kill Wumpus)- Climb (to exit)|
|**S** (Sensors)|- Stench (near Wumpus)- Breeze (near pit)- Glitter (gold present)- Bump (wall hit)- Scream (Wumpus killed)|

---

### Example Agent Strategy:

1. **Enter and perceive**.
    
2. If **breeze**, mark adjacent cells as risky.
    
3. If **no stench or breeze**, mark safe.
    
4. Plan safest route to unvisited safe cell.
    
5. Grab gold when glitter is perceived.
    
6. Exit by climbing from the starting cell.
    

---

Let me know if you want a diagram or simulation for this!