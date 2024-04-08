---
description: Realizado por Daniel Bazo Correa.
---

## 1. Teoría

Las imágenes de contenedores son más livianas que las máquinas virtuales, ya que no incluyen un sistema operativo completo.

En el caso de querer brindar servicios web, requerimos tanto un servidor como una base de datos. Los contenedores ofrecen una solución eficaz para implementar estos servicios en entornos de prueba y producción. Se recomienda utilizar un contenedor separado para el servidor web y otro para la base de datos, esto facilita las labores de mantenimiento. Además, es importante configurar la persistencia de los contenedores Docker para garantizar que tengan acceso a un espacio de almacenamiento de datos consistente.

Al proporcionar infraestructura como servicio (IaaS), es fundamental considerar la infraestructura necesaria para alojar la totalidad del servicio. Esto es precisamente lo que realizan los proveedores de servicios de infraestructura, ofreciendo soluciones IaaS que abarcan desde la implementación de contenedores hasta la gestión de recursos y la garantía de disponibilidad del servicio.

### 1.2. Comandos útiles

|                                      Comando                                      |                                                                                                                                                                                                                                    Uso/función                                                                                                                                                                                                                                   |
| :-------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|            **docker run -d -p 8080:80 -i --name Debian debian:latest**            | Crear un contenedor para alojar un servicio y publicarlo en un puerto del host para que sea accesible. Donde: Debian es el nombre del contenedor, debian:latest es la imagen del contenedor, 8080 es el puerto del host, 80 el puerto del contenedor, -d ejecuta el contenedor en segundo plano e imprime el ID del contenedor, -p publica el puerto(s) de un contenedor al host, -i mantiene el STDIN abierto aunque no este conectado y --name asigna un nombre al contenedor. |
|                               **docker network ls**                               |                                                                                                                                                                                                                 Comprobamos las interfaces disponibles en Docker.                                                                                                                                                                                                                |
|                          **docker rm nombre\_contenedor**                         |                                                                                                                                                                                                                          Borrar un contenedor de Docker.                                                                                                                                                                                                                         |
|                                  **docker ps -a**                                 |                                                                                                                                                                                                       Ver los contenedores que tenemos en el equipo, activos y no activos.                                                                                                                                                                                                       |
|                                   **docker ps**                                   |                                                                                                                                                                                                                        Ver solo los contenedores activos.                                                                                                                                                                                                                        |
|                        **docker start nombre\_contenedor**                        |                                                                                                                                                                                                                                Iniciar contenedor.                                                                                                                                                                                                                               |
|                         **docker stop nombre\_contenedor**                        |                                                                                                                                                                                                                                 Parar contenedor.                                                                                                                                                                                                                                |
|                    **docker exec -it nombre\_contenedor bash**                    |                                                                                                                                                                                                                   Abrir un terminal de linux en el contenedor.                                                                                                                                                                                                                   |
|                       **docker network inspect nombre\_red**                      |                                                                                                                                                                                                                         Conocer la IP de los contenedor.                                                                                                                                                                                                                         |
|                       **docker network inspect nombre\_red**                      |                                                                                                                                                                                   Permite inspeccionar, en tiempo de ejecución, qué contenedores pertenecen a una red virtual Docker concreta.                                                                                                                                                                                   |
|                        **docker stats nombre\_contenedor**                        |                                                                                                                                                                                           Monitorizar el consumo de CPU, memoria y ancho de banda de un contenedor Docker en ejecución.                                                                                                                                                                                          |
| **docker cp rutas\_archivos\_host nombre\_contenedor:ruta\_archivos\_contenedor** |                                                                                                                                                                                                                           Pasar archivos al contenedor.                                                                                                                                                                                                                          |
|               **docker update \[OPTIONS] CONTAINER \[CONTAINER...]**              |                                                                                                                                              Actualizar la configuración de uno o varios contenedores. [https://docs.docker.com/engine/reference/commandline/update/](https://docs.docker.com/engine/reference/commandline/update/)                                                                                                                                              |

### 1.3. Práctica

**¿Cuál es la finalidad del modo bridge en Docker? ¿Qué necesitas para que grupos de contenedores estén aislados entre sí, dentro de un mismo demonio Docker?**

> El modo bridge permite a un contenedor que sea accesible desde otro contenedor y el host, pero no desde el exterior.

**Ejecuta dos contenedores conectados por un bridge y comprueba si se pueden comunicar en red. Ejecuta dos contenedores conectados a bridges diferentes y comprueba su conectividad.**

> **Para el mismo bridge**
>
> Primero descargamos Docker. En Windows Docker se instala bajo WSL. Una bez instalado descargamos dos contenedores cualquiera, o podemos utilizar el mismo contenedor pero en 2 instancias diferentes, que será lo que haremos. Todos los comandos se ejecutarán desde el terminal del Sistema Operativo Host:
>
> 1.  Comprobamos las interfaces disponibles en Docker con el comando:
>
>     ```scala
>     docker network ls
>     ```
> 2.  Podemos crear una nueva conexión de red con el driver bridge ejecutando el siguiente comando:
>
>     ```scala
>     docker network create -d bridge nombre_red
>     ```
> 3.  Al ejecutar el comando del paso 1 veremos la nueva red creada. Para crear un contenedor que use dicha red creada podemos utilizar el comando siguiente:
>
>     ```scala
>     docker create --name nombre_contenedor --network nombre_red --publish 8081:80 nginx:latest
>     ```
>
>     Del comando anterior nginx:latest es una imagen que se descargará en el caso de no estar ya disponible en el equipo.
> 4.  Para iniciar el contenedor utilizamos el comando siguiente:
>
>     ```scala
>     docker start nombre_contenedor
>     ```
> 5.  Para poder ver los contenedores que se están ejecutando podemos utilizar el comando:
>
>     ```scala
>     docker ps
>     ```
> 6. Ahora vamos a crear otro contenedor con la misma imagen pero utilizando un puerto diferente, para ello utilizamos el mismo comando que en el paso 3 cambiando el nombre y el puerto. Y lo iniciamos.
> 7.  Para abrir un terminal y ejecutar comandos para debug y testeo desde cada contenedor utilizamos el comando siguiente:
>
>     ```scala
>     docker exec -it nombre_contenedor bash
>     ```
>
>     Hacemos lo mismo para los dos contenedores.
> 8.  En caso de que no reconozca el comando `ping` es porque la imagen no contiene los paquetes mínimos, en ese caso instalamos los paquetes utilizando el comando:
>
>     ```scala
>     apt update
>     apt install -y iputils-ping
>     apt install -y nano net-tools ifupdown
>     ```
> 9.  Para conocer la IP de los contenedor podemos ejecutar el comando siguiente:
>
>     ```scala
>     docker network inspect nombre_red
>     ```
>
>     Con ello podemos saber la IP y hacer un `ping` desde el terminal de uno de los contenedores al otro y veremos que funciona. Incluso, podríamos hacer un ping de un contenedor a otro utilizando el nombre del contenedor.
>
> **Para distintos bridge**
>
> 1. Creamos un nuevo bridge con el mismo comando que el paso 2 para un solo bridge.
> 2.  Podemos modificar las configuraciones de los contenedores que hemos creado antes para no crear unos nuevos. Para ello, podemos **ver los contenedores que tenemos en el equipo (activos y no activos)** con el comando:
>
>     ```scala
>     docker ps -a
>     ```
> 3.  Tenemos que desconectar el contenedor del bridge definido, para ello utilizamos el comando:
>
>     ```scala
>     docker network disconnect nombre_red nombre_contenedor
>     ```
>
>     Donde el parámetro `nombre_red` es el nombre de la red con el driver de bridge creado y `nombre_contenedor` el nombre del contenedor creado anteriormente.
> 4.  Ahora conectamos ese contenedor al nuevo bridge con el comando:
>
>     ```scala
>     docker network connect nombre_red nombre_contenedor
>     ```
>
>     Si inicializamos los contenedores e inspeccionamos la interfaz de red de uno de los bridges creados veremos que ahora solo hay un docker en cada bridge.
>
>     Al intentar hacer un ping no se podrá ya que no es accesible.
> 5.  Podemos parar el contenedor con el comando:
>
>     ```scala
>     docker container stop nombre_contenedor
>     ```

**¿Se puede hacer port forwarding en Docker?**

> Sí, podemos publicar los puertos de un contenedor para que sea accesible desde fuera, aunque este proceso no es seguro. Por ello, podemos publicarlo para que sea accesible unicamente desde el Host utilizando el comando:
>
> ```scala
> docker run -p 127.0.0.1:8080:80 nginx
> ```

**¿Cual es el equivalente al modo de red de tipo "host" de Docker en VirtualBox?**

> Según la documentación de Docker sobre el modo de red host: “Si utilizas el modo de red de host para un contenedor, la pila de red de ese contenedor no está aislada del host Docker (el contenedor comparte el espacio de nombres de red del host), y el contenedor no tiene asignada su propia dirección IP. Por ejemplo, si ejecutas un contenedor que se enlaza al puerto 80 y utilizas la red de host, la aplicación del contenedor estará disponible en el puerto 80 de la dirección IP del host. Dado que el contenedor no tiene su propia dirección IP cuando se utiliza el modo host de red, el mapeo de puertos no tiene efecto, y las opciones -p, --publish, -P, y --publish-all son ignoradas, produciendo en su lugar una advertencia”
>
> El equivalente será el adaptador sólo-anfitrión (Host-only Adapter).

**Los logs son herramientas para gestionar las incidencias de Docker y sus contenedores. a) ¿Tiene Docker alguna forma de activar logs? ¿Qué grado de configuración presenta?, b) ¿Es posible establecer logs rotatorios (son aquellos con un tamaño máximo, que impide desbordar recursos de almacenaje)?, y c) ¿Es posible almacenar los logs en la nube?.**

> a) Sí, podemos ver la información del log utilizando el comando:
>
> ```scala
> docker logs nombre_contenedor
> ```
>
> b) Sí. Primero, saber que los logging drivers son mecanismos para registrar información de contenedores. Cada Docker tiene su propio logging driver por defecto al menos que se configure uno. Por defecto, no se realiza ninguna rotación de logs, como resultado los archivos de registro almacenados pueden ocupar mucho espacio en disco. Hay que hacer copias de seguridad, truncarlo, para dar espacio a nueva información. Ese tamaño se ellige por ensallo y error. Cuando se llega al máximo de ese fichero se va al siguiente fichero, y cuando se llega al último fichero se machaca el primero. [JSON File logging driver | Docker Docs](https://docs.docker.com/config/containers/logging/json-file/)
>
> ```scala
> {
>   "log-driver": "json-file",
>   "log-opts": {
>     "max-size": "10m",
>     "max-file": "3" 
>   }
> }
> ```

**a). ¿Cómo se asignan procesadores core y gpus a un contenedor?, b). ¿Cómo se asigna la memoria de un contenedor?, y c). ¿Existe una forma nativa en Docker para asignar ancho de banda? ¿Hay alguna alternativa?.**

> a) Para asignar núcleos de un procesador a un contenedor de Docker podemos utilizar la opción **`--cpuset-cpus`**. Por ejemplo, **`docker run --cpuset-cpus="0-2" ubuntu`** asignará los cores 0, 1 y 2 al contenedor1.
>
> En el caso de las GPU de NVIDIA, se requiere instalar primero nvidia-container-runtime y utilizar la opción **`--gpus`** , por ejemplo **`docker run -it --rm --gpus all ubuntu nvidia-smi`** permite utilizar todas las gráficas disponibles mientras que **`docker run -it --rm --gpus '"device=0,2"' nvidia-smi`** permite utilizar las gráficas de la posición 0 y 3. Docker no tiene, hasta la fecha, soporte nativo para gráficas de AMD.
>
> b) Para asignar memoria a un contenedor Docker, podemos usar la opción `-m` o `--memory` en el comando `docker run`. Por ejemplo, `docker run -m 300M ubuntu` limitará la memoria del contenedor a 300MB.
>
> c) Docker no proporciona una forma nativa para limitar el ancho de banda de red de un contenedor. Sin embargo, puedes usar herramientas externas como `tc` (Traffic Control) en Linux para controlar el ancho de banda.

**Imagina que vas a montar una infraestructura web con LAMPP o XAMPP (que tiene en servidor Apache y una base de datos Mysql). ¿Elegirías ejecutar toda la infraestructura en el mismo contenedor o separarías cada servicio en su propio contenedor?.**

> En la mayoría de los casos, **es preferible separar cada servicio en su propio contenedor**, algunas razones son:
>
> 1. **Aislamiento**: Cada contenedor se ejecuta de forma aislada, lo que significa que si un servicio falla, no afectará a los demás servicios.
> 2. **Escalabilidad**: Si tienes cada servicio en su propio contenedor, puedes escalar cada servicio de forma independiente según sea necesario.
> 3. **Reutilización y mantenimiento**: Los contenedores individuales pueden ser reutilizados en diferentes entornos y es más fácil de mantener y actualizar.
> 4. **Seguridad**: Si un contenedor se ve comprometido, el atacante no tendrá acceso a los otros servicios.

**Asignar un volumen en Docker para crear persistencia en elos contenedores.**

> Con el fin de almacenar datos en el contenedor e intalar paquetes en el, sería una buena idea crear un volumen para dotar de persistencia al contenedor con el fin de que todo lo que se esté haciendo quede almacenado. Decir que el espacio asignado a un volumen de Docker no tiene un límite predefinido y no está directamente relacionado con el espacio en disco de tu sistema. El espacio disponible para un volumen se gestiona de forma dinámica y depende de diversos factores, incluyendo la configuración del sistema y el espacio en disco disponible en el host.
>
> Para ello, lo primero es parar el contenedor con el comando siguiente:
>
> ```scala
> docker stop Debian
> ```
>
> Creamos el volumen con el siguiente comando:
>
> ```scala
> docker volume create NOMBRE_DEL_VOLUMEN
> ```
>
> Yo lo he llamado `**ServerDisk`.\*\*
>
> Una vez creado el volumen lo asignamos al contenedor, si no tuviesemos el contenedor creado utilizariamos el comando siguiente:
>
> ```scala
> docker run -d -p 8080:80 -i -v ServerDisk:/mnt/ --name Debian debian:latest
> ```
>
> **Si el contenedor ya esta creado** tenemos que utilizar el comando **`docker update`** para actualizar los parámetros del contenedor. Sin embargo, no existe ninguna opción para asignarle un volumen así que borraremos el contenedor y lo crearemos de nuevo. con el comando anterior.
>
> Para poder acceder al terminal de linux del contenedor utilizamos el comando siguiente:
>
> ```scala
> docker exec -it Debian bash
> ```

**Automatizaciones con Dockerfile.**

> Con el fin de automatizar el proceso de arrojar un servicio en un contenedor, en este caso un servidor web, vamos a crear desde el host un fichero **Dockerfile** que posteriormente podremos compilar con el fin de crear una imagen de Docker y que todo el proceso sea automático.
>
> Lo primero, desde el host creamos un dichero llamado Dockerfile sin extensión, editándolo por ejemplo con el bloc de notas, y escribimos:
>
> ```docker
> # El FROM define la imagen base utilizada
> FROM debian:latest
>
> # El MAINTAINER permite añadir informacion
> MAINTAINER Daniel
>
> # WORKDIR especifica el directorio desde el que se van a ejecutar las ordenes
> WORKDIR /app
>
> # COPY permite Copia archivos o directorios desde la máquina local 
> # (donde esta instalado docker) al contenedor Docker.
> COPY servidor.py /app/
> COPY requirements.txt /app/
>
> # RUN permite ejecutar comandos
> RUN apt-get update && apt-get install 
> RUN apt-get install -y python3
> RUN apt-get install -y python3-pip
> RUN pip install --trusted-host pypi.python.org -r requirements.txt --break-system-packages
>
> # EXPOSE indica (no expone) el puerto del contenedor
> # Útil para que los puertos no se expongan aleatoriamente.
> # Es complementario a docker run -p. Si es -p (minúscula) tienes que 
> # indicar puerto entrada:puerto salida. 
> # Si es -P (mayúscula) el de salida es fijo y el de entrada aleatorio.
> # También, si solo usas EXPOSE y al hacer run no especificas ni -p ni -P lo que va a 
> # pasar es que esos puertos solo sean accesibles desde otros contenedores, no desde el exterior.
> # Se puede especificar también si es TCP o UDP. Por defecto es TCP.
> EXPOSE 80
> EXPOSE 8080
>
> # En CMD el comando que se especifique a continuación, 
> # se ejecutara cuando haga docker run si no se especificar otro comando.
> CMD python3 servidor.py
> ```
>
> La **`-y`** de **`RUN apt-get install -y python3`** es para indicar **yes** a la hora de instalar los paquetes. **En CMD se debería dejar el comando que va a dejar en constante funcionamiento al contenedor, de no ser así, realizada la ejecución el contenedor se cerrará.**
>
> En el directorio donde se encuentra este fichero Dockerfile escribimos el comando siguiente en el terminal del host:
>
> ```docker
> docker build -t servicioweb .
> ```
>
> Donde **servicioweb** es el nombre de la imagen.
>
> Si ejecutamos el comando **`docker image ls`** debería aparecer la nueva imagen creada, por lo que podríamos crear el contenedor docker utilizando dicha imagen con el comando siguiente:
>
> ```docker
> docker run -d -p 8080:80 -i -v ServerDisk:/mnt/ --name Servidor servicioweb
> ```

**Combinar los servicios de varios contenedores para que trabajen en conjunto.**

> Por ejemplo, el servidor que hemos alojado en el contenedor mediante el proceso anterior cuenta con un número de visitas que emplea el servicio de _redis._ Para crear el contenedor redis y actualizar el número de visitas, realizaremos los pasos siguientes.
>
> Primero creamos un contenedor de Docker con la imagen de redis, para ello podemos utilizar el comando:
>
> ```docker
> docker run -d -i --name DBRedis redis
> ```
>
> **Para que ambos contenedores**, el Servidor que utiliza Flask y el contendor de redis, **se puedan comunicar es necesario que estén en la misma red.** Para ello podemos inicializar ambos contenedores con el comando **`docker start DBRedis Servidor`** para posteriormente, o crear una nueva red, o conectar los contenedores a una red existente.
>
> Para crear la red utilizamos el comando:
>
> ```docker
> docker network create -d bridge NOMBRE_RED
> ```
>
> En este caso ya se tenía una red creada, llamada **`lan0`** así que **conectaremos los contenedores a la misma red**. Para ello, y con los contenedores activos, utilizamos el comando:
>
> ```docker
> docker network connect lan0 DBRedis
> docker network connect lan0 Servidor
> ```
>
> Al escribir el comando `**docker network inspect lan0`\*\* veremos que ambos contenedores se encuentran en la misma red con diferentes IP.
>
> Ahora, tenemos que modificar el ficero **`servidor.py`** del contenedor Servidor. Para ello, entramos al terminal del contenedor y modificamos la línea **`redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)`** por la IP del contenedor de Redis, en este caso la 172.18.0.2, quedando tal que así **`redis = Redis(host="172.18.0.2", db=0, socket_connect_timeout=2, socket_timeout=2)` .**
>
> Detenemos los contenedores con el comando **`docker stop DBRedis Servidor`** y los iniciamos de nuevo con el comando **`docker start DBRedis Servidor` ,** así iniciaremos primero el contenedor donde se encuentra Redis y luego el servidor en si.

**Despliegue de varios contenedores de forma simultanea utilizando Dockercompose.**

> Para poder ejecutar los dos contenedores al mismo tiempo podemos crear un fichero Dockercompose. Para ello, desde el mismo directorio donde se encontraba nuestro Dockerfile podemos crear un nuevo fichero llamado **`docker-compose.yml` .**
>
> En dicho fichero escribimos lo siguiente:
>
> ```docker
> version: '3'
>
> services:
>
>   flask:
>
>     build: .
>
>     image: servicioweb
>
>     ports:
>
>       - "8080:80"
>
>     depends_on:
>
>       - redis
>
>   redis:
>
>     image: redis:latest
> ```
>
> Indicamos en este fichero los servicios que vamos a utilizar, con **`build`** podemos indicar donde se encuentra el Dockerfile con la configuración para ese contenedor. Como hemos creado anteriormente un imagen (servicioweb) con su Dockerfile para automatizar la instalación de paquetes, pues podemos hacerlo tal y como se indica. Pero dicho contenedor depende de otro, del contenedor que tiene el servicio de redis.
>
> En este caso, dicho contenedor no requiere ninguna configuración extra, por lo que podemos directamente utilizar la imagen que existe en el hub de Docker.
>
> Algunos de los comandos que podemos utilizar ahora son:
>
> * **`docker-compose up`**: Da instrucciones a Docker para crear el contendor y ejecutarlo.
> * **`docker-compose down`**: Apaga todo los servicios que levantó con docker-compose up.
> * **`docker-compose ps`**: Permite ver los contenedores funcionando.
> * **`docker-compose exec`**: Permite ejecutar un comando a uno de los servicios levantados de Docker-compose.