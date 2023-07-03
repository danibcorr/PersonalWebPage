---
description: Realizado por Daniel Bazo Correa.
---

# LeNet

Vamos a implementar la arquitectura de LeNet, una arquitectura basada en una red neuronal convolucional propuesta por Yann Lecun en 1998.

[LeNet - Wikipedia](https://en.wikipedia.org/wiki/LeNet)

## 1. Conceptos previos

A continuación se muestra una imagen con algunas de las anotaciones para aclarar ciertos conceptos de la arquitectura y de las modificaciones que vamos a realizar. Con ellas, hemos conseguido una precisión durante el entrenamiento de 99,58 % con una pérdida de 0,0123. En la evaluación del modelo, se ha conseguido una precisión del 98,42 % con una pérdida del 0,0666.

<figure><img src="../../.gitbook/assets/160DD17B-DDE1-4C60-BAF1-A441AF9DBE98.jpeg" alt=""><figcaption></figcaption></figure>

## 2. Código

```python
import tensorflow as tf
from tensorflow.keras import layers, datasets, losses
import numpy as np
import pandas as pd
from sklearn.preprocessing import normalize
import matplotlib.pyplot as plt
from keras.utils.np_utils import to_categorical

# NVIDIA GPU
!nvidia-smi
tf.config.list_physical_devices('GPU')

# Creamos la clase LeNet
class LeNet(tf.keras.Model):

    def __init__(self, num_clases):

        super().__init__()

        self.arquitectura = models.Sequential([
            layers.Conv2D(input_shape = (28, 28, 1), filters = 6, kernel_size = 5, padding = 'same', activation = 'relu'),
            layers.BatchNormalization(),
            layers.MaxPooling2D(pool_size = 2, strides = 2),
            layers.Conv2D(filters = 16, kernel_size = 5, activation = 'relu'),
            layers.BatchNormalization(),
            layers.MaxPooling2D(pool_size = 2, strides = 2),
            
            layers.Flatten(),

            layers.Dense(units = 120, activation = 'relu'),
            layers.Dense(units = 84, activation = 'relu'),
            layers.Dense(units = num_clases, activation = 'softmax'),
        ])

# Hiperpámetros
num_clases = 10
lr = 1e-3
tam_batch = 64
num_epocas = 10

# Creamos una variable modelo con la clase LeNet
modelo = LeNet(num_clases)
print(modelo.arquitectura.summary())

# Descargamos el dataset de MNIST
(x_train, y_train), (x_test, y_test) = datasets.mnist.load_data()

print(f"Dimension x_train: {x_train.shape}")
print(f"Dimension y_train: {y_train.shape}")
print(f"Dimension x_test: {x_test.shape}")
print(f"Dimension y_test: {y_test.shape}")

# Normalización de los datos
x_train = x_train.astype('float32')
x_test = x_test.astype('float32')

x_train = tf.keras.utils.normalize(x_train, axis = 1)
x_test = tf.keras.utils.normalize(x_test, axis = 1)

x_train = np.reshape(x_train, (x_train.shape[0], x_train.shape[1], x_train.shape[1], 1))
x_test = np.reshape(x_test, (x_test.shape[0], x_test.shape[1], x_test.shape[1], 1))

y_train = to_categorical(y_train, num_clases)
y_test = to_categorical(y_test, num_clases)

print(f"Dimension x_train: {x_train.shape}")
print(f"Dimension x_test: {x_test.shape}")
print(f"Dimension y_train: {y_train.shape}")
print(f"Dimension y_test: {y_test.shape}")

# Observamos algunos datos
plt.figure(figsize = (10,10))

for i in range(25):

    plt.subplot(5, 5, i + 1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(x_train[i], cmap = 'gray')
    plt.xlabel(f"Etiqueta: {np.argmax(y_train[i])}", color = 'white')

plt.show()

# Compilamos el modelo
modelo.arquitectura.compile(
    optimizer = tf.optimizers.Adam(learning_rate = lr),
    loss = losses.CategoricalCrossentropy(), 
    metrics = ['accuracy']
)

# Entrenamos el modelo
historia = modelo.arquitectura.fit(
            x_train, y_train,
            batch_size = tam_batch,
            epochs = num_epocas,
            verbose = 1
            )

# Creamos una gráfica para mostrar el accuracy obtenido tanto en el set de entrenamiento como en el de validacion
plt.plot(historia.history['accuracy'])
plt.grid(which = 'both', axis = 'both')
plt.title('Precisión del modelo')
plt.ylabel('Precisión')
plt.xlabel('Época')
plt.legend(['Entrenamiento', 'Test'], loc='upper right')
plt.show()

# Creamos una gráfica para mostrar la función de pérdida obtenida tanto en el set de entrenamiento como en el de validacion
plt.plot(historia.history['loss'])
plt.grid(which = 'both', axis = 'both')
plt.title('Pérdida del modelo')
plt.ylabel('Pérdida')
plt.xlabel('Época')
plt.legend(['Entrenamiento', 'Test'], loc='upper right')
plt.show()

# Evaluamos el modelo en el set de pruebas
# El primer valor obtenido corresponde con la pérdida, el segundo con el accuracy
modelo.arquitectura.evaluate(x_test, y_test)
```
