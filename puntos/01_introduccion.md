# 1. Introducción

## 1.1 ¿Qué es Kubernetes?

**Kubernetes** (abreviado habitualmente como **K8s**) es una plataforma de código abierto para la **orquestación de contenedores**. Permite automatizar el despliegue, el escalado y la gestión de aplicaciones empaquetadas en contenedores (como Docker o containerd) sobre uno o varios nodos.

Mientras que un motor de contenedores ejecuta aplicaciones aisladas en una máquina, Kubernetes coordina múltiples contenedores repartidos en un clúster para garantizar que los servicios sigan disponibles, se recuperen ante fallos y se adapten a la carga de trabajo.

## 1.2 Funcionalidades principales

| Característica | Descripción |
| --- | --- |
| **Despliegue automatizado** | Define el estado deseado de la aplicación mediante manifiestos YAML y Kubernetes se encarga de alcanzarlo y mantenerlo. |
| **Autocuración (*self-healing*)** | Reinicia contenedores que fallan, reemplaza nodos caídos y reprograma cargas de trabajo sin intervención manual. |
| **Escalado horizontal** | Aumenta o reduce el número de réplicas de una aplicación según la demanda de recursos o de forma manual. |
| **Balanceo de carga y descubrimiento** | Expone los contenedores mediante servicios estables y distribuye el tráfico entre las réplicas disponibles. |
| **Actualizaciones y rollbacks** | Permite desplegar nuevas versiones de forma progresiva (*rolling updates*) y volver atrás si se detecta algún fallo. |
| **Gestión de configuración y secretos** | Separa la configuración (`ConfigMap`) y los datos sensibles (`Secret`) del código de la aplicación. |

## 1.3 Arquitectura básica de un clúster

Un clúster de Kubernetes se divide en dos partes diferenciadas:

- **Control Plane (plano de control):** gestiona el estado global del clúster, toma decisiones de planificación y responde a eventos. Sus componentes principales son `kube-apiserver`, `etcd`, `kube-scheduler` y `kube-controller-manager`.
- **Worker Nodes (nodos de trabajo):** ejecutan las cargas de trabajo reales (los contenedores). Cada nodo incluye `kubelet` (agente que se comunica con el plano de control), `kube-proxy` (gestión de red y reglas de tráfico) y un entorno de ejecución de contenedores (*container runtime*).

## 1.4 Entorno de laboratorio y alcance

Para realizar las prácticas de este repositorio se utiliza **Minikube** junto con **`kubectl`**:

- **Minikube:** permite levantar un clúster local de Kubernetes en un único nodo (sobre VirtualBox o Docker) para aprender y probar despliegues sin necesidad de infraestructura en producción.
- **`kubectl`:** herramienta de línea de comandos oficial para interactuar con el clúster, crear recursos y consultar su estado.

En los siguientes apartados se aborda la instalación del entorno y el uso de los recursos fundamentales de Kubernetes: **Pods**, **ReplicaSets** y **Deployments**.
