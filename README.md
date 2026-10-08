# Coxda Microservices Helm Chart (Local Kubernetes & Production Ready)

This Helm Chart is configured to deploy all services seamlessly to **Docker Desktop Kubernetes**, **Minikube**, or any Cloud Kubernetes cluster.

---

## 🌐 Localhost Port Mapping (Docker Desktop Kubernetes)

With `service.type: LoadBalancer`, all services are directly mapped to `localhost` on your local PC:

| Service | Localhost URL / Port | Description |
|---|---|---|
| **Frontend Web App** | **`http://localhost:8080`** | `coxda-app:latest` (Vue.js App) |
| **Auth Service** | **`http://localhost:8081`** | `coxda-auth-service:latest` (Lumen Auth API) |
| **Common Service** | **`http://localhost:8082`** | `coxda-common-service:latest` (Lumen Core API) |
| **phpMyAdmin** | **`http://localhost:8083`** | Web MySQL Manager (User: `root`, Pass: `password`) |
| **MySQL Database** | **`localhost:3306`** | MySQL 8.0 (Persistent Volume attached) |
| **Redis Cache** | `Internal Port 6379` | Internal Cluster Service for caching & sessions |

---

## 🚀 How to Deploy on Local Docker Desktop Kubernetes

### Step 1: Ensure Local Docker Images Exist
Make sure your local images are built and available in Docker:
```bash
docker images | findstr coxda
```
Expected images:
- `coxda-app:latest`
- `coxda-auth-service:latest`
- `coxda-common-service:latest`

### Step 2: Install the Chart
```bash
helm install coxda "F:\k8s setup gude\helm\coxda-chart" -n coxda --create-namespace
```

### Step 3: Check Running Status
```bash
kubectl get all -n coxda
```

### Step 4: Upgrade After Modifying values.yaml
```bash
helm upgrade coxda "F:\k8s setup gude\helm\coxda-chart" -n coxda
```

### Step 5: Uninstall / Clean Up
```bash
helm uninstall coxda -n coxda
```

---

## 🛠️ Verification in Browser
- Open `http://localhost:8080` for Frontend App
- Open `http://localhost:8081/healthz` for Auth Service
- Open `http://localhost:8082/` for Common Service
- Open `http://localhost:8083` for phpMyAdmin
