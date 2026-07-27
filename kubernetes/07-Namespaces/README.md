# 🏷️ Kubernetes Namespaces

> **A Namespace is a logical partition within a Kubernetes cluster that allows multiple teams, projects, or environments to share the same cluster while remaining isolated from one another.**
>
> Namespaces help organize resources, prevent naming conflicts, and enable resource management and access control in large Kubernetes environments.

---

# 📖 Table of Contents

* What is a Namespace?
* Why Do We Need Namespaces?
* Default Kubernetes Namespaces
* Namespace Architecture
* Creating a Namespace
* Working with Namespaces
* Resource Isolation
* Namespace vs Cluster
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Namespace?

A **Namespace** is a virtual cluster inside a Kubernetes cluster.

It provides logical separation between resources such as:

* Pods
* Deployments
* Services
* ConfigMaps
* Secrets
* Jobs
* ReplicaSets

Namespaces help organize applications without creating separate Kubernetes clusters.

---

# 🎯 Why Do We Need Namespaces?

Imagine multiple teams sharing one Kubernetes cluster.

Without Namespaces:

* Resource names may conflict.
* Teams can accidentally modify each other's resources.
* Managing permissions becomes difficult.
* Resource usage is hard to control.

Namespaces solve these problems by providing logical isolation.

---

# 🏗️ Namespace Architecture

```text
                 Kubernetes Cluster
                        │
     ┌──────────────────┼──────────────────┐
     ▼                  ▼                  ▼
 Development        Testing          Production
 Namespace          Namespace         Namespace
     │                  │                  │
 ┌───┼────┐         ┌────┼────┐        ┌────┼────┐
 ▼   ▼    ▼         ▼    ▼    ▼        ▼    ▼    ▼
Pods Services   Pods Services     Pods Services
Deployments     Deployments       Deployments
```

Each Namespace has its own set of Kubernetes resources while sharing the same underlying cluster.

---

# 🌍 Default Kubernetes Namespaces

Every Kubernetes cluster comes with built-in Namespaces.

## 1️⃣ default

The default Namespace for user-created resources if no Namespace is specified.

---

## 2️⃣ kube-system

Contains Kubernetes system components such as:

* CoreDNS
* kube-proxy
* API Server components
* Scheduler

---

## 3️⃣ kube-public

Accessible by all users.

Stores publicly readable cluster information.

---

## 4️⃣ kube-node-lease

Stores lease information for Worker Nodes.

Used by Kubernetes to detect node health efficiently.

---

# 🚀 Creating a Namespace

Create a Namespace:

```bash
kubectl create namespace development
```

Verify:

```bash
kubectl get namespaces
```

Example output:

```text
NAME              STATUS   AGE
default           Active   12d
development       Active   5s
kube-system       Active   12d
```

---

# 📄 Namespace YAML

```yaml
apiVersion: v1
kind: Namespace

metadata:
  name: development
```

Create it:

```bash
kubectl apply -f namespace.yaml
```

---

# ⚙️ Working with Namespaces

Deploy resources into a Namespace:

```bash
kubectl apply -f deployment.yaml -n development
```

List Pods in a Namespace:

```bash
kubectl get pods -n development
```

List Services:

```bash
kubectl get services -n development
```

Describe a Namespace:

```bash
kubectl describe namespace development
```

Delete a Namespace:

```bash
kubectl delete namespace development
```

Deleting a Namespace removes all resources inside it.

---

# 🔒 Resource Isolation

Namespaces isolate Kubernetes resources.

Example:

```text
Development Namespace

Deployment
Service
Pods
ConfigMaps
Secrets
```

```text
Production Namespace

Deployment
Service
Pods
ConfigMaps
Secrets
```

Although resource names can be identical, they remain isolated because they exist in different Namespaces.

For example:

```text
development/nginx

production/nginx
```

Both resources can coexist without conflict.

---

# ⚖️ Namespace vs Cluster

| Namespace               | Cluster                                     |
| ----------------------- | ------------------------------------------- |
| Logical isolation       | Physical/virtual infrastructure             |
| Shares Worker Nodes     | Own Worker Nodes                            |
| Low cost                | Higher cost                                 |
| Fast to create          | Requires provisioning                       |
| Common for environments | Used for complete infrastructure separation |

---

# ☁️ DevOps Perspective

A common production setup uses separate Namespaces for different environments.

```text
Kubernetes Cluster
        │
        ├───────────────► dev
        │
        ├───────────────► test
        │
        ├───────────────► staging
        │
        └───────────────► production
```

Benefits:

* Environment isolation
* Easier access control (RBAC)
* Resource quotas
* Team separation
* Simplified management

---

# 🏭 Production Example

A company has three environments.

```text
Kubernetes Cluster
        │
 ┌──────┼─────────────┐
 ▼      ▼             ▼
Dev   Staging    Production
 │        │             │
Pods    Pods          Pods
Deploy  Deploy        Deploy
Svc     Svc           Svc
```

Developers deploy new features into the **development** Namespace.

After testing, the application is promoted to **staging** and then **production**, while all environments remain isolated within the same cluster.

---

# 🎯 Common Interview Questions

### What is a Namespace?

A Namespace is a logical partition within a Kubernetes cluster that isolates resources.

---

### Why do we use Namespaces?

Namespaces organize resources, prevent naming conflicts, and enable environment and team isolation.

---

### What are the default Namespaces?

* default
* kube-system
* kube-public
* kube-node-lease

---

### Can two Pods have the same name?

Yes, if they exist in different Namespaces.

Example:

```text
dev/nginx

prod/nginx
```

---

### Does a Namespace create a new Kubernetes cluster?

No.

Namespaces provide logical isolation within the same Kubernetes cluster.

---

# 🔍 Useful Commands

```bash
kubectl get namespaces

kubectl create namespace development

kubectl delete namespace development

kubectl describe namespace development

kubectl get pods -n development

kubectl get deployments -n development

kubectl get services -n development

kubectl apply -f deployment.yaml -n development
```

---

# 📑 Interview Cheat Sheet

```text
Kubernetes Cluster
        │
 ┌──────┼──────────────┐
 ▼      ▼              ▼
 Dev   Test       Production
  │      │              │
Pods   Pods          Pods
Svc    Svc           Svc
```

Remember:

* **Namespace = Logical Isolation**
* **Cluster = Physical Infrastructure**
* **Same resource names are allowed in different Namespaces**
* **Namespaces are commonly used for Dev, Test, Staging, and Production**
* **RBAC and Resource Quotas are often applied at the Namespace level**

---

# 📚 Summary

Namespaces provide a simple and efficient way to organize and isolate Kubernetes resources within a single cluster. They enable multiple teams and environments to share the same infrastructure while avoiding naming conflicts and simplifying access control.

For DevOps Engineers, Namespaces are a foundational concept used in nearly every production Kubernetes cluster to separate environments, manage permissions, and allocate resources effectively.

---

# 🔗 Related Topics

⬅️ **Previous:** Deployments → `../06-Deployments/README.md`

➡️ **Next:** Services → `../08-Services/README.md`

### 📖 Recommended Reading

* Kubernetes Services
* Kubernetes RBAC
* Kubernetes Resource Quotas
* Kubernetes Official Documentation
* Kubernetes Best Practices
