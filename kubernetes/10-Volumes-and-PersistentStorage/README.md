# 💾 Kubernetes Volumes & Persistent Storage

> **Kubernetes Volumes provide storage that can be shared by containers within a Pod, while Persistent Storage ensures that application data survives Pod restarts, rescheduling, and failures.**
>
> Without persistent storage, all data stored inside a container is lost when the container or Pod is deleted. Kubernetes solves this problem using **Volumes**, **Persistent Volumes (PV)**, and **Persistent Volume Claims (PVC)**.

---

# 📖 Table of Contents

* What are Kubernetes Volumes?
* Why Do We Need Persistent Storage?
* Ephemeral vs Persistent Storage
* Kubernetes Storage Architecture
* Types of Volumes
* Persistent Volumes (PV)
* Persistent Volume Claims (PVC)
* Storage Classes
* Creating PV & PVC
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Kubernetes Volumes?

A **Volume** is a storage resource attached to a Pod.

Unlike the container filesystem, a Volume exists for the lifetime of the Pod and can be shared between containers in the same Pod.

Volumes are commonly used to:

* Store application data
* Share files between containers
* Mount configuration files
* Persist logs
* Store database data

---

# 🎯 Why Do We Need Persistent Storage?

Containers are **ephemeral**.

When a Pod is deleted:

* Container filesystem is removed.
* Application data is lost.
* Logs disappear.
* Uploaded files are deleted.

Example:

```text
Container
   │
   ▼
Database Running
   │
   ▼
Pod Deleted
   │
   ▼
❌ Data Lost
```

Persistent storage prevents data loss by storing data outside the Pod lifecycle.

---

# ⚖️ Ephemeral vs Persistent Storage

| Ephemeral Storage  | Persistent Storage     |
| ------------------ | ---------------------- |
| Temporary          | Permanent              |
| Deleted with Pod   | Survives Pod deletion  |
| Suitable for cache | Suitable for databases |
| No recovery        | Data retained          |
| Local to Pod       | Independent of Pod     |

---

# 🏗️ Kubernetes Storage Architecture

```text
                 Application
                      │
                      ▼
                     Pod
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
      Container             Mounted Volume
                                      │
                                      ▼
                         Persistent Volume Claim
                                      │
                                      ▼
                           Persistent Volume
                                      │
                                      ▼
                    AWS EBS / Azure Disk / GCE PD / NFS
```

---

# 📦 Types of Volumes

## 1️⃣ emptyDir

Created when a Pod starts.

Characteristics:

* Exists only while the Pod exists
* Shared by containers in the same Pod
* Deleted when the Pod is removed

Use cases:

* Temporary cache
* Scratch space
* Intermediate processing

---

## 2️⃣ hostPath

Mounts a directory from the Worker Node.

```text
Worker Node
      │
      ▼
/var/log
      │
      ▼
Pod
```

Use cases:

* Local development
* Log collection

Not generally recommended for production because it ties workloads to a specific node.

---

## 3️⃣ Persistent Volume (PV)

A **Persistent Volume** is a storage resource managed by Kubernetes.

Storage can come from:

* AWS EBS
* Azure Disk
* Google Persistent Disk
* NFS
* Ceph
* Local Storage

A PV exists independently of Pods.

---

## 4️⃣ Persistent Volume Claim (PVC)

A **Persistent Volume Claim** is a request for storage made by a Pod.

Instead of requesting a specific disk, the application requests:

* Storage Size
* Access Mode
* Storage Class

Kubernetes binds the claim to a suitable Persistent Volume.

---

# 🔄 PV & PVC Workflow

```text
Application
      │
      ▼
Pod
      │
      ▼
Persistent Volume Claim
      │
      ▼
Persistent Volume
      │
      ▼
Cloud Storage / Disk
```

Pods use PVCs—not PVs directly.

---

# 🚀 Creating a Persistent Volume

```yaml
apiVersion: v1
kind: PersistentVolume

metadata:
  name: pv-demo

spec:
  capacity:
    storage: 2Gi

  accessModes:
    - ReadWriteOnce

  hostPath:
    path: /data
```

Create it:

```bash
kubectl apply -f pv.yaml
```

---

# 🚀 Creating a Persistent Volume Claim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: pvc-demo

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 2Gi
```

Create it:

```bash
kubectl apply -f pvc.yaml
```

---

# 📦 Mounting PVC Inside a Pod

```yaml
volumes:
- name: app-storage
  persistentVolumeClaim:
    claimName: pvc-demo

containers:
- name: nginx
  image: nginx

  volumeMounts:
  - mountPath: /usr/share/nginx/html
    name: app-storage
```

The application now stores data on persistent storage instead of the container filesystem.

---

# 📂 Storage Classes

A **StorageClass** enables **dynamic provisioning**.

Without a StorageClass:

```text
Administrator
      │
Creates PV Manually
```

With a StorageClass:

```text
Application
      │
Requests PVC
      │
      ▼
StorageClass
      │
Automatically Creates PV
```

Benefits:

* Dynamic provisioning
* Less manual work
* Better cloud integration
* Faster deployments

---

# ☁️ DevOps Perspective

Modern Kubernetes environments use dynamic storage provisioning.

Typical cloud mapping:

| Cloud        | Storage            |
| ------------ | ------------------ |
| AWS          | Amazon EBS         |
| Azure        | Azure Managed Disk |
| Google Cloud | Persistent Disk    |

Production applications using persistent storage include:

* MySQL
* PostgreSQL
* MongoDB
* Elasticsearch
* Jenkins
* Prometheus

Stateless applications usually do not require persistent storage.

---

# 🏭 Production Example

A company deploys MySQL on Kubernetes.

Architecture:

```text
Application
      │
      ▼
MySQL Pod
      │
      ▼
Persistent Volume Claim
      │
      ▼
Persistent Volume
      │
      ▼
Amazon EBS Volume
```

If the MySQL Pod crashes:

* Kubernetes creates a new Pod.
* The new Pod reattaches the same Persistent Volume through the PVC.
* Database data remains intact.

---

# 🎯 Common Interview Questions

### What is a Kubernetes Volume?

A Volume is storage attached to a Pod that allows containers to share data and, depending on the type, persist data.

---

### What is the difference between PV and PVC?

* **Persistent Volume (PV):** The actual storage resource.
* **Persistent Volume Claim (PVC):** A request for storage made by an application.

---

### What is a StorageClass?

A StorageClass enables dynamic provisioning of Persistent Volumes based on application requests.

---

### Does data survive Pod deletion?

* **emptyDir:** No
* **Persistent Volume:** Yes

---

### Which applications require Persistent Storage?

Applications that store data, such as databases, logging systems, monitoring tools, and CI/CD servers.

---

# 🔍 Useful Commands

```bash
kubectl get pv

kubectl get pvc

kubectl describe pv <pv-name>

kubectl describe pvc <pvc-name>

kubectl get storageclass

kubectl apply -f pv.yaml

kubectl apply -f pvc.yaml

kubectl delete pvc <pvc-name>

kubectl delete pv <pv-name>
```

---

# 📑 Interview Cheat Sheet

```text
Application
      │
      ▼
Pod
      │
      ▼
PVC
      │
      ▼
PV
      │
      ▼
Cloud Storage
```

Remember:

* **Volumes share data within a Pod.**
* **PV = Actual storage resource.**
* **PVC = Storage request.**
* **StorageClass = Dynamic provisioning.**
* **Databases should always use persistent storage.**
* **Pods use PVCs, not PVs directly.**

---

# 📚 Summary

Kubernetes Volumes and Persistent Storage provide reliable data management for applications running in containers. While Volumes enable containers within a Pod to share storage, Persistent Volumes and Persistent Volume Claims ensure that critical data survives Pod failures, restarts, and rescheduling.

For DevOps Engineers, understanding Kubernetes storage is essential because nearly every stateful application—such as databases, CI/CD tools, monitoring platforms, and logging systems—depends on persistent storage to maintain data integrity and availability.

---

# 🔗 Related Topics

⬅️ **Previous:** ConfigMaps & Secrets → `../09-ConfigMaps-and-Secrets/README.md`

➡️ **Next:** Ingress → `../11-Ingress/README.md`

### 📖 Recommended Reading

* Kubernetes Ingress
* Kubernetes StatefulSets
* Kubernetes Storage Classes
* Kubernetes Official Documentation
* Kubernetes Storage Best Practices
