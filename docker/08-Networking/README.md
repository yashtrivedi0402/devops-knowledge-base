# 🌐 Docker Networking

> **Docker Networking enables communication between Docker containers, the host machine, and external networks.**
>
> It provides isolated virtual networks that allow containers to securely communicate with each other while keeping applications portable, scalable, and easy to manage.

---

# 📖 Table of Contents

* What is Docker Networking?
* Why Do We Need Docker Networking?
* Docker Networking Architecture
* Network Drivers
* How Container Communication Works
* Port Mapping
* Working with Networks
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Docker Networking?

Docker Networking is the mechanism that connects:

* Container ↔ Container
* Container ↔ Host Machine
* Container ↔ Internet
* Container ↔ External Services

Every container is attached to a Docker network, allowing it to send and receive data securely.

---

# 🎯 Why Do We Need Docker Networking?

Without networking:

* Containers cannot communicate.
* Applications cannot access databases.
* Users cannot access containerized applications.
* Multi-container applications cannot function.

Docker Networking provides:

* Secure communication
* Network isolation
* Service discovery
* Easy scalability
* Simplified microservices communication

---

# 🏗️ Docker Networking Architecture

```text
                     Internet
                         │
                         ▼
                  Host Machine
                         │
                  Docker Engine
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
   Bridge Network   Host Network    Overlay Network
        │                │                │
        ▼                ▼                ▼
   Container A      Container B      Container C
```

---

# 🌍 Docker Network Drivers

Docker supports multiple network drivers.

## 1️⃣ Bridge Network (Default)

The default network for containers running on a single host.

Features:

* Automatic IP assignment
* Container-to-container communication
* Network isolation

Example:

```bash
docker network create mybridge
```

---

## 2️⃣ Host Network

The container shares the host machine's network stack.

Features:

* No network isolation
* Better performance
* No port mapping required

Example:

```bash
docker run --network host nginx
```

---

## 3️⃣ None Network

The container has no network connectivity.

Example:

```bash
docker run --network none ubuntu
```

Useful for highly secure or isolated workloads.

---

## 4️⃣ Overlay Network

Used in Docker Swarm for communication across multiple Docker hosts.

Features:

* Multi-host networking
* Encrypted communication
* Distributed applications

---

# 🔄 How Container Communication Works

Containers connected to the same Docker network can communicate using:

* Container Name
* Container IP Address

Example:

```text
Frontend Container
        │
        ▼
Backend Container
        │
        ▼
Database Container
```

Instead of using IP addresses, Docker automatically resolves container names using its built-in DNS.

---

# 🔌 Port Mapping

Containers have their own internal ports.

To make an application accessible from outside the container, ports must be mapped.

Example:

```bash
docker run -d -p 8080:80 nginx
```

Explanation:

```text
Host Port 8080
        │
        ▼
Container Port 80
```

Now users can access NGINX using:

```text
http://localhost:8080
```

---

# 🛠️ Working with Networks

### List Networks

```bash
docker network ls
```

---

### Inspect a Network

```bash
docker network inspect bridge
```

---

### Create a Network

```bash
docker network create mynetwork
```

---

### Connect a Container

```bash
docker network connect mynetwork mycontainer
```

---

### Disconnect a Container

```bash
docker network disconnect mynetwork mycontainer
```

---

### Remove a Network

```bash
docker network rm mynetwork
```

---

# ☁️ DevOps Perspective

Docker Networking is essential for:

* Microservices
* API communication
* Database connectivity
* Docker Compose
* Kubernetes networking
* Service discovery
* Cloud-native applications

Best Practices:

* Use custom bridge networks instead of the default bridge.
* Expose only required ports.
* Avoid using the Host network unless necessary.
* Use service names instead of IP addresses.
* Isolate applications using separate networks.

---

# 🏭 Production Example

An e-commerce application has three containers:

```text
Frontend
     │
     ▼
Backend API
     │
     ▼
MySQL Database
```

All containers are attached to the same custom bridge network.

Deployment:

```bash
docker network create ecommerce-net

docker run -d --network ecommerce-net --name mysql mysql

docker run -d --network ecommerce-net --name backend backend:v1

docker run -d -p 80:8080 --network ecommerce-net --name frontend frontend:v1
```

The frontend communicates with the backend using the container name **backend**, and the backend connects to the database using **mysql**, without needing hardcoded IP addresses.

---

# 🎯 Common Interview Questions

### What is Docker Networking?

Docker Networking enables communication between containers, the host, and external networks.

---

### Which is the default Docker network?

**Bridge Network**

---

### What command lists Docker networks?

```bash
docker network ls
```

---

### What does `-p 8080:80` mean?

It maps:

* Host Port → **8080**
* Container Port → **80**

---

### Can containers communicate without exposing ports?

Yes. Containers on the same Docker network can communicate using container names or internal IP addresses.

---

### What is an Overlay Network?

An Overlay Network connects containers running on multiple Docker hosts, primarily used in Docker Swarm.

---

# 🔍 Useful Commands

```bash
docker network ls

docker network inspect

docker network create

docker network rm

docker network connect

docker network disconnect

docker inspect

docker run -p
```

---

# 📑 Interview Cheat Sheet

```text
Docker Engine
      │
      ▼
Docker Network
      │
 ┌────┼────┐
 ▼    ▼    ▼
Frontend Backend Database
      │
      ▼
Container Communication
```

Remember:

* Bridge is the default network.
* Containers on the same network communicate directly.
* Docker provides built-in DNS resolution.
* `-p HostPort:ContainerPort` exposes applications.
* Overlay Networks are used for multi-host communication.

---

# 📚 Summary

Docker Networking provides secure and efficient communication between containers, the host machine, and external systems. It enables containerized applications to work together through isolated networks, service discovery, and port mapping.

For DevOps Engineers, understanding Docker Networking is essential for deploying microservices, designing scalable architectures, troubleshooting connectivity issues, and preparing for Kubernetes and cloud-native environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Volumes → `../07-Volumes/README.md`

➡️ **Next:** Docker Compose → `../09-Docker-Compose/README.md`

### 📖 Recommended Reading

* Docker Compose
* Docker Containers
* Docker Volumes
* Kubernetes Networking
* Docker Official Documentation
