---
description: Realizado por Daniel Bazo Correa.
---

<div align="justify">

# Python

## Bibliografía

* [Python Docs](https://docs.python.org/3/)
* [Python Bootcamps Udemy](https://www.udemy.com/course/complete-python-bootcamp/)

## 0. Utilidades

### 0.1. Linea de comandos

Comandos útiles a la hora de utilizar el terminal. Tener en cuenta que los comandos pueden variar según el sistema operativo:

| Comando                  | Función                                                                                       |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| `pwd`                    | Muestra el directorio actual                                                                  |
| `ls`                     | Muestra todos los archivos y carpetas que hay en ese directorio                               |
| `cd "nombre_lugar_a_ir"` | Permite ir a la carpeta con el nombre insertado                                               |
| `clear`                  | Permite limpiar el terminal                                                                   |
| `cd ...`                 | Permite llevarnos a nuestro Home del sistema (Carpeta Usuario y Carpeta de acceso compartido) |
| `cmd + shift + p`        | Abrir un cuaderno Jupyter en Visual Studio                                                    |
| `shift + tab`            | Permite ver la documentación de una función, método... dentro de Jupyter                      |

En el caso de estar utilizando Anaconda en Linux:

| Comando                                                              | Función                                                                                                                              |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `anaconda-navigator`                                                 | Para abrir el navegador de Anaconda desde el terminal de Linux                                                                       |
| `cd /home/"usuario"/anaconda3/bin + ./jupyter-notebook --allow-root` | En el caso de que el navegador de Anaconda de problemas al abrir el cuaderno Jupyter, podemos abrirlo directamente sin usar Anaconda |

## 1. Objetos y estructura de datos básica

### 1.1. Tipos de datos fundamentales

| Tipo de datos                                                      | Palabra reservada | Ejemplos                             |
| ------------------------------------------------------------------ | ----------------- | ------------------------------------ |
| Números enteros                                                    | int               | 3, 300, 200                          |
| Números con coma flotante                                          | float             | 2.3, 4.6, 100.0                      |
| Strings                                                            | str               | "Hola", "Hola muy buenas", "2000"    |
| Listas                                                             | list              | \[ 10, "hello", 200.3]               |
| Diccionarios                                                       | dict              | { "edad" : "20", "nombre" : "Dani" } |
| Secuencia de objetos ordenada y que no se puede modificar o Tuples | tup               | ( 10, "hello", 200.3 )               |
| Colección de objetos únicos desordenada o Sets                     | set               | { "a", "b" }                         |
| Indicador de valor lógico o Boleanos                               | bool              | True o False                         |

### 1.2. Operaciones con números

| Operador            | Función                                                                                                  |
| ------------------- | -------------------------------------------------------------------------------------------------------- |
| +, -, \*, /, %      | suma, resta, producto, división y módulo (devuelve el resto de la división), respectivamente.            |
| `numero = -x`       | Python permite mostrar números negativos.                                                                |
| `abs(numero)`       | Valor absoluto del numero.                                                                               |
| `pow(x ,y) = x**y`  | $$x^y$$.                                                                                                 |
| `max(x, y)`         | Me muestra el mayor número de los que le paso. El contrario sería → `min(…)`.                            |
| `round(math.pi, 2)` | Redondear números con unos decimales especificados. Por ejemplo, redondear el numero pi con 2 decimales. |
| `floor(x)`          | Redondea las unidades hacia abajo. Necesita → `import math`                                              |
| `ceil(x)`           | Redondea las unidades hacia arriba. Necesita → `import math`                                             |
| `math.sqrt(x)`      | Devuelve la raíz cuadrada, necesita importar la librería→ `import math`                                  |
| `math.pi`           | Valor numérico de Pi, necesita importar la librería → `import math`                                      |
| `hex(512)`          | Convertir números a hexadecimal.                                                                         |
| `bin(1234)`         | Convertir números a binario.                                                                             |

### 1.3. Asignación de variables

Reglas a seguir a la hora de crear variables:

* Los nombres no pueden empezar con números.
* No puede haber espacios en el nombre de la variable.
* No se pueden usar los siguientes símbolos: `: ''' <> / , ? | \ ( ) ! @ # $ % ^ & * ~ - +`

Es considerado como buena práctica usar nombres de variables en minúsculas.

Python usa _**Dynamic Typing**_, es decir, no hace falta indicar el tipo de dato (int, double, ...) ya que dependiendo del valor que se le asigne lo interpretará acorde al dato. Podríamos por ejemplo crear una variable que contenga un tipo de dato y posteriormente en el código asignarle otro tipo de datos:

```python
mis_perros = 2
mis_perros = [ "Pixel" , "One" ]
```

Al escribir **`type(variable)`** Python nos muestra el tipo (int, string, bool...) de la variable.

### 1.4. Imprimir por pantalla

La función empleada para imprimir en pantalla es **`print()`**:

```python
print("Esto es una prueba")
```

Podemos concatenar variables que contienen strings o métodos/funciones que devuelvan un valor utilizando el operador **+,** por ejemplo:

```python
char_name = "Daniel"
char_age = 19

print("Yo me llamo " + char_name + " y tengo " + str(char_age) + " años.")
```

El procedimiento anterior no parece muy eficiente. Por ello, Python permite darle formato (convertir la expresión de un objeto para que pueda ser impreso por pantalla sin modificar su tipo) a la función `print()` utilizando la letra `f` después del primer paréntesis de la función `print()` . Así, mediante llaves `{}` podemos colocar las funciones, variables o cualquier elemento que queremos mostrar por pantalla. Esto es válido a partir de la versión de Python 3. Aplicando este formato al ejemplo anterior, el resultado sería el siguiente:

```python
char_name = "Daniel"
char_age = 19

print(f"Yo me llamo {char_name} y tengo {char_age} años")
```

### 1.5. String

Definimos a un string como una cadena de caracteres, por ejemplo:

```python
frase = "Hola buenas"

# Muestra el caracter 'H'
print("El primer caracter de mi string es " + frase[0])

mis_animales=["Misifu" , "One"]
print(f"Mi conejo se llama {mis_animales[0]} y mi gato {mis_animales[1]}")
```

Al igual que las listas, el índice de una variable de tipo string empieza en 0 pero con la diferencias de ser inmutables por lo que no podemos utilizar el indexado con el fin de modificar un elemento individual del string.

#### 1.5.1. Funciones

Utilizaremos la palabra “variable” en referencia a una variable de tipo string. Algunas de las funciones a poder realizar con variables de tipo string son:

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

Ejemplo de localización y conteo de caracteres en un string:

```python
diccionario_caracteres = {}

def contador(frase):

	frase = frase.lower()

	for letra in frase:

		if letra in diccionario_caracteres:

			diccionario_caracteres[letra] += 1

		else:

			diccionario_caracteres[letra] = 1

s = input("Introduce una frase para contar los caracteres: ")
contador(s)

for llaves in diccionario_caracteres.keys():

	print(f"El caracter {llaves} aparece {diccionario_caracteres[llaves]}")

s.count('a')
```

#### 1.5.2. Formato impresión por pantalla

Si queremos mostrar un dato de tipo float (número con coma flotante) pero con una cantidad determinada de decimales podemos especificarlo con el siguiente formato:

`{valor_float:.precision}`

```python
pi = math.pi
print(f"El número pi con 5 decimales es: {pi:.5}")
```

### 1.6. Listas

Las listas son una secuencia ordenada y mutable la cual puede almacenar elementos de manera dinámica además de poder almacenar elementos de diferente tipo. Que una lista sea ordenada conlleva a tener un índice por cada posición siendo el índice de la posición inicial el 0. El término de mutable hace referencia a que los elementos almacenados en la lista pueden ser modificados a lo largo del programa. Por último, que sea dinámico provoca que lista no tenga un tamaño fijo por lo que este puede ir variando también a lo largo del código. Por ejemplo:

```python
lista_amigos = ["Jorge", "Fran", "Ricardo"]
```

Incluso podemos inicializar una lista sin valores:

```python
lista = []
```

Para acceder a los elementos de la lista podemos seguir el código siguiente:

```python
print(f"El amigo que está en la misma UNI que yo es {lista_amigos[0]}")

# Al indicar el índice [-1] empezaría por el índice final, en este caso Ricardo
print(f"Mi amigo del pueblo es {lista_amigos[-1]}")

# Seleccionamos un rango
print(lista_amigos[0:2])

# Mostramos la lista de amigos al completo
print(lista_amigos)
```

#### 1.6.1. Operaciones / Funciones

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

Ejemplo de cómo utilizar bucles **`for`** (se verán con mayor detalle en adelante) directamente en una lista (más eficiente que un bucle **`for`** común):

```python
mi_lista = [letra for letra in "Hola"]

# Podríamos utilizar rangos y operaciones
mi_lista = [numero ** 2 for numero in range(0,20,2)]

celcius = [0,10,20,34.5]

fahrenheit = [((9/5)*temp + 32) for temp in celcius]

# Incluso añadir condiciones
mi_lista = [numero ** 2 for numero in range(0,15,2) if numero % 2 == 0]
```

#### 1.6.2. Listas en 2D (matrices)

Ejemplo de como hacer una lista dentro de otra lista creando una especie de malla o matriz:

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

Numpy y Pandas son librerías muy útiles para manipular datos y realizar operaciones con datos, entre ellas, matrices.

### 1.7. Diccionarios

Un diccionario es una colección de datos no ordenada, mutable e indexada. En Python, los diccionarios están escritos con corchetes y cuentan con **claves** (**keys**) y **valores** (**values**). Cada clave tiene que estar asociado a un valor único. Por ejemplo:

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

En caso de buscar un valor de clave no encontrado en un diccionario podemos utilizar la función **`get()`** permitiendo mostrar un texto en caso de error:

```jsx
clave = "Daniel"
conversion_meses.get(clave, f"La key {clave} no esta en el diccionario")
```

#### 1.7.1. Funciones

| Función                | Definición                                           |
| ---------------------- | ---------------------------------------------------- |
| `diccionario.items()`  | Permite obtener la clave y el valor del diccionario. |
| `diccionario.keys()`   | Permite obtener solo la clave del diccionario.       |
| `diccionario.values()` | Permite obtener solo el valor del diccionario.       |

También se admite introducir otra clave dentro de una clave, ejemplo:

```python
diccionario = {"k3":{'insideKey':100}}
```

Para acceder sería:

```python
diccionario["k3"]['insideKey']
```

Ejemplo de cómo realizar iteraciones en llaves, valores y objetos de un diccionario:

```python
# Realizar iteraciones en llaves, valores y objetos de un diccionario
d = {'k1':1,'k2':2}

for llaves in d.keys():

	print(llaves)

for valores in d.values():
	
	print(valores)

for objeto in d.items():
	
	print(objeto)
```

Podemos combinar las listas con los diccionarios para crear estructuras de datos complejas, por ejemplo:

```python
clientes = [
	{"nombre": "Daniel", "animales": ["Pakito", "Pakon", "Pakonazo"]},
	{"nombre": "Clemencia", "animales": ["Rodolfo"]},
	{"nombre": "Carolina"}
]

for cliente in clientes:

	print(f"{cliente['nombre']} tiene: {cliente.get('animales', 'No tiene animales')}")
```

### 1.8. Tuples

Los tuples son similares a las listas con la principal diferencia de que los elementos que almacena son inmutables, es decir, no pueden sufrir modificaciones. Una de las ventajas principales de los tuples es que suelen ser más rápidos de iterar sobre ellos en comparación con las listas. Por ejemplo:

```python
# Este es mi tuple, recordar que una vez creado no se puede modificar
coordenadas = (4, 5)

print(f"Coordenada completa {coordenadas}" + str(coordenadas))
print(f"Primera coordenada {coordenadas[0]} y la segunda coordenada {coordenadas[1]}")
```

#### 1.8.1. Funciones

| Función           | Definición                                                                                      |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| `tuples.count(x)` | Devuelve el número de veces que se repite en el tuple la ‘x’ siendo este un número, string, ... |
| `tuples.index(x)` | Devuelve el primer índice donde se encuentra ‘x’, siendo este un número, string, ...            |

También se puede crear una lista de tuples, por ejemplo:

```python
lista_tuples = [(1,2) , (3,4) , (5,6)]
print(f"Mi lista de tuples es {lista_tuples}")
```

### 1.9. Sets

Un set es una colección sin orden compuesto por elementos únicos, es decir, solo puede haber una representación del mismo objeto. Ejemplo:

```python
# Para inicializar un set a cero
mi_set = set()

# Se añade el 1 
mi_set.add(1) 

# No se vuelve a añadir otro 1 pues cada objeto es único e irrepetible
# Por lo que no añadirá nada
mi_set.add(1) 

mi_nuevo_set = {'a', 'b', 'c'}
```

#### 1.9.1 Funciones

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

### 1.10. Bool

Operadores que permiten transmitir declaraciones de verdadero (**True**) o falso (**False**). Los operadores booleanos son muy útiles en el control de flujo y lógica. Veremos diferentes casos de usos en los ejemplos siguientes.

### 1.11. Introducción de datos

Existe la posibilidad de obtener información introducida por el usuario con la función **`input(...)`**. Tener en cuenta que la función `input()` transforma todo el contenido pasado a tipo string, esto es importante si posteriormente necesitamos manipular datos con un tipo de dato concreto. Por ejemplo:

```python
*# Variable name se queda con el input*
nombre = input("Introduce tu nombre: ")
edad = input("Introduce tu edad: ")

print("\n\t- DATOS DEL USUARIO - \n")
print(f"Nombre: {nombre}")
print(f"Edad: {edad}")
```

Para convertir un input en un número y no como un string, tenemos que realizar una conversión de tipo de dato. Este procedimiento recibe el nombre de “**casting**”, por ejemplo:

```python
# Hacemos un casting (conversión) de string a float
numero = float(input("Introduce un numero: "))
```

### 1.12. Manejo de archivos

Podemos abrir un fichero usando la función **`open()`**:

```python
file = open(dirección_del_fichero)
```

Python permite asignar diferentes permisos (escritura/lectura/ambas...) al fichero, algunos de estos permisos son:

| Permiso | Definición                                                                   |
| ------- | ---------------------------------------------------------------------------- |
| r       | Solo lectura.                                                                |
| w       | Solo escritura, reescribirá los archivos existentes o creará uno nuevo.      |
| a       | Para añadir información al final del archivo.                                |
| r+      | Lectura y escritura.                                                         |
| w+      | Escritura y lectura, reescribirá los archivos existentes o creará uno nuevo. |
| wb      | Modo archivo, escritura y binario.                                           |

#### 1.12.1. Lectura de archivos

Para poder leer un fichero podemos utilizar algunas funciones como:

| Función       | Definición                                                        |
| ------------- | ----------------------------------------------------------------- |
| `readable()`  | Devuelve un booleano para saber si se puede leer o no el fichero. |
| `read()`      | Muestra toda la información del fichero.                          |
| `readline()`  | Lee la primera línea del fichero.                                 |
| `readlines()` | Lee todas las líneas del fichero y las inserta en una lista.      |

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

#### 1.12.2. Escritura de archivos

Un ejemplo de cómo escribir en un fichero sería:

```python
nombre_fic = input("Nombre del fichero: ")

fichero = open(nombre_fic,"a") *# Voy a añadir texto al final*

nuevo_empleado = input("Nombre del nuevo empleado: ")
funcion_empleado = input(f"Puesto del empleado {nuevo_empleado}: ")

fichero.write("\\n" + nuevo_empleado + " - " + funcion_empleado)

fichero.close()
```

## 2. Operadores

### 2.1. Operadores de comparación

Además de poder comparar números también podemos comparar string, distinguiendo entre ellos mayúsculas y minúsculas.

| Expresión | Definición                |
| --------- | ------------------------- |
| A == B    | A es igual a B.           |
| A != B    | A es distinto que B.      |
| A < B     | A es menor que B.         |
| A <= B    | A es menor o igual que B. |
| A > B     | A es mayor que B.         |
| A >= B    | A es mayor o igual que B. |

### 2.2. Operadores lógicos

Podemos utilizar operadores lógicos para combinarlos con los operadores de comparación. Los operadores lógicos son:

| Expresión | Definición                                                                                                                 |
| --------- | -------------------------------------------------------------------------------------------------------------------------- |
| `and`     | Todas las condiciones han de ser verdaderas para que sea True, si una de las condiciones es False el resultado será False. |
| `or`      | Basta con que una de las condiciones sea True.                                                                             |
| `not`     | Sirve para negar la condición.                                                                                             |

### 2.3. Operadores útiles

Cambiar el orden de manera aleatoria de una lista:

```python
import random

mi_lista = [1,2,3,4,5,6,7,8,9,10]

# No devuelve nada, se baraja de manera aleatoria en el mismo lugar
random.shuffle(mi_lista) 
```

Obtener un número aleatorio de un rango establecido:

```python
import random

# Importamos de la libreria random la función randint
from random import randint

randint(0,100)
```

## 3. Declaraciones

### 3.1. Declaraciones if , elif y else

Utilizamos las declaraciones `if`, `elif` o `else` para comprobar si se cumplen con las condiciones necesarias para ejecutar una determinada parte del código.

Sintaxis de una declaración del tipo `if`:

```python
if condicion:
	
	# Codigo a ejecutar
```

Sintaxis de una declaración del tipo `if/else`:

```python
if codicion:
	
	# codigo a ejecutar

else:
	
	# si no cumple la condicion del if pasamos al else
```

Sintaxis de una declaración del tipo `if/else` pero con varias condiciones:

```python
if primera_condicion:
	
	# codigo a ejecutar para la primera condicion

elif segunda_condicion:

	# codigo a ejecutar para la segunda condicion

else:
	
	# codigo a ejecutar en el caso de que no se cumple la primera ni la
	# segunda condicion
```

Ejemplo en el que se comprueba con declaraciones `if` y `else` si un elemento se encuentra dentro de una lista:

```python
# Primer ejemplo
numero = 1
lista = [1,2,3]

if numero in lista:
	
	print(f"El numero {numero} se encuentra en la lista")

else:
	
	print(f"El numero {numero} no se encuentra en la lista")

# Segundo ejemplo
d = {'mykey' : 345}

if 345 in d.keys():

	print("El valor se encuntra dentro del diccionario")

else:
	
	print("El valor no se encuntra dentro del diccionario")
```

### 3.2. Bucles

#### 3.2.1. Bucle for

Muchos objetos en Python son iterables, es decir, podemos recorrer cada elemento del objeto. Un ejemplo podría ser recorrer cada elemento que compone una lista o los caracteres que compone un string. Usamos entonces los bucles **`for`** para iterar sobre dichos elementos. Su sintaxis:

```python
for variable_recorre in lugar_a_recorrer:
	
	# codigo a ejecutar
```

Podemos establecer un rango de recorrido para el bucle con la función:

* **`range(x, y, z)`** → Donde ‘x’ es el inicio, ‘y’ es el fin - 1 y ‘z’ es el tamaño de paso.

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

La función **`zip()`** permite asignar un índice a un valor de dos listas diferentes para formar un tuple. Hay que tener en cuenta que si las listas tienen diferentes tamaños, se hará un zip con el máximo de elementos de la lista con menor número de elementos.

* **`zip(x, y, ...)`** → Se puede meter tantas listas como se requieran.

Por ejemplo:

```python
mi_lista1 = [1, 2, 3]
mi_lista2 = ['a', 'b', 'c']
mi_lista3 = [100, 200, 300]

for item in zip(mi_lista1, mi_lista2, mi_lista3):

	print(item)
```

Otros ejemplos de bucles **`for`**:

```python
# Primer ejemplo

mi_lista = [1 ,2 ,3]
i = 0

for elemento_lista in mi_lista:

	print(f"{elemento_lista} ocupa la posicion {i} de la lista")
	i += 1

# Segundo ejemplo

# "letra" coge cada caracter del string
for letra in "Hola muy buenas": 
	
	print(letra )

# Tercer ejemplo

# Creamos una lista de tuples
mi_lista = [(1,2) , (3,4) , (5,6)]

for a, b in mi_lista:
	
	print(f"X: {a} \n\tY: {b}")

# Cuarto ejemplo

# Para obtener los elementos de uns tring en forma de tuples
# Utilizamos la función "enumerate" ya que devuelve el índice y el elemento

word = "abcde"

for elemento in enumerate(word):
	
	print(elemento)
```

#### 3.2.2. Bucle while

El bucle **`while`** realiza un bucle mientras se cumpla la condición. Su sintaxis:

```python
while condicion:

	# codigo a ejecutar
```

También, existe la condición de combinarlo con un **`else`**:

```python
while condicion:

	# codigo a ejecutar

else:
	
	# codigo a ejecutar en el caso de que la condicion del while no se cumpla
```

### 3.3. Break, continue y pass

`break`→ Rompe con el bucle que se esté ejecutando en ese momento, ejemplo:

```python
mi_string = "Daniel"

# Es este bucle, al encontrar la letra 'a' saldríamos del bucle
for letra in mi_string:

	if letra == a: 
		
		break
	
	print(letra)
```

`continue`→ Va a la parte superior del bucle de cierre más cercano, ejemplo:

```python
mi_string = "Daniel"

# En este bucle, al encontrar la letra 'a' se pasará al siguiente caracter sin mostrar
# la 'a', es decir, se salta el "print(letra)"

for letra in mi_string:

	if letra == a:
		
		continue

	print(letra)
```

`pass`→ No hace nada del bucle para evitar errores.

## 4. Métodos y funciones

### 4.1. Métodos

La mejor opción es visitar la página oficial de Python ya que los métodos se actualizan conforme avanzan las versiones de Python.

Web con la documentación→ [https://docs.python.org/](https://docs.python.org/)

### 4.2. Funciones

Las funciones nos permiten crear bloques de código fáciles de ejecutar varias veces sin necesidad de reescribir constantemente el código, así si queremos repetir un mismo proceso (una misma función) podremos implementar una función con el código necesario y realizar llamadas a dicha función cuando sea necesario.

En Python, definimos una función usando la palabra reservada **`def`**, por ejemplo:

```python
def nombre_de_la_funcion():

	# Bloque de codigo a ejecutar dentro de la funcion, tener en cuenta
	# que la funcion solo ejecutará el código que se encuentra tabulado

# Llamada a la función
nombre_de_la_funcion()
```

El nombre de la función se rige por convención con el formato de _**Snake casing**_. Este formato consiste en utilizar palabras en minúscula empleando barras bajas entre cada palabra.

Dentro de los paréntesis de la función podemos pasar argumentos o parámetros.

A modo de colocar una descripción de la función podemos utilizar 3 comillas ( ''' ) ya que permiten añadir comentarios en múltiples líneas.

Una función puede devolver un dato, para ello, utilizaremos la palabra reservada **`return`** al finalizar la función junto con el/los dato/s. Este procedimiento permite asignar el valor que devuelve función a una variable cuando se llama a la función.

A continuación veremos un ejemplo de función que utiliza parámetros y devuelve un dato:

```python
import math

# Esta funcion calcula la parte positiva de la ecuacion
def segundo_grado_pos(a, b, c, discriminante):
	
	# Es negativo, numero complejo
	if discriminante < 0: 
	
		discriminante *= -1 # Pasarlo positivo
		parte_real = (-b / (2 * a))
		parte_imag = ((math.sqrt(discriminante)) / (2 * a))
		funcion1 = str(parte_real) + " + " + str(parte_imag) + "i"
	
	else:
		
		funcion1 = ((-b + math.sqrt(discriminante)) / (2 * a))
	
	return funcion1

# Esta funcion calcula la parte negativa de la ecuacion
def segundo_grado_neg(a, b, c, discriminante):
	
	# Es negativo, numero complejo
	if discriminante < 0: 
		
		# Pasarlo positivo
		discriminante *= -1 
		parte_real = (-b / (2 * a))
		parte_imag = ((math.sqrt(discriminante)) / (2 * a))
		funcion2 = str(parte_real) + " - " + str(parte_imag) + "i"
	
	else:

		funcion2 = ((-b - math.sqrt(discriminante)) / (2 * a))
	
	return funcion2

print("Ecuacion segundo grado: ax^2 + bx + c ")
a = float(input("Valor a: "))
b = float(input("Valor b: "))
c = float(input("Valor c: "))

discriminante = (pow(b, 2) - (4 * a * c))

print(f"Positivo: {segundo_grado_pos(a,b,c,discriminante)}")
print(f"Negativo: {segundo_grado_neg(a,b,c,discriminante)}")
```

En los parámetros de las funciones, se puede establecer un valor por defecto. En el caso de no pasar ningún valor a la función, se utilizará el que hay por defecto, por ejemplo:

```python
# "Paquito" sería el valor por defecto en el caso de no introducir ningún valor
def di_hola(name = "Paquito"): 
	
	print(f"Hola {name}")

# Al no pasar ningún valor, mostrará como valor por defecto "Paquito"
di_hola() 
```

#### 4.2.1. Funciones con lógica

Dentro de las funciones podemos incluir bucles, llamadas a otras funciones y más. Algunos ejemplos:

```python
def comprobar_lista(lista):

	lista_par_devolver = set()
	lista_impar_devolver = set()

	for indice in lista:
	
		if indice % 2 == 0:
	
			lista_par_devolver.add(indice)
	
		else:
	
			lista_impar_devolver.add(indice)

	print(f"Lista numeros pares de la lista principal: {lista_par_devolver}")
	print(f"Lista numeros impares de la lista principal: {lista_impar_devolver}")

comprobar_lista([1, 1, 1, 1, 1, 1, 23, 56, 87, 918, 23, 12, 3, 2, 4, 6, 5])
```

Ejemplo de funciones con tuples:

```python
horas_trabajadores = [("Daniel", 22), ("Kike", 20), ("Ricardo", 25)]

def mejor_trabajador(lista):

	maximo = 0
	mejor = ""

	for empleado,horas in horas_trabajadores:
	
		if horas > maximo:
		
			maximo = horas
			mejor = empleado
		
		else:
		
			pass
	
	return (mejor,maximo)

mejor, maximo = mejor_trabajador(horas_trabajadores)

print(f"El mejor trabajador es {mejor} que ha trabajado un total de {maximo} horas")
```

Ahora veremos un ejemplo interesante donde funciones llaman a otras funciones y donde se emplea la función **`shuffle()`** permitiendo ordenar una lista de manera aleatoria en el lugar, es decir, no devuelve nada:

```python
# El juego de la bolita
vasos = [' ','O',' ']

def shuffle_list (mi_lista):

	shuffle(mi_lista)
	return mi_lista

def inicio():

	print("La bolita se encuentra en vaso 2\n")
	print('vaso 1: ')
	print('vaso 2: O')
	print('vaso 3: ')
	print("\nMoviendo la bola por los diferentes vasos...\n")

def operar():

	resultado = int(input("En qué vaso está la bolita?: "))

	while resultado != 1 and resultado != 2 and resultado != 3:

		print("Este vaso no existe")
		resultado = int(input("En qué vaso está la bolita?: "))

	comprobar(resultado)

def comprobar(resultado):

	i = 1

	if vasos[resultado-1] == 'O':

		print("\nHas acertado!!\\n")
		
		for vaso in vasos:
		
			print(f"vaso {i}: {vaso}")
			i += 1
	
	else:
	
		print("\nHas fallado :( \n")
		
		for vaso in vasos:
	
			print(f"vaso {i}: {vaso}")
			i += 1

inicio()
shuffle_list(vasos)
operar()
```

### 4.3. \*Args y \*\*Kwargs

Los **`args`** y los **`kwargs`** representan parámetros (palabras claves) utilizados para obtener números arbitrarios de argumentos al usar funciones sin tener que predefinir un conjunto de parámetros en las llamadas a funciones. Por ejemplo:

```python
# a y b son argumentos posicionales
def mifuncion(a, b):
 
	return sum((a, b)) * 0.05

# el primer argumento se asigna en a y el segundo a b
mifuncion(40,60) 
```

El problema ocurre cuando queremos trabajar con una función, por ejemplo, el del caso anterior pero en vez de emplear 2 números operar con mas. Una de los opciones sería trabajar asignando una gran cantidad de parámetros asignándoles un valor por defecto en el caso de que dicho valor no sea introducido por el usuario, es decir:

```python
# si el usuario no mete un parametro c, este será 0
def mifuncion(a, b, c = 0):

	return sum((a, b, c)) * 0.05
```

Es en estos casos donde utilizaremos **`*args`**, ya que nos permitirá configurar la función para tomar cantidades arbitrarias de argumentos. Por ejemplo:

```python
def mifunction(*args):

	return sum(args) * 0.05
```

**`*args`, permite tratar la entrada como una tupla de parámetros**, ahora puedo pasar tantos argumentos como quiera. Por defecto, Python toma todos los parámetros que se pasan y los configura como una tupla. Tener en cuenta que el termino reservado args está elegido por convención, por lo que puede ser sustituido por cualquier otra palabra.

De forma similar, **Python ofrece una forma de manejar una cantidad arbitraria de argumentos de palabras clave donde en vez de crear una tupla crea un diccionario, para ello usaremos los `kwargs`.** Por ejemplo:

```python
def mifuncion(**kwargs):

	if 'fruta' in kwargs:
	
		print(f"Mi fruta favorita es la {kwargs['fruta']}")
	
	else:
	
		print("No se encontro la fruta")
	
	if 'verduras' in kwargs:
	
		print(f"Mi verdura favorita es la {kwargs['verduras']}")
	
	else:
	
		print("No se encontro la verdura")

mifuncion(fruta = 'manzana', verduras = 'zanahoria')
```

Al igual que el termino `args`, el termino `kwargs` también es escogido por convención así que puede ser sustituido por cualquier otro término. También podremos crear funciones que combinen `*args` con `**kwargs` , por ejemplo:

```python
def mifuncion(*args, **kwargs):

	print(f"Tengo {args[0]} coneja llamada {kwargs['animal']}")

mifuncion(1,2,3,4,fruta = "manzana",verdurra = "zanahoria",animal = "Misifu")
```

### 4.4. Expresiones lambda, funciones map y filter

Este tipo de expresiones son útiles para procesar los datos de una manera avanzada. Primero, hay que tener en cuenta que el orden en el que se pasan los parámetros a la hora de llamar a la función es importante, de lo contrario Python saltará con un error.

**Las expresiones Lambda** son una manera rápida de crear funciones anónimas. Estas funciones anónimas son funciones de un único uso, es decir, se hacen referencia una sola vez y ya no se vuelven a usar.

**La función `map(...)`**, permite mapear una función a cada elemento de una lista con la posibilidad de devolver una nueva lista con los resultados de la función. Lo que devuelve es la posición en memoria, esto se ve fácil ya que los parámetros que admite son la función (primer parámetro) y un iterador (segundo parámetro). Este iterador, es un puntero que apunta a un espacio de memoria. A continuación veremos cómo convertir una función normal a una función Map partiendo del siguiente bloque:

```python
def square(num):

	return pow(num, 2)

mis_nums = [1, 2, 3, 4, 5]
```

Podríamos recorrer con un bucle cada elemento de “mis\_nums” para luego guardarlos en una lista pero en este caso usaremos la función **`map()`** iterando de 2 maneras posibles:

```python
for item in map(square, mis_nums):

	print(item)

# Otra opción
list(map(square, mis_nums))
```

La función **`filter()`** permite filtrar los elementos dependiendo de la función, al igual que la función `map()`, devuelve un iterador. Un ejemplo muy sencillo sería:

```python
def par(num):

	return num % 2 == 0

numeros = [1, 2, 3, 4, 5, 6]

# Me quedo con los elementos pares, filtro los impares
list(filter(par, numeros)) 
```

Ahora que hemos visto las funciones `map()` y `filter()`, podemos ver las expresiones lambda de manera mas sencilla. Como primer ejemplo, cogeremos una función cualquiera para ir convirtiéndola en una función lambda:

```python
def cuadrado(num):

	res = pow(num,2)
	return res

cuadrado(3)
```

Vemos que la función anterior podemos simplificarla. **La simplicidad es el motivo principal de usar funciones lambda**:

```python
def cuadrado(num):

	return pow(num,2)

cuadrado(3)
```

Incluso, podríamos expresarlo en una sola línea:

```python
def cuadrado(num): return pow(num,2)
```

La expresión lambda, se conoce como función anónima por implementar una funcionalidad que es realizada una sola vez. En esta función lambda no emplearemos la palabra reservada `return` ya que asumimos que vamos a devolver algo, incluso podemos asignar a una variable el resultado de la función lambda pero no suele ser lo normal, en cambio, sí la utilizaremos comúnmente juntos con otras funciones como `maps()` o `filter()`, por ejemplo:

```python
# Expresión lambda
lambda num: pow(num,2)

# Expresión lambda asignada a una variable
cuadrado = lambda num: pow(num,2)

# Expresión lambda junto con una función map()
mis_nums = [1,2,3,4,5]
list(map(lambda num: pow(num,2),mis_nums))

# Expresión lambda junto con una función filter()
mis_nums = [1,2,3,4,5]
list(filter(lambda num: num % 2 == 0,mis_nums))
```

Otro ejemplo de función lambda:

```python
people = ['Dr. Christopher Brooks', 'Dr. Kevyn Collins-Thompson',
					'Dr. VG Vinod Vydiswaran', 'Dr. Daniel Romero']

def split_title_and_name(person):

	return person.split()[0] + ' ' + person.split()[-1]

# Opción 1
for person in people:

	print(split_title_and_name(person) == 
				(lambda x: x.split()[0] + ' ' + x.split()[-1])(person))

# Opción 2
list(map(split_title_and_name, people)) ==
list(map(lambda person: person.split()[0] + ' ' + person.split()[-1], people))
```

Tener en cuenta que podemos pasar múltiples argumentos en la expresión lambda.

### 4.5. Declaraciones anidadas (nested statements) y el alcance del código (scope)

Ya hemos tratado con funciones en Python pero es importante comprender como trata Python las variables que creamos. Estas variables se almacenan y estos tienen un alcance. Dicho alcance determina la visibilidad de la variable a otras partes del código. Por ejemplo:

```python
x = 25

def printer():

	x = 50
	return x

# Devuelve 25
print(x) 

# Devuelve 50
print(printer()) 
```

En el ejemplo anterior vemos que es interesante ver la interpretación que hace Python con las variables, ver el por qué la reasignación de la función `printer()` no afecta a la asignación que aparece antes ("x = 25"), teniendo ambos el mismo nombre de variable (x). Esto viene por la idea del Scope o Alcance, el cual permite a Python comprender que tiene un conjunto de reglas para decidir a que variables hace referencia en cada parte del código. Esas reglas se acortan por las siglas de la regla LEGB:

* L, espacio de nombre local → nombres asignados de alguna manera dentro de una función (def o lambda) y no se declara de manera global en dicha función.
* E, función de encierro local → nombres en el ámbito local de cualquier y toda función de encierro (def o lambda), de interior a exterior.
* G, global → nombres asignados en el nivel superior de un archivo de módulo, o declarados globales en un def dentro del archivo.
* B, built-in → nombres pre-asignados en el módulo de nombres incorporado: open, range, SyntaxError

Este es el orden en el que Python buscará las variables, ejemplo:

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

La función anterior mostrará primero la variable local Carlitos, si la comentásemos cogería la variable de encierro local Daniel y si la comentásemos también cogería la variable global Esto es un string global.

Ahora veremos que ocurre al reasignar una variable global dentro de una función, ya que si hacemos una reasignación dentro de dicha función, por el alcance (Scope), el valor de reasignación solo se mantiene dentro de la función, una vez que salimos de ella el valor de la variable mantendrá el mismo valor que se le asignó al comienzo, para ello usaremos la palabra reservada global, como en el siguiente ejemplo:

```python
x = 50

def prueba():
	
	# Cogemos del nivel global la variable x para llevarlo al nivel local
	global x
 
	# y asi poder reasignar su valor
	print(f"Valor de x antes {x}")
	
	x = 200
	print(f"Valor de x despues {x}")

prueba()
print(f"Valor de x fuera {x}")
```

Pero, hay que evitar usar la palabra clave global a menos que sea absolutamente necesario. Sería más correcto el devolver un objeto y luego asignarlo a la variable, por ser mucho mas seguro. Así evitaremos sobrescribir la palabra clave global dentro de una función sin siquiera saberlo.

## 5. Validación de datos

A la hora de realizar funciones que tomen valores de entrada (inputs) del usuario, es recomendable verificar esas entradas para asegurar que el valor introducido sea correcto.

También tener en cuenta que la función `input()` puede ser un poco complicada porque esta espera la interacción del usuario, lo que significa que si se ejecuta accidentalmente 2 veces, el programa puede atascarse esperando una respuesta que no vemos. En el caso de que suceda, en Jupyter deberemos reiniciar el kernel teniendo en cuenta que todas las variables anteriores se borrarán, teniendo que ejecutarlas de nuevo (Jupyter ofrece una opción para ello).

Lo más cómodo a la hora de validar datos es utilizar bucles while para pedir al usuario que ingrese un valor repetidamente cuando este no es válido, por ejemplo:

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

En el caso de querer limpiar la consola cuando el usuario introduce valores incorrectos, podemos importar y usar la biblioteca siguiente:

* `from IPython.display import clear_output` → Con esta biblioteca usaríamos la función → `clear_output()`.

## 6. Programación Orientada a Objetos (POO)

### 6.1. Introducción

La programación orientada a objetos (POO) permite crear objetos propios que tienen métodos y atributos. Estos métodos actúan como funciones que usan información sobre el objeto y también sobre el objeto mismo (`self`) o cambiar el objeto actual. La programación orientada a objetos permite crear código que es repetible y organizado, es decir, crear programas flexibles. Normalmente, al usar bibliotecas externas, estas suelen emplear la programación orientada a objetos. Un ejemplo sencillo para ver la sintaxis puede ser el siguiente:

```python
# Las clases por convención son palabras en mayúsculas
class NombreDeClase():

	# __init__ , permite crear una instancia del objeto actual
	# donde el parametro1 y el parametro2 son parametros que definen al objeto
	# y que Python espera a que le pasemos
	# Lo que hacemos es conectar el parametro con el uso de ese para vincularlo
	# al objeto
	
	# Metodo 1
	def __init__(self,parametro1,parametro2): 
	
		self.parametro1 = parametro1
		self.parametro2 = parametro2

	# Luego podemos tener otros metodos dentro de la misma clase
	# Se le pasa el self para que Python reconozca que no es solo una funcion,
	# sino que se trata de un metodo

	# Método 2
	def algun_metodo(self): 

		# Se realiza alguna accion dentro de la funcion
	
# Cuando una funcion se encuentra dentro de una clase
# pasa de llamarse funcion a llamarse método
```

### 6.2. Atributos y clases

La clase es un plano que define la naturaleza de un objeto. Podemos construir un objeto en una instancia, esta instancia es un objeto especifico creado a partir de una clase en particular. Ejemplo de una clase junto con sus atributos y sus métodos:

```python
# Variable Global
max_personas = 4 

class Coche():

	# __init__ es un metodo especial, invocado cada vez que creemos una instancia 
	# de la clase, empezaremos siempre con la palabra clave "self" que conecta este 
	# metodo con la instancia de la clase y nos permite referirnos a si mismo, 
	# luego pasamos el resto de atributos.
	# En c++ ese self se hace de manera oculta, en Python hay que especificar el self

	def __init__(self,marca,modelo,mejorado,acceso_coche):
	
		self.marca = marca
		self.modelo = modelo
		self.mejorado = mejorado
		self.acceso_coche = acceso_coche

	lista_personas = []
	mejorado = False

# No tiene por qué tener el mismo nombre de variable que los parametros de la clase
marca = input("Marca del coche: ")
modelo = input("Modelo del coche: ")
m = input("Mejoras incluidas? (S: si , N: no): " ).upper()

while m != 'S' and m!= 'N':

	m = input("Mejoras incluidas? (S: si , N: no): " ).upper()

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

### 6.3. Atributos de la clase objeto y métodos

Los atributos de los objetos de clase van a ser los mismos para cualquier instancia de la clase y los métodos son acciones que realizamos con el objeto que hemos creado. Ejemplo:

```python
class Perro():

	# Atributo del objeto de la clase Perro
	# Es igual para cualquier instancia de la clase, vemos que cualquier perro
	# independientemente de sus caracteristicas es un mamifero
	# Es como sacar la esencia del objeto
	especie = "mamifero"

	def __init__(self,raza,nombre,edad):
		
		# Los atributos no se ejecutan, son características del objeto
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

### 6.4. Herencia y el polimorfismo

La herencia es una manera de formar nuevas clases usando clases ya definidas. La principal ventaja de la herencia es reutilizar el código para así reducir la complejidad del programa. Ejemplo de herencia:

```python
# La clase principal se denomina **clase base**
class Animal():

	def __init__(self):

		print("Se ha creado el animal")
	
	def quien_soy(self):
		
		print("Soy un animal")
	
	def comer(self):
	
		print("Estoy comiendo")

# Entonces, por ejemplo, si quiero crear otra instancia de la clase "*Animal*",
# Por ejemplo la clase Perro, esta comparte características de la clase Animal
# por lo que podemos utilizar el código anterior en la nueva clase, esto es la Herencia

# La clase "Perro" se denomina "clase derivada"

#  Así es como se realiza la herencia
class Perro(Animal):
 
	def __init__(self):
		
		Animal.__init__(self)
	
	# También podemos sobrescrbir los métodos de la clase base
	# Si quitaramos este método, se ejecutaría el metodo de la clase base

	def quien_soy(self):

		print("Soy un perro")

	# También podemos añadir nuevos metodos a la clase derivada
	def sonido(self):

		print("El perro hace: Woof!")

mi_perro = Perro()
```

El polimorfismo es la forma en que diferentes clases de objetos pueden compartir el mismo nombre de método y luego poder llamar a esos métodos desde el mismo lugar aunque se puedan pasar una variedad de objetos diferentes. Por ejemplo:

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

Una práctica mas común es usar clases abstractas combinadas con herencia. Las clases abstractas son aquellas que no esperan ser instanciadas, están diseñadas para servir como clase base, por ejemplo:

```python
class Animal():

	def __init__(self,nombre):

		self.nombre = nombre

	def sonido(self):

		# La palabra clave "***raise***" se utiliza para plantear una excepción.
		raise NotImplementedError("Subclase debe implementrar este metodo abstracto")

# Herencia
class Dog(Animal): 

	# Si no implementamos el método "*sonido*" saltará el fallo del "*raise*" de 
	# la excepción lo que hay que hacer es en cada clase que derive de la clase 
	# base Animal sobreescribir el método "*sonido*", así caracterizamos cada 
	# clase derivada
	
	def sonido(self):

		return self.nombre + " hace woof!"
```

Uno de los ejemplos mas realistas del polimorfismo podría ser crear una clase base que implemente el método de abrir un fichero en general pero con diferentes clases derivadas que se encarguen de abrir ficheros con formatos específicos.

### 6.5. Métodos especiales

Los métodos especiales nos permiten usar algunas de las operaciones integradas en Python en objetos propios que ha definido el usuario. Por ejemplo:

```python
class Libro():

	def __init__(self,titulo,autor,paginas):

		self.titulo = titulo
		self.autor = autor
		self.paginas = paginas

	# Este metodo permite que si alguna funcion que solicite la representacion
	# de cadenas de caracteres de su clase, devolverá lo que devuelve el método __str__	
	def __str__(self):

		return f"{self.titulo} por {self.autor} con {self.paginas} paginas"

	# Podemos hacer lo mismo para el metodo de longitud
	def __len__(self):
		
		# La longitud será el numero de paginas porque es lo que mas sentido tiene en este 
		# ejemplo, dependiendo de la clase y los atributos del objeto pondremos una cosa
		# u otro
		return self.paginas

	# Permite mostrar un informe cuando borramos una variable
	def __del__(self):

		print("El objeto libro ha sido eliminado")

mi_libro = Libro("Libro de Python","Daniel",100)

# Al utilizar ahora la funcion print, ya no aparecerá un error, lo que hará es
# preguntar al objeto Libro si tiene una representacion en forma de String de si mismo
# devolverá que si ya que tenemos implementado el metodo especial __str__
print(mi_libro)
len(mi_libro)
del mi_libro
```

Existen otros métodos diferentes del ejemplo anterior que se pueden ver en la documentación de Python.

## 7. Módulos y Paquetes

### 7.1. Pip install y PyPi

PIP es el instalador de paquetes de Python para instalar nuevos módulos. Muy utilizado para instalar paquetes de entornos de programación en Anaconda.

PyPi es un repositorio para paquetes Python de código abierto de terceros. Las bibliotecas que hemos estando utilizando hasta ahora son bibliotecas integradas pero podemos utilizar el comando **`pip install`** en el terminal junto con el nombre del paquete que queramos instalar estos. Por ejemplo:

```python
# pip install colorama, en el terminal esta libreria permite utilizar texto de colores
from colorama import init
from colorama import Fore

init()

print(Fore.RED + "Texto de prueba")
```

### 7.2. Módulos y Paquetes

Veremos cómo podemos crear nuestros propios módulos y paquetes incluso cómo personalizarlos. Tener en cuenta que los módulos son solo scripts .py que pueden ser llamados desde otro script .py y los paquetes son una colección de módulos.

Esto es interesante con programas muy largos con la intención de modularizar y dividir el problema en partes mas pequeñas, con la intención de luego crear un paquete.

Ahora veremos un ejemplo donde utilizaremos un programa principal, junto un paquete (paquete78 como ejemplo) el cual cuenta con un sub-paquete, la estructura de este ejemplo sería tal que así:

> Estructura:
>
> * [main.py](http://main.py/)
> * Paquete78 → Carpeta
>   * some\_main\_script.py
>   * [init.py](http://init.py/)
>   * Subpaquetes → Carpeta
>     * mysubscript.py
>     * init.py

Cuando queramos crear paquetes y empecemos a crear una jerarquía de carpetas, tendremos que meter en la carpeta del paquete y en los sub-paquetes el fichero llamado _init_\*.py\* para que Python pueda entender que queremos tratar estos directorios no solo como un directorio normal sino como un paquete real. Este _init.py_ no tiene por qué contener algo.

Programa Principal:

```python
from paquete78 import some_main_script as p
from paquete78.Subpaquetes import mysubscript as s

p.main_report()
s.sub_report()
```

Paquete78 fichero _some\_main\_script_:

```python
def main_report():

	print("Hola soy una funcion dentro de mi script principal")
```

Sub-paquetes, carpeta dentro de la carpeta Paquete78, fichero _mysubscript_:

```python
def sub_report():

	print("Hola soy una funcion dentro de mi subscript")
```

### 7.3. Name y "main"

Partiendo del código siguiente:

```python
if __name__ == "__main__":

	# bloque de codigo a ejecutar
```

La idea detrás de la línea de código anterior es que cuando se está importando funciones desde un módulo, podamos ver cuando un módulo es ejecutado directamente o está importado.

Cuando creamos un módulo en Python, este puede definir funciones, clases y variables. Entonces cuando el interprete ejecuta el módulo directamente y no importado, la variable `name**` se pondrá en valor `main**` en el caso contrario, `name**` se establecerá con el nombre de ese módulo.

Esto es muy empleado para permitir o evitar que se ejecuten partes de código cuando se importen los módulos.

Por ejemplo, partiendo de dos archivos _one79.py_ y _two79.py_, importaremos un fichero al otro:

_one79.py_:

```python
import two79

print(f"Arhivo 1 __name__ establecido a: {__name__}")

if __name__ == "__main__":

	# Ejecuto un bloque de codigo
	print("Archivo 1 ejecutado directamente")

else:

	# Ejecuto un bloque de codigo distinto
	print("Archivo 1 ejecutado como importado a otro modulo")
```

_two79.py_:

```python
import one79 as t

print(f"Arhivo 2 __name__ establecido a: {__name__}")

if __name__ == "__main__":

	# Ejecuto un bloque de codigo
	print("Archivo 2 ejecutado directamente")

else:
	
	# Ejecuto un bloque de codigo distinto
	print("Archivo 2 ejecutado como importado a otro modulo")
```

## 8. Manejo de errores y excepciones

### 8.1. Errores y manejo de excepciones

Podemos usar el manejo de errores en un intento de planificar posibles errores que puedan surgir en nuestro código.

Por ejemplo, un usuario intenta escribir en un fichero que se ha abierto en modo de solo lectura, entonces, si no hay ningún tipo de declaración del error en el código el programa entero parará, por eso, utilizamos el manejo de excepciones, ya que permiten continuar el programa, notificar el error y seguir con el código.

Hay 3 palabras claves para el manejo de errores:

* `try` → Este es el bloque de código que se intentará (puede llevar a un error).
* `except` → Bloque de código que se ejecutará en caso de que haya un error en el bloque de prueba (try).
* `finally` → Un bloque final de código para ser ejecutado independientemente de un error.

Ejemplo:

```python
try:

	f.open("fichero",'w')
	f.write("Linea de prueba")
	# lo mas comun es mostrar diferentes mensajes dependiendo del error introducido

except TypeError:
	
	print("Hubo un problema con el tipo")
	
# Esta excepción se plantea cuando una función del sistema
# devuelve un error relacionado con el sistema,
# incluidos fallos de E/S como "archivo no encontrado" o "disco lleno"
except OSError: 
		
		print("Hubo un error de OSError")

except:

	print("Hubo un fallo en otro tipo de excepciones")

finally:

	print("De todos modos segui ejecutando el codigo")
```

Otro ejemplo donde pediremos constantemente el dato en el caso de que no sea un valor adecuado:

```python
def introducir_entero():

	while True:

		try:

			valor = int(input("Introduce un numero entero: "))

		except:
	
			print("El valor introducido no es un numero")
	
		else:
	
			print(f"El valor {valor} es un valor correcto")
			break;

introducir_entero()
```

Existen mas excepciones implementados en Python que se pueden ver en la documentación en el apartado:

* Library → Exceptions.

### 8.2. Pylint

Vamos a discutir las pruebas unitarias.

A medida que comenzamos a expandir los proyectos con varios archivos o comenzamos a trabajar con un equipo, se vuelve importante tener pruebas en el lugar. De esta forma, al realizar cualquier cambio o actualización en el código, podemos ejecutar estos archivos de prueba para asegurarnos de que el código anterior aún se ejecuta de forma esperada.

Existen diferentes herramientas de testado del código, nos enfocaremos en 2 de ellas:

* Pylint → Esta es una biblioteca que mira el código e informa de posibles problemas.
* Unittest → Esta biblioteca incorporada permite probar sus propios programas y comprobar que está obteniendo los resultados deseados.

Para Pylint ejecutaremos el siguiente código en el terminal:

* pylint nombre\_fichero.py -r y .

### 8.3. Unittest

Con unittest, podemos implementar un script en Python que analice los resultados devueltos y ver si es el resultado esperado. Por ejemplo:

Partiremos de 2 archivos, _cap85a.py_ y _cap85b.py_. _cap85a.py_:

```python
def prueba(texto):

	return texto.capitalize()
```

_cap85b.py_:

```python
import cap85a
import unittest

class Test(unittest.TestCase):

	# Ejemplo de estructura de un test
	def test_1(self):

		texto = 'python'
		resultado = cap85a.prueba(texto)
		self.assertEqual(resultado,'Python')

if __name__ == '__main__':
	
	unittest.main()
```

## 9. Decoradores

Los decoradores en Python permiten decorar una función. Para explicarlo en este contexto, partiremos de un función sencilla:

```python
def funcion_simple():

	# Codigo
	return algo
```

Si tenemos una función sencilla pero ahora queremos añadir nuevas funcionalidades, necesitaríamos añadir más código por lo que podríamos añadir el nuevo código y juntarlo con el código antiguo, esto origina dos problemas:

* Al añadir nuevo código al antiguo podemos tener problemas a la hora de llamar a la función original ya que hemos cambiado su funcionalidad.
* Si creamos otra función donde copiamos el código antiguo mas el nuevo estaríamos creando la función de nuevo, algo que es ineficiente.

Si en un futuro queremos borrar esa funcionalidad tendríamos que reeditar la función, borrarla etc. por lo que sería muy conveniente tener una especie de botón que permita agregar o eliminar la nueva funcionalidad que queramos implementar, aquí es donde entran los decoradores/decorators.

Tenemos que tener en cuenta que las funciones son objetos que se pueden pasar a otros objetos, por ejemplo:

```python
def funcion_saludo():

	return "Hola"

copia = funcion_saludo()

del funcion_saludo # Borramos la funcion_saludo

# Si se ejecuta este código en Jupyter veremos que seguiríamos viendo "Hola"
copia() 
# Lo que hemos hecho es hacer una copia completa de la función a un nuevo objeto
```

Un ejemplo de decorador:

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

Lo que ocurre es que le estoy agregando las líneas de código de nuevo\_decorador a la función funcion\_necesita\_decorador, si comentase @nuevo\_decorador, la función funcion\_necesita\_decorador mostraría únicamente el mensaje que contiene.

Una de las utilidades más usadas de los decoradores son los logger, ya que nos permite escribir en un fichero los resultados de ciertas operaciones, que funciones han sido llamadas o cualquier información que en un futuro resulte útil para ver que ha pasado u otro caso de uso es en frameworks de desarrollo web como Flask, para asegurarse de que una función es llamada cuando el usuario se ha autentificado.

## 10. Generadores

Una función generadora es una función normal pero siempre que necesita generar un valor lo hará con la palabra clave yield en lugar de return.

Lo que hacen es automáticamente suspender y reanudar sus ejecuciones sobre el último punto de generación del valor. La principal ventaja es que en vez de computar una serie entera para luego almacenarla en memoria, se genera un valor y cuando se solicite el siguiente valor se generará este.

Un ejemplo de función generador sería la función `range()`, la cual no produce una lista en memoria de todos los valores desde el principio al final, lo que hace es un seguimiento del último número que pedimos para el tamaño de paso (step size, que por defecto es 1, es decir voy haciendo la generación de números de 1 en 1) para proporcionar un flujo constante de números.

Ejemplo:

```python
def funcion_cubo(n):

	resultado = []
	for numero in range(n):
		
		resultado.append(pow(numero,3))

	return resultado

funcion_cubo(10)
```

Esta función almacena en una lista todos los valores que se van generando hasta n = 10, aplicando generadores obtendríamos algo así:

```python
def funcion_cubo_generador(n):

	for x in range(n):
		
		# yield es la palabra clave
		yield pow(x,3) 

list(funcion_cubo_generador(10))
```

Otro ejemplo:

```python
def fibonacci(n):

	a = 1
	b = 1
	
	for numero in range(n):
	
		yield a
		a,b = b,a+b # a = b, b = a + b

# El bucle for para mostrar cada uno de los valores del generador
# llama a la funcion "next()" que se encarga de ir avanzando los valores
# hasta llegar al último por lo que al hacer el siguiente next daría un fallo
# diciendo que el generador a terminado
for x in fibonacci(10):
	
	print(x)
```

Luego nos encontramos con la función `iter()`, que nos permite convertir un objeto normal en un objeto que se pueda iterar, por ejemplo:

```python
s = "hello"
s_iterador = iter(s)
next(s_iterador)
```

## 11. Módulos avanzados

### 11.1. Módulos de colección

Implementa tipos de datos de contenedores especializados que son una alternativa de los contenedores propios de Python. Un contenedor es algo así como un diccionario o una tupla. Por ejemplo:

```python
from collections import Counter

# Vamos a poner la situación que tengo una lista con un conjunto de objetos
# que se repiten y quiero saber cuantas veces se repite ese objeto
# dentro de la lista

lista = [1,1,1,1,1,1,2,2,2,2,3,3,3]

Counter(lista)

lista = [1,1,1,1,1,1,2,2,2,2,3,3,3,'a','adios']

Counter(lista)
```

Dentro de Counter, los elementos se almacenan como claves de diccionario y los recuentos de los objetos se almacenan como valores. Las claves son siempre el objeto y el valor es siempre el recuento. Incluso puedo asignar el contador a una variable y obtener funciones extras:

* `variable.most_common()` → Permite mostrar en orden decreciente los objetos desde el más repetido hasta el menos, incluso podemos especificar cuantos objetos queremos que se muestren:
  * `variable.most_common(n)` → Siendo n, el número a especificar para indicar cuantos objetos de los mas repetidos queremos que se muestren

Ejemplo del código:

```python
algo = "aaaaaaabbbbbbbbcccccc"

recuento = Counter(algo)

recuento.most_common()

recuento.most_common(1)
```

#### 11.1.1. Diccionario

Nos puede ser útil cuando queremos llamar a una clave de un diccionario que no existe en dicho diccionario por lo que podemos asignar un valor por defecto. Con el diccionario que ya viene incluido en Python el resultado que nos daría es un error de llave (key error), en este caso el resultado sería el valor que hemos puesto como defecto:

```python
from collections import defaultdict

d = defaultdict(lambda:0)

d["Prueba"]
```

El ejemplo anterior devuelve el valor por defecto que hemos puesto en la función lambda.

#### 11.1.2. Nombre Tuple

El nombre tupla, intenta expandir el concepto de un objeto de tipo tuple al tener índices nombrados, veamos un ejemplo sencillo:

```python
tupla = (10,20,30)

# El resultado sería 10
tupla[0]
```

En este ejemplo tenemos una tupla con 3 elementos, si queremos unos de los elementos podemos verlo fácilmente, pero, ¿qué ocurre cuando tenemos una tupla con mas objetos y queremos sacar uno de ellos?

```python
from collections import namedtuple

conejo = namedtuple("Conejo",["Edad","Color","Nombre"])

misifu = conejo(Edad = 2, Color = "Blanco", Nombre = "Misifu")
```

Ahora podemos acceder a la tupla por el índice, por ejemplo:

```python

# Devolvería la edad de misifu por estar la edad en el indice 0
misifu[0]
```

O podemos acceder a la tupla por el nombre del índice, por ejemplo:

```python
# Devolvería 2, que es la Edad de misifu
misifu.Edad
```

### 11.2. Abrir y/o leer archivos y carpetas

Utilizaremos módulos para la apertura y lectura de archivos del ordenador.

Los módulos a usar son:

* Shutil
* OS Modules (OS → Operative System)

Anteriormente hemos visto cómo abrir un único archivo en Python, pero ¿qué ocurre si tenemos que abrir cada archivo y un directorio y leer y escribir en él ó archivos que están metidos en subcarpetas?

Python's OS Module permite navegar fácilmente por los archivos y directorios en el ordenador y realizar ciertas operaciones.

En Jupyter para conocer el directorio de trabajo actual utilizamos el comando **pwd**.

Suponiendo que en el directorio tenemos un archivo llamado _Prueba.txt_, vamos a abrir dicho archivo y utilizar el modulo del sistema operativo para devolver el directorio actual, hacer una lista de los elementos en el directorio, hacer una lista con los elementos del directorio, mover archivos entre directorios y eliminar archivos de forma segura:

```python
import os
import shutil
import send2trash

f = open("Prueba.txt",'w+')
f.write("Esto es una prueba de escritura en un archivo")
f.close()

# Devuelve el directorio de trabajo actual
os.getcwd()

# Me hace una lista de todos los elementos que tengo
# en el directorio de trabajo
os.listdir()

# Si quiero mostrar una lista de elementos que tengo en
# otro directorio, pongo el directorio dentro del método
os.listdir('/home/usuario/')

# Ahora veremos cómo podemos mover archivos de un directorio
# a otro utilizando el modulo shutil
# shutil.move(ORIGEN,DESTINO), TENER EN CUENTA que al
# mover archivos a ciertos directorios tenemos que tener
# permisos en esos directorios, de lo contrario dará error
shutil.move("Prueba.txt",'/home/daniel/')

# Para borrar un archivo existen varias formas pero la más
# segura es la siguiente, usando la librería send2trash,
# Al eliminar de esta forma podemos revertirlo,
# ya que se encuentra en la papelera, de otra forma
# sería complicado recuperar el fichero
send2trash.send2trash("Prueba.txt")
```

Ahora veremos cómo podemos hacer un árbol con todos los archivos de un directorio, mostrando carpetas, subcarpetas y ficheros que contienen:

```python
import os

directorio = '/home/daniel/Desktop'

for carpeta,sub_carpetas,archivos in os.walk(directorio):

	print(f"Estamos en la carpeta: {carpeta} \\n")
	print("Las subcarpetas son: ")

	for sub_carpeta in sub_carpetas:

		print(f"\\t{sub_carpeta}")

	print("Los archivos son: ")

	for archivo in archivos:

		print(f"\\t{archivo}")

print('\\n')
```

### 11.3. Módulo de fecha y hora

Permite crear objetos que tienen información no solo sobre la fecha o la hora, también objetos con zona horaria, operaciones con fecha y hora (como cuantos segundos han pasado o cuantos días han pasado):

```python
import datetime
# Para hacer operaciones con fechas
from datetime import date

mi_tiempo = datetime.time(2,20)

# Mostrar los minutos
mi_tiempo.minute

# Hacer un print de la hora
print(mi_tiempo)

# Podemos asignar incluso microsegundos,
# con un formato de 24 horas
# Así queda el formato de la fecha del día
hoy = datetime.date.today()
print(hoy)

# Incluso puedo extraer la información de la fecha para
# obtener los datos concretos
print(f"Día: {hoy.day}")
print(f"Mes: {hoy.month}")
print(f"Año: {hoy.year}")

# Incluso podemos realizar operaciones con las fechas,
# por ejemplo para ver la diferencia de días que hay
# entre una fecha y otra, debo importar
fecha1 = date(2021,11,3)
fecha2 = date(2020,11,2)

print(fecha1 - fecha2)
```

### 11.4. Modulo math y random

Algunos ejemplos de utilización de la librería Math:

```python
import math

# Podemos ver todas los métodos que incluye el módulo math
help(math)

# El numero pi
math.pi

# EL numero e
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

Algunos ejemplos de utilización de la librería Random:

```python
# Modulo aleatorio
# El modulo aleatorio permite crear numeros aleatorios
# e incluso generar una semilla para producir esos numeros aleatorios
import random

# Devuelve un valor entero aleatorio
random.randint(0,100)

# Podemos poner cualquier valor, el mas común es el 101,
# lo que hace es un generador pseudo aleatorio,
# pero son puramente determinista, están operados por un
# algoritmo.
# Este algoritmo depende de la semilla, lo que significa
# que si siempre aportas la misma semilla tendrás
# siempre la misma lista de números aleatorios.
random.seed(101)

# Para crear una lista de numeros desde el 0 hasta el 9
lista = list(range(0,10))
print(lista)

numero_elegido_aleatorio = random.choice(lista)
print(numero_elegido_aleatorio)

# Si quiero elegir mas de un elemento aleatorio de la lista
# haría lo siguiente:
# Puedo elegir estos valores repiento alguno
# Population elige de donde se toman los valores y K indica
# el numero de objetos a coger
numeros_aleatorios_repetidos = random.choices(population = lista,k = 5)
print(numeros_aleatorios_repetidos)

# O puedo elegir valores sin repetir ninguno
numeros_aleatorios_sin_repetir = random.sample(population = lista,k = 4)
print(numeros_aleatorios_sin_repetir)

# Ya hemos visto en otros ejemplos anteriores que podemos
# reordenar de manera aleatoria una lista con Shuffle
# RECORDAR QUE ESTA REORGANIZACIÓN SUCEDE EN EL LUGAR, NO DEVUELVE NADA
random.shuffle(lista)
print(lista)
```

### 11.5. Depurador de Python

El deburador o **debugger** se emplea para averiguar qué errores hay en el código, en vez de utilizar `print()` para ver qué sucede a cada rato, por ejemplo:

```python
# Primero importamos el depurador
import pdb

x = [1,2,3]
z = 2
y = 1

# Al ejecutarlo, el compilador nos mostrará en qué fila se encuentra el fallo, 
# pues antes de esa línea añadiremos lo siguiente:

resultado1 = z + y

# Al añadir este depurador, podemos introducir las variables que se hayan declarado 
# con la intención de ver el tipo incluso podemos realizar operaciones en ella,
# para ver si el resultado es el esperado o no.
# Una vez que hemos visto posibles casos y los fallos, pulsamos "q" para salir 
# del depurador

pdb.set_trace()

resultado2 = y + x # ERROR
```

### 11.6. Expresiones regulares

Veremos 3 partes con expresiones regulares diferentes, para la primera parte:

```python
import re

texto = "El numero del agente es 111-111-1111"
patron = "numero"

# Localiza la palabra y te muestra el indice desde donde empieza hasta donde acaba
busqueda = re.search(patron,texto)

# Me muestra el indice de la palabra
busqueda.span()

# Me muestra el indice inicial de la palabra
print(busqueda.start())

# Me muestra el indice final de la palabra
print(busqueda.end())

# Si queremos encontrar todas las mismas palabras y no una única, haremos lo siguiente
texto2 = "Mi numero favorito es el numero 8"
busqueda2 = re.findall("numero",texto2)

# O si queremos ver en qué indice se encuentra la palabra repetida varias veces
print("La palabra 'numero' está en los indices siguientes:")

for palabra in re.finditer('numero',texto2):

	print(f"\\t{palabra.span()}")

# Si queremos mostrar la palabra en vez del indice pondremos:
# group
print("\\nLa palabra 'numero' está en los indices siguientes:")

for palabra in re.finditer('numero',texto2):

	print(f"\\t{palabra.group()} -> {palabra.span()}")
```

En esta segunda parte nos centraremos en encontrar patrones generales, podemos encontrar mas caracteres identificadores en la documentación de Python:

* [https://docs.python.org/3/library/re.html](https://docs.python.org/3/library/re.html)

Ejemplos:

```python
import re

texto = "Mi numero de telefono es 11 11 11 111"

# Importante poner la r para indicar a Python que se trata de un patrón
numero = re.search(r"\\d\\d \\d\\d \\d\\d \\d\\d\\d",texto)
numero.group()

# Pero en el caso de querer patrones de numeros más largos, o en este caso en vez 
# de repetir \\d, podemos utilizar cuantificadores, por ejemplo:
numero = re.search(r"\\d{2} \\d{2} \\d{2} \\d{3}",texto)
numero.group()

# Si queremos extraer areas concretas del codigo del patron, podemos utilizar grupos 
# para cualquier tarea general que implique agrupar expresioner.
# Tener en cuenta que el indexado de estos grupos empieza en 1 y no en 0, ejemplo
numero_grupos = numero = re.compile(r"(\\d{2}) (\\d{2}) (\\d{2}) (\\d{3})")
resultado = re.search(numero_grupos,texto)

resultado.group()

# Podemos coger un incide incluso del grupo, el grupo anterior, su resultado 
# sería 11 11 11 111 si queremos quedarnos con el 111 seleccionaremos el indice 4
resultado.group(4)
```

Para la tercera parte, nos enfocaremos en encontrar patrones de palabras en un texto:

```python
import re

texto = "Tengo una coneja que se llama Misifu"

busq1 = re.search(r'coneja|perro',texto)
print(busq1.group())

texto2 = "Tengo un perro que se llama Tom"

busq2 = re.search(r'coneja|perro',texto2)
print(busq2.group())

# Otro ejemplo puede ser el querer encontrar palabras que tienen la misma terminación
texto3 = "The cat in the hat sat there"

# Pero esto solo permite coger un caracter mas, es decir la c de cat, la h de hat y 
# la s de sat
terminadas_at = re.findall(r'.at',texto3)
print(terminadas_at)

# Si añadimos una palabra con la misma terminacion pero más larga
texto4 = "The cat in the hat went splat."
termin_at = re.findall(r'.at',texto4)

# No muestra splat completo, mostraria lat, se solucionaria poniendo mas puntos 
# pero cogeria mas caracteres para las otras palabras
print(termin_at)

# Podemos encontrar valores que empiezan con un numero o finalizan con un numero
# Para indicar el principio usamos -> ^\\d
principio = re.findall(r'^\\d','2 es un numero')
print(principio)

# Para indicar el final usamos -> \\d$
final = re.findall(r'\\d$','Es un numero 4')
print(final)

# Incluso podemos hacer exclusiones, por ejemplo excluir un número de una frase
phrase = "there are 3 numbers 34 inside 5 this sentence."
re.findall(r'[^\\d]',phrase)

# Si queremos tener la palabra completa en vez de letra por letra
re.findall(r'[^\\d]+',phrase)

# Otro ejemplo de como podemos remover los signos de puntuación, exclamacion etc
test_phrase = """This is a string! But it has punctuation. How can we remove it?"""
re.findall('[^!.? ]+',test_phrase)

# Así puedo unificar las palabras para formar la frase sin los signos que hemos excluido
clean = ' '.join(re.findall('[^!.? ]+',test_phrase))
print(clean)

# Encontrar palabras que empiecen con la terminación 'cat'
# y terminen con una de estas opciones: 'fish','nap', o 'claw'
text = 'Hello, would you like some catfish?'
texttwo = "Hello, would you like to take a catnap?"
textthree = "Hello, have you seen this caterpillar?"
re.search(r'cat(fish|nap|claw)',text)
re.search(r'cat(fish|nap|claw)',texttwo)

# No devuelve nada porque la frase 3 tiene como terminación
# 'erpillar', que no es 'fish', 'nap' o 'claw'
re.search(r'cat(fish|nap|claw)',textthree)
```

### 11.7. Cronometrar el tiempo de una función

Con el fin de comprobar la eficiencia de nuestro código podemos cronometrar el tiempo que tarda en realizar una determinada acción una función, por ejemplo:

```python
import time

def func_uno(n):

	return [str(num) for num in range(n)]

def func_dos(n):

	return list(map(str,range(n)))

# Paso 1: Tener el tiempo de inicio
start_time = time.time()

# Paso 2: Ejercutar el código que queramos cronometrar
result = func_uno(1000000)

# Paso 3: Calcular el total del tiempo
end_time = time.time() - start_time
end_time
```

En el código anterior, ambos dan un resultado muy próximo por lo que es complicado ver una diferencia real pero podemos importar la librería timeit que permite hacer mediciones mas precisas con un número de repeticiones y parámetros que podemos asignar, ejemplo:

```python
import timeit

# Haremos la preparación para la primera función
# Necesitamos un SETUP

setup = '''
def func_uno(n):
return [str(num) for num in range(n)]
'''

# Un statement
stmt = 'func_uno(100)'

timeit.timeit(stmt, setup, number=100000) # Le pasamos un valor

# Haremos lo mismo para la segunda función
setup2 = '''
def func_dos(n):
return list(map(str,range(n)))
'''

stmt2 = 'func_dos(100)'

timeit.timeit(stmt2, setup2, number=100000)
```

Decir que Jupyter permite utilizar **funciones mágicas** (recordar que las funciones mágicas de Jupyter se activan con 2 % al comienzo del bloque de código), una de ellas es la función timeit:

```python
%%timeit
func_uno(100)

# En un bloque de código distinto haríamos lo mismo
# para la función 2
```

### 11.8. Descomprimir y comprimir archivos

Código de ejemplo:

```python
# Para comprimir archivos hacemos lo siguiente
import zipfile

f = open("nuevo_archivo.txt",'w+')
f.write("Esto es solo un ejemplo de introduccion de texto")
f.close()

f = open("nuevo_archivo2.txt",'w+')
f.write("Un poquito mas de texto")
f.close()

# Así creamos el zip
archivo_comprimido = zipfile.ZipFile('comprimido_1.zip','w')

# Así introducimos el fichero nuevo_archivo.txt al zip
archivo_comprimido.write("nuevo_archivo.txt", compress_type=zipfile.ZIP_DEFLATED)

# Así introducimos el fichero nuevo_archivo2.txt al zip
archivo_comprimido.write('nuevo_archivo2.txt', compress_type=zipfile.ZIP_DEFLATED)

# Así cerramos el zip una vez hemos introducido en él todos los archivos
archivo_comprimido.close()

# Para extraer archivos zip haríamos lo siguiente
zip_obj = zipfile.ZipFile('comprimido_1.zip', 'r')

# Extrae todo el contenido del zip en una carpeta con el nombre que hemos introducido
zip_obj.extractall("contenido_extraio")
```

## 12. Trabajar con ficheros CSV

CSV son las siglas de Comma Separated Values, es el tipo de formato que utiliza Excel u otros programas de bases de datos. Muy útil en la manipulación de datos de un fichero pero sólo contiene el contenido en crudo por lo que no podemos obtener imágenes, macros...solo los datos.

Trabajaremos con el modulo csv incluido en Python.

Una de las librerías a considerar para la manipulación de datos en Python sería Pandas.

Otra librería que puede ser interesante para archivos de Excel es Openpyxl o la API de Google Sheets para Python.

```python
import csv

# Primero abrimos el fichero
# utf-8, es por el tipo de caracteres del fichero
datos = open('example.csv',encoding = 'utf-8')

# csv.reader
csv_datos = csv.reader(datos)

# Le damos formato como un objeto de Python, lo mas comun es una lista
lineas_datos = list(csv_datos)

correos = []

for linea in lineas_datos[1:]:

	if linea[3] not in correos:

		correos.append(linea[3])

	else:

		pass

numero = 0

for correo in correos:

	print(f"{numero} : {correo}")
	numero += 1
```

Ahora vamos a ver como podemos escribir en un archivo csv:

```python
# Con newline debemos especificar que la nueva línea es una cadena vacía
archivo_salida = open('fichero_prueba.csv', mode = 'w', newline = '')

# "delimiter", es un delimitador o separador, separa una columna de otra
# cuando encuentra una coma (',')
csv_escribir = csv.writer(archivo_salida, delimiter = ',')

csv_escribir.writerow(['a', 'b', 'c'])

csv_escribir.writerows([['1', '2', '3'],['4', '5', '6']])

# Una vez que ya hemos realizado la escritura/ cambios en el archivo CSV,
# para guardarlos
archivo_salida.close()

# Ahora para un archivo creado, por ejemplo,
# partiendo del archivo que hemos creado antes
# El modo a, permite añadir informacion al final del archivo
f = open('fichero_prueba.csv', mode = 'a', newline = '')

csv_writer = csv.writer(f)

csv_writer.writerow(['Nombre', 'Apellido', 'Correo'])

csv_writer.writerows([['Daniel', 'BC', 'bsjhcjhs@gmail.com'], 
											['Clara', 'RA', 'jsasdjb@gmail.com']])

f.close()
```

## 13. Trabajar con ficheros JSON

A la hora de trabajar con ficheros JSON tenemos que importar la siguiente librería:

```python
import json
```

Vamos a crear una variable de tipo JSON en Python:

```python
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

</div>