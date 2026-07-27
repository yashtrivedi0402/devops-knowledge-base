# 🌍 Kubernetes Ingress

> **Ingress is a Kubernetes API object that manages external HTTP and HTTPS access to applications running inside a Kubernetes cluster.**
>
> Instead of exposing every application using a separate LoadBalancer or NodePort Service, Ingress provides a centralized entry point that routes traffic to different Services based on rules such as hostnames and URL paths.

---

# 📖 Table of Contents

* What is Ingress?
* Why Do We Need Ingress?
* Problems Without Ingress
* Ingress Architecture
* Ingress Controller
* Creating an Ingress
* Path-Based Routing
* Host-Based Routing
* TLS with Ingress
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Ingress?

An **Ingress** is a Kubernetes resource that controls how external users access applications inside a Kubernetes cluster.

Instead of exposing multiple Services directly, Ingress provides:

* Centralized Routing
* HTTP & HTTPS Support
* SSL/TLS Termination
* Host-Based Routing
* Path-Based Routing
* Single Public Entry Point

Ingress works together with an **Ingress Controller**, which implements the routing rules.

---

# 🎯 Why Do We Need Ingress?

Suppose a cluster hosts three applications:

* Frontend
* Backend API
* Admin Dashboard

Without Ingress, each application requires its own external Service.

Example:

```text
Frontend Service   → LoadBalancer
Backend Service    → LoadBalancer
Admin Service      → LoadBalancer
```

Problems:

* Higher cloud costs
* Multiple public IP addresses
* Difficult traffic management
* Separate SSL configuration for each Service

Ingress solves these problems by exposing all applications through a single entry point.

---

# ❌ Problems Without Ingress

```text
Internet
   │
   ├────────► LoadBalancer → Frontend
   │
   ├────────► LoadBalancer → Backend
   │
   └────────► LoadBalancer → Admin
```

Multiple LoadBalancers increase infrastructure complexity and cost.

---

# 🏗️ Ingress Architecture

```text
                    Internet
                        │
                        ▼
                Ingress Controller
                        │
                        ▼
                   Ingress Rules
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
Frontend Service   API Service   Admin Service
        │               │               │
        ▼               ▼               ▼
      Pods            Pods            Pods
```

Ingress routes incoming requests to the appropriate Service based on defined rules.

---

# ⚙️ What is an Ingress Controller?

An **Ingress Controller** is the component that watches Ingress resources and applies the routing rules.

Popular Ingress Controllers include:

* NGINX Ingress Controller
* Traefik
* HAProxy
* Kong
* AWS Load Balancer Controller
* Istio Gateway (Service Mesh)

Without an Ingress Controller, an Ingress resource does nothing.

---

# 🚀 Creating an Ingress

Example Ingress YAML:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: web-ingress

spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix

        backend:
          service:
            name: frontend-service

            port:
              number: 80
```

Create it:

```bash
kubectl apply -f ingress.yaml
```

---

# 🌐 Path-Based Routing

Different URL paths can route to different applications.

Example:

```text
example.com/
        │
        ▼
Frontend

example.com/api
        │
        ▼
Backend API

example.com/admin
        │
        ▼
Admin Dashboard
```

Architecture:

```text
                 Ingress
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      /           /api       /admin
        │           │           │
        ▼           ▼           ▼
   Frontend      API       Admin
```

---

# 🏠 Host-Based Routing

Ingress can also route traffic using different domain names.

Example:

```text
shop.example.com
        │
        ▼
Shopping App

api.example.com
        │
        ▼
Backend API

admin.example.com
        │
        ▼
Admin Portal
```

This enables multiple applications to share the same external IP address.

---

# 🔒 TLS with Ingress

Ingress supports HTTPS using TLS certificates.

Architecture:

```text
Internet
    │
 HTTPS
    │
    ▼
Ingress Controller
(TLS Termination)
    │
    ▼
Kubernetes Services
```

Benefits:

* Encrypted communication
* Centralized certificate management
* Simplified SSL configuration

---

# ☁️ DevOps Perspective

A typical production deployment uses the following networking flow:

```text
Internet
     │
     ▼
Cloud Load Balancer
     │
     ▼
Ingress Controller
     │
     ▼
Ingress
     │
     ▼
Services
     │
     ▼
Deployments
     │
     ▼
Pods
```

This architecture provides:

* Centralized routing
* Secure HTTPS access
* Simplified application exposure
* Better scalability
* Lower infrastructure costs

---

# 🏭 Production Example

An e-commerce platform hosts three applications.

Routing rules:

```text
shop.company.com
        │
        ▼
Frontend

shop.company.com/api
        │
        ▼
Backend API

shop.company.com/admin
        │
        ▼
Admin Dashboard
```

Traffic Flow:

```text
Internet
      │
      ▼
NGINX Ingress Controller
      │
      ▼
Ingress
      │
 ┌────┼──────────────┐
 ▼    ▼              ▼
Shop API         Admin
 │     │             │
 ▼     ▼             ▼
Pods Pods          Pods
```

All applications are accessible through a single public endpoint while remaining logically separated.

---

# 🎯 Common Interview Questions

### What is an Ingress?

Ingress is a Kubernetes resource that manages external HTTP and HTTPS access to Services inside a cluster.

---

### Why do we use Ingress?

Ingress provides centralized routing, SSL termination, host-based routing, and path-based routing while reducing the number of external LoadBalancers required.

---

### What is an Ingress Controller?

An Ingress Controller watches Ingress resources and configures the underlying proxy (such as NGINX or Traefik) to enforce routing rules.

---

### Can Ingress work without an Ingress Controller?

No.

An Ingress resource defines rules, but an Ingress Controller is required to implement those rules.

---

### What routing methods does Ingress support?

* Host-Based Routing
* Path-Based Routing

---

# 🔍 Useful Commands

```bash
kubectl get ingress

kubectl describe ingress <ingress-name>

kubectl apply -f ingress.yaml

kubectl delete ingress <ingress-name>

kubectl get ingress -A

kubectl get svc

kubectl get pods
```

---

# 📑 Interview Cheat Sheet

```text
Internet
     │
     ▼
Ingress Controller
     │
     ▼
Ingress
     │
 ┌───┼─────────────┐
 ▼   ▼             ▼
Service1      Service2
 │              │
 ▼              ▼
Pods          Pods
```

Remember:

* **Ingress manages external HTTP/HTTPS traffic.**
* **Ingress routes requests to Services, not directly to Pods.**
* **An Ingress Controller is required.**
* **Supports Host-Based and Path-Based Routing.**
* **TLS termination is commonly handled at the Ingress layer.**
* **One Ingress can expose multiple applications through a single public endpoint.**

---

# 📚 Summary

Ingress provides a flexible and centralized way to expose Kubernetes applications to external users. By routing traffic through a single entry point, it simplifies networking, reduces infrastructure costs, and enables advanced features such as host-based routing, path-based routing, and TLS termination.

For DevOps Engineers, Ingress is a key production component because it acts as the gateway between users and Kubernetes workloads, making secure and scalable application delivery possible.

---

# 🔗 Related Topics

⬅️ **Previous:** Volumes & Persistent Storage → `../10-Volumes-and-PersistentStorage/README.md`

➡️ **Next:** Scheduling → `../12-Scheduling/README.md`

### 📖 Recommended Reading

* Kubernetes Services
* Kubernetes Scheduling
* NGINX Ingress Controller
* Kubernetes Official Documentation
* Kubernetes Networking Best Practices
