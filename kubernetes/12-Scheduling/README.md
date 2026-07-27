# 📅 Kubernetes Scheduling

> **Kubernetes Scheduling is the process of assigning Pods to the most suitable Worker Node in a cluster based on resource availability, scheduling rules, constraints, and policies.**
>
> The **Kubernetes Scheduler** ensures that workloads are distributed efficiently while maintaining high availability, performance, and resource utilization.

---

# 📖 Table of Contents

* What is Scheduling?
* Why Do We Need Scheduling?
* How the Scheduler Works
* Scheduling Architecture
* Scheduling Factors
* Node Selectors
* Node Affinity
* Taints & Tolerations
* Pod Affinity & Anti-Affinity
* Resource Requests & Limits
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Kubernetes Scheduling?

The **Kubernetes Scheduler** is a Control Plane component responsible for assigning newly created Pods to Worker Nodes.

When a Pod is created:

* It has **no assigned node**.
* The Scheduler evaluates all available Worker Nodes.
* It selects the most suitable node.
* The Pod is scheduled to that node.

The Scheduler aims to place Pods where they can run efficiently while satisfying all scheduling requirements.

---

# 🎯 Why Do We Need Scheduling?

Imagine a cluster with three Worker Nodes.

```text
Node 1
CPU: 95%

Node 2
CPU: 40%

Node 3
CPU: 10%
```

If Kubernetes randomly placed Pods, Node 1 could become overloaded while Node 3 remained mostly idle.

The Scheduler balances workloads by considering:

* CPU availability
* Memory availability
* Scheduling rules
* Labels
* Affinity rules
* Taints and tolerations
* Resource requests

---

# 🏗️ Scheduling Architecture

```text
                 User
                   │
                   ▼
             Deployment
                   │
                   ▼
             Kubernetes API
                   │
                   ▼
             Scheduler
                   │
      ┌────────────┼────────────┐
      ▼            ▼            ▼
   Worker 1     Worker 2     Worker 3
      │            │            │
     Pod          Pod          Pod
```

The Scheduler continuously watches for Pods that have not yet been assigned to a node.

---

# ⚙️ How the Scheduler Works

Scheduling occurs in two phases.

### 1️⃣ Filtering

The Scheduler removes nodes that cannot run the Pod.

Examples:

* Insufficient CPU
* Insufficient Memory
* Node unavailable
* Label mismatch
* Untolerated taints

---

### 2️⃣ Scoring

The remaining nodes are scored.

The node with the highest score is selected.

Example:

```text
Node 1 → Score: 65

Node 2 → Score: 92

Node 3 → Score: 81
```

Result:

```text
Pod Scheduled → Node 2
```

---

# 📌 Scheduling Factors

The Scheduler considers multiple factors before assigning a Pod.

* CPU Requests
* Memory Requests
* Node Labels
* Node Affinity
* Pod Affinity
* Pod Anti-Affinity
* Taints
* Tolerations
* Node Health
* Existing Workloads

---

# 🏷️ Node Selectors

A **Node Selector** schedules Pods only onto nodes with matching labels.

Example node label:

```bash
kubectl label node worker-1 environment=production
```

Pod YAML:

```yaml
spec:
  nodeSelector:
    environment: production
```

The Pod will only run on nodes with the label:

```text
environment=production
```

---

# ❤️ Node Affinity

Node Affinity is a more flexible version of Node Selector.

It supports:

* Required Rules
* Preferred Rules
* Multiple Conditions

Example:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
```

Use Node Affinity when scheduling requirements are more complex than simple label matching.

---

# 🚫 Taints & Tolerations

**Taints** prevent Pods from being scheduled onto specific nodes.

Example:

```bash
kubectl taint nodes worker-1 dedicated=database:NoSchedule
```

Result:

```text
worker-1

❌ No Pods Allowed
```

Unless the Pod has a matching **Toleration**.

Pod Example:

```yaml
tolerations:
- key: dedicated
  operator: Equal
  value: database
  effect: NoSchedule
```

Now the Pod is allowed to run on the tainted node.

---

# 🤝 Pod Affinity & Anti-Affinity

### Pod Affinity

Schedules Pods close together.

Example:

```text
Frontend Pod

↓

Backend Pod

Same Worker Node
```

Useful for reducing network latency.

---

### Pod Anti-Affinity

Keeps Pods separated.

Example:

```text
Worker 1

Pod A
```

```text
Worker 2

Pod B
```

This improves fault tolerance because replicas are spread across different nodes.

---

# 📊 Resource Requests & Limits

Pods specify the resources they require.

Example:

```yaml
resources:
  requests:
    cpu: "500m"
    memory: "512Mi"

  limits:
    cpu: "1"
    memory: "1Gi"
```

Scheduler uses **requests** to determine placement.

Limits prevent containers from consuming excessive resources after they are running.

---

# ☁️ DevOps Perspective

Production clusters typically combine several scheduling features.

Example:

```text
Deployment
      │
      ▼
Scheduler
      │
 ┌────┼──────────────┐
 ▼    ▼              ▼
Node Selector

Node Affinity

Taints

Resource Requests
```

Common production scenarios:

* GPU workloads
* Database nodes
* Monitoring nodes
* Logging nodes
* AI/ML workloads

Each workload can be directed to appropriate nodes using scheduling policies.

---

# 🏭 Production Example

A company has three Worker Nodes.

```text
Worker 1
GPU Enabled
```

```text
Worker 2
Database
```

```text
Worker 3
General Applications
```

Scheduling policy:

```text
AI Application
      │
      ▼
GPU Node

Database
      │
      ▼
Database Node

Web Application
      │
      ▼
General Worker Node
```

This ensures each workload runs on the most suitable infrastructure.

---

# 🎯 Common Interview Questions

### What is the Kubernetes Scheduler?

The Scheduler is a Control Plane component that assigns Pods to suitable Worker Nodes.

---

### What factors does the Scheduler consider?

* CPU
* Memory
* Labels
* Node Affinity
* Pod Affinity
* Taints
* Tolerations
* Resource Requests

---

### What is the difference between Node Selector and Node Affinity?

* **Node Selector** uses simple label matching.
* **Node Affinity** supports advanced scheduling rules and preferences.

---

### What are Taints and Tolerations?

Taints prevent Pods from being scheduled onto nodes.

Tolerations allow specific Pods to run on tainted nodes.

---

### What is Pod Anti-Affinity?

Pod Anti-Affinity spreads Pods across different nodes to improve availability and fault tolerance.

---

# 🔍 Useful Commands

```bash
kubectl get nodes

kubectl describe node <node-name>

kubectl label node worker-1 environment=production

kubectl taint nodes worker-1 dedicated=db:NoSchedule

kubectl get pods -o wide

kubectl describe pod <pod-name>

kubectl top nodes

kubectl top pods
```

---

# 📑 Interview Cheat Sheet

```text
Deployment
      │
      ▼
Scheduler
      │
      ▼
Select Best Worker Node
      │
      ▼
Pod Running
```

Remember:

* **Scheduler assigns Pods to Worker Nodes.**
* **Node Selector provides simple label-based scheduling.**
* **Node Affinity provides advanced scheduling rules.**
* **Taints repel Pods.**
* **Tolerations allow Pods onto tainted nodes.**
* **Pod Anti-Affinity spreads replicas across nodes.**
* **Resource Requests influence scheduling decisions.**

---

# 📚 Summary

Kubernetes Scheduling ensures that Pods are placed on the most appropriate Worker Nodes based on available resources and scheduling policies. By using features such as Node Selectors, Affinity rules, Taints, Tolerations, and Resource Requests, Kubernetes optimizes workload distribution, improves reliability, and enhances cluster utilization.

For DevOps Engineers, understanding scheduling is critical for designing efficient production clusters, isolating specialized workloads, and ensuring high availability across infrastructure.

---

# 🔗 Related Topics

⬅️ **Previous:** Ingress → `../11-Ingress/README.md`

➡️ **Next:** StatefulSets & DaemonSets → `../13-StatefulSets-and-DaemonSets/README.md`

### 📖 Recommended Reading

* Kubernetes StatefulSets
* Kubernetes DaemonSets
* Kubernetes Resource Management
* Kubernetes Official Documentation
* Kubernetes Scheduling Best Practices
