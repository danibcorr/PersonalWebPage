---
description: Realizado por Daniel Bazo Correa.
---

# GoogleLeNet

Vamos a implementar la arquitectura de GoogleLeNet, una arquitectura basada en una red neuronal convolucional caracterizada por contar con unos bloques llamados "Inception", propuesta por Christian Szegedy, Wei Liu, Yangqing Jia, Pierre Sermanet, Scott Reed, Dragomir Anguelov, Dumitru Erhan, Vincent Vanhoucke, Andrew Rabinovich en 2014.

Paper: [https://arxiv.org/abs/1409.4842v1](https://arxiv.org/abs/1409.4842v1)

## 1. Conceptos previos

<figure><img src="../.gitbook/assets/96399E43-0921-4087-91CD-65389E3CBDB6.jpeg" alt=""><figcaption></figcaption></figure>

## 2. Código

```python
import tensorflow as tf
from tensorflow.keras import layers, datasets, losses
import numpy as np
import pandas as pd
from sklearn.preprocessing import normalize
import matplotlib.pyplot as plt
from keras.utils.np_utils import to_categorical
from skimage.transform import resize
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.preprocessing import image as image_utils

# Comprobamos si tenemos una GPU disponible
tf.config.list_physical_devices('GPU')

class Bloque_Conv(layers.Layer):

    def __init__(self, num_filtros, tam_kernel, stride):

        super().__init__()

        self.capa_conv = models.Sequential([
            layers.Conv2D(filters = num_filtros, kernel_size = tam_kernel, padding = 'same', strides = stride, activation = 'relu'),
            layers.BatchNormalization()
        ])

    def call(self, input_tensor):

        return self.capa_conv(input_tensor)

class Bloque_Inception(layers.Layer):

    def __init__(self, num_fil_r1_1, num_fil_r2_1, num_fil_r2_3, num_fil_r3_1, num_fil_r3_5, num_fil_r4_1):

        super().__init__()

        self.rama_1 = Bloque_Conv(num_filtros = num_fil_r1_1, tam_kernel = 1, stride = 1)

        self.rama_2 = models.Sequential([
            Bloque_Conv(num_filtros = num_fil_r2_1, tam_kernel = 1, stride = 1),
            Bloque_Conv(num_filtros = num_fil_r2_3, tam_kernel = 3, stride = 1)
        ])

        self.rama_3 = models.Sequential([
            Bloque_Conv(num_filtros = num_fil_r3_1, tam_kernel = 1, stride = 1),
            Bloque_Conv(num_filtros = num_fil_r3_5, tam_kernel = 5, stride = 1)
        ])

        self.rama_4 = models.Sequential([
            layers.MaxPool2D(pool_size = 3, strides = 1, padding = 'same'),
            Bloque_Conv(num_filtros = num_fil_r4_1, tam_kernel = 1, stride = 1)
        ])

    def call(self, input_tensor): 
    
        return tf.concat([self.rama_1(input_tensor), self.rama_2(input_tensor), self.rama_3(input_tensor), self.rama_4(input_tensor)], axis = 3)

class GoogleLeNet(tf.keras.Model):

    def __init__(self, num_clases):

        super().__init__()

        self.arquitectura = models.Sequential([
            layers.Conv2D(input_shape = (224, 224, 3), padding = 'same', filters = 64, kernel_size = 7, strides = 2, activation = 'relu'),
            layers.BatchNormalization(),
            layers.MaxPool2D(pool_size = 3, strides = 2, padding = 'same'),
            
            Bloque_Conv(num_filtros = 192, tam_kernel = 3, stride = 1),
            layers.MaxPool2D(pool_size = 3, strides = 2, padding = 'same'),
            
            Bloque_Inception(num_fil_r1_1 = 64, num_fil_r2_1 = 96, num_fil_r2_3 = 128, num_fil_r3_1 = 16, num_fil_r3_5 = 32, num_fil_r4_1 = 32),
            Bloque_Inception(num_fil_r1_1 = 128, num_fil_r2_1 = 128, num_fil_r2_3 = 192, num_fil_r3_1 = 32, num_fil_r3_5 = 96, num_fil_r4_1 = 64),
            layers.MaxPool2D(pool_size = 3, strides = 2, padding = 'same'),

            Bloque_Inception(num_fil_r1_1 = 192, num_fil_r2_1 = 96, num_fil_r2_3 = 208, num_fil_r3_1 = 16, num_fil_r3_5 = 48, num_fil_r4_1 = 64),
            Bloque_Inception(num_fil_r1_1 = 160, num_fil_r2_1 = 112, num_fil_r2_3 = 224, num_fil_r3_1 = 24, num_fil_r3_5 = 64, num_fil_r4_1 = 64),
            Bloque_Inception(num_fil_r1_1 = 128, num_fil_r2_1 = 128, num_fil_r2_3 = 256, num_fil_r3_1 = 24, num_fil_r3_5 = 64, num_fil_r4_1 = 64),
            Bloque_Inception(num_fil_r1_1 = 112, num_fil_r2_1 = 144, num_fil_r2_3 = 288, num_fil_r3_1 = 32, num_fil_r3_5 = 64, num_fil_r4_1 = 64),
            Bloque_Inception(num_fil_r1_1 = 256, num_fil_r2_1 = 160, num_fil_r2_3 = 320, num_fil_r3_1 = 32, num_fil_r3_5 = 128, num_fil_r4_1 = 128),
            layers.MaxPool2D(pool_size = 3, strides = 2, padding = 'same'),

            Bloque_Inception(num_fil_r1_1 = 256, num_fil_r2_1 = 160, num_fil_r2_3 = 320, num_fil_r3_1 = 32, num_fil_r3_5 = 128, num_fil_r4_1 = 128),
            Bloque_Inception(num_fil_r1_1 = 384, num_fil_r2_1 = 192, num_fil_r2_3 = 384, num_fil_r3_1 = 48, num_fil_r3_5 = 128, num_fil_r4_1 = 128),
            layers.AveragePooling2D(pool_size = 7, strides = 1),

            layers.Flatten(),
            
            layers.Dropout(rate = 0.4),

            layers.Dense(units = 1000, activation = 'relu'),
            layers.BatchNormalization(),

            layers.Dense(units = num_clases, activation = 'sigmoid'),
        ])

class CallBack(tf.keras.callbacks.Callback):
    
    def on_epoch_end(self, epocas, logs = {}):
    
        if(logs.get('val_accuracy') >= 0.99): 
            
            print("\nSe alcanzo un 99% de precision, cancelamos el entrenamiento")
            self.model.stop_training = True

callback = CallBack()

# Para la reducción del learning rate atenderemos a la métrica de la precisión del set de validación
reducir_lr = tf.keras.callbacks.ReduceLROnPlateau(
    monitor = 'val_accuracy', factor = 0.04,
    patience = 8, min_lr = 1e-5, verbose = 1
)

callbacks = [callback, reducir_lr]

# Hiperpámetros
num_clases = 1
lr = 1e-3
tam_batch = 64
num_epocas = 30

modelo = GoogleLeNet(num_clases)
modelo.arquitectura.summary()

train_datagen = ImageDataGenerator(
    rescale = 1./255,
    vertical_flip = True,
    rotation_range = 45,  
    zoom_range = 0.1,  
    width_shift_range = 0.1,  
    height_shift_range = 0.1, 
    horizontal_flip = True, 
    brightness_range = (0.4, 0.75)
)  

valid_datagen = ImageDataGenerator(
    rescale = 1./255
)

train_dir = 'D:/Datasets/dogs-vs-cats/train/'
valid_dir = 'D:/Datasets/dogs-vs-cats/validation/'

train_generator = train_datagen.flow_from_directory(
    train_dir,
    batch_size = tam_batch,
    class_mode = "binary",
    target_size = (224, 224)
)

valid_generator = valid_datagen.flow_from_directory(
    valid_dir,
    batch_size = tam_batch,
    class_mode = "binary",
    target_size = (224, 224)
)

plt.figure(figsize = (10,10))

for i in range(25):

    img, label = train_generator.next()
    plt.subplot(5, 5, i + 1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(img[i], cmap = 'gray')
    
    if label[i] == 0:
        
        plt.xlabel(f"Etiqueta: gato", color = 'white')

    else:

        plt.xlabel(f"Etiqueta: perro", color = 'white')

plt.show()

modelo.arquitectura.compile(
    optimizer = tf.optimizers.Adam(learning_rate = lr),
    loss = losses.BinaryCrossentropy(), 
    metrics = ['accuracy']
)

historia = modelo.arquitectura.fit(
            train_generator,
            steps_per_epoch = train_generator.samples // tam_batch,
            epochs = num_epocas,
            verbose = 1,
            validation_data = valid_generator,
            validation_steps = valid_generator.samples // tam_batch
            )

# Creamos una gráfica para mostrar el accuracy obtenido tanto en el set de entrenamiento como en el de validacion
plt.plot(historia.history['accuracy'])
plt.plot(historia.history['val_accuracy'])
plt.grid(which = 'both', axis = 'both')
plt.title('Precisión del modelo')
plt.ylabel('Precisión')
plt.xlabel('Época')
plt.legend(['Entrenamiento', 'Test'], loc='upper right')
plt.show()

# Creamos una gráfica para mostrar la función de pérdida obtenida tanto en el set de entrenamiento como en el de validacion
plt.plot(historia.history['loss'])
plt.plot(historia.history['val_loss'])
plt.grid(which = 'both', axis = 'both')
plt.title('Pérdida del modelo')
plt.ylabel('Pérdida')
plt.xlabel('Época')
plt.legend(['Entrenamiento', 'Test'], loc='upper right')
plt.show()

# El primer valor obtenido corresponde con la pérdida, el segundo con el accuracy
modelo.arquitectura.evaluate(valid_generator)

foto = 'C:/Users/Daniel/Desktop/adios.jpg'

image = image_utils.load_img(foto, target_size=(224,224))
plt.imshow(image)

image = image_utils.img_to_array(image)
image = image.reshape(1, 224, 224, 3)
image = image / 255.

prediction = modelo.arquitectura.predict(image)
print(prediction)
```
