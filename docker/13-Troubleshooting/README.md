# 🛠️ Docker Troubleshooting

> **Docker Troubleshooting is the process of identifying, diagnosing, and resolving issues related to Docker Images, Containers, Networks, Volumes, and the Docker Engine.**
>
> Troubleshooting is one of the most important skills for a DevOps Engineer because real-world production issues often involve container failures, networking problems, storage issues, and deployment errors.

---

# 📖 Table of Contents

* What is Docker Troubleshooting?
* Why is Troubleshooting Important?
* Docker Troubleshooting Workflow
* Common Docker Issues
* Image Troubleshooting
* Container Troubleshooting
* Network Troubleshooting
* Volume Troubleshooting
* Docker Engine Troubleshooting
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Docker Troubleshooting?

Docker Troubleshooting is the process of analyzing Docker-related problems and finding their root cause.

Problems may occur in:

* Docker Images
* Containers
* Dockerfile
* Networks
* Volumes
* Registries
* Docker Engine
* Resource Utilization

A good DevOps Engineer should troubleshoot systematically instead of guessing.

---

# 🎯 Why is Troubleshooting Important?

In production, even a small issue can affect thousands of users.

Examples:

* Container keeps restarting
* Application is inaccessible
* Database data is missing
* Image build fails
* Port conflicts
* High CPU or Memory usage

Troubleshooting minimizes downtime and restores services quickly.

---

# 🏗️ Docker Troubleshooting Workflow

```text
Problem Reported
       │
       ▼
Identify Symptoms
       │
       ▼
Check Container Status
       │
       ▼
Inspect Logs
       │
       ▼
Verify Configuration
       │
       ▼
Find Root Cause
       │
       ▼
Apply Fix
       │
       ▼
Validate Solution
```

---

# 🚨 Common Docker Issues

| Problem                         | Possible Cause                           |
| ------------------------------- | ---------------------------------------- |
| Container exits immediately     | Application process finished or crashed  |
| Port already allocated          | Host port is already in use              |
| Image build fails               | Dockerfile or dependency issue           |
| Cannot pull image               | Registry authentication or network issue |
| Container cannot reach database | Network misconfiguration                 |
| Data lost after restart         | Missing Docker Volume                    |
| High disk usage                 | Unused images, containers, and volumes   |
| Permission denied               | File permission or user issue            |

---

# 🖼️ Image Troubleshooting

### Check Available Images

```bash
docker images
```

---

### View Image History

```bash
docker history <image_name>
```

---

### Inspect an Image

```bash
docker image inspect <image_name>
```

---

### Remove Unused Images

```bash
docker image prune
```

---

### Remove All Unused Docker Resources

```bash
docker system prune
```

---

# 📦 Container Troubleshooting

### Check Running Containers

```bash
docker ps
```

---

### Check All Containers

```bash
docker ps -a
```

---

### View Container Logs

```bash
docker logs <container_name>
```

---

### Follow Logs in Real Time

```bash
docker logs -f <container_name>
```

---

### Enter a Running Container

```bash
docker exec -it <container_name> bash
```

---

### Inspect Container Configuration

```bash
docker inspect <container_name>
```

---

### View Resource Usage

```bash
docker stats
```

---

# 🌐 Network Troubleshooting

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

### Test Network Connectivity

```bash
docker exec -it frontend ping backend
```

---

### Verify Port Mapping

```bash
docker port <container_name>
```

---

### Check Listening Ports

```bash
ss -tuln
```

or

```bash
netstat -tuln
```

---

# 💾 Volume Troubleshooting

### List Volumes

```bash
docker volume ls
```

---

### Inspect a Volume

```bash
docker volume inspect myvolume
```

---

### Verify Mounts

```bash
docker inspect <container_name>
```

Look under:

```text
Mounts
```

---

### Remove Unused Volumes

```bash
docker volume prune
```

---

# ⚙️ Docker Engine Troubleshooting

### Check Docker Version

```bash
docker version
```

---

### Check Docker Information

```bash
docker info
```

---

### Verify Docker Service

```bash
sudo systemctl status docker
```

---

### Restart Docker

```bash
sudo systemctl restart docker
```

---

### Check Docker Logs

```bash
journalctl -u docker
```

---

# ☁️ DevOps Perspective

In production, troubleshooting commonly involves:

* CI/CD pipeline failures
* Image build failures
* Kubernetes Pod issues
* Registry authentication errors
* Docker daemon failures
* Resource exhaustion
* Network connectivity issues

Best Practices:

* Read logs before restarting containers.
* Verify configuration changes.
* Use health checks.
* Monitor CPU, memory, and disk usage.
* Keep Docker updated.
* Avoid deleting resources before identifying the root cause.

---

# 🏭 Production Example

A Spring Boot application is deployed in Docker.

Problem:

```text
Application is inaccessible.
```

Troubleshooting steps:

1. Check running containers.

```bash
docker ps
```

2. View logs.

```bash
docker logs springboot-app
```

3. Verify port mapping.

```bash
docker port springboot-app
```

4. Check Docker network.

```bash
docker network inspect app-network
```

5. Confirm database connectivity.

6. Restart the application only after identifying the root cause.

This structured approach minimizes downtime and avoids unnecessary changes.

---

# 🎯 Common Interview Questions

### Which command shows running containers?

```bash
docker ps
```

---

### Which command displays container logs?

```bash
docker logs <container_name>
```

---

### How do you access a running container?

```bash
docker exec -it <container_name> bash
```

---

### Which command shows Docker resource usage?

```bash
docker stats
```

---

### How do you inspect a container?

```bash
docker inspect <container_name>
```

---

### How do you clean unused Docker resources?

```bash
docker system prune
```

---

### What is the first step in troubleshooting?

Identify the symptoms and collect logs before making changes.

---

# 🔍 Useful Commands

```bash
docker ps

docker ps -a

docker logs

docker exec

docker inspect

docker stats

docker network inspect

docker volume inspect

docker system prune

docker info

docker version
```

---

# 📑 Interview Cheat Sheet

```text
Problem
   │
   ▼
docker ps
   │
   ▼
docker logs
   │
   ▼
docker inspect
   │
   ▼
Network Check
   │
   ▼
Volume Check
   │
   ▼
Docker Service
   │
   ▼
Root Cause
   │
   ▼
Fix
```

Remember:

* Check logs before restarting.
* Use `docker inspect` to verify configuration.
* Monitor CPU, memory, and storage.
* Verify networks and volumes.
* Solve the root cause, not just the symptoms.

---

# 📚 Summary

Docker Troubleshooting is an essential DevOps skill that focuses on diagnosing and resolving issues affecting Docker containers, images, networks, volumes, and the Docker Engine. A structured troubleshooting process helps minimize downtime and maintain reliable application deployments.

For DevOps Engineers, mastering Docker troubleshooting means understanding how to interpret logs, inspect configurations, verify networking and storage, and systematically identify root causes instead of relying on trial and error.

---

# 🔗 Related Topics

⬅️ **Previous:** Best Practices → `../12-Best-Practices/README.md`

➡️ **Next:** End-to-End Docker Flow → `../14-End-to-End-Docker-Flow/README.md`

### 📖 Recommended Reading

* Docker Best Practices
* Docker Networking
* Docker Volumes
* Docker Compose
* Docker Official Documentation
