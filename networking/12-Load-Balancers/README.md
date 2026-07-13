# ⚖️ AWS Load Balancers

> **A Load Balancer is a networking component that distributes incoming client requests across multiple servers or applications to improve availability, scalability, and fault tolerance.**
>
> Without a Load Balancer, every request would go to a single server, creating a **Single Point of Failure (SPOF)**. Modern production systems rely on Load Balancers to ensure applications remain highly available even if one or more servers fail.

---

# 📖 Table of Contents

* What is a Load Balancer?
* Why Do We Need It?
* Problem It Solves
* Load Balancer Architecture
* How Load Balancers Work
* Types of AWS Load Balancers
* Layer 4 vs Layer 7 Load Balancing
* Load Balancing Algorithms
* Health Checks
* Sticky Sessions
* Real-World Analogy
* DevOps Perspective
* Production Example
* Real Interview Scenario
* Production Decision
* Senior Engineer Tip
* Common Interview Questions
* Common Mistakes
* Troubleshooting Guide
* Commands to Verify
* Interview Cheat Sheet
* Summary
* Related Topics

---

# ❓ What is a Load Balancer?

A **Load Balancer (LB)** sits between clients and backend servers.

Instead of clients connecting directly to servers,

they send requests to the Load Balancer.

The Load Balancer then forwards each request to an appropriate backend server.

This ensures:

* High Availability
* Scalability
* Better Performance
* Fault Tolerance

---

# 🎯 Why Do We Need a Load Balancer?

Imagine 10,000 users trying to access one server.

```text
Users

↓

Server
```

The server eventually becomes overloaded.

Now imagine three servers:

```text
Users

↓

Load Balancer

├── Server A

├── Server B

└── Server C
```

Requests are distributed among all servers,

allowing the application to handle much higher traffic.

---

# ⚠️ Problem It Solves

Without a Load Balancer:

* One server handles all traffic.
* Performance decreases under heavy load.
* Server failure causes complete downtime.
* Scaling becomes difficult.
* Maintenance requires application downtime.

A Load Balancer solves these problems by intelligently distributing requests.

---

# 🏗️ Load Balancer Architecture

```text
                Internet
                    │
            Internet Gateway
                    │
          Application Load Balancer
          /          |           \
         /           |            \
     EC2-A       EC2-B        EC2-C
         │           │            │
      Application Application Application
```

Clients communicate only with the Load Balancer.

They never know which backend server processes the request.

---

# ⚙️ How Load Balancers Work

Suppose 6 users send requests.

```text
User 1 → LB → Server A

User 2 → LB → Server B

User 3 → LB → Server C

User 4 → LB → Server A

User 5 → LB → Server B

User 6 → LB → Server C
```

The Load Balancer continuously distributes requests according to its routing algorithm.

---

# 🌐 Types of AWS Load Balancers

AWS provides four Load Balancer types.

| Load Balancer                   | OSI Layer   | Primary Use                            |
| ------------------------------- | ----------- | -------------------------------------- |
| Application Load Balancer (ALB) | Layer 7     | HTTP / HTTPS Applications              |
| Network Load Balancer (NLB)     | Layer 4     | TCP / UDP Applications                 |
| Gateway Load Balancer (GWLB)    | Layer 3/4   | Virtual Firewalls & Network Appliances |
| Classic Load Balancer (CLB)     | Layer 4 & 7 | Legacy Applications                    |

---

# 🏆 Application Load Balancer (ALB)

Works at:

```text
Layer 7 (Application Layer)
```

Supports:

* HTTP
* HTTPS
* WebSocket
* gRPC

Features:

* Host-based Routing
* Path-based Routing
* SSL/TLS Termination
* WebSocket Support
* WAF Integration

Example

```text
example.com/api

↓

Backend API
```

```text
example.com/images

↓

Image Server
```

---

# 🚀 Network Load Balancer (NLB)

Works at:

```text
Layer 4 (Transport Layer)
```

Supports:

* TCP
* UDP
* TLS

Designed for:

* Ultra-low latency
* Millions of requests
* High-performance applications

Examples:

* Gaming
* Financial Trading
* VoIP
* DNS

---

# 🛡️ Gateway Load Balancer (GWLB)

Works with:

* Firewalls
* IDS
* IPS
* Security Appliances

Instead of forwarding requests to applications,

it forwards them to security devices.

---

# 📦 Classic Load Balancer (CLB)

Older AWS Load Balancer.

Supports:

* Layer 4
* Layer 7

AWS recommends using ALB or NLB for new deployments.

---

# 🔄 Layer 4 vs Layer 7

| Layer 4 (NLB)          | Layer 7 (ALB)                 |
| ---------------------- | ----------------------------- |
| Routes using IP & Port | Routes using HTTP Information |
| Faster                 | More Intelligent              |
| TCP / UDP              | HTTP / HTTPS                  |
| Lower Latency          | More Features                 |
| No Path Routing        | Supports Path Routing         |

---

# ⚙️ Load Balancing Algorithms

Common algorithms include:

### Round Robin

Requests are distributed equally.

```text
A → B → C → A → B → C
```

---

### Least Connections

The server handling the fewest active connections receives the next request.

---

### Weighted Routing

Powerful servers receive more traffic than weaker ones.

Example:

```text
Server A → 60%

Server B → 30%

Server C → 10%
```

---

### IP Hash

The client's IP determines which backend server receives the request.

Useful for maintaining user consistency.

---

# ❤️ Health Checks

A Load Balancer continuously checks backend server health.

Example:

```text
ALB

↓

GET /health
```

If:

```text
HTTP 200
```

Server is healthy.

If:

```text
HTTP 500
```

or timeout,

the server is removed from the rotation until it becomes healthy again.

---

# 🍪 Sticky Sessions

Normally,

each request may reach a different backend server.

Sticky Sessions ensure that requests from the same user continue reaching the same server for a specific period.

Useful for:

* Shopping carts
* Legacy web applications
* Session-based authentication

Modern microservices usually prefer stateless architectures instead.

---

# 🌍 Real-World Analogy

Imagine a restaurant.

Customers don't enter the kitchen directly.

A receptionist greets customers and assigns them to available tables.

If one waiter becomes unavailable,

new customers are assigned elsewhere.

The receptionist is the Load Balancer.

---

# ☁️ DevOps Perspective

You'll encounter Load Balancers in almost every cloud deployment.

Examples:

* AWS ALB
* AWS NLB
* Kubernetes Ingress
* NGINX
* HAProxy
* Traefik
* Istio Gateway

Typical uses:

* High Availability
* SSL Termination
* Traffic Distribution
* Blue-Green Deployments
* Canary Releases

---

# 🏭 Production Example

A typical production architecture:

```text
Internet

↓

Route53

↓

Application Load Balancer

├── EC2 Instance A

├── EC2 Instance B

└── EC2 Instance C

↓

RDS Database
```

The ALB distributes traffic among healthy application servers.

---

# 🎯 Real Interview Scenario

### Scenario

Your application runs on three EC2 instances behind an Application Load Balancer.

One instance crashes.

What happens?

### Solution

1. ALB performs periodic Health Checks.
2. Failed instance stops responding.
3. ALB marks it **Unhealthy**.
4. Traffic is automatically routed only to healthy instances.
5. Users experience little or no downtime.
6. Auto Scaling may launch a replacement instance.

This combination of **ALB + Auto Scaling** provides high availability.

---

# 🚀 Production Decision

Choose **ALB** when:

* Hosting web applications.
* Running REST APIs.
* Using Kubernetes Ingress.
* Requiring path-based or host-based routing.
* Needing SSL termination.

Choose **NLB** when:

* Using TCP/UDP protocols.
* Building gaming platforms.
* Handling financial transactions.
* Requiring ultra-low latency.
* Managing millions of concurrent connections.

Choose **GWLB** when:

* Deploying network security appliances.

Avoid **Classic Load Balancers** for new applications.

---

# 🧠 Senior Engineer Tip

Many beginners think:

> "A Load Balancer simply distributes traffic."

A senior engineer knows it also provides:

* SSL Termination
* Health Checks
* High Availability
* Fault Tolerance
* Intelligent Routing
* Traffic Shifting
* Blue-Green Deployments
* Canary Releases
* WAF Integration

Modern Load Balancers are much more than traffic distributors.

---

# 💼 Common Interview Questions

### Q1. What is a Load Balancer?

A service that distributes incoming traffic across multiple backend servers.

---

### Q2. Why do we use a Load Balancer?

To improve availability, scalability, and fault tolerance.

---

### Q3. What is the difference between ALB and NLB?

ALB operates at Layer 7 using HTTP/HTTPS.

NLB operates at Layer 4 using TCP/UDP.

---

### Q4. What are Health Checks?

Periodic requests sent by the Load Balancer to determine whether a backend server is healthy.

---

### Q5. What happens if one server fails?

The Load Balancer removes it from the routing pool and forwards requests only to healthy servers.

---

### Q6. What is SSL Termination?

The Load Balancer decrypts HTTPS traffic, reducing the encryption workload on backend servers.

---

### Q7. Why is ALB commonly used with Kubernetes?

Because it supports:

* Path-based Routing
* Host-based Routing
* HTTPS
* Ingress Integration

---

# 🔥 Common Mistakes

❌ Every Load Balancer understands HTTP.

✅ Only Layer 7 Load Balancers understand HTTP.

---

❌ Load Balancers replace Auto Scaling.

✅ Load Balancers distribute traffic.

Auto Scaling adjusts the number of servers.

---

❌ Failed servers automatically recover.

✅ Health Checks only stop routing traffic.

Recovery typically requires Auto Scaling or manual intervention.

---

❌ Sticky Sessions should always be enabled.

✅ Modern cloud-native applications are usually designed to be stateless.

---

# 🔍 Troubleshooting Guide

If traffic isn't reaching the application:

1. Verify DNS resolution.
2. Check Load Balancer status.
3. Review Listener configuration.
4. Verify Target Group registration.
5. Check Health Check endpoint.
6. Confirm Security Groups.
7. Verify Route Tables.
8. Check application logs.
9. Confirm backend service is listening on the expected port.

---

# 💻 Commands to Verify

AWS CLI

```bash
aws elbv2 describe-load-balancers

aws elbv2 describe-target-groups

aws elbv2 describe-target-health

aws elbv2 describe-listeners
```

Linux

```bash
curl http://localhost:8080/health

ss -tulnp

netstat -tulnp
```

---

# 💼 Interview Cheat Sheet

Remember:

```text
Internet

↓

Route53

↓

Load Balancer

↓

Target Group

↓

Healthy Backend Servers

↓

Application
```

Key Facts

* ALB → Layer 7
* NLB → Layer 4
* GWLB → Security Appliances
* CLB → Legacy
* Health Checks remove failed servers automatically.
* Auto Scaling replaces failed instances.
* ALB supports Path-Based and Host-Based Routing.

---

# 📚 Summary

A Load Balancer is a critical component of modern cloud architecture that distributes incoming traffic across multiple backend resources.

By performing health checks, intelligent routing, and SSL termination, it ensures applications remain highly available, scalable, and resilient.

Understanding the different AWS Load Balancer types and when to use each is essential for every DevOps Engineer designing production-grade infrastructure.

---

# 🔗 Related Topics

⬅️ Previous: **Security Groups vs NACLs** → `../11-Security-Groups-vs-NACLs/README.md`

➡️ Next: **Network Troubleshooting** → `../13-Network-Troubleshooting/README.md`

### 📖 Recommended Reading

* Security Groups vs NACLs
* Internet Gateway
* NAT Gateway
* Route Tables
* Kubernetes Ingress
* AWS Auto Scaling
* Route 53
