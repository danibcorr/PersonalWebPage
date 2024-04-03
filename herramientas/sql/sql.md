---
description: >-
  Conceptos sobre SQL.
---

# Bibliografía

+ https://www.youtube.com/watch?v=xqhJud-ryyI&t=6152s

# 1. Conceptos básicos de SQL

## 1.1. Introducción

**SQL** (Structured Query Language) es un lenguaje de programación diseñado para administrar y manipular bases de datos. A diferencia de herramientas como *Excel*, que tienen un límite de alrededor de 1 millón de filas, las bases de datos SQL pueden manejar grandes volúmenes de datos.

Las bases de datos se clasifican en dos tipos principales:

- **Relacionales**: Estas bases de datos almacenan datos estructurados en tablas, compuestas por filas y columnas. Cada tabla tiene un identificador único que permite relacionarla con otras tablas.
- **No relacionales**: También conocidas como *No-SQL* (Not Only SQL), estas bases de datos almacenan datos no estructurados. Los datos pueden estar basados en grafos, documentos, pares clave-valor, entre otros.

A continuación, se presenta una tabla que resume las ventajas y desventajas de cada tipo de base de datos:

|  | Datos relacionales | Datos no relacionales |
|---|---|---|
| Pros | Esquema estandarizado<br>Gran comunidad de usuarios<br>Lenguaje de consulta estandarizado<br>ACID | Disponibilidad continua<br>Velocidad de consulta<br>Agilidad<br>Costo |
| Contras | Dificultad de agrupación<br>Normalización de datos<br>Primero el esquema<br>Escalado intensivo en recursos | No hay un lenguaje de consulta estandarizado<br>Comunidad de usuarios más pequeña<br>Se requieren habilidades de desarrollador<br>Inconsistencia en la recuperación de datos |

En la tabla anterior, el "esquema estandarizado" se refiere a que todas las tablas o datos deben seguir una plantilla predefinida, lo que puede ser una desventaja debido a la necesidad de crear esa plantilla y a la poca flexibilidad resultante. 

El acrónimo *ACID* se refiere a Atomicity, Consistency, Isolation y Durability (Atomicidad, Consistencia, Aislamiento y Durabilidad), que son un conjunto de propiedades que garantizan la integridad y confiabilidad de los datos en entornos transaccionales. Los entornos transaccionales se refieren a sistemas o aplicaciones que manejan una gran cantidad de transacciones cortas en línea, permitiendo el procesamiento rápido de consultas a información muy actual y detallada. Estos entornos son comunes en bases de datos y sistemas de procesamiento de transacciones en línea (OLTP) como los cajeros automáticos, la banca en línea, las cajas registradoras y el comercio electrónico. Las propiedades *ACID* son:

1. **Atomicidad**: Garantiza que una transacción se ejecute como una unidad atómica, es decir, ocurrirá en su totalidad o no ocurrirá en absoluto. Si una parte de la transacción falla, la totalidad de la transacción se revierte a su estado inicial.

2. **Consistencia**: Garantiza que una transacción lleve la base de datos de un estado consistente a otro estado consistente. Las transacciones deben respetar las reglas de integridad definidas en la base de datos. Si una transacción viola alguna regla, se revierte y no se aplica.

3. **Aislamiento**: Garantiza que una transacción en ejecución sea invisible para otras transacciones hasta que se complete. Esto evita interferencias entre transacciones concurrentes y garantiza que cada transacción se ejecute de manera independiente.

4. **Durabilidad**: Garantiza que una vez que una transacción ha sido confirmada, sobrevivirá a fallos posteriores del sistema.

Estas propiedades son fundamentales para mantener la integridad de los datos en las bases de datos SQL.

La dificultad de escalar las bases de datos relacionales se debe a que escalan verticalmente, lo que supone incrementar el tamaño de la máquina que tenemos tanto en RAM, CPU u otros, o migrar a otros equipos más caros. Debido a las relaciones que existen entre las diferentes tablas de una misma base de datos, se requiere mantener consistencia. Por lo tanto, la tendencia para mitigar este problema ha sido crear *NewSQL*, cuya premisa es conseguir la gestión de datos relacionales con la escalabilidad de sistemas *NoSQL*.

Por otro lado, las bases de datos *NoSQL* tienen como principales ventajas la reducción de costos y la capacidad de escalar, ya que permiten crear sistemas distribuidos. Sin embargo, no cuentan con una sintaxis estándar, lo que puede resultar en una gestión más compleja.

Para interactuar con una base de datos utilizando SQL, se utilizan las consultas o **queries**. Las operaciones que se pueden realizar con las queries se resumen en el acrónimo **CRUD**, que hace referencia a *Create* (Crear), *Read* (Leer), *Update* (Actualizar) y *Delete* (Eliminar).

Las bases de datos pueden almacenarse localmente o en servidores. La opción local se utiliza generalmente para desarrollo. A nivel de servidores, existen dos tipos de sistemas:

- **On-Prem**: El servidor pertenece a la propia empresa.
- **Serverless**: El servidor está en la nube y es proporcionado por un tercero, como *AWS* o *Azure*.

Un concepto importante en el manejo de bases de datos es el **ERD** (Entity Relationship Diagram), que permite visualizar y entender las relaciones entre las diferentes tablas de la base de datos.

Las tablas en una base de datos pueden ser de dos tipos:

- **Fact tables**: Contienen los datos principales para el análisis de datos. Permiten medir y almacenar eventos.
- **Dimension tables**: Describen atributos o dimensiones de los datos. Se utilizan para filtrar, agrupar, etc. Estas tablas son esenciales para proporcionar contexto a los datos contenidos en las tablas de hechos. Por ejemplo, una tabla de hechos puede contener registros de ventas, mientras que una tabla de dimensiones puede contener información sobre los clientes, como su ubicación y segmento de mercado. Esta información adicional permite realizar análisis más detallados y significativos. 

## 1.2. Palabras clave y estructura de las consultas SQL

Las consultas SQL se componen de varias palabras clave que permiten seleccionar, filtrar, ordenar y limitar los datos que se recuperan de una base de datos. A continuación se presenta un resumen de las palabras clave más importantes y cómo se utilizan:

+ **SELECT**: La palabra clave `SELECT` se utiliza para especificar las columnas que se quieren recuperar de la base de datos. Por ejemplo:
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

+ **FROM**: La palabra clave `FROM` se utiliza para especificar la tabla de la que se quieren recuperar los datos. Por ejemplo:

    ```sql
    SELECT 
        job_title_short, 
        job_location

    FROM 
        job_posting_fact
    ```

+ **WHERE**: La palabra clave `WHERE` se utiliza para filtrar las filas que se quieren recuperar. Por ejemplo:

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

+ **ORDER BY**: La palabra clave `ORDER BY` se utiliza para ordenar las filas recuperadas. Por defecto, las filas se ordenan en orden ascendente. Si se quiere ordenar en orden descendente, se puede utilizar la palabra clave `DESC`. Por ejemplo:

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

+ **LIMIT**: La palabra clave `LIMIT` se utiliza para limitar el número de filas recuperadas. Por ejemplo:

    ```sql
    SELECT 
        job_title_short, 
        job_location
    FROM 
        job_posting_fact
    LIMIT 5
    ```

    En este caso, sólo se recuperarán las primeras 5 filas.

+ **SELECT DISTINCT**: La combinación de palabras clave `SELECT DISTINCT` se utiliza para recuperar sólo filas únicas. Por ejemplo:

    ```sql
    SELECT DISTINCT 
        salary_year_avg
    FROM 
        job_posting_fact
    ```

    En este caso, se recuperarán todos los valores únicos de la columna `salary_year_avg`.

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

## 1.3. Operadores y comparadores en SQL

En SQL, se utilizan operadores y comparadores para realizar operaciones lógicas y comparaciones entre valores. A continuación, se presentan algunos de los operadores y comparadores más comunes con ejemplos de su uso:

- **AND**: Este operador se utiliza para combinar condiciones en una cláusula `WHERE`. Si todas las condiciones separadas por `AND` son verdaderas, entonces la fila cumple con la condición y se incluye en el resultado de la consulta.

- **OR**: Este operador se utiliza para combinar condiciones en una cláusula `WHERE`. Si alguna de las condiciones separadas por `OR` es verdadera, entonces la fila cumple con la condición y se incluye en el resultado de la consulta.

- **NOT** o **<>**: Este operador se utiliza para negar una condición en una cláusula `WHERE`. Si la condición después de `NOT` es falsa, entonces la fila cumple con la condición y se incluye en el resultado de la consulta.

- **BETWEEN**: Este operador se utiliza para seleccionar valores dentro de un rango. Los valores pueden ser números, texto o fechas.

- **LIKE**: Este operador se utiliza en una cláusula `WHERE` para buscar un patrón específico en una columna. El símbolo `%` es un carácter comodín que representa cero, uno o varios caracteres.

- **IN**: Este operador comprueba si un valor se encuentra en una lista de valores especificados.

- **>**, **<**: Estos comparadores indican que el valor debe ser mayor o menor al especificado.

- **>=**, **<=**: Estos comparadores indican que el valor debe ser mayor o igual, o menor o igual al especificado.

Por ejemplo, si se desea seleccionar los trabajos de 'Data Scientist' o 'Machine Learning Engineer' con un salario promedio anual entre 50000 y 100000, se podría utilizar la siguiente consulta:

```sql
SELECT
    job_title_short,
    job_location,
    job_via,
    salary_year_avg
FROM
    job_posting_fact
WHERE
    (job_title_short = 'Data Scientist' OR job_title_short = 'Machine Learning Engineer') AND
    salary_year_avg BETWEEN 50000 AND 100000;
```

En este caso, se están combinando los operadores `AND`, `OR` y `BETWEEN` para formar una condición compleja en la cláusula `WHERE`.

## 1.4. Comodines (Wildcards) en SQL

Los comodines son caracteres especiales que se utilizan en SQL para buscar patrones en cadenas de texto. Se utilizan en combinación con el operador `LIKE` en una cláusula `WHERE`. Los comodines más comunes en SQL son:

- **%**: Este comodín representa cero, uno o varios caracteres. Por ejemplo, si se desea buscar todos los trabajos que contengan la palabra 'Analyst' en cualquier parte del título, se podría utilizar la siguiente consulta:

    ```sql
    WHERE
        job_title LIKE '%Analyst%'
    ```

- **_**: Este comodín representa exactamente un carácter. Por ejemplo, si se desea buscar todos los trabajos cuyo título tenga exactamente 10 caracteres, se podría utilizar la siguiente consulta:

    ```sql
    WHERE
        job_title LIKE '__________'
    ```

    En este caso, cada guión bajo `_` representa un carácter, y como hay 10 guiones bajos, se buscarán los títulos de trabajo que tengan exactamente 10 caracteres.

Es importante tener en cuenta que el uso de comodines puede hacer que las consultas sean más lentas, especialmente si se utiliza el comodín `%` al principio de un patrón, ya que en ese caso SQL tiene que buscar el patrón en todas las posiciones de cada valor de la columna. Por lo tanto, se recomienda utilizar los comodines con cuidado y solo cuando sean necesarios.

## 1.5. Alias

Los alias en SQL permiten asignar un nombre temporal a una columna o a una tabla, lo que puede facilitar la lectura de las consultas. Por ejemplo:

```sql
SELECT
    job_title_short AS job_title
```

En este caso, la columna `job_title_short` se mostrará como `job_title` en los resultados de la consulta.

## 1.6. Operaciones

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

## 1.7. Agregación en SQL

Las funciones de agregación en SQL calculan un solo resultado a partir de un conjunto de valores de entrada. Aquí tienes una lista de las más comunes:

- **SUM()**: Suma todos los valores en una columna específica.
- **COUNT()**: Cuenta el número de filas que coinciden con un criterio.
- **AVG()**: Calcula el promedio de una columna.
- **MAX()**: Encuentra el valor máximo en un conjunto de valores.
- **MIN()**: Encuentra el valor mínimo en un conjunto de valores.

Estas funciones se pueden combinar con las cláusulas `GROUP BY` y/o `HAVING`:

- **GROUP BY**: Agrupa las filas que comparten una propiedad para que la función de agregación se pueda aplicar.
- **HAVING**: Filtra grupos basados en el resultado de una función agregada (a diferencia de `WHERE`, que filtra filas).

Aquí tienes un ejemplo de cómo se pueden usar estas funciones y cláusulas en una consulta SQL:

```sql
SELECT
    -- Realizar la suma de todos los salarios
    SUM(job_posting_fact.salary_year_avg) AS salary_sum,

    -- Contar el número de filas que hay en la base de datos
    COUNT(*) AS count_rows,

    -- Contar el número de trabajos diferentes
    COUNT(DISTINCT job_posting_fact.job_title_short) AS tipo_trabajos,

    -- Promedio del salario
    AVG(job_posting_fact.salary_year_avg) AS salario_promedio
FROM
    job_posting_fact
WHERE
    -- Ahora podemos aplicar todos los filtros anteriores pero
    -- solo en aquellos casos donde el título del trabajo contenga el
    -- término Machine Learning
    job_posting_fact.job_title LIKE '%Machine%Learning%'
```

Y aquí tienes otro ejemplo que muestra cómo se pueden usar estas funciones y cláusulas para obtener información más detallada sobre los trabajos:

```sql
SELECT
    -- Nos quedamos con los tipos de trabajos
    job_posting_fact.job_title_short as Trabajos,

    -- Obtenemos el salario mínimo para cada puesto
    MIN(job_posting_fact.salary_year_avg) as MIN_SAL_YER,

    -- Obtenemos el salario máximo para cada puesto
    MAX(job_posting_fact.salary_year_avg) as MAX_SAL_YER,

    -- Obtenemos el salario promedio para cada puesto
    AVG(job_posting_fact.salary_year_avg) as AVG_SAL_YER,

    -- Contamos las veces que aparece un puesto de trabajo
    COUNT(job_posting_fact.job_title_short) as JOB_COUNT
FROM
    job_posting_fact
GROUP BY
    -- Agrupamos los datos por el tipo de trabajo
    Trabajos
HAVING
    -- Filtramos aquellos trabajos que no se repitan más de 100 veces
    -- Es muy útil para en el caso de calcular media no haya grandes
    -- desviaciones
    JOB_COUNT > 100
ORDER BY
    -- Ordenamos las filas según el salario promedio anual
    AVG_SAL_YER
```

## 1.8. Valores NULL en SQL

Los valores `NULL` en SQL representan la ausencia de información. Podemos filtrar estos valores utilizando la cláusula `IS NOT NULL` en una consulta `WHERE`. Por ejemplo:

```sql
WHERE
    salary_year_avg IS NOT NULL
```

Otra estrategia es reemplazar los valores `NULL` con un valor calculado, como el promedio de los valores no nulos que pertenecen a la misma categoría. Por ejemplo, si tenemos una tabla de ofertas de trabajo donde algunos registros tienen salarios publicados y otros no, podríamos rellenar los valores `NULL` con la media de los salarios de la misma categoría de trabajo. Esto se puede hacer de la siguiente manera:

```sql
UPDATE empleados
SET salario = (
    SELECT AVG(salario)
    FROM empleados AS e2
    WHERE e2.trabajo = empleados.trabajo
    AND e2.salario IS NOT NULL
)
WHERE salario IS NULL;
```

Este código actualizará la columna `salario` de la tabla `empleados`, estableciendo los valores `NULL` al promedio de salario para cada tipo de trabajo. La subconsulta calcula el promedio de salario para cada tipo de trabajo, excluyendo los valores `NULL`. Ten en cuenta que este comando actualizará la tabla `empleados` en su lugar. Si no quieres modificar la tabla original, podrías crear una nueva tabla o vista con los valores `NULL` reemplazados.

## 1.9. Joins en SQL

Existen cuatro tipos de `JOIN` en SQL, suponiendo que tenemos dos tablas separadas A y B:

- **LEFT JOIN**: Devuelve los datos de A y las coincidencias de B.
- **RIGHT JOIN**: Devuelve los datos de B y las coincidencias de A.
- **INNER JOIN**: Devuelve únicamente los datos que coinciden en ambas tablas.
- **FULL JOIN**: Devuelve todos los datos de ambas tablas, coincidan o no.

Por ejemplo, si dos tablas contienen un identificador común y queremos combinarlas para obtener los datos asociados a ese identificador, como el nombre de la empresa, podemos hacer lo siguiente:

```sql
SELECT
    job_postings_fact.job_id,
    company_dim.name as Empresa
FROM
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
```

En este caso, estamos utilizando un `LEFT JOIN` para combinar las tablas `job_postings_fact` y `company_dim` basándonos en la columna `company_id` que es común en ambas tablas. Como resultado, obtendremos una tabla que incluye el `job_id` y el nombre de la empresa (`Empresa`) para cada registro en `job_postings_fact`. Si un `job_id` en `job_postings_fact` no tiene una coincidencia en `company_dim`, el valor de `Empresa` será `NULL` para ese registro. 

# 2. Conceptos avanzados

## 2.1. Instalación de PostgreSQL en Linux

Aquí tienes un resumen de los pasos para instalar PostgreSQL en Linux utilizando el sistema operativo PopOS, una distribución de Linux basada en Ubuntu y, por tanto, en Debian.

1. **Instalación de PostgreSQL**: Sigue los pasos de la página web oficial de PostgreSQL para instalarlo en tu sistema.

2. **Interfaz de usuario gráfica (GUI)**: Puedes usar pgAdmin, que es la interfaz gráfica de PostgreSQL. En algunos casos, será necesario para inicializar la base de datos. Sin embargo, también puedes hacerlo manualmente desde el terminal. En este caso, se usará VS Code.

3. **Configuración del firewall**: Una vez instalado PostgreSQL, en el caso de PopOS, se utiliza UFW como firewall. Deberás habilitar el puerto 5432, que es el puerto por defecto que utiliza PostgreSQL. Puedes comprobar el estado y las reglas de UFW con `sudo ufw status verbose`.

    ```bash
    sudo ufw allow 5432
    sudo ufw status verbose
    ```

4. **Creación de un usuario y una base de datos**: Abre un terminal y ejecuta los siguientes comandos para crear un usuario con contraseña y una base de datos:

    ```sql
    sudo -i -u postgres
    psql
    CREATE USER nombre_usuario WITH ENCRYPTED PASSWORD 'clave';
    CREATE DATABASE nombre_database OWNER nombre_usuario;
    ```

5. **Instalación de extensiones en VS Code**: En VS Code, instala las extensiones SQLTools y SQLTools PostgreSQL de Matheus Teixeira.

6. **Permisos del usuario**: El usuario creado inicialmente no tiene permisos para hacer nada. Para que pueda crear bases de datos, deberás ejecutar el siguiente comando en psql:

    ```sql
    ALTER USER nombre_usuario CREATEDB;
    ```

Además, aquí tienes algunos comandos útiles dentro de psql:

- `\l`: Muestra las bases de datos existentes.
- `\du`: Muestra los usuarios creados.

## 2.2. Tipos de datos en SQL

En SQL, se utilizan diferentes tipos de datos para crear columnas en una base de datos. Estos tipos de datos ayudan a mantener la integridad de los datos y a mejorar la eficiencia al procesar consultas. Los tipos de datos más comunes son:

- **INT**: Este tipo de datos se utiliza para almacenar números enteros. Por ejemplo, si tienes una tabla de `empleados` y quieres almacenar la `edad` de cada empleado, puedes usar el tipo de datos `INT`.

    ```sql
    CREATE TABLE empleados (
        id INT,
        nombre VARCHAR(100),
        edad INT
    );
    ```

- **VARCHAR** o **TEXT**: Estos tipos de datos se utilizan para almacenar cadenas de caracteres. `VARCHAR` requiere que especifiques una longitud máxima para los caracteres. `TEXT` se utiliza para cadenas de caracteres de longitud variable. Por ejemplo, puedes usar `VARCHAR` para almacenar el `nombre` de los empleados.

    ```sql
    CREATE TABLE empleados (
        id INT,
        nombre VARCHAR(100),
        edad INT
    );
    ```

- **BOOLEAN**: Este tipo de datos se utiliza para almacenar valores booleanos, es decir, verdadero o falso (1 o 0). Por ejemplo, si quieres almacenar si un empleado ha completado una tarea, puedes usar el tipo de datos `BOOLEAN`.

    ```sql
    CREATE TABLE tareas (
        id INT,
        descripcion VARCHAR(255),
        completada BOOLEAN
    );
    ```

- **TIMESTAMP**: Este tipo de datos se utiliza para almacenar fechas y horas. Por ejemplo, puedes usar `TIMESTAMP` para almacenar la `fecha_de_contratacion` de un empleado.

    ```sql
    CREATE TABLE empleados (
        id INT,
        nombre VARCHAR(100),
        fecha_de_contratacion TIMESTAMP
    );
    ```

- **NUMERIC**: Este tipo de datos se utiliza para almacenar números decimales o de precisión exacta. Por ejemplo, puedes usar `NUMERIC` para almacenar el `salario` de un empleado.

    ```sql
    CREATE TABLE empleados (
        id INT,
        nombre VARCHAR(100),
        salario NUMERIC(10, 2)
    );
    ```

    En el ejemplo anterior, `NUMERIC(10, 2)` significa que el salario puede tener hasta 10 dígitos en total, de los cuales 2 son decimales.

## 2.3. Manipulación de tablas en SQL

En SQL, se utilizan varias instrucciones para manipular tablas:

- **CREATE TABLE**: Se utiliza para crear nuevas tablas. Por ejemplo:

    ```sql
    CREATE TABLE job_applied(
        job_id INT,
        application_sent_date DATE,
        custom_resume BOOLEAN,
        resume_file_name VARCHAR(255),
        cover_letter_sent BOOLEAN,
        cover_letter_file_name VARCHAR(255),
        status VARCHAR(50)
    );
    ```
    En el código anterior, `job_applied` es el nombre de la tabla y los parámetros dentro de los paréntesis son los nombres de las columnas con sus respectivos tipos de datos.

- **INSERT INTO**: Se utiliza para añadir datos a la tabla. Por ejemplo:

    ```sql
    INSERT INTO job_applied(
        job_id,
        application_sent_date,
        custom_resume,
        resume_file_name,
        cover_letter_sent,
        cover_letter_file_name,
        status
    )
    VALUES  (1,
        '2024-02-01',
        TRUE,
        'CV_01.pdf',
        true,
        'cover_letter_01.pdf',
        'submitted'),
        (2,
        '2024-03-01',
        TRUE,
        'CV_02.pdf',
        true,
        'cover_letter_02.pdf',
        'submitted');
    ```

- **ALTER TABLE**: Esta instrucción se utiliza para modificar la estructura de una tabla existente. Por ejemplo, puedes añadir una nueva columna a una tabla existente de la siguiente manera:

    ```sql
    ALTER TABLE empleados
    ADD COLUMN email VARCHAR(255);
    ```

    En el ejemplo anterior, se añade una nueva columna llamada `email` a la tabla `empleados`. El tipo de datos de la nueva columna es `VARCHAR(255)`.

    También puedes eliminar una columna existente de una tabla utilizando la instrucción `ALTER TABLE`. Por ejemplo:

    ```sql
    ALTER TABLE empleados
    DROP COLUMN email;
    ```

    En este caso, se elimina la columna `email` de la tabla `empleados`.

- **DROP TABLE**: Esta instrucción se utiliza para eliminar una tabla existente. Por ejemplo, si quieres eliminar la tabla `empleados`, puedes hacerlo de la siguiente manera:

    ```sql
    DROP TABLE empleados;
    ```

    Ten en cuenta que esta operación eliminará la tabla y todos los datos que contiene, por lo que debes tener cuidado al utilizarla. Es una buena práctica hacer una copia de seguridad de tus datos antes de realizar operaciones que puedan resultar en la pérdida de datos.

## 2.4. Actualización de datos en SQL

La instrucción **UPDATE** en SQL se utiliza para modificar los datos existentes en una tabla. Esta instrucción resulta muy útil cuando se necesita cambiar los valores de ciertas filas o columnas.

La sintaxis básica de la instrucción `UPDATE` es la siguiente:

```sql
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2, ...
WHERE condicion;
```

En esta sintaxis:

- `nombre_tabla` es el nombre de la tabla que se desea actualizar.
- `SET` es la cláusula que se utiliza para especificar las columnas a actualizar y los nuevos valores que se desean asignar a esas columnas. Se pueden actualizar una o varias columnas a la vez.
- `WHERE` es la cláusula que se utiliza para especificar las filas que se desean actualizar. Si se omite la cláusula `WHERE`, todas las filas de la tabla se actualizarán, lo cual puede no ser lo deseado.

Por ejemplo, si se tiene una tabla llamada `empleados` y se desea aumentar el salario de todos los empleados que tienen un salario inferior a 30000 en un 10%, se podría hacer de la siguiente manera:

```sql
UPDATE empleados
SET salario = salario * 1.1
WHERE salario < 30000;
```

En este caso, la cláusula `WHERE` se utiliza para seleccionar solo las filas donde el salario es inferior a 30000. Luego, la cláusula `SET` se utiliza para aumentar el salario de esas filas en un 10%.

Es muy importante utilizar la cláusula `WHERE` cuando se utiliza la instrucción `UPDATE`, para evitar cambios no deseados en los datos. Siempre es una buena práctica hacer una copia de seguridad de los datos antes de realizar operaciones que pueden modificarlos.

## 2.5. Tratamiento de columnas en SQL

En SQL, se pueden realizar varias operaciones en las columnas de una tabla:

- **Renombrar columnas**: Se puede cambiar el nombre de una columna utilizando la instrucción **RENAME COLUMN**. Por ejemplo:

    ```sql
    ALTER TABLE job_applied
    RENAME COLUMN contact TO contact_name;
    ```

- **Cambiar el tipo de una columna**: Se puede cambiar el tipo de datos de una columna utilizando la instrucción **TYPE**. Por ejemplo:

    ```sql
    ALTER TABLE job_applied
    ALTER COLUMN contact_name TYPE TEXT;
    ```

- **Eliminar una columna**: Se puede eliminar una columna de una tabla utilizando la instrucción **DROP COLUMN**. Por ejemplo:

    ```sql
    ALTER TABLE job_applied
    DROP COLUMN contact_name;
    ```

## 2.6. Carga de datos en una base de datos SQL

Para copiar el contenido de un archivo CSV a una base de datos, se utiliza la instrucción **COPY**. Esta instrucción permite importar datos desde un archivo CSV a una tabla de la base de datos. La sintaxis es la siguiente:

```sql
COPY nombre_tabla
FROM ruta_archivo_csv
DELIMITER ',' CSV HEADER;
```

En esta sintaxis, `nombre_tabla` es el nombre de la tabla a la que se desean importar los datos, `ruta_archivo_csv` es la ruta del archivo CSV que contiene los datos y `DELIMITER ',' CSV HEADER` indica que los datos están separados por comas y que la primera fila del archivo CSV contiene los nombres de las columnas.

## 2.7. Funciones para fechas en SQL

En SQL, se pueden utilizar varias funciones para realizar operaciones en valores de fechas y tiempos:

- **::DATE**: Esta operación convierte un valor de fecha y hora a un formato de fecha, eliminando la parte del tiempo. El operador **::** permite realizar un casting (conversión de tipos). Por ejemplo, si se tiene una columna `fecha_hora` de tipo `TIMESTAMP`, se puede obtener solo la parte de la fecha de la siguiente manera:

    ```sql
    SELECT fecha_hora::DATE FROM nombre_tabla;
    ```

- **AT TIME ZONE**: Esta función convierte un valor de fecha y hora a una zona horaria específica. Por ejemplo, si se desea convertir la hora actual a la zona horaria UTC, se puede hacer de la siguiente manera:

    ```sql
    SELECT NOW() AT TIME ZONE 'UTC';
    ```

- **EXTRACT**: Esta función se utiliza para obtener partes específicas de una fecha. Por ejemplo, para filtrar las fechas que corresponden al mes de enero, se puede utilizar:

    ```sql
    WHERE EXTRACT(MONTH FROM fecha) = 1;
    ```

    En este caso, `EXTRACT(MONTH FROM fecha)` devuelve el mes de la fecha, y la condición `= 1` selecciona solo las fechas que corresponden al mes de enero.

## 2.8. Expresiones CASE en SQL

Las expresiones **CASE** en SQL se utilizan para crear diferentes resultados basados en diferentes condiciones. Son similares a las declaraciones **if-then-else** en otros lenguajes de programación. Por ejemplo, si se desea clasificar los trabajos en función del salario, se podría utilizar la siguiente consulta:

```sql
SELECT job_title,
       CASE
           WHEN salary_year_avg > 100000 THEN 'High'
           WHEN salary_year_avg > 50000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_category
FROM job_posting_fact;
```

En este caso, la expresión `CASE` clasifica los trabajos en 'High', 'Medium' o 'Low' en función del salario promedio anual.

## 2.9. Subconsultas y CTEs en SQL

Las subconsultas y los CTEs (Common Table Expressions) son técnicas avanzadas de SQL que permiten realizar consultas más complejas. Por ejemplo, si se desea obtener el salario promedio de los trabajos de 'Data Scientist', se podría utilizar una subconsulta de la siguiente manera:

```sql
SELECT AVG(salary_year_avg)
FROM (
    SELECT salary_year_avg
    FROM job_posting_fact
    WHERE job_title = 'Data Scientist'
) AS subquery;
```

En este caso, la subconsulta selecciona los salarios de los trabajos de 'Data Scientist', y la consulta principal calcula el salario promedio.

Un CTE es similar a una subconsulta, pero se define antes de la consulta principal y se puede referenciar varias veces en la consulta. Por ejemplo:

```sql
WITH data_scientist_jobs AS (
    SELECT *
    FROM job_posting_fact
    WHERE job_title = 'Data Scientist'
)
SELECT AVG(salary_year_avg)
FROM data_scientist_jobs;
```

En este caso, el CTE `data_scientist_jobs` selecciona los trabajos de 'Data Scientist', y luego se utiliza en la consulta principal para calcular el salario promedio.

## 2.10. UNION en SQL

La operación **UNION** en SQL se utiliza para combinar los resultados de dos o más consultas `SELECT` en un solo conjunto de resultados. Las consultas deben tener el mismo número de columnas y los tipos de datos deben ser compatibles. Por ejemplo, si se desea obtener una lista de todos los títulos de trabajo únicos para los trabajos de 'Data Scientist' y 'Machine Learning Engineer', se podría utilizar la operación `UNION` de la siguiente manera:

```sql
SELECT job_title
FROM job_posting_fact
WHERE job_title = 'Data Scientist'
UNION
SELECT job_title
FROM job_posting_fact
WHERE job_title = 'Machine Learning Engineer';
```

En este caso, la operación `UNION` combina los resultados de las dos consultas `SELECT` en un solo conjunto de resultados. Como `UNION` elimina las filas duplicadas, el resultado será una lista de todos los títulos de trabajo únicos para los trabajos de 'Data Scientist' y 'Machine Learning Engineer'.