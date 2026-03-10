# ☸️ Kubernetes Iris API Deployment — AZ-400 DevOps Portfolio

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-000000?style=for-the-badge&logo=yaml&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)

> Production-grade Kubernetes deployment of the Iris Model API —
> demonstrating container orchestration, autoscaling, rolling updates,
> and multi-environment namespace isolation.

---

## 📋 Table of Contents

- [Purpose](#purpose)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Kubernetes Concepts Demonstrated](#kubernetes-concepts-demonstrated)
- [Multi-Environment Setup](#multi-environment-setup)
- [Technologies](#technologies)
- [How to Deploy](#how-to-deploy)
- [Pipeline](#pipeline)
- [Credits](#credits)

---

## 💼 Purpose

This project deploys the Iris Model API (from the ML-CI-CD-Pipeline project)
to a Kubernetes cluster — demonstrating production-grade container orchestration
as required for the AZ-400 DevOps Engineer Expert certification.

The same Docker image built and pushed in the CI/CD pipeline is now
**orchestrated by Kubernetes** — with automatic scaling, self-healing,
rolling updates, and environment isolation built in.

| Concept | Implementation |
|---|---|
| **Container Orchestration** | Kubernetes manages all containers |
| **High Availability** | 2 replicas always running |
| **Zero Downtime Deployments** | Rolling update strategy |
| **Autoscaling** | HPA scales 2→10 pods based on CPU/memory |
| **Environment Isolation** | Separate namespaces for dev/staging/production |
| **Configuration Management** | ConfigMap injects environment variables |
| **Health Monitoring** | Liveness and readiness probes |
| **Security Scanning** | Checkov scans manifests on every push |

---

## 🏗️ Architecture
```
                    ┌─────────────────────────────────────┐
                    │         Kubernetes Cluster           │
                    │                                      │
                    │  ┌─────────────────────────────┐    │
                    │  │     iris-production namespace │    │
                    │  │                              │    │
Internet ──────────▶│  │  Service (NodePort :30000)   │    │
                    │  │       │                      │    │
                    │  │       ▼                      │    │
                    │  │  Pod 1 (iris-api)            │    │
                    │  │  Pod 2 (iris-api)            │    │
                    │  │       │                      │    │
                    │  │       ▼                      │    │
                    │  │  HPA (scales 2 → 10 pods)    │    │
                    │  └─────────────────────────────┘    │
                    │                                      │
                    │  iris-dev namespace (dev workloads)  │
                    │  iris-staging namespace              │
                    └─────────────────────────────────────┘
```

---

## 📁 Project Structure
```
K8s-Iris-Deployment/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # Validates and scans manifests on every push
├── k8s/
│   ├── namespace.yaml         # Dev, staging, production namespaces
│   ├── configmap.yaml         # Environment variables
│   ├── deployment.yaml        # Pod spec, replicas, rolling update strategy
│   ├── service.yaml           # Exposes API via NodePort
│   └── hpa.yaml               # Autoscaling configuration
└── README.md
```

---

## ☸️ Kubernetes Concepts Demonstrated

### Deployment
Manages the lifecycle of the API pods. Ensures 2 replicas are always
running, automatically restarts failed containers, and performs
zero-downtime rolling updates when a new image is pushed.

### Service
Exposes the Deployment to network traffic via NodePort. Without a
Service, pods are unreachable. Routes traffic to all healthy pods
automatically.

### ConfigMap
Stores non-sensitive environment configuration. Decouples config
from the container image — the same image runs in dev, staging,
and production with different configs injected at runtime.

### HorizontalPodAutoscaler
Automatically scales the number of pods based on CPU and memory
usage. Under normal traffic — 2 pods. Under heavy load — scales
up to 10 pods automatically. Scales back down when traffic drops.

### Namespaces
Provides isolated environments within a single cluster. Dev,
staging, and production workloads run on the same cluster without
interfering with each other.

---

## 🌍 Multi-Environment Setup

| Environment | Namespace | Description |
|---|---|---|
| **Development** | `iris-dev` | Fast iteration, relaxed resource limits |
| **Staging** | `iris-staging` | Mirrors production, used for final testing |
| **Production** | `iris-production` | Full resource limits, autoscaling enabled |
```bash
# Deploy to dev
kubectl apply -f k8s/ -n iris-dev

# Deploy to staging
kubectl apply -f k8s/ -n iris-staging

# Deploy to production
kubectl apply -f k8s/ -n iris-production
```

---

## 🛠️ Technologies

**Container Orchestration**

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-000000?style=for-the-badge&logo=yaml&logoColor=white)

**Container & Registry**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Docker Hub](https://img.shields.io/badge/Docker%20Hub-2496ED?style=for-the-badge&logo=docker&logoColor=white)

**CI/CD & Security**

![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Checkov](https://img.shields.io/badge/Checkov-Security%20Scan-brightgreen?style=for-the-badge)

**ML API**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

| Category | Tools |
|---|---|
| **Orchestration** | Kubernetes, kubectl |
| **Config** | YAML, ConfigMap |
| **Autoscaling** | HorizontalPodAutoscaler |
| **CI/CD** | GitHub Actions |
| **Security** | Checkov |
| **API** | FastAPI, Docker Hub |

---

## ⚙️ How to Deploy

### Prerequisites
- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed
- A Kubernetes cluster running locally:
  - [minikube](https://minikube.sigs.k8s.io/docs/start/) (recommended for local)
  - [kind](https://kind.sigs.k8s.io/)
  - [Docker Desktop](https://www.docker.com/products/docker-desktop/) with Kubernetes enabled

### Deploy
```bash
# Clone the repo
git clone https://github.com/AZ400-DevOps-Portfolio/K8s-Iris-Deployment.git
cd K8s-Iris-Deployment

# Create namespaces
kubectl apply -f k8s/namespace.yaml

# Deploy to dev
kubectl apply -f k8s/ -n iris-dev

# Check pods are running
kubectl get pods -n iris-dev

# Check service
kubectl get service iris-api-service -n iris-dev

# Access the API
curl http://localhost:30000/health
curl http://localhost:30000/predict \
  -H "Content-Type: application/json" \
  -d '{"sepal_length": 5.1, "sepal_width": 3.5, "petal_length": 1.4, "petal_width": 0.2}'

# Check autoscaler
kubectl get hpa -n iris-dev

# Tear down
kubectl delete -f k8s/ -n iris-dev
```

---

## 🔄 Pipeline

On every push to `main` the GitHub Actions pipeline:

1. **Validates** all YAML manifests against the Kubernetes schema
2. **Security scans** manifests using Checkov for misconfigurations
3. **Prints deployment summary** showing what would be applied

| Job | Purpose |
|---|---|
| Validate K8s Manifests | Catches YAML errors before they reach the cluster |
| Security Scan | Flags security misconfigurations in manifests |
| Deployment Summary | Documents exactly what gets deployed and why |

---

## 🙏 Credits

**Developed by Lindiwe Songelwa — Data Scientist | DevOps Engineer | Insight Creator**

| Platform | Link |
|---|---|
| 💼 LinkedIn | [Lindiwe S.](https://www.linkedin.com/in/lindiwe-songelwa) |
| 🌐 Portfolio | [Creative Portfolio](https://lindiwe-22.github.io/Portfolio-Website/) |
| 🏅 Credly | [Lindiwe Songelwa – Badges](https://www.credly.com/users/samnkelisiwe-lindiwe-songelwa) |
| 🐳 Docker Hub | [lindiwe22/iris-model-api](https://hub.docker.com/r/lindiwe22/iris-model-api) |
| 📧 Email | [sl.songelwa@hotmail.co.za](mailto:sl.songelwa@hotmail.co.za) |

---

*© 2026 Lindiwe Songelwa. All rights reserved.*
