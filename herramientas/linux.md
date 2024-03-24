<div align="justify">

# Linux

## Linux

Los comandos pueden variar según la distribución de Linux. En este caso, se está utilizando PopOS, basado en Ubuntu (Debian).

### Instalar drivers de Nvidia

Los pasos a seguir son:

1. Descargamos los drivers directamente desde la web de Nvidia.
2. Descargado el fichero, tendremos que deshabilitar el uso del manejador del display. Para ello, colocamos en el terminal:

```
sudo systemctl isolate multi-user.target
```

3. Ahora debemos deshabilitar el driver de Nvidia:

```
modprobe -r nvidia-drm
```

4. A continuación nos dirigimos a la ubicación donde tenemos el fichero de instalación utilizando el comando `cd` junto con la dirección sin utilizar las comillas:

```
cd "directio_fichero"
```

5. Ejecutamos el fichero .run de la descarga del driver de Nvidia. Puede que el fichero esté comprimido, en ese caso habrá que descomprimirlo primero:

```
sudo sh NVIDIA-Linux-x86_64-$DRIVER_VERSION.run
```

6. Seguido los pasos durante la instalación de los drivers de Nvidia, inicializamos de nuevo el manejador del display:

```
sudo systemctl start graphical.target
```

7. Finalmente, reiniciamos el ordenador y comprobamos la instalación con el siguiente comando en el terminal:

```
nvidia-smi
```

</div>