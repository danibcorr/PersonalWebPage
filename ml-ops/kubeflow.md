---
description: Realizado por Daniel Bazo Correa.
---

# 1. Introducción

Gestionar todas las aplicaciones, plataformas y consideraciones de los recursos de cada una puede ser tedioso. Existen múltiples procesos para cada paso, como el entrenamiento e inferencia de un modelo, cada uno con diferentes requisitos y dependencias.

Kubeflow pretende ser un estándar para el despliegue de aplicaciones de ML a nivel empresarial de extremo a extremo. Es open source y su objetivo es facilitar el desarrollo, despliegue y gestión de la inteligencia artificial de manera portable y escalable.

Kubeflow se ejecuta sobre Kubernetes y se caracteriza por su:

- **Composabilidad**: Permite elegir los componentes adecuados para cada proyecto.
- **Portabilidad**: Permite ejecutar el pipeline en cualquier lugar que soporte Kubeflow.
- **Escalabilidad**: Facilita la gestión eficiente de los recursos.

# 2. Instalación

En este caso, se instalará Kubeflow en Debian. Cada instancia de Kubeflow necesita un clúster de Kubernetes para ejecutarse. Para simplificar, se usará MicroK8s, que es la forma más rápida y sencilla de crear un clúster de Kubernetes.

Debian no incluye Snap, por lo que primero debe instalarse con el comando:

```bash
sudo apt install snapd
```

Para evitar usar `sudo` en cada comando de MicroK8s, se deben ejecutar los siguientes comandos:

```bash
sudo usermod -a -G microk8s $USER
newgrp microk8s
```

Luego, reiniciar el equipo para poder ejecutar los comandos de MicroK8s.

Seguir los pasos descritos en [la guía de Charmed Kubeflow](https://charmed-kubeflow.io/docs/get-started-with-charmed-kubeflow):

```bash
sudo snap install microk8s --classic --channel=1.29/stable
sudo usermod -a -G microk8s $USER
newgrp microk8s
sudo chown -f -R $USER ~/.kube
microk8s enable dns hostpath-storage ingress metallb:10.64.140.43-10.64.140.49 rbac
microk8s status
sudo snap install juju --classic --channel=3.4/stable
microk8s config > ~/.kube/config
export KUBECONFIG=~/.kube/config
mkdir -p ~/.local/share
microk8s config | juju add-k8s my-k8s --client
juju bootstrap my-k8s uk8sx
juju add-model kubeflow
sudo sysctl fs.inotify.max_user_instances=1280
sudo sysctl fs.inotify.max_user_watches=655360
juju deploy kubeflow --trust --channel=1.8/stable
```

## 2.1. Error en la instalación

En caso de error, eliminar todo y repetir los pasos anteriores:

```bash
sudo snap remove --purge juju
rm -rf ~/.local/share/juju
sudo snap remove --purge microk8s
sudo rm -rf /var/snap/microk8s
```

# 3. Componentes

Kubeflow incluye varios componentes esenciales para el desarrollo y despliegue de modelos de aprendizaje automático:

- **Katib**: Utilizado para la búsqueda de hiperparámetros, permite optimizar los modelos seleccionando métricas como la precisión.
- **Plataforma de Pipelines**: Permite crear un conjunto de pasos para manejar desde la recopilación de datos hasta la inferencia de un modelo. Está basada en contenedores, lo que garantiza portabilidad y escalabilidad. Facilita la orquestación de pipelines de ML, la compartición de experimentos, su reproducción y la reutilización de componentes. Cada componente del pipeline es un contenedor Docker dentro de un Pod de Kubernetes. La UI permite realizar las conexiones del pipeline.
- **Soporte para Frameworks**: Compatible con diferentes frameworks como TensorFlow y PyTorch. Define recursos personalizados para trabajos de entrenamiento distribuidos (como RAY).
- **KFServing**: Permite ejecutar aplicaciones serverless en Kubernetes.
- **Jupyter Notebooks**: Ofrece una implementación de Jupyter notebooks con integración mejorada con otros componentes de Kubeflow. Facilita el acceso a servicios del clúster utilizando direcciones IP del mismo, además de permitir el control de acceso, autenticación, administración de roles, compartir notebooks dentro de la organización y realizar despliegues en Kubernetes. Los notebooks se alojan en un pod de Kubernetes.