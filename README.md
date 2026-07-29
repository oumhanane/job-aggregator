# 🚀 Job Aggregator – Cloud Native DevOps Project

Personal job offer aggregation platform developed with **FastAPI**, containerized with **Docker**, and deployed on **Kubernetes (Minikube)**.

This project implements a complete DevOps workflow including:

* Automated CI pipeline with GitHub Actions
* Automatic versioning with Semantic Release
* Docker image publishing on Docker Hub
* GitOps deployment with Argo CD
* Application security (SAST, SCA, container image scanning)
* Continuous deployment on Kubernetes
* Observability with Prometheus and Grafana

The goal of this project is to reproduce a modern Cloud Native architecture similar to those used in professional environments.

---

# 🎯 Objective

This project simulates a modern DevOps platform providing:

* Job offer aggregation from multiple sources
* Job processing and scoring
* REST API exposure
* Lightweight Web interface
* Docker containerization
* Kubernetes deployment
* GitOps continuous delivery
* Application and Kubernetes cluster monitoring

---

# ⚙️ Technical Stack

## Application

* Python 3.12
* FastAPI
* Uvicorn
* HTML / CSS / JavaScript
* Pytest

## Containerization

* Docker
* Docker Hub

## Kubernetes

* Kubernetes
* Minikube
* NGINX Ingress Controller
* Readiness Probe
* Liveness Probe
* Resource Requests / Limits
* Metrics Server

## GitOps

* Argo CD
* GitHub Repository as Single Source of Truth
* Automated synchronization
* Self-healing
* Automatic pruning

## CI/CD

* GitHub Actions
* Semantic Release
* Conventional Commits

## Security

* Bandit (SAST)
* pip-audit (SCA)
* Trivy (Container Security)

## Observability

* Prometheus
* Grafana
* kube-prometheus-stack
* Alertmanager
* kube-state-metrics
* node-exporter

---

# 📁 Project Structure

```text
job-aggregator/

├── api.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── README.md

├── core/
│   └── business logic

├── sources/
│   ├── HelloWork
│   ├── Welcome To The Jungle
│   └── Remotive

├── ui/
│   ├── index.html
│   ├── css/
│   └── javascript/

├── tests/

├── k8s/
│
│   ├── app/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
│   │
│   └── monitoring/
│       ├── namespace.yaml
│       └── monitoring.yaml

├── argocd/
│   ├── application.yaml
│   └── project.yaml

└── .github/
    └── workflows/
        ├── ci.yaml
        ├── release.yaml
        └── docker-release.yaml
```

---

# 🎨 User Interface

A lightweight HTML interface allows users to:

* Browse job offers
* Call the API
* Quickly test the application

Local access:

```text
http://localhost:8000/ui
```

---

# 🚀 Running the Application

## Python

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the application:

```bash
uvicorn api:app --reload
```

API:

```text
http://localhost:8000
```

Swagger documentation:

```text
http://localhost:8000/docs
```

UI:

```text
http://localhost:8000/ui
```

---

# 🐳 Docker

Build image:

```bash
docker build -t job-aggregator .
```

Run container:

```bash
docker run -p 8000:8000 job-aggregator
```

---

# ☸️ Kubernetes Deployment

Kubernetes manifests are version-controlled in Git.

Application manifests:

```text
k8s/app/
```

Deployment:

```bash
kubectl apply -f k8s/app/
```

Deployed resources:

* Deployment
* Service
* Ingress

The deployment uses:

* Rolling Update strategy
* Readiness Probe
* Liveness Probe
* Resource Requests / Limits

---

# 🔄 GitOps Deployment with Argo CD

Kubernetes deployment is managed through Argo CD using a GitOps approach.

GitHub is used as the **Single Source of Truth**.

Architecture:

```text
GitHub Repository
        |
        v
      Argo CD
        |
        v
 Kubernetes Cluster
```

The application is managed through:

```text
argocd/

├── project.yaml
└── application.yaml
```

Enabled features:

* Automated synchronization
* Self-healing
* Automatic pruning

Every Git repository change is automatically detected and synchronized with the Kubernetes cluster.

---

# 📊 Kubernetes Observability

A complete observability stack has been added using Argo CD.

Deployment:

```text
k8s/monitoring/
```

Technologies:

* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics
* node-exporter

Installation:

```text
kube-prometheus-stack Helm Chart
```

Architecture:

```text
FastAPI Application
        |
        v
    Metrics
        |
        v
   Prometheus
        |
        v
    Grafana
```

This stack provides visibility into:

* Kubernetes resources
* Pod health
* CPU and memory usage
* Application metrics
* Cluster performance

---

# 📊 API

| Endpoint | Description |
|---|---|
| GET / | Application status |
| GET /jobs | Job offers list |
| GET /stats | Statistics |
| GET /docs | Swagger documentation |
| GET /ui | User interface |

---

# 🔐 Continuous Integration

The CI pipeline automatically executes:

* Pytest tests
* SAST analysis with Bandit
* SCA analysis with pip-audit
* Docker image scanning with Trivy

Workflow:

```text
.github/workflows/ci.yaml
```

---

# 🚀 Automatic Release

Version management is handled by Semantic Release.

Based on Conventional Commits:

```text
feat:
```

New feature

```text
fix:
```

Bug fix

```text
docs:
```

Documentation update

Semantic Release automatically generates:

* Version number
* CHANGELOG
* Git tag
* GitHub Release

Workflow:

```text
.github/workflows/release.yaml
```

---

# 🐳 Docker Release

Each new Git tag automatically triggers:

* Docker image build
* Docker Hub publication

Published images:

```text
saliha91700/job-aggregator:vX.Y.Z

saliha91700/job-aggregator:latest
```

Workflow:

```text
.github/workflows/docker-release.yaml
```

---

# 🔄 Complete DevOps Workflow

```text
Developer

    |
    v

Git Push

    |
    v

GitHub

    |
    v

GitHub Actions CI

    |
    v

Semantic Release

    |
    v

Docker Hub

    |
    v

Argo CD

    |
    v

Kubernetes

    |
    v

Prometheus / Grafana
```

---

# 🎯 DevOps Skills Demonstrated

* Docker
* Kubernetes
* GitHub Actions
* GitOps
* Argo CD
* Docker Hub
* Semantic Release
* CI/CD
* Continuous Delivery
* Rolling Update
* Health Checks
* Security Scanning
* Infrastructure as Code
* Kubernetes Observability
* Cloud Native Monitoring

---

# 📈 Completed and Future Improvements

## Completed

✅ GitHub Actions CI/CD  
✅ Docker containerization  
✅ Kubernetes deployment  
✅ GitOps with Argo CD  
✅ Prometheus  
✅ Grafana  
✅ Kubernetes monitoring  

## Future Improvements

* FastAPI instrumentation with application metrics
* Prometheus ServiceMonitor
* Custom Grafana dashboards
* Vault secret management
* Helm Charts
* Argo Rollouts
* Argo Image Updater
* cert-manager
* Cloud deployment (EKS / AKS / GKE)
* Microservices architecture
* MLOps (job recommendation personalization)

---

# 👨‍💻 Author

**Saliha Hammad**

Personal project developed as part of my transition towards a **DevOps / Cloud Native Engineer** role.

The objective is to implement modern practices around CI/CD, GitOps, Kubernetes, automation, and observability using a production-like Cloud Native architecture.