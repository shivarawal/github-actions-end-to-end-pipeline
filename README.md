# GitHub Actions End-to-End CI/CD Pipeline

## Project Overview

This project demonstrates a complete DevOps CI/CD pipeline using GitHub Actions, Docker, Docker Hub, Kubernetes, and a Self-Hosted GitHub Runner.

The goal of this project is to automate application build, testing, security scanning, container image creation, image publishing, and Kubernetes deployment using industry-standard DevOps practices.

---

## Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    v
GitHub Actions (Self-Hosted Runner)
    |
    +--> npm install
    +--> npm test
    +--> Trivy Security Scan
    +--> Docker Build
    +--> Docker Push
    |
    v
Kubernetes Deployment Rollout
    |
    v
Node.js Application
```

---

## Technologies Used

* Linux (Rocky Linux)
* Git & GitHub
* GitHub Actions
* Self-Hosted GitHub Runner
* Node.js
* Docker
* Docker Hub
* Kubernetes (kubeadm)
* Containerd
* Trivy Security Scanner

---

## Project Structure

```text
.
├── app.js
├── Dockerfile
├── package.json
├── package-lock.json
├── k8s
│   ├── deployment.yaml
│   └── service.yaml
└── .github
    └── workflows
        └── ci.yml
```

---

## Application Features

* Node.js Web Application
* Health Check Endpoint
* Dockerized Application
* Kubernetes Deployment
* Kubernetes Service
* Readiness Probe
* Liveness Probe

Endpoints:

```bash
/
```

Response:

```text
Hello from Node.js app!
```

Health Check:

```bash
/health
```

Response:

```json
{
  "status": "UP"
}
```

---

## CI/CD Pipeline Workflow

### Continuous Integration

When code is pushed to the main branch:

1. Checkout Source Code
2. Install Dependencies
3. Execute Tests
4. Run Trivy Security Scan
5. Build Docker Image

### Continuous Delivery

6. Push Docker Image to Docker Hub
7. Connect to Kubernetes Cluster
8. Restart Deployment
9. Verify Rollout Status

---

## Docker Commands

Build Image

```bash
docker build -t shivarawal81/nodejs-cicd-app:latest .
```

Run Container

```bash
docker run -d -p 3000:3000 shivarawal81/nodejs-cicd-app:latest
```

---

## Kubernetes Deployment

Deploy Application

```bash
kubectl apply -f k8s/
```

Verify Pods

```bash
kubectl get pods
```

Verify Service

```bash
kubectl get svc
```

Rollout Restart

```bash
kubectl rollout restart deployment nodejs-app
```

---

## Self-Hosted GitHub Runner

This project uses a self-hosted GitHub Actions runner running on the Kubernetes master node.

Benefits:

* Full control over execution environment
* Direct access to Kubernetes cluster
* Faster deployment process
* Real-world production experience

---

## Security Implementation

### Trivy Security Scan

Trivy is integrated into the GitHub Actions workflow.

Security checks:

* Dependency vulnerabilities
* Package vulnerabilities
* Secret detection
* Misconfiguration checks

---

## Challenges Faced

### Issue 1

Docker daemon not available on self-hosted runner.

Solution:

* Installed Docker Engine
* Started Docker service
* Added runner user to docker group

### Issue 2

Kubernetes deployment failed.

Solution:

* Copied Kubernetes admin.conf to runner user
* Configured kubectl access

### Issue 3

CrashLoopBackOff in Kubernetes.

Solution:

* Fixed Dockerfile syntax errors
* Rebuilt Docker image
* Redeployed application

---

## Learning Outcomes

Through this project I learned:

* GitHub Actions workflow creation
* Self-hosted runner setup
* Docker image build and push
* Kubernetes deployment management
* Security scanning with Trivy
* CI/CD automation
* Kubernetes troubleshooting
* Production deployment practice
