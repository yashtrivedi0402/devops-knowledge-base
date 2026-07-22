# 📝 Dockerfile

> **A Dockerfile is a text file that contains a set of instructions used by Docker to automatically build a Docker Image.**
>
> Instead of manually configuring containers, a Dockerfile defines the entire application environment in code, making builds repeatable, consistent, and version-controlled.

---

# 📖 Table of Contents

* What is a Dockerfile?
* Why Do We Need a Dockerfile?
* Dockerfile Architecture
* Common Dockerfile Instructions
* Sample Dockerfile
* Building an Image
* Dockerfile Best Practices
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Dockerfile?

A **Dockerfile** is a plain text file that contains instructions for creating a Docker Image.

Docker reads these instructions one by one and builds the image layer by layer.

A Dockerfile defines:

* Base Image
* Application Code
* Dependencies
* Environment Variables
* Startup Command

---

# 🎯 Why Do We Need a Dockerfile?

Without a Dockerfile:

* Applications are configured manually.
* Builds become inconsistent.
* Deployments are difficult to reproduce.
* Scaling becomes harder.

With a Dockerfile:

* Builds are automated.
* Images are version-controlled.
* Deployments are consistent.
* CI/CD pipelines become easier to implement.

---

# 🏗️ Dockerfile Architecture

```text
Application Source Code
          │
          ▼
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

# 📚 Common Dockerfile Instructions

| Instruction  | Purpose                                            |
| ------------ | -------------------------------------------------- |
| `FROM`       | Specifies the base image                           |
| `WORKDIR`    | Sets the working directory                         |
| `COPY`       | Copies files into the image                        |
| `ADD`        | Copies files and supports URLs/archives            |
| `RUN`        | Executes commands during image build               |
| `ENV`        | Sets environment variables                         |
| `EXPOSE`     | Documents the application's listening port         |
| `CMD`        | Default command executed when the container starts |
| `ENTRYPOINT` | Defines the main executable for the container      |

---

# 🧱 Sample Dockerfile

Example:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

What happens?

1. Pulls the Python base image.
2. Creates `/app` as the working directory.
3. Copies application files.
4. Installs dependencies.
5. Exposes port **5000**.
6. Starts the application.

---

# 🔄 Building an Image

Build an image from a Dockerfile:

```bash
docker build -t myapp:v1 .
```

List images:

```bash
docker images
```

Run the image:

```bash
docker run -d -p 5000:5000 myapp:v1
```

---

# ⭐ Dockerfile Best Practices

* Use official base images.
* Keep images as small as possible.
* Combine commands to reduce image layers where appropriate.
* Use `.dockerignore` to exclude unnecessary files.
* Use **Multi-Stage Builds** for production images.
* Avoid storing secrets inside the Dockerfile.
* Pin image versions instead of always using `latest`.

---

# ☁️ DevOps Perspective

Dockerfiles are essential for:

* CI/CD pipelines
* Automated application builds
* Infrastructure as Code
* Kubernetes deployments
* Cloud-native applications
* Version-controlled infrastructure

In most organizations, every application repository includes a Dockerfile.

---

# 🏭 Production Example

A developer pushes code to GitHub.

Pipeline:

1. GitHub Actions/Jenkins detects the commit.
2. Docker builds the image using the Dockerfile.
3. The image is tagged (`v1.0.3`).
4. The image is pushed to Docker Hub or a private registry.
5. Kubernetes or Docker pulls the latest image.
6. New containers are deployed automatically.

This automation is possible because the Dockerfile defines the application environment.

---

# 🎯 Common Interview Questions

### What is a Dockerfile?

A Dockerfile is a text file containing instructions to build a Docker Image automatically.

---

### Which command builds an image?

```bash
docker build -t myapp:v1 .
```

---

### What does `FROM` do?

It specifies the base image used to build the Docker Image.

---

### Difference between `COPY` and `ADD`?

* `COPY` copies local files into the image.
* `ADD` can also download files from URLs and automatically extract local archives.

---

### Difference between `CMD` and `ENTRYPOINT`?

* `CMD` provides the default command and can be overridden.
* `ENTRYPOINT` defines the main executable and is generally not overridden.

---

### Why is `WORKDIR` used?

It sets the default working directory for all subsequent Dockerfile instructions.

---

# 🔍 Useful Commands

```bash
docker build

docker images

docker run

docker history

docker image inspect

docker tag

docker push
```

---

# 📑 Interview Cheat Sheet

```text
Source Code
     │
Dockerfile
     │
docker build
     │
Docker Image
     │
docker run
     │
Container
```

Remember:

* Dockerfile = Recipe
* Image = Blueprint
* Container = Running Instance
* `FROM` = Base Image
* `COPY` = Copy Files
* `RUN` = Execute Build Commands
* `CMD` = Default Startup Command
* `ENTRYPOINT` = Main Executable

---

# 📚 Summary

A Dockerfile is the blueprint for building Docker Images. It automates the process of packaging applications, dependencies, and configurations into portable images that can run consistently across environments.

For DevOps Engineers, Dockerfiles are a critical part of CI/CD pipelines, infrastructure automation, and cloud-native application deployment. Writing optimized Dockerfiles leads to smaller images, faster builds, and more reliable deployments.

---

# 🔗 Related Topics

⬅️ **Previous:** Containers → `../05-Containers/README.md`

➡️ **Next:** Volumes → `../07-Volumes/README.md`

### 📖 Recommended Reading

* Docker Volumes
* Docker Images
* Multi-Stage Builds
* Docker Best Practices
* Docker Official Documentation
