# Kubernetes Multi-Tier Web Application Demo

A learning project demonstrating a 3-tier architecture on Kubernetes:
- Frontend: Simple HTML/JS web interface
- Backend: Node.js/Express API
- Database: PostgreSQL

## Architecture
```
[Frontend Pod] -> [Backend Pod] -> [Database Pod]
       |              |              |
   [Service]      [Service]    [Service + PV]
       |              |
   [Ingress]     [Internal]
```

## Components
- **Frontend**: Serves static HTML/JS, communicates with backend API
- **Backend**: REST API that handles business logic and database operations
- **Database**: PostgreSQL with persistent storage

## Kubernetes Concepts Covered
- Deployments and Pods
- Services (ClusterIP, NodePort)
- Ingress
- Persistent Volumes and Claims
- Secrets and ConfigMaps
- Resource limits and requests

## Prerequisites
- Docker installed
- Kubernetes cluster running (minikube, kind, or cloud)
- kubectl configured
- For ingress: nginx-ingress-controller installed (`minikube addons enable ingress`)

## Quick Start
```bash
# 1. Build Docker images
./build-images.sh

# 2. Load images to cluster (minikube/kind)
./load-images.sh

# 3. Deploy the application
./deploy.sh

# 4. Access the app at http://k8s-demo.local
# (Add cluster IP to /etc/hosts first)
```

## Manual Deployment
```bash
# Apply manifests in order
kubectl apply -f k8s/postgres-secret.yaml
kubectl apply -f k8s/postgres-pv.yaml
kubectl apply -f k8s/backend-configmap.yaml
kubectl apply -f k8s/postgres-deployment.yaml
kubectl apply -f k8s/postgres-service.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/backend-service.yaml
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml
kubectl apply -f k8s/ingress.yaml
```

## Cleanup
```bash
./cleanup.sh
```

## Learning Points
This project demonstrates:
- **Deployments**: Scalable application pods
- **Services**: Internal cluster networking
- **Ingress**: External traffic routing
- **Persistent Volumes**: Database data persistence
- **Secrets**: Sensitive data management
- **ConfigMaps**: Application configuration
- **Health Checks**: Liveness and readiness probes
- **Resource Limits**: CPU and memory constraints