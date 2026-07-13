# 🔍 Network Troubleshooting Guide for DevOps Engineers

> **Troubleshooting is one of the most important skills for a DevOps Engineer.**
>
> In production, nobody pays you for memorizing networking concepts—they pay you for **finding and fixing problems quickly**.
>
> A senior DevOps Engineer never guesses. They troubleshoot **layer by layer**, eliminating possibilities until the root cause is identified.

---

# 📖 Table of Contents

* What is Network Troubleshooting?
* Why Do We Need It?
* Troubleshooting Mindset
* Layer-by-Layer Troubleshooting
* Common Networking Problems
* Troubleshooting Flowchart
* Essential Linux Commands
* AWS Network Troubleshooting
* Kubernetes Network Troubleshooting
* Docker Network Troubleshooting
* Production Scenarios
* Real Interview Scenarios
* Senior Engineer Tips
* Common Interview Questions
* Common Mistakes
* Troubleshooting Cheat Sheet
* Summary
* Related Topics

---

# ❓ What is Network Troubleshooting?

Network Troubleshooting is the systematic process of identifying, isolating, and resolving network-related problems.

Instead of randomly changing configurations,

a DevOps Engineer investigates each networking layer until the root cause is found.

---

# 🎯 Why Do We Need It?

Suppose your users report:

* Website is down
* SSH is not working
* API timeout
* Kubernetes Pods cannot communicate
* Docker containers cannot pull images

Jumping directly to conclusions often wastes time.

Instead,

follow a structured troubleshooting approach.

---

# 🧠 Troubleshooting Mindset

A professional DevOps Engineer always asks:

* Is the problem DNS?
* Is the problem routing?
* Is the port blocked?
* Is TLS failing?
* Is the application running?
* Is the database reachable?

Never assume.

Verify.

---

# 🏗️ Layer-by-Layer Troubleshooting

Always troubleshoot in this order:

```text
Application

↓

HTTP / HTTPS

↓

TLS

↓

TCP / UDP

↓

DNS

↓

Routing

↓

Security Groups

↓

Network ACL

↓

Internet Gateway / NAT Gateway

↓

Operating System

↓

Hardware
```

This prevents random debugging.

---

# 🌐 Complete Troubleshooting Flow

```text
User

↓

Browser

↓

DNS

↓

TCP Connection

↓

TLS Handshake

↓

HTTP Request

↓

Load Balancer

↓

Application

↓

Database
```

If something fails,

identify exactly which stage is failing.

---

# ⚠️ Common Networking Problems

| Problem               | Possible Cause          |
| --------------------- | ----------------------- |
| Website not loading   | DNS Failure             |
| Connection Timeout    | Route Table / Firewall  |
| Connection Refused    | Application not running |
| SSL Error             | Invalid Certificate     |
| SSH Timeout           | Security Group          |
| Slow Website          | High Latency / CPU      |
| Pod Cannot Pull Image | NAT Gateway             |
| API Returns 502       | Load Balancer / Backend |

---

# 🔍 Troubleshooting Flowchart

Whenever someone says:

> "The application isn't working."

Follow this sequence.

---

## Step 1 — Is DNS Working?

Commands

```bash
nslookup example.com

dig example.com

host example.com
```

If DNS fails,

nothing else matters.

---

## Step 2 — Can We Reach the Server?

```bash
ping <IP>
```

or

```bash
traceroute <IP>
```

If packets never reach,

check:

* Route Table
* Internet Gateway
* NAT Gateway

---

## Step 3 — Is the Port Open?

```bash
nc -zv server 80

nc -zv server 443

telnet server 443
```

If closed,

check:

* Security Groups
* NACL
* Firewall

---

## Step 4 — Is the Application Listening?

```bash
ss -tulnp

netstat -tulnp
```

Verify:

* Correct Port
* Running Process

---

## Step 5 — Is HTTPS Working?

```bash
curl -Iv https://example.com
```

```bash
openssl s_client -connect example.com:443
```

Check:

* Certificate
* Expiry
* Hostname

---

## Step 6 — Is the Application Healthy?

```bash
curl http://localhost:8080/health
```

or

```bash
curl http://localhost:8080/actuator/health
```

---

## Step 7 — Check Logs

Linux

```bash
journalctl

tail -f

cat
```

Docker

```bash
docker logs
```

Kubernetes

```bash
kubectl logs
```

---

# 💻 Essential Linux Commands

## Network Information

```bash
ip addr
```

```bash
hostname -I
```

```bash
ip route
```

---

## Connectivity

```bash
ping
```

```bash
traceroute
```

```bash
tracepath
```

---

## DNS

```bash
nslookup
```

```bash
dig
```

```bash
host
```

---

## Ports

```bash
ss -tulnp
```

```bash
netstat -tulnp
```

---

## HTTP

```bash
curl
```

```bash
wget
```

---

## Process

```bash
ps -ef
```

```bash
top
```

---

# ☁️ AWS Network Troubleshooting

Check in this order:

✅ Route Table

↓

✅ Internet Gateway

↓

✅ NAT Gateway

↓

✅ Security Group

↓

✅ Network ACL

↓

✅ Target Group

↓

✅ EC2

↓

✅ Application

Never begin with the application.

Networking failures are often the root cause.

---

# ☸️ Kubernetes Network Troubleshooting

Common commands

```bash
kubectl get pods -o wide
```

```bash
kubectl get svc
```

```bash
kubectl get ingress
```

```bash
kubectl describe pod
```

```bash
kubectl logs
```

Check:

* Pod IP
* Service
* Ingress
* CoreDNS
* Network Policies

---

# 🐳 Docker Network Troubleshooting

Commands

```bash
docker ps
```

```bash
docker network ls
```

```bash
docker network inspect bridge
```

```bash
docker inspect <container>
```

Check:

* Bridge Network
* Port Mapping
* DNS
* Container IP

---

# 🏭 Production Scenarios

## Scenario 1

Users cannot access your website.

Checklist

* DNS
* Load Balancer
* Security Group
* Target Group
* Application

---

## Scenario 2

SSH timeout

Check

* Public IP
* Internet Gateway
* Route Table
* Security Group
* SSH Service

---

## Scenario 3

Kubernetes Pod cannot pull image

Check

* NAT Gateway
* Route Table
* Internet Gateway
* DNS
* IAM Role

---

## Scenario 4

Database Connection Failed

Check

* Security Group
* Database Port
* Database Running
* Application Config
* Route Table

---

## Scenario 5

502 Bad Gateway

Check

* Target Group
* Backend Service
* Application Logs
* Health Checks

---

# 🎯 Real Interview Scenarios

## Scenario 1

EC2 cannot access the Internet.

Possible causes:

* Missing Internet Gateway
* Wrong Route Table
* Missing Public IP
* Security Group
* NACL

---

## Scenario 2

Private EC2 cannot pull Docker images.

Possible causes:

* NAT Gateway Missing
* Wrong Route Table
* DNS Failure
* Security Group

---

## Scenario 3

Application works locally but not through ALB.

Possible causes:

* Target Group
* Health Checks
* Security Group
* Listener Rules

---

## Scenario 4

SSH works but HTTPS doesn't.

Possible causes:

* Port 443 blocked
* Web Server stopped
* TLS Certificate expired

---

# 🧠 Senior Engineer Tips

Always troubleshoot from **outside → inside**.

```text
Internet

↓

DNS

↓

Load Balancer

↓

Security Groups

↓

EC2

↓

Application

↓

Database
```

Never jump directly to the application.

---

Use logs to confirm assumptions.

Don't guess.

Verify.

---

# 💼 Common Interview Questions

### Q1.

How would you troubleshoot if a website is not opening?

Walk through:

DNS → Routing → Security → Application

---

### Q2.

How would you troubleshoot SSH timeout?

Check:

* Public IP
* Route Table
* Security Group
* SSH Service

---

### Q3.

Pod cannot pull Docker image.

Check:

* NAT Gateway
* Route Table
* DNS
* IAM

---

### Q4.

How do you troubleshoot HTTPS failure?

Check:

* Certificate
* TLS
* Port 443
* Load Balancer

---

### Q5.

What is your troubleshooting approach?

Always isolate the failing layer before making changes.

---

# 🔥 Common Mistakes

❌ Restarting services immediately.

✅ Diagnose first.

---

❌ Ignoring logs.

✅ Logs often contain the exact error.

---

❌ Assuming DNS is working.

✅ Verify with `dig` or `nslookup`.

---

❌ Checking Security Groups before confirming routing.

✅ Follow a structured order.

---

❌ Changing multiple configurations simultaneously.

✅ Make one change at a time.

---

# 💼 Troubleshooting Cheat Sheet

Remember this order:

```text
1️⃣ DNS

↓

2️⃣ Routing

↓

3️⃣ Security Groups

↓

4️⃣ Network ACL

↓

5️⃣ Internet Gateway / NAT Gateway

↓

6️⃣ Port

↓

7️⃣ TLS

↓

8️⃣ Application

↓

9️⃣ Database
```

Useful Commands

```bash
ping
traceroute
dig
nslookup
curl
ss -tulnp
ip route
docker logs
kubectl logs
journalctl
```

---

# 📚 Summary

Successful DevOps Engineers don't fix problems by trial and error.

They follow a systematic troubleshooting process, verifying each layer of the network stack before moving to the next.

Mastering this approach allows you to solve production incidents quickly, reduce downtime, and build reliable cloud infrastructure.

---

# 🔗 Related Topics

⬅️ Previous: **Load Balancers** → `../12-Load-Balancers/README.md`


### 📖 Next Recommended Learning Path

* Linux
* Git & GitHub
* Docker
* Kubernetes
* AWS
* Terraform
* Jenkins
* Ansible
* Monitoring (Prometheus & Grafana)
* CI/CD Pipelines
