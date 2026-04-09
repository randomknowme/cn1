https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

# Minimax and Alpha-Beta Pruning
```python
# Tree structure (manual representation)
tree = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F', 'G'],
    'D': [3, 5],
    'E': [2, 9],
    'F': [0, 7],
    'G': [1, 8]
}

visited_minimax = 0
visited_ab = 0

# ---------------- MINIMAX ----------------
def minimax(node, is_max):
    global visited_minimax
    visited_minimax += 1

    # Leaf node
    if isinstance(node, int):
        return node

    if is_max:
        return max(minimax(child, False) for child in tree[node])
    else:
        return min(minimax(child, True) for child in tree[node])

# ---------------- ALPHA-BETA ----------------
def alpha_beta(node, alpha, beta, is_max):
    global visited_ab
    visited_ab += 1

    if isinstance(node, int):
        return node

    if is_max:
        value = float('-inf')
        for child in tree[node]:
            value = max(value, alpha_beta(child, alpha, beta, False))
            alpha = max(alpha, value)
            if beta <= alpha:
                print("Pruned at:", child)
                break
        return value
    else:
        value = float('inf')
        for child in tree[node]:
            value = min(value, alpha_beta(child, alpha, beta, True))
            beta = min(beta, value)
            if beta <= alpha:
                print("Pruned at:", child)
                break
        return value

# Run
print("Minimax Value:", minimax('A', True))
print("Nodes Visited (Minimax):", visited_minimax)

print("\nAlpha-Beta Value:", alpha_beta('A', float('-inf'), float('inf'), True))
print("Nodes Visited (Alpha-Beta):", visited_ab)
```


# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
