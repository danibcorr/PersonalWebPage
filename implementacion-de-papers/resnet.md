---
description: Realizado por Daniel Bazo Correa.
---

# ResNet

## 1. Conceptos previos

<figure><img src="../.gitbook/assets/8CB782A8-0612-4DCA-8BFA-5D3C6110CA8F.jpeg" alt=""><figcaption></figcaption></figure>

## 2. Código

```python
import tensorflow as tf
from tensorflow.keras import layers, losses, optimizers
import numpy as np

# Downsampling CNN con stride de 2
# Fin de la capa es Global Average Pooling con 1000 neuronas y softmax
class Bloque_Residual_Doble(layers.Layer):

    def __init__(self, num_filtros, stride, downsampling):

        super().__init__()

        self.bloque_rama1 = models.Sequential([
            layers.Conv2D(filters = num_filtros, kernel_size = 3, strides = stride, padding = 'same'),
            layers.BatchNormalization(),
            layers.ReLU(),
            
            layers.Conv2D(filters = num_filtros, kernel_size = 3, strides = 1, padding = 'same'),
            layers.BatchNormalization()
        ])

        self.downsampling = downsampling
        self.num_filtros = num_filtros
        self.stride = stride

    def call(self, input_tensor):

        if self.downsampling == True:

            input_conexion_rama2 = layers.Conv2D(filters = self.num_filtros, kernel_size = 1, strides = self.stride, padding = 'same')(input_tensor)
            salida_conexion_rama2 = layers.BatchNormalization()(input_conexion_rama2)

        else:

            salida_conexion_rama2 = input_tensor

        salida_conexion_rama1 = self.bloque_rama1(input_tensor)

        concatenacion = layers.Add()([salida_conexion_rama1, salida_conexion_rama2])    

        return layers.ReLU()(concatenacion)

class Bloque_Residual_Triple(layers.Layer):

    def __init__(self, num_filtros, incremento, stride, downsampling):

        super().__init__()

        self.bloque_rama1 = models.Sequential([
            layers.Conv2D(filters = num_filtros, kernel_size = 1, strides = stride, padding = 'same'),
            layers.BatchNormalization(),
            layers.ReLU(),
            
            layers.Conv2D(filters = num_filtros, kernel_size = 3, strides = 1, padding = 'same'),
            layers.BatchNormalization(),
            layers.ReLU(),
            
            layers.Conv2D(filters = num_filtros * incremento, kernel_size = 1, strides = 1, padding = 'same'),
            layers.BatchNormalization()
        ])

        #self.downsampling = downsampling
        self.num_filtros = num_filtros
        self.incremento = incremento
        self.stride = stride

    def call(self, input_tensor):

        input_conexion_rama2 = layers.Conv2D(filters = self.num_filtros * self.incremento, kernel_size = 1, strides = self.stride, padding = 'same')(input_tensor)
        salida_conexion_rama2 = layers.BatchNormalization()(input_conexion_rama2)

        salida_conexion_rama1 = self.bloque_rama1(input_tensor)

        concatenacion = layers.Add()([salida_conexion_rama1, salida_conexion_rama2])    

        return layers.ReLU()(concatenacion)

class ResNet(tf.keras.Model):

    def __init__(self, configuracion, incremento, num_clases):

        super().__init__()
        
        self.arquitectura = models.Sequential([
            layers.Conv2D(input_shape = (224, 224, 3), filters = 64, kernel_size = 7, strides = 2, padding = 'same'),
            layers.BatchNormalization(),
            layers.ReLU(),

            layers.MaxPool2D(pool_size = 3, strides = 2, padding = 'same')
        ])

        if configuracion[0] == 18 or configuracion[0] == 34:

            for i in range(configuracion[1]):

                self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 64, stride = 1, downsampling = False))

            for i in range(configuracion[2]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 128, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 128, stride = 1, downsampling = False))

            for i in range(configuracion[3]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 256, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 256, stride = 1, downsampling = False))

            for i in range(configuracion[4]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 512, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Doble(num_filtros = 512, stride = 1, downsampling = False))

        if configuracion[0] == 50 or configuracion[0] == 101 or configuracion[0] == 152:

            for i in range(configuracion[1]):

                self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 64, incremento = incremento, stride = 1, downsampling = False))

            for i in range(configuracion[2]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 128, incremento = incremento, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 128, incremento = incremento, stride = 1, downsampling = False))

            for i in range(configuracion[3]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 256, incremento = incremento, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 256, incremento = incremento, stride = 1, downsampling = False))

            for i in range(configuracion[4]):

                if i == 0:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 512, incremento = incremento, stride = 2, downsampling = True))

                else:

                    self.arquitectura.add(Bloque_Residual_Triple(num_filtros = 512, incremento = incremento, stride = 1, downsampling = False))

        self.arquitectura.add(layers.GlobalAveragePooling2D())
        
        self.arquitectura.add(layers.Flatten())

        self.arquitectura.add(layers.Dense(units = 1000))

        self.arquitectura.add(layers.Dense(units = num_clases, activation = 'softmax'))

modelo = 'resnet152'

x = tf.random.normal(shape = (2, 224, 224, 3))
x = tf.convert_to_tensor(x)

if modelo == 'resnet18':    modelo1 = ResNet(configuracion = [18, 2, 2, 2, 2], incremento = 1, num_clases = 1000)
if modelo == 'resnet34':    modelo1 = ResNet(configuracion = [34, 3, 4, 6, 3], incremento = 1, num_clases = 1000)
if modelo == 'resnet50':    modelo1 = ResNet(configuracion = [50, 3, 4, 6, 3], incremento = 4, num_clases = 1000)
if modelo == 'resnet101':    modelo1 = ResNet(configuracion = [101, 3, 4, 23, 3], incremento = 4, num_clases = 1000)
if modelo == 'resnet152':    modelo1 = ResNet(configuracion = [152, 3, 8, 36, 3], incremento = 4, num_clases = 1000)

modelo1.arquitectura.summary()
```

