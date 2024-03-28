---
description: >-
  Conceptos sobre SQL.
---

# SQL

# Bibliografía

+ https://www.youtube.com/watch?v=xqhJud-ryyI&t=6152s

# Conceptos básicos

## Introducción

**SQL** (Structured Query Language) es un lenguaje de programación utilizado para gestionar y manipular bases de datos. A diferencia de herramientas como Excel, que tienen un límite de alrededor de 1 millón de filas, las bases de datos pueden almacenar grandes cantidades de datos.

Las bases de datos pueden ser de dos tipos:

- **Relacionales**: Estas bases de datos almacenan datos estructurados en forma de tablas, con filas y columnas. Cada tabla tiene un identificador único que permite relacionarla con otras tablas.
- **No relacionales**: También conocidas como No-SQL (Not Only SQL), estas bases de datos almacenan datos no estructurados. Los datos pueden estar basados en grafos, documentos, pares clave-valor, entre otros.

Para interactuar con una base de datos utilizando SQL, se utilizan las consultas o **queries**. Las operaciones que se pueden realizar con las queries se resumen en el acrónimo **CRUD**, que hace referencia a Create (Crear), Read (Leer), Update (Actualizar) y Delete (Eliminar).

Las bases de datos pueden almacenarse localmente o en servidores. La opción local se utiliza generalmente para desarrollo. A nivel de servidores, existen dos tipos de sistemas:

- **On-Prem**: El servidor pertenece a la propia empresa.
- **Serverless**: El servidor está en la nube y es proporcionado por un tercero, como AWS o Azure.

Un concepto importante en el manejo de bases de datos es el **ERD** (Entity Relationship Diagram), que permite visualizar y entender las relaciones entre las diferentes tablas de la base de datos.

Las tablas en una base de datos pueden ser de dos tipos:

- **Fact tables**: Contienen los datos principales para el análisis de datos. Permiten medir y almacenan eventos.
- **Dimension tables**: Describen atributos o dimensiones de los datos. Se utilizan para filtrar, agrupar, etc.

Finalmente, dos de las herramientas más comunes para trabajar con SQL son **SQLite** y **PostgreSQL**.

## Palabras clave y estructura de las consultas SQL

Las consultas SQL se componen de varias palabras clave que permiten seleccionar, filtrar, ordenar y limitar los datos que se recuperan de una base de datos. Aquí tienes un resumen de las palabras clave más importantes y cómo se utilizan:

### SELECT

La palabra clave `SELECT` se utiliza para especificar las columnas que se quieren recuperar de la base de datos. Por ejemplo:

```sql
SELECT 
    job_title_short, 
    job_location

FROM 
    job_posting_fact
```

En este caso, se están seleccionando las columnas `job_title_short` y `job_location` de la tabla `job_posting_fact`.

Si se quiere seleccionar todas las columnas de una tabla, se puede utilizar el símbolo `*`:

```sql
SELECT *

FROM 
    job_posting_fact
```

### FROM

La palabra clave `FROM` se utiliza para especificar la tabla de la que se quieren recuperar los datos. Por ejemplo:

```sql
SELECT 
    job_title_short, 
    job_location

FROM 
    job_posting_fact
```

### WHERE

La palabra clave `WHERE` se utiliza para filtrar las filas que se quieren recuperar. Por ejemplo:

```sql
SELECT 
    job_title_short, 
    job_location, 
    job_via, 
    salary_year_avg

FROM 
    job_posting_fact

WHERE 
    job_title_short = 'Machine Learning Engineer'
```

En este caso, sólo se recuperarán las filas donde `job_title_short` sea igual a `'Machine Learning Engineer'`.

### ORDER BY

La palabra clave `ORDER BY` se utiliza para ordenar las filas recuperadas. Por defecto, las filas se ordenan en orden ascendente. Si se quiere ordenar en orden descendente, se puede utilizar la palabra clave `DESC`. Por ejemplo:

```sql
SELECT 
    job_title_short, 
    job_location, 
    job_via, 
    salary_year_avg

FROM 
    job_posting_fact

ORDER BY 
    salary_year_avg DESC
```

### LIMIT

La palabra clave `LIMIT` se utiliza para limitar el número de filas recuperadas. Por ejemplo:

```sql
SELECT 
    job_title_short, 
    job_location
FROM 
    job_posting_fact
LIMIT 5
```

En este caso, sólo se recuperarán las primeras 5 filas.

### SELECT DISTINCT

La combinación de palabras clave `SELECT DISTINCT` se utiliza para recuperar sólo filas únicas. Por ejemplo:

```sql
SELECT DISTINCT 
    salary_year_avg
FROM 
    job_posting_fact
```

En este caso, se recuperarán todos los valores únicos de la columna `salary_year_avg`.

### Orden de las palabras clave

El orden correcto para escribir las palabras clave en una consulta SQL es:

1. `SELECT`
2. `FROM`
3. `WHERE`
4. `GROUP BY`
5. `HAVING`
6. `ORDER BY`
7. `LIMIT`

Es importante recordar que las palabras clave no son sensibles a mayúsculas o minúsculas, pero se suelen escribir en mayúsculas por convención. También se pueden añadir comentarios a las consultas SQL utilizando `--` para comentarios de una línea y `/* */` para comentarios de varias líneas. Por ejemplo:

```sql
-- Este es un comentario de una línea

/*
Este es un comentario
de varias líneas
*/
```

## Operadores

Los operadores en SQL permiten realizar comparaciones y operaciones lógicas. Algunos de los operadores más comunes son:

- `AND`: Este operador se utiliza para combinar condiciones. Por ejemplo:

    ```sql
    SELECT
        job_title_short,
        job_location,
        job_via,
        salary_year_avg
    FROM
        job_posting_fact
    WHERE
        job_title_short = 'Machine Learning Engineer' AND
        salary_year_avg > 90000
    ```

## Comparadores

Los comparadores en SQL permiten realizar comparaciones entre valores. Algunos de los comparadores más comunes son:

- `NOT` o `<>`: Indica que el valor no debe ser igual al especificado.
- `>`, `<`: Indica que el valor debe ser mayor o menor al especificado.
- `>=`, `<=`: Indica que el valor debe ser mayor o igual, o menor o igual al especificado.
- `BETWEEN`: Indica que el valor debe estar entre dos valores especificados. Por ejemplo:

    ```sql
    WHERE
        salary_year_avg BETWEEN 100000 AND 200000
    ```

- `IN`: Comprueba si un valor se encuentra en una lista de valores especificados. Por ejemplo:

    ```sql
    WHERE
        job_location IN ('Boston, MA', 'Anywhere')
    ```

## Comodines (Wildcards)

Los comodines en SQL son caracteres especiales que se utilizan para realizar búsquedas de patrones en una cadena de texto. Se utilizan con el operador `LIKE` en una cláusula `WHERE`. Por ejemplo:

```sql
WHERE
    job_title LIKE '%Analyst%'
```

En este caso, se buscarán todos los trabajos que contengan la palabra 'Analyst' en su título.

## Alias

Los alias en SQL permiten asignar un nombre temporal a una columna o a una tabla, lo que puede facilitar la lectura de las consultas. Por ejemplo:

```sql
SELECT
    job_title_short AS job_title
```

En este caso, la columna `job_title_short` se mostrará como `job_title` en los resultados de la consulta.

## Operaciones

En SQL se pueden realizar operaciones aritméticas comunes como suma, resta, multiplicación, división y módulo. Por ejemplo:

```sql
SELECT
    hours_spent,
    hours_rate +  5 AS rate_hike
FROM
    job_posting_fact
WHERE
    rate_hike * hours_spent > 1000
```

En este caso, se está calculando un nuevo salario por hora (`rate_hike`) al sumar 5 al salario por hora actual (`hours_rate`). Luego, se filtran los resultados para mostrar sólo aquellos donde el producto de `rate_hike` y `hours_spent` sea mayor a 1000.