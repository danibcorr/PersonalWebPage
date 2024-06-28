---
description: Realizado por Daniel Bazo Correa.
---

# Bibliografía

* [Aprende Docker ahora! curso completo gratis desde cero!](https://youtu.be/4Dko5W96WHg?si=pOAHHRxpPkqpQ2go)
  
# 1. Diferencia entre un contenedor y una máquina virtual

Las tecnologías de virtualización, como los contenedores y las máquinas virtuales, comparten algunos objetivos pero presentan diferencias significativas en su implementación y uso.

## 1.1. Contenedores

Un contenedor es una unidad de software que empaqueta una aplicación y todas sus dependencias, incluyendo archivos de configuración y variables de entorno, en un formato estándar. Esta característica permite que los contenedores sean portátiles y fáciles de compartir, optimizando el desarrollo y despliegue de aplicaciones y evitando problemas relacionados con versiones y dependencias.

Los contenedores se pueden almacenar en repositorios públicos o privados, como Docker Hub, que es un ejemplo destacado de repositorio público. Las imágenes de contenedores son significativamente más ligeras que las máquinas virtuales, ya que no incluyen un sistema operativo completo. En su lugar, los contenedores se basan en imágenes Linux que pueden soportar múltiples versiones simultáneamente, siendo su única dependencia el *runtime* de Docker.

Un contenedor se compone de múltiples capas de imágenes, donde la capa base suele ser una distribución ligera de Linux, como Alpine o Debian. Sobre esta base, se añaden las dependencias del código y los componentes específicos de la aplicación.

## 1.2. Máquinas virtuales

Una máquina virtual, por otro lado, virtualiza tanto la aplicación como el *kernel* del sistema operativo, lo que implica un mayor uso de recursos de memoria y almacenamiento en comparación con un contenedor. Cada máquina virtual incluye su propio sistema operativo completo, lo que resulta en un mayor consumo de recursos y tiempos de inicio más prolongados.

## 1.3. Comparación y usos

Docker, una plataforma de contenedores ampliamente utilizada, representa una forma de virtualización que se centra únicamente en la aplicación. A diferencia de las máquinas virtuales, Docker utiliza el kernel del sistema operativo anfitrión, resultando en una solución más ligera y eficiente.

En entornos de desarrollo y producción, los contenedores ofrecen ventajas significativas para la implementación de servicios web y bases de datos. En estos casos, se recomienda utilizar contenedores separados para el servidor web y la base de datos, lo que facilita el mantenimiento. Además, es crucial configurar la persistencia de los contenedores para garantizar el acceso a un almacenamiento de datos consistente.

En el contexto de la infraestructura como servicio (IaaS), los proveedores ofrecen soluciones que abarcan desde la implementación de contenedores hasta la gestión de recursos y la garantía de disponibilidad del servicio.

Herramientas como Docker Desktop permiten gestionar y ejecutar contenedores, acceder al sistema de archivos, utilizar la interfaz de línea de comandos (CLI) y Docker Compose, entre otras funcionalidades, facilitando el trabajo con contenedores en entornos de desarrollo. Estas herramientas son esenciales para aprovechar al máximo las ventajas de la virtualización basada en contenedores.

# 2. Comandos de Docker

| Comando | Uso/función |
|:-------:|:-----------:|
| **docker images** | Devuelve un listado de todas las imágenes descargadas en la máquina. |
| **docker pull nombre_imagen** | Descargar una imagen. Ejemplo: `docker pull nginx:version` para especificar la versión. |
| **docker image rm nombre_imagen:tag** | Eliminar una imagen. |
| **docker create nombre_imagen** | Crear un contenedor con esa imagen, devuelve el ID del contenedor creado. |
| **docker create --name nombre_contenedor nombre_imagen** | Crear un contenedor con un nombre específico a partir de una imagen. |
| **docker start ID_contenedor_creado** | Iniciar el contenedor. |
| **docker start nombre_contenedor** | Iniciar un contenedor utilizando su nombre. |
| **docker ps** | Ver solo los contenedores activos. Devuelve una tabla con Container-ID, Image, Command, Created, Status, Ports, y Names. |
| **docker ps -a** | Ver los contenedores en el equipo, activos y no activos. |
| **docker stop nombre_contenedor** | Parar un contenedor utilizando su nombre. |
| **docker stop ID_contenedor** | Parar un contenedor utilizando su ID. |
| **docker rm nombre_contenedor** | Borrar un contenedor de Docker. |
| **docker run -d -p 8080:80 -i --name Debian debian:latest** | Crear un contenedor para alojar un servicio y publicarlo en un puerto del host para que sea accesible. <br> - **Debian**: Nombre del contenedor <br> - **debian:latest**: Imagen del contenedor <br> - **8080**: Puerto del host <br> - **80**: Puerto del contenedor <br> - **-d**: Ejecuta el contenedor en segundo plano e imprime el ID del contenedor <br> - **-p**: Publica el puerto(s) de un contenedor al host <br> - **-i**: Mantiene el STDIN abierto aunque no esté conectado <br> - **--name**: Asigna un nombre al contenedor |
| **docker exec -it nombre_contenedor bash** | Abrir un terminal de Linux en el contenedor. |
| **docker cp ruta_archivos_host nombre_contenedor:ruta_archivos_contenedor** | Pasar archivos del host al contenedor. |
| **docker stats nombre_contenedor** | Monitorizar el consumo de CPU, memoria y ancho de banda de un contenedor en ejecución. |
| **docker network ls** | Listar las redes disponibles en Docker. |
| **docker network inspect nombre_red** | Inspeccionar la red virtual de Docker, conocer la IP y ver qué contenedores pertenecen a esa red. |
| **docker update [OPTIONS] CONTAINER [CONTAINER...]** | Actualizar la configuración de uno o varios contenedores. [Documentación Docker Update](https://docs.docker.com/engine/reference/commandline/update/) |

# 3. Mapeo de puertos

El mapeo de puertos, también conocido como ***Port Mapping***, es una técnica que permite asignar un puerto específico del host al puerto utilizado por un contenedor para aceptar peticiones. Esta funcionalidad facilita la comunicación entre varios contenedores y permite que las aplicaciones dentro de los contenedores sean accesibles desde el host o desde otros contenedores.

Por ejemplo, el siguiente comando crea un contenedor utilizando la imagen de MongoDB y mapea el puerto 27017 del host al puerto 27017 del contenedor:

```bash
docker container create -p27017:27017 --name mongodb mongo
```

En este comando:

- `-p`: Indica que se va a publicar el puerto. El primer número es el puerto del host y el segundo es el puerto del contenedor.
- `mongodb`: Es el nombre asignado al contenedor.
- `mongo`: Es la imagen del contenedor que se va a utilizar.

Además, Docker proporciona comandos para capturar los logs de los contenedores y verificar su funcionamiento:

- `docker logs "nombre_contenedor"`: Muestra los logs del contenedor.
- `docker logs -f "nombre_contenedor"`: Muestra los logs del contenedor de forma continua.

# 4. Docker Run

El comando `docker run` es una combinación de dos comandos de Docker: `docker create` y `docker start`. Este comando realiza tres pasos:

1. Busca la imagen especificada. Si no la encuentra en el sistema local, la descarga del repositorio.
2. Crea un contenedor a partir de la imagen.
3. Inicia el contenedor.

Por ejemplo, el siguiente comando ejecuta un contenedor de MongoDB, mapea el puerto 27017 del host al puerto 27017 del contenedor, y lo ejecuta en segundo plano:

```bash
docker run -d -p27017:27017 --name mongodb mongo
```

# 5. Conexión con los contenedores

Para conectar una base de datos con una aplicación en Docker, se utilizan variables de entorno para configurar el contenedor. Estas variables dependen de la imagen del contenedor que se esté utilizando.

Por ejemplo, para crear un contenedor de MongoDB con un nombre de usuario y una contraseña específicos, se pueden utilizar las siguientes variables de entorno:

```bash
docker create -e MONGO_INITDB_ROOT_USERNAME=dani -e MONGO_INITDB_ROOT_PASSWORD=clave
```

Estas son variables de entorno específicas de MongoDB que permiten configurar el nombre de usuario y la contraseña del administrador de la base de datos durante la inicialización del contenedor. Es importante tener en cuenta que las variables de entorno pueden variar dependiendo de la imagen del contenedor que se esté utilizando. Por lo tanto, siempre es recomendable consultar la documentación de la imagen para conocer las variables de entorno disponibles y cómo utilizarlas.
# 6. Dockerfile

Un `Dockerfile` es un archivo de texto que contiene las instrucciones necesarias para construir una imagen Docker, que luego puede ser utilizada para crear contenedores. Cada imagen se basa en una imagen previa, que puede ser una imagen oficial de Docker o una creada por el usuario.

Aquí tienes un ejemplo de un `Dockerfile`:

```dockerfile
FROM node:18  # Imagen base
RUN mkdir -p /home/app  # Crear carpeta para el código dentro del contenedor
COPY . /home/app  # Copiar archivos del host al contenedor
EXPOSE 3000  # Exponer puerto
CMD ["node", "/home/app/index.js"]  # Ejecutar aplicación
```

Para permitir la comunicación entre contenedores, es necesario agruparlos en una red interna, ya que por defecto están aislados. Docker proporciona comandos para gestionar estas redes:

- `docker network ls`: Lista todas las redes configuradas en Docker.
- `docker network create mi-nueva-red`: Crea una nueva red.

Los contenedores en la misma red interna de Docker pueden comunicarse entre sí utilizando el nombre del contenedor como dominio.

Para construir una imagen a partir de un `Dockerfile`, puedes utilizar el comando `docker build`:

```bash
docker build -t nombre-imagen:etiqueta ruta/dockerfile
```

Y para crear un contenedor y conectarlo a una red específica:

```bash
docker create -p27017:27017 --name mongodb --network mi-nueva-red
```

Docker ofrece varios modos de red para los contenedores:

- **Modo bridge**: Es el modo predeterminado y permite que la red sea reconocible solo dentro del host y el contenedor.
- **Red personalizada**: Permite especificar el rango de direcciones IP y otros parámetros.

# 7. Docker Compose

Docker Compose es una herramienta que permite definir y gestionar múltiples contenedores como un conjunto de servicios interconectados. Estos servicios se definen en un archivo llamado `docker-compose.yml`, que utiliza el formato YAML.

Aquí tienes un ejemplo de un archivo `docker-compose.yml`:

```yaml
version: "3.9"
services:
  mi-app:
    build: .  # Construye la imagen en la ruta actual
    ports:
      - "3000:3000"  # "puertoHost:puertoContenedor"
    links:
      - mongodb  # Indica el contenedor a integrar
  mongodb:
    image: mongo  # Imagen base
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=dani
      - MONGO_INITDB_ROOT_PASSWORD=clave
```

Para ejecutar los servicios definidos en `docker-compose.yml`, puedes utilizar el comando `docker compose up`. Y para detener y eliminar todos los servicios, incluyendo imágenes y contenedores, puedes utilizar el comando `docker compose down`. Estos comandos facilitan la gestión de aplicaciones multi-contenedor en Docker.

# 8. Volúmenes

Los volúmenes en Docker son una funcionalidad que permite crear persistencia en los datos de los contenedores. Esto es especialmente útil para preservar la información incluso si se elimina un contenedor. Los datos se almacenan en el equipo anfitrión.

Existen tres tipos de volúmenes:

1. **Anónimo**: Se indica la ruta que se desea montar, pero no se puede referenciar para que lo use otro contenedor.
2. **De anfitrión a host**: Se especifica qué carpeta montar y dónde montarla.
3. **Nombrado**: Similar al anónimo, pero permite referenciar el volumen al crear otro contenedor.

Para asignar los volúmenes, se realizan los cambios en `docker-compose.yml`:

Ejemplo de `docker-compose.yml` con volúmenes:

```yaml
version: "3.9"
services:
  mi-app:
    build: .
    ports:
      - "3000:3000"
    links:
      - mongodb
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=dani
      - MONGO_INITDB_ROOT_PASSWORD=clave
    volumes:
      - mongo-data:/data/db  # ruta que MongoDB usa para almacenar datos
volumes:
  mongo-data:
```

# 9. Ambientes y Hot Reload

Los diferentes ambientes permiten separar la configuración de desarrollo de la de producción. Para ello, se crean un fichero `Dockerfile.dev` y `docker-compose-dev.yml`.

Ejemplo de `Dockerfile.dev`:

```dockerfile
FROM node:18  # Imagen base
RUN mkdir -p /home/app  # Crear carpeta para el código dentro del contenedor
COPY package*.json /home/app/  # Copiar archivos necesarios
WORKDIR /home/app  # Establecer el directorio de trabajo
RUN npm install  # Instalar dependencias
COPY . /home/app  # Copiar el resto del código
EXPOSE 3000  # Exponer puerto
CMD ["npm", "run", "dev"]  # Ejecutar en modo desarrollo
```

Ejemplo de `docker-compose-dev.yml`:

```yaml
version: "3.9"
services:
  mi-app:
    build:
      context: .  # Define el contexto donde va a estar trabajando
      dockerfile: Dockerfile.dev  # Indica el Dockerfile de desarrollo
    ports:
      - "3000:3000"
    links:
      - mongodb
    volumes:
      - .:/home/app  # Define un volumen anónimo
  mongodb:
    image: mongo
    ports:
      - "27017:27017"
    environment:
      - MONGO_INITDB_ROOT_USERNAME=dani
      - MONGO_INITDB_ROOT_PASSWORD=clave
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:
```

Para ejecutar Docker Compose en el entorno de desarrollo, se utiliza el siguiente comando:

```bash
docker compose -f docker-compose-dev.yml up
```