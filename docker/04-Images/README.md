# 🖼️ Docker Images

> **A Docker Image is a lightweight, read-only template that contains everything required to run an application, including the application code, runtime, libraries, dependencies, and configuration files.**
>
> Images are the blueprint for containers. Every Docker container is created from a Docker Image.

---

# 📖 Table of Contents

* What is a Docker Image?
* Why Do We Need Images?
* Image Architecture
* Docker Image Layers
* Image Lifecycle
* Working with Images
* Image vs Container
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Docker Image?

A **Docker Image** is a packaged snapshot of an application and everything it needs to run.

An image includes:

* Application Code
* Runtime
* System Libraries
* Dependencies
* Environment Variables
* Configuration Files

Docker Images are **read-only** and cannot be modified after they are built. If changes are needed, a new image is created.

---

# 🎯 Why Do We Need Images?

Docker Images solve several deployment challenges:

* Package applications with all dependencies
* Ensure consistency across environments
* Enable fast deployments
* Support versioning and rollbacks
* Make applications portable

Without Docker Images, developers would need to manually install software and dependencies on every server.

---

# 🏗️ Docker Image Architecture

```text
                 Dockerfile
                      │
              docker build
                      │
                      ▼
               Docker Image
                      │
               docker run
                      ▼
             Docker Container
```

---

# 🧱 Docker Image Layers

Docker Images are built in **layers**.

Each instruction in a Dockerfile creates a new layer.

Example Dockerfile:

```dockerfile
FROM ubuntu:24.04
RUN apt update
RUN apt install -y nginx
COPY . /app
CMD ["nginx", "-g", "daemon off;"]
```

Layer structure:

```text
Layer 5 → CMD
Layer 4 → COPY
Layer 3 → RUN apt install
Layer 2 → RUN apt update
Layer 1 → Base Image (Ubuntu)
```

### Benefits of Layers

* Faster builds
* Layer caching
* Reduced storage usage
* Efficient image sharing

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
 ┌──────┴──────┐
 ▼             ▼
docker push   docker run
 ▼             ▼
Registry    Container
```

---

# 🛠️ Working with Images

### Pull an Image

Download an image from Docker Hub.

```bash
docker pull nginx
```

---

### List Images

```bash
docker images
```

---

### Build an Image

```bash
docker build -t myapp:v1 .
```

---

### Remove an Image

```bash
docker rmi nginx
```

---

### Inspect an Image

```bash
docker image inspect nginx
```

---

### View Image History

```bash
docker history nginx
```

---

# ⚖️ Image vs Container

| Docker Image                 | Docker Container             |
| ---------------------------- | ---------------------------- |
| Read-only template           | Running instance of an image |
| Cannot execute               | Executes the application     |
| Static                       | Dynamic                      |
| Created using `docker build` | Created using `docker run`   |

---

# ☁️ DevOps Perspective

Docker Images are central to every DevOps workflow.

They are used for:

* CI/CD pipelines
* Kubernetes deployments
* Microservices
* Cloud deployments
* Application versioning
* Rollbacks
* Immutable infrastructure

Best practices include:

* Use official base images
* Keep images lightweight
* Tag images with versions
* Avoid storing secrets inside images

---

# 🏭 Production Example

A company develops an e-commerce application.

Pipeline:

1. Developer writes a Dockerfile.
2. CI server builds the Docker Image.
3. Image is tagged as `ecommerce:v1.2`.
4. Image is pushed to Docker Hub or a private registry.
5. Production servers pull the image.
6. Containers are started from the same image.

Because every environment uses the same image, deployments remain consistent and reliable.

---

# 🎯 Common Interview Questions

### What is a Docker Image?

A Docker Image is a read-only template used to create Docker Containers.

---

### Can you modify a Docker Image?

No. Images are immutable. To make changes, build a new image.

---

### What command builds an image?

```bash
docker build -t myapp:v1 .
```

---

### What command lists Docker Images?

```bash
docker images
```

---

### What command downloads an image?

```bash
docker pull nginx
```

---

### Why are Docker Images layered?

Layering improves caching, reduces storage usage, and speeds up image builds.

---

# 🔍 Useful Commands

```bash
docker images

docker pull

docker build

docker rmi

docker image inspect

docker history

docker tag

docker push
```

---

# 📑 Interview Cheat Sheet

```text
Dockerfile
     │
docker build
     │
Docker Image
     │
docker push
     │
Docker Registry
     │
docker pull
     │
docker run
     │
Docker Container
```

Remember:

* Images are templates.
* Containers are running instances.
* Images are immutable.
* Dockerfile creates images.
* Images consist of multiple layers.
* Use tags for version control.

---

# 📚 Summary

Docker Images are the foundation of containerization. They package applications with all required dependencies into portable, immutable templates that can run consistently across any environment. Layered architecture enables efficient storage, faster builds, and simplified version management.

For DevOps Engineers, understanding Docker Images is essential because every container deployment, CI/CD pipeline, and Kubernetes workload begins with a well-designed Docker Image.

---

# 🔗 Related Topics

⬅️ **Previous:** Installation → `../03-Installation/README.md`

➡️ **Next:** Containers → `../05-Containers/README.md`

### 📖 Recommended Reading

* Docker Containers
* Dockerfile
* Docker Registry
* Multi-Stage Builds
* Docker Official Documentation
