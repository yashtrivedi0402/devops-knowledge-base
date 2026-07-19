# 🛠️ Linux Troubleshooting

> **Linux Troubleshooting is the process of identifying, analyzing, and resolving issues affecting a Linux system, application, or service.**
>
> It involves checking logs, system resources, services, networking, storage, and configurations to find the root cause and restore normal operation.

---

# 📖 Table of Contents

* What is Troubleshooting?
* Why Do We Need It?
* Troubleshooting Workflow
* Common Linux Issues
* Service Troubleshooting
* Resource Troubleshooting
* Network Troubleshooting
* Storage Troubleshooting
* Log Analysis
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Troubleshooting?

Troubleshooting is the systematic process of finding and fixing problems in a Linux system.

It helps identify issues related to:

* Services
* Applications
* Network
* Storage
* CPU & Memory
* Permissions
* Configuration

---

# 🎯 Why Do We Need Troubleshooting?

Troubleshooting helps to:

* Restore failed services
* Reduce downtime
* Improve performance
* Identify root causes
* Prevent recurring issues
* Maintain production systems

---

# 🏗️ Troubleshooting Workflow

```text
Issue Reported
      │
      ▼
Identify Problem
      │
      ▼
Check Logs
      │
      ▼
Verify Services
      │
      ▼
Check CPU / Memory / Disk
      │
      ▼
Check Network
      │
      ▼
Fix Issue
      │
      ▼
Verify Solution
```

---

# 🚨 Common Linux Issues

* Service not starting
* Website not accessible
* Permission denied
* Disk full
* High CPU usage
* High Memory usage
* SSH connection failure
* DNS issues
* Network connectivity problems

---

# ⚙️ Service Troubleshooting

Check service status:

```bash
systemctl status nginx
```

Restart service:

```bash
sudo systemctl restart nginx
```

Check failed services:

```bash
systemctl --failed
```

---

# 📊 Resource Troubleshooting

CPU usage:

```bash
top
```

Memory usage:

```bash
free -h
```

Disk usage:

```bash
df -h
```

Directory size:

```bash
du -sh /var/*
```

---

# 🌐 Network Troubleshooting

Check IP address:

```bash
ip addr
```

Check routing:

```bash
ip route
```

Test connectivity:

```bash
ping google.com
```

Check listening ports:

```bash
ss -tuln
```

Verify DNS:

```bash
nslookup google.com
```

---

# 💽 Storage Troubleshooting

Display block devices:

```bash
lsblk
```

Check mounted filesystems:

```bash
mount
```

Check filesystem UUID:

```bash
blkid
```

Persistent mounts:

```bash
cat /etc/fstab
```

---

# 📜 Log Analysis

View system logs:

```bash
journalctl
```

View service logs:

```bash
journalctl -u nginx
```

Follow logs:

```bash
tail -f /var/log/syslog
```

Search logs:

```bash
grep "ERROR" /var/log/syslog
```

---

# ☁️ DevOps Perspective

Troubleshooting is a daily responsibility for DevOps Engineers.

Common tasks include:

* Investigating production incidents
* Debugging failed deployments
* Resolving application crashes
* Monitoring server health
* Identifying performance bottlenecks
* Restoring service availability

---

# 🏭 Production Example

Users report that a website is down.

Investigation:

Check the service:

```bash
systemctl status nginx
```

View logs:

```bash
journalctl -u nginx
```

Check if the port is listening:

```bash
ss -tuln
```

Verify disk space:

```bash
df -h
```

Test locally:

```bash
curl localhost
```

The investigation shows that the disk is full, preventing NGINX from writing logs. After cleaning unnecessary files and restarting the service, the website becomes accessible again.

---

# 🎯 Common Interview Questions

### What is the first step in troubleshooting?

Understand the problem and collect information before making changes.

---

### Which command checks service status?

```bash
systemctl status <service>
```

---

### Which command shows real-time resource usage?

```bash
top
```

---

### Which command checks disk usage?

```bash
df -h
```

---

### Which command checks memory usage?

```bash
free -h
```

---

### Which command views service logs?

```bash
journalctl -u <service>
```

---

### Which command checks listening ports?

```bash
ss -tuln
```

---

# 🔍 Useful Commands

```bash
systemctl status

journalctl

top

htop

free -h

df -h

du -sh

ip addr

ip route

ping

ss -tuln

curl

lsblk

mount

grep
```

---

# 📑 Interview Cheat Sheet

```text
Problem
   │
   ▼
Check Service
   │
   ▼
Check Logs
   │
   ▼
Check CPU / RAM / Disk
   │
   ▼
Check Network
   │
   ▼
Find Root Cause
   │
   ▼
Fix & Verify
```

Remember:

* Don't restart blindly—identify the root cause first.
* Check logs before making changes.
* Verify CPU, memory, disk, and network health.
* Test the application after applying the fix.
* Document the issue and its resolution to prevent recurrence.

---

# 📚 Summary

Linux Troubleshooting is a structured approach to diagnosing and resolving system, application, and infrastructure issues. By analyzing logs, monitoring resources, checking services, and verifying network connectivity, administrators can quickly identify the root cause of problems.

For DevOps Engineers, troubleshooting is one of the most critical skills, enabling faster incident resolution, improved system reliability, and reduced production downtime.

---

# 🔗 Related Topics

⬅️ **Previous:** Important Commands → `../16-Important-Commands/README.md`

➡️ **Next:** End-to-End Linux Flow → `../18-End-to-End-Linux-Flow/README.md`

### 📖 Recommended Reading

* End-to-End Linux Flow
* Logs & Monitoring
* Systemd & Systemctl
* Linux Networking
* Shell Scripting Basics
