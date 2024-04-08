---
description: >-
  Conceptos básicos sobre la herramienta Git. Contribuyentes @AsuncionBueneke,
  @iamcay y @LuisMiguelCG en GitHub.
---

# 1. Control de versiones

El control de versiones es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, permitiendo así recuperar versiones específicas más adelante.

## 1.1. Terminología del control de versiones

- **Repositorio Local**: Es una base de datos centralizada que almacena las distintas versiones de los archivos bajo control de versiones.
- **Copia Local**: Es la copia de un archivo bajo control de versiones que los usuarios modifican. El directorio local contiene todas estas copias.
- **Repositorio Remoto**: Son versiones de nuestros proyectos que se alojan en Internet o en cualquier otra red.
- **Histórico (Log)**: Es un registro de todos los cambios que se han producido en el repositorio. Es responsabilidad del usuario añadir información al log cuando se produce un cambio.
- **Conflicto**: Se produce cuando dos usuarios han modificado las mismas líneas en un archivo, o si un usuario eliminó un archivo mientras otro usuario lo estaba modificando. En estos casos, Git no puede determinar automáticamente qué versión es correcta.

## 1.2. Estados de un archivo

- **Sin Seguimiento**: Git ve un archivo que no estaba en la instantánea anterior. Git no empezará a incluirlo en las confirmaciones hasta que se lo indiques explícitamente.
- **Confirmado**: Los datos están almacenados de manera segura en tu base de datos local.
- **Modificado**: Has modificado el archivo pero todavía no lo has confirmado a tu base de datos.
- **Preparado**: Has marcado un archivo modificado en su versión actual para que vaya en tu próxima confirmación.
- **Ignorado**: Un archivo que se le ha indicado explícitamente a Git que ignore.

## 1.3. Operaciones

- **Clone**: Crea un clon o copia local de un repositorio remoto.
- **Add**: Añade contenido del directorio de trabajo al área de ensayo para la próxima confirmación.
- **Commit**: Toma todos los contenidos de los archivos a los que se les realiza el seguimiento con git add y registra una nueva instantánea permanente en la base de datos y luego avanza el puntero de la rama en la rama actual.
- **Push**: Se utiliza para comunicar con otro repositorio, calcular lo que tu base de datos local tiene que la remota no tiene, y luego subir la diferencia al otro repositorio.
- **Pull**: Se emplea para extraer y descargar contenido desde un repositorio remoto y actualizar al instante el repositorio local para reflejar ese contenido.
- **Fork**: Copiar un proyecto y partir de este, hacerle modificaciones. Cuando trabajamos con repositorios Git, supone hacer una copia exacta del proyecto, generando dos URL distintas.
- **Pull Request**: Solicitudes de integración, forma de contribuir a un proyecto grupal o de código abierto.

# 2. Git y GitHub

Git es un sistema de control de versiones distribuido que permite a los equipos de desarrollo colaborar en proyectos de software. GitHub es una plataforma de alojamiento de código que utiliza Git para el control de versiones.

## 2.1. Comandos básicos de Git-Bash

Git-Bash es una interfaz de línea de comandos para interactuar con Git. Aquí te dejo una tabla con algunos de los comandos más utilizados:

| Comando   | Argumentos           | Función                                                                                                                                                  |
| --------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **pwd**   |                      | Muestra el directorio actual en el que te encuentras.                                                                                                    |
| **mkdir** | \<dir>               | Crea un nuevo directorio.                                                                                                                                |
| **cd**    | \<dir>               | Cambia al directorio especificado.                                                                                                                       |
| **ls**    | \[-l] \[-a]          | Lista los archivos en el directorio actual. Con **ls -l**, muestra una lista detallada, y con **ls -a**, incluye archivos ocultos.                      |
| **rm**    | \<fichero>           | Elimina el archivo especificado.                                                                                                                         |
| **mv**    | \<origen> \<destino> | Mueve o renombra un archivo del origen al destino.                                                                                                       |

Estos comandos son fundamentales para la navegación y gestión de archivos en Git-Bash. Recuerda que siempre puedes usar el comando `man` seguido del nombre del comando para obtener más información sobre su uso. Por ejemplo, `man ls` te dará una descripción detallada del comando `ls`.

## 2.2. Control de versiones local

Git es un sistema de control de versiones distribuido que permite a los equipos de desarrollo colaborar en proyectos de software. Aquí te dejo una tabla con algunos de los comandos más utilizados en Git para el control de versiones local:

| Comando | Argumentos | Función |
| --- | --- | --- |
| **git init** | | Crea un nuevo repositorio local en tu máquina. |
| **git clone** | \[url] | Clona un repositorio existente. |
| **git add** | \<dir> | Prepara archivos para ser confirmados en el repositorio local. |
| **git commit -m** | 'texto' | Confirma cambios en el repositorio local. |
| **git commit -a -m** | 'texto' | Confirma cambios en el repositorio local sin pasar por el área de preparación. |
| **git reset HEAD** | \<dir> | Deshace la operación de preparación. |
| **git commit --amend** | | Deshace la operación de confirmación. |
| **git status** | | Identifica el estado de un archivo o archivos en un repositorio local. |
| **git checkout --** | \<dir> | Descarta los cambios de un archivo de trabajo recuperando una versión almacenada en el repositorio local. |
| **git branch** | | Muestra las ramas existentes en un repositorio local. |
| **git branch** | \<nombre_rama> | Crea una rama en un repositorio local. |
| **git branch -d** | \<nombre_rama> | Elimina una rama del repositorio local. |
| **git switch** | \<nombre_rama> | Cambia de rama en la copia local. |
| **git checkout -b** | \<nombre_rama> | Crea una rama y cambia a ella sin realizar un commit en la rama master. |

## 2.3. Control de versiones centralizado

Git también permite el control de versiones centralizado, donde un servidor central alberga el repositorio principal y los colaboradores clonan y sincronizan sus copias locales con él.

### 2.3.1. Configuración de Git para trabajar a través de un proxy

Para configurar un proxy global para todos los repositorios, puedes usar los siguientes comandos:

```bash
git config --global http.proxy http://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
git config --global https.proxy https://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
```

Para configurar un proxy para un dominio específico:

```bash
git config --global http.<http://domain.com>.proxy http://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
git config --global https.<https://domain.com>.proxy https://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
```

### 2.3.2. Clonar un repositorio remoto localmente

Para clonar un repositorio remoto en tu máquina local, puedes usar el siguiente comando:

```bash
git clone <url>
```

### 2.3.3. Clonar un repositorio local en un servidor remoto

Para replicar tu repositorio local en un servidor remoto, puedes usar los siguientes comandos:

```bash
git remote add <remote> <url>
git push <remote> main
```

### 2.3.4. Traer cambios de un repositorio remoto a un repositorio local

Para traer los cambios de un repositorio remoto a tu repositorio local, puedes usar el siguiente comando:

```bash
git pull
```

### 2.3.5. Resolver conflictos al traer cambios

Si al realizar `git pull` tienes cambios en tu repositorio local que coinciden con cambios realizados en el repositorio remoto, se generará un conflicto. Para resolver este conflicto, tienes dos opciones:

1. Subir tus cambios a otra rama y luego realizar un pull request donde puedes solucionar los conflictos manualmente.
2. Realizar un `commit` de tus cambios y volver a ejecutar el comando `git pull` para que se ejecute el solucionador de conflictos que incluye Git.

### 2.3.6. Enviar cambios de un repositorio local a uno remoto

Para enviar los cambios de tu repositorio local a un repositorio remoto, puedes usar el siguiente comando:

```bash
git push -u origin main
```

### 2.3.7. Enviar una rama local al remoto

Para enviar una rama local al repositorio remoto, puedes usar el siguiente comando:

```bash
git push origin <rama>
```

### 2.3.8. Incorporar cambios del repositorio remoto a ramas locales

Existen diferentes métodos para incorporar los cambios que se producen en el repositorio remoto a tus ramas locales:

1. `git pull --all`: Este comando incorpora los cambios de todas las ramas en el repositorio remoto.
2. `git switch <rama> && git pull`: Este comando te permite cambiar a una rama local específica y traer los cambios.
3. `git switch <rama> && git fetch`: Este comando te permite cambiar a una rama local específica y traer los cambios sin iniciar un merge si hubiera conflictos.

### 2.3.9. Realizar un Pull Request entre dos ramas de un repositorio remoto

Una vez que hayas subido tus cambios a tu rama de desarrollo, puedes hacer un pull request de la siguiente manera:

1. Cuando ingreses en tu repositorio a través de GitHub, aparecerá un botón que dice _"Compare & pull request"_. Haz clic en él.
2. Esto te llevará al apartado de comparar cambios. En esta parte, es muy importante seleccionar bien la rama base en la que se van a introducir los cambios.
3. Una vez que hayas escogido la rama adecuada, se te avisará si se pueden incluir los cambios automáticamente o si es necesario resolver algún conflicto.
4. En caso de que haya conflictos, aparecerá un botón que te permitirá entrar en un editor donde puedes solucionarlos manualmente.
5. Una vez que hayas solucionado los conflictos (si los había), puedes hacer clic en el botón verde que dice _"Create pull request"_ y ya tendrás tu pull request solicitado.

## 2.4. Control de versiones distribuido

Git es un sistema de control de versiones distribuido que permite a los equipos de desarrollo colaborar en proyectos de software. Aquí te dejo una tabla con algunos de los comandos más utilizados en Git para el control de versiones distribuido:

### 2.4.1. Operaciones con Git Bash

| Comando | Argumentos | Función |
| --- | --- | --- |
| **git branch** | \<branch_name> | Crea una nueva rama en el repositorio local. |
| **git checkout** | \<branch_name> | Cambia a la rama especificada en el repositorio local. |
| **git push** | \[-u] \<remote> \<branch> | Envía la rama especificada al repositorio remoto. |

### 2.4.2. Operaciones desde GitHub

| Operación | Descripción |
| --- | --- |
| **Pull Request** (entre ramas) | En la página principal del repositorio, selecciona "New pull request" y elige la rama deseada. |
| **Pull Request** (entre repositorios) | Dentro de la misma opción anterior, selecciona "compare across forks". |
