---
description: Realizado por Daniel Bazo Correa.
---

# Pandas

## Bibliografía

* [https://pandas.pydata.org/docs/](https://pandas.pydata.org/docs/)

## Capítulo 0: Útiles

### 0.1. Leer un fichero CSV

```python
import pandas as pd

df = pd.read_csv("fichero")

# Podemos mostrar las primeras 5 filas
display(df[:5])
```

### 0.2. Optimizar DataFrame con CUDA (cuDF)

Pandas no procesa en GPU ni permite la paralelización. Por lo que, podemos utilizar cuDF para acelerar ciertos procesos de Pandas. Mucha de la sintaxis se comparte aunque hay funciones específicas de cada librería.

```python
import cudf as df
```
