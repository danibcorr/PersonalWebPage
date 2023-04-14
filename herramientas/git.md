---
description: >-
  Conceptos básicos sobre la herramienta Git. Contribuyentes @AsuncionBueneke,
  @iamcay y @LuisMiguelCG en GitHub.
---

# Git

## 1. Conceptos mínimos sobre el control de versiones

### **1.1. En qué consiste el control de versiones**

Es un sistema que registra los cambios que ha sufrido un fichero, de manera que se pueda recuperar cualquier versión pasada si fuera necesario.

### _**1.2. Conceptos**_

* _**REPOSITORIO LOCAL (Local Repository)**_: Es una base de datos centralizado donde se guardan las distintas versiones de los ficheros sometidos a control de versiones.
* _**COPIA LOCAL (working copy)**_: Es la copia que hacen los usuarios de un fichero sometido a control de versiones. El directorio local (working directory/working tree/workspace) es el que contiene todas las copias locales.
* _**REPOSITORIO REMOTO (Remote Repository)**_: Los repositorios remotos son versiones de nuestros proyectos que están hospedadas en Internet o en cualquier otra red.
* _**HISTÓRICO (LOG)**_: Registro de todos los cambios que se han producido en el repositorio. Es responsabilidad del cliente añadir información al log cuando se produce un cambio.
* _**CONFLICTO**_: se crean cuando dos desarrolladores han cambiado las mismas líneas en un archivo, o si un desarrollador eliminó un archivo mientras otro lo estaba modificando. En estos casos, Git no puede determinar automáticamente qué es correcto.

### _**1.3. Estados de un fichero**_

* _**SIN SEGUIMIENTO**_: significa que Git ve un archivo que no estaba en la instantánea anterior. Git no empezará a incluirlo en las confirmaciones de tus instantáneas hasta que se lo indiques explícitamente. Lo hace para que no incluyas accidentalmente archivos binarios generados u otros archivos que no tenías intención de incluir.
* _**CONFIRMADO**_: significa que los datos están almacenados de manera segura en tu base de datos local.
* _**MODIFICADO**_: significa que has modificado el archivo pero todavía no lo has confirmado a tu base de datos.
* _**PREPARADO**_: significa que has marcado un archivo modificado en su versión actual para que vaya en tu próxima confirmación
* _**IGNORADO**_: Un archivo que se le ha indicado explícitamente a Git que ignore. Los archivos ignorados suelen ser artefactos de compilación y archivos generados por el equipo que pueden derivarse de tu fuente de repositorios o que no deberían confirmarse por algún otro motivo.

### _**1.4. Operaciones con Git**_

* **CLONE**: hace un clon o copia local de un repositorio remoto
* **ADD**: añade contenido del directorio de trabajo al área de ensayo (staging area o 'index') para la próxima confirmación.
* **COMMIT**: toma todos los contenidos de los archivos a los que se les realiza el seguimiento con git add y registra una nueva instantánea permanente en la base de datos y luego avanza el puntero de la rama en la rama actual.
* **PUSH**: se utiliza para comunicar con otro repositorio, calcular lo que tu base de datos local tiene que la remota no tiene, y luego subir (push) la diferencia al otro repositorio. Se requiere acceso de escritura al otro repositorio y por tanto normalmente se autentica de alguna manera.
* _**PULL**_: se emplea para extraer y descargar contenido desde un repositorio remoto y actualizar al instante el repositorio local para reflejar ese contenido.
* _**FORK**_: copiar un proyecto y partir de este, hacerle modificaciones. Cuando trabajamos con repositorios Git, supone hacer una copia exacta del proyecto, generando dos URL distintas.
* _**PULL REQUEST**_: solicitudes de integración, forma de contribuir a un proyecto grupal o de código abierto.

## 2. Conceptos sobre Git y GitHub

### 2.1. Comandos de git-bash

| Comando   | Argumentos           | Función                                                                                                                                                  |
| --------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **pwd**   |                      | Mostrar en qué directorio estamos.                                                                                                                       |
| **mkdir** | \<dir>               | Crear un directorio.                                                                                                                                     |
| **cd**    | \<dir>               | Cambiar de directorio.                                                                                                                                   |
| **ls**    | \[-l] \[-a]          | Mostrar la lista de ficheros de un directorio. Si utilizamos **ls -l** mostrará una lista detallada y si utilizamos **ls -a** incluirá ficheros ocultos. |
| **rm**    | \<fichero>           | Borrar un fichero.                                                                                                                                       |
| **mv**    | \<origen> \<destino> | Cambiar (mover) un fichero de directorio.                                                                                                                |

### 2.2. Control de versiones local

|         Comando        |    Argumentos   |                                                           Función                                                          |
| :--------------------: | :-------------: | :------------------------------------------------------------------------------------------------------------------------: |
|      **git init**      |                 |                                       Crear un repositorio local en nuestra máquina.                                       |
|      **git clone**     |      \[url]     |                                             Copia un repositorio ya existente.                                             |
|       **git add**      |      \<dir>     |                               Preparar ficheros para ser confirmados en un repositorio local.                              |
|    **git commit -m**   |     'texto'     |                                         Confirmar cambios en un repositorio local.                                         |
|  **git commit -a -m**  |     'texto'     |                       Confirmar cambios en un repositorio local sin pasar por el área de preparación.                      |
|   **git reset HEAD**   |      \<dir>     |                                             Deshacer la operación de preparar.                                             |
| **git commit --amend** |                 |                                             Deshacer la operación de confirmar.                                            |
|     **git status**     |                 |                           Identificar el estado de un fichero o ficheros en un repositorio local.                          |
|   **git checkout --**  |      \<dir>     | Descartar los cambios de un fichero de trabajo mediante la recuperación de una versión almacenada en el repositorio local. |
|     **git branch**     |                 |                                    Muestra las ramas existentes en un repositorio local.                                   |
|     **git branch**     | \<nombre\_rama> |                                           Crear una rama en un repositorio local.                                          |
|    **git branch -d**   | \<nombre\_rama> |                                           Elimina una rama del repositorio local.                                          |
|     **git switch**     | \<nombre\_rama> |                                             Cambiar de rama en la copia local.                                             |
|   **git checkout -b**  | \<nombre\_rama> |                           Crea una rama y cambia a ella sin realizar un commit en la rama master.                          |

### 2.3. Control de versiones centralizado

#### 2.3.1. Configurar git para que trabaje tras un proxy

Para configurar un proxy global para todos los repositorios:

```bash
git config --global http.proxy http://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
git config --global https.proxy https://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
```

Para configurarlo en un dominio en especifico:

```bash
git config --global http.<http://domain.com>.proxy http://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
git config --global https.<https://domain.com>.proxy https://<proxyUsername>:<proxyPassword>@<proxy.server.com>:<port>
```

#### 2.3.2. Replicar un repositorio remoto localmente en nuestra máquina

```bash
git clone <url>
```

#### 2.3.3. Replicar un repositorio local en un servidor remoto

```bash
git remote add <remote> <url>
git push <remote> main
```

#### 2.3.4. Traer los cambios de un repositorio remoto a un repositorio local

```bash
git pull
```

#### 2.3.5. Resolver los conflictos que se puedan producir al traerse estos cambios

Al realizar `git pull`, si tenemos cambios en nuestro repositorio local que coinciden con cambios efectuados en el repositorio remoto, estos generaran un conflicto. Para solucionar este conflicto tenemos dos caminos:

1. Subir nuestros cambios a otra rama y despues realizar un pull request donde podemos solucionar dichos conflictos manualmente.
2. Realizar un `commit` de nuestros cambios y volver a ejecutar el comando `git pull` para que se ejecute el solucionador de conflictos que incluye git.

#### 2.3.6. Enviar los cambios de un repositorio local a uno remoto

```bash
git push -u origin main
```

#### 2.3.7. Enviar una rama local al remoto

```bash
git push origin <rama>
```

#### 2.3.8. Incorporar a ramas locales cambios que se producen en el repositorio remoto

Para realizar esta acción tenemos diferentes métodos:

1. `git pull --all` : incorpora los cambios de todas las ramas en el repositorio remoto.
2. `git switch <rama> && git pull`: cambiar a una rama local especifica y traerse los cambios.
3. `git switch <rama> && git fetch`: cambiar a una rama local especifica y traerse los cambios sin iniciar un merge si hubiera conflictos.

#### 2.3.9. Realizar un pull request entre dos ramas de un repositorio remoto.

Una vez tengamos subidos nuestros cambios a nuestra rama de desarrollo, podremos hacer un pull request de la siguiente manera:

1. Cuando ingresemos en nuestro repositorio a traves de github nos aparecera un botón que pone _"Compare & pull request"_, y le haremos click.
2. Esto nos llevara al apartado de comparar cambios. En esta parte es muy importante seleccionar bien la rama base en la que se van a introducir los cambios.
3. Una vez escogida la rama adecuada nos avisará si se pueden incluir los cambios automáticamente o es necesario resolver algun conflicto.
4. En el caso que haya conflictos, nos aparecerá un botón el cual nos permite entrar en un editor donde podemos solucionarlos manualmente.
5. Una vez solucionados los conflictos (si los había), podemos clickar en el botón verde que pone _"Create pull request"_ y ya tendremos nuestro pull request solicitado.

Por ultimo, quedaría que el dueño del repositorio o algún usuario con los permisos necesarios validase los cambios y aceptara el pull request.

### 2.4. Control de versiones distribuido

Operaciones con Git Bash:

| Comando          | Argumentos                | Función                                      |
| ---------------- | ------------------------- | -------------------------------------------- |
| **git branch**   | \<branch\_name>           | Crea una rama nueva en el repositorio local. |
| **git checkout** | \<branch\_name>           | Cambia de rama en el repositorio local.      |
| **git push**     | \[-u] \<remote> \<branch> | Envía la rama al repositorio remoto.         |

Operaciones desde Github:

| Operacion                             | Descripción                                                                                |
| ------------------------------------- | ------------------------------------------------------------------------------------------ |
| **pull request** (entre ramas)        | En la página principal del repositorio: "New pull request" y se selecciona la rama deseada |
| **pull request** (entre repositorios) | Dentro de la misma opción anterior, seleccionando: "compare across forks"                  |

Hay que tener en cuenta a la hora de hacer un Pull Request desde un repositorio al que se ha hecho un fork de seleccionar el repositorio nuestro, no el del profesor. De lo contrario, todos los Pull Request aparecerán en su repositorio y no en el nuestro.
