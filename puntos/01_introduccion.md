# 1. Introducción a Kubernetes

## 1.1 El problema real

En los entornos actuales de producción, las aplicaciones deben cumplir una serie de exigencias críticas:

- **Disponibilidad 24/7:** los servicios deben estar operativos de forma continua.
- **Gran volumen de usuarios:** las aplicaciones reciben picos y cargas elevadas de tráfico simultáneo.
- **Cambios constantes:** el software se actualiza con frecuencia para corregir errores o añadir funcionalidades.
- **Sin paradas de servicio:** las actualizaciones y los fallos no pueden interrumpir la disponibilidad para los usuarios.

## 1.2 Contenedores: primera solución

Un **contenedor** empaqueta una **aplicación junto con sus dependencias**. Su uso resuelve problemas clásicos de desarrollo y despliegue (como el habitual *"en mi máquina funcionaba"*):

- **Aíslan la aplicación** del resto del sistema.
- **Funcionan igual en cualquier entorno** (desarrollo, pruebas o producción).
- **Facilitan el despliegue y la actualización** de versiones.

Sin embargo, usar únicamente contenedores **no es suficiente en producción**, ya que por sí solos:

- **No escalan solos** cuando aumenta el número de usuarios.
- **No se recuperan ante fallos** de forma automática.
- **No balancean la carga** entre múltiples instancias.

## 1.3 ¿Qué es Kubernetes?

**Kubernetes** es un **orquestador de contenedores** pensado para entornos de producción que gestiona grandes cantidades de contenedores y automatiza las decisiones sobre ellos.

Entre sus funciones principales se encuentran:

- **Ejecutar contenedores automáticamente** en los servidores disponibles.
- **Crear y mantener varias copias** de una misma aplicación.
- **Escalar según la carga** de trabajo.
- **Recuperarse ante fallos** reprogramando contenedores o sustituyendo instancias caídas.
- **Actualizar sin parar el servicio** mediante despliegues progresivos.

## 1.4 Arquitectura de Kubernetes

Un **clúster** de Kubernetes es un conjunto de máquinas (servidores) que trabajan juntas, donde cada máquina recibe el nombre de **nodo**. Disponer de varios nodos permite **escalar** (más copias), lograr **alta disponibilidad** (si un nodo cae, otro continúa dando servicio) y realizar **reparto de carga**.

El clúster se divide en dos tipos de nodos:

### Control Plane (Master)

Es la parte que **toma las decisiones y controla el estado del clúster**; no ejecuta aplicaciones de usuario. Sus componentes principales son:

| Componente | Función |
| --- | --- |
| **API Server (`kube-apiserver`)** | Punto de entrada a Kubernetes; toda comunicación con el clúster pasa por aquí (por ejemplo, desde `kubectl`). |
| **Scheduler (`kube-scheduler`)** | Decide en qué *Worker Node* se debe ejecutar cada carga de trabajo. |
| **Base de datos (`etcd`)** | Almacena de forma persistente el estado completo del clúster. |
| **Controller Manager (`kube-controller-manager`)** | Vigila que el estado actual del sistema coincida con el estado deseado definido. |

### Worker Nodes

Son los nodos **donde se ejecutan las aplicaciones**. Sus elementos clave son:

- **`kubelet`:** agente de Kubernetes en el nodo que recibe órdenes del *Control Plane* y se asegura de que los contenedores estén funcionando.
- **Container Runtime (`containerd`):** componente encargado de ejecutar, arrancar y parar realmente los contenedores *(aunque en diagramas antiguos aparezca Docker, actualmente Kubernetes utiliza `containerd`)*.
- **`kube-proxy`:** gestiona la comunicación de red en el nodo.
- **Pod:** unidad mínima de ejecución en Kubernetes; agrupa uno o varios contenedores que se ejecutan juntos en el mismo nodo.

## 1.5 Otros orquestadores

Existen otras soluciones de orquestación además de Kubernetes:

- **Docker Swarm:** orquestador sencillo integrado directamente en Docker.
- **Apache Mesos:** proyecto potente para gestión de recursos, aunque hoy poco usado para contenedores.
- **Nomad:** orquestador simple desarrollado por HashiCorp.
- **Kubernetes:** estándar de facto en producción.

### Comparativa: Docker Swarm vs Kubernetes

| Característica | Docker Swarm | Kubernetes |
| --- | --- | --- |
| **Tipo** | Orquestador básico | Orquestador completo |
| **Facilidad de uso** | Muy sencillo | Más complejo |
| **Integración** | Integrado en Docker | Independiente de Docker |
| **Escalado automático** | Básico | Avanzado |
| **Alta disponibilidad** | Limitada | Completa |
| **Actualizaciones sin parada** | Básicas | Muy avanzadas |
| **Uso en producción** | Pequeños entornos | Estándar en producción |
| **Ecosistema** | Muy reducido | Muy amplio |
| **Popularidad actual** | En desuso | Estándar de facto |
