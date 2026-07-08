# 🚀 Job Aggregator – DevOps Project

Projet personnel d’agrégation d’offres d’emploi développé avec **FastAPI**, conteneurisé avec **Docker**, et déployé sur **Kubernetes (Minikube)** avec une pipeline **CI/CD GitHub Actions** et versioning automatique (**semantic-release**).

---

## 🎯 Objectif

Ce projet simule une architecture DevOps complète permettant :

- Agrégation d’offres d’emploi depuis plusieurs sources (HelloWork, WTTJ, Remotive)
- Traitement et scoring des offres
- Exposition via API REST
- Interface utilisateur HTML simple
- Déploiement Kubernetes avec Ingress
- Automatisation CI/CD et sécurité

---

## ⚙️ Stack technique

- Python 3.12
- FastAPI
- Uvicorn
- HTML / CSS / JavaScript (UI simple)
- Docker
- Kubernetes (Minikube)
- NGINX Ingress Controller
- GitHub Actions (CI/CD)
- semantic-release
- Pytest
- Bandit (SAST)
- pip-audit (SCA)
- Trivy (scan container)

---
📁 Structure du projet
 - sources/        → scraping des offres (HelloWork, WTTJ, Remotive)
 - core/           → scoring + logique métier
 - api.py          → API FastAPI
 - ui/             → interface HTML simple
 - tests/          → tests unitaires (pytest)

k8s/
 - deployment.yaml
 - service.yaml
 - ingress.yaml

.github/
  - workflows/ CI/CD pipelines

🎨 Interface utilisateur (UI HTML)

Le projet inclut une interface HTML simple permettant d’interagir avec l’API.

Fonctionnalités
Affichage des offres d’emploi
Appel API /jobs
Interface légère HTML/CSS/JS
Visualisation rapide des résultats
🚀 Accès UI
🔹 Mode local (Python / Docker)
http://localhost:8000/ui
🔹 Mode Kubernetes (port-forward)
kubectl port-forward service/job-aggregator-service 8080:8000

Accès :

http://localhost:8080/ui
http://localhost:8080/docs
🔹 Mode Ingress (simulation production)
http://job.local/ui
🚀 Lancer le projet
1. Mode Python
pip install -r requirements.txt
uvicorn api:app --reload
API : http://localhost:8000
Swagger : http://localhost:8000/docs
UI : http://localhost:8000/ui
2. Mode Docker
docker build -t job-aggregator .
docker run -p 8000:8000 job-aggregator
3. Mode Kubernetes (Minikube)
eval $(minikube docker-env)

docker build -t job-aggregator:1.0.0 .

kubectl apply -f k8s/
🌐 Accès Kubernetes
🔹 Mode DEV (recommandé)
kubectl port-forward service/job-aggregator-service 8080:8000
API : http://localhost:8080
Swagger : http://localhost:8080/docs
UI : http://localhost:8080/ui
🔹 Mode Ingress
http://job.local
http://job.local/ui
📊 API Endpoints
Endpoint	Description
GET /	Status API
GET /jobs	Liste des offres filtrées
GET /stats	Statistiques par source
GET /docs	Swagger UI
GET /ui	Interface utilisateur
🔐 CI/CD Pipeline

Pipeline GitHub Actions :

Tests (pytest)
SAST (Bandit)
SCA (pip-audit)
Build Docker image
Scan sécurité (Trivy)
Release automatique (semantic-release)
🔢 Versioning automatique

Basé sur Conventional Commits :

feat: → nouvelle fonctionnalité
fix: → correction
docs: → documentation

Exemple :

v1.0.0 → initial release
v1.1.0 → new features
v1.1.1 → bug fixes
☸️ Ressources Kubernetes
Deployment → application FastAPI
Service (ClusterIP / NodePort)
Ingress → routing HTTP via job.local
🎯 Objectifs DevOps atteints
✔ Containerisation Docker
✔ CI/CD automatisée
✔ Security scanning (SAST / SCA / Trivy)
✔ Kubernetes deployment
✔ Ingress HTTP routing
✔ Interface utilisateur simple
✔ Versioning automatique
✔ Architecture cloud-ready
📈 Améliorations futures
Base de données PostgreSQL
Helm charts Kubernetes
Monitoring Prometheus + Grafana
TLS (cert-manager)
Déploiement cloud (EKS / AKS)
Frontend React/Vue
Service Mesh (Istio)
👨‍💻 Auteur

Projet DevOps – Saliha Hammad
