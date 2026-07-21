# ⚙️ Docker Installation

> **Docker Installation is the process of setting up the Docker Engine, Docker CLI, and related components on an operating system so you can build, run, and manage containers.**
>
> Installing Docker correctly is the first step toward containerizing applications and building modern DevOps workflows.

---

# 📖 Table of Contents

* What is Docker Installation?
* Why Do We Need Docker?
* Prerequisites
* Installing Docker on Ubuntu
* Verify Installation
* First Docker Container
* Docker Service Management
* Docker Without Sudo
* DevOps Perspective
* Production Example
* Interview Questions
* Summary
* Related Topics

---

# ❓ What is Docker Installation?

Docker Installation involves setting up:

* Docker Engine
* Docker CLI
* Docker Daemon (`dockerd`)
* Docker Runtime

Once installed, Docker allows you to:

* Build Images
* Run Containers
* Pull Images
* Push Images
* Manage Networks
* Manage Volumes

---

# 🎯 Why Do We Need Docker?

Installing Docker enables developers and DevOps engineers to:

* Run applications consistently
* Build containerized applications
* Test locally before deployment
* Deploy applications quickly
* Build CI/CD pipelines
* Run Kubernetes workloads

---

# 📋 Prerequisites

Before installing Docker:

* Ubuntu 20.04 or later (recommended)
* 64-bit Operating System
* Internet Connection
* User with `sudo` privileges

Check Ubuntu version:

```bash
lsb_release -a
```

Check architecture:

```bash
uname -m
```

---

# 🐧 Installing Docker on Ubuntu

## Step 1: Update Package Index

```bash
sudo apt update
```

---

## Step 2: Install Required Packages

```bash
sudo apt install -y ca-certificates curl gnupg
```

---

## Step 3: Add Docker's Official GPG Key

```bash
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

---

## Step 4: Add Docker Repository

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## Step 5: Update Packages Again

```bash
sudo apt update
```

---

## Step 6: Install Docker

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

# ✅ Verify Installation

Check Docker version:

```bash
docker --version
```

Example output:

```text
Docker version 28.x.x
```

Check Docker information:

```bash
docker info
```

---

# 🚀 Run Your First Docker Container

Run the official Hello World container:

```bash
sudo docker run hello-world
```

Expected output:

```text
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

---

# ⚙️ Docker Service Management

Check Docker status:

```bash
sudo systemctl status docker
```

Start Docker:

```bash
sudo systemctl start docker
```

Stop Docker:

```bash
sudo systemctl stop docker
```

Restart Docker:

```bash
sudo systemctl restart docker
```

Enable Docker at boot:

```bash
sudo systemctl enable docker
```

---

# 👤 Run Docker Without sudo

Add your user to the Docker group:

```bash
sudo usermod -aG docker $USER
```

Apply the new group membership:

```bash
newgrp docker
```

Verify:

```bash
docker run hello-world
```

Now Docker commands can be executed without `sudo`.

---

# ☁️ DevOps Perspective

Docker installation is one of the first tasks performed when preparing:

* CI/CD servers
* Development machines
* Cloud virtual machines
* Kubernetes worker nodes
* Build servers

A correctly installed Docker environment forms the foundation for containerized application deployment.

---

# 🏭 Production Example

A DevOps engineer launches a new Ubuntu EC2 instance.

The typical setup process is:

1. Update the operating system.
2. Install Docker.
3. Enable the Docker service.
4. Add the deployment user to the Docker group.
5. Pull the required application image.
6. Start the application container.

This prepares the server for application deployment.

---

# 🎯 Common Interview Questions

### How do you check if Docker is installed?

```bash
docker --version
```

---

### Which command starts the Docker service?

```bash
sudo systemctl start docker
```

---

### How do you check Docker service status?

```bash
sudo systemctl status docker
```

---

### Which command runs the Docker test container?

```bash
docker run hello-world
```

---

### How can you use Docker without sudo?

Add the user to the Docker group:

```bash
sudo usermod -aG docker $USER
```

---

# 📑 Interview Cheat Sheet

```text
Install Docker
      │
      ▼
Start Docker Service
      │
      ▼
Verify Installation
      │
      ▼
Run hello-world
      │
      ▼
Docker Ready
```

Remember:

* `docker --version` → Docker version
* `docker info` → Docker information
* `docker run hello-world` → Test installation
* `systemctl status docker` → Service status
* `systemctl enable docker` → Start Docker on boot
* `usermod -aG docker $USER` → Run Docker without sudo

---

# 📚 Summary

Installing Docker involves setting up the Docker Engine, CLI, and supporting components required to build and run containers. After installation, verifying the service and running the `hello-world` container confirms that Docker is working correctly.

For DevOps Engineers, Docker installation is a fundamental setup task performed on local machines, cloud instances, and CI/CD servers before deploying containerized applications.

---

# 🔗 Related Topics

⬅️ **Previous:** Docker Architecture → `../02-Docker-Architecture/README.md`

➡️ **Next:** Images → `../04-Images/README.md`

### 📖 Recommended Reading

* Docker Images
* Docker Containers
* Dockerfile
* Docker Official Documentation
