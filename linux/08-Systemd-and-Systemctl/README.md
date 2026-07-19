# ⚙️ Linux Systemd & Systemctl

> **systemd is the default system and service manager in most modern Linux distributions.** It is responsible for booting the system, managing services (daemons), handling dependencies, logging, and controlling system resources.
>
> **systemctl** is the command-line tool used to interact with systemd.

---

# 📖 Table of Contents

* What is systemd?
* Why Do We Need systemd?
* systemd Architecture
* What is systemctl?
* Units in systemd
* Managing Services
* Boot Targets
* Viewing Logs
* Creating a Service
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is systemd?

**systemd** is the first process started by the Linux kernel after boot.

It has:

* PID = 1
* Starts system services
* Manages background processes
* Handles system startup and shutdown
* Tracks service health
* Maintains service dependencies

---

# 🎯 Why Do We Need systemd?

systemd helps Linux to:

* Boot faster
* Automatically start services
* Restart failed services
* Manage dependencies
* Centralize logging
* Control system resources

Without systemd, services would need to be started manually.

---

# 🏗️ systemd Architecture

```text
             Linux Kernel
                  │
                  ▼
          systemd (PID 1)
                  │
      ┌───────────┼───────────┐
      ▼           ▼           ▼
   NGINX       Docker      MySQL
      │           │           │
      ▼           ▼           ▼
   Running     Running     Running
```

systemd acts as the parent process for most system services.

---

# 🖥️ What is systemctl?

`systemctl` is the command used to manage services handled by systemd.

It can:

* Start services
* Stop services
* Restart services
* Check status
* Enable services at boot
* Disable services

---

# 📦 systemd Units

Everything managed by systemd is called a **Unit**.

| Unit       | Purpose             |
| ---------- | ------------------- |
| `.service` | Background services |
| `.target`  | Boot targets        |
| `.socket`  | Socket activation   |
| `.mount`   | Mount points        |
| `.timer`   | Scheduled tasks     |
| `.path`    | File monitoring     |

Example:

```text
nginx.service

docker.service

multi-user.target
```

---

# 🚀 Managing Services

### Check Service Status

```bash
systemctl status nginx
```

---

### Start a Service

```bash
sudo systemctl start nginx
```

---

### Stop a Service

```bash
sudo systemctl stop nginx
```

---

### Restart a Service

```bash
sudo systemctl restart nginx
```

---

### Reload Configuration

```bash
sudo systemctl reload nginx
```

---

### Enable at Boot

```bash
sudo systemctl enable nginx
```

---

### Disable at Boot

```bash
sudo systemctl disable nginx
```

---

### List Running Services

```bash
systemctl list-units --type=service
```

---

# 🎯 Boot Targets

Targets define the system's boot state.

Common targets:

| Target              | Purpose           |
| ------------------- | ----------------- |
| `multi-user.target` | Command-line mode |
| `graphical.target`  | GUI mode          |
| `rescue.target`     | Rescue mode       |
| `reboot.target`     | Reboot system     |
| `poweroff.target`   | Shutdown system   |

Check current target:

```bash
systemctl get-default
```

Change target:

```bash
sudo systemctl set-default multi-user.target
```

---

# 📜 Viewing Logs

systemd uses **journald** for logging.

View service logs:

```bash
journalctl -u nginx
```

Latest logs:

```bash
journalctl -xe
```

Boot logs:

```bash
journalctl -b
```

---

# 📝 Creating a Custom Service

Example service file:

```ini
[Unit]
Description=My Python App

[Service]
ExecStart=/usr/bin/python3 /home/yash/app.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Location:

```text
/etc/systemd/system/
```

Reload systemd:

```bash
sudo systemctl daemon-reload
```

Enable service:

```bash
sudo systemctl enable myapp
```

Start service:

```bash
sudo systemctl start myapp
```

---

# ☁️ DevOps Perspective

systemd is used daily in DevOps for:

* Starting web servers
* Managing Docker
* Running Jenkins
* Monitoring applications
* Auto-restarting failed services
* Viewing logs
* Running custom applications

Almost every production server depends on systemd.

---

# 🏭 Production Example

A website is down.

Check NGINX:

```bash
systemctl status nginx
```

Restart it:

```bash
sudo systemctl restart nginx
```

If it still fails:

```bash
journalctl -u nginx
```

The logs reveal a configuration error. After fixing the configuration, restart the service and verify it is active.

---

# 🎯 Common Interview Questions

### What is systemd?

The default system and service manager in modern Linux.

---

### What is PID 1?

`systemd`

---

### What is systemctl?

A command-line utility used to manage services controlled by systemd.

---

### Difference between `start` and `enable`?

* **start** → Starts the service immediately.
* **enable** → Starts the service automatically on system boot.

---

### Difference between `restart` and `reload`?

* **restart** → Stops and starts the service.
* **reload** → Reloads configuration without stopping the service (if supported).

---

### Where are custom service files stored?

```text
/etc/systemd/system/
```

---

# 🔍 Useful Commands

```bash
systemctl status

systemctl start

systemctl stop

systemctl restart

systemctl reload

systemctl enable

systemctl disable

systemctl list-units

systemctl daemon-reload

journalctl

journalctl -u nginx

journalctl -xe
```

---

# 📑 Interview Cheat Sheet

```text
Linux Boot
     │
     ▼
Kernel
     │
     ▼
systemd (PID 1)
     │
     ▼
Services (.service)
     │
     ▼
Applications
```

Remember:

* `systemd` = Service Manager
* `systemctl` = Management Command
* PID = 1
* `start` = Run now
* `enable` = Run on boot
* `journalctl` = View logs
* `daemon-reload` = Reload unit files after changes

---

# 📚 Summary

**systemd** is the core service manager in modern Linux systems. It controls system startup, manages services, handles dependencies, and centralizes logging. The **systemctl** utility provides an easy way to start, stop, restart, enable, disable, and inspect services.

For DevOps Engineers, mastering **systemd** and **systemctl** is essential for deploying applications, troubleshooting services, automating server operations, and maintaining reliable production environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Processes & Services → `../07-Processes-and-Services/README.md`

➡️ **Next:** Package Management → `../09-Package-Management/README.md`

### 📖 Recommended Reading

* Package Management
* Logs & Monitoring
* SSH & Remote Access
* Linux Troubleshooting
* End-to-End Linux Flow
