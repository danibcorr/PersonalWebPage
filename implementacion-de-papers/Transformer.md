# Transformer

```python
import tensorflow as tf
from tensorflow.keras import layers, losses, optimizers
import numpy as np
import math

def mask_fill_inf(matrix, mask):
    
    negmask = 1 - mask
    num = 3.4 * math.pow(10, 38)
    return (matrix * mask) + (-((negmask * num + num) - num))

class Scaled_Dot_Product_Attention(layers.Layer):

    def __init__(self):

        super().__init__()

    def call(self, Q, K, V, d_k, mask = None):

        # Producto punto entre Queries y Keys
        out_matmul = tf.matmul(Q, K, transpose_b = True)

        # Escalado
        out_scale = out_matmul / tf.math.sqrt(tf.cast(d_k, tf.float32))

        # Añadimos una condición en caso de que sea el decodificador para añadir la parte del mascarado
        if mask != None:

            mask_fill_inf(out_scale, -1e20)

        # Softmax
        out_softmax = layers.Softmax()(out_scale)

        # Producto punto entre Softmax y Values
        return tf.matmul(out_softmax, V)

class Multi_Head_Attention(layers.Layer):

    def __init__(self, h, dv, dk, d_model):

        super().__init__()

        self.attention = Scaled_Dot_Product_Attention()
        self.h = h
        self.dv = dv
        self.dk = dk
        self.d_model = d_model

        # Linear
        self.Wv = layers.Dense(units = dv)
        self.Wk = layers.Dense(units = dk)
        self.Wq = layers.Dense(units = dk)

        # Salida
        self.Wo = layers.Dense(units = d_model)

    def reshape_tensor(self, x, heads, flag):
    
        if flag == True:

            # Forma del tensor tras la remodelación y la transposición: (batch_size, heads, seq_length, -1)
            x = tf.reshape(x, shape=(tf.shape(x)[0], tf.shape(x)[1], heads, -1))
            x = tf.transpose(x, perm=(0, 2, 1, 3))
        
        else:
        
            # Revertir las operaciones de remodelación y transposición: (batch_size, seq_length, d_k)
            x = tf.transpose(x, perm=(0, 2, 1, 3))
            x = tf.reshape(x, shape=(tf.shape(x)[0], tf.shape(x)[1], self.d_k))
        
        return x

    def call(self, Q, K, V, mask = None):

        V_reshape = self.reshape_tensor(self.Wv(V), self.h, True) 
        K_reshape = self.reshape_tensor(self.Wk(K), self.h, True)
        Q_reshape = self.reshape_tensor(self.Wq(Q), self.h, True)
 
        Output = self.attention(Q = Q_reshape, K = K_reshape, V = V_reshape, d_k = self.dk, mask = False)

        return self.Wo(Output)

# Hiperparámetros
# Numero de cabezas de self-attention
h = 8  
# Dimension de los vectores Q y K
d_k = 64  
# Dimension del vector V
d_v = 64  
# Dimension de la capa de salida
d_model = 512  
batch_size = 64 

# Longitud maximo de la secuencia de entrada
input_seq_length = 5  
 
queries = np.random.random((batch_size, input_seq_length, d_k))
keys = np.random.random((batch_size, input_seq_length, d_k))
values = np.random.random((batch_size, input_seq_length, d_v))

multihead_attention = Multi_Head_Attention(h = h, dv = d_v, dk = d_k, d_model = d_model)
print(multihead_attention(queries, keys, values))
```