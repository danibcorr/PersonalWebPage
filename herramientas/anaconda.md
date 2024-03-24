<div align="justify">

# Anaconda

# Resumen

Anaconda es una plataforma de código abierto diseñada para la ciencia de datos y el aprendizaje automático. Cuenta con una versión de Python con numerosas bibliotecas preinstaladas, un gestor de paquetes que facilita la administración de dependencias, la capacidad de crear entornos virtuales y una integración fluida con cuadernos Jupyter. 

# Comandos

## **Actualizar todos los paquetes de Conda**

```bash
conda update --all
```

## **Añadir entornos en los cuadernos jupyter**

Pasos:

1. Primero creamos un entorno:
    
    ```bash
    conda create --name nombre_del_entorno
    ```
    
2. Activamos el entorno:
    
    ```bash
    conda activate nombre_del_entorno
    ```
    
3. Actualizamos la versión de pip (pip es un gestor de paquete) a la última versión:
    
    ```bash
    python3 -m pip install --upgrade pip
    ```
    
4. Instalados los paquetes necesarios en el entorno, instalamos ipykernel:
    
    ```bash
    pip install ipykernel
    ```
    
5. Finalmente, agregamos el entorno:
    
    ```bash
    python -m ipykernel install --user --name=nombre_del_entorno
    ```

</div>