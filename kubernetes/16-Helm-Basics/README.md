# ⛵ Kubernetes Helm Basics

> **Helm is the package manager for Kubernetes that simplifies deploying, managing, upgrading, and versioning applications using reusable templates called Charts.**
>
> Instead of writing and managing dozens of Kubernetes YAML files manually, Helm allows you to package all Kubernetes resources into a single, reusable Chart, making deployments faster, more consistent, and easier to maintain.

---

# 📖 Table of Contents

* What is Helm?
* Why Do We Need Helm?
* Problems Without Helm
* Helm Architecture
* Helm Components
* Helm Charts
* Helm Repository
* Installing Applications with Helm
* Helm Upgrade & Rollback
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Helm?

**Helm** is the **official package manager for Kubernetes**.

Think of Helm as:

* **APT** for Ubuntu
* **YUM/DNF** for RHEL
* **npm** for Node.js
* **pip** for Python

But for Kubernetes applications.

Instead of applying multiple YAML files manually:

```bash id="8v2n5g"
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f pvc.yaml
```

You simply run:

```bash id="6d7nrx"
helm install my-app ./chart
```

Helm creates and manages all Kubernetes resources automatically.

---

# 🎯 Why Do We Need Helm?

Managing Kubernetes applications manually becomes difficult as applications grow.

Imagine deploying:

* Deployment
* Service
* Ingress
* ConfigMap
* Secret
* PVC
* ServiceAccount
* RBAC
* HPA

Without Helm:

```text id="rz9v5w"
Application
     │
     ├── deployment.yaml
     ├── service.yaml
     ├── ingress.yaml
     ├── secret.yaml
     ├── configmap.yaml
     ├── pvc.yaml
     └── ...
```

Problems:

* Too many YAML files
* Duplicate configurations
* Difficult version management
* Manual upgrades
* Error-prone deployments

Helm packages everything into a single Chart.

---

# ❌ Problems Without Helm

```text id="j8ukoe"
Developer
     │
Writes 15 YAML Files
     │
Applies Files One by One
     │
Manual Updates
```

With Helm:

```text id="otkpd6"
Developer
     │
Helm Chart
     │
helm install
     │
Application Deployed
```

---

# 🏗️ Helm Architecture

```text id="3um9lf"
               Helm CLI
                   │
                   ▼
             Helm Chart
                   │
                   ▼
         Kubernetes API Server
                   │
                   ▼
Deployment • Service • Ingress
ConfigMap • Secret • PVC
                   │
                   ▼
              Kubernetes Cluster
```

The Helm CLI communicates with the Kubernetes API Server and deploys all resources defined in a Chart.

---

# 🧩 Helm Components

### 1️⃣ Helm CLI

The command-line tool used to install, upgrade, rollback, and manage Helm releases.

---

### 2️⃣ Chart

A **Chart** is a package containing all Kubernetes manifests required to deploy an application.

Typical Chart structure:

```text id="scgdhm"
my-chart/
│
├── Chart.yaml
├── values.yaml
├── templates/
│     ├── deployment.yaml
│     ├── service.yaml
│     ├── ingress.yaml
│     └── ...
└── charts/
```

---

### 3️⃣ Repository

A Helm Repository stores and distributes Charts.

Popular repositories include:

* Bitnami
* Artifact Hub
* Grafana
* Prometheus Community

---

### 4️⃣ Release

A **Release** is a deployed instance of a Helm Chart.

Example:

```text id="jpw31g"
Chart
     │
helm install
     │
Release
```

The same Chart can create multiple Releases with different configurations.

---

# 📦 Helm Charts

A Chart contains:

* Metadata (`Chart.yaml`)
* Configuration (`values.yaml`)
* Kubernetes Templates (`templates/`)
* Dependencies (`charts/`)

Example:

```text id="l5pygm"
Chart.yaml
      │
values.yaml
      │
templates/
      │
Deployment
Service
Ingress
ConfigMap
```

---

# 🌐 Helm Repository

Add a repository:

```bash id="hn7ggk"
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Update repositories:

```bash id="8gjlwm"
helm repo update
```

Search for Charts:

```bash id="up4h9u"
helm search repo nginx
```

Repositories make it easy to install production-ready applications.

---

# 🚀 Installing an Application

Install NGINX:

```bash id="0r5c2d"
helm install nginx bitnami/nginx
```

Check releases:

```bash id="kwy4if"
helm list
```

The application is deployed with all required Kubernetes resources.

---

# 🔄 Upgrading an Application

Upgrade using new values:

```bash id="jajyqu"
helm upgrade nginx bitnami/nginx
```

Helm updates only the resources that changed.

---

# ⏪ Rolling Back

View release history:

```bash id="cqwnv8"
helm history nginx
```

Rollback:

```bash id="9cjlwm"
helm rollback nginx 1
```

If a deployment fails, Helm can quickly restore a previous working version.

---

# ☁️ DevOps Perspective

Helm is widely used in CI/CD pipelines.

Typical deployment flow:

```text id="xls8su"
Git Repository
       │
       ▼
CI/CD Pipeline
       │
       ▼
Helm Chart
       │
helm upgrade --install
       │
       ▼
Kubernetes Cluster
```

Production use cases:

* NGINX Ingress Controller
* Prometheus
* Grafana
* Argo CD
* Jenkins
* Elasticsearch
* Kafka

Helm simplifies deployment, upgrades, and configuration management across environments.

---

# 🏭 Production Example

A company deploys an e-commerce platform.

Instead of maintaining multiple YAML files:

```text id="xv35dq"
Deployment
Service
Ingress
ConfigMap
Secret
PVC
HPA
RBAC
```

The DevOps team creates one Helm Chart.

Deployment workflow:

```text id="bwdjlwm"
GitHub
     │
     ▼
Jenkins Pipeline
     │
     ▼
helm upgrade --install ecommerce
     │
     ▼
Kubernetes Cluster
```

When a new version is released:

* Update the Chart
* Run one Helm command
* Kubernetes performs a rolling update
* Roll back instantly if required

---

# 🎯 Common Interview Questions

### What is Helm?

Helm is the package manager for Kubernetes that packages, deploys, upgrades, and manages Kubernetes applications using Charts.

---

### What is a Helm Chart?

A Chart is a package containing all Kubernetes manifests, templates, metadata, and configuration required to deploy an application.

---

### What is a Helm Release?

A Release is a deployed instance of a Helm Chart running inside a Kubernetes cluster.

---

### What is `values.yaml`?

`values.yaml` stores configurable values used by Helm templates, allowing the same Chart to be deployed with different settings.

---

### Why is Helm preferred in production?

Because it provides:

* Reusable templates
* Version control
* Easy upgrades
* Rollbacks
* Consistent deployments
* Simplified CI/CD integration

---

# 🔍 Useful Commands

```bash id="4kblzv"
helm version

helm repo add bitnami https://charts.bitnami.com/bitnami

helm repo update

helm search repo nginx

helm install nginx bitnami/nginx

helm list

helm upgrade nginx bitnami/nginx

helm history nginx

helm rollback nginx 1

helm uninstall nginx
```

---

# 📑 Interview Cheat Sheet

```text id="x43ec8"
Helm CLI
    │
    ▼
Chart
    │
    ▼
Release
    │
    ▼
Kubernetes Cluster
```

Remember:

* **Helm = Kubernetes Package Manager**
* **Chart = Application Package**
* **Release = Installed Chart**
* **Repository = Collection of Charts**
* **values.yaml = Custom Configuration**
* **Templates generate Kubernetes manifests**
* **Helm supports upgrades and rollbacks**
* **Helm is widely used in production CI/CD pipelines**

---

# 📚 Summary

Helm simplifies Kubernetes application management by packaging multiple Kubernetes resources into reusable Charts. It enables consistent deployments, centralized configuration management, version control, seamless upgrades, and quick rollbacks, making Kubernetes operations significantly more efficient.

For DevOps Engineers, Helm is an essential tool because most production Kubernetes environments rely on Helm Charts to deploy and manage complex applications with minimal manual effort.

---

# 🔗 Related Topics

⬅️ **Previous:** RBAC → `../15-RBAC/README.md`

➡️ **Next:** Troubleshooting → `../17-Troubleshooting/README.md`

### 📖 Recommended Reading

* Kubernetes Troubleshooting
* Helm Official Documentation
* Artifact Hub
* Kubernetes Package Management
* Helm Best Practices
