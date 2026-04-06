https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

https://colab.research.google.com/drive/1X2dGROXlIoXCn41NOHh-NPqjwi1NdqQg?usp=sharing

# Boltzmann.py
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.neural_network import BernoulliRBM
from sklearn.datasets import fetch_openml
from sklearn.preprocessing import MinMaxScaler
mnist = fetch_openml('mnist_784', version=1)
X = mnist.data
scaler = MinMaxScaler()
X = scaler.fit_transform(X)
rbm = BernoulliRBM(n_components=100, learning_rate=0.01, n_iter=10, verbose=True)
rbm.fit(X)
plt.figure(figsize=(10,10))
for i, comp in enumerate(rbm.components_[:16]):
    plt.subplot(4,4,i+1)
    plt.imshow(comp.reshape(28,28), cmap='gray')
    plt.axis('off')
plt.show()
```


# Eigen.py

```python
import numpy as np
from sklearn.datasets import load_iris
from sklearn.preprocessing import StandardScaler
iris = load_iris()
X = iris.data
print("Original Data Shape:", X.shape)
scaler = StandardScaler()
X_std = scaler.fit_transform(X)
cov_matrix = np.cov(X_std.T)
eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)
print("\nEigenvalues:\n", eigenvalues)
print("\nEigenvectors:\n", eigenvectors)
sorted_index = np.argsort(eigenvalues)[::-1]
eigenvalues = eigenvalues[sorted_index]
eigenvectors = eigenvectors[:, sorted_index]
principal_components = eigenvectors[:, 0:2]
X_reduced = np.dot(X_std, principal_components)
print("\nReduced Data Shape:", X_reduced.shape)
print("\nFirst 5 Reduced Values:\n", X_reduced[:5])
```


# Hopfield.py
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import fetch_openml
def show(x, t):
    plt.imshow(x.reshape(28,28), cmap='gray')
    plt.title(t); plt.axis('off'); plt.show()
def bin(x): return np.where(x > 0.5, 1, -1)
def noise(x, p):
    i = np.random.choice(len(x), int(p*len(x)), False)
    x = x.copy(); x[i] *= -1
    return x
mnist = fetch_openml('mnist_784', version=1)
X = mnist.data.to_numpy()/255
y = mnist.target.astype(int)
p1 = bin(X[y==3][0])
p2 = bin(X[y==8][0])
W = np.outer(p1,p1) + np.outer(p2,p2)
np.fill_diagonal(W,0)
W = W / len(p1)
n = noise(p1, 0.35)
for _ in range(15):
    for i in range(len(n)):
        n[i] = 1 if np.dot(W[i], n) >= 0 else -1
show(p1,"Original")
show(n,"Restored")
```


# SOM.py
```python
!pip install minisom
#-----------------
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.preprocessing import MinMaxScaler
from minisom import MiniSom
data = load_iris()
X = data.data
X_scaled = MinMaxScaler().fit_transform(X)
som = MiniSom(8, 8, 4, sigma=1.0, learning_rate=0.5)
som.random_weights_init(X_scaled)
som.train_random(X_scaled, 100)
plt.figure(figsize=(8,8))
for i, x in enumerate(X_scaled):
    w = som.winner(x)
    plt.text(w[0]+0.5, w[1]+0.5, str(data.target[i]), color='red', fontsize=9)
plt.title("SOM Clustering - Iris Dataset")
plt.xlim([0,8])
plt.ylim([0,8])
plt.grid()
plt.show()
```

https://colab.research.google.com/drive/1X2dGROXlIoXCn41NOHh-NPqjwi1NdqQg?usp=sharing

# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
