https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

https://tinyurl.com/DL-ITALY
https://colab.research.google.com/drive/1Cfq6ju2CDB0c3CYbGeFn18fCS4DWOJ05?usp=sharing

# Text Classification using Simple RNN
```python
import tensorflow as tf
from tensorflow.keras.datasets import imdb
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, SimpleRNN, Dense

vocab_size = 10000
(X_train, y_train), (X_test, y_test) = imdb.load_data(num_words=vocab_size)

max_len = 200
X_train = pad_sequences(X_train, maxlen=max_len)
X_test = pad_sequences(X_test, maxlen=max_len)

model_rnn = Sequential()
model_rnn.add(Embedding(input_dim=vocab_size, output_dim=128, input_length=max_len))
model_rnn.add(SimpleRNN(64))
model_rnn.add(Dense(1, activation='sigmoid'))

model_rnn.compile(loss='binary_crossentropy',
                  optimizer='adam',
                  metrics=['accuracy'])

model_rnn.fit(X_train, y_train, epochs=3, batch_size=64, validation_split=0.2)

loss, acc = model_rnn.evaluate(X_test, y_test)
print("RNN Test Accuracy:", acc)
```

# SentimentRNN
```python
import tensorflow as tf
from tensorflow.keras.datasets import imdb
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, SimpleRNN, Dense
vocab_size = 10000
(X_train, y_train), (X_test, y_test) = imdb.load_data(num_words=vocab_size)
max_len = 200
X_train = pad_sequences(X_train, maxlen=max_len)
X_test = pad_sequences(X_test, maxlen=max_len)
model = Sequential([
    Embedding(vocab_size, 128, input_length = max_len),
    SimpleRNN(64),
    Dense(1, activation='sigmoid')
])
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
model.fit(X_train, y_train, epochs=3, batch_size=64, validation_split=0.2)
model.evaluate(X_test, y_test)
```

# LSTM-NewsClassify
```python
import tensorflow as tf
from tensorflow.keras.datasets import reuters
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, LSTM, Dense, Dropout
vocab_size, max_len = 10000, 200
(X_train, y_train), (X_test, y_test) = reuters.load_data(num_words=vocab_size)
X_train = pad_sequences(X_train, maxlen=max_len, dtype='int32')
X_test  = pad_sequences(X_test,  maxlen=max_len, dtype='int32')
model = Sequential([
    Embedding(vocab_size, 128),              # removed input_length (fix)
    LSTM(64, dropout=0.2),                  # removed recurrent_dropout (Windows-safe)
    Dense(64, activation='relu'),
    Dropout(0.3),
    Dense(46, activation='softmax')
])
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
model.fit(X_train, y_train,
          epochs=8,
          batch_size=64,
          validation_split=0.2,
          verbose=1)
loss, acc = model.evaluate(X_test, y_test)
print(f"Test Accuracy: {acc:.4f}")
```

# Fake News Classification (Error-Free Version)
```python
import tensorflow as tf
from tensorflow.keras.datasets import imdb
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, LSTM, Dense, Dropout
import numpy as np
vocab_size, max_len = 10000, 200
(X_train, y_train), (X_test, y_test) = imdb.load_data(num_words=vocab_size)
X_train = pad_sequences(X_train, maxlen=max_len, dtype='int32')
X_test  = pad_sequences(X_test,  maxlen=max_len, dtype='int32')
y_train = np.array(y_train).astype('float32')
y_test  = np.array(y_test).astype('float32')
model = Sequential([
    Embedding(vocab_size, 128),
    LSTM(64, dropout=0.2),
    Dense(32, activation='relu'),
    Dropout(0.3),
    Dense(1, activation='sigmoid')
])
model.compile(optimizer='adam',
              loss='binary_crossentropy',
              metrics=['accuracy'])
model.fit(X_train, y_train,
          epochs=6,
          batch_size=64,
          validation_split=0.2,
          verbose=1)
loss, acc = model.evaluate(X_test, y_test)
print(f"Test Accuracy: {acc:.4f}")
```

# Deep Autoencoder (Optimized)
```python
import numpy as np
import matplotlib.pyplot as plt
from tensorflow.keras import regularizers
from tensorflow.keras.datasets import fashion_mnist
from tensorflow.keras.models import Model
from tensorflow.keras.layers import Dense, Input, Dropout
(X_train, _), (X_test, _) = fashion_mnist.load_data()
X_train, X_test = X_train.reshape(-1,784)/255.0, X_test.reshape(-1,784)/255.0
input_dim, latent_dim = 784, 64
inp = Input(shape=(input_dim,))
x = Dense(512, 'relu', kernel_regularizer=regularizers.l2(1e-5))(inp)
x = Dropout(0.2)(x)
x = Dense(256, 'relu')(x)
x = Dense(128, 'relu')(x)
encoded = Dense(latent_dim, 'relu')(x)
x = Dense(128, 'relu')(encoded)
x = Dense(256, 'relu')(x)
x = Dense(512, 'relu')(x)
out = Dense(input_dim, 'sigmoid')(x)
autoencoder = Model(inp, out)
autoencoder.compile('adam', 'mse')
autoencoder.fit(X_train, X_train, epochs=10, batch_size=128,
                validation_data=(X_test, X_test), verbose=0)
decoded = autoencoder.predict(X_test[:10])
print(f"Input: {input_dim}, Latent: {latent_dim}, Compression: {input_dim/latent_dim:.1f}")
print("Architecture: 512-256-128-64-128-256-512 (L2 + Dropout)")
fig, ax = plt.subplots(2,10, figsize=(15,4))
for i in range(10):
    for j, data in enumerate([X_test, decoded]):
        ax[j,i].imshow(data[i].reshape(28,28), cmap='gray')
        ax[j,i].axis('off')
ax[0,0].set_title("Original")
ax[1,0].set_title("Reconstructed")
plt.show()
```

# DimensionRedAutoEncoder
```python
import numpy as np
import matplotlib.pyplot as plt
from tensorflow.keras.layers import Dense, Input
from tensorflow.keras.models import Model
from tensorflow.keras.datasets import mnist
(X_train, y_train), _ = mnist.load_data()
X_train = X_train.reshape(-1,784)/255.0
original_dim, reduced_dim = 784, 32
inp = Input(shape=(original_dim,))
x = Dense(256, 'relu')(inp)
x = Dense(128, 'relu')(x)
encoded = Dense(reduced_dim, 'relu')(x)
x = Dense(128, 'relu')(encoded)
x = Dense(256, 'relu')(x)
out = Dense(original_dim, 'sigmoid')(x)
autoencoder = Model(inp, out)
encoder = Model(inp, encoded)
autoencoder.compile('adam', 'mse')
autoencoder.fit(X_train, X_train, epochs=10, batch_size=256, verbose=0)
features = encoder.predict(X_train)
decoded = autoencoder.predict(X_train[:1000])
mse = np.mean((X_train[:1000] - decoded)**2)
reduction = (1 - reduced_dim/original_dim) * 100
print(f"Original: {original_dim}, Reduced: {reduced_dim}, Reduction: {reduction:.2f}%")
print(f"MSE: {mse:.6f}, Encoded Shape: {features.shape}")
decoded_vis = autoencoder.predict(X_train[:10])
mse_vis = np.mean((X_train[:10] - decoded_vis)**2)
fig, ax = plt.subplots(2,10, figsize=(15,4))
for i in range(10):
    for j, data in enumerate([X_train, decoded_vis]):
        ax[j,i].imshow(data[i].reshape(28,28), cmap='gray')
        ax[j,i].axis('off')
ax[0,0].set_title("Original")
ax[1,0].set_title("Reconstructed")
plt.suptitle(f"MSE (10 samples): {mse_vis:.6f}")
plt.tight_layout()
plt.show()
plt.scatter(features[:5000,0], features[:5000,1],
            c=y_train[:5000], cmap='tab10', s=5)
plt.colorbar()
plt.title("Latent Space")
plt.show()
```


# DnoiseAutoE/ncoders
```python
import torch, torch.nn as nn, torch.optim as optim
from torchvision import datasets, transforms
from torch.utils.data import DataLoader
import matplotlib.pyplot as plt
class DAE(nn.Module):
    def __init__(self, d):
        super().__init__()
        self.encoder = nn.Sequential(nn.Linear(d,256), nn.ReLU(),
                                     nn.Linear(256,128), nn.ReLU(),
                                     nn.Linear(128,64), nn.ReLU())
        self.decoder = nn.Sequential(nn.Linear(64,128), nn.ReLU(),
                                     nn.Linear(128,256), nn.ReLU(),
                                     nn.Linear(256,d), nn.Sigmoid())
    def forward(self,x): return self.decoder(self.encoder(x))
add_noise = lambda x, f=0.3: torch.clamp(x + f*torch.randn_like(x), 0., 1.)
def train(model, loader, e=20, lr=1e-3):
    opt, loss_fn = optim.Adam(model.parameters(), lr), nn.MSELoss()
    for ep in range(e):
        total = 0
        for x,_ in loader:
            x = x.view(x.size(0), -1)
            noisy = add_noise(x)
            opt.zero_grad()
            out = model(noisy)
            loss = loss_fn(out, x)
            loss.backward()
            opt.step()
            total += loss.item()
        print(f"Epoch {ep+1}, Loss: {total:.4f}")
data = DataLoader(
    datasets.MNIST('./data', train=True, download=True,
                   transform=transforms.ToTensor()),
    batch_size=128, shuffle=True
)
model = DAE(784)
train(model, data)
x,_ = next(iter(data))
x = x.view(x.size(0), -1)
noisy = add_noise(x)
rec = model(noisy)
plt.figure(figsize=(12,5))
for i in range(5):
    for j, img, title in [(0,x,"Original"), (1,noisy,"Noisy"), (2,rec,"Reconstructed")]:
        plt.subplot(3,5,i+1+j*5)
        plt.imshow(img[i].view(28,28).detach().numpy(), cmap='gray')
        plt.title(title)
        plt.axis("off")
plt.tight_layout()
plt.show()
```


# Vanilla Gans

```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, LeakyReLU
import numpy as np
import matplotlib.pyplot as plt

(X_train, _), _ = tf.keras.datasets.mnist.load_data()
X_train = X_train / 255.0
X_train = X_train.reshape(-1, 784)
latent_dim = 100

generator = Sequential([
    Dense(256, input_dim=latent_dim),
    LeakyReLU(0.2),
    Dense(512),
    LeakyReLU(0.2),
    Dense(784, activation='sigmoid')
])
discriminator = Sequential([
    Dense(512, input_dim=784),
    LeakyReLU(0.2),
    Dense(256),
    LeakyReLU(0.2),
    Dense(1, activation='sigmoid')
])

discriminator.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
discriminator.trainable = False

gan = Sequential([generator, discriminator])
gan.compile(optimizer='adam', loss='binary_crossentropy')
epochs = 1000
batch_size = 128

for epoch in range(epochs):
    idx = np.random.randint(0, X_train.shape[0], batch_size)
    real_imgs = X_train[idx]

    noise = np.random.normal(0, 1, (batch_size, latent_dim))
    fake_imgs = generator.predict(noise, verbose=0)

    d_loss_real = discriminator.train_on_batch(real_imgs, np.ones((batch_size, 1)))
    d_loss_fake = discriminator.train_on_batch(fake_imgs, np.zeros((batch_size, 1)))

    noise = np.random.normal(0, 1, (batch_size, latent_dim))
    g_loss = gan.train_on_batch(noise, np.ones((batch_size, 1)))

    if epoch % 200 == 0:
        print(f"Epoch {epoch}, D Loss: {d_loss_real[0] + d_loss_fake[0]}, G Loss: {g_loss}")

noise = np.random.normal(0, 1, (9, latent_dim))
generated_imgs = generator.predict(noise, verbose=0)

plt.figure(figsize=(6,6))
for i in range(9):
    plt.subplot(3,3,i+1)
    plt.imshow(generated_imgs[i].reshape(28,28), cmap='gray')
    plt.axis('off')

plt.suptitle("Generated Images using GAN")
plt.tight_layout()
plt.show()
```

https://colab.research.google.com/drive/1Cfq6ju2CDB0c3CYbGeFn18fCS4DWOJ05?usp=sharing
https://tinyurl.com/DL-ITALY


# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
