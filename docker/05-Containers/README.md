# 📦 Docker Containers

> **A Docker Container is a lightweight, isolated, and executable instance of a Docker Image.**
>
> Containers package an application with all its dependencies and run consistently across different environments while sharing the host operating system's kernel.

---

# 📖 Table of Contents

* What is a Docker Container?
* Why Do We Need Containers?
* Container Architecture
* Container Lifecycle
* Working with Containers
* Container States
* Container vs Image
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Docker Container?

A **Docker Container** is a **running instance of a Docker Image**.

It provides an isolated environment where an application can execute without interfering with other applications running on the same host.

Each container contains:

* Application Code
* Runtime
* Libraries
* Dependencies
* Configuration

Containers **share the host OS kernel**, making them much lighter than Virtual Machines.

---

# 🎯 Why Do We Need Containers?

Containers solve many deployment challenges:

* Environment consistency
* Application isolation
* Fast startup
* Efficient resource usage
* Easy scaling
* Portable deployments

Instead of configuring every server manually, developers simply run the same container everywhere.

---

# 🏗️ Container Architecture

```text
                Docker Image
                      │
               docker run
                      │
                      ▼
              Docker Container
        ┌──────────┼──────────┐
        ▼          ▼          ▼
   Application   Libraries   Config
        │
        ▼
 Host Operating System Kernel
        │
        ▼
      Hardware
```

---

# 🔄 Container Lifecycle

```text
Docker Image
      │
docker run
      ▼
Created
      ▼
Running
      ▼
Paused
      ▼
Stopped
      ▼
Removed
```

Container lifecycle commands:

| State          | Command          |
| -------------- | ---------------- |
| Create & Start | `docker run`     |
| Stop           | `docker stop`    |
| Start Again    | `docker start`   |
| Restart        | `docker restart` |
| Pause          | `docker pause`   |
| Resume         | `docker unpause` |
| Delete         | `docker rm`      |

---

# 🛠️ Working with Containers

### Run a Container

```bash
docker run nginx
```

---

### Run in Detached Mode

```bash
docker run -d nginx
```

---

### List Running Containers

```bash
docker ps
```

---

### List All Containers

```bash
docker ps -a
```

---

### Stop a Container

```bash
docker stop <container_id>
```

---

### Start a Container

```bash
docker start <container_id>
```

---

### Restart a Container

```bash
docker restart <container_id>
```

---

### Remove a Container

```bash
docker rm <container_id>
```

---

### Execute Commands Inside a Running Container

```bash
docker exec -it <container_id> bash
```

---

### View Container Logs

```bash
docker logs <container_id>
```

---

# 🚦 Container States

```text
Created
   │
   ▼
Running
   │
 ┌─┴─────────┐
 ▼           ▼
Paused    Stopped
              │
              ▼
          Removed
```

---

# ⚖️ Container vs Image

| Docker Image                          | Docker Container                          |
| ------------------------------------- | ----------------------------------------- |
| Blueprint                             | Running instance                          |
| Read-only                             | Read & Write                              |
| Static                                | Dynamic                                   |
| Created using `docker build`          | Created using `docker run`                |
| Multiple containers can use one image | Each container has its own writable layer |

---

# ☁️ DevOps Perspective

Containers are the foundation of modern DevOps.

They are used for:

* Microservices
* CI/CD pipelines
* Kubernetes Pods
* Cloud-native applications
* Testing environments
* Production deployments
* Application scaling

Best practices:

* Run one main process per container.
* Keep containers stateless whenever possible.
* Store persistent data in Docker Volumes.
* Monitor container health and logs.

---

# 🏭 Production Example

A company deploys an online shopping application.

Deployment flow:

1. Build the Docker Image.
2. Push the image to Docker Hub.
3. Production server pulls the image.
4. Run the application container:

```bash
docker run -d -p 80:8080 ecommerce:v1
```

Docker creates an isolated container, maps port **8080** inside the container to port **80** on the host, and starts serving user requests.

---

# 🎯 Common Interview Questions

### What is a Docker Container?

A Docker Container is a running instance of a Docker Image.

---

### What command creates and starts a container?

```bash
docker run
```

---

### What command lists running containers?

```bash
docker ps
```

---

### What command stops a container?

```bash
docker stop <container_id>
```

---

### What command opens a shell inside a running container?

```bash
docker exec -it <container_id> bash
```

---

### Why are Docker Containers lightweight?

Because they share the host operating system's kernel instead of running a separate guest operating system like virtual machines.

---

# 🔍 Useful Commands

```bash
docker run

docker ps

docker ps -a

docker stop

docker start

docker restart

docker rm

docker exec

docker logs

docker inspect
```

---

# 📑 Interview Cheat Sheet

```text
Docker Image
      │
docker run
      ▼
Container
      │
 ┌────┼────┐
 ▼    ▼    ▼
Logs Exec Stop
      │
      ▼
Remove
```

Remember:

* Container = Running Image
* Images are immutable
* Containers are isolated
* `docker run` creates a container
* `docker ps` lists running containers
* `docker exec` accesses a running container
* `docker logs` displays application logs

---

# 📚 Summary

Docker Containers are lightweight, isolated runtime environments created from Docker Images. They provide consistency, portability, and efficient resource utilization, making them ideal for deploying modern applications.

For DevOps Engineers, containers are the core deployment unit used in CI/CD pipelines, Kubernetes clusters, cloud platforms, and microservices architectures. Understanding the container lifecycle and management commands is essential for real-world DevOps operations.

---

# 🔗 Related Topics

⬅️ **Previous:** Images → `../04-Images/README.md`

➡️ **Next:** Dockerfile → `../06-Dockerfile/README.md`

### 📖 Recommended Reading

* Dockerfile
* Docker Volumes
* Docker Networking
* Docker Compose
* Docker Official Documentation
