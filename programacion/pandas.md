---
description: Realizado por Daniel Bazo Correa.
---

# Pandas

## Bibliografía

* [https://pandas.pydata.org/docs/](https://pandas.pydata.org/docs/)

## Capítulo 1: Utilidades con Pandas

A continuación se mostrarán algunas utilidades con Pandas.

### 1.1. Leer un fichero

Si utilizamos `pd.read_` podemos ver todas las opciones de lectura de ficheros que ofrece Pandas, entre los más comunes se encuentran los CSV y parquet.

```python
import pandas as pd

df = pd.read_csv("fichero")

# Podemos mostrar las primeras 5 filas
display(df[:5])
```

### 1.2. Optimizar DataFrame con CUDA (cuDF)

Pandas no procesa en GPU ni permite la paralelización. Por lo que, podemos utilizar cuDF para acelerar ciertos procesos de Pandas. Mucha de la sintaxis se comparte aunque hay funciones específicas de cada librería.

```python
import cudf as df
```

### 1.3. Búsquedas por índice

```python
import pandas as pd

df.iloc[indices]
```

### 1.4. Obtener una parte que cumple con una condición

```python
import pandas as pd

# Suponiendo que tenemos un DataFrame de Pandas y nos queremos quedar
# con aquella filas que tengan la etiqueta 'A' en la columna 'etiqueta'
# haríamos lo siguiente
df[df['etiqueta'] == 'A']
```
