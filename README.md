🚀 Job Aggregator – Cloud Native DevOps Project

Projet personnel d'agrégation d'offres d'emploi développé avec FastAPI, conteneurisé avec Docker et déployé sur Kubernetes (Minikube).

Le projet met en œuvre une chaîne DevOps complète intégrant :

CI automatisée avec GitHub Actions
Versioning automatique avec Semantic Release
Publication des images sur Docker Hub
Déploiement GitOps avec ArgoCD
Sécurité applicative (SAST, SCA, scan d'images)
Déploiement continu sur Kubernetes

🎯 Objectif

Ce projet simule une plateforme DevOps moderne permettant :

Agrégation d'offres d'emploi depuis plusieurs sources
Traitement et scoring des offres
Exposition via une API REST
Interface Web légère
Déploiement Kubernetes
Livraison continue GitOps

L'objectif est de reproduire une architecture proche de celles rencontrées en entreprise.

⚙️ Stack technique
Python 3.12
FastAPI
Uvicorn
HTML / CSS / JavaScript
Docker
Docker Hub
Kubernetes (Minikube)
NGINX Ingress Controller
ArgoCD
GitHub Actions
Semantic Release
Pytest
Bandit
pip-audit
Trivy

📁 Structure du projet
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
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml

├── argocd/
│   ├── application.yaml
│   └── project.yaml

└── .github/
    └── workflows/
        ├── ci.yaml
        ├── release.yaml
        └── docker-release.yaml

🎨 Interface utilisateur

Une interface HTML légère permet :

consulter les offres
appeler l'API
tester rapidement le projet

Accès :

http://localhost:8000/ui

🚀 Exécution
Python
pip install -r requirements.txt

uvicorn api:app --reload

API

http://localhost:8000

Swagger

http://localhost:8000/docs

UI

http://localhost:8000/ui
Docker
docker build -t job-aggregator .

docker run -p 8000:8000 job-aggregator
Kubernetes
kubectl apply -f k8s/

🌐 Accès Kubernetes

Port Forward

kubectl port-forward service/job-aggregator-service 8080:8000

Accès :

http://localhost:8080

http://localhost:8080/docs

http://localhost:8080/ui

Ingress

http://job.local

http://job.local/ui

☸️ Ressources Kubernetes

Le projet déploie :

Deployment
Service
Ingress

Le déploiement utilise :

Rolling Update
Readiness Probe
Liveness Probe
Resource Requests/Limits

🔄 Déploiement GitOps avec ArgoCD

Le déploiement Kubernetes est piloté par ArgoCD.

Deux ressources sont utilisées :

argocd/

project.yaml

application.yaml

Le projet ArgoCD :

job-aggregator

surveille automatiquement le dépôt Git.

Fonctionnalités activées :

Synchronisation automatique
Auto-healing
Prune automatique

Flux GitOps :

GitHub
      │
      ▼
 ArgoCD
      │
      ▼
 Kubernetes

Chaque modification du dépôt est détectée puis appliquée automatiquement au cluster.

📊 API
Endpoint	Description
GET /	Status
GET /jobs	Liste des offres
GET /stats	Statistiques
GET /docs	Swagger
GET /ui	Interface utilisateur

🔐 CI

La pipeline de Continuous Integration exécute automatiquement :

Tests Pytest
Analyse SAST avec Bandit
Analyse SCA avec pip-audit
Scan de l'image Docker avec Trivy

Workflow :

.github/workflows/ci.yaml

🚀 Release automatique

Le versioning est assuré par Semantic Release.

Basé sur Conventional Commits :

feat:

→ nouvelle fonctionnalité

fix:

→ correction

docs:

→ documentation

Workflow :

.github/workflows/release.yaml

Semantic Release génère automatiquement :

le numéro de version
le CHANGELOG
le tag Git
la GitHub Release

🐳 Docker Release

Chaque nouveau tag Git déclenche automatiquement :

construction de l'image
publication sur Docker Hub

Images publiées :

saliha91700/job-aggregator:vX.Y.Z

saliha91700/job-aggregator:latest

Workflow :

.github/workflows/docker-release.yaml

🔄 Flux DevOps
Developer

      │

git push

      │

GitHub

      │

CI

      │

Semantic Release

      │

Git Tag

      │

Docker Hub

      │

ArgoCD

      │

Kubernetes

🎯 Compétences DevOps mises en œuvre
Docker
Kubernetes
GitHub Actions
GitOps
ArgoCD
Docker Hub
Semantic Release
CI
Continuous Delivery
Rolling Update
Health Checks
Security Scanning
Infrastructure as Code

📈 Évolutions prévues
PostgreSQL
Authentification utilisateurs
Helm Charts
Prometheus
Grafana
Vault
Argo Rollouts
Argo Image Updater
cert-manager
EKS
AKS
GKE
Architecture microservices
MLOps (personnalisation des offres)

👨‍💻 Auteur

Saliha Hammad

Projet personnel réalisé dans le cadre de ma montée en compétences vers un poste d'Ingénieure DevOps / Cloud Native, avec pour objectif de mettre en œuvre des pratiques modernes de CI/CD, GitOps et d'automatisation sur Kubernetes.