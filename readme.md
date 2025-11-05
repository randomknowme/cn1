https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

https://tinyurl.com/ML-LABEND
https://gist.github.com/KrishnaSrinivas-24/2e89d25af68fe05b3afe694bf8d7cc05

# 1. Support Vector Regression (SVR)

**Aim:**
To implement Support Vector Regression with linear, polynomial and RBF kernels and compare their performance on a sample regression dataset.

**Description:**
This experiment demonstrates how SVR fits a regression function while ignoring small errors inside an epsilon-tube and penalizing larger deviations. You will standardize features/targets, train SVR models using different kernels (linear, poly, RBF), vary hyperparameters `C`, `epsilon`, and `gamma`/`degree`, and visualize predicted vs actual values. The exercise highlights how kernels change the function shape (straight line vs curved vs complex local fits) and how `C` / `epsilon` control bias–variance tradeoffs.

**Expected outcome:**
Students will observe differences in fit quality across kernels, understand the effect of `epsilon` and `C`, and learn to visually and quantitatively compare regression performance (e.g., MSE, plots).

# 2. K-Means Clustering & Image Segmentation

**Aim:**
To apply K-Means clustering for unsupervised color quantization and segment an image into K color regions.

**Description:**
K-Means partitions pixel RGB vectors into `K` clusters by minimizing within-cluster variance; each pixel is mapped to its cluster centroid producing a quantized/segmented image. In the lab you will load an image, reshape pixels to a 2D feature matrix, run KMeans for various `K` values, and reconstruct segmented images. This demonstrates how K-Means groups similar color values and the impact of `K` on coarse vs fine segmentation.

**Expected outcome:**
Students will produce segmented images for different `K`, learn when K-Means works well (compact color clusters) and its limitations (sensitivity to K and initialization).

# 3. DBSCAN Clustering and Anomaly Detection

**Aim:**
To implement DBSCAN for density-based clustering and to detect noise/anomalies in a 2D dataset.

**Description:**
DBSCAN groups points into density-connected clusters using neighborhood radius `eps` and minimum points `min_samples`. Unlike K-Means it does not require `K` and can find arbitrarily shaped clusters and label sparse points as noise. The experiment generates blob data plus outliers, runs DBSCAN, and visualizes core, border, and noise points. You will vary `eps` and `min_samples` to see how cluster membership and anomaly detection change.

**Expected outcome:**
Students will understand density-based clustering concepts, tune DBSCAN parameters to separate clusters from noise, and appreciate DBSCAN’s utility for anomaly detection.

# 4. Perceptron (Single-Layer Neural Network)

**Aim:**
To implement a single-layer perceptron and train it to learn the AND logic gate; explore learning dynamics and the perceptron learning rule.

**Description:**
This experiment covers the perceptron model: weighted sum plus bias followed by a step activation function. You will initialize weights, apply the perceptron update rule across training epochs on the AND dataset, and test predictions. The lab highlights linear separability, weight updates driven by prediction error, and the perceptron’s limitation (cannot solve nonlinearly separable problems like XOR).

**Expected outcome:**
Students will implement training and demonstrate the perceptron correctly classifies AND, learn the update rule’s mechanics, and discuss limitations and extensions (multi-layer networks).

# 5. Artificial Neural Network (ANN) for MNIST

**Aim:**
To build and train a feedforward ANN to classify handwritten digits from the MNIST dataset and evaluate its accuracy.

**Description:**
This experiment uses a multilayer perceptron (input → hidden layers → softmax output) to perform 10-class digit classification. Steps include loading MNIST, normalizing and flattening images, converting labels to one-hot vectors, building an ANN (e.g., 128 → 64 hidden units with ReLU), compiling with an optimizer (Adam) and categorical crossentropy loss, and training with validation. You will observe training/validation loss and accuracy, and evaluate test performance.

**Expected outcome:**
Students will obtain a working classifier with reasonable test accuracy, interpret training curves (overfitting/underfitting), and learn how model size, epochs, and preprocessing affect performance.

---

https://gist.github.com/KrishnaSrinivas-24/2e89d25af68fe05b3afe694bf8d7cc05
https://tinyurl.com/ML-LABEND

# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
