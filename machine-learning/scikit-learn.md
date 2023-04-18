---
description: Realizado por Daniel Bazo Correa.
---

# Scikit Learn

### Bibliografía

* [scikit-learn: machine learning in Python — scikit-learn 1.1.2 documentation](https://scikit-learn.org/stable/index.html)
* [Intuitive Machine Learning - YouTube](https://www.youtube.com/c/IntuitiveMachineLearning)
* [Yellowbrick: Machine Learning Visualization — Yellowbrick v1.5 documentation (scikit-yb.org)](https://www.scikit-yb.org/en/latest/index.html)

## 1. Obtención de características

### 1.2. Procesado de datos



## 2. Algoritmos de Clustering

La función principal de la agrupación o _clustering_ consiste en reducir la distancia entre los puntos de un grupo y maximizar la distancia entre el resto de grupos, es decir, que los puntos de datos que pertenezcan a un mismo grupo se encuentren lo más cerca posible pero alejados del resto de puntos de datos del resto de grupos. <mark style="background-color:yellow;">**Este problema se vuelve más complejo conforme se aumenta la dimensión del cluster**</mark>, ya que puntos de datos que parecían alejados pueden pasar a estar más cerca.

Por ello, <mark style="background-color:yellow;">**es muy común el uso de procesos para la reducción de la dimensionalidad en los datos que tienen alta dimensionalidad**</mark> ya que al añadir más características a la entrada del _cluster_, los datos se vuelven dispersos y el análisis sufre de la denominada _**curse of dimensionality**_ o _**maldición de dimensionalidad.**_

Algunas de las técnicas de extracción de características son el análisis de componentes principales (_**Principle Component Analysis**_, _**PCA**_) y los _**Autoencoders**_. El _PCA_ garantiza la búsqueda de la mejor transformación lineal que reduzca el número de dimensiones con una pérdida mínima de información. A veces, la información que se pierde se considera ruido (información irrelevante) mientras que los _Autoencoders_ comprimen la información recibida a la entrada para adquirir una representación de esta en su espacio latente.

A continuación, veremos algunos de los algoritmos de clustering más utilizados. Tener en cuenta que los algoritmos de _clustering_ se utilizan en problemas no supervisados, es decir, problemas donde no contamos con etiquetas y queremos obtener agrupaciones de datos con similitudes.

### 2.1. K-means clustering

#### 2.1.1. Anotaciones

K-means es un tipo de algoritmo de clustering no supervisados. Su principal función es intentar dividir el dataset en $$k$$ grupos pre-definidos donde cada dato pertenece a un sólo grupo. Consta de 3 pasos:

**Paso 1**, elegimos de manera aleatoria $$k$$ puntos del set de datos los cuales interpretaremos como el centro de los datos al conjunto.

<figure><img src="../.gitbook/assets/Untitled (2).png" alt=""><figcaption></figcaption></figure>

**Paso 2**, calculamos la distancia de los puntos tomados como centros en el paso 1 con respecto al resto de puntos del set de datos. La distancia, la definimos con la siguiente función:&#x20;

<figure><img src="../.gitbook/assets/Untitled 1 (2).png" alt=""><figcaption></figcaption></figure>

Con la imagen anterior, vemos que $$A$$ tiene una menor distancia $$d_3$$, con respecto al punto $$C_3$$ en comparación al resto de puntos $$C_1$$ y $$C_2$$. Por lo tanto, diremos que el punto $$A$$ pertenece al grupo $$C_3$$ por su cercanía con respecto al resto de los centros. Este proceso se realiza de manera reiterativa para el resto de puntos con el fin de que todos se encuentren agrupados.

<figure><img src="../.gitbook/assets/Untitled 2 (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Untitled 3 (2).png" alt=""><figcaption></figcaption></figure>

**Paso 3**, a continuación, movemos el centro con la intención de obtener el centro real de cada grupo de datos. Para ello, realizamos la media de todos los puntos de cada grupo de manera reiterativa hasta que los centros converjan.

<figure><img src="../.gitbook/assets/Untitled 4 (1).png" alt=""><figcaption></figcaption></figure>

#### 2.1.2. Código

```python
# Importamos NumPy para el tratamiento de datos
import numpy as np

# Importamos make_blobs para generar manchas gaussianas isotrópicas para la
# agrupación.
# Wikipedia: La isotropía es la característica de algunos fenómenos en el espacio
# cuyas propiedades no dependen de la dirección en que son examinadas
from sklearn.datasets import make_blobs

# Importamos el modelo KMeans de Scikit Learn
from sklearn.cluster import KMeans

# Importamos la librería MatplotLib para realizar gráficos
import matplotlib.pyplot as plt

# make_blobs permite hacer una distribucion gaussiana de datos, donde tenemos que 
# considerar que una desviación típica baja indica que la mayor parte de los datos
# de una muestra tienden a estar agrupados cerca de su media
# mientras que una desviación típica alta indica que los datos tienen una mayor
# dispersión de valores.
# Por lo tanto, si cambiamos el valor del cluster_std a un valor menor, veremos
# que los puntos se irán agrupando más y se encontrarán mejor diferenciados
x, y = make_blobs(
	n_samples = 200, # Numero total de puntos
	n_features = 2, # Número de características, 2 dimensiones
	centers = 3, # 3 grupos
	cluster_std = 0.5, # desviacion típica de cada distribucion gaussiana
	random_state = 0 # estado de aleatoriedad de la preparacion de los datos
)

# 'x' son 200 muestras aleatorias hay 2 columnas, cada columna representa una una 
# característica para esa muestra
x

# 'y' es sólo una lista de etiquetas de grupos para cada muestra
y

# Vamos a visulizar los datos en 2D con la funcion scatter de Matplotlib
# Si tenemos más de 2 dimensiones podemos aplicar técnicas como PCA
# para la reduccion de dimensiones a 2 y verlo en 2D
plt.scatter(
	x[:, 0], x[:, 1],
	c = 'white',
	edgecolors = 'black'
)

# n_cluster = el numero de agrupaciones (clusters) que queremos formar, así
# como el número de centros que queremos generar.
# init = inicialización de los centros.
# n_init = indica el número de veces que el algoritmo de k-means
# se ejecutará con diferentes centros como estado inicial. El resultado final
# será la mejor salida de n_init.
# max_iter = número de iteraciones máximas de k-means para una ejecución.
# tol = Tolerancia relativa con respecto a la norma de Frobenius de la diferencia
# de los centros de los clusters de dos iteraciones consecutivas para declarar 
# la convergencia.
kmeans = KMeans(
	n_clusters = 3, init = 'random',
	n_init = 1, max_iter = 10,
	tol = 1e-04, random_state = 2
)

y_km = kmeans.fit_predict(x)

# Graficamos los 3 grupos
colores = ['lightgreen', 'orange', 'lightblue']
marcas = ['s', 'o', 'v']

for i in range(0, 3):

	plt.scatter(
		x[y_km == i, 0], x[y_km == i, 1],
		s = 50, c = colores[i],
		marker = marcas[i], edgecolor='black',
		label = "cluster " + str(i)
	)

# Graficamos el centro de los grupos
plt.scatter(
	kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1],
	s=250, marker='*',
	c='red', edgecolor='black',
	label='centros'
)

plt.legend(scatterpoints=1)
```

### 2.2. Spectral Clustering

#### 2.2.1. Anotaciones

Permite agrupar data sets muchos más complejos que no son linealmente separables como ocurría en el caso de K-means. La idea de este algoritmo consiste en crear un grafo de pesos o un grafo de afinidad (un grafo similar) donde cada punto de los datos es un nodo del grafo y la relación (edges) entre nodos indica la similitud entre ellos.

Podemos utilizar la función gaussiana para poder expresar el valor de esa relación entre la unión de nodos. Cuando la distancia es próxima obtenemos un 0 que con la exponente se queda en 1, indicando una gran similitud, igual ocurre al contrario.

<figure><img src="../.gitbook/assets/Untitled 5.png" alt=""><figcaption></figcaption></figure>

El resultado es una matriz de pesos o de similitud:

$$
W=\begin{pmatrix} W_{1,1}&... & W_{1,n}\\ .& ... & .\\ .& ...& .\\ .& ...& .\\ W_{n,1}&...& W_{n,n}\\ \end{pmatrix}_{n\cdot n}
$$

Obtenido el grafo de similitud, queremos dividir los nodos en $$k$$ grupos:

<figure><img src="../.gitbook/assets/Untitled 6 (1).png" alt=""><figcaption></figcaption></figure>

#### 2.2.2. Código

```python
import numpy as np
import matplotlib.pyplot as plt

from sklearn.cluster import KMeans, SpectralClustering
from sklearn.datasets import make_blobs

plt.figure(figsize = (6, 5))

n_samples = 1500
random_state = 170

X, y = make_blobs(
    n_samples = n_samples,
    random_state = random_state
)

transformation = [[0.60834549, -0.63667341], [-0.40887718, 0.85253229]]

X_aniso = np.dot(X, transformation)

y_pred = SpectralClustering(
    n_clusters = 3,
    gamma = 5,
    random_state = random_state
).fit_predict(X_aniso)

plt.scatter(X_aniso[:, 0 ], X_aniso[:, 1], c = y_pred, s = 10)
plt.title("Spectral Clustering")
```

### 2.3. DBSCAN Clustering

#### 2.3.1. Anotaciones

#### 2.3.2. Código

### 2.4. K-Medoids

#### 2.4.1. Anotaciones

#### 2.4.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Algoritmos de clustering
from sklearn_extra.cluster import KMedoids

# Metricas de optimizacion
from sklearn.metrics import silhouette_score, calinski_harabasz_score

# Normalización de los datos de entrada
from sklearn import preprocessing

# Buscar el número de clusters utilizando algún algoritmo
algoritmo = KMedoids(
    n_clusters = num_cluster,
    metric = 'euclidean',
    # cambiar por 'pam' para que sea mas preciso pero es mas lento
    method = 'alternate', 
    init = 'k-medoids++',
    max_iter = 300,
    random_state = 0
)

# Complementar con un dataset
```

### 2.5. AHC o HAC (Agglomerative Hierarchical Clustering)

#### 2.5.1. Anotaciones

#### 2.5.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Algoritmos de clustering
from sklearn.cluster import AgglomerativeClustering

# Metricas de optimizacion
from sklearn.metrics import silhouette_score, calinski_harabasz_score

# Normalización de los datos de entrada
from sklearn import preprocessing

# Buscar el número de clusters utilizando algún algoritmo
algoritmo = AgglomerativeClustering(
    n_clusters = num_cluster,
    affinity = 'euclidean',
    linkage = 'ward'
)

# Complementar con un dataset
```

### 2.6. Spectral Clustering

#### 2.6.1. Anotaciones

#### 2.6.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Algoritmos de clustering
from sklearn.cluster import SpectralClustering

# Metricas de optimizacion
from sklearn.metrics import silhouette_score, calinski_harabasz_score

# Normalización de los datos de entrada
from sklearn import preprocessing

algoritmo = SpectralClustering(
    n_clusters = num_cluster,
    gamma = 5,
    random_state = 0
)

# Complementar con un dataset
```

### 2.7. K-Nearest Neighbors (KNN)

#### 2.7.1. Anotaciones

A diferencia del resto de algoritmo vistos hasta este punto, KNN es un algoritmo supervisado utilizado para problemas de clasificación y regresión.

Su funcionamiento se detalla a continuación:

**Primero**, suponemos que queremos clasificar puntos de datos (puntos en azul y rojo en la imagen) en grupos (en la imagen vemos que tenemos 2 clases).

<figure><img src="../.gitbook/assets/Untitled 7 (2).png" alt=""><figcaption></figcaption></figure>

**Segundo**, para encontrar el K-nearest neigbors de un punto determinado, tenemos que calcular la distancia de dicho punto respecto al resto de puntos del set de datos.

<figure><img src="../.gitbook/assets/Untitled 8.png" alt=""><figcaption></figcaption></figure>

Para calcular la distancia, podemos utilizar la función de distancia Euclídea o la Manhattan, aunque la Euclídea es la más usada.

**Tercero**, posteriormente, ordenamos las distancias de los puntos vecinos a un determinado punto con un orden decreciente. Contamos con $$k$$ que indica a cantidad de grupos que tenemos en el set de datos.

Para el caso de la clasificación, el mejor valor de $$k$$ se obtiene utilizando _**cross validation**_ y una curva de aprendizaje.

* Un valor pequeño de $$k$$ indica un sesgo bajo pero una alta varianza → Overfitting.
* Un valor grande de $$k$$ indica un sesgo alto pero baja varianza → Underfitting

Por lo que un buen valor de $$k$$ es un equilibrio entre los 2 valores anteriores.

Para el caso de la regresión, se devuelve la media de las etiquetas de los vecinos:

<figure><img src="../.gitbook/assets/Untitled 9 (1).png" alt=""><figcaption></figcaption></figure>

#### 2.7.2. Código

## 3. Optimización de algoritmos de clustering

Los métodos de optimización de clustering que veremos a continuación, pretenden obtener el valor óptimo de número de clusters pre-definidos necesario en los algoritmos de clustering.

### 3.1. Método del codo (Elbow Method)

#### 3.1.1. Anotaciones

Utiliza como medida el _WCSS, Whitin-Cluster Sum of Squares_. El _**WCSS**_ es una medida de la variabilidad de las observaciones dentro de los clusters que se calcula tomando la suma de las distancias al cuadrado entre cada observación y el centroide de su respectivo cluster. Los valores de _**WCSS**_ de los clusters se promedian para obtener un _**WCSS**_ global para el algoritmo de clustering. Aquí, la mejor solución del número de clusters necesarios se conseguirá con el menor valor posible de _WCSS_ (los valores más bajos de _**WCSS**_ son preferibles ya que indican una agrupación de los datos más compacta) con el menor valor posible del número de clusters. Es decir, se realizará un bucle que empleará algún método de clustering insertando diferentes números de clusters. Posteriormente, calculará el _**WCSS.**_ Finalmente, aquél valor de cluster que obtenga una reducción del **WCSS** significativo con un coste computacional moderado será la mejor opción.

Para obtener el valor del _WCSS_ utilizando Scikit Learn, suponiendo que estamos utilizando K-means, utilizamos:

```python
kmeans.inertia_
```

`inertia_` devuelve la suma de las distancias al cuadrado de las muestras a su centro de cluster más cercano (ponderada por los pesos de la muestra si se proporcionan).

#### 3.1.2. Código

```python
# Supondremos que vamos a utilizar K-Means
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.cluster import KMeans

# Variables que definiran el rango de valores que tomará el número de clusters
inf = 2
sup = 10

wcss = []

for i in range(inf, sup + 1):

		algoritmo = KMeans(
			# Numero de clusters
			n_clusters = i,     
			# Método de inicialización
			init = 'k-means++', 
			max_iter = 300,     
			n_init = 10,        
			random_state = 0
		)

    algoritmo.fit(x)
    
    wcss.append(algoritmo.inertia_)

plt.scatter(range(inf, sup + 1), wcss, c = 'red')
plt.plot(range(inf, sup + 1), wcss)
plt.grid(visible=True)
plt.title('Método del codo')
plt.xlabel('Numero de clusters')
plt.ylabel('WCSS')
plt.show()
```

#### 3.1.3. Ejemplo

<figure><img src="../.gitbook/assets/Untitled 10.png" alt=""><figcaption></figcaption></figure>

Con la imagen anterior, se ha utilizado el dataset de IRIS junto con el código mostrado anteriormente en combinación con K-means, con rangos de valores para el número de clusters de \[2, 10]. Vemos que hasta el número de clusters 3, obtenemos un descenso del valor del _**WCSS**_ considerable pero a partir del 3 la reducción es mínima. Por tanto, el valor óptimo de la imagen anterior sería 3, lugar donde se produce el codo.

### 3.2. Puntuación de la Silueta (Silhouette Score)

#### 3.2.1. Anotaciones

El coeficiente de silueta se emplea para conocer el valor óptimo del número de clusters a utilizar. La puntuación se calcula promediando el coeficiente de silueta de cada muestra, calculado como la diferencia entre la distancia media dentro del propio clúster y la distancia media al clúster más cercano de cada dato, normalizada por el valor máximo. Esto produce una puntuación entre $$[-1, 1]$$, donde 1 corresponde a clusters muy densos (valor ideal) y -1 a una agrupación incorrecta (pero valor posible).

Cada cluster tiene su propia puntuación de silueta. Se trata de un proceso iterativo donde realizamos el cluster con un rango de valores de $$k$$, en el que al finalizar el cluster calculamos la puntuación de silueta para cada posible iteración del cluster con los diferentes valores de $$k$$ hasta obtener un valor $$k$$ promedio más cercano a 1.

#### 3.2.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.cluster import KMeans

# Métricas de optimización
from sklearn.metrics import silhouette_score

# Visualización
from yellowbrick.cluster import SilhouetteVisualizer

# Variables que definiran el rango de valores que tomará el número de clusters
inf = 2
sup = 10

punt_silu = []

for i in range(inf, sup + 1):

    algoritmo = KMeans(
        # Numero de clusters
        n_clusters = i,     
        # Método de inicialización
        init = 'k-means++', 
        max_iter = 300,     
        n_init = 10,        
        random_state = 0
    )
    
    visualizer = SilhouetteVisualizer(algoritmo, colors='yellowbrick')
    visualizer.fit(x)
    visualizer.show()
    punt_silu.append(silhouette_score(x, algoritmo.labels_))

sil = np.argmax(punt_silu) + 2
            
plt.grid(visible=True)
plt.plot(range(inf, sup + 1), punt_silu)
plt.scatter(sil, punt_silu[sil - 2], c = 'red', s = 300)
plt.axvline(x = sil, linestyle = '--', c = 'green', label = 'Punto optimo')
plt.legend(shadow = True)
plt.title('Método de Puntuación de Silueta')
plt.xlabel('Numero de clusters')
plt.ylabel('Puntuación Silueta') 
plt.show()
```

#### 3.2.3. Ejemplo

<figure><img src="../.gitbook/assets/Untitled 11.png" alt=""><figcaption></figcaption></figure>

Con la imagen anterior, podemos observar el grueso de los clusters (barras de colores) y su distribución. Todos parten desde 0, por lo que son agrupaciones correctas densas que sobrepasan la puntuación media de la silueta (línea roja).

### 3.3. Factor o índice CH (Caliński-Harabasz index)

#### 3.3.1. Anotaciones

Utilizamos el factor _CH_ para evaluar el modelo con el fin de ver qué tan bien se ha realizado la agrupación utilizando cantidades y características inherentes al conjunto de datos.

El factor _CH_ es una medida que expresa como de similar es un objeto a su propio grupo (cohesión) en comparación con otros grupos (separación). Aquí la cohesión se estima en función de las distancias desde los puntos de datos en un cluster hasta su centroide y la separación se basa en la distancia de los centroides de clúster del centroide global.

Un valor más alto del índice CH significa que los grupos son densos y están bien separados, aunque no hay un valor de corte "aceptable". Hay que elegir soluciones que tengan un punto abrupto en el gráfico de línea de los índices CH.

Si obtenemos una gráfica suave, no hay razón para preferir una solución sobre otras.

#### 3.3.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.cluster import KMeans

# Métricas de optimización
from sklearn.metrics import silhouette_score

# Visualización
from sklearn.metrics import calinski_harabasz_score

# Variables que definiran el rango de valores que tomará el número de clusters
inf = 2
sup = 10

puntuaciones_CH = []

for i in range(inf, sup + 1):

    algoritmo = funciones_clustering(met_algo, i)
    algoritmo.fit(x)
    
    puntuaciones_CH.append(calinski_harabasz_score(x, algoritmo.labels_))

# Devuelve el índice del valor máximo, por lo que como empezamos por el número de clusters
# 2, tendremos que sumar 2 al índice
ch = np.argmax(puntuaciones_CH) + 2

plt.grid(visible=True)
plt.plot(range(inf, sup + 1), puntuaciones_CH)
plt.scatter(ch, puntuaciones_CH[ch - 2], c = 'red', s = 300)
plt.axvline(x = ch, linestyle = '--', c = 'green', label = 'Punto optimo')
plt.legend(shadow = True)
plt.title('Método de Puntuación CH')
plt.xlabel('Numero de clusters')
plt.ylabel('Índice CH') 
plt.show()
```

#### 3.3.3. Ejemplo

<figure><img src="../.gitbook/assets/Untitled 12 (1).png" alt=""><figcaption></figcaption></figure>

Con la imagen anterior, podemos observar el punto óptimo del número de clusters ha utilizar para el dataset. Para este ejemplo se utilizó el dataset de _IRIS_.

### 3.4. Combinación de optimizaciones

#### 3.4.1. Anotaciones

Sería buena idea combinar los métodos de búsqueda del óptimo valor del número de cluster para tener un rango de valores óptimos. En este caso, combinaremos las gráficas de los métodos del codo, Silhouette Score y factor CH.

#### 3.4.2. Código

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Algoritmos de clustering
from sklearn.cluster import KMeans, AgglomerativeClustering, SpectralClustering
from sklearn_extra.cluster import KMedoids

# Metricas de optimizacion
from sklearn.metrics import silhouette_score, calinski_harabasz_score

# Visualización
from yellowbrick.cluster import SilhouetteVisualizer

# Normalización de los datos de entrada
from sklearn import preprocessing

# Variables que definiran el rango de valores que tomará el número de clusters
inf = 2
sup = 10

wcss = []
puntuaciones_CH = []
punt_silu = []

for i in range(inf, sup + 1):

    algoritmo = funciones_clustering(met_algo, i)
    algoritmo.fit(x)

    punt_silu.append(silhouette_score(x, algoritmo.labels_))
    puntuaciones_CH.append(calinski_harabasz_score(x, algoritmo.labels_))
    wcss.append(algoritmo.inertia_)

# Calcular el valor óptimo de K
#sil = np.argmax(punt_silu) + 2
#ch = np.argmax(puntuaciones_CH) + 2
#mejor_k = (int)((sil + ch) / 2)

# Normalizamos
punt_silu /= np.linalg.norm(punt_silu)
puntuaciones_CH /= np.linalg.norm(puntuaciones_CH)
wcss /= np.linalg.norm(wcss)

plt.grid(visible=True)

plt.plot(range(inf, sup + 1), punt_silu, label = 'Silueta')
plt.plot(range(inf, sup + 1), puntuaciones_CH, label = 'CH')
plt.plot(range(inf, sup + 1), wcss, label = 'Codo')

#plt.axvline(x = mejor_k, linestyle = '--', c = 'green', label = 'Punto optimo')
plt.legend(shadow = True)
plt.title('Combinación de métodos')
plt.xlabel('Numero de clusters')
plt.ylabel('Puntuacion Normalizada') 

plt.legend(loc='upper right')
plt.show()
```

## 4. Reducción dimensionalidad

### 4.1. PCA

### 4.2. Autoencoders
