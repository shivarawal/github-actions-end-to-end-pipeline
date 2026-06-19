# GitHub Actions End-to-End CI Pipeline with Kubernetes

## Overview

This project demonstrates a complete CI pipeline using GitHub Actions, Docker, Docker Hub, and Kubernetes.

The application is a simple Node.js web service that exposes:

* `/` → Returns a welcome message
* `/health` → Returns application health status

The project automatically:

1. Runs tests using GitHub Actions
2. Builds a Docker image
3. Pushes the image to Docker Hub
4. Deploys the application to Kubernetes

---

## Tech Stack

* Git
* GitHub
* GitHub Actions
* Node.js
* Docker
* Docker Hub
* Kubernetes (kubeadm)

---

## Project Structure

```text
github-actions-end-to-end-pipeline/
├── app.js
├── Dockerfile
├── package.json
├── package-lock.json
├── .github/
│   └── workflows/
│       └── ci.yml
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
└── README.md
```

---

## CI Pipeline Flow

```text
Developer Push
      ↓
GitHub Actions
      ↓
Install Dependencies
      ↓
Run Tests
      ↓
Build Docker Image
      ↓
Push Image to Docker Hub
```

---

## Kubernetes Deployment

Deployment:

* 2 replicas
* Readiness Probe
* Liveness Probe

Service:

* NodePort Service
* Application exposed on Kubernetes cluster

---

## Docker Image

Docker Hub Repository:

```text
shivarawal81/nodejs-cicd-app
```

---

## Application Endpoints

Home Page:

```bash
curl http://<NODE-IP>:<NODEPORT>
```

Response:

```text
Hello from Node.js app!
```

Health Check:

```bash
curl http://<NODE-IP>:<NODEPORT>/health
```

Response:

```json
{"status":"UP"}
```

---

## Challenges Faced

### GitHub Actions Workflow Permission Issue

Issue:

```text
Personal Access Token missing workflow scope
```

Resolution:

* Created a new GitHub Personal Access Token
* Added workflow permissions

### Dockerfile Syntax Error

Issue:

```dockerfile
CMD ["node, "app.js"]
```

Resolution:

```dockerfile
CMD ["node", "app.js"]
```

### Kubernetes CrashLoopBackOff

Issue:

Application container repeatedly crashed.

Resolution:

* Investigated pod logs
* Corrected Dockerfile syntax
* Rebuilt Docker image
* Restarted deployment

---

## Learning Outcomes

* Git Workflow
* GitHub Actions CI
* Docker Image Build
* Docker Hub Integration
* Kubernetes Deployment
* Kubernetes Service Exposure
* Troubleshooting CrashLoopBackOff
* Health Checks
* Container Logging
* Rolling Updates

---

## Future Improvements

* Docker Image Versioning
* Trivy Security Scanning
* Automatic Kubernetes Deployment
* Helm Charts
* ArgoCD Integration
* Monitoring with Prometheus and Grafana
* Production Release Workflow

```
```

# test
