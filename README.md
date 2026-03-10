# K8s-Iris-Deployment
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