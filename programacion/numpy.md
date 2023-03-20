---
description: Realizado por Daniel Bazo Correa.
---

# NumPy

## Capítulo 1: Utilidades con NumPy

A continuación se mostrarán algunas utilidades con NumPy.

### 1.1. Aplicar condiciones

```python
import numpy as np

# Generamos una matriz de 4 x 4 con valores aleatorios
matriz = np.random.rand(4, 4)
# Establecemos un umbral
umbral = 0.5

# Aplicamos la lógica que necesitas
condicion = matriz > umbral
# Donde se cumpla la condicion se coge dicho valor y se le resta el umbral
# En caso contrario se coloca un 0
matriz = np.where(condicion, (matriz - umbral), 0)
```
