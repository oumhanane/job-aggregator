# 🚀 Job Aggregator – Cloud Native DevOps Project

Projet personnel d'agrégation d'offres d'emploi développé avec **FastAPI**, conteneurisé avec **Docker** et déployé sur **Kubernetes (Minikube)**.

Le projet met en œuvre une chaîne DevOps complète intégrant :

* CI automatisée avec GitHub Actions
* Versioning automatique avec Semantic Release
* Publication des images Docker sur Docker Hub
* Déploiement GitOps avec Argo CD
* Sécurité applicative (SAST, SCA, scan d'images)
* Déploiement continu sur Kubernetes
* Observabilité avec Prometheus et Grafana

L'objectif est de reproduire une architecture Cloud Native proche de celles rencontrées en entreprise.

---

# 🎯 Objectif

Ce projet simule une plateforme DevOps moderne permettant :

* Agrégation d'offres d'emploi depuis plusieurs sources
* Traitement et scoring des offres
* Exposition via une API REST
* Interface Web légère
* Conteneurisation Docker
* Déploiement Kubernetes
* Livraison continue GitOps
* Supervision de l'application et du cluster Kubernetes

---

# ⚙️ Stack technique

## Application

* Python 3.12
* FastAPI
* Uvicorn
* HTML / CSS / JavaScript
* Pytest

## Conteneurisation

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
* GitHub Repository as Source of Truth
* Synchronisation automatique
* Auto-healing
* Prune automatique

## CI/CD

* GitHub Actions
* Semantic Release
* Conventional Commits

## Sécurité

* Bandit (SAST)
* pip-audit (SCA)
* Trivy (Container Security)

## Observabilité

* Prometheus
* Grafana
* kube-prometheus-stack
* Alertmanager
* kube-state-metrics
* node-exporter

---

# 📁 Structure du projet

```text
job-aggregator/

├── api.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── README.md

├── core/
│   └── logique métier

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

# 🎨 Interface utilisateur

Une interface HTML légère permet :

* consulter les offres
* appeler l'API
* tester rapidement le projet

Accès local :

```text
http://localhost:8000/ui
```

---

# 🚀 Exécution

## Python

Installation :

```bash
pip install -r requirements.txt
```

Lancement :

```bash
uvicorn api:app --reload
```

API :

```text
http://localhost:8000
```

Swagger :

```text
http://localhost:8000/docs
```

UI :

```text
http://localhost:8000/ui
```

---

# 🐳 Docker

Construction :

```bash
docker build -t job-aggregator .
```

Exécution :

```bash
docker run -p 8000:8000 job-aggregator
```

---

# ☸️ Déploiement Kubernetes

Les manifests Kubernetes sont versionnés dans Git.

Application :

```text
k8s/app/
```

Déploiement :

```bash
kubectl apply -f k8s/app/
```

Ressources déployées :

* Deployment
* Service
* Ingress

Le déploiement utilise :

* Rolling Update
* Readiness Probe
* Liveness Probe
* Resource Requests/Limits

---

# 🔄 Déploiement GitOps avec Argo CD

Le déploiement Kubernetes est piloté par Argo CD.

GitHub est utilisé comme **Source of Truth**.

Architecture :

```text
GitHub
   |
   v
 Argo CD
   |
   v
 Kubernetes
```

L'application métier est gérée par :

```text
argocd/

├── project.yaml
└── application.yaml
```

Fonctionnalités activées :

* Synchronisation automatique
* Auto-healing
* Prune automatique

Chaque modification du dépôt Git est automatiquement détectée puis appliquée au cluster Kubernetes.

---

# 📊 Observabilité Kubernetes

Une stack complète d'observabilité a été ajoutée avec Argo CD.

Déploiement :

```text
k8s/monitoring/
```

Technologies utilisées :

* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics
* node-exporter

Installation réalisée via :

```text
kube-prometheus-stack Helm Chart
```

Architecture :

```text
Application FastAPI
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

Cette stack permet de superviser :

* ressources Kubernetes
* état des pods
* utilisation CPU / mémoire
* métriques applicatives
* performances du cluster

---

# 📊 API

| Endpoint   | Description           |
| ---------- | --------------------- |
| GET /      | Status                |
| GET /jobs  | Liste des offres      |
| GET /stats | Statistiques          |
| GET /docs  | Swagger               |
| GET /ui    | Interface utilisateur |

---

# 🔐 CI

La pipeline Continuous Integration exécute automatiquement :

* Tests Pytest
* Analyse SAST avec Bandit
* Analyse SCA avec pip-audit
* Scan de l'image Docker avec Trivy

Workflow :

```text
.github/workflows/ci.yaml
```

---

# 🚀 Release automatique

Le versioning est assuré par Semantic Release.

Basé sur Conventional Commits :

```text
feat:
```

Nouvelle fonctionnalité

```text
fix:
```

Correction

```text
docs:
```

Documentation

Semantic Release génère automatiquement :

* numéro de version
* CHANGELOG
* tag Git
* GitHub Release

Workflow :

```text
.github/workflows/release.yaml
```

---

# 🐳 Docker Release

Chaque nouveau tag Git déclenche automatiquement :

* construction de l'image Docker
* publication sur Docker Hub

Images publiées :

```text
saliha91700/job-aggregator:vX.Y.Z

saliha91700/job-aggregator:latest
```

Workflow :

```text
.github/workflows/docker-release.yaml
```

---

# 🔄 Flux DevOps complet

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

# 🎯 Compétences DevOps mises en œuvre

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
* Observabilité Kubernetes
* Monitoring Cloud Native

---

# 📈 Évolutions réalisées et futures

## Réalisées

✅ CI/CD GitHub Actions
✅ Conteneurisation Docker
✅ Déploiement Kubernetes
✅ GitOps avec Argo CD
✅ Prometheus
✅ Grafana
✅ Monitoring Kubernetes

## Futures évolutions

* Instrumentation FastAPI avec métriques applicatives
* ServiceMonitor Prometheus
* Dashboards Grafana personnalisés
* Vault pour la gestion des secrets
* Helm Charts
* Argo Rollouts
* Argo Image Updater
* cert-manager
* Déploiement Cloud (EKS / AKS / GKE)
* Architecture microservices
* MLOps (personnalisation des offres)

---

# 👨‍💻 Auteur

**Saliha Hammad**

Projet personnel réalisé dans le cadre d'une montée en compétences vers un poste d'Ingénieure DevOps / Cloud Native.

Objectif : mettre en œuvre des pratiques modernes de CI/CD, GitOps, Kubernetes, automatisation et observabilité dans une architecture proche des environnements professionnels.
