https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER


https://gist.github.com/KrishnaSrinivas-24/d1cf00ddaba0e17d587db8097bb3e84e#file-monkeybanana-py-L39


---

# 🔵 1️⃣ 8PuzzleProblem.py

### ✅ Sample Input 1 (Simple – 1 Move Away)

```
Enter Initial State:
1 2 3
4 5 6
7 0 8

Enter Goal State:
1 2 3
4 5 6
7 8 0
```

---

### ✅ Sample Input 2 (Moderate Case)

```
Enter Initial State:
1 2 3
4 0 6
7 5 8

Enter Goal State:
1 2 3
4 5 6
7 8 0
```

---

# 🔵 2️⃣ BFS.py (Unweighted Graph)

### ✅ Sample Input

```
Number of nodes: 4

Node: A
Neighbors count: 2
Neighbor: B
Neighbor: C

Node: B
Neighbors count: 1
Neighbor: D

Node: C
Neighbors count: 0

Node: D
Neighbors count: 0

Start node: A
Goal node: D
```

Expected shortest path:

```
A → B → D
```

---

# 🔵 3️⃣ MonkeyBanana.py

### ✅ Sample Input 1

```
Monkey position: entrance
Box position: table
Banana position: window
```

---

### ✅ Sample Input 2 (Easy Case)

```
Monkey position: table
Box position: table
Banana position: table
```

Solution:

```
Climb box
Grab banana
```

---

# 🔵 4️⃣ UCS.py (Weighted Graph)

### ✅ Sample Input

```
Number of nodes: 4

Node: A
Neighbors count: 2
Neighbor: B
Cost: 1
Neighbor: C
Cost: 4

Node: B
Neighbors count: 1
Neighbor: D
Cost: 2

Node: C
Neighbors count: 1
Neighbor: D
Cost: 1

Node: D
Neighbors count: 0

Start node: A
Goal node: D
```

Expected optimal path:

```
A → B → D
Cost = 3
```

(Not A → C → D because that costs 5)

---

# 🔵 5️⃣ VacuumCleaner.py

### ✅ Sample Input

```
Enter location (A/B): A
Enter Room A status (dirty/clean/exit): dirty
Enter Room A status (dirty/clean/exit): clean
Enter Room B status (dirty/clean/exit): dirty
Enter Room B status (dirty/clean/exit): clean
Enter Room A status (dirty/clean/exit): exit
```

---

# 🔵 6️⃣ WaterJug.py

### ✅ Classic Test Case

```
Enter Jug A Capacity: 3
Enter Jug B Capacity: 5
Enter Target in Jug A: 2
```

This is the famous 3L & 5L problem → get 2L.

---

### ✅ Another Test Case

```
Enter Jug A Capacity: 4
Enter Jug B Capacity: 7
Enter Target in Jug A: 5
```


A*
```py
import heapq

# Goal State
goal = ((1,2,3),
        (4,5,6),
        (7,8,0))

# Heuristic: Manhattan Distance
def h(s):
    d = 0
    for i in range(3):
        for j in range(3):
            v = s[i][j]
            if v != 0:
                for x in range(3):
                    for y in range(3):
                        if goal[x][y] == v:
                            d += abs(i-x) + abs(j-y)
    return d

# Get possible moves
def get_neighbors(state):
    neighbors = []
    for i in range(3):
        for j in range(3):
            if state[i][j] == 0:
                x, y = i, j

    directions = [(1,0), (-1,0), (0,1), (0,-1)]

    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < 3 and 0 <= ny < 3:
            new_state = [list(row) for row in state]
            new_state[x][y], new_state[nx][ny] = new_state[nx][ny], new_state[x][y]
            neighbors.append(tuple(tuple(row) for row in new_state))

    return neighbors

def a_star(start):
    pq = []
    heapq.heappush(pq, (h(start), 0, start))
    visited = set()

    while pq:
        f, g, state = heapq.heappop(pq)

        if state == goal:
            print("Goal Reached!")
            return

        if state in visited:
            continue

        visited.add(state)

        for neighbor in get_neighbors(state):
            if neighbor not in visited:
                heapq.heappush(pq, (g + 1 + h(neighbor), g + 1, neighbor))

    print("No solution found.")

# ===== Dynamic Input =====
print("Enter the 8-puzzle start state (use 0 for blank):")

start = []
for i in range(3):
    row = list(map(int, input(f"Enter row {i+1} (3 numbers separated by space): ").split()))
    start.append(tuple(row))

start = tuple(start)

a_star(start)
```

https://gist.github.com/KrishnaSrinivas-24/d1cf00ddaba0e17d587db8097bb3e84e#file-monkeybanana-py-L39

# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
