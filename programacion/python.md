---
description: Realizado por Daniel Bazo Correa.
---

# Bibliografía

* [Python Docs](https://docs.python.org/3/)
* [Python Bootcamps Udemy](https://www.udemy.com/course/complete-python-bootcamp/)

# 1. Utilidades

## 1.1. Línea de comandos

Los comandos de terminal son herramientas poderosas que pueden variar según el sistema operativo. Aquí se presentan algunos comandos útiles:

| Comando                  | Función                                                                                       |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| `pwd`                    | Muestra el directorio actual                                                                  |
| `ls`                     | Lista todos los archivos y carpetas en el directorio actual                                   |
| `cd "nombre_lugar_a_ir"` | Cambia al directorio especificado                                                             |
| `clear`                  | Limpia el terminal                                                                            |
| `cd ...`                 | Navega al directorio Home del sistema (Carpeta Usuario y Carpeta de acceso compartido)        |
| `cmd + shift + p`        | Abre un cuaderno Jupyter en Visual Studio Code                                                |
| `shift + tab`            | Muestra la documentación de una función, método, etc. dentro de Jupyter                       |

Si estás utilizando Anaconda en Linux, estos comandos pueden ser útiles:

| Comando                                                              | Función                                                                                                                              |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `anaconda-navigator`                                                 | Abre el navegador de Anaconda desde el terminal de Linux                                                                             |
| `cd /home/"usuario"/anaconda3/bin + ./jupyter-notebook --allow-root` | Si el navegador de Anaconda tiene problemas para abrir el cuaderno Jupyter, puedes abrirlo directamente sin usar Anaconda            |

# 2. Objetos y estructura de datos básica

## 2.1. Tipos de datos fundamentales

Python ofrece una variedad de tipos de datos fundamentales que se utilizan para definir y manipular información en el código. Aquí hay una lista de los tipos de datos más comunes:

| Tipo de datos | Palabra reservada | Ejemplos |
| --- | --- | --- |
| Números enteros | `int` | 3, 300, 200 |
| Números con coma flotante | `float` | 2.3, 4.6, 100.0 |
| Cadenas de texto | `str` | "Hola", "Hola muy buenas", "2000" |
| Listas | `list` | [10, "hello", 200.3] |
| Diccionarios | `dict` | { "edad" : "20", "nombre" : "Dani" } |
| Tuplas (secuencia de objetos ordenada e inmutable) | `tup` | (10, "hello", 200.3) |
| Conjuntos (colección de objetos únicos desordenada) | `set` | { "a", "b" } |
| Booleanos (indicador de valor lógico) | `bool` | True o False |

## 2.2. Operaciones con números

Python también proporciona una serie de operadores que se pueden utilizar para realizar operaciones matemáticas en números:

| Operador | Función |
| --- | --- |
| +, -, *, /, % | Suma, resta, producto, división y módulo (devuelve el resto de la división), respectivamente. |
| `numero = -x` | Python permite mostrar números negativos. |
| `abs(numero)` | Valor absoluto del número. |
| `pow(x ,y) = x**y` | $$x^y$$. |
| `max(x, y)` | Devuelve el mayor número de los que se pasan como argumentos. El contrario sería `min(…)`. |
| `round(math.pi, 2)` | Redondea números a un número especificado de decimales. Por ejemplo, redondea el número pi a 2 decimales. |
| `floor(x)` | Redondea las unidades hacia abajo. Necesita `import math`. |
| `ceil(x)` | Redondea las unidades hacia arriba. Necesita `import math`. |
| `math.sqrt(x)` | Devuelve la raíz cuadrada de un número. Necesita `import math`. |
| `math.pi` | Valor numérico de Pi. Necesita `import math`. |
| `hex(512)` | Convierte números a hexadecimal. |
| `bin(1234)` | Convierte números a binario. |

## 2.3. Asignación de variables

Cuando creamos variables en Python, debemos seguir ciertas reglas:

* Los nombres de las variables no pueden comenzar con números.
* No puede haber espacios en el nombre de la variable.
* No se pueden usar los siguientes símbolos: `: ''' <> / , ? | \ ( ) ! @ # $ % ^ & * ~ - +`

Es considerado una buena práctica utilizar nombres de variables en minúsculas.

Python utiliza la tipificación dinámica, lo que significa que no es necesario indicar el tipo de dato (int, double, ...) ya que Python interpretará el tipo de dato en función del valor que se le asigne. Por ejemplo, podríamos crear una variable que contenga un tipo de dato y luego en el código asignarle otro tipo de datos:

```python
mis_perros = 2
mis_perros = [ "Pixel" , "One" ]
```

Al escribir `type(variable)` en Python, nos muestra el tipo (int, string, bool...) de la variable.

## 2.4. Imprimir en pantalla

La función utilizada para imprimir en pantalla es `print()`:

```python
print("Esto es una prueba")
```

Podemos concatenar variables que contienen cadenas de texto o métodos/funciones que devuelvan un valor utilizando el operador `+`, por ejemplo:

```python
char_name = "Daniel"
char_age = 19

print("Yo me llamo " + char_name + " y tengo " + str(char_age) + " años.")
```

El procedimiento anterior puede no ser muy eficiente. Por ello, Python permite dar formato a la función `print()` utilizando la letra `f` después del primer paréntesis de la función `print()`. Así, mediante llaves `{}` podemos colocar las funciones, variables o cualquier elemento que queremos mostrar en pantalla. Esto es válido a partir de la versión de Python 3. Aplicando este formato al ejemplo anterior, el resultado sería el siguiente:

```python
char_name = "Daniel"
char_age = 19

print(f"Yo me llamo {char_name} y tengo {char_age} años")
```

## 2.5. Cadenas de texto (String)

Definimos a un string como una cadena de caracteres, por ejemplo:

```python
frase = "Hola buenas"

# Muestra el caracter 'H'
print("El primer caracter de mi string es " + frase[0])

mis_animales=["Misifu" , "One"]
print(f"Mi conejo se llama {mis_animales[0]} y mi gato {mis_animales[1]}")
```

Al igual que las listas, el índice de una variable de tipo string comienza en 0, pero a diferencia de las listas, los strings son inmutables, lo que significa que no podemos utilizar el indexado para modificar un elemento individual del string.

### 2.5.1. Funciones de las cadenas de texto (String)
Las variables de tipo string en Python tienen una serie de funciones incorporadas que permiten manipular y analizar el contenido de la cadena. Aquí hay algunas de las funciones más comunes:

| Función                                            | Definición                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `str(variable_a_convertir_en_string)`              | Permite transformar una variable en string.                                                                                                                                                                                                                                                                                                                                                         |
| `variable *= x`                                    | Devuelve la variable string copiandola ‘x’ veces, siendo ‘x’ un número entero.                                                                                                                                                                                                                                                                                                                      |
| `variable[índice:]`                                | Permite quedarte con una parte del string desde el índice hasta el final del string.                                                                                                                                                                                                                                                                                                                |
| `variable[::X]`                                    | Permite coger todo el string pero con un tamaño de paso (step size) de 2, es decir, voy cogiendo caracteres de X en X, siendo X un número entero.                                                                                                                                                                                                                                                   |
| `variable[::-1]`                                   | Permite invertir un string.                                                                                                                                                                                                                                                                                                                                                                         |
| `variable.lower()`                                 | Convierte el string entero en minúsculas.                                                                                                                                                                                                                                                                                                                                                           |
| `variable.upper()`                                 | Convierte el string entero en mayúsculas.                                                                                                                                                                                                                                                                                                                                                           |
| `variable.isupper()`                               | Devuelve True si todo el string está en mayúsculas y devuelve False en caso contrario.                                                                                                                                                                                                                                                                                                              |
| `variable.upper().isupper()`                       | Convierte el string a mayúsculas y devuelve True si todo el string está en mayúsculas.                                                                                                                                                                                                                                                                                                              |
| `variable.split()`                                 | Permite crear una lista con el string, donde cada elemento de la lista es cada palabra separada del espacio. Si ponemos por ejemplo `variable.split('i')` permite crear la lista quitando de todas las palabras la letra i. Esto se llama "tokenización", la cadena se separa en sub-cadenas basadas en patrones. La tokenización es una actividad central en el NLP (Natural Language Processing). |
| `len(variable)`                                    | Devuelve el número de caracteres del string ( tamaño del string ).                                                                                                                                                                                                                                                                                                                                  |
| `variable.index("a")` o `variable.index("buenas")` | Devuelve el primer índice del string donde se encuentra el parámetro que se le pasa.                                                                                                                                                                                                                                                                                                                |
| `variable.replace("buenas", "me llamo Daniel")`    | Por ejemplo, si mi string es "Hola buenas", reemplaza el "buenas" de mi string, por "me llamo Daniel".                                                                                                                                                                                                                                                                                              |
| `variable.count('x')`                              | Cuenta el número de veces que aparece un carácter.                                                                                                                                                                                                                                                                                                                                                  |
| variable.find('x')                                 | Devuelve la primera posición en la que encuentra el carácter ‘x’.                                                                                                                                                                                                                                                                                                                                   |
| `variable.isalnum()`                               | Devuelve True si todos los caracteres son alfanuméricos.                                                                                                                                                                                                                                                                                                                                            |
| `variable.isalpha()`                               | Devuelve True si todos los caracteres son alfabéticos.                                                                                                                                                                                                                                                                                                                                              |
| `variable.islower()`                               | Devuelve True si todos los caracteres están en minúscula.                                                                                                                                                                                                                                                                                                                                           |
| `variable.isspace()`                               | Devuelve True si todos los caracteres son espacios en blanco.                                                                                                                                                                                                                                                                                                                                       |
| `variable.istitle()`                               | Devuelve True si la primera letra de cada palabra está en mayúsculas.                                                                                                                                                                                                                                                                                                                               |
| `variable.isupper()`                               | Devuelve True si todos los caracteres están en mayúsculas.                                                                                                                                                                                                                                                                                                                                          |
| `variable.split('x')`                              | Corta la frase cuando encuentra el carácter ‘x’ y la divide en varias partes.                                                                                                                                                                                                                                                                                                                       |
| `variable.partition('x')`                          | Divide la frase en 2 partes cuando se encuentra el carácter ‘x’ introducido.                                                                                                                                                                                                                                                                                                                        |
| `variable.strip()`                                 | Elimina los espacios al principio y al final de la cadena.                                                                                                                                                                                                                                                                                                                                          |

A continuación se muestra un ejemplo de cómo contar la frecuencia de cada carácter en una cadena de texto en Python. El código es el siguiente:

```python
# Creamos un diccionario vacío para almacenar los caracteres y sus frecuencias
diccionario_caracteres = {}

def contador(frase):
    # Convertimos la frase a minúsculas para que el conteo no sea sensible a mayúsculas
    frase = frase.lower()

    # Iteramos sobre cada carácter en la frase
    for letra in frase:
        # Si el carácter ya está en el diccionario, incrementamos su conteo
        if letra in diccionario_caracteres:
            diccionario_caracteres[letra] += 1
        # Si el carácter no está en el diccionario, lo agregamos con un conteo de 1
        else:
            diccionario_caracteres[letra] = 1

# Solicitamos al usuario que introduzca una frase
s = input("Introduce una frase para contar los caracteres: ")
# Llamamos a la función contador con la frase del usuario
contador(s)

# Iteramos sobre las llaves (caracteres) en el diccionario
for llaves in diccionario_caracteres.keys():
    # Imprimimos cada carácter y su frecuencia
    print(f"El carácter '{llaves}' aparece {diccionario_caracteres[llaves]} veces")

# También podemos usar el método count de las cadenas de texto para contar la aparición de un carácter específico
print(f"El carácter 'a' aparece {s.count('a')} veces")
```

Este código cuenta la frecuencia de cada carácter en la cadena de texto ingresada por el usuario. También muestra cómo usar el método `count()` de las cadenas de texto para contar la aparición de un carácter específico. Este método es sensible a mayúsculas y minúsculas. Por lo tanto, si queremos contar la aparición de un carácter sin importar si está en mayúsculas o minúsculas, podemos convertir la cadena de texto a minúsculas o mayúsculas antes de usar el método `count()`. Por ejemplo, `s.lower().count('a')`.

### 2.5.2. Formato de impresión en pantalla

Si queremos mostrar un dato de tipo `float` (número con coma flotante) pero con una cantidad determinada de decimales, podemos especificarlo con el siguiente formato: `{valor_float:.precision}`

Por ejemplo, si queremos mostrar el número pi con 5 decimales, podemos hacerlo de la siguiente manera:

```python
import math
pi = math.pi
print(f"El número pi con 5 decimales es: {pi:.5f}")
```

## 2.6. Listas

Las listas en Python son una secuencia ordenada y mutable que puede almacenar elementos de manera dinámica y de diferentes tipos. Que una lista sea ordenada significa que cada posición tiene un índice, siendo el índice de la posición inicial el 0. El término mutable hace referencia a que los elementos almacenados en la lista pueden ser modificados a lo largo del programa. Por último, que sea dinámica significa que la lista no tiene un tamaño fijo, por lo que este puede variar a lo largo del código. Por ejemplo:

```python
lista_amigos = ["Jorge", "Fran", "Ricardo"]
```

También podemos inicializar una lista sin valores:

```python
lista = []
```

Para acceder a los elementos de la lista, podemos hacerlo de la siguiente manera:

```python
print(f"El amigo que está en la misma universidad que yo es {lista_amigos[0]}")

# Al indicar el índice [-1] empezaría por el índice final, en este caso Ricardo
print(f"Mi amigo del pueblo es {lista_amigos[-1]}")

# Seleccionamos un rango
print(lista_amigos[0:2])

# Mostramos la lista de amigos al completo
print(lista_amigos)
```

### 2.6.1. Operaciones / Funciones

| Función                  | Definición                                                                                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `lista[indice] = x`      | Permite cambiar el dato de la lista que ocupa ese índice por el dato que se le asigne a continuación.                                                   |
| `lista.extend(x)`        | Permite concatenar listas o se puede usar el signo '+'. Permite agregar los objetos de una lista a otra lista sin tener una lista dentro de otra lista. |
| `lista.append(x)`        | Permite añadir un objeto al final de la lista.                                                                                                          |
| `lista.insert(indice,x)` | Primer parámetro es el índice de la lista ( posición a insertar en la lista ) y el segundo es el elemento a añadir.                                     |
| `lista.remove(x)`        | Para eliminar el objeto de la lista.                                                                                                                    |
| `lista.clear()`          | Permite vaciar la lista.                                                                                                                                |
| `lista.pop()`            | Elimina el último elemento de la lista o se le pude introducir un índice, así borraría el elemento de la lista que ocupe ese índice.                    |
| `lista.index(x)`         | Me dice el índice del parámetro dentro de la lista.                                                                                                     |
| `lista.count(x)`         | Devuelve el número de veces que se repite el dato en la lista.                                                                                          |
| `lista.sort()`           | Permite ordenar una lista de menor a mayor.                                                                                                             |
| `lista.reverse()`        | Invierte la lista.                                                                                                                                      |
| `lista2 = lista1.copy()` | Permite copiar los atributos de la `lista1` a la `lista2`.                                                                                              |
| `max(lista)`             | Muestra el máximo de una lista, para hacer lo contrario → `min(lista)`                                                                                  |
| `del lista[x]`           | Podemos eliminar el dato encontrado en el índice ‘x’ de la lista.                                                                                       |

Python permite utilizar bucles `for` directamente en una lista, lo cual puede ser más eficiente que un bucle `for` común. Aquí tienes un ejemplo:

```python
mi_lista = [letra for letra in "Hola"]

# Podríamos utilizar rangos y operaciones
mi_lista = [numero ** 2 for numero in range(0,20,2)]

celcius = [0,10,20,34.5]

fahrenheit = [((9/5)*temp + 32) for temp in celcius]

# Incluso añadir condiciones
mi_lista = [numero ** 2 for numero in range(0,15,2) if numero % 2 == 0]
```

### 2.6.2. Listas en 2D (matrices)

Python permite crear listas dentro de otras listas, creando una especie de malla o matriz. Aquí tienes un ejemplo:

```python
number_grid = [
    [1,2,3],
    [4,5,6],
    [7,8,9],
    [0]
]

# Para poder acceder a la fila 3 (porque se parte del 0) columna 3
print(number_grid[2][2])
```

Las librerías Numpy y Pandas son muy útiles para manipular datos y realizar operaciones con datos, entre ellas, matrices.

## 2.7. Diccionarios

Un diccionario en Python es una colección de datos no ordenada, mutable e indexada. Los diccionarios están escritos con corchetes y cuentan con **claves** (**keys**) y **valores** (**values**). Cada clave tiene que estar asociada a un valor único. Por ejemplo:

```python
conversion_meses = {
    "Ene": "Enero",
    "Feb": "Febrero",
    "Marz": "Marzo"
}
```

Con el diccionario anterior, vamos a mostrar cómo acceder a las claves del diccionario:

```python
# Devuelve el valor de "Ene" que es "Enero"
print(conversion_meses["Ene"]) 

print(conversion_meses.get("Ene"))
```

En caso de buscar un valor de clave no encontrado en un diccionario podemos utilizar la función `get()`, que permite mostrar un texto en caso de error:

```python
clave = "Daniel"
print(conversion_meses.get(clave, f"La clave {clave} no está en el diccionario"))
```
### 2.7.1. Funciones de los diccionarios

Los diccionarios en Python tienen varias funciones incorporadas que permiten manipular y acceder a sus elementos. Aquí tienes algunas de las más comunes:

* `diccionario.items()`: Devuelve una vista de los pares clave-valor del diccionario.
* `diccionario.keys()`: Devuelve una vista de las claves del diccionario.
* `diccionario.values()`: Devuelve una vista de los valores del diccionario.

Además, los diccionarios en Python pueden contener otros diccionarios, lo que permite crear estructuras de datos complejas. Por ejemplo:

```python
diccionario = {"k3":{'insideKey':100}}
```

Para acceder al valor de 'insideKey' en el diccionario anidado, puedes hacerlo de la siguiente manera:

```python
diccionario["k3"]['insideKey']
```

También puedes iterar sobre las claves, los valores y los elementos (pares clave-valor) de un diccionario. Aquí tienes un ejemplo:

```python
d = {'k1':1,'k2':2}

for llave in d.keys():

	print(llave)

for valor in d.values():

	print(valor)

for elemento in d.items():

	print(elemento)
```

Puedes combinar listas y diccionarios para crear estructuras de datos más complejas. Por ejemplo, puedes tener una lista de diccionarios, donde cada diccionario representa a un cliente y sus animales:

```python
clientes = [
	{"nombre": "Daniel", "animales": ["Pakito", "Pakon", "Pakonazo"]},
	{"nombre": "Clemencia", "animales": ["Rodolfo"]},
	{"nombre": "Carolina"}
]

for cliente in clientes:

	print(f"{cliente['nombre']} tiene: {cliente.get('animales', 'No tiene animales')}")
```

## 2.8. Tuplas

Las tuplas en Python son similares a las listas, pero con la principal diferencia de que los elementos que almacenan son inmutables, es decir, no pueden sufrir modificaciones una vez creados. Una de las ventajas principales de las tuplas es que suelen ser más rápidas de iterar sobre ellas en comparación con las listas. Por ejemplo:

```python
# Este es mi tuple, recordar que una vez creado no se puede modificar
coordenadas = (4, 5)

print(f"Coordenada completa {coordenadas}")
print(f"Primera coordenada {coordenadas[0]} y la segunda coordenada {coordenadas[1]}")
```

### 2.8.1. Funciones de las tuplas

Las tuplas en Python tienen algunas funciones incorporadas que permiten manipular y acceder a sus elementos. Aquí tienes las más comunes:

* `tupla.count(x)`: Devuelve el número de veces que 'x' aparece en la tupla.
* `tupla.index(x)`: Devuelve el primer índice donde se encuentra 'x'.

También puedes crear una lista de tuplas. Por ejemplo:

```python
lista_tuplas = [(1,2) , (3,4) , (5,6)]
print(f"Mi lista de tuplas es {lista_tuplas}")
```

## 2.9. Conjuntos (Sets)

Un conjunto (`set`) en Python es una colección desordenada de elementos únicos. Esto significa que cada elemento puede aparecer solo una vez en un conjunto. Aquí tienes un ejemplo:

```python
# Para inicializar un conjunto vacío
mi_set = set()

# Añadimos el número 1 al conjunto
mi_set.add(1) 

# Intentamos añadir de nuevo el número 1 al conjunto
# Como cada elemento es único en un conjunto, no se añadirá nada
mi_set.add(1) 

mi_nuevo_set = {'a', 'b', 'c'}
```

### 2.9.1. Funciones de los conjuntos

Los conjuntos en Python tienen varias funciones incorporadas que permiten manipular y acceder a sus elementos. Aquí tienes algunas de las más comunes:

| Función                    | Definición                                                                                                                 |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `s.add(x)`                 | Añadir un elemento ‘x’ a un set.                                                                                           |
| `s.clear()`                | Borrar todos los elementos de un set.                                                                                      |
| `sc = s.copy()`            | Realizar una copia del set. Los cambios que se hagan en el set original no se verán afectados en la copia.                 |
| `s1.difference(s2)`        | Devolver la diferencia entre dos o mas sets, por ejemplo, un set que contenga un valor no encontrado en otro set.          |
| `s1.difference_update(s2)` | Borrar los elementos de un set que coinciden con los elementos de otro set.                                                |
| `s.discard(elem)`          | Descartar un elemento del set. En el caso de que no encuentre el dato no se produce ningún cambio.                         |
| `s1.intersection(s2)`      | Realizar la intersección de 2 o mas sets. Recordar que la intersección devuelve los elementos que son comunes en los sets. |
| `s1.issubset(s2)`          | Ver si un set contiene a otro set. Devuelve True o False.                                                                  |
| `s1.union(s2)`             | Unión de dos sets. Recordar que la unión consiste en combinar todos los elementos de los sets sin repetir ningún elemento. |

## 2.10. Booleanos (Bool)

Los booleanos son operadores que permiten transmitir declaraciones de verdadero (**True**) o falso (**False**). Los operadores booleanos son muy útiles en el control de flujo y lógica. Veremos diferentes casos de usos en los ejemplos siguientes.

## 2.11. Introducción de datos

Python ofrece la posibilidad de obtener información introducida por el usuario con la función `input(...)`. Es importante tener en cuenta que la función `input()` transforma todo el contenido pasado a tipo string. Esto es relevante si posteriormente necesitamos manipular datos con un tipo de dato concreto. Por ejemplo:

```python
# La variable nombre se queda con el input
nombre = input("Introduce tu nombre: ")
edad = input("Introduce tu edad: ")

print("\n\t- DATOS DEL USUARIO - \n")
print(f"Nombre: {nombre}")
print(f"Edad: {edad}")
```

Para convertir un input en un número y no como un string, tenemos que realizar una conversión de tipo de dato. Este procedimiento recibe el nombre de “casting”. Por ejemplo:

```python
# Hacemos un casting (conversión) de string a float
numero = float(input("Introduce un numero: "))
```

## 2.12. Manejo de archivos

Podemos abrir un fichero usando la función `open()`:

```python
file = open(dirección_del_fichero)
```

Python permite asignar diferentes permisos (escritura/lectura/ambas...) al fichero, algunos de estos permisos son:

| Permiso | Definición |
| ------- | ---------- |
| r       | Solo lectura. |
| w       | Solo escritura, reescribirá los archivos existentes o creará uno nuevo. |
| a       | Para añadir información al final del archivo. |
| r+      | Lectura y escritura. |
| w+      | Escritura y lectura, reescribirá los archivos existentes o creará uno nuevo. |
| wb      | Modo archivo, escritura y binario. |

### 2.12.1. Lectura de archivos

Para poder leer un fichero podemos utilizar algunas funciones como:

| Función       | Definición |
| ------------- | ---------- |
| `readable()`  | Devuelve un booleano para saber si se puede leer o no el fichero. |
| `read()`      | Muestra toda la información del fichero. |
| `readline()`  | Lee la primera línea del fichero. |
| `readlines()` | Lee todas las líneas del fichero y las inserta en una lista. |

Por ejemplo:

```python
nombre_fic = input("Nombre del fichero: ")

fichero = open(nombre_fic,"r")

if fichero.readable():
	
	lista = fichero.readlines()
```

Alternativa:

```python
for empleado in empleado_fic: 

	print(empleado)

# Es recomendado cerrar el fichero luego de tratar con el
empleado_fic.close() 
```

Si leemos archivos directamente con métodos como `read()`, al leer de nuevo el fichero no aparecerá nada, para solucionarlo hay que usar:

* `nombre_fichero.seek(0)` → Permite poner el cursor al principio del fichero.

Otra forma de abrir un fichero y operar con él sería:

```python
with open('myfile.txt', mode='w') as my_new_file:

	contents = my_new_file.read()

print(contents)
```

### 2.12.2. Escritura de archivos

Un ejemplo de cómo escribir en un fichero sería:

```python
nombre_fic = input("Nombre del fichero: ")

fichero = open(nombre_fic,"a") # Voy a añadir texto al final

nuevo_empleado = input("Nombre del nuevo empleado: ")
funcion_empleado = input(f"Puesto del empleado {nuevo_empleado}: ")

fichero.write("\\n" + nuevo_empleado + " - " + funcion_empleado)

fichero.close()
```

# 3. Operadores

## 3.1. Operadores de comparación

En Python, además de poder comparar números, también podemos comparar cadenas de texto (`string`), distinguiendo entre mayúsculas y minúsculas. Aquí tienes una lista de los operadores de comparación más comunes:

| Expresión | Definición |
| --------- | ---------- |
| A == B    | A es igual a B. |
| A != B    | A es distinto que B. |
| A < B     | A es menor que B. |
| A <= B    | A es menor o igual que B. |
| A > B     | A es mayor que B. |
| A >= B    | A es mayor o igual que B. |

## 3.2. Operadores lógicos

Los operadores lógicos se pueden utilizar para combinar operadores de comparación. Los operadores lógicos en Python son:

| Expresión | Definición |
| --------- | ---------- |
| `and`     | Todas las condiciones han de ser verdaderas para que sea True. Si una de las condiciones es False, el resultado será False. |
| `or`      | Basta con que una de las condiciones sea True para que el resultado sea True. |
| `not`     | Sirve para negar la condición. |

## 3.3. Operadores útiles

Python ofrece una serie de operadores útiles para trabajar con listas y números. Aquí tienes algunos ejemplos:

Para cambiar el orden de manera aleatoria de una lista:

```python
import random

mi_lista = [1,2,3,4,5,6,7,8,9,10]

# No devuelve nada, se baraja de manera aleatoria en el mismo lugar
random.shuffle(mi_lista) 
```

Para obtener un número aleatorio de un rango establecido:

```python
import random

# Importamos de la librería random la función randint
from random import randint

randint(0,100)
```

# 4. Declaraciones `if`, `elif` y `else`

Las declaraciones `if`, `elif` y `else` se utilizan en Python para controlar el flujo de ejecución del programa en función de ciertas condiciones.

La sintaxis de una declaración `if` es la siguiente:

```python
if condicion:

    # Código a ejecutar si la condición es verdadera
```

La sintaxis de una declaración `if/else` es la siguiente:

```python
if condicion:

    # Código a ejecutar si la condición es verdadera

else:

    # Código a ejecutar si la condición es falsa
```

La sintaxis de una declaración `if/elif/else` con varias condiciones es la siguiente:

```python
if primera_condicion:

    # Código a ejecutar si la primera condición es verdadera

elif segunda_condicion:
    
	# Código a ejecutar si la segunda condición es verdadera

else:
    
	# Código a ejecutar si ninguna de las condiciones anteriores es verdadera
```

Aquí tienes un ejemplo en el que se utiliza una declaración `if` y `else` para comprobar si un elemento se encuentra dentro de una lista:

```python
# Primer ejemplo
numero = 1
lista = [1,2,3]

if numero in lista:
    
	print(f"El número {numero} se encuentra en la lista")

else:
    
	print(f"El número {numero} no se encuentra en la lista")

# Segundo ejemplo
d = {'mykey' : 345}

if 345 in d.keys():
    
	print("El valor se encuentra dentro del diccionario")

else:
    
	print("El valor no se encuentra dentro del diccionario")
```
En el primer ejemplo, se comprueba si el número 1 está en la lista. En el segundo ejemplo, se comprueba si el valor 345 está entre las claves del diccionario `d`. En ambos casos, se imprime un mensaje en función del resultado de la comprobación. Si la condición es verdadera, se imprime un mensaje indicando que el elemento se encuentra en la lista o en el diccionario. Si la condición es falsa, se imprime un mensaje indicando que el elemento no se encuentra en la lista o en el diccionario.

# 5. Bucles

## 5.1. Bucle `for`

Muchos objetos en Python son iterables, es decir, podemos recorrer cada uno de sus elementos. Un ejemplo podría ser recorrer cada elemento que compone una lista o los caracteres que componen un string. Usamos entonces los bucles `for` para iterar sobre dichos elementos. Aquí tienes la sintaxis:

```python
for variable_recorre in lugar_a_recorrer:

    # Código a ejecutar
```

Podemos establecer un rango de recorrido para el bucle con la función `range(x, y, z)`, donde 'x' es el inicio, 'y' es el fin - 1 y 'z' es el tamaño de paso.

Por ejemplo:

```python
# Primer ejemplo

# Imprimir los números del 1 hasta el 10
for index in range(1, 11): 

    print(index)

# Segundo ejemplo

# Recorrer la lista hasta llegar al tamaño máximo de la lista
for index in range(len(mi_lista)):

    print(mi_lista[index])

# Tercer ejemplo
# Muy útil si operamos con matrices

mylist = []

for x in [2, 4, 6]:

    for y in [100, 200, 300]:

        # Multiplicamos cada valor de x por y
        mylist.append(x * y) 
```

La función `zip()` permite asignar un índice a un valor de dos listas diferentes para formar una tupla. Hay que tener en cuenta que si las listas tienen diferentes tamaños, se hará un zip con el máximo de elementos de la lista con menor número de elementos.

* `zip(x, y, ...)` → Se pueden meter tantas listas como se requieran.

Por ejemplo:

```python
mi_lista1 = [1, 2, 3]
mi_lista2 = ['a', 'b', 'c']
mi_lista3 = [100, 200, 300]

for item in zip(mi_lista1, mi_lista2, mi_lista3):

    print(item)
```

Otros ejemplos de bucles `for`:

```python
# Primer ejemplo

mi_lista = [1 ,2 ,3]
i = 0

# Con enumerate podemos descomponer los elementos de un array en su indice y valor
for idx, elemento_lista in enumerate(mi_lista):

    print(f"{elemento_lista} ocupa la posición {idx} de la lista")

# Segundo ejemplo

# "letra" coge cada carácter del string
for letra in "Hola muy buenas": 

    print(letra )

# Tercer ejemplo

# Creamos una lista de tuplas
mi_lista = [(1,2) , (3,4) , (5,6)]

for a, b in mi_lista:

    print(f"X: {a} \n\tY: {b}")

# Cuarto ejemplo

# Para obtener los elementos de un string en forma de tuplas
# Utilizamos la función "enumerate" ya que devuelve el índice y el elemento

word = "abcde"

for elemento in enumerate(word):

    print(elemento)
```

## 5.2. Bucle `while`

El bucle `while` realiza un bucle mientras se cumpla la condición. Aquí tienes la sintaxis:

```python
while condicion:

    # Código a ejecutar
```

También existe la posibilidad de combinarlo con un `else`:

```python
while condicion:

    # Código a ejecutar

else:
    
	# Código a ejecutar en el caso de que la condición del while no se cumpla
```

## 5.3. `break`, `continue` y `pass`

`break`→ Rompe con el bucle que se esté ejecutando en ese momento. Por ejemplo:

```python
mi_string = "Daniel"

# En este bucle, al encontrar la letra 'a' saldríamos del bucle
for letra in mi_string:

    if letra == 'a': 
    
	    break
    
	print(letra)
```

`continue`→ Va a la parte superior del bucle de cierre más cercano. Por ejemplo:

```python
mi_string = "Daniel"

# En este bucle, al encontrar la letra 'a' se pasará al siguiente carácter sin mostrar
# la 'a', es decir, se salta el "print(letra)"
for letra in mi_string:

    if letra == 'a':
    
	    continue
    
	print(letra)
```

`pass`→ No hace nada en el bucle y se utiliza para evitar errores cuando se requiere una declaración sintáctica pero no se quiere ejecutar ningún código. Es útil como un marcador de posición cuando se está diseñando código a nivel de esquema. Por ejemplo:

```python
for letra in 'Python':

    if letra == 'h':
    
	    pass
        print('Esta es la letra h')
    
	print('Letra actual:', letra)
```
En este ejemplo, la declaración `pass` permite que el bucle `for` continúe su iteración normalmente después de la letra 'h'. Sin la declaración `pass`, habría un error porque Python espera una declaración después del `if` pero no encuentra ninguna. Con `pass`, Python tiene una declaración que no hace nada, lo que evita el error.

# 6. Métodos y funciones

## 6.1. Métodos

Los métodos son funciones que están asociadas a un objeto y pueden actuar sobre el objeto mismo. Cada tipo de objeto tiene un conjunto de métodos asociados. Por ejemplo, los objetos de tipo `str` (cadenas de texto) tienen métodos para convertir a mayúsculas, dividir la cadena en palabras, reemplazar una subcadena, etc.

Para obtener una lista completa de los métodos disponibles para un tipo de objeto en particular, puedes usar la función `dir()`. Por ejemplo, `dir(str)` te dará una lista de todos los métodos que puedes usar en objetos de tipo `str`.

Además, puedes obtener ayuda sobre un método específico usando la función `help()`. Por ejemplo, `help(str.upper)` te dará información sobre el método `upper()` que se puede usar en cadenas de texto.

Para obtener información más detallada y actualizada sobre los métodos en Python, te recomiendo visitar la documentación oficial de Python en [https://docs.python.org/](https://docs.python.org/).

## 6.2. Funciones

Las funciones en Python son bloques de código reutilizables que realizan una tarea específica. Puedes definir tus propias funciones usando la palabra clave `def`, seguida del nombre de la función y una lista de parámetros entre paréntesis. El código de la función va indentado después de los dos puntos.

Aquí tienes un ejemplo de cómo definir y usar una función en Python:

```python
def saludo(nombre):

    return f"Hola, {nombre}!"

print(saludo("Mundo"))
```

En este ejemplo, `saludo` es una función que toma un parámetro, `nombre`, y devuelve una cadena de texto que es un saludo a ese nombre.

Las funciones pueden tomar cualquier número de parámetros, y estos parámetros pueden tener valores predeterminados. Si un parámetro tiene un valor predeterminado, puedes omitir ese parámetro cuando llamas a la función. Aquí tienes un ejemplo:

```python
def saludo(nombre="Mundo"):
    
	return f"Hola, {nombre}!"

print(saludo())
print(saludo("Python"))
```

En este ejemplo, `nombre` tiene un valor predeterminado de `"Mundo"`. Si llamas a `saludo()` sin ningún argumento, usará el valor predeterminado. Si proporcionas un argumento, ese argumento reemplazará el valor predeterminado.

Las funciones son una excelente manera de organizar tu código y hacerlo más legible y reutilizable. También pueden ayudarte a dividir problemas complejos en partes más manejables.

### 6.2.1. Funciones con Lógica

Las funciones en Python pueden contener una variedad de estructuras de control, como bucles y llamadas a otras funciones. Aquí te presento algunos ejemplos:

+ Función para comprobar una lista:	Esta función toma una lista de números como entrada y separa los números pares e impares en dos conjuntos diferentes:

	```python
	def comprobar_lista(lista):

		lista_par_devolver = set()
		lista_impar_devolver = set()

		for indice in lista:
		
			if indice % 2 == 0:
		
				lista_par_devolver.add(indice)
		
			else:
		
				lista_impar_devolver.add(indice)

		print(f"Lista de números pares de la lista principal: {lista_par_devolver}")
		print(f"Lista de números impares de la lista principal: {lista_impar_devolver}")

	comprobar_lista([1, 1, 1, 1, 1, 1, 23, 56, 87, 918, 23, 12, 3, 2, 4, 6, 5])
	```

+ Función con tuplas: Este ejemplo muestra una función que determina el trabajador con más horas trabajadas:

	```python
	horas_trabajadores = [("Daniel", 22), ("Kike", 20), ("Ricardo", 25)]

	def mejor_trabajador(lista):
	
		maximo = 0
		mejor = ""

		for empleado, horas in horas_trabajadores:
	
			if horas > maximo:

				maximo = horas
				mejor = empleado

		return (mejor, maximo)

	mejor, maximo = mejor_trabajador(horas_trabajadores)

	print(f"El mejor trabajador es {mejor} que ha trabajado un total de {maximo} horas")
	```

+ Funciones que llaman a otras funciones: En este ejemplo, se muestra un juego simple donde las funciones llaman a otras funciones. Se utiliza la función `shuffle()` de Python, que reordena una lista de manera aleatoria:

	```python
	# El juego de la bolita
	vasos = [' ','O',' ']

	def shuffle_list(mi_lista):
	
		shuffle(mi_lista)
		return mi_lista

	def inicio():
	
		print("La bolita se encuentra en el vaso 2\n")
		print('vaso 1: ')
		print('vaso 2: O')
		print('vaso 3: ')
		print("\nMoviendo la bola por los diferentes vasos...\n")

	def operar():
	
		resultado = int(input("¿En qué vaso está la bolita?: "))

		while resultado != 1 and resultado != 2 and resultado != 3:
	
			print("Este vaso no existe")
			resultado = int(input("¿En qué vaso está la bolita?: "))

		comprobar(resultado)

	def comprobar(resultado):
	
		i = 1

		if vasos[resultado-1] == 'O':
	
			print("\n¡Has acertado!\n")
	
			for vaso in vasos:
	
				print(f"vaso {i}: {vaso}")
				i += 1
	
		else:
	
			print("\nHas fallado :(\n")
	
			for vaso in vasos:
	
				print(f"vaso {i}: {vaso}")
				i += 1

	inicio()
	shuffle_list(vasos)
	operar()
	```
Estos ejemplos muestran cómo las funciones en Python pueden contener lógica compleja y cómo pueden interactuar entre sí para realizar tareas más grandes.

## 6.3. Argumentos Arbitrarios: \*Args y \*\*Kwargs

En Python, los términos **`*args`** y **`**kwargs`** se utilizan en la definición de funciones para permitir que estas acepten un número arbitrario de argumentos. Veamos algunos ejemplos:

### 6.3.1. Funciones con Argumentos Posicionales

En el siguiente ejemplo, `a` y `b` son argumentos posicionales. La función `mifuncion` toma estos dos argumentos, los suma y luego multiplica el resultado por 0.05:

```python
def mifuncion(a, b):

    return sum((a, b)) * 0.05

mifuncion(40,60) 
```

Sin embargo, si quisiéramos que esta función pudiera manejar más de dos números, tendríamos que modificar la definición de la función para incluir más parámetros. Una opción sería asignar un valor predeterminado a estos parámetros adicionales:

```python
def mifuncion(a, b, c = 0):

    return sum((a, b, c)) * 0.05
```

### 6.3.2. Funciones con \*Args

Aquí es donde **`*args`** resulta útil. Nos permite configurar la función para aceptar un número arbitrario de argumentos:

```python
def mifuncion(*args):

    return sum(args) * 0.05
```

En este caso, **`*args`** permite tratar la entrada como una tupla de parámetros. Ahora podemos pasar tantos argumentos como queramos. Por defecto, Python toma todos los parámetros que se pasan y los configura como una tupla.

### 6.3.3. Funciones con \*\*Kwargs

De manera similar, Python ofrece una forma de manejar un número arbitrario de argumentos de palabras clave. En lugar de crear una tupla, crea un diccionario. Para ello, usamos **`**kwargs`**:

```python
def mifuncion(**kwargs):

    if 'fruta' in kwargs:

        print(f"Mi fruta favorita es la {kwargs['fruta']}")

    else:

        print("No se encontró la fruta")
    
    if 'verduras' in kwargs:

        print(f"Mi verdura favorita es la {kwargs['verduras']}")

    else:

        print("No se encontró la verdura")

mifuncion(fruta = 'manzana', verduras = 'zanahoria')
```

### 6.3.4. Combinando \*Args y \*\*Kwargs

También podemos combinar **`*args`** y **`**kwargs`** en la misma función:

```python
def mifuncion(*args, **kwargs):

    print(f"Tengo {args[0]} coneja llamada {kwargs['animal']}")

mifuncion(1,2,3,4,fruta = "manzana",verdura = "zanahoria",animal = "Misifu")
```

En este caso, `args` es una tupla de los argumentos posicionales y `kwargs` es un diccionario de los argumentos de palabras clave. Esto nos da una gran flexibilidad a la hora de definir funciones en Python.

## 6.4. Expresiones Lambda, Funciones Map y Filter

Las **expresiones Lambda**, junto con las funciones **`map()`** y **`filter()`**, son herramientas poderosas en Python que permiten un procesamiento de datos avanzado. 

### 6.4.1. Expresiones Lambda

Las **expresiones Lambda** son una forma rápida de crear funciones anónimas, es decir, funciones que se utilizan una sola vez. 

```python
lambda num: pow(num,2)
```

Esta expresión lambda toma un número, lo eleva al cuadrado y devuelve el resultado. 

### 6.4.2. Función Map

La función **`map()`** aplica una función a cada elemento de una lista, devolviendo una nueva lista con los resultados. 

```python
mis_nums = [1,2,3,4,5]
list(map(lambda num: pow(num,2),mis_nums))
```

En este ejemplo, la función `map()` aplica la expresión lambda a cada elemento de `mis_nums`, devolviendo una nueva lista con los cuadrados de los números originales.

### 6.4.3. Función Filter

La función **`filter()`** filtra los elementos de una lista basándose en una función de filtrado, devolviendo una nueva lista con los elementos que cumplen la condición de filtrado.

```python
mis_nums = [1,2,3,4,5]
list(filter(lambda num: num % 2 == 0,mis_nums))
```

En este ejemplo, la función `filter()` aplica la expresión lambda a cada elemento de `mis_nums`, devolviendo una nueva lista con solo los números pares.

### 6.4.4. Combinando Lambda, Map y Filter

Las expresiones lambda se utilizan comúnmente junto con las funciones `map()` y `filter()`, permitiendo un procesamiento de datos más conciso y eficiente.

```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson',
			'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

list(map(lambda person: person.split()[0] + ' ' + person.split()[-1], people))
```

En este ejemplo, la función `map()` aplica la expresión lambda a cada elemento de `people`, devolviendo una nueva lista con solo el título y el apellido de cada persona.

Es importante recordar que las expresiones lambda pueden tomar múltiples argumentos, lo que aumenta su flexibilidad y utilidad. Sin embargo, debido a su naturaleza anónima y de un solo uso, las expresiones lambda son más adecuadas para operaciones simples y concisas. Para operaciones más complejas, es recomendable definir una función completa.

## 6.5. Declaraciones anidadas y alcance del código (Scope)

En Python, es crucial entender cómo se manejan las variables que creamos. Estas variables se almacenan en lo que se conoce como un "alcance" o "scope", que determina la visibilidad de la variable a otras partes del código.

Por ejemplo:

```python
x = 25

def printer():

    x = 50
    return x

print(x)  # Devuelve 25
print(printer())  # Devuelve 50
```

En este ejemplo, la reasignación de `x` dentro de la función `printer()` no afecta a la asignación global de `x`. Esto se debe a la regla de alcance (scope) en Python, que sigue la regla LEGB:

* **L, Local** — Nombres asignados de alguna manera dentro de una función (`def` o `lambda`) y que no se declaran globales en esa función.
* **E, Enclosing function locals** — Nombres en el ámbito local de cualquier y todas las funciones de encierro (`def` o `lambda`), de interior a exterior.
* **G, Global (module)** — Nombres asignados en el nivel superior de un archivo de módulo, o declarados globales en un `def` dentro del archivo.
* **B, Built-in (Python)** — Nombres preasignados en el módulo de nombres incorporado: `open`, `range`, `SyntaxError`, etc.

Este es el orden en el que Python buscará las variables. Aquí hay un ejemplo de cómo funciona:

```python
# VARIABLE GLOBAL
nombre = "Esto es un string global"

def prueba():

    # VARIABLE DE ENCIERRO LOCAL
    nombre = "Daniel"

    def hola():

        # VARIABLE LOCAL
        nombre = "Carlitos"
        print(f"Hola {nombre}")

    hola()

prueba()
```

En este ejemplo, la función `hola()` mostrará primero la variable local "Carlitos". Si comentamos la asignación local, cogerá la variable de encierro local "Daniel". Y si también comentamos esa asignación, cogerá la variable global "Esto es un string global".

Ahora, veamos qué sucede cuando reasignamos una variable global dentro de una función. Si hacemos una reasignación dentro de la función, por el alcance (scope), el valor de reasignación solo se mantiene dentro de la función. Una vez que salimos de ella, el valor de la variable vuelve a ser el valor que se le asignó al principio. Para cambiar esto, podemos usar la palabra clave `global`, como en el siguiente ejemplo:

```python
x = 50

def prueba():

    global x
    print(f"Valor de x antes {x}")
    x = 200
    print(f"Valor de x despues {x}")

prueba()
print(f"Valor de x fuera {x}")
```

Sin embargo, se recomienda evitar el uso de la palabra clave `global` a menos que sea absolutamente necesario. Es más seguro devolver un objeto y luego asignarlo a la variable. De esta manera, evitamos sobrescribir la variable global dentro de una función sin siquiera saberlo.

## 6.6. Validación de Datos

Cuando se crean funciones que toman valores de entrada del usuario, es importante verificar esas entradas para asegurarse de que son correctas. Esto se conoce como validación de datos.

La función `input()` en Python puede ser un poco complicada porque espera la interacción del usuario. Si se ejecuta accidentalmente dos veces, el programa puede quedarse esperando una respuesta que no llega. En ese caso, en Jupyter tendrías que reiniciar el kernel, teniendo en cuenta que todas las variables anteriores se borrarán y tendrías que ejecutarlas de nuevo.

Una forma cómoda de validar datos es utilizar bucles `while` para pedir al usuario que introduzca un valor repetidamente cuando este no es válido. Aquí tienes un ejemplo:

```python
def limite(eleccion):

    return int(eleccion) >= 1 and int(eleccion) <= 10

def eleccion_usuario():

    eleccion = input("Numero de 1-10: ")
    
    while not eleccion.isdigit() or not limite(eleccion):

        eleccion = input("Numero de 1-10: ")
        
        if not eleccion.isdigit():

            print("El valor introducido no es un numero")
        
        if eleccion.isdigit() and not limite(eleccion):

            print("El numero introducido supero el limite")
    
    return int(eleccion)

eleccion_usuario()
```

En este ejemplo, la función `eleccion_usuario()` pide al usuario que introduzca un número entre 1 y 10. Si el valor introducido no es un número o si no está en el rango correcto, la función le pide al usuario que introduzca un nuevo valor.

Si quieres limpiar la consola cuando el usuario introduce valores incorrectos, puedes importar y usar la biblioteca `IPython.display` y usar la función `clear_output()`:

```python
from IPython.display import clear_output
```

Esta función borra la salida de la celda actual en un cuaderno Jupyter, lo que puede ser útil para mantener la interfaz de usuario limpia. Sin embargo, ten en cuenta que `clear_output()` solo funciona en cuadernos Jupyter y no en otros entornos de Python.

# 7. Programación Orientada a Objetos (POO)

## 7.1. Introducción

La Programación Orientada a Objetos (POO) permite crear objetos propios que tienen métodos y atributos. Estos métodos actúan como funciones que usan información sobre el objeto, así como el objeto mismo (`self`), para realizar operaciones o cambiar el estado del objeto. La POO permite crear código que es repetible y organizado, facilitando la creación de programas flexibles y escalables. A menudo, al usar bibliotecas externas, estas emplean la POO. Aquí tienes un ejemplo sencillo para entender la sintaxis:

```python
# Las clases por convención se nombran con palabras en mayúsculas
class NombreDeClase():

	# __init__ es un método especial que permite crear una instancia del objeto actual
	# donde parametro1 y parametro2 son parámetros que definen al objeto
	# y que Python espera que le pasemos
	# Lo que hacemos es conectar el parámetro con el uso de ese parámetro para vincularlo
	# al objeto
	
	# Método 1
	def __init__(self,parametro1,parametro2): 
	
		self.parametro1 = parametro1
		self.parametro2 = parametro2

	# Luego podemos tener otros métodos dentro de la misma clase
	# Se le pasa el self para que Python reconozca que no es solo una función,
	# sino que se trata de un método

	# Método 2
	def algun_metodo(self): 

		# Se realiza alguna acción dentro de la función
	
# Cuando una función se encuentra dentro de una clase
# pasa de llamarse función a llamarse método
```

## 7.2. Atributos y Clases

La clase es un plano que define la naturaleza de un objeto. Podemos construir un objeto en una instancia, esta instancia es un objeto específico creado a partir de una clase en particular. Aquí tienes un ejemplo de una clase junto con sus atributos y sus métodos:

```python
# Variable Global
max_personas = 4 

class Coche():

	# __init__ es un método especial, invocado cada vez que creamos una instancia 
	# de la clase, empezaremos siempre con la palabra clave "self" que conecta este 
	# método con la instancia de la clase y nos permite referirnos a sí mismo, 
	# luego pasamos el resto de atributos.

	def __init__(self,marca,modelo,mejorado,acceso_coche):
	
		self.marca = marca
		self.modelo = modelo
		self.mejorado = mejorado
		self.acceso_coche = acceso_coche

	lista_personas = []
	mejorado = False

# No tiene por qué tener el mismo nombre de variable que los parámetros de la clase
marca = input("Marca del coche: ")
modelo = input("Modelo del coche: ")
m = input("¿Mejoras incluidas? (S: sí , N: no): " ).upper()

while m != 'S' and m!= 'N':

	m = input("¿Mejoras incluidas? (S: sí , N: no): " ).upper()

if m == 'S':

	mejorado = True

for i in range(0,max_personas):

	lista_personas.append(input(f"Persona {i} con acceso al coche: "))

# Creamos un objeto "*mi_coche*" del tipo "*Coche*"
mi_coche = Coche(marca,modelo,mejorado,lista_personas)

print(f"Mi coche es un {mi_coche.marca} y es el modelo {mi_coche.modelo}")

if mi_coche.mejorado:

	print(", con todas las mejoras incluidas")

else:

	print(", sin mejoras incluidas")

for persona in mi_coche.acceso_coche:
	
	print(f"{persona} tiene acceso a mi coche")
```
En este ejemplo, creamos una clase `Coche` con varios atributos y métodos. Luego creamos una instancia de `Coche`, `mi_coche`, y utilizamos sus métodos y atributos. La Programación Orientada a Objetos nos permite organizar nuestro código de manera eficiente y reutilizable.

## 7.3. Atributos de la Clase y Métodos

Los atributos de los objetos de una clase son los mismos para cualquier instancia de la clase. Los métodos, por otro lado, son acciones que realizamos con el objeto que hemos creado. Aquí tienes un ejemplo:

```python
class Perro():

	# Atributo del objeto de la clase Perro
	# Es igual para cualquier instancia de la clase. Por ejemplo, cualquier perro,
	# independientemente de sus características, es un mamífero.
	especie = "mamifero"

	def __init__(self,raza,nombre,edad):
		
		# Los atributos son características del objeto
		self.raza = raza 
		self.nombre = nombre
		self.edad = edad

	# Método de la clase Perro
	def sonido(self): 
	
		return "Woof!"
	
	def informacion(self):
	
		print(f"Nombre del perro: {mi_perro.nombre}")
		print(f"Raza del perro: {mi_perro.raza}")
		print(f"Edad del perro: {mi_perro.edad}")
		print(f"Especie: {mi_perro.especie}")
		print(f"Sonido: {mi_perro.sonido()}")

name = input("Nombre del perro: ")
raza = input("Raza del perro: ")
edad = int(input("Edad del perro: "))

mi_perro = Perro(raza,name,edad)
mi_perro.informacion()
```

## 7.4. Herencia y Polimorfismo

La herencia es una forma de crear nuevas clases utilizando clases ya definidas. La principal ventaja de la herencia es la reutilización del código, lo que reduce la complejidad del programa. Aquí tienes un ejemplo de herencia:

```python
class Animal():

	def __init__(self):

		print("Se ha creado el animal")
	
	def quien_soy(self):
		
		print("Soy un animal")
	
	def comer(self):
	
		print("Estoy comiendo")

class Perro(Animal):
 
	def __init__(self):
		
		Animal.__init__(self)
	
	def quien_soy(self):

		print("Soy un perro")

	def sonido(self):

		print("El perro hace: Woof!")

mi_perro = Perro()
```

El polimorfismo se refiere a la forma en que diferentes clases de objetos pueden compartir el mismo nombre de método. Luego, esos métodos se pueden llamar desde el mismo lugar, aunque se puedan pasar una variedad de objetos diferentes. Aquí tienes un ejemplo:

```python
class Perro():

	def __init__(self,nombre):
	
		self.nombre = nombre

	def sonido(self):

		print(f"El perro {self.nombre} ladra")

class Gato():

	def __init__(self,nombre):

		self.nombre = nombre

	def sonido(self): # el metodo es único para cada clase

		print(f"El gato {self.nombre} maulla")

mi_perro = Perro("Roberto")
mi_gato = Gato("Catalina")
```

Una práctica más común es usar clases abstractas combinadas con herencia. Las clases abstractas son aquellas que no esperan ser instanciadas. Están diseñadas para servir como clase base. Aquí tienes un ejemplo:

```python
class Animal():

	def __init__(self,nombre):

		self.nombre = nombre

	def sonido(self):

		# La palabra clave "***raise***" se utiliza para plantear una excepción.
		raise NotImplementedError("Subclase debe implementar este método abstracto")

class Dog(Animal): 

	def sonido(self):

		return self.nombre + " hace woof!"
```

Uno de los ejemplos más realistas del polimorfismo podría ser crear una clase base que implemente el método de abrir un archivo en general, pero con diferentes clases derivadas que se encarguen de abrir archivos con formatos específicos.

# 8. Módulos y Paquetes

## 8.1. Pip install y PyPi

PIP es un sistema de gestión de paquetes utilizado para instalar y administrar paquetes de software escritos en Python. Por ejemplo, puedes usar PIP para instalar paquetes desde PyPi, que es un repositorio de software para el lenguaje de programación Python.

PyPi es un repositorio para paquetes de Python de código abierto de terceros. Las bibliotecas que hemos estado utilizando hasta ahora son bibliotecas integradas, pero puedes utilizar el comando `pip install` en la terminal junto con el nombre del paquete que deseas instalar. Por ejemplo:

```python
# pip install colorama, en el terminal esta libreria permite utilizar texto de colores
from colorama import init
from colorama import Fore

init()

print(Fore.RED + "Texto de prueba")
```

## 8.2. Módulos y Paquetes

Un módulo es simplemente un archivo de Python con la extensión .py, y puede contener funciones, clases y variables. Un paquete, por otro lado, es una forma de organizar módulos relacionados en una carpeta jerárquica. La carpeta del paquete debe contener un archivo especial llamado `__init__.py`, que puede estar vacío pero debe estar presente en la carpeta.

Aquí tienes un ejemplo de cómo puedes organizar tu código en módulos y paquetes:

```python
# main.py
from paquete78 import some_main_script as p
from paquete78.Subpaquetes import mysubscript as s

p.main_report()
s.sub_report()
```

```python
# paquete78/some_main_script.py
def main_report():

	print("Hola soy una funcion dentro de mi script principal")
```

```python
# paquete78/Subpaquetes/mysubscript.py
def sub_report():

	print("Hola soy una funcion dentro de mi subscript")
```

## 8.3. Name y "main"

Cuando ejecutas un script de Python, Python asigna al nombre `__name__` el valor `"__main__"`. Pero si este código se importa como un módulo en otro script, el atributo `__name__` se asigna al nombre del archivo del script (sin la extensión .py). Aquí tienes un ejemplo:

```python
# one79.py
import two79

print(f"Archivo 1 __name__ establecido a: {__name__}")

if __name__ == "__main__":

	print("Archivo 1 ejecutado directamente")

else:

	print("Archivo 1 ejecutado como importado a otro modulo")
```

```python
# two79.py
import one79 as t

print(f"Archivo 2 __name__ establecido a: {__name__}")

if __name__ == "__main__":

	print("Archivo 2 ejecutado directamente")

else:

	print("Archivo 2 ejecutado como importado a otro modulo")
```

En este ejemplo, si ejecutas `one79.py`, verás que `__name__` se establece en `"__main__"` para `one79.py` y se establece en `"two79"` para `two79.py`. Esto es útil si quieres que cierto código se ejecute solo cuando el archivo se ejecuta directamente, y no cuando se importa como un módulo.

# 9. Manejo de errores y excepciones

## 9.1. Errores y manejo de excepciones

El manejo de errores es una estrategia que nos permite planificar y gestionar posibles errores que puedan surgir en nuestro código. Por ejemplo, si un usuario intenta escribir en un archivo que se ha abierto en modo de solo lectura y no hay ninguna declaración de error en el código, el programa entero se detendrá. Para evitar esto, utilizamos el manejo de excepciones, que nos permite continuar con el programa, notificar el error y seguir con el código.

Existen tres palabras clave para el manejo de errores en Python:

* `try`: Este es el bloque de código que se intentará ejecutar (puede llevar a un error).
* `except`: Bloque de código que se ejecutará en caso de que haya un error en el bloque de prueba (`try`).
* `finally`: Un bloque final de código que se ejecutará independientemente de si hubo un error o no.

Aquí tienes un ejemplo de cómo se utilizan estas palabras clave:

```python
try:

    f.open("fichero",'w')
    f.write("Linea de prueba")

except TypeError:

    print("Hubo un problema con el tipo")

except OSError: 

    print("Hubo un error de OSError")

except:

    print("Hubo un fallo en otro tipo de excepciones")

finally:

    print("De todos modos seguí ejecutando el código")
```

En este otro ejemplo, pediremos constantemente un dato al usuario hasta que introduzca un valor adecuado:

```python
def introducir_entero():

    while True:

        try:

            valor = int(input("Introduce un número entero: "))

        except:

            print("El valor introducido no es un número")

        else:

            print(f"El valor {valor} es un valor correcto")
            break

introducir_entero()
```

Python tiene más excepciones implementadas que puedes consultar en la documentación, en el apartado "Library → Exceptions".

## 9.2. Pylint

Las pruebas unitarias son esenciales a medida que expandimos nuestros proyectos con varios archivos o comenzamos a trabajar en equipo. Al realizar cualquier cambio o actualización en el código, podemos ejecutar archivos de prueba para asegurarnos de que el código anterior aún se ejecuta de la manera esperada.

Existen diferentes herramientas para probar el código, pero nos centraremos en dos de ellas:

* Pylint: Esta es una biblioteca que analiza el código e informa de posibles problemas.
* Unittest: Esta biblioteca incorporada permite probar tus propios programas y comprobar que estás obteniendo los resultados deseados.

Para usar Pylint, ejecuta el siguiente código en la terminal:

```bash
pylint nombre_fichero.py -r y
```

## 9.3. Unittest

Con `unittest`, puedes implementar un script en Python que analice los resultados devueltos por tu código y compruebe si son los esperados. Aquí tienes un ejemplo con dos archivos, `cap85a.py` y `cap85b.py`.

`cap85a.py`:

```python
def prueba(texto):

    return texto.capitalize()
```

`cap85b.py`:

```python
import cap85a
import unittest

class Test(unittest.TestCase):

    def test_1(self):

        texto = 'python'
        resultado = cap85a.prueba(texto)
        self.assertEqual(resultado,'Python')

if __name__ == '__main__':

    unittest.main()
```

En este ejemplo, `unittest` se utiliza para comprobar que la función `prueba` del archivo `cap85a.py` devuelve el resultado esperado. Si el resultado es el esperado, la prueba pasará. Si no, la prueba fallará y se mostrará un mensaje de error. 

# 10. Decoradores

Los decoradores en Python son una herramienta poderosa que permite "decorar" una función, es decir, modificar su comportamiento sin alterar su código fuente. Esto es útil cuando queremos añadir funcionalidades a una función existente sin modificar su definición.

## 10.1. Funciones como objetos

En Python, las funciones son objetos de primera clase. Esto significa que pueden ser asignadas a variables, almacenadas en estructuras de datos, pasadas como argumentos a otras funciones e incluso retornadas como valores de otras funciones. Aquí tienes un ejemplo:

```python
def funcion_saludo():

    return "Hola"

copia = funcion_saludo
del funcion_saludo

print(copia())  # Imprime: Hola
```

En este ejemplo, hemos asignado la función `funcion_saludo` a la variable `copia`, y luego hemos eliminado `funcion_saludo`. A pesar de esto, aún podemos llamar a la función original a través de `copia`.

## 10.2. Definición de un decorador

Un decorador es una función que toma otra función y extiende su comportamiento sin modificar explícitamente su código fuente. Aquí tienes un ejemplo de cómo se define y se usa un decorador:

```python
def nuevo_decorador(funcion_original):

    def funcion_nueva():

        print("Antes de la funcion original")
        funcion_original()
        print("Despues de la funcion original")

    return funcion_nueva

@nuevo_decorador
def funcion_necesita_decorador():

    print("Necesita un nuevo decorador")

funcion_necesita_decorador()
```

En este ejemplo, `nuevo_decorador` es un decorador que añade dos líneas de impresión antes y después de la ejecución de la función original. La sintaxis `@nuevo_decorador` antes de la definición de `funcion_necesita_decorador` es lo que aplica el decorador a la función.

## 10.3. Aplicaciones de los decoradores

Los decoradores tienen muchas aplicaciones. Por ejemplo, se utilizan en el desarrollo web con frameworks como Flask para añadir comportamientos a las funciones de ruta, como requerir que un usuario esté autenticado para acceder a ciertas páginas. También se utilizan para crear *loggers*, que registran cuándo se llaman a ciertas funciones y con qué argumentos, lo cual es útil para depurar y entender el flujo de ejecución de un programa. En resumen, los decoradores ofrecen una forma elegante y potente de modificar el comportamiento de las funciones en Python.

# 11. Generadores

Los generadores en Python son una forma eficiente de crear iteradores. A diferencia de las funciones normales, los generadores utilizan la palabra clave `yield` en lugar de `return`. Esto permite que los generadores produzcan valores de uno en uno, y solo cuando se necesitan, en lugar de calcular todos los valores a la vez y almacenarlos en memoria.

## 11.1. Funciones generadoras

Una función generadora es una función que utiliza la palabra clave `yield`. Cuando se llama a una función generadora, en lugar de ejecutar todo el cuerpo de la función y devolver un resultado, devuelve un objeto generador. Este objeto puede ser iterado para obtener los valores generados por `yield`. Aquí tienes un ejemplo de una función generadora que genera los cubos de los números hasta `n`:

```python
def funcion_cubo_generador(n):

    for x in range(n):

        yield pow(x,3) 

print(list(funcion_cubo_generador(10)))  # Imprime: [0, 1, 8, 27, 64, 125, 216, 343, 512, 729]
```

## 11.2. Generadores y rendimiento

Los generadores son especialmente útiles cuando trabajamos con grandes cantidades de datos que no caben en memoria. En lugar de generar todos los datos a la vez, los generadores los producen de uno en uno, solo cuando se necesitan. Esto puede mejorar significativamente el rendimiento de nuestro programa.

## 11.3. Generadores y la función `iter()`

La función `iter()` en Python convierte un objeto iterable en un iterador. Esto significa que podemos utilizar la función `next()` en el objeto para acceder a sus elementos uno a uno. Aquí tienes un ejemplo:

```python
s = "hello"
s_iterador = iter(s)
print(next(s_iterador))  # Imprime: h
```

En este ejemplo, hemos convertido la cadena `s` en un iterador utilizando la función `iter()`. Luego, hemos utilizado la función `next()` para obtener el primer elemento del iterador.

# 12. Módulos avanzados

## 12.1. Módulos de colección

El módulo `collections` en Python implementa tipos de datos de contenedores especializados que proporcionan alternativas a los contenedores generales de Python como `dict`, `list`, `set`, y `tuple`.

### 12.1.1. Counter

`Counter` es una subclase de diccionario para contar objetos hashables. Los elementos se almacenan como claves de diccionario y sus recuentos se almacenan como valores de diccionario.

```python
from collections import Counter

lista = [1,1,1,1,1,1,2,2,2,2,3,3,3,'a','adios']
cuenta = Counter(lista)
```

Puedes usar el método `most_common()` para obtener los elementos y sus recuentos desde el más común hasta el menos común.

```python
cuenta.most_common()
```

### 12.1.2. defaultdict

`defaultdict` es una subclase de diccionario que proporciona un valor predeterminado para la clave que no existe.

```python
from collections import defaultdict

d = defaultdict(lambda:0)
print(d["Prueba"])  # Imprime: 0
```

### 12.1.3. namedtuple

`namedtuple` genera subclases de tupla con campos nombrados. Esto permite acceder a los elementos de la tupla por nombre en lugar de índice.

```python
from collections import namedtuple

Conejo = namedtuple("Conejo",["Edad","Color","Nombre"])
misifu = Conejo(Edad = 2, Color = "Blanco", Nombre = "Misifu")

print(misifu.Edad)  # Imprime: 2
```

Estos son solo algunos ejemplos de los tipos de contenedores especializados disponibles en el módulo `collections`. Estos pueden ser muy útiles para hacer que tu código sea más legible y eficiente.

## 12.2. Manejo de archivos y directorios

En Python, se utilizan varios módulos para la apertura, lectura y manipulación de archivos y directorios en el sistema operativo. Los módulos principales son:

* *shutil*
* *os* (OS → Sistema Operativo)

Estos módulos permiten realizar operaciones como abrir y leer archivos individuales, navegar por los directorios, mover y eliminar archivos, entre otras.

```python
import os
import shutil
import send2trash

# Creación de un archivo de prueba
f = open("Prueba.txt",'w+')
f.write("Esto es una prueba de escritura en un archivo")
f.close()

# Obtención del directorio de trabajo actual
print(os.getcwd())

# Listado de los elementos en el directorio de trabajo
print(os.listdir())

# Listado de los elementos en un directorio específico
print(os.listdir('/home/usuario/'))

# Movimiento de archivos entre directorios
shutil.move("Prueba.txt",'/home/daniel/')

# Eliminación segura de archivos con send2trash
send2trash.send2trash("Prueba.txt")
```

Además, Python permite listar todos los archivos de un directorio, incluyendo carpetas, subcarpetas y ficheros que contienen:

```python
import os

directorio = '/home/daniel/Desktop'

for carpeta, sub_carpetas, archivos in os.walk(directorio):

    print(f"Estamos en la carpeta: {carpeta}")
    print("Las subcarpetas son: ")

    for sub_carpeta in sub_carpetas:

        print(f"\t{sub_carpeta}")

    print("Los archivos son: ")

    for archivo in archivos:

        print(f"\t{archivo}")
```

## 12.3. Módulo de fecha y hora

El módulo *datetime* de Python permite crear objetos que contienen información sobre la fecha y la hora, incluyendo la zona horaria. También permite realizar operaciones con fechas y horas, como calcular la diferencia entre dos fechas:

```python
import datetime
from datetime import date

mi_tiempo = datetime.time(2,20)

# Mostrar los minutos
print(mi_tiempo.minute)

# Imprimir la hora
print(mi_tiempo)

# Crear un objeto con la fecha del día
hoy = datetime.date.today()
print(hoy)

# Extraer información específica de la fecha
print(f"Día: {hoy.day}")
print(f"Mes: {hoy.month}")
print(f"Año: {hoy.year}")

# Realizar operaciones con las fechas
fecha1 = date(2021,11,3)
fecha2 = date(2020,11,2)

print(fecha1 - fecha2)
```

## 12.4. Módulo *math* y *random*

El módulo *math* en Python proporciona funciones matemáticas definidas por el estándar de C. Algunos ejemplos de su uso son:

```python
import math

# Podemos ver todas los métodos que incluye el módulo math
help(math)

# El número pi
math.pi

# El número e
math.e

# Infinito
math.inf

# Hacer el logaritmo neperiano
math.log(math.e)

# Podemos cambiar la base del logaritmo, por ejemplo
# El siguiente ejemplo hace el logaritmo de 100 en base 2
math.log(100,2)

# Seno:
math.sin(90)

# Pasar a radianes o grados
print(math.degrees(math.pi/2))
print(math.cos(math.radians(90)))
```

El módulo *random* en Python se utiliza para generar números aleatorios. Algunos ejemplos de su uso son:

```python
import random

# Devuelve un valor entero aleatorio
random.randint(0,100)

# Podemos poner cualquier valor, el más común es el 101,
# lo que hace es un generador pseudoaleatorio,
# pero son puramente deterministas, están operados por un
# algoritmo.
random.seed(101)

# Para crear una lista de números desde el 0 hasta el 9
lista = list(range(0,10))
print(lista)

numero_elegido_aleatorio = random.choice(lista)
print(numero_elegido_aleatorio)

# Si quiero elegir más de un elemento aleatorio de la lista
# haría lo siguiente:
numeros_aleatorios_repetidos = random.choices(population = lista,k = 5)
print(numeros_aleatorios_repetidos)

# O puedo elegir valores sin repetir ninguno
numeros_aleatorios_sin_repetir = random.sample(population = lista,k = 4)
print(numeros_aleatorios_sin_repetir)

# Ya hemos visto en otros ejemplos anteriores que podemos
# reordenar de manera aleatoria una lista con Shuffle
random.shuffle(lista)
print(lista)
```

## 12.5. Depurador de Python

El depurador o **debugger** se emplea para identificar y corregir errores en el código. En lugar de utilizar `print()` para ver qué sucede a cada rato, podemos usar el depurador de Python, *pdb*. Por ejemplo:

```python
import pdb

x = [1,2,3]
z = 2
y = 1

resultado1 = z + y

# Al añadir este depurador, podemos introducir las variables que se hayan declarado 
# con la intención de ver el tipo incluso podemos realizar operaciones en ella,
# para ver si el resultado es el esperado o no.
# Una vez que hemos visto posibles casos y los fallos, pulsamos "q" para salir 
# del depurador

pdb.set_trace()

resultado2 = y + x # ERROR
```

## 12.6. Expresiones regulares

En esta sección, exploraremos expresiones regulares en Python para manipular y buscar patrones en texto.

### 12.6.1. Búsqueda y manipulación de patrones

Primero, aprenderemos cómo buscar y manipular patrones específicos en cadenas de texto.

```python
import re

texto = "El número del agente es 111-111-1111"
patron = "número"

# Localiza la palabra y muestra el índice desde donde empieza hasta donde acaba
busqueda = re.search(patron,texto)

# Muestra el índice de inicio de la palabra
print(busqueda.start())

# Muestra el índice de finalización de la palabra
print(busqueda.end())

# Si queremos encontrar todas las mismas palabras y no solo una, utilizamos findall
texto2 = "Mi número favorito es el número 8"
busqueda2 = re.findall("número",texto2)

# Para ver en qué índice se encuentra la palabra repetida varias veces
print("La palabra 'número' está en los siguientes índices:")

for palabra in re.finditer('número',texto2):

    print(f"\t{palabra.span()}")

# Para mostrar la palabra en vez del índice
print("\nLa palabra 'número' está en los siguientes índices:")

for palabra in re.finditer('número',texto2):

    print(f"\t{palabra.group()} -> {palabra.span()}")
```

### 12.6.2. Patrones generales

A continuación, exploraremos cómo encontrar patrones más generales en texto.

```python
import re

texto = "Mi número de teléfono es 11 11 11 111"

# Importante usar la 'r' para indicar a Python que es un patrón raw
numero = re.search(r"\d{2} \d{2} \d{2} \d{3}",texto)
print(numero.group())

# Para extraer áreas concretas del patrón, podemos utilizar grupos
numero_grupos = re.compile(r"(\d{2}) (\d{2}) (\d{2}) (\d{3})")
resultado = re.search(numero_grupos,texto)

# Podemos acceder a un índice específico del grupo
print(resultado.group(4))
```

### 12.6.3. Patrones de palabras

Finalmente, nos centraremos en encontrar patrones de palabras específicas en un texto.

```python
import re

texto = "Tengo una coneja que se llama Misifu"

busq1 = re.search(r'coneja|perro',texto)
print(busq1.group())

texto2 = "Tengo un perro que se llama Tom"

busq2 = re.search(r'coneja|perro',texto2)
print(busq2.group())

texto3 = "The cat in the hat sat there"

# Encontrar palabras que terminen con 'at'
terminadas_at = re.findall(r'.at',texto3)
print(terminadas_at)

# Exclusión de caracteres específicos
phrase = "there are 3 numbers 34 inside 5 this sentence."
print(re.findall(r'[^\\d]+',phrase))

# Eliminar signos de puntuación
test_phrase = """This is a string! But it has punctuation. How can we remove it?"""
clean = ' '.join(re.findall('[^!.? ]+',test_phrase))
print(clean)

# Encontrar palabras específicas que comienzan y terminan con ciertos patrones
text = 'Hello, would you like some catfish?'
texttwo = "Hello, would you like to take a catnap?"
re.search(r'cat(fish|nap|claw)',text)
re.search(r'cat(fish|nap|claw)',texttwo)
```

## 12.7. Cronometrar el tiempo de ejecución de una función

Para evaluar la eficiencia de nuestro código, podemos medir el tiempo que una función tarda en ejecutar una acción específica. Por ejemplo:

```python
import time

def func_uno(n):

    return [str(num) for num in range(n)]

def func_dos(n):

    return list(map(str, range(n)))

# Paso 1: Registrar el tiempo de inicio
start_time = time.time()

# Paso 2: Ejecutar el código que queremos cronometrar
result = func_uno(1000000)

# Paso 3: Calcular el tiempo total de ejecución
end_time = time.time() - start_time
print(end_time)
```

En el código anterior, ambas funciones dan un resultado muy similar, por lo que es difícil ver una diferencia real. Sin embargo, podemos importar la biblioteca *timeit*, que permite realizar mediciones más precisas con un número de repeticiones y parámetros que podemos asignar. Por ejemplo:

```python
import timeit

# Preparación para la primera función
setup = '''
def func_uno(n):
    return [str(num) for num in range(n)]
'''

# Declaración
stmt = 'func_uno(100)'

# Ejecución del cronometraje
print(timeit.timeit(stmt, setup, number=100000))

# Hacemos lo mismo para la segunda función
setup2 = '''
def func_dos(n):
    return list(map(str, range(n)))
'''

stmt2 = 'func_dos(100)'

print(timeit.timeit(stmt2, setup2, number=100000))
```

Es importante mencionar que Jupyter permite utilizar **funciones mágicas** (las funciones mágicas de Jupyter se activan con dos signos de porcentaje al comienzo del bloque de código), una de ellas es la función *timeit*:

```python
%%timeit
func_uno(100)
```

## 12.8. Comprimir y descomprimir archivos

Aquí tienes un ejemplo de cómo comprimir y descomprimir archivos:

```python
import zipfile

# Creación de archivos de prueba
f = open("nuevo_archivo.txt",'w+')
f.write("Esto es solo un ejemplo de introducción de texto")
f.close()

f = open("nuevo_archivo2.txt",'w+')
f.write("Un poquito más de texto")
f.close()

# Creación del archivo zip
archivo_comprimido = zipfile.ZipFile('comprimido_1.zip','w')

# Añadir archivos al zip
archivo_comprimido.write("nuevo_archivo.txt", compress_type=zipfile.ZIP_DEFLATED)
archivo_comprimido.write('nuevo_archivo2.txt', compress_type=zipfile.ZIP_DEFLATED)

# Cerrar el archivo zip
archivo_comprimido.close()

# Extraer archivos de un archivo zip
zip_obj = zipfile.ZipFile('comprimido_1.zip', 'r')
zip_obj.extractall("contenido_extraido")
```

# 13. Trabajar con ficheros CSV

Los archivos CSV (Comma Separated Values) son un tipo de formato que utilizan Excel y otros programas de bases de datos. Son útiles para la manipulación de datos de un fichero, pero sólo contienen el contenido en crudo, por lo que no podemos obtener imágenes, macros, etc., solo los datos.

En Python, trabajaremos con el módulo `csv` incluido en la biblioteca estándar. Otras bibliotecas a considerar para la manipulación de datos en Python serían Pandas, Openpyxl o la API de Google Sheets para Python.

```python
import csv

# Abrimos el fichero
datos = open('example.csv',encoding = 'utf-8')

# csv.reader
csv_datos = csv.reader(datos)

# Convertimos los datos a una lista
lineas_datos = list(csv_datos)

correos = []

for linea in lineas_datos[1:]:
	if linea[3] not in correos:
		correos.append(linea[3])

for numero, correo in enumerate(correos):
	print(f"{numero} : {correo}")
```

Ahora vamos a ver cómo podemos escribir en un archivo CSV:

```python
# Creamos un archivo CSV
archivo_salida = open('fichero_prueba.csv', mode = 'w', newline = '')

# "delimiter" es un delimitador o separador, separa una columna de otra
# cuando encuentra una coma (',')
csv_escribir = csv.writer(archivo_salida, delimiter = ',')

csv_escribir.writerow(['a', 'b', 'c'])
csv_escribir.writerows([['1', '2', '3'],['4', '5', '6']])

# Cerramos el archivo CSV
archivo_salida.close()

# Añadimos información al final del archivo
f = open('fichero_prueba.csv', mode = 'a', newline = '')
csv_writer = csv.writer(f)

csv_writer.writerow(['Nombre', 'Apellido', 'Correo'])
csv_writer.writerows([['Daniel', 'BC', 'bsjhcjhs@gmail.com'], 
						['Clara', 'RA', 'jsasdjb@gmail.com']])

f.close()
```

# 14. Trabajar con ficheros JSON

Para trabajar con ficheros JSON, importamos la biblioteca `json`.

```python
import json

# Creamos una variable de tipo JSON en Python
json_string = '{"Nombre":"Antonio", "Apellidos":"Adrian"}'
obj = json.loads(json_string)

print(f"Nombre: {obj['Nombre']} \nApellidos: {obj['Apellidos']}")
```

Python incluso permite cargar ficheros JSON directamente desde una URL:

```python
import requests

r = requests.get("url")

print(r.json())
```