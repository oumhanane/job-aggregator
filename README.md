# 🚀 Job Aggregator – Cloud Native DevOps Project

A personal **Cloud Native DevOps project** for aggregating job offers from multiple sources, processing them through a Python backend, and deploying the application on Kubernetes with a complete DevOps and GitOps workflow.

The project demonstrates the implementation of a modern software delivery pipeline combining:

* 🐍 Python / FastAPI
* 🐳 Docker
* ☸️ Kubernetes
* 🔄 GitHub Actions
* 🚀 Semantic Release
* 🔐 Kubernetes security hardening
* 🔄 GitOps with Argo CD
* 📊 Prometheus & Grafana
* 🌐 NGINX Ingress
* 🧪 Automated testing and security scanning

---

## 🎯 Project Objective

The objective of **Job Aggregator** is to build a realistic Cloud Native application while applying DevOps, Kubernetes, GitOps, observability, and security best practices.

The application:

1. Collects job offers from multiple sources.
2. Normalizes the collected data.
3. Filters and scores job offers.
4. Exposes the data through a FastAPI REST API.
5. Provides a lightweight web interface.
6. Packages the application as a Docker image.
7. Deploys the application on Kubernetes.
8. Uses Argo CD to implement GitOps.
9. Applies Kubernetes security controls.
10. Integrates CI/CD, testing, security scanning, and automated releases.

---

# 🛠️ Technical Stack

| Category                     | Technologies                               |
| ---------------------------- | ------------------------------------------ |
| Backend                      | Python 3.12, FastAPI, Uvicorn              |
| Frontend                     | HTML, CSS, JavaScript                      |
| Data Sources                 | Remotive, Welcome to the Jungle, HelloWork |
| Application Logic            | Python                                     |
| Containerization             | Docker, Docker Compose                     |
| Orchestration                | Kubernetes, Minikube                       |
| Ingress                      | NGINX Ingress Controller                   |
| CI                           | GitHub Actions                             |
| Release Management           | Semantic Release                           |
| Container Registry           | Docker Hub                                 |
| GitOps                       | Argo CD                                    |
| Monitoring                   | Prometheus, Grafana                        |
| Testing                      | Pytest                                     |
| Security                     | Bandit, pip-audit, Trivy                   |
| Kubernetes Security          | Pod Security Admission                     |
| Infrastructure Configuration | Kubernetes YAML                            |

---

# 📁 Project Structure

```text
job-aggregator/
├── CHANGELOG.md
├── Dockerfile
├── README.md
├── api.py
├── app.py
├── bandit.yaml
├── config.py
├── docker-compose.yml
├── generate_html.py
├── package-lock.json
├── package.json
├── requirements.txt
│
├── core/
│   ├── filter.py
│   ├── normalize.py
│   └── scorer.py
│
├── sources/
│   ├── hellowork.py
│   ├── hellowork_pw.py
│   ├── remotive.py
│   └── wttj.py
│
├── static/
│   └── index.html
│
├── tests/
│   └── test_api.py
│
├── k8s/
│   ├── app/
│   ├── infrastructure/
│   └── monitoring/
│
├── argocd/
│   ├── application.yaml
│   └── project.yaml
│
└── .github/
    └── workflows/
```

### Main directories

* `core/` — application business logic: filtering, normalization, and scoring.
* `sources/` — job offer connectors and data collection logic.
* `tests/` — automated application tests.
* `static/` — web interface.
* `k8s/app/` — Kubernetes application resources.
* `k8s/infrastructure/` — Kubernetes infrastructure resources such as the production namespace.
* `k8s/monitoring/` — monitoring configuration.
* `argocd/` — Argo CD Application and Project definitions.
* `.github/workflows/` — CI/CD and release automation.

Generated and local directories such as `__pycache__`, `venv`, `node_modules`, and `output` are excluded from the documented project structure.

---

# 🖥️ Application

The application provides a web interface for retrieving and displaying aggregated job offers.

The backend is implemented with **FastAPI** and exposes REST endpoints used by the frontend.

The application architecture separates:

```text
Data Sources
     ↓
Normalization
     ↓
Filtering
     ↓
Scoring
     ↓
FastAPI API
     ↓
Web Interface
```

---

# 🧠 Application Logic

The `core/` directory contains the main processing logic.

### `normalize.py`

Normalizes job offer data coming from different sources into a consistent structure.

### `filter.py`

Applies filtering criteria to the collected job offers.

### `scorer.py`

Calculates a relevance score for job offers based on the configured criteria.

This separation makes the application easier to maintain and extend with additional job sources or scoring rules.

---

# 🌐 Job Sources

The application currently integrates several job offer sources:

* Remotive
* Welcome to the Jungle
* HelloWork

The `sources/` directory isolates source-specific collection logic from the rest of the application.

This makes it possible to add new job platforms without significantly modifying the core application logic.

---

# 🧪 Testing

Automated tests are implemented with **Pytest**.

Tests are located in:

```text
tests/
└── test_api.py
```

Tests can be executed locally with:

```bash
pytest
```

---

# 🐳 Docker

The application is containerized using Docker.

Build the image:

```bash
docker build -t job-aggregator .
```

Run the container:

```bash
docker run -p 8000:8000 job-aggregator
```

The project also contains a `docker-compose.yml` file for local containerized execution.

---

# ☸️ Kubernetes Deployment

The application is deployed on Kubernetes using **Minikube** for local development and experimentation.

The Kubernetes configuration is organized into separate concerns:

```text
k8s/
├── infrastructure/
├── app/
└── monitoring/
```

### Application resources

The application deployment contains:

* Kubernetes Deployment
* Kubernetes Service
* NGINX Ingress

The application runs with:

```text
replicas: 2
```

This provides basic redundancy within the Kubernetes cluster.

The deployment also uses:

* RollingUpdate strategy
* Readiness probe
* Liveness probe
* CPU and memory requests
* CPU and memory limits

---

# 🔐 Kubernetes Security Hardening

Security is implemented using Kubernetes native security controls.

The `production` namespace uses **Pod Security Admission (PSA)** with the `restricted` security standard.

Namespace configuration:

```text
pod-security.kubernetes.io/enforce=restricted
pod-security.kubernetes.io/audit=restricted
pod-security.kubernetes.io/warn=restricted
```

The application containers are hardened with:

```yaml
securityContext:
  privileged: false
  allowPrivilegeEscalation: false
  readOnlyRootFilesystem: true
  capabilities:
    drop:
      - ALL
```

The Pod security context also enforces:

```yaml
securityContext:
  runAsUser: 1000
  runAsGroup: 1000
  runAsNonRoot: true
  seccompProfile:
    type: RuntimeDefault
```

### Security controls implemented

| Security Control              | Status       |
| ----------------------------- | ------------ |
| Pod Security Admission        | ✅ Restricted |
| Non-root container            | ✅            |
| Fixed UID/GID                 | ✅            |
| Privileged mode disabled      | ✅            |
| Privilege escalation disabled | ✅            |
| Linux capabilities dropped    | ✅            |
| Read-only root filesystem     | ✅            |
| Seccomp RuntimeDefault        | ✅            |
| Resource requests/limits      | ✅            |
| Liveness probe                | ✅            |
| Readiness probe               | ✅            |

---

# 🌐 Kubernetes Ingress

The application is exposed through the **NGINX Ingress Controller**.

The configured hostname is:

```text
job.local
```

The Ingress routes traffic to:

```text
job-aggregator-ingress
        ↓
job-aggregator-service
        ↓
FastAPI application
```

For local Minikube testing, the hostname can be mapped to the Minikube IP through the local hosts configuration.

---

# 🔄 GitOps with Argo CD

The Kubernetes deployment follows a **GitOps approach** using Argo CD.

The Git repository acts as the **Single Source of Truth**.

Argo CD Application:

```text
job-aggregator
```

Configuration:

```text
Project:       job-aggregator
Namespace:     production
Repository:    GitHub
Branch:        main
Path:          k8s/app
```

Argo CD automated synchronization is enabled:

```yaml
syncPolicy:
  automated:
    prune: true
    selfHeal: true
```

This provides:

* Automatic synchronization
* Automatic pruning of removed resources
* Self-healing when Kubernetes resources drift from Git
* Declarative infrastructure management

The deployment workflow is therefore:

```text
Developer
    ↓
Git commit
    ↓
GitHub
    ↓
Argo CD
    ↓
Kubernetes
    ↓
Production Namespace
```

---

# 📊 Kubernetes Observability

The project integrates **Prometheus and Grafana** using the Kubernetes monitoring stack.

The monitoring configuration is located under:

```text
k8s/monitoring/
```

The monitoring architecture is:

```text
Kubernetes
     ↓
Prometheus
     ↓
Metrics
     ↓
Grafana
     ↓
Dashboards
```

The current monitoring implementation focuses primarily on Kubernetes infrastructure and cluster-level observability.

Application-level FastAPI instrumentation and dedicated application dashboards are planned improvements.

---

# 🔄 Continuous Integration

GitHub Actions is used to automate the CI process.

The CI pipeline includes activities such as:

* Python dependency installation
* Automated testing
* Static security analysis
* Dependency security scanning
* Container security scanning

Security tools currently integrated include:

* **Bandit** — Python security analysis
* **pip-audit** — Python dependency vulnerability scanning
* **Trivy** — container and filesystem vulnerability scanning

The CI workflow is located in:

```text
.github/workflows/ci.yaml
```

---

# 🚀 Automatic Release

The project uses **Semantic Release** and Conventional Commits to automate version management.

Examples of Conventional Commit types:

```text
feat: add new job source
fix: correct job filtering
docs: update README
refactor: improve scoring logic
```

Semantic Release automatically manages:

* Version calculation
* Git tags
* Changelog generation
* Release commits

The generated changelog is stored in:

```text
CHANGELOG.md
```

---

# 🐳 Docker Release

Docker image releases are automated through GitHub Actions.

The Docker release workflow builds and publishes the application image to Docker Hub.

Current Docker image:

```text
saliha91700/job-aggregator
```

The workflow is located in:

```text
.github/workflows/docker-release.yaml
```

---

# 🔁 Complete DevOps Workflow

The complete project workflow can be summarized as:

```text
                 Developer
                     │
                     ▼
                Git Commit
                     │
                     ▼
                  GitHub
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
     GitHub Actions         Semantic Release
          │                     │
          ▼                     ▼
     Tests & Security       Version / Tag
          │
          ▼
       Docker Build
          │
          ▼
      Docker Hub
          │
          ▼
        Argo CD
          │
          ▼
       Kubernetes
          │
     ┌────┴────┐
     ▼         ▼
  FastAPI    NGINX
     │         │
     └────┬────┘
          ▼
       Users
          
Kubernetes
     │
     ▼
Prometheus
     │
     ▼
Grafana
```

---

# 🛡️ Security & Reliability Model

The project applies a defense-in-depth approach across several layers:

```text
┌──────────────────────────────────────┐
│              CI / CD                 │
│  Tests • Bandit • pip-audit • Trivy │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│             Kubernetes               │
│   PSA Restricted • Non-root •        │
│   Seccomp • Capabilities • Probes    │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│             Container                │
│   Non-root • Read-only filesystem   │
│   No privilege escalation            │
└──────────────────┬───────────────────┘
                   │
                   ▼
┌──────────────────────────────────────┐
│              Runtime                 │
│       Prometheus • Grafana           │
└──────────────────────────────────────┘
```

---

# 📚 DevOps Skills Demonstrated

This project demonstrates practical experience with:

### Application

* Python
* FastAPI
* REST API
* Data normalization
* Filtering
* Scoring logic
* Automated testing

### Containers

* Docker
* Docker Compose
* Container security

### Kubernetes

* Deployments
* Services
* Ingress
* Namespaces
* Probes
* Resource management
* Security contexts
* Pod Security Admission

### CI/CD

* GitHub Actions
* Conventional Commits
* Semantic Release
* Automated testing
* Security scanning
* Docker image publishing

### GitOps

* Argo CD
* Declarative Kubernetes configuration
* Automated synchronization
* Self-healing
* Pruning
* Git as the Single Source of Truth

### Observability

* Prometheus
* Grafana
* Kubernetes monitoring

---

# ✅ Completed / 🔜 Future Improvements

## ✅ Implemented

* [x] FastAPI backend
* [x] Multiple job sources
* [x] Job normalization
* [x] Job filtering
* [x] Job scoring
* [x] Automated tests
* [x] Docker containerization
* [x] Kubernetes deployment
* [x] Kubernetes Ingress
* [x] NGINX Ingress Controller
* [x] Kubernetes Pod Security Admission
* [x] Restricted security profile
* [x] Non-root containers
* [x] Seccomp RuntimeDefault
* [x] Linux capabilities dropped
* [x] Read-only root filesystem
* [x] Resource requests and limits
* [x] Liveness and readiness probes
* [x] GitHub Actions CI
* [x] Bandit
* [x] pip-audit
* [x] Trivy
* [x] Semantic Release
* [x] Docker image release
* [x] Argo CD GitOps
* [x] Automated synchronization
* [x] Self-healing
* [x] Prometheus
* [x] Grafana

## 🔜 Planned Improvements

### Security

* [ ] Kubesec
* [ ] Kube-bench
* [ ] Falco
* [ ] Kube-hunter
* [ ] Network Policies
* [ ] Vault
* [ ] cert-manager

### Observability

* [ ] FastAPI application instrumentation
* [ ] Prometheus ServiceMonitor
* [ ] Custom Grafana dashboards
* [ ] Application-level alerts

### Kubernetes / Platform

* [ ] Helm
* [ ] Horizontal Pod Autoscaler
* [ ] Argo Rollouts
* [ ] Argo Image Updater
* [ ] Deployment on AWS EKS
* [ ] Deployment on Azure AKS
* [ ] Deployment on GKE

### Architecture

* [ ] Evolution toward microservices
* [ ] Event-driven architecture
* [ ] Improved scalability and resilience
* [ ] Job recommendation capabilities using ML/MLOps

---

# 🧩 Troubleshooting & Lessons Learned

This project is also used as a practical environment for understanding Kubernetes behavior and debugging real deployment issues.

## Pod Security Admission

When the `production` namespace was configured with the `restricted` Pod Security standard, Kubernetes initially rejected the application Pods because the required Seccomp profile was missing.

The deployment was updated with:

```yaml
seccompProfile:
  type: RuntimeDefault
```

After this change, the Pods were successfully admitted by Kubernetes.

This highlighted an important Kubernetes security principle:

> Security policies must be considered at the namespace, Pod, and container levels.

---

## Ingress Conflict

An old Ingress resource remained in the `default` namespace with the same host and path:

```text
host: job.local
path: /
```

The NGINX admission webhook therefore rejected the new Ingress in the `production` namespace.

The obsolete resource was removed, allowing Argo CD to recreate the intended Ingress.

The final state became:

```text
Argo CD:      Synced / Healthy
Deployment:   2/2
Pods:         2/2 Running
Service:      Synced
Ingress:      Synced
```

This incident demonstrated the importance of:

* Checking resources across all namespaces
* Understanding admission webhooks
* Investigating Argo CD resource status
* Keeping Kubernetes resources aligned with Git
* Avoiding orphaned resources after architectural changes

---

# 🏗️ Current Architecture

```text
                       GitHub
                          │
              ┌───────────┴───────────┐
              │                       │
              ▼                       ▼
       GitHub Actions            Argo CD
              │                       │
       ┌──────┴──────┐                │
       ▼             ▼                │
     Tests       Security             │
       │          Scanning            │
       │             │                │
       └──────┬──────┘                │
              ▼                       ▼
          Docker Hub             Kubernetes
                                      │
                              ┌───────┴────────┐
                              │                │
                              ▼                ▼
                           Ingress          Monitoring
                              │                │
                              ▼           Prometheus
                           Service             │
                              │             Grafana
                              ▼
                           FastAPI
                              │
                    ┌─────────┼─────────┐
                    ▼         ▼         ▼
                Remotive  HelloWork    WTTJ
```

---

# 🎓 Project Goal

The long-term goal of **Job Aggregator** is to progressively evolve the application from a personal Kubernetes project into a more complete **Cloud Native platform**, while continuing to apply DevOps, security, observability, GitOps, and eventually MLOps practices.

The project is intentionally developed incrementally, with each new capability documented and integrated into the existing architecture.

---

# 👩‍💻 Author

**Saliha Hammad**

Cloud Native / DevOps Engineer

Interested in:

* DevOps
* Kubernetes
* Cloud Native
* GitOps
* Platform Engineering
* Cloud Security
* MLOps

---

⭐ This project is continuously evolving as a practical learning and portfolio project.
