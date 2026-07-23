# 🚀 Multi-Stage Builds

> **Multi-Stage Builds are a Docker feature that allows multiple build stages within a single Dockerfile, enabling you to separate the build environment from the runtime environment.**
>
> This helps create **smaller, faster, and more secure Docker images** by including only the files required to run the application.

---

# 📖 Table of Contents

* What are Multi-Stage Builds?
* Why Do We Need Multi-Stage Builds?
* Multi-Stage Build Architecture
* How Multi-Stage Builds Work
* Sample Dockerfile
* Benefits
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Multi-Stage Builds?

A **Multi-Stage Build** is a Docker build technique where a Dockerfile contains **multiple `FROM` instructions**.

Each `FROM` starts a new build stage.

Typically:

* **Stage 1:** Build the application.
* **Stage 2:** Copy only the compiled application into a lightweight runtime image.

This removes unnecessary build tools, source code, and temporary files from the final image.

---

# 🎯 Why Do We Need Multi-Stage Builds?

In a traditional Dockerfile:

* Build tools remain in the final image.
* Image size becomes large.
* More packages increase the attack surface.
* Deployment becomes slower.

With Multi-Stage Builds:

* Smaller images
* Faster deployments
* Better security
* Cleaner Dockerfiles
* Reduced storage usage

---

# 🏗️ Multi-Stage Build Architecture

```text
        Source Code
             │
             ▼
     Stage 1 (Builder)
 ┌─────────────────────┐
 │ Maven / Gradle      │
 │ Node.js             │
 │ Go Compiler         │
 │ Build Dependencies  │
 └─────────────────────┘
             │
        Build Artifact
             │
   COPY --from=builder
             ▼
     Stage 2 (Runtime)
 ┌─────────────────────┐
 │ Lightweight Image   │
 │ Java Runtime        │
 │ Nginx               │
 │ Alpine Linux        │
 └─────────────────────┘
             │
             ▼
     Production Container
```

---

# 🔄 How Multi-Stage Builds Work

A Multi-Stage Dockerfile consists of:

1. A **builder stage** that compiles the application.
2. A **runtime stage** that contains only the necessary output.

Docker copies only the required files from the builder stage into the final image.

This keeps the production image clean and lightweight.

---

# 📝 Sample Dockerfile

```dockerfile
# Stage 1 - Build
FROM maven:3.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY . .

RUN mvn clean package

# Stage 2 - Runtime
FROM eclipse-temurin:21-jre

WORKDIR /app

COPY --from=builder /app/target/app.jar app.jar

EXPOSE 8080

CMD ["java","-jar","app.jar"]
```

In this example:

* Maven is available only during the build stage.
* The final image contains only the JRE and the application JAR.
* Source code and build tools are excluded.

---

# ⭐ Benefits

* Smaller image size
* Faster image downloads
* Reduced attack surface
* Lower storage consumption
* Faster CI/CD pipelines
* Cleaner production environment
* Easier maintenance

---

# ☁️ DevOps Perspective

Multi-Stage Builds are widely used for:

* Java (Maven/Gradle)
* Node.js Applications
* Go Applications
* .NET Applications
* React/Angular Builds
* CI/CD Pipelines
* Kubernetes Deployments

Best Practices:

* Use minimal runtime images (e.g., Alpine or slim variants).
* Copy only required artifacts to the final stage.
* Keep build and runtime environments separate.
* Name stages using `AS` for readability.
* Remove unnecessary files from runtime images.

---

# 🏭 Production Example

A company develops a Spring Boot application.

Pipeline:

1. Developer pushes code to GitHub.
2. Jenkins starts the pipeline.
3. Docker builds the application using Maven in the builder stage.
4. The generated JAR is copied into a lightweight Java runtime image.
5. The final image is pushed to Amazon ECR.
6. Kubernetes deploys the optimized image.

Benefits:

* Final image size reduced from **850 MB** to **220 MB**.
* Faster deployments.
* Lower bandwidth usage.
* Improved container startup time.

---

# 🎯 Common Interview Questions

### What is a Multi-Stage Build?

A Multi-Stage Build is a Docker feature that uses multiple `FROM` statements to separate the build environment from the runtime environment.

---

### Why are Multi-Stage Builds used?

To create smaller, faster, and more secure Docker images by excluding unnecessary build dependencies from the final image.

---

### What does `COPY --from=builder` do?

It copies files from a previous build stage into the current stage.

---

### Can a Dockerfile have multiple `FROM` instructions?

Yes. Each `FROM` instruction creates a new build stage.

---

### Which applications commonly use Multi-Stage Builds?

* Java
* Node.js
* Go
* .NET
* React
* Angular

---

# 🔍 Useful Commands

```bash
docker build

docker images

docker history

docker image inspect

docker image prune

docker push

docker pull
```

---

# 📑 Interview Cheat Sheet

```text
Source Code
      │
      ▼
Builder Stage
(Maven / Node / Go)
      │
Build Artifact
      │
COPY --from
      ▼
Runtime Stage
(JRE / Nginx / Alpine)
      │
      ▼
Small Production Image
```

Remember:

* Multiple `FROM` instructions create multiple stages.
* `COPY --from` transfers build artifacts.
* Build tools stay in the builder stage.
* Runtime images should contain only what is necessary.
* Multi-Stage Builds improve security, performance, and image size.

---

# 📚 Summary

Multi-Stage Builds enable Docker to separate the application build process from the runtime environment, producing lightweight and production-ready images. By excluding unnecessary dependencies and build tools, they improve performance, security, and maintainability.

For DevOps Engineers, Multi-Stage Builds are considered a best practice for containerizing applications and are commonly used in CI/CD pipelines, Kubernetes deployments, and cloud-native architectures.

---

# 🔗 Related Topics

⬅️ **Previous:** Registry → `../10-Registry/README.md`

➡️ **Next:** Best Practices → `../12-Best-Practices/README.md`

### 📖 Recommended Reading

* Dockerfile
* Docker Registry
* Docker Compose
* CI/CD Pipelines
* Docker Official Documentation
