# 🚀 Kubernetes Deployments

> **A Deployment is a Kubernetes controller that manages the lifecycle of applications by creating and managing ReplicaSets and Pods.**
>
> Deployments provide declarative updates, rolling updates, rollbacks, scaling, and self-healing, making them the preferred way to deploy stateless applications in production.

---

# 📖 Table of Contents

* What is a Deployment?
* Why Do We Need Deployments?
* Deployment Architecture
* How Deployments Work
* Creating a Deployment
* Scaling Deployments
* Rolling Updates
* Rollbacks
* Deployment Strategies
* Deployment vs ReplicaSet
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Deployment?

A **Deployment** is a higher-level Kubernetes object that manages ReplicaSets, which in turn manage Pods.

Instead of creating Pods directly, you create a Deployment and specify:

* Container Image
* Number of Replicas
* Labels
* Resource Configuration
* Update Strategy

Kubernetes ensures that the desired number of Pods are always running and automatically replaces failed Pods.

---

# 🎯 Why Do We Need Deployments?

Managing Pods manually is difficult because:

* Pods can fail
* Updates require recreation
* Scaling is manual
* Rollbacks are complex

Deployments solve these problems by providing:

* Self-Healing
* Horizontal Scaling
* Rolling Updates
* Rollbacks
* Declarative Configuration
* High Availability

---

# 🏗️ Deployment Architecture

```text
                 Deployment
                      │
                      ▼
                 ReplicaSet
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
      Pod 1         Pod 2         Pod 3
```

Relationship:

```text
Deployment
      │
      ▼
ReplicaSet
      │
      ▼
Pods
      │
      ▼
Containers
```

---

# ⚙️ How Deployments Work

When a Deployment is created:

1. Deployment creates a ReplicaSet.
2. ReplicaSet creates the required Pods.
3. Scheduler places Pods on Worker Nodes.
4. kubelet starts the containers.
5. Deployment continuously monitors the desired state.

Flow:

```text
Developer
     │
kubectl apply
     │
     ▼
Deployment
     │
     ▼
ReplicaSet
     │
     ▼
Pods
     │
     ▼
Running Application
```

---

# 🚀 Creating a Deployment

## Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:
    metadata:
      labels:
        app: nginx

    spec:
      containers:
      - name: nginx
        image: nginx:latest

        ports:
        - containerPort: 80
```

Create the Deployment:

```bash
kubectl apply -f deployment.yaml
```

---

# 🔍 Verify Deployment

List Deployments:

```bash
kubectl get deployments
```

Example:

```text
NAME               READY   UP-TO-DATE   AVAILABLE
nginx-deployment   3/3     3            3
```

View ReplicaSets:

```bash
kubectl get rs
```

View Pods:

```bash
kubectl get pods
```

Describe Deployment:

```bash
kubectl describe deployment nginx-deployment
```

---

# 📈 Scaling Deployments

Increase replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Result:

```text
Deployment
      │
      ▼
ReplicaSet
      │
Creates 2 More Pods
```

Reduce replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=2
```

Deployment updates the ReplicaSet, which adjusts the number of Pods automatically.

---

# 🔄 Rolling Updates

One of the biggest advantages of Deployments is **zero-downtime updates**.

Suppose the application image changes:

```text
Old Image
nginx:1.24

        │

        ▼

New Image
nginx:1.25
```

Update the Deployment:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25
```

Deployment process:

```text
Old Pods Running
        │
        ▼
Create New Pod
        │
        ▼
Health Check
        │
        ▼
Delete Old Pod
        │
        ▼
Repeat Until Complete
```

Users continue accessing the application during the update.

---

# ⏪ Rollbacks

If the new version has issues, Kubernetes can restore the previous version.

View rollout history:

```bash
kubectl rollout history deployment nginx-deployment
```

Rollback:

```bash
kubectl rollout undo deployment nginx-deployment
```

Check rollout status:

```bash
kubectl rollout status deployment nginx-deployment
```

---

# 🎯 Deployment Strategies

## 1️⃣ Rolling Update (Default)

* Zero downtime
* Gradual replacement
* Most commonly used

---

## 2️⃣ Recreate

```text
Old Pods Deleted
        │
        ▼
New Pods Created
```

Characteristics:

* Temporary downtime
* Simpler strategy
* Suitable for applications that cannot run multiple versions simultaneously

---

# ⚖️ Deployment vs ReplicaSet

| Deployment                 | ReplicaSet              |
| -------------------------- | ----------------------- |
| Manages ReplicaSets        | Manages Pods            |
| Supports rolling updates   | No rolling updates      |
| Supports rollback          | No rollback             |
| Declarative updates        | Basic Pod management    |
| Recommended for production | Rarely created directly |

---

# ☁️ DevOps Perspective

In production environments, DevOps engineers almost always deploy applications using **Deployments**.

Typical CI/CD workflow:

```text
Developer
     │
     ▼
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
kubectl apply
     │
     ▼
Deployment
     │
     ▼
ReplicaSet
     │
     ▼
Pods
```

Deployments provide reliable application updates while maintaining service availability.

---

# 🏭 Production Example

An e-commerce company runs an application with **5 replicas**.

Current version:

```text
v1.0

Pod
Pod
Pod
Pod
Pod
```

A new version (**v2.0**) is released.

Deployment performs a rolling update:

```text
Old Pod → New Pod

Old Pod → New Pod

Old Pod → New Pod

Old Pod → New Pod

Old Pod → New Pod
```

Users continue using the application without interruption.

If **v2.0** fails health checks, Kubernetes rolls back to **v1.0** automatically or on command.

---

# 🎯 Common Interview Questions

### What is a Deployment?

A Deployment is a Kubernetes controller that manages ReplicaSets and Pods while providing rolling updates, scaling, self-healing, and rollback capabilities.

---

### Why do we use Deployments instead of ReplicaSets?

Deployments provide additional features such as rolling updates, rollbacks, and declarative application management, making them suitable for production workloads.

---

### What is a Rolling Update?

A Rolling Update gradually replaces old Pods with new Pods without causing application downtime.

---

### Can a Deployment rollback to a previous version?

Yes. Deployments maintain revision history and support rolling back to earlier versions using rollout commands.

---

### What object does a Deployment create?

A Deployment creates and manages a ReplicaSet, which in turn manages Pods.

---

# 🔍 Useful Commands

```bash
kubectl get deployments

kubectl describe deployment <deployment-name>

kubectl get rs

kubectl get pods

kubectl apply -f deployment.yaml

kubectl scale deployment <deployment-name> --replicas=5

kubectl set image deployment/<deployment-name> <container-name>=<image>

kubectl rollout status deployment <deployment-name>

kubectl rollout history deployment <deployment-name>

kubectl rollout undo deployment <deployment-name>

kubectl delete deployment <deployment-name>
```

---

# 📑 Interview Cheat Sheet

```text
Developer
      │
      ▼
Deployment
      │
      ▼
ReplicaSet
      │
      ▼
Pods
      │
      ▼
Containers
```

Remember:

* **Deployment is the recommended way to deploy stateless applications.**
* **Deployment manages ReplicaSets.**
* **ReplicaSets manage Pods.**
* **Deployments support rolling updates and rollbacks.**
* **Scaling a Deployment automatically scales its Pods.**

---

# 📚 Summary

Deployments are the standard way to manage stateless applications in Kubernetes. They simplify application lifecycle management by automating Pod creation, scaling, rolling updates, and rollbacks through ReplicaSets.

For DevOps Engineers, Deployments are one of the most frequently used Kubernetes resources because they enable safe, reliable, and repeatable application releases with minimal downtime.

---

# 🔗 Related Topics

⬅️ **Previous:** ReplicaSets → `../05-ReplicaSets/README.md`

➡️ **Next:** Namespaces → `../07-Namespaces/README.md`

### 📖 Recommended Reading

* Kubernetes ReplicaSets
* Kubernetes Services
* Kubernetes Rolling Updates
* Kubernetes Official Documentation
* Kubernetes Best Practices
