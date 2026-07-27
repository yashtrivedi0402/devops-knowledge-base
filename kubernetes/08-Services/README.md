# 🌐 Kubernetes Services

> **A Service is a Kubernetes resource that provides a stable network endpoint for accessing one or more Pods.**
>
> Since Pods are temporary and their IP addresses can change, Services ensure reliable communication between applications and users by exposing Pods through a consistent IP address and DNS name.

---

# 📖 Table of Contents

* What is a Service?
* Why Do We Need Services?
* Problems Without Services
* Service Architecture
* Types of Services
* Creating a Service
* Service Discovery
* Load Balancing
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Service?

A **Service** is a Kubernetes object that provides a **stable network endpoint** for a group of Pods.

Instead of connecting directly to individual Pods, applications communicate through a Service.

A Service provides:

* Stable IP Address
* DNS Name
* Load Balancing
* Service Discovery
* Reliable Communication

Even if Pods are recreated, the Service remains available.

---

# 🎯 Why Do We Need Services?

Pods are **ephemeral**.

Whenever a Pod:

* Crashes
* Is deleted
* Is recreated
* Is rescheduled

its IP address changes.

If applications communicated directly with Pod IPs, communication would frequently break.

Services solve this problem by providing a permanent endpoint.

---

# ❌ Problems Without Services

Suppose an application has three Pods.

```text
Pod A → 10.0.0.2

Pod B → 10.0.0.5

Pod C → 10.0.0.9
```

If **Pod B** crashes:

```text
Old Pod B
10.0.0.5

↓

New Pod B
10.0.0.12
```

Every client would need to know the new IP address.

This becomes impossible in large production environments.

---

# 🏗️ Service Architecture

```text
                 Client
                    │
                    ▼
            Kubernetes Service
             (Stable IP / DNS)
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
    Pod 1         Pod 2         Pod 3
```

The Service automatically forwards traffic to healthy Pods.

Applications communicate with the Service rather than individual Pods.

---

# 🌍 Types of Kubernetes Services

## 1️⃣ ClusterIP (Default)

* Internal communication only
* Accessible inside the cluster
* Default Service type

Architecture:

```text
Application
      │
      ▼
ClusterIP Service
      │
      ▼
Pods
```

Example:

```yaml
spec:
  type: ClusterIP
```

---

## 2️⃣ NodePort

Exposes the application on a port of every Worker Node.

Architecture:

```text
Internet
     │
     ▼
NodeIP:30080
     │
     ▼
NodePort Service
     │
     ▼
Pods
```

Example:

```yaml
spec:
  type: NodePort
```

Default NodePort range:

```text
30000 - 32767
```

---

## 3️⃣ LoadBalancer

Creates an external cloud load balancer.

Commonly used on:

* Amazon EKS
* Azure AKS
* Google GKE

Architecture:

```text
Internet
     │
     ▼
Cloud Load Balancer
     │
     ▼
Service
     │
     ▼
Pods
```

Example:

```yaml
spec:
  type: LoadBalancer
```

---

## 4️⃣ ExternalName

Maps a Kubernetes Service to an external DNS name.

Example:

```yaml
spec:
  type: ExternalName
```

Useful when applications need to access external services such as managed databases or third-party APIs.

---

# 🚀 Creating a Service

Example YAML:

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
  - port: 80
    targetPort: 80

  type: ClusterIP
```

Create the Service:

```bash
kubectl apply -f service.yaml
```

---

# 🔍 Verify the Service

List Services:

```bash
kubectl get services
```

Example:

```text
NAME            TYPE        CLUSTER-IP      PORT(S)
nginx-service   ClusterIP   10.96.120.15    80/TCP
```

Describe the Service:

```bash
kubectl describe service nginx-service
```

View Endpoints:

```bash
kubectl get endpoints
```

---

# 🔄 Service Discovery

Every Service automatically receives:

* Cluster IP
* DNS Name

Example:

```text
nginx-service.default.svc.cluster.local
```

Applications inside the cluster usually communicate using the shorter Service name:

```text
http://nginx-service
```

instead of using IP addresses.

---

# ⚖️ Load Balancing

When multiple Pods exist:

```text
Service
   │
 ┌─┼──────────────┐
 ▼ ▼              ▼
Pod1           Pod2
                  ▼
                Pod3
```

Incoming requests are distributed across healthy Pods.

Benefits:

* Better performance
* High availability
* Fault tolerance

---

# ☁️ DevOps Perspective

In production:

* Deployments manage Pods.
* Services expose Pods.
* Ingress provides external routing.

Typical architecture:

```text
Internet
     │
     ▼
Ingress
     │
     ▼
Service
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

This layered design provides scalability, reliability, and easier management.

---

# 🏭 Production Example

An e-commerce application runs five Pods.

```text
Internet
     │
     ▼
LoadBalancer Service
     │
 ┌───┼───────────────┐
 ▼   ▼               ▼
Pod1 Pod2          Pod3
 │
Pod4
 │
Pod5
```

If one Pod fails:

* The Service automatically stops sending traffic to it.
* Requests continue to be routed to healthy Pods.
* The Deployment creates a replacement Pod.

Users experience little or no disruption.

---

# 🎯 Common Interview Questions

### What is a Kubernetes Service?

A Service is a Kubernetes resource that provides a stable network endpoint for accessing one or more Pods.

---

### Why do we need Services?

Because Pods are temporary and their IP addresses change. Services provide stable communication using a fixed IP and DNS name.

---

### What are the four main Service types?

* ClusterIP
* NodePort
* LoadBalancer
* ExternalName

---

### Which Service type is the default?

**ClusterIP**

---

### Which Service type is commonly used in cloud environments?

**LoadBalancer**

---

### Can a Service perform load balancing?

Yes. It distributes traffic across multiple healthy Pods selected by its label selector.

---

# 🔍 Useful Commands

```bash
kubectl get services

kubectl describe service <service-name>

kubectl get endpoints

kubectl expose deployment nginx \
  --port=80 \
  --target-port=80 \
  --type=ClusterIP

kubectl delete service <service-name>
```

---

# 📑 Interview Cheat Sheet

```text
Client
   │
   ▼
Service
   │
 ┌─┼──────────────┐
 ▼ ▼              ▼
Pod1           Pod2
                  ▼
                Pod3
```

Remember:

* **Pods have temporary IP addresses.**
* **Services provide stable networking.**
* **ClusterIP is the default Service type.**
* **NodePort exposes applications through node ports.**
* **LoadBalancer is commonly used in cloud environments.**
* **Services use label selectors to identify target Pods.**

---

# 📚 Summary

Kubernetes Services provide a stable and reliable networking layer for applications running in Pods. By abstracting away the dynamic nature of Pod IP addresses, Services enable seamless communication, built-in load balancing, and service discovery.

For DevOps Engineers, understanding Services is essential because nearly every production Kubernetes application relies on them to expose workloads internally or externally while maintaining high availability and scalability.

---

# 🔗 Related Topics

⬅️ **Previous:** Namespaces → `../07-Namespaces/README.md`

➡️ **Next:** ConfigMaps & Secrets → `../09-ConfigMaps-and-Secrets/README.md`

### 📖 Recommended Reading

* Kubernetes ConfigMaps
* Kubernetes Ingress
* Kubernetes Networking
* Kubernetes Official Documentation
* Kubernetes Best Practices
