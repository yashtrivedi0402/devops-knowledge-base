# 🛠️ Kubernetes Troubleshooting

> **Kubernetes Troubleshooting is the systematic process of identifying, diagnosing, and resolving issues affecting applications, Pods, nodes, networking, storage, and cluster components.**
>
> A successful DevOps Engineer spends a significant amount of time troubleshooting production environments. Understanding **where to look, what commands to use, and how Kubernetes components interact** is one of the most valuable production skills.

---

# 📖 Table of Contents

* What is Kubernetes Troubleshooting?
* Why is Troubleshooting Important?
* Kubernetes Troubleshooting Flow
* Common Production Issues
* Troubleshooting Pods
* Troubleshooting Nodes
* Troubleshooting Deployments
* Troubleshooting Networking
* Troubleshooting Storage
* Troubleshooting Control Plane
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Kubernetes Troubleshooting?

Kubernetes troubleshooting is the process of finding the **root cause** of issues within a cluster and restoring applications to a healthy state.

Typical issues include:

* Pods not starting
* CrashLoopBackOff
* ImagePullBackOff
* Services not reachable
* DNS failures
* PVC not binding
* Node failures
* Scheduling failures
* Ingress issues

The goal is not just to restart Pods—it is to identify **why** the problem occurred.

---

# 🎯 Why is Troubleshooting Important?

In production environments, applications must remain highly available.

A single issue can impact thousands of users.

Example:

```text
User
 │
 ▼
Website Down ❌
 │
 ▼
Business Impact
```

An effective troubleshooting process reduces:

* Downtime
* Revenue loss
* Customer impact
* Recovery time (MTTR)

---

# 🔄 Kubernetes Troubleshooting Flow

Whenever an issue occurs, follow a structured approach.

```text
Application Issue
        │
        ▼
Check Pod Status
        │
        ▼
Check Events
        │
        ▼
Check Logs
        │
        ▼
Check Describe Output
        │
        ▼
Check Node
        │
        ▼
Check Networking
        │
        ▼
Check Storage
        │
        ▼
Resolve Root Cause
```

Avoid making random changes before identifying the actual problem.

---

# 🚨 Common Production Issues

| Issue               | Possible Cause                                              |
| ------------------- | ----------------------------------------------------------- |
| CrashLoopBackOff    | Application crash or incorrect startup command              |
| ImagePullBackOff    | Invalid image name or registry authentication issue         |
| Pending Pod         | Insufficient resources, PVC issue, or scheduler constraints |
| ErrImagePull        | Image not found or registry unavailable                     |
| OOMKilled           | Container exceeded memory limit                             |
| Node NotReady       | Node failure or kubelet issue                               |
| Service Unreachable | Service selector or networking problem                      |
| PVC Pending         | Storage class or Persistent Volume issue                    |

---

# 📦 Troubleshooting Pods

Start with checking Pod status.

```bash
kubectl get pods
```

View detailed information:

```bash
kubectl describe pod <pod-name>
```

Check logs:

```bash
kubectl logs <pod-name>
```

If multiple containers exist:

```bash
kubectl logs <pod-name> -c <container-name>
```

For previously crashed containers:

```bash
kubectl logs <pod-name> --previous
```

---

# 🖥️ Troubleshooting Nodes

Check node health:

```bash
kubectl get nodes
```

Describe the node:

```bash
kubectl describe node <node-name>
```

Common node issues:

* Disk pressure
* Memory pressure
* CPU pressure
* Kubelet stopped
* Network unavailable

Example:

```text
Node

Status: NotReady ❌

Reason:
Kubelet stopped
```

---

# 🚀 Troubleshooting Deployments

Check Deployment status:

```bash
kubectl get deployments
```

Describe Deployment:

```bash
kubectl describe deployment <deployment-name>
```

Check ReplicaSets:

```bash
kubectl get rs
```

Verify rollout status:

```bash
kubectl rollout status deployment <deployment-name>
```

View rollout history:

```bash
kubectl rollout history deployment <deployment-name>
```

Rollback if necessary:

```bash
kubectl rollout undo deployment <deployment-name>
```

---

# 🌐 Troubleshooting Networking

Check Services:

```bash
kubectl get svc
```

Verify Endpoints:

```bash
kubectl get endpoints
```

Test DNS inside a Pod:

```bash
nslookup kubernetes.default
```

Test connectivity:

```bash
curl http://service-name
```

Common networking problems:

* Incorrect Service selector
* DNS resolution failure
* NetworkPolicy restrictions
* Ingress misconfiguration
* Port mismatch

---

# 💾 Troubleshooting Storage

Check Persistent Volumes:

```bash
kubectl get pv
```

Check Persistent Volume Claims:

```bash
kubectl get pvc
```

Describe the claim:

```bash
kubectl describe pvc <pvc-name>
```

Common storage issues:

* PVC Pending
* StorageClass mismatch
* Insufficient storage
* Volume mount failure

---

# ⚙️ Troubleshooting Control Plane

Verify system Pods:

```bash
kubectl get pods -n kube-system
```

Important components:

* API Server
* Scheduler
* Controller Manager
* CoreDNS
* etcd

If these components are unhealthy, the cluster itself may become unavailable.

---

# ☁️ DevOps Perspective

A common production troubleshooting workflow looks like this:

```text
Alert
   │
   ▼
Grafana / Prometheus
   │
   ▼
kubectl get pods
   │
   ▼
Describe Pod
   │
   ▼
Logs
   │
   ▼
Identify Root Cause
   │
   ▼
Fix Configuration
   │
   ▼
Verify Application
```

Successful troubleshooting relies on:

* Monitoring
* Logging
* Observability
* Root cause analysis
* Proper rollback strategy

---

# 🏭 Production Example

An e-commerce website suddenly becomes unavailable.

Initial check:

```bash
kubectl get pods
```

Output:

```text
frontend-5b8c9d8f9-xd7qp

CrashLoopBackOff
```

Next step:

```bash
kubectl logs frontend-5b8c9d8f9-xd7qp
```

Output:

```text
Database Connection Failed
```

Further investigation:

```bash
kubectl describe secret database-secret
```

Root cause:

```text
Incorrect database password stored in Secret.
```

Solution:

* Update the Secret.
* Restart the Deployment.
* Verify application health.

This structured approach resolves the issue without unnecessary changes.

---

# 🎯 Common Interview Questions

### What is CrashLoopBackOff?

A Pod repeatedly starts, crashes, and Kubernetes continuously attempts to restart it.

---

### How do you troubleshoot a Pod that is not starting?

Typical steps:

1. `kubectl get pods`
2. `kubectl describe pod`
3. `kubectl logs`
4. Check Events
5. Verify image, resources, configuration, and Secrets.

---

### What causes ImagePullBackOff?

* Incorrect image name
* Private registry authentication failure
* Image does not exist
* Network connectivity issues

---

### How do you troubleshoot a Pending Pod?

Check:

* Available CPU and Memory
* Node status
* PVC status
* Scheduler events
* Node affinity or taints

---

### Which command do you use most during troubleshooting?

Common commands include:

* `kubectl describe`
* `kubectl logs`
* `kubectl get`
* `kubectl rollout`
* `kubectl top`

---

# 🔍 Useful Commands

```bash
kubectl get all

kubectl get events --sort-by=.metadata.creationTimestamp

kubectl describe pod <pod-name>

kubectl logs <pod-name>

kubectl logs <pod-name> --previous

kubectl get nodes

kubectl describe node <node-name>

kubectl get svc

kubectl get endpoints

kubectl get pv

kubectl get pvc

kubectl rollout status deployment <deployment-name>

kubectl rollout undo deployment <deployment-name>

kubectl top nodes

kubectl top pods
```

---

# 📑 Interview Cheat Sheet

```text
Application Issue
        │
        ▼
Pods
        │
        ▼
Events
        │
        ▼
Logs
        │
        ▼
Describe
        │
        ▼
Node
        │
        ▼
Network
        │
        ▼
Storage
        │
        ▼
Root Cause
```

Remember:

* **Never restart blindly—identify the root cause first.**
* **Start with `kubectl get` and `kubectl describe`.**
* **Use `kubectl logs` to inspect application errors.**
* **Check Events for scheduling and resource issues.**
* **Verify Services, Endpoints, DNS, and Ingress for networking problems.**
* **Inspect PVCs and PVs for storage-related issues.**
* **Use monitoring and logs together for faster incident resolution.**

---

# 📚 Summary

Kubernetes troubleshooting is one of the most important production skills for a DevOps Engineer. By following a structured approach—checking Pods, Events, Logs, Nodes, Networking, and Storage—you can quickly identify the root cause of issues and restore application availability.

In real-world production environments, effective troubleshooting reduces downtime, improves reliability, and enables faster incident response, making it an essential competency for every Kubernetes professional.

---

# 🔗 Related Topics

⬅️ **Previous:** Helm Basics → `../16-Helm-Basics/README.md`

➡️ **Next:** End-to-End Kubernetes Flow → `../18-End-to-End-Kubernetes-Flow/README.md`

### 📖 Recommended Reading

* Kubernetes End-to-End Flow
* Kubernetes Logging
* Kubernetes Monitoring (Prometheus & Grafana)
* Kubernetes Official Documentation
* Kubernetes Debugging Best Practices
