# 🗄️ Kubernetes StatefulSets & DaemonSets

> **StatefulSets and DaemonSets are specialized Kubernetes workload controllers designed for applications with unique deployment requirements.**
>
> **StatefulSets** manage stateful applications that require stable identities and persistent storage, while **DaemonSets** ensure that a copy of a Pod runs on every (or selected) Worker Node in the cluster.

---

# 📖 Table of Contents

* What are StatefulSets?
* What are DaemonSets?
* Why Do We Need Them?
* StatefulSet vs Deployment
* DaemonSet vs Deployment
* StatefulSet Architecture
* DaemonSet Architecture
* Creating StatefulSets
* Creating DaemonSets
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a StatefulSet?

A **StatefulSet** is a Kubernetes controller used to manage **stateful applications**.

Unlike Deployments, StatefulSets provide:

* Stable Pod Names
* Persistent Storage
* Ordered Deployment
* Ordered Scaling
* Ordered Termination
* Stable Network Identity

Each Pod has a unique identity that is maintained even after rescheduling.

---

# 🎯 Why Do We Need StatefulSets?

Some applications cannot use randomly created Pods.

Examples:

* MySQL
* PostgreSQL
* MongoDB
* Cassandra
* Kafka
* Elasticsearch
* ZooKeeper

These applications require:

* Persistent storage
* Stable hostnames
* Predictable Pod names
* Ordered startup and shutdown

Deployments cannot guarantee these requirements.

---

# ❓ What is a DaemonSet?

A **DaemonSet** ensures that a copy of a Pod runs on **every Worker Node** (or selected nodes) in the cluster.

When:

* A new Worker Node joins → Kubernetes creates the Pod automatically.
* A Worker Node is removed → Kubernetes removes the Pod automatically.

DaemonSets are ideal for node-level services.

---

# 🎯 Why Do We Need DaemonSets?

Some services must run on every node.

Examples:

* Log Collection
* Monitoring Agents
* Security Agents
* Networking Plugins
* Storage Plugins

Instead of manually deploying Pods to each node, Kubernetes automatically manages them through a DaemonSet.

---

# 🏗️ StatefulSet Architecture

```text
                StatefulSet
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
     mysql-0      mysql-1      mysql-2
        │            │            │
        ▼            ▼            ▼
      PVC-0        PVC-1        PVC-2
        │            │            │
        ▼            ▼            ▼
 Persistent      Persistent    Persistent
   Volume          Volume        Volume
```

Each Pod receives:

* Unique Name
* Dedicated Persistent Volume
* Stable DNS Name

Example:

```text
mysql-0
mysql-1
mysql-2
```

---

# 🏗️ DaemonSet Architecture

```text
                 DaemonSet
                      │
      ┌───────────────┼───────────────┐
      ▼               ▼               ▼
 Worker-1         Worker-2        Worker-3
      │               │               │
      ▼               ▼               ▼
 Log Agent       Log Agent      Log Agent
```

Each Worker Node runs exactly one Pod managed by the DaemonSet.

---

# ⚖️ StatefulSet vs Deployment

| StatefulSet           | Deployment             |
| --------------------- | ---------------------- |
| Stateful applications | Stateless applications |
| Stable Pod names      | Random Pod names       |
| Persistent storage    | Optional storage       |
| Ordered updates       | Parallel updates       |
| Stable identities     | Dynamic identities     |
| Databases             | Web applications       |

---

# ⚖️ DaemonSet vs Deployment

| DaemonSet                      | Deployment                                     |
| ------------------------------ | ---------------------------------------------- |
| One Pod per node               | User-defined replicas                          |
| Runs on every node             | Runs on selected nodes                         |
| Node services                  | Application services                           |
| Logging & Monitoring           | Web Apps & APIs                                |
| Automatically covers new nodes | Does not automatically create one Pod per node |

---

# 🚀 Creating a StatefulSet

Example YAML:

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: mysql

spec:
  serviceName: mysql

  replicas: 3

  selector:
    matchLabels:
      app: mysql

  template:
    metadata:
      labels:
        app: mysql

    spec:
      containers:
      - name: mysql
        image: mysql:8
```

Create it:

```bash
kubectl apply -f statefulset.yaml
```

---

# 🚀 Creating a DaemonSet

Example YAML:

```yaml
apiVersion: apps/v1
kind: DaemonSet

metadata:
  name: fluentd

spec:
  selector:
    matchLabels:
      app: fluentd

  template:
    metadata:
      labels:
        app: fluentd

    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd
```

Create it:

```bash
kubectl apply -f daemonset.yaml
```

---

# ☁️ DevOps Perspective

Typical production architecture:

```text
Internet
     │
     ▼
Ingress
     │
     ▼
Deployment
(Web Applications)
     │
     ▼
Pods

----------------------------

Database
     │
     ▼
StatefulSet
     │
     ▼
Persistent Volumes

----------------------------

Worker Nodes
     │
     ▼
DaemonSet
(Log Agents, Monitoring)
```

A production Kubernetes cluster commonly uses all three workload controllers:

* **Deployments** for stateless applications
* **StatefulSets** for databases and stateful workloads
* **DaemonSets** for node-level infrastructure services

---

# 🏭 Production Example

An online shopping platform runs the following workloads:

```text
Frontend
      │
      ▼
Deployment
```

```text
MySQL Database
      │
      ▼
StatefulSet
      │
      ▼
Persistent Volume
```

```text
Prometheus Node Exporter
      │
      ▼
DaemonSet
```

Traffic flow:

```text
Internet
     │
     ▼
Ingress
     │
     ▼
Frontend Deployment
     │
     ▼
MySQL StatefulSet
     │
     ▼
Persistent Storage

Worker Nodes
     │
     ▼
DaemonSet
(Node Exporter / Fluentd)
```

This architecture ensures:

* Web applications scale easily.
* Database data remains persistent.
* Every node continuously reports logs and metrics.

---

# 🎯 Common Interview Questions

### What is a StatefulSet?

A StatefulSet manages stateful applications that require stable identities, persistent storage, and ordered deployment.

---

### When should we use StatefulSets?

Use StatefulSets for applications such as:

* MySQL
* PostgreSQL
* MongoDB
* Cassandra
* Kafka
* Elasticsearch

---

### What is a DaemonSet?

A DaemonSet ensures that one Pod runs on every Worker Node (or selected nodes).

---

### What are common DaemonSet use cases?

* Fluentd
* Prometheus Node Exporter
* Filebeat
* CNI Plugins
* Security Agents

---

### What is the difference between a Deployment and a StatefulSet?

Deployments manage stateless applications, while StatefulSets manage stateful applications with stable identities and persistent storage.

---

# 🔍 Useful Commands

```bash
kubectl get statefulsets

kubectl get daemonsets

kubectl describe statefulset <statefulset-name>

kubectl describe daemonset <daemonset-name>

kubectl apply -f statefulset.yaml

kubectl apply -f daemonset.yaml

kubectl delete statefulset <statefulset-name>

kubectl delete daemonset <daemonset-name>

kubectl get pods -o wide
```

---

# 📑 Interview Cheat Sheet

```text
Deployment
      │
Stateless Apps
(Web/API)

────────────────────────

StatefulSet
      │
Databases
(Persistent Data)

────────────────────────

DaemonSet
      │
Every Worker Node
(Log Agent / Monitoring)
```

Remember:

* **Deployment → Stateless applications**
* **StatefulSet → Databases & Stateful workloads**
* **DaemonSet → One Pod on every Worker Node**
* **StatefulSets provide stable Pod names and persistent storage**
* **DaemonSets automatically run on newly added nodes**
* **Deployments, StatefulSets, and DaemonSets each solve different workload requirements**

---

# 📚 Summary

StatefulSets and DaemonSets address specialized workload requirements that Deployments cannot handle. StatefulSets are designed for applications requiring persistent storage, stable identities, and ordered operations, while DaemonSets ensure that essential infrastructure services run consistently on every Worker Node.

For DevOps Engineers, understanding when to use Deployments, StatefulSets, or DaemonSets is critical for building reliable, scalable, and production-ready Kubernetes environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Scheduling → `../12-Scheduling/README.md`

➡️ **Next:** Jobs & CronJobs → `../14-Jobs-and-CronJobs/README.md`

### 📖 Recommended Reading

* Kubernetes Jobs
* Kubernetes Persistent Storage
* Kubernetes Deployments
* Kubernetes Official Documentation
* Kubernetes Workload Best Practices
