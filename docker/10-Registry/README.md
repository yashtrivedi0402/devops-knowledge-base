# 🗄️ Docker Registry

> **A Docker Registry is a centralized repository used to store, manage, version, and distribute Docker Images.**
>
> It enables developers and DevOps teams to build an image once and deploy the same image consistently across development, testing, staging, and production environments.

---

# 📖 Table of Contents

* What is a Docker Registry?
* Why Do We Need a Registry?
* Docker Registry Architecture
* Types of Docker Registries
* Docker Hub
* Working with Registries
* Image Lifecycle
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Docker Registry?

A **Docker Registry** is a service that stores Docker Images.

Instead of building an image on every server, images are stored in a registry and downloaded whenever required.

A registry allows teams to:

* Store images
* Share images
* Version images
* Pull images anywhere
* Maintain a centralized image repository

---

# 🎯 Why Do We Need a Registry?

Imagine a company with multiple servers.

Without a registry:

```text
Developer
     │
Build Image
     │
Copy Image Manually
     │
Production Server
```

Manual image transfer is slow and error-prone.

With a Docker Registry:

```text
Developer
      │
docker push
      ▼
Docker Registry
      │
docker pull
      ▼
Production Server
```

Benefits:

* Centralized storage
* Version control
* Faster deployments
* Easy collaboration
* Consistent environments
* CI/CD integration

---

# 🏗️ Docker Registry Architecture

```text
Developer Machine
        │
 docker build
        │
        ▼
 Docker Image
        │
 docker push
        ▼
 Docker Registry
        │
 docker pull
        ▼
 Docker Host
        │
        ▼
 Docker Container
```

---

# 🌍 Types of Docker Registries

## 1️⃣ Docker Hub

The default public Docker Registry maintained by Docker.

Features:

* Public repositories
* Private repositories
* Official Docker Images
* Community Images

Example:

```text
docker.io/library/nginx
```

---

## 2️⃣ Private Registry

Organizations often host their own registry.

Examples:

* Harbor
* Nexus Repository
* JFrog Artifactory
* Self-hosted Docker Registry

Benefits:

* Better security
* Internal image storage
* Access control
* Compliance

---

## 3️⃣ Cloud Container Registries

Cloud providers offer managed registries.

Examples:

* Amazon ECR (AWS)
* Google Artifact Registry (GCP)
* Azure Container Registry (Azure)

These services integrate with their respective cloud platforms.

---

# 🔄 Image Lifecycle

```text
Write Dockerfile
        │
        ▼
docker build
        │
        ▼
Docker Image
        │
docker tag
        │
        ▼
docker push
        │
        ▼
Docker Registry
        │
docker pull
        │
        ▼
Production Container
```

---

# 🛠️ Working with Registries

### Login

```bash
docker login
```

---

### Build Image

```bash
docker build -t myapp:v1 .
```

---

### Tag Image

```bash
docker tag myapp:v1 username/myapp:v1
```

Tag format:

```text
<registry>/<repository>:<tag>
```

Example:

```text
docker.io/yashtrivedi/myapp:v1
```

---

### Push Image

```bash
docker push username/myapp:v1
```

---

### Pull Image

```bash
docker pull username/myapp:v1
```

---

### Logout

```bash
docker logout
```

---

# ☁️ DevOps Perspective

Docker Registries are an essential part of modern DevOps workflows.

They are commonly used in:

* CI/CD pipelines
* Kubernetes deployments
* Blue-Green Deployments
* Canary Releases
* Multi-environment deployments
* Microservices

Best Practices:

* Tag images using versions (e.g., `v1.0.0`) instead of relying only on `latest`.
* Scan images for security vulnerabilities.
* Remove unused images from the registry.
* Use private registries for sensitive applications.
* Enable role-based access control (RBAC) where supported.

---

# 🏭 Production Example

A developer updates an e-commerce application.

Deployment flow:

1. Code is pushed to GitHub.
2. Jenkins starts the pipeline.
3. Docker builds the image.
4. Image is tagged:

```text
ecommerce:v2.3.0
```

5. Jenkins pushes the image to Amazon ECR.
6. Kubernetes pulls the latest image.
7. New Pods are deployed automatically.

The registry acts as the central source of truth for application images.

---

# 🎯 Common Interview Questions

### What is a Docker Registry?

A Docker Registry is a repository used to store and distribute Docker Images.

---

### What is Docker Hub?

Docker Hub is Docker's default cloud-based registry for storing and sharing container images.

---

### Which command uploads an image?

```bash
docker push
```

---

### Which command downloads an image?

```bash
docker pull
```

---

### Why is `docker tag` used?

It assigns a repository name and version to an image before pushing it to a registry.

---

### What is the difference between Docker Hub and a Private Registry?

| Docker Hub                        | Private Registry                             |
| --------------------------------- | -------------------------------------------- |
| Public by default                 | Private/Internal                             |
| Managed by Docker                 | Managed by an organization or cloud provider |
| Community images                  | Organization-specific images                 |
| Suitable for open-source projects | Suitable for enterprise workloads            |

---

# 🔍 Useful Commands

```bash
docker login

docker logout

docker build

docker tag

docker push

docker pull

docker search

docker images
```

---

# 📑 Interview Cheat Sheet

```text
Dockerfile
     │
     ▼
docker build
     │
     ▼
Docker Image
     │
docker tag
     │
     ▼
docker push
     │
     ▼
Docker Registry
     │
docker pull
     │
     ▼
Production Container
```

Remember:

* Registry stores Docker Images.
* Docker Hub is the default registry.
* `docker push` uploads images.
* `docker pull` downloads images.
* Always tag images with meaningful versions.
* Private registries are preferred for enterprise applications.

---

# 📚 Summary

A Docker Registry is a centralized platform for storing, managing, and distributing Docker Images. It enables teams to maintain consistent application versions across environments and plays a key role in CI/CD pipelines and cloud-native deployments.

For DevOps Engineers, registries are fundamental to automated software delivery. Understanding image tagging, pushing, pulling, and registry security is essential for deploying reliable and scalable applications.

---

# 🔗 Related Topics

⬅️ **Previous:** Docker Compose → `../09-Docker-Compose/README.md`

➡️ **Next:** Multi-Stage Builds → `../11-Multi-Stage-Builds/README.md`

### 📖 Recommended Reading

* Multi-Stage Builds
* Docker Images
* Dockerfile
* CI/CD Pipelines
* Docker Official Documentation
