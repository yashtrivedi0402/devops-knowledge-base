# 📦 Kubernetes Pods

> **A Pod is the smallest and most basic deployable unit in Kubernetes.**
>
> A Pod acts as a wrapper around one or more containers, providing them with shared networking, storage, and lifecycle management. Every application running in Kubernetes is deployed inside a Pod.

---

# 📖 Table of Contents

* What is a Pod?
* Why Do We Need Pods?
* Pod Architecture
* Pod Lifecycle
* Single-Container vs Multi-Container Pods
* Creating Pods
* Managing Pods
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Pod?

A **Pod** is the smallest deployable object in Kubernetes.

A Pod can contain:

* One Container (Most Common)
* Multiple Containers (Advanced Use Cases)

Containers inside the same Pod:

* Share the same Network Namespace
* Share the same IP Address
* Share Storage Volumes
* Communicate using `localhost`

Think of a Pod as a **logical host** for one or more closely related containers.

---

# 🎯 Why Do We Need Pods?

Kubernetes does **not** manage containers directly.

Instead, it manages **Pods**, which provide:

* Container lifecycle management
* Shared networking
* Shared storage
* Health monitoring
* Scheduling
* Restart policies

This abstraction makes applications easier to deploy and manage.

---

# 🏗️ Pod Architecture

```text
                  Worker Node
                       │
        ┌────────────────────────────┐
        │            Pod             │
        │                            │
        │  ┌──────────────────────┐  │
        │  │     Container        │  │
        │  └──────────────────────┘  │
        │                            │
        │ Shared Network & Storage   │
        └────────────────────────────┘
```

A Pod is deployed on a Worker Node and contains one or more containers that share networking and storage resources.

---

# 🔄 Pod Lifecycle

Every Pod goes through several phases during its lifetime.

```text
Pending
   │
   ▼
Container Creating
   │
   ▼
Running
   │
   ▼
Succeeded / Failed
```

### Pending

The Pod has been accepted by Kubernetes but is waiting to be scheduled or for images to be downloaded.

---

### Running

The Pod has been successfully scheduled and at least one container is running.

---

### Succeeded

All containers completed successfully and exited normally.

---

### Failed

One or more containers terminated unexpectedly and could not recover.

---

# 📦 Single-Container vs Multi-Container Pods

## Single-Container Pod

The most common deployment model.

```text
Pod
 └── Nginx Container
```

Suitable for:

* Web Servers
* APIs
* Microservices

---

## Multi-Container Pod

Multiple containers work together inside the same Pod.

```text
Pod
├── Application Container
└── Logging Sidecar Container
```

Common use cases:

* Sidecar Pattern
* Log Collection
* Monitoring Agents
* Service Mesh Proxies

---

# 🚀 Creating a Pod

## Create a Pod Imperatively

```bash
kubectl run nginx \
  --image=nginx \
  --restart=Never
```

---

## Verify the Pod

```bash
kubectl get pods
```

Example output:

```text
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          20s
```

---

## Describe the Pod

```bash
kubectl describe pod nginx
```

Displays:

* Events
* IP Address
* Node
* Image
* Resource Information

---

## Pod YAML Example

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Create it using:

```bash
kubectl apply -f pod.yaml
```

---

# ⚙️ Managing Pods

Delete a Pod:

```bash
kubectl delete pod nginx
```

View detailed information:

```bash
kubectl get pod nginx -o wide
```

Execute commands inside a Pod:

```bash
kubectl exec -it nginx -- bash
```

View logs:

```bash
kubectl logs nginx
```

Watch Pod status:

```bash
kubectl get pods -w
```

---

# ☁️ DevOps Perspective

In production environments, DevOps engineers rarely create standalone Pods manually.

Instead, Pods are typically managed by higher-level Kubernetes objects such as:

* Deployments
* ReplicaSets
* StatefulSets
* DaemonSets
* Jobs

These controllers ensure Pods are recreated automatically if they fail and support rolling updates and scaling.

---

# 🏭 Production Example

An e-commerce application is deployed using a Deployment with three replicas.

```text
                Deployment
                     │
     ┌───────────────┼───────────────┐
     ▼               ▼               ▼
   Pod 1           Pod 2           Pod 3
     │               │               │
     ▼               ▼               ▼
 Nginx App       Nginx App       Nginx App
```

If **Pod 2** crashes, Kubernetes automatically creates a replacement Pod to maintain the desired number of running instances.

---

# 🎯 Common Interview Questions

### What is a Pod?

A Pod is the smallest deployable unit in Kubernetes that encapsulates one or more containers.

---

### Can a Pod contain multiple containers?

Yes. Multiple containers can run inside the same Pod and share networking and storage resources.

---

### Do containers inside a Pod have different IP addresses?

No. All containers in the same Pod share the same IP address and can communicate using `localhost`.

---

### Why doesn't Kubernetes manage containers directly?

Pods provide an abstraction layer that enables shared networking, storage, lifecycle management, health checks, and scheduling.

---

### Are Pods permanent?

No. Pods are ephemeral. If a Pod is deleted or fails, controllers such as Deployments or ReplicaSets create replacement Pods.

---

# 🔍 Useful Commands

```bash
kubectl get pods

kubectl get pods -o wide

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl exec -it <pod-name> -- bash

kubectl delete pod <pod-name>

kubectl apply -f pod.yaml

kubectl get pods -w
```

---

# 📑 Interview Cheat Sheet

```text
Deployment
      │
      ▼
 ReplicaSet
      │
      ▼
     Pod
      │
      ▼
 Container(s)
```

Remember:

* **Pod = Smallest Deployable Unit**
* A Pod contains one or more containers.
* Containers inside a Pod share networking and storage.
* Every Pod gets a unique IP address.
* Pods are temporary and are usually managed by controllers like Deployments.

---

# 📚 Summary

Pods are the fundamental execution unit in Kubernetes. They provide a consistent environment for one or more containers by sharing networking, storage, and lifecycle management. While standalone Pods are useful for learning and testing, production workloads are almost always managed through controllers such as Deployments or StatefulSets to ensure availability, scalability, and self-healing.

---

# 🔗 Related Topics

⬅️ **Previous:** Cluster Setup → `../03-Cluster-Setup/README.md`

➡️ **Next:** ReplicaSets → `../05-ReplicaSets/README.md`

### 📖 Recommended Reading

* Kubernetes ReplicaSets
* Kubernetes Deployments
* Kubernetes Services
* Kubernetes Official Documentation
* Kubernetes Best Practices
