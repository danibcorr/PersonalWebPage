---
description: Realizado por Daniel Bazo Correa.
---

# Bibliografía

* [YouTube Cesar Ramos](https://www.youtube.com/@cesarramos2592)
# 1. Notación Big O

La notación Big O ofrece una evaluación de la eficiencia de los algoritmos en términos de complejidad temporal y espacial. La complejidad temporal se refiere a la variación del tiempo requerido para un proceso en función del número de elementos de entrada. En contraste, la complejidad espacial se relaciona con el número de variables empleadas en las operaciones del algoritmo.

A continuación, se presentan ejemplos de notaciones Big O:

+ **O(logN)**: Esta notación indica que el tiempo de ejecución crece logarítmicamente en relación con el tamaño de la entrada. Es típico de los algoritmos que dividen a la mitad el problema en cada paso, como la búsqueda binaria.

+ **O(NlogN)**: Esta notación es típica de los algoritmos que involucran una combinación de comportamiento lineal y logarítmico. Un ejemplo común de un algoritmo con esta complejidad es el algoritmo de ordenación rápida o *quicksort*.

+ **O(N)**: Esta notación indica que el tiempo de ejecución crece de manera lineal con el número de elementos de la estructura. Es típico de los algoritmos que realizan una única operación simple en cada elemento de la entrada, como un algoritmo que suma todos los elementos de una lista.

+ **O(N^2)**: Esta notación indica que el tiempo de ejecución crece cuadráticamente con el tamaño de la entrada. Es típico de los algoritmos que realizan una operación simple en cada par de elementos de la entrada, como un algoritmo de ordenación por burbuja.

+ **O(2^N)**: Esta notación indica que el tiempo de ejecución crece exponencialmente con el tamaño de la entrada. Es típico de los algoritmos que resuelven problemas mediante la generación de todas las posibles combinaciones de sus elementos, como el "problema del viajante".

+ **O(1)**: Como ya se mencionó, esta notación indica que el tiempo de ejecución es constante, independientemente del tamaño de la entrada. Es típico de los algoritmos que acceden a un número fijo de elementos de la entrada, sin importar su tamaño, como un algoritmo que devuelve el primer elemento de una lista.

En situaciones donde se realizan múltiples operaciones con diferentes costes temporales, generalmente se selecciona el peor caso.

Existen también casos como los algoritmos multipartes. Por ejemplo:

```python
def funcion():

    for i in arrayA:

        ...

    for i in arrayB:

        ...
```

En el ejemplo anterior, cada bucle tendría una complejidad de $$O(N)$$, pero al tratarse de arrays diferentes, la complejidad total de la función es $$O(A + B)$$, siendo A y B la cantidad de elementos de los arrays A y B respectivamente.

```python
def funcion():

    for i in arrayA:

        for j in arrayB:

            ...
```

En este último ejemplo, se podría pensar que la complejidad sería $$O(N^2)$$, pero al igual que en el caso anterior, al tratarse de arrays diferentes, la complejidad total es $$O(A \cdot B)$$.

Es importante destacar que en la notación Big O no es necesario utilizar la letra N, se puede expresar con cualquier otra letra dependiendo del contexto.

# 2. Métodos de ordenación

En este capítulo, vamos a explorar algunos de los métodos de ordenación más comunes en el campo de las estructuras de datos y algoritmos. 

## 2.1. Ordenación de burbuja (*Bubble Sort*)

El método de ordenación de burbuja es uno de los algoritmos de ordenación más simples. Funciona comparando pares adyacentes de elementos en la lista y los intercambia si están en el orden incorrecto. Este proceso se repite hasta que no se requieren más intercambios, lo que indica que la lista está ordenada.

En términos de eficiencia, la ordenación de burbuja tiene una complejidad de tiempo de $$O(n^2)$$ en el peor de los casos, donde $$n$$ es el número de elementos en la lista. Esto se debe a que cada elemento de la lista puede ser comparado con todos los demás elementos. En términos de espacio, la ordenación de burbuja es $$O(1)$$, ya que solo requiere un pequeño número de variables temporales, independientemente del tamaño de la lista.

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

## 2.2. Ordenación por selección (*Selection Sort*)

La ordenación por selección funciona seleccionando el elemento más pequeño de la lista y colocándolo al principio. Este proceso se repite para el resto de la lista, hasta que toda la lista está ordenada.

La ordenación por selección tiene una complejidad de tiempo de $$O(n^2)$$ en el peor de los casos, similar a la ordenación de burbuja. Esto se debe a que, para cada elemento de la lista, el algoritmo busca el mínimo en el resto de la lista. La complejidad de espacio es también $$O(1)$$, ya que solo se requiere un espacio constante adicional.

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

## 2.3. Ordenación por inserción (*Insertion Sort*)

La ordenación por inserción es un algoritmo de ordenación que funciona de manera similar a cómo las personas ordenan las cartas en sus manos en un juego de cartas. La lista se divide en una parte ordenada y otra desordenada. Se toma un elemento de la parte desordenada y se inserta en la posición correcta en la parte ordenada. Este proceso se repite hasta que no quedan elementos en la parte desordenada.

La ordenación por inserción tiene una complejidad de tiempo de $$O(n^2)$$ en el peor de los casos, ya que cada elemento puede ser comparado con todos los otros elementos antes de él. Sin embargo, en el mejor de los casos, cuando la lista ya está ordenada, la ordenación por inserción puede ser $$O(n)$$. La complejidad de espacio es $$O(1)$$, ya que solo se requiere un espacio constante adicional.

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

# 3. Métodos de búsqueda

En este capítulo, vamos a explorar algunos de los métodos de búsqueda más comunes en el campo de las estructuras de datos y algoritmos. 

## 3.1. Búsqueda lineal (*Linear Search*)

La búsqueda lineal es el método de búsqueda más simple. Funciona recorriendo cada elemento de la lista uno por uno hasta que encuentra el elemento buscado o hasta que ha recorrido todos los elementos.

En términos de eficiencia, la búsqueda lineal tiene una complejidad de tiempo de $$O(n)$$ en el peor de los casos, donde $$n$$ es el número de elementos en la lista. Esto se debe a que, en el peor de los casos, el algoritmo puede tener que recorrer todos los elementos de la lista. La complejidad de espacio es $$O(1)$$, ya que solo se requiere un espacio constante adicional.

Una posible implementación en Python sería:

```python
def busqueda_lineal(lista: list[int], valor_buscar: int) -> int:

    for idx, valor in enumerate(lista):

        if valor_buscar == valor:

            return idx

    return None
```

## 3.2. Búsqueda binaria (*Binary Search*)

La búsqueda binaria es un método de búsqueda eficiente que funciona dividiendo repetidamente a la mitad la parte de la lista que podría contener el elemento buscado, hasta reducir las ubicaciones posibles a solo una.

Para utilizar la búsqueda binaria, la lista debe estar ordenada. La búsqueda binaria tiene una complejidad de tiempo de $$O(\log n)$$ en el peor de los casos, ya que con cada comparación, el algoritmo reduce a la mitad el número de elementos que necesita examinar. La complejidad de espacio es $$O(1)$$, ya que solo se requiere un espacio constante adicional.

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

# 4. Estructuras de datos

## 4.1. Pilas

Una pila es una estructura de datos que organiza los elementos de manera secuencial. El acceso a sus elementos sigue el principio LIFO (Last In, First Out), lo que significa que el último elemento añadido a la pila es el primero en ser retirado. Las operaciones fundamentales en una pila son: apilar (push), que añade un elemento a la pila, y desapilar (pop), que retira el último elemento añadido. Las pilas pueden ser de tamaño estático o dinámico.

A continuación, se presenta una implementación de una pila en Python:

```python
class Pila:

    def __init__(self, tam: int = None):

        self.lista = []
        self.tope = 0
        self.tam = tam
        self.dinamico = False if self.tam is not None else True

    def empty(self):

        return len(self.lista) == 0

    def push(self, elem: int):

        if self.dinamico or self.tope < self.tam:

            self.lista.append(elem)
            self.tope += 1

            if self.dinamico:

                self.tam = self.tope
        else:

            raise Exception("Error, pila llena.")

    def pop(self):

        if not self.empty():

            self.tope -= 1
            return self.lista.pop()

        else:

            raise Exception("Error, pila vacía.")

    def show(self):

        print(self.lista)

    def top(self):

        if not self.empty():

            return self.lista[self.tope - 1]

        else:

            raise Exception("Error, pila vacía.")

    def size(self):

        return len(self.lista)
```

## 4.2. Colas

Una cola es una estructura de datos que organiza los elementos de manera secuencial. La operación de inserción (push) se realiza por un extremo y la operación de extracción (pop) por el otro. Esta estructura sigue el principio FIFO (First In, First Out).

A continuación, se presenta una implementación de una cola en Python:

```python
class Cola():

    def __init__(self, tam: int = None):

        self.lista = []
        self.tope = 0
        self.tam = tam
        self.dinamico = False if self.tam is not None else True

    def size(self):

        return len(self.lista)

    def empty(self):

        return self.size() == 0

    def insertar(self, elem: int):

        if self.dinamico or self.tope < self.tam:

            self.lista.append(elem)
            self.tope += 1

            if self.dinamico:

                self.tam = self.tope
        else:

            raise Exception("Error, cola llena.")

    def eliminar(self):
        
        if not self.empty():

            self.lista.pop(0)
            self.tope -= 1

        else:

            raise Exception("Error, cola vacía.")

    def buscar(self, elem: int):

        if not self.empty():

            for idx, value in enumerate(self.lista):

                if elem == value:

                    return idx

            raise Exception("Error, valor no encontrado.")

        else:

            raise Exception("Error, cola vacía.")

    def top(self):

        if not self.empty():

            return self.lista[0]

        else:

            raise Exception("Error, cola vacía.")

    def show(self):

        print(self.lista)
```

## 4.3. Nodos

En el ámbito de la programación y, concretamente, en las estructuras de datos, un nodo es un elemento fundamental de una lista enlazada, un árbol o un grafo. Cada nodo es una estructura o registro que dispone de varios campos. Al menos uno de estos campos es un puntero o referencia a otro nodo. De esta manera, una vez conocido un nodo, a partir de esa referencia, es posible acceder a otros nodos de la estructura.

## 4.4. Listas enlazadas

Las listas enlazadas son estructuras de datos similares a los arrays o listas en Python, con la diferencia de que el acceso a un elemento se realiza mediante un puntero. Una lista enlazada simple cuenta con un enlace por nodo. Este enlace apunta al siguiente nodo en la lista o al valor `None` si es el último nodo.

A continuación, se presenta una implementación de una lista enlazada en Python:

```python
class Nodo():

    def __init__(self, dato: int):

        self.dato = dato
        self.ptr = None

class ListaEnlazada():

    def __init__(self):

        self.nodo_inicial = None
        self.nodo_final = None

    def vacia(self) -> bool:

        return self.nodo_inicial is None

    def insertar_final(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            self.nodo_final.ptr = nuevo_nodo
            self.nodo_final = nuevo_nodo

    def insertar_principio(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            nuevo_nodo.ptr = self.nodo_inicial
            self.nodo_inicial = nuevo_nodo

    def recorrido(self):

        puntero = self.nodo_inicial

        while puntero is not None:

            print(puntero.dato)
            puntero = puntero.ptr

    def eliminar_ultimo(self):

        if not self.vacia():

            if self.nodo_inicial.ptr is None:

                self.nodo_inicial = self.nodo_final = None

            else:

                anterior = self.nodo_inicial
                actual = anterior.ptr

                while actual.ptr is not None:

                    anterior = actual
                    actual = actual.ptr

                del actual
                anterior.ptr = None
                self.nodo_final = anterior

    def eliminar_primero(self):

        if not self.vacia():

            if self.nodo_inicial.ptr is None:

                self.nodo_inicial = self.nodo_final = None

            else:

                nuevo_nodo_inicial = self.nodo_inicial.ptr
                del self.nodo_inicial
                self.nodo_inicial = nuevo_nodo_inicial
```

## 4.5. Listas doblemente enlazadas

Una lista doblemente enlazada es una estructura de datos que consta de una secuencia de nodos. Cada nodo tiene dos campos de enlace: uno apunta al nodo siguiente y el otro al nodo anterior. Esta estructura permite recorrer la lista en ambos sentidos, desde el inicio hasta el final y viceversa. Además, facilita la eliminación de elementos y es dinámica.

A continuación, se presenta una implementación de una lista doblemente enlazada en Python:

```python
class Nodo():

    def __init__(self, dato: int):

        self.dato = dato
        self.ptr_sig = None
        self.ptr_ant = None

class ListaDobleEnlazada:

    def __init__(self):

        self.nodo_inicial = None
        self.nodo_final = None

    def vacia(self):

        return self.nodo_inicial is None

    def insertar_final(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            self.nodo_final.ptr_sig = nuevo_nodo
            nuevo_nodo.ptr_ant = self.nodo_final
            self.nodo_final = nuevo_nodo

    def insertar_principio(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            self.nodo_inicial.ptr_ant = nuevo_nodo
            nuevo_nodo.ptr_sig = self.nodo_inicial
            self.nodo_inicial = nuevo_nodo

    def recorrido_hacia_adelante(self):

        nodo = self.nodo_inicial

        while nodo is not None:

            print(nodo.dato)
            nodo = nodo.ptr_sig

    def recorrido_hacia_atras(self):

        nodo = self.nodo_final

        while nodo is not None:

            print(nodo.dato)
            nodo = nodo.ptr_ant

    def eliminar_ultimo(self):
        
        if not self.vacia():

            if self.nodo_inicial.ptr is None:

                self.nodo_inicial = self.nodo_final = None
            
            else:
                
                ultimo = self.nodo_final
                penultimo = ultimo.ptr_ant
                penultimo.ptr_sig = None
                del ultimo
                self.nodo_final = penultimo

    def eliminar_primero(self):

        if not self.vacia():

            if self.nodo_inicial.ptr is None:

                self.nodo_inicial = self.nodo_final = None

            else:

                primero = self.nodo_inicial
                segundo = primero.ptr_sig
                segundo.ptr_ant = None
                del primero
                self.nodo_inicial = segundo
```

## 4.6. Lista circular simple

Una lista circular simple es una estructura de datos en la que cada nodo tiene un enlace, similar al de las listas enlazadas simples, con la particularidad de que el enlace del último nodo apunta al primero. En una lista enlazada simple, los nuevos nodos pueden ser insertados eficientemente solo después de un nodo que ya se conoce.

A continuación, se presenta una implementación de una lista circular simple en Python:

```python
class Nodo():

    def __init__(self, dato: int):

        self.dato = dato
        self.ptr = None

class ListaCircular():

    def __init__(self):

        self.nodo_inicial = None
        self.nodo_final = None

    def vacia(self):

        return self.nodo_inicial is None

    def insertar_final(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            self.nodo_final.ptr = nuevo_nodo
            nuevo_nodo.ptr = self.nodo_inicial
            self.nodo_final = nuevo_nodo

    def insertar_principio(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            nuevo_nodo.ptr = self.nodo_inicial
            self.nodo_final.ptr = nuevo_nodo
            self.nodo_inicial = nuevo_nodo

    def recorrido(self):

        nodo = self.nodo_inicial

        while (nodo != None):

            print(nodo.dato)
            nodo = nodo.ptr

            if nodo == self.nodo_inicial:

                break

    def eliminar_ultimo(self):

        if self.vacia():

            if self.nodo_inicial == self.nodo_final:

                self.nodo_inicial = self.nodo_final = None

            else:

                ant = self.nodo_inicial
                act = ant.ptr

                while (act.ptr != self.nodo_inicial):

                    ant = act
                    act = act.ptr

                del act
                ant.ptr = self.nodo_inicial
                self.nodo_final = ant

    def eliminar_primero(self):
        
        if self.vacia():

            if self.nodo_inicial == self.nodo_final:

                self.nodo_inicial = self.nodo_final = None

            else:

                siguiente_nodo = self.nodo_inicial.ptr
                self.nodo_final.ptr = siguiente_nodo
                del self.nodo_inicial
                self.nodo_inicial = siguiente_nodo
```

## 4.7. Lista circular doble

Una lista circular doble es una estructura de datos en la que cada nodo tiene dos enlaces, uno al nodo siguiente y otro al nodo anterior, similar a las listas doblemente enlazadas. La particularidad de esta estructura es que el enlace del último nodo apunta al primero y el enlace del primer nodo apunta al último, formando una estructura circular.

A continuación, se presenta una implementación de una lista circular doble en Python:

```python
class Nodo():

    def __init__(self, dato: int):

        self.dato = dato
        self.ptr_siguiente = None
        self.ptr_anterior = None
        
class ListaDobleCircular():

    def __init__(self):

        self.nodo_inicial = None
        self.nodo_final = None

    def vacia(self):

        return self.nodo_inicial == self.nodo_final == None

    def insertar_final(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            self.nodo_final.ptr_siguiente = nuevo_nodo

            nuevo_nodo.ptr_anterior = self.nodo_final
            nuevo_nodo.ptr_siguiente = self.nodo_inicial

            self.nodo_inicial.ptr_anterior = nuevo_nodo

            self.nodo_final = nuevo_nodo

    def insertar_principio(self, dato: int):

        nuevo_nodo = Nodo(dato)

        if self.vacia():

            self.nodo_inicial = self.nodo_final = nuevo_nodo

        else:

            nuevo_nodo.ptr_siguiente = self.nodo_inicial
            nuevo_nodo.ptr_anterior = self.nodo_final

            self.nodo_inicial.ptr_anterior = nuevo_nodo

            self.nodo_final.ptr_siguiente = nuevo_nodo

            self.nodo_inicial = nuevo_nodo

    def recorrido_hacia_adelante(self):

        nodo = self.nodo_inicial

        while (nodo != None):

            print(nodo.dato)
            nodo = nodo.ptr_siguiente

            if nodo == self.nodo_inicial:

                break

    def recorrido_hacia_atras(self):

        nodo = self.nodo_final

        while (nodo != None):

            print(nodo.dato)
            nodo = nodo.ptr_anterior

            if nodo == self.nodo_final:

                break

    def eliminar_ultimo(self):

        if self.vacia():

            if self.nodo_inicial == self.nodo_final:

                self.nodo_inicial = self.nodo_final = None

            else:

                ultimo = self.nodo_final
                penultimo = ultimo.ptr_anterior

                penultimo.ptr_siguiente = self.nodo_inicial

                self.nodo_inicial.ptr_anterior = penultimo

                del self.nodo_final

                self.nodo_final = penultimo

    def eliminar_primero(self):
        
        if self.vacia():

            if self.nodo_inicial == self.nodo_final:

                self.nodo_inicial = self.nodo_final = None

            else:

                segundo = self.nodo_inicial.ptr_siguiente

                segundo.ptr_anterior = self.nodo_final

                self.nodo_final.ptr_siguiente = segundo

                del self.nodo_inicial

                self.nodo_inicial = segundo
```

## 4.8. Árboles binarios

Un árbol binario se define como una estructura de datos en la que cada nodo puede tener, como máximo, dos descendientes denominados hijo izquierdo y hijo derecho. Esta estructura es una forma eficaz de organizar y buscar datos.

En términos de características, cada nodo de un árbol binario posee un valor y dos descendientes. El valor del hijo izquierdo de un nodo es siempre inferior al del nodo padre, mientras que el valor del hijo derecho es siempre superior. Cada nodo tiene un único progenitor, a excepción del nodo raíz, que carece de padre.

Un árbol binario puede no contener nodos, es decir, estar vacío. Si un árbol binario contiene nodos, entonces se compone de una raíz y dos árboles binarios disjuntos, denominados subárbol izquierdo y subárbol derecho.

Existen varios tipos de recorridos en los árboles binarios:

+ Recorrido en orden: Se visita primero el hijo izquierdo, luego la raíz y, finalmente, el hijo derecho.
+ Recorrido en preorden: Se visita primero la raíz, luego el hijo izquierdo y, finalmente, el hijo derecho.
+ Recorrido en postorden: Se visita primero el hijo izquierdo, luego el hijo derecho y, finalmente, la raíz. 

A continuación, se presenta una implementación de un árbol binario en Python:

```python
class Nodo():
    
    def __init__(self, valor: int = None, padre: int = None, es_raiz: bool = False, es_izquierdo: bool = False, es_derecho: bool = False):
        
        # Valor del nodo
        self.valor = valor   
        # Nodo hijo izquierdo          
        self.izquierdo = None   
        # Nodo hijo derecho            
        self.derecho = None            
        # Nodo padre     
        self.padre = padre                  
        # Indica si el nodo es la raíz
        self.es_raiz = es_raiz              
        # Indica si el nodo es un hijo derecho
        self.es_derecho = es_derecho        
        # Indica si el nodo es un hijo izquierdo
        self.es_izquierdo = es_izquierdo    

class ArbolBinario():

    def __init__(self):

        # Nodo raíz del árbol
        self.nodo_raiz = None              

    def esta_vacio(self):

        return self.nodo_raiz is None

    def agregar_nodo(self, dato: int):

        if self.esta_vacio():

            self.nodo_raiz = Nodo(valor = dato, es_raiz = True)

        else:

            nodo = self._obtener_sitio(dato)

            if dato <= nodo.valor:

                nodo.izquierdo = Nodo(valor = dato, padre = nodo, es_izquierdo = True)

            else:

                nodo.derecho = Nodo(valor = dato, padre = nodo, es_derecho = True)

    def _obtener_sitio(self, valor):

        nodo = self.nodo_raiz

        while nodo is not None:

            temp = nodo

            if valor <= nodo.valor:

                nodo = nodo.izquierdo

            else:

                nodo = nodo.derecho

        return temp

    # Método para mostrar el árbol en orden (izquierda, raíz, derecha)
    def mostrar_en_orden(self, nodo):

        if nodo:

            self.mostrar_en_orden(nodo.izquierdo)
            print(nodo.valor)
            self.mostrar_en_orden(nodo.derecho)

    # Método para mostrar el árbol en postorden (izquierda, derecha, raíz)
    def mostrar_en_postorden(self, nodo):

        if nodo:

            self.mostrar_en_postorden(nodo.izquierdo)
            self.mostrar_en_postorden(nodo.derecho)
            print(nodo.valor)

    # Método para mostrar el árbol en preorden (raíz, izquierda, derecha)
    def mostrar_en_preorden(self, nodo):

        if nodo:

            print(nodo.valor)
            self.mostrar_en_preorden(nodo.izquierdo)
            self.mostrar_en_preorden(nodo.derecho)

    def buscar(self, nodo, valor):

        if nodo == None:

            return None

        else:

            if valor == nodo.valor:

                return nodo

            elif valor <= nodo.valor:

                return self.buscar(nodo.izquierdo, valor)

            else:

                return self.buscar(nodo.derecho, valor)
```