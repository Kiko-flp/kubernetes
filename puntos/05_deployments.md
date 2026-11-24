# 5. Deployments

Un **Deployment** gestiona de forma declarativa los **ReplicaSets** y los **Pods**, permitiendo realizar despliegues controlados, actualizaciones progresivas (*rolling updates*) y reversiones (*rollbacks*) sin interrumpir el servicio.

## 5.1 Operaciones básicas

```bash
kubectl get deployments
kubectl describe deployment <nombre>
kubectl rollout status deployment/<nombre>
kubectl rollout undo deployment/<nombre>
```

| Comando | Descripción |
| --- | --- |
| `kubectl get deployments` | Lista los Deployments activos en el clúster. |
| `kubectl describe deployment <nombre>` | Muestra la configuración, estrategia de actualización y eventos. |
| `kubectl rollout status deployment/<nombre>` | Consulta el estado de una actualización en curso. |
| `kubectl rollout undo deployment/<nombre>` | Revierte el Deployment a la revisión anterior. |
