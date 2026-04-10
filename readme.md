https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER


https://colab.research.google.com/drive/10Arx2Iqr5_7MC2tFUeUACDDaSiG89P0h?usp=sharing


# Minimax and Alpha-Beta Pruning
```python
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

print("Minimax Value:", minimax('A', True))
print("Nodes Visited (Minimax):", visited_minimax)

print("\nAlpha-Beta Value:", alpha_beta('A', float('-inf'), float('inf'), True))
print("Nodes Visited (Alpha-Beta):", visited_ab)
```


# Hangman
```python
import random

words = ["python", "ai", "hangman", "code"]
word = random.choice(words)
guessed = ["_"] * len(word)
attempts = 6

stages = [
    """
     -----
     |   |
         |
         |
         |
         |
    """,
    """
     -----
     |   |
     O   |
         |
         |
         |
    """,
    """
     -----
     |   |
     O   |
     |   |
         |
         |
    """,
    """
     -----
     |   |
     O   |
    /|   |
         |
         |
    """,
    """
     -----
     |   |
     O   |
    /|\\  |
         |
         |
    """,
    """
     -----
     |   |
     O   |
    /|\\  |
    /    |
         |
    """,
    """
     -----
     |   |
     O   |
    /|\\  |
    / \\  |
         |
    """
]

while attempts > 0 and "_" in guessed:
    print(stages[6 - attempts])
    print("Word:", " ".join(guessed))

    guess = input("\nEnter letter: ")

    if guess in word:
        for i in range(len(word)):
            if word[i] == guess:
                guessed[i] = guess

    else:
        attempts -= 1
        print("Wrong guess!")

if "_" not in guessed:
    print("You win! Word:", word)
else:
    print(stages[-1])
    print("Game Over! Word was:", word)
```




# propositional logic
```python
from sympy import symbols
from sympy.logic.boolalg import And, Or, Not, Implies, Equivalent
from sympy.logic.inference import satisfiable

p, q, r = symbols('p q r')

expr1 = And(p, q)
expr2 = Or(p, Not(q))
expr3 = Implies(p, q)
expr4 = Equivalent(p, q)


values = {p: True, q: False}

print("AND:", expr1.subs(values))
print("OR:", expr2.subs(values))
print("IMPLIES:", expr3.subs(values))
print("EQUIVALENT:", expr4.subs(values))

print("Satisfiable:", satisfiable(expr1))

from sympy.logic.boolalg import to_cnf, to_dnf

print("CNF:", to_cnf(expr3))
print("DNF:", to_dnf(expr3))
```




# Decision Tree
```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix, ConfusionMatrixDisplay
iris = load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
df['target'] = iris.target
df = df[df['target'] != 2]
X = df.iloc[:, :-1]
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = DecisionTreeClassifier()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
cm = confusion_matrix(y_test, y_pred)
ConfusionMatrixDisplay(cm).plot()
plt.title("Confusion Matrix")
plt.show()
plt.figure(figsize=(10, 6))
plot_tree(model, feature_names=iris.feature_names, class_names=["setosa", "versicolor"], filled=True)
plt.title("Decision Tree")
plt.show()
```



# Decision Tree CSV 
```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, confusion_matrix, ConfusionMatrixDisplay
df = pd.read_csv("data.csv")
target_col = df.columns[-1]
X = df.drop(columns=[target_col])
y = df[target_col]
if y.dtype == 'object':
    y = y.astype('category').cat.codes
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
model = DecisionTreeClassifier(max_depth=3)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
cm = confusion_matrix(y_test, y_pred)
ConfusionMatrixDisplay(cm).plot()
plt.title("Confusion Matrix")
plt.show()
plt.figure(figsize=(10, 6))
plot_tree(model, feature_names=X.columns, class_names=["Class 0", "Class 1"], filled=True)
plt.title("Decision Tree")
plt.show()
```



# FOL
```python
!pip install pyDatalog
from pyDatalog import pyDatalog
pyDatalog.clear()
pyDatalog.create_terms('A, B, C, relation, ancestor')
n = int(input("How many entries do you want to add? "))
print("Enter data like: relation(john,mary)")
for _ in range(n):
    data = input().replace(" ", "")
    x, y = data[data.find("(")+1:data.find(")")].split(",")
    +relation(x, y)
ancestor(A, C) <= relation(A, B) & relation(B, C)
query = input("\nEnter query (example: relation(john,X) or ancestor(X,susan)): ").replace(" ", "")
name = query[:query.find("(")]
x, y = query[query.find("(")+1:query.find(")")].split(",")
print("\nOutput:")
if name == "relation":
    result = relation(x, y) if y.islower() else relation(x, A)
elif name == "ancestor":
    if x.islower() and y.islower():
        result = ancestor(x, y)
    elif x.islower():
        result = ancestor(x, A)
    else:
        result = ancestor(A, y)
else:
    result = []
if result == []:
    print("False (No matching data)")
elif result == [()]:
    print("True (Exists)")
else:
    print(result)
```

https://colab.research.google.com/drive/10Arx2Iqr5_7MC2tFUeUACDDaSiG89P0h?usp=sharing



# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
