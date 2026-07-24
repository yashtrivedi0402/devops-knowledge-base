# 🏗️ Kubernetes Architecture

> **Kubernetes Architecture defines how a Kubernetes cluster is organized to deploy, manage, scale, and monitor containerized applications.**
>
> A Kubernetes cluster consists of a **Control Plane** that makes decisions about the cluster and one or more **Worker Nodes** that run the application workloads.

---

# 📖 Table of Contents

* What is Kubernetes Architecture?
* Why Do We Need It?
* Kubernetes Cluster Components
* Control Plane Components
* Worker Node Components
* How Kubernetes Works
* Kubernetes Request Flow
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Kubernetes Architecture?

A Kubernetes cluster is divided into two main parts:

1. **Control Plane (Master Node)** – Manages and controls the cluster.
2. **Worker Nodes** – Execute containerized applications inside Pods.

The Control Plane continuously monitors the cluster and ensures that the **actual state matches the desired state** defined by the user.

---

# 🎯 Why Do We Need Kubernetes Architecture?

A production application may run across multiple servers.

Without Kubernetes:

* Manual deployment
* Manual scaling
* Manual monitoring
* Manual recovery
* Difficult networking

With Kubernetes:

* Automated scheduling
* Self-healing
* Auto scaling
* Service discovery
* High availability
* Centralized management

---

# 🏗️ Kubernetes Cluster Architecture

```text
                         User
                           │
                           ▼
                     kubectl CLI
                           │
                           ▼
                    API Server
                           │
        ┌──────────────────┼──────────────────┐
        ▼                  ▼                  ▼
    Scheduler      Controller Manager       etcd
                           │
                           ▼
────────────────────────────────────────────────────
               Worker Node 1        Worker Node 2
             ┌──────────────┐      ┌──────────────┐
             │ kubelet      │      │ kubelet      │
             │ kube-proxy   │      │ kube-proxy   │
             │ Container    │      │ Container    │
             │ Runtime      │      │ Runtime      │
             │ Pods         │      │ Pods         │
             └──────────────┘      └──────────────┘
```

---

# 🧠 Control Plane Components

The **Control Plane** is the brain of the Kubernetes cluster.

## 1️⃣ API Server

The API Server is the **entry point** for all Kubernetes requests.

Responsibilities:

* Receives requests from users and tools
* Validates requests
* Updates cluster state
* Communicates with other control plane components

Example:

```bash
kubectl get pods
```

The command is sent to the API Server.

---

## 2️⃣ etcd

**etcd** is Kubernetes' distributed key-value database.

It stores:

* Cluster configuration
* Node information
* Pod information
* Secrets
* ConfigMaps
* Desired state

Think of **etcd** as the cluster's database.

---

## 3️⃣ Scheduler

The Scheduler decides **which Worker Node should run a Pod**.

It considers:

* Available CPU
* Available Memory
* Node Labels
* Taints & Tolerations
* Affinity Rules
* Resource Requests

---

## 4️⃣ Controller Manager

The Controller Manager continuously compares:

```text
Desired State
      │
      ▼
Actual State
```

If they differ, it takes corrective action.

Examples:

* Restart failed Pods
* Create missing Pods
* Maintain ReplicaSets
* Monitor Nodes

---

# 💻 Worker Node Components

Worker Nodes are responsible for running application workloads.

## 1️⃣ kubelet

The kubelet is an agent running on every Worker Node.

Responsibilities:

* Receives instructions from the API Server
* Starts Pods
* Monitors Pods
* Reports Pod status

---

## 2️⃣ kube-proxy

kube-proxy manages networking.

Responsibilities:

* Service networking
* Load balancing
* Traffic routing
* Network rules

---

## 3️⃣ Container Runtime

The Container Runtime runs containers.

Examples:

* containerd
* CRI-O

Its responsibilities include:

* Pulling container images
* Starting containers
* Stopping containers
* Managing container lifecycle

---

## 4️⃣ Pods

A **Pod** is the smallest deployable unit in Kubernetes.

A Pod contains:

* One or more containers
* Shared network
* Shared storage

Pods are scheduled onto Worker Nodes by the Scheduler.

---

# 🔄 How Kubernetes Works

```text
Developer
     │
kubectl apply
     │
     ▼
API Server
     │
Store Configuration
     ▼
etcd
     │
Scheduler Selects Node
     ▼
Worker Node
     │
kubelet Starts Pod
     ▼
Container Runtime
     │
Application Running
```

---

# 🌐 Kubernetes Request Flow

Example:

```bash
kubectl apply -f deployment.yaml
```

Flow:

1. User submits a Deployment.
2. API Server validates the request.
3. Desired state is stored in **etcd**.
4. Scheduler selects the best Worker Node.
5. kubelet receives instructions.
6. Container Runtime pulls the image.
7. Pod starts running.
8. Controller Manager continuously monitors the application.

---

# ☁️ DevOps Perspective

Every Kubernetes deployment follows this architecture.

Typical workflow:

```text
Git Push
     │
     ▼
CI/CD Pipeline
     │
     ▼
Docker Image
     │
     ▼
Container Registry
     │
     ▼
Kubernetes API Server
     │
     ▼
Scheduler
     │
     ▼
Worker Nodes
     │
     ▼
Pods
```

Understanding the responsibilities of each component is essential for troubleshooting and production deployments.

---

# 🏭 Production Example

A company deploys an online banking application.

Deployment process:

1. Developer applies a Deployment manifest.
2. API Server accepts the request.
3. etcd stores the desired state.
4. Scheduler selects healthy Worker Nodes.
5. kubelet creates Pods.
6. Container Runtime starts the containers.
7. kube-proxy routes user traffic.
8. Controller Manager ensures the required number of Pods remain available.

If a Worker Node fails, Kubernetes automatically schedules replacement Pods on healthy nodes.

---

# 🎯 Common Interview Questions

### What are the two major parts of a Kubernetes cluster?

* Control Plane
* Worker Nodes

---

### What is the role of the API Server?

It is the entry point for all Kubernetes API requests and coordinates communication within the cluster.

---

### What is etcd?

etcd is a distributed key-value store that maintains the cluster's configuration and desired state.

---

### What does the Scheduler do?

It selects the most suitable Worker Node for newly created Pods based on resource availability and scheduling rules.

---

### What does kubelet do?

kubelet runs on every Worker Node, starts Pods, monitors them, and reports their status to the Control Plane.

---

### What is kube-proxy?

kube-proxy manages Service networking, traffic routing, and load balancing within the cluster.

---

# 🔍 Useful Commands

```bash
kubectl cluster-info

kubectl get nodes

kubectl get componentstatuses

kubectl version

kubectl get pods -A

kubectl describe node <node-name>

kubectl get namespaces
```

---

# 📑 Interview Cheat Sheet

```text
User
 │
 ▼
kubectl
 │
 ▼
API Server
 │
 ├───────────────┐
 ▼               ▼
Scheduler      etcd
 │               │
 ▼               │
Worker Node      │
 │               │
 ▼               │
kubelet          │
 │
 ▼
Container Runtime
 │
 ▼
Pod
```

Remember:

* **API Server** → Entry point
* **etcd** → Cluster database
* **Scheduler** → Selects nodes
* **Controller Manager** → Maintains desired state
* **kubelet** → Runs Pods
* **kube-proxy** → Networking
* **Container Runtime** → Executes containers

---

# 📚 Summary

Kubernetes Architecture is built around a **Control Plane** that manages the cluster and **Worker Nodes** that execute workloads. Each component has a specific responsibility, ensuring applications are deployed reliably, scaled efficiently, and automatically recovered from failures.

For DevOps Engineers, understanding Kubernetes Architecture is fundamental because it explains how every deployment, scaling event, rolling update, and self-healing operation works behind the scenes. This knowledge is essential for designing, operating, and troubleshooting production Kubernetes clusters.

---

# 🔗 Related Topics

⬅️ **Previous:** Introduction → `../01-Introduction/README.md`

➡️ **Next:** Cluster Setup → `../03-Cluster-Setup/README.md`

### 📖 Recommended Reading

* Kubernetes Pods
* Kubernetes Deployments
* Kubernetes Services
* Kubernetes Official Documentation
* CNCF Kubernetes Learning Path
