https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

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

# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
