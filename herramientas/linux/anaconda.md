# Anaconda

## Conda

Conda es un gestor de paquetes y de entornos para la programación.

### Actualizar todos los paquetes de Conda

```
conda update --all
```

### Añadir entornos en los cuadernos jupyter

1. Primero creamos un entorno:

```
conda create --name nombre_del_entorno
```

2. Activamos el entorno:

```
conda activate nombre_del_entorno
```

3. Actualizamos la versión de pip (pip es un gestor de paquete) a la última versión:

```
python3 -m pip install --upgrade pip
```

4. Instalados los paquetes necesarios en el entorno, instalamos ipykernel:

```
pip install ipykernel
```

5. Finalmente, agregamos el entorno:

```
python -m ipykernel install --user --name=nombre_del_entorno
```
