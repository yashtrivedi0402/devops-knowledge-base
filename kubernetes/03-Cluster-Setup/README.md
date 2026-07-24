# ⚙️ Kubernetes Cluster Setup

> **A Kubernetes Cluster is a group of machines (nodes) that work together to run containerized applications.**
>
> Before deploying applications, a Kubernetes cluster must be created and configured. This module explains different cluster setup methods, required components, installation tools, and best practices for both learning and production environments.

---

# 📖 Table of Contents

* What is a Kubernetes Cluster?
* Why Do We Need a Cluster?
* Types of Kubernetes Clusters
* Cluster Components
* Kubernetes Installation Tools
* Setting Up a Local Cluster
* Verifying the Cluster
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Kubernetes Cluster?

A **Kubernetes Cluster** is a collection of one or more machines that work together to run and manage containerized applications.

A cluster consists of:

* Control Plane
* One or More Worker Nodes

Together, they provide:

* High Availability
* Scalability
* Fault Tolerance
* Automated Management

---

# 🎯 Why Do We Need a Cluster?

Running Kubernetes requires multiple components working together.

A cluster provides:

* Centralized management
* Automatic scheduling
* Self-healing
* Scaling
* Networking
* Storage management

Instead of managing individual containers manually, the cluster manages the entire application lifecycle.

---

# 🏗️ Kubernetes Cluster Architecture

```text
                    Kubernetes Cluster
                           │
        ┌──────────────────┴──────────────────┐
        ▼                                     ▼
   Control Plane                        Worker Node(s)
        │                                     │
 ┌──────┼─────────┐                   ┌────────┼────────┐
 ▼      ▼         ▼                   ▼        ▼        ▼
API   Scheduler  etcd            kubelet  kube-proxy  Pods
Server Controller
```

---

# 🌍 Types of Kubernetes Clusters

## 1️⃣ Local Cluster

Used for:

* Learning
* Development
* Testing

Popular tools:

* Minikube
* KIND (Kubernetes IN Docker)
* Docker Desktop Kubernetes

---

## 2️⃣ On-Premises Cluster

Installed on physical or virtual servers inside an organization's data center.

Common tools:

* kubeadm
* Rancher
* OpenShift

---

## 3️⃣ Managed Kubernetes Services

Cloud providers manage the Control Plane.

Examples:

| Cloud Provider | Managed Service                |
| -------------- | ------------------------------ |
| AWS            | Amazon EKS                     |
| Azure          | Azure Kubernetes Service (AKS) |
| Google Cloud   | Google Kubernetes Engine (GKE) |

These services reduce operational overhead by handling upgrades, backups, and high availability.

---

# 🛠️ Kubernetes Installation Tools

## Minikube

* Single-node cluster
* Beginner-friendly
* Ideal for local development

---

## KIND (Kubernetes IN Docker)

* Runs Kubernetes nodes as Docker containers
* Lightweight
* Excellent for CI/CD testing

---

## kubeadm

* Official Kubernetes bootstrap tool
* Used to create production-ready clusters
* Supports multi-node environments

---

# 🚀 Setting Up a Local Cluster

## Using Minikube

### Start the Cluster

```bash
minikube start
```

---

### Check Cluster Status

```bash
minikube status
```

---

### Stop the Cluster

```bash
minikube stop
```

---

### Delete the Cluster

```bash
minikube delete
```

---

## Using KIND

### Create a Cluster

```bash
kind create cluster --name dev-cluster
```

---

### List Clusters

```bash
kind get clusters
```

---

### Delete the Cluster

```bash
kind delete cluster --name dev-cluster
```

---

# ✅ Verifying the Cluster

Check cluster information:

```bash
kubectl cluster-info
```

---

List all nodes:

```bash
kubectl get nodes
```

Example output:

```text
NAME                 STATUS   ROLES           AGE   VERSION
control-plane        Ready    control-plane   10m   v1.33.x
```

---

View system Pods:

```bash
kubectl get pods -A
```

---

Check Kubernetes version:

```bash
kubectl version
```

---

# ☁️ DevOps Perspective

Different environments use different cluster setup methods:

| Environment               | Recommended Tool |
| ------------------------- | ---------------- |
| Learning                  | Minikube         |
| Local Development         | KIND             |
| Production (Self-managed) | kubeadm          |
| AWS                       | Amazon EKS       |
| Azure                     | AKS              |
| Google Cloud              | GKE              |

In most enterprise environments, managed Kubernetes services are preferred because they reduce operational complexity and provide built-in high availability.

---

# 🏭 Production Example

A company wants to deploy a banking application.

Development:

```text
Developer Laptop
       │
       ▼
     Minikube
```

Testing:

```text
CI/CD Pipeline
      │
      ▼
     KIND
```

Production:

```text
GitHub
    │
    ▼
Jenkins Pipeline
    │
    ▼
Amazon EKS
    │
    ▼
Worker Nodes
    │
    ▼
Pods
```

Each environment serves a different purpose while using the same Kubernetes concepts.

---

# 🎯 Common Interview Questions

### What is a Kubernetes Cluster?

A Kubernetes Cluster is a group of machines that work together to deploy, manage, and scale containerized applications.

---

### What are the two main parts of a Kubernetes Cluster?

* Control Plane
* Worker Nodes

---

### What is Minikube?

Minikube is a tool for running a local single-node Kubernetes cluster, mainly for learning and development.

---

### What is KIND?

KIND (Kubernetes IN Docker) runs Kubernetes clusters inside Docker containers and is commonly used for testing and CI/CD.

---

### What is kubeadm?

kubeadm is the official Kubernetes tool used to bootstrap and configure Kubernetes clusters, especially self-managed production clusters.

---

### Which managed Kubernetes services are commonly used?

* Amazon EKS
* Azure Kubernetes Service (AKS)
* Google Kubernetes Engine (GKE)

---

# 🔍 Useful Commands

```bash
kubectl cluster-info

kubectl get nodes

kubectl get pods -A

kubectl version

minikube start

minikube stop

minikube status

kind create cluster

kind get clusters

kind delete cluster
```

---

# 📑 Interview Cheat Sheet

```text
Laptop
   │
   ▼
Minikube / KIND
   │
   ▼
Kubernetes Cluster
   │
   ├──────────────┐
   ▼              ▼
Control Plane  Worker Nodes
                    │
                    ▼
                   Pods
```

Remember:

* **Minikube** → Learning & Development
* **KIND** → Docker-based local clusters & CI/CD
* **kubeadm** → Self-managed production clusters
* **EKS / AKS / GKE** → Managed Kubernetes services
* Always verify cluster health using `kubectl cluster-info` and `kubectl get nodes`.

---

# 📚 Summary

A Kubernetes Cluster provides the infrastructure required to deploy and manage containerized applications. Whether using Minikube for learning, KIND for testing, kubeadm for self-managed environments, or managed services like Amazon EKS, the underlying Kubernetes concepts remain consistent.

For DevOps Engineers, understanding cluster setup is essential because it forms the foundation for deploying workloads, configuring networking, managing storage, and operating production Kubernetes environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Kubernetes Architecture → `../02-Kubernetes-Architecture/README.md`

➡️ **Next:** Pods → `../04-Pods/README.md`

### 📖 Recommended Reading

* Kubernetes Pods
* Kubernetes Architecture
* KIND Documentation
* Minikube Documentation
* Kubernetes Official Documentation
