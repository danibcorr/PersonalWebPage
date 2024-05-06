---
description: Realizado por Daniel Bazo Correa.
---

# Bibliografía

* [YouTube Cesar Ramos](https://www.youtube.com/@cesarramos2592)

# 1. Métodos de ordenación

En este capítulo, vamos a explorar algunos de los métodos de ordenación más comunes en el campo de las estructuras de datos y algoritmos. 

## 1.1. Ordenación de burbuja (*Bubble Sort*)

El método de ordenación de burbuja es uno de los algoritmos de ordenación más simples. Funciona comparando pares adyacentes de elementos en la lista y los intercambia si están en el orden incorrecto. Este proceso se repite hasta que no se requieren más intercambios, lo que indica que la lista está ordenada.

En términos de eficiencia, la ordenación de burbuja tiene una complejidad de tiempo de $O(n^2)$ en el peor de los casos, donde $n$ es el número de elementos en la lista. Esto se debe a que cada elemento de la lista puede ser comparado con todos los demás elementos. En términos de espacio, la ordenación de burbuja es $O(1)$, ya que solo requiere un pequeño número de variables temporales, independientemente del tamaño de la lista.

Una posible implementación en Python sería:

```python
def ordenacion_burbuja(lista: list[int]) -> list[int]:

    for i in range(len(lista)):

        for j in range(len(lista) - 1):

            if (lista[j] > lista[j + 1]):

                temp = lista[j]
                lista[j] = lista[j + 1]
                lista[j + 1] = temp

    return lista
```

## 1.2. Ordenación por selección (*Selection Sort*)

La ordenación por selección funciona seleccionando el elemento más pequeño de la lista y colocándolo al principio. Este proceso se repite para el resto de la lista, hasta que toda la lista está ordenada.

La ordenación por selección tiene una complejidad de tiempo de $O(n^2)$ en el peor de los casos, similar a la ordenación de burbuja. Esto se debe a que, para cada elemento de la lista, el algoritmo busca el mínimo en el resto de la lista. La complejidad de espacio es también $O(1)$, ya que solo se requiere un espacio constante adicional.

Una posible implementación en Python sería:

```python
def ordenacion_seleccion(lista: list[int]) -> list[int]:

    for i in range(len(lista)):

        idx_min_value = i

        for j in range(len(lista)):

            if (lista[idx_min_value] > lista[j]):

                idx_min_value = j

        temp = lista[i]
        lista[i] = lista[idx_min_value]
        lista[idx_min_value] = temp

    return lista
```

## 1.3. Ordenación por inserción (*Insertion Sort*)

La ordenación por inserción es un algoritmo de ordenación que funciona de manera similar a cómo las personas ordenan las cartas en sus manos en un juego de cartas. La lista se divide en una parte ordenada y otra desordenada. Se toma un elemento de la parte desordenada y se inserta en la posición correcta en la parte ordenada. Este proceso se repite hasta que no quedan elementos en la parte desordenada.

La ordenación por inserción tiene una complejidad de tiempo de $O(n^2)$ en el peor de los casos, ya que cada elemento puede ser comparado con todos los otros elementos antes de él. Sin embargo, en el mejor de los casos, cuando la lista ya está ordenada, la ordenación por inserción puede ser $O(n)$. La complejidad de espacio es $O(1)$, ya que solo se requiere un espacio constante adicional.

Una posible implementación en Python sería:

```python
def ordenacion_insercion(lista: list[int]) -> list[int]:

    if (len(lista) > 1):

        for i in range(1, len(lista)):

              j = i

              while j > 0 and lista[j - 1] > lista[j]:

                  temp = lista[j - 1]
                  lista[j - 1] = lista[j]
                  lista[j] = temp

                  j -= 1

    return lista
```

# 2. Métodos de búsqueda

En este capítulo, vamos a explorar algunos de los métodos de búsqueda más comunes en el campo de las estructuras de datos y algoritmos. 

## 2.1. Búsqueda lineal (*Linear Search*)

La búsqueda lineal es el método de búsqueda más simple. Funciona recorriendo cada elemento de la lista uno por uno hasta que encuentra el elemento buscado o hasta que ha recorrido todos los elementos.

En términos de eficiencia, la búsqueda lineal tiene una complejidad de tiempo de $O(n)$ en el peor de los casos, donde $n$ es el número de elementos en la lista. Esto se debe a que, en el peor de los casos, el algoritmo puede tener que recorrer todos los elementos de la lista. La complejidad de espacio es $O(1)$, ya que solo se requiere un espacio constante adicional.

Una posible implementación en Python sería:

```python
def busqueda_lineal(lista: list[int], valor_buscar: int) -> int:

    for idx, valor in enumerate(lista):

        if valor_buscar == valor:

            return idx

    return None
```

## 2.2. Búsqueda binaria (*Binary Search*)

La búsqueda binaria es un método de búsqueda eficiente que funciona dividiendo repetidamente a la mitad la parte de la lista que podría contener el elemento buscado, hasta reducir las ubicaciones posibles a solo una.

Para utilizar la búsqueda binaria, la lista debe estar ordenada. La búsqueda binaria tiene una complejidad de tiempo de $O(\log n)$ en el peor de los casos, ya que con cada comparación, el algoritmo reduce a la mitad el número de elementos que necesita examinar. La complejidad de espacio es $O(1)$, ya que solo se requiere un espacio constante adicional.

Una posible implementación en Python sería:

```python
def busqueda_binaria(lista: list[int], valor_buscar: int) -> int:

    lista = metodo_ordenacion_ascendente(lista)

    izquierda = 0
    derecha = len(lista) - 1

    while (izquierda <= derecha):

        punto_medio = (izquieda + derecha) // 2

        if valor_buscar == lista[punto_medio]:

            return punto_medio

        elif valor_buscar > lista[punto_medio]:

            izquieda = punto_medio + 1

        elif valor_buscar < lista[punto_medio]:

            derecha = punto_medio - 1

    return None
```