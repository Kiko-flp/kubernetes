# 4. ReplicaSets

Un **ReplicaSet** garantiza que un número determinado de réplicas idénticas de un Pod estén ejecutándose en todo momento. Si un Pod falla o se elimina, el ReplicaSet crea uno nuevo automáticamente.

## 4.1 Definición de un ReplicaSet

Ejemplo de manifiesto en [nginx-rs.yaml](../ficheros/nginx-rs.yaml):

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: contenedor-nginx
```

| Campo | Descripción |
| --- | --- |
| `replicas` | Número de Pods idénticos que debe mantener activos el ReplicaSet. |
| `selector.matchLabels` | Etiquetas que identifican los Pods gestionados por el ReplicaSet. |
| `template` | Plantilla utilizada para crear los nuevos Pods cuando faltan réplicas. |

## 4.2 Gestión y escalado

```bash
kubectl apply -f ../ficheros/nginx-rs.yaml
kubectl get replicasets
kubectl get pods
kubectl scale replicaset/replicaset-nginx --replicas=4
kubectl delete -f ../ficheros/nginx-rs.yaml
```

| Comando | Descripción |
| --- | --- |
| `kubectl apply -f ../ficheros/nginx-rs.yaml` | Crea el ReplicaSet definido en el manifiesto. |
| `kubectl get replicasets` | Lista los ReplicaSets y muestra cuántas réplicas están listas. |
| `kubectl scale replicaset/replicaset-nginx --replicas=4` | Escala el número de réplicas del ReplicaSet. |
| `kubectl delete -f ../ficheros/nginx-rs.yaml` | Elimina el ReplicaSet y los Pods que gestiona. |
