# 🧩 Docker Compose

> **Docker Compose is a tool that allows you to define and manage multi-container Docker applications using a single YAML configuration file.**
>
> Instead of running multiple `docker run` commands manually, Docker Compose enables you to start, stop, and manage an entire application stack with a single command.

---

# 📖 Table of Contents

* What is Docker Compose?
* Why Do We Need Docker Compose?
* Docker Compose Architecture
* docker-compose.yml File
* Common Docker Compose Commands
* Docker Compose Workflow
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Docker Compose?

Docker Compose is a tool for running **multiple Docker containers as a single application**.

Instead of starting each container individually, you define all services inside a **YAML** file.

Example application:

* Frontend
* Backend API
* MySQL Database
* Redis Cache

All can be started together using one command.

---

# 🎯 Why Do We Need Docker Compose?

Imagine an application with:

* React Frontend
* Spring Boot Backend
* MySQL Database
* Redis Cache

Without Docker Compose:

```text
docker run mysql

docker run redis

docker run backend

docker run frontend
```

Managing each container separately becomes difficult.

With Docker Compose:

```text
docker compose up
```

Everything starts automatically.

Benefits:

* Easy deployment
* Centralized configuration
* Automatic networking
* Simplified management
* Better scalability
* Faster development

---

# 🏗️ Docker Compose Architecture

```text
             docker-compose.yml
                     │
             docker compose up
                     │
                     ▼
              Docker Engine
                     │
      ┌──────────────┼──────────────┐
      ▼              ▼              ▼
Frontend        Backend API      MySQL
                                      │
                                      ▼
                                   Volume
```

---

# 📄 docker-compose.yml File

A Compose file defines:

* Services
* Images
* Networks
* Volumes
* Environment Variables
* Port Mappings

Example:

```yaml
version: "3.9"

services:

  web:
    image: nginx
    ports:
      - "80:80"

  database:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: password
```

---

# 🛠️ Common Docker Compose Commands

### Start Services

```bash
docker compose up
```

---

### Start in Background

```bash
docker compose up -d
```

---

### Stop Services

```bash
docker compose down
```

---

### View Running Services

```bash
docker compose ps
```

---

### View Logs

```bash
docker compose logs
```

---

### Restart Services

```bash
docker compose restart
```

---

### Build Images

```bash
docker compose build
```

---

# 🔄 Docker Compose Workflow

```text
Create docker-compose.yml
           │
           ▼
docker compose up
           │
           ▼
Create Network
           │
           ▼
Create Volumes
           │
           ▼
Start Containers
           │
           ▼
Application Running
```

Docker Compose automatically:

* Creates networks
* Creates volumes
* Starts containers
* Connects services together

---

# ☁️ DevOps Perspective

Docker Compose is widely used for:

* Local development
* Testing environments
* CI/CD pipelines
* Multi-container applications
* Microservices
* Development stacks

Although Kubernetes is preferred for large-scale production environments, Docker Compose is an excellent choice for development, demos, and small deployments.

Best Practices:

* Store configuration in environment variables.
* Use named volumes for persistent data.
* Avoid hardcoding secrets.
* Keep services modular.
* Version-control the Compose file.

---

# 🏭 Production Example

A company has an online shopping application.

Components:

```text
Frontend
Backend API
MySQL
Redis
```

Compose file manages all services.

Deployment:

```bash
docker compose up -d
```

Docker Compose:

1. Creates the application network.
2. Creates required volumes.
3. Starts MySQL.
4. Starts Redis.
5. Starts Backend.
6. Starts Frontend.

All services communicate automatically using service names.

---

# 🎯 Common Interview Questions

### What is Docker Compose?

Docker Compose is a tool for defining and managing multi-container Docker applications using a YAML configuration file.

---

### Which file does Docker Compose use?

```text
docker-compose.yml
```

---

### Which command starts all services?

```bash
docker compose up
```

---

### Which command stops all services?

```bash
docker compose down
```

---

### What are Services in Docker Compose?

Services define the containers that make up an application, including their images, ports, volumes, and environment variables.

---

### Does Docker Compose automatically create networks?

Yes. Docker Compose creates a default network and connects all services unless a custom network is specified.

---

# 🔍 Useful Commands

```bash
docker compose up

docker compose up -d

docker compose down

docker compose ps

docker compose logs

docker compose restart

docker compose build

docker compose pull
```

---

# 📑 Interview Cheat Sheet

```text
docker-compose.yml
         │
         ▼
docker compose up
         │
         ▼
Create Network
         │
         ▼
Create Volumes
         │
         ▼
Start Containers
         │
         ▼
Application Running
```

Remember:

* Docker Compose manages multi-container applications.
* Configuration is stored in `docker-compose.yml`.
* `docker compose up` starts all services.
* `docker compose down` stops and removes them.
* Services communicate using Docker's built-in DNS.
* Compose automatically creates a default network.

---

# 📚 Summary

Docker Compose simplifies the deployment and management of multi-container applications by defining infrastructure in a single YAML file. It automates networking, volume creation, and service orchestration, making development and testing significantly easier.

For DevOps Engineers, Docker Compose is an essential tool for local development, CI/CD pipelines, and microservices. Understanding Compose also provides a strong foundation before learning Kubernetes orchestration.

---

# 🔗 Related Topics

⬅️ **Previous:** Networking → `../08-Networking/README.md`

➡️ **Next:** Registry → `../10-Registry/README.md`

### 📖 Recommended Reading

* Docker Registry
* Docker Volumes
* Docker Networking
* Kubernetes Basics
* Docker Official Documentation
