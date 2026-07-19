# ⚙️ Linux Processes & Services

> **A Process is a running instance of a program, while a Service is a background process that provides functionality to the system or other applications.**
>
> Every application you run creates one or more processes. Services (also called daemons) keep essential system functions running, such as web servers, databases, SSH, and scheduling tasks.

---

# 📖 Table of Contents

* What are Processes & Services?
* Why Do We Need Them?
* Process Lifecycle
* Process States
* Foreground vs Background
* Process Hierarchy
* Daemons (Services)
* Process Management
* Service Management
* Signals
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Process?

A **Process** is a program that is currently running.

Examples:

* Chrome
* NGINX
* MySQL
* Jenkins
* Python Script

Every process has:

* Process ID (PID)
* Parent Process ID (PPID)
* User
* Memory Allocation
* CPU Usage
* State

---

# ❓ What is a Service?

A **Service (Daemon)** is a background process that starts automatically or manually to perform specific tasks.

Examples:

* SSH (`sshd`)
* NGINX
* MySQL
* Docker
* Jenkins

Services usually continue running even when no user is logged in.

---

# 🎯 Why Do We Need Processes & Services?

They allow Linux to:

* Run multiple applications simultaneously
* Execute tasks independently
* Provide background services
* Manage system resources
* Improve multitasking

---

# 🔄 Process Lifecycle

```text
Program
   │
   ▼
Created
   │
   ▼
Running
   │
   ▼
Waiting / Sleeping
   │
   ▼
Running Again
   │
   ▼
Terminated
```

Every process follows this lifecycle from creation to termination.

---

# 📊 Process States

| State | Description           |
| ----- | --------------------- |
| R     | Running               |
| S     | Sleeping              |
| D     | Uninterruptible Sleep |
| T     | Stopped               |
| Z     | Zombie Process        |

---

# 💻 Foreground vs Background

### Foreground Process

Runs directly in the terminal.

Example:

```bash
python app.py
```

---

### Background Process

Runs independently without occupying the terminal.

Example:

```bash
python app.py &
```

---

# 🌳 Process Hierarchy

Every process is created by another process.

```text
systemd (PID 1)
│
├── sshd
│
├── nginx
│
├── docker
│
└── mysql
```

* **PID** → Process ID
* **PPID** → Parent Process ID

---

# ⚙️ Daemons (Services)

A **Daemon** is a background service that waits for requests and performs tasks automatically.

Examples:

| Service | Purpose          |
| ------- | ---------------- |
| sshd    | Remote Login     |
| nginx   | Web Server       |
| mysqld  | Database         |
| docker  | Container Engine |
| cron    | Scheduled Jobs   |

---

# 🛠️ Process Management

## View Running Processes

```bash
ps
```

Detailed view:

```bash
ps -ef
```

Interactive view:

```bash
top
```

or

```bash
htop
```

---

## Find a Process

```bash
pgrep nginx
```

or

```bash
pidof nginx
```

---

## Kill a Process

Gracefully stop:

```bash
kill PID
```

Force stop:

```bash
kill -9 PID
```

---

# 🚀 Service Management

Most Linux distributions use **systemd** to manage services.

Check status:

```bash
systemctl status nginx
```

Start:

```bash
systemctl start nginx
```

Stop:

```bash
systemctl stop nginx
```

Restart:

```bash
systemctl restart nginx
```

Enable at boot:

```bash
systemctl enable nginx
```

Disable:

```bash
systemctl disable nginx
```

---

# 📡 Signals

Signals are used to communicate with processes.

| Signal       | Purpose                |
| ------------ | ---------------------- |
| SIGTERM (15) | Gracefully stop        |
| SIGKILL (9)  | Force kill             |
| SIGHUP (1)   | Reload configuration   |
| SIGINT (2)   | Interrupt (`Ctrl + C`) |

---

# ☁️ DevOps Perspective

Processes and services are monitored continuously in production.

Examples:

* Ensure NGINX is running
* Restart failed services
* Monitor CPU and memory usage
* Kill hung processes
* Check application health

---

# 🏭 Production Example

A website becomes inaccessible.

Investigation:

```bash
systemctl status nginx
```

If stopped:

```bash
sudo systemctl restart nginx
```

Check logs:

```bash
journalctl -u nginx
```

Verify process:

```bash
ps -ef | grep nginx
```

Website is restored.

---

# 🎯 Common Interview Questions

### What is a Process?

A running instance of a program.

---

### What is a PID?

A unique Process ID assigned by Linux.

---

### Difference between Process and Service?

* **Process** → Any running program.
* **Service** → A background process managed by the system.

---

### What is a Zombie Process?

A terminated process whose parent hasn't collected its exit status.

---

### What is PID 1?

`systemd` (or `init` on older systems), the first process started during boot.

---

### Difference between `kill` and `kill -9`?

* `kill` sends **SIGTERM**, allowing graceful shutdown.
* `kill -9` sends **SIGKILL**, immediately terminating the process.

---

# 🔍 Useful Commands

```bash
ps

ps -ef

top

htop

pstree

pgrep

pidof

kill

killall

systemctl

journalctl
```

---

# 📑 Interview Cheat Sheet

```text
Program
   │
   ▼
Process (PID)
   │
   ▼
Running / Sleeping
   │
   ▼
Service (Daemon)
   │
   ▼
Managed by systemd
```

Remember:

* Process = Running program
* Service = Background process
* PID = Process ID
* PPID = Parent Process ID
* PID 1 = systemd
* `kill` = Graceful stop
* `kill -9` = Force stop
* `systemctl` = Service management

---

# 📚 Summary

A **Process** is a running instance of a program, while a **Service** is a long-running background process that provides system functionality. Linux manages processes using PIDs, process states, and signals, while services are typically managed by **systemd**.

For DevOps Engineers, understanding processes and services is essential for monitoring applications, troubleshooting failures, managing resources, and ensuring production systems remain healthy and available.

---

# 🔗 Related Topics

⬅️ **Previous:** File Permissions → `../06-File-Permissions/README.md`

➡️ **Next:** Systemd & Systemctl → `../08-Systemd-and-Systemctl/README.md`

### 📖 Recommended Reading

* Systemd & Systemctl
* Logs & Monitoring
* SSH & Remote Access
* Linux Troubleshooting
* Networking in Linux
