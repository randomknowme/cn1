https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

Got it 👍 — I’ve **only removed the extra blank lines** and **kept everything else exactly the same (no logic changes, no edits)**.

---

# 1️⃣ Predict House Prices Based on a Single Feature

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import fetch_california_housing
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
housing = fetch_california_housing()
X = housing.data[:, 3].reshape(-1,1)
y = housing.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
plt.scatter(X_test, y_test, color='blue', label='Actual Prices')
plt.plot(X_test, y_pred, color='red', label='Predicted Prices')
plt.xlabel("Average Number of Rooms")
plt.ylabel("House Price")
plt.title("House Price Prediction using Linear Regression")
plt.legend()
plt.show()
```

---

# 2️⃣ Decision Tree Classification on Iris Dataset

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.tree import plot_tree
from sklearn.metrics import accuracy_score
iris = load_iris()
X = iris.data
y = iris.target
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
model = DecisionTreeClassifier()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print("Accuracy:", accuracy)
plt.figure(figsize=(12,8))
plot_tree(
    model,
    feature_names=iris.feature_names,
    class_names=iris.target_names,
    filled=True
)
plt.title("Decision Tree for Iris Classification")
plt.show()
```

---

# 3️⃣ Binary Classification

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score
iris = load_iris()
X = iris.data[:, :2]
y = (iris.target == 0).astype(int)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)
model = LogisticRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
x_min, x_max = X[:,0].min()-1, X[:,0].max()+1
y_min, y_max = X[:,1].min()-1, X[:,1].max()+1
xx, yy = np.meshgrid(
    np.arange(x_min, x_max, 0.1),
    np.arange(y_min, y_max, 0.1)
)
Z = model.predict(np.c[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)
plt.contourf(xx, yy, Z)
plt.scatter(X[:,0], X[:,1], c=y)
plt.xlabel("Sepal Length")
plt.ylabel("Sepal Width")
plt.title("Logistic Regression Decision Boundary")
plt.show()
```

---

# 4️⃣ Linear Regression

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
iris = load_iris()
X = iris.data[:, 0].reshape(-1, 1)
y = iris.data[:, 2]
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
plt.scatter(X_test, y_test, color='blue', label='Actual')
plt.plot(X_test, y_pred, color='red', label='Predicted')
plt.xlabel("Sepal Length")
plt.ylabel("Petal Length")
plt.title("Linear Regression on Iris Dataset")
plt.legend()
plt.show()
```

---

# 5️⃣ Logistic Regression + Confusion Matrix

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, confusion_matrix
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
from sklearn.preprocessing import StandardScaler
data = load_breast_cancer()
X = pd.DataFrame(data.data, columns=data.feature_names)
y = pd.Series(data.target)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
model = LogisticRegression()
model.fit(X_train_scaled, y_train)
y_pred = model.predict(X_test_scaled)
print("Accuracy:", accuracy_score(y_test, y_pred))
print("Precision:", precision_score(y_test, y_pred))
print("Recall:", recall_score(y_test, y_pred))
print("F1 Score:", f1_score(y_test, y_pred))
conf_matrix = confusion_matrix(y_test, y_pred)
print("Confusion Matrix:")
print(conf_matrix)
plt.imshow(conf_matrix)
plt.title("Confusion Matrix")
plt.xlabel("Predicted Label")
plt.ylabel("True Label")
plt.show()
print(classification_report(y_test, y_pred, target_names=data.target_names))
```

---

(Reply continues if you want 6–11 in same compressed format — I can also give **ultra-compact exam sheet version**)
Continuing with **6️⃣ to 1️⃣1️⃣** — same rule applied: **only removed extra blank lines, nothing else changed** 👇

---

# 6️⃣ Feedforward Neural Network (Different Optimizers)

```python id="r9k2vl"
import numpy as np
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.metrics import accuracy_score
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import Adam, SGD, RMSprop
iris = load_iris()
X, y = iris.data, iris.target
scaler = StandardScaler()
X = scaler.fit_transform(X)
encoder = OneHotEncoder(sparse_output=False)
y = encoder.fit_transform(y.reshape(-1, 1))
X_train, X_test, y_train, y_test = train_test_split(X, y,
test_size=0.3, random_state=42)
def build_and_train_model(optimizer_name, optimizer_instance):
    print(f"\n--- Training with {optimizer_name} ---")
    model = Sequential([
        Dense(10, input_dim=X_train.shape[1], activation='relu'),
        Dense(10, activation='relu'),
        Dense(3, activation='softmax')
    ])
    model.compile(optimizer=optimizer_instance,
                  loss='categorical_crossentropy',
                  metrics=['accuracy'])
    history = model.fit(X_train, y_train, epochs=50, batch_size=5,
                        validation_split=0.2, verbose=0)
    y_pred = model.predict(X_test, verbose=0)
    y_pred_classes = np.argmax(y_pred, axis=1)
    y_test_classes = np.argmax(y_test, axis=1)
    accuracy = accuracy_score(y_test_classes, y_pred_classes)
    print(f"Test Accuracy with {optimizer_name}: {accuracy:.4f}")
    return accuracy
optimizers = {
    "SGD": SGD(learning_rate=0.01),
    "Adam": Adam(learning_rate=0.001),
    "RMSprop": RMSprop(learning_rate=0.001)
}
performance_results = {}
for name, optimizer in optimizers.items():
    acc = build_and_train_model(name, optimizer)
    performance_results[name] = acc
print("\n--- Summary of Performance ---")
for name, accuracy in performance_results.items():
    print(f"{name}: {accuracy:.4f} accuracy")
```

---

# 7️⃣ Feedforward Neural Network with Regularization

```python id="k1d8xt"
import tensorflow as tf
from tensorflow.keras import layers, models, regularizers
from tensorflow.keras.datasets import mnist
import pandas as pd
import time
(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train = x_train / 255.0
x_test = x_test / 255.0
x_train = x_train.reshape(-1, 784)
x_test = x_test.reshape(-1, 784)
def build_model(reg_type=None):
    model = models.Sequential()
    if reg_type == "L1":
        reg = regularizers.l1(0.001)
    elif reg_type == "L2":
        reg = regularizers.l2(0.001)
    else:
        reg = None
    model.add(layers.Dense(128, activation='relu',
                            kernel_regularizer=reg,
                            input_shape=(784,)))
    if reg_type == "Dropout":
        model.add(layers.Dropout(0.5))
    model.add(layers.Dense(64, activation='relu',
                            kernel_regularizer=reg))
    if reg_type == "Dropout":
        model.add(layers.Dropout(0.5))
    model.add(layers.Dense(10, activation='softmax'))
    return model
regularization_methods = [
    "None",
    "L1",
    "L2",
    "Dropout"
]
results = []
for reg in regularization_methods:
    print(f"\nTraining model with {reg} regularization")
    model = build_model(None if reg == "None" else reg)
    model.compile(
        optimizer='adam',
        loss='sparse_categorical_crossentropy',
        metrics=['accuracy']
    )
    start_time = time.time()
    model.fit(
        x_train, y_train,
        epochs=10,
        batch_size=128,
        validation_split=0.1,
        verbose=0
    )
    training_time = time.time() - start_time
    test_loss, test_accuracy = model.evaluate(x_test, y_test, verbose=0)
    results.append({
        "Regularization": reg,
        "Test Accuracy": round(test_accuracy, 4),
        "Test Loss": round(test_loss, 4),
        "Training Time (s)": round(training_time, 2)
    })
results_df = pd.DataFrame(results)
print("\nPerformance Comparison:")
print(results_df)
```

---

# 8️⃣ ANN without Backpropagation

```python id="u3pq7n"
import numpy as np
def sigmoid(x):
    return 1 / (1 + np.exp(-x))
def sigmoid_derivative(x):
    return x * (1 - x)
class SimpleNNRandomSearch:
    def __init__(self, input_size, hidden_size, output_size):
        self.input_size = input_size
        self.hidden_size = hidden_size
        self.output_size = output_size
        self.weights_ih = None
        self.weights_ho = None
        self.best_accuracy = 0
    def forward(self, X):
        self.hidden_input = np.dot(X, self.weights_ih)
        self.hidden_output = sigmoid(self.hidden_input)
        self.output_input = np.dot(self.hidden_output, self.weights_ho)
        self.output = sigmoid(self.output_input)
        return self.output
    def calculate_accuracy(self, X, y):
        predictions = (self.forward(X) > 0.5).astype(int)
        accuracy = np.mean(predictions == y)
        return accuracy
    def train_random_search(self, X, y, iterations=1000):
        print(f"Starting random search training for {iterations} iterations...")
        best_weights_ih = np.random.randn(self.input_size,
self.hidden_size) * 0.1
        best_weights_ho = np.random.randn(self.hidden_size,
self.output_size) * 0.1
        for i in range(iterations):
            current_weights_ih = np.random.randn(self.input_size,
self.hidden_size)
            current_weights_ho = np.random.randn(self.hidden_size,
self.output_size)
            self.weights_ih = current_weights_ih
            self.weights_ho = current_weights_ho
            current_accuracy = self.calculate_accuracy(X, y)
            if current_accuracy > self.best_accuracy:
                self.best_accuracy = current_accuracy
                best_weights_ih = current_weights_ih
                best_weights_ho = current_weights_ho
                print(f"Iteration {i}: New best accuracy found:
{self.best_accuracy:.4f}")
                if self.best_accuracy == 1.0:
                    print("Achieved perfect accuracy! Stopping early.")
                    break
        self.weights_ih = best_weights_ih
        self.weights_ho = best_weights_ho
        print(f"Training finished. Final best accuracy:
{self.best_accuracy:.4f}")
X = np.array([[0,0],[0,1],[1,0],[1,1]])
y = np.array([[0],[1],[1],[0]])
INPUT_SIZE = 2
HIDDEN_SIZE = 3
OUTPUT_SIZE = 1
nn = SimpleNNRandomSearch(INPUT_SIZE,HIDDEN_SIZE,OUTPUT_SIZE)
nn.train_random_search(X,y,iterations=5000)
print("\nTesting the trained model:")
predictions = (nn.forward(X)>0.5).astype(int)
print("Inputs:",X)
print("Predicted outputs:",predictions.flatten())
print("Actual outputs:",y.flatten())
```

---

# 9️⃣ ANN with Backpropagation

```python id="d5l2qs"
import numpy as np
class NeuralNetwork:
    def __init__(self,input_size,hidden_size,output_size,learning_rate=0.1):
        self.input_size=input_size
        self.hidden_size=hidden_size
        self.output_size=output_size
        self.learning_rate=learning_rate
        self.weights_ih=np.random.randn(self.input_size,self.hidden_size)*0.01
        self.bias_h=np.random.randn(1,self.hidden_size)*0.01
        self.weights_ho=np.random.randn(self.hidden_size,self.output_size)*0.01
        self.bias_o=np.random.randn(1,self.output_size)*0.01
    def sigmoid(self,x):
        return 1/(1+np.exp(-x))
    def sigmoid_derivative(self,x):
        return x*(1-x)
    def forward_pass(self,X):
        self.hidden_input=np.dot(X,self.weights_ih)+self.bias_h
        self.hidden_output=self.sigmoid(self.hidden_input)
        self.output_input=np.dot(self.hidden_output,self.weights_ho)+self.bias_o
        self.predicted_output=self.sigmoid(self.output_input)
        return self.predicted_output
    def backward_pass(self,X,y,output):
        self.output_error=y-output
        self.output_delta=self.output_error*self.sigmoid_derivative(output)
        self.hidden_error=self.output_delta.dot(self.weights_ho.T)
        self.hidden_delta=self.hidden_error*self.sigmoid_derivative(self.hidden_output)
        self.weights_ho+=self.hidden_output.T.dot(self.output_delta)*self.learning_rate
        self.bias_o+=np.sum(self.output_delta,axis=0,keepdims=True)*self.learning_rate
        self.weights_ih+=X.T.dot(self.hidden_delta)*self.learning_rate
        self.bias_h+=np.sum(self.hidden_delta,axis=0,keepdims=True)*self.learning_rate
    def train(self,X,y,epochs):
        for epoch in range(epochs):
            output=self.forward_pass(X)
            self.backward_pass(X,y,output)
            if epoch%1000==0:
                loss=np.mean(np.square(y-output))
                print(f"Epoch {epoch}, Loss: {loss:.4f}")
        print(f"Final Loss after {epochs} epochs: {np.mean(np.square(y-output)):.4f}")
X=np.array([[0,0],[0,1],[1,0],[1,1]])
y=np.array([[0],[1],[1],[0]])
nn=NeuralNetwork(2,4,1,0.1)
print("Starting training...")
nn.train(X,y,10000)
print("Training finished.")
print("\nTesting results:")
predictions=nn.forward_pass(X)
print("Predicted outputs:")
print(predictions)
print("\nThresholded predictions:")
print((predictions>0.5).astype(int))
```

---

# 🔟 CNN on CIFAR-10 Dataset

```python id="c8p4mj"
import tensorflow as tf
from tensorflow.keras import datasets, layers, models
(train_images, train_labels), (test_images, test_labels) = datasets.cifar10.load_data()
train_images = train_images / 255.0
test_images = test_images / 255.0
model = models.Sequential()
model.add(layers.Conv2D(32,(3,3),activation='relu',input_shape=(32,32,3)))
model.add(layers.MaxPooling2D((2,2)))
model.add(layers.Conv2D(64,(3,3),activation='relu'))
model.add(layers.MaxPooling2D((2,2)))
model.add(layers.Conv2D(64,(3,3),activation='relu'))
model.add(layers.Flatten())
model.add(layers.Dense(64,activation='relu'))
model.add(layers.Dense(10))
model.compile(optimizer='adam',
loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),
metrics=['accuracy'])
model.fit(train_images,train_labels,epochs=10,
validation_data=(test_images,test_labels))
```

---

# 1️⃣1️⃣ Image Classification using CNN

```python id="v0nz6r"
import tensorflow as tf
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras import layers, models
train_datagen = ImageDataGenerator(rescale=1./255)
train_generator = train_datagen.flow_from_directory(
    'dataset/',
    target_size=(150,150),
    batch_size=32,
    class_mode='binary'
)
model = models.Sequential()
model.add(layers.Conv2D(32,(3,3),activation='relu',input_shape=(150,150,3)))
model.add(layers.MaxPooling2D(2,2))
model.add(layers.Conv2D(64,(3,3),activation='relu'))
model.add(layers.MaxPooling2D(2,2))
model.add(layers.Conv2D(128,(3,3),activation='relu'))
model.add(layers.MaxPooling2D(2,2))
model.add(layers.Flatten())
model.add(layers.Dense(128,activation='relu'))
model.add(layers.Dense(1,activation='sigmoid'))
model.compile(
optimizer='adam',
loss='binary_crossentropy',
metrics=['accuracy']
)
model.fit(train_generator,epochs=10)
model.save("cat_dog_classifier.h5")
```

---

If you want next level prep, I can give you:

* 🔥 **Ultra-short viva answers for all 11 (1–2 lines each)**
* 📄 **One-page revision sheet (night-before exam)**
* 🎯 **Important questions examiner might ask from each code**

Just tell me 👍


# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
