# Despliegue de Grafana en Kubernetes (Deployment, ReplicaSet y Service)

Repositorio con los manifiestos de Kubernetes para el despliegue, escalamiento y exposición de **Grafana** aplicando los conceptos de **Pod**, **ReplicaSet**, **Deployment** y **Service (`NodePort`)**.

## Estructura del Repositorio

- `grafana-deployment.yaml`: Define el `Deployment` de Grafana (`grafana/grafana:11.2.0`) con 3 réplicas, estrategia `RollingUpdate`, asignación de recursos y sondas de disponibilidad (`readinessProbe` / `livenessProbe`).
- `grafana-replicaset.yaml`: Definición explícita de un `ReplicaSet` con 3 réplicas de Grafana.
- `grafana-service.yaml`: Define el `Service` de tipo `NodePort` (`3000:30300/TCP`) con afinidad de sesión (`ClientIP`) para exponer la plataforma fuera del clúster.
- `INFORME_KUBERNETES_GRAFANA.md`: Informe detallado de la práctica, casos de uso y guía de comandos.

## Ejecución Rápida

```powershell
minikube start --driver=docker

kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml

kubectl get deploy,rs,pods,svc -l app=grafana -o wide

kubectl port-forward deployment/grafana-deployment 3000:3000
```

Acceso en navegador: `http://localhost:3000` (Usuario: `admin` / Contraseña: `admin123`).
