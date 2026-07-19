# 💻 Linux Important Commands

> **Linux commands are utilities used to interact with the operating system through the terminal.**
>
> They help users navigate the file system, manage files, monitor resources, configure networking, control processes, and administer Linux servers. Mastering these commands is essential for every Linux Administrator and DevOps Engineer.

---

# 📖 Table of Contents

* Why Learn Linux Commands?
* Command Categories
* File & Directory Commands
* File Viewing Commands
* User Commands
* Process Commands
* Memory & Disk Commands
* Networking Commands
* Service Management Commands
* Package Management Commands
* Search Commands
* Compression Commands
* DevOps Perspective
* Production Example
* Interview Questions
* Summary
* Related Topics

---

# 🎯 Why Learn Linux Commands?

Linux commands help you:

* Navigate the system
* Manage files and directories
* Monitor resources
* Troubleshoot issues
* Configure servers
* Automate tasks
* Manage applications

Almost every DevOps tool interacts with Linux through the command line.

---

# 🗂️ Command Categories

* File & Directory
* File Viewing
* User Management
* Process Management
* Memory & Storage
* Networking
* Service Management
* Package Management
* Search
* Compression

---

# 📁 File & Directory Commands

| Command | Purpose                  |
| ------- | ------------------------ |
| `pwd`   | Show current directory   |
| `ls`    | List files               |
| `cd`    | Change directory         |
| `mkdir` | Create directory         |
| `rmdir` | Remove empty directory   |
| `touch` | Create file              |
| `cp`    | Copy files               |
| `mv`    | Move/Rename files        |
| `rm`    | Delete files             |
| `tree`  | Show directory structure |

---

# 📄 File Viewing Commands

| Command   | Purpose                   |
| --------- | ------------------------- |
| `cat`     | Display file contents     |
| `less`    | View large files          |
| `more`    | View files page by page   |
| `head`    | Show first lines          |
| `tail`    | Show last lines           |
| `tail -f` | Monitor logs in real time |
| `nano`    | Terminal text editor      |
| `vim`     | Advanced text editor      |

---

# 👤 User Commands

| Command  | Purpose                      |
| -------- | ---------------------------- |
| `whoami` | Current user                 |
| `id`     | User & Group IDs             |
| `groups` | User groups                  |
| `passwd` | Change password              |
| `su`     | Switch user                  |
| `sudo`   | Run command as administrator |

---

# ⚙️ Process Commands

| Command   | Purpose                |
| --------- | ---------------------- |
| `ps`      | Show running processes |
| `top`     | Real-time monitoring   |
| `htop`    | Interactive monitoring |
| `kill`    | Stop process           |
| `killall` | Stop processes by name |
| `pgrep`   | Find process ID        |
| `pidof`   | Show process ID        |

---

# 💾 Memory & Disk Commands

| Command   | Purpose            |
| --------- | ------------------ |
| `free -h` | Memory usage       |
| `df -h`   | Disk usage         |
| `du -sh`  | Directory size     |
| `lsblk`   | Block devices      |
| `mount`   | Mount filesystem   |
| `umount`  | Unmount filesystem |

---

# 🌐 Networking Commands

| Command      | Purpose                 |
| ------------ | ----------------------- |
| `ip addr`    | Show IP address         |
| `ip route`   | Show routing table      |
| `ping`       | Test connectivity       |
| `ss -tuln`   | Show listening ports    |
| `netstat`    | Network statistics      |
| `nslookup`   | DNS lookup              |
| `dig`        | DNS query               |
| `traceroute` | Trace network path      |
| `curl`       | Transfer data from URLs |
| `wget`       | Download files          |

---

# ⚡ Service Management Commands

| Command             | Purpose           |
| ------------------- | ----------------- |
| `systemctl status`  | Service status    |
| `systemctl start`   | Start service     |
| `systemctl stop`    | Stop service      |
| `systemctl restart` | Restart service   |
| `systemctl enable`  | Enable at boot    |
| `journalctl`        | View service logs |

---

# 📦 Package Management Commands

| Ubuntu/Debian | RHEL/Fedora        |
| ------------- | ------------------ |
| `apt update`  | `dnf check-update` |
| `apt install` | `dnf install`      |
| `apt remove`  | `dnf remove`       |
| `apt upgrade` | `dnf upgrade`      |

---

# 🔍 Search Commands

| Command   | Purpose                     |
| --------- | --------------------------- |
| `find`    | Search files                |
| `locate`  | Fast file search            |
| `which`   | Find command location       |
| `whereis` | Find binary & documentation |
| `grep`    | Search text inside files    |

Example:

```bash
find /home -name "*.log"

grep "ERROR" app.log

which docker
```

---

# 📦 Compression Commands

| Command  | Purpose             |
| -------- | ------------------- |
| `tar`    | Archive files       |
| `gzip`   | Compress files      |
| `gunzip` | Decompress files    |
| `zip`    | Create ZIP archive  |
| `unzip`  | Extract ZIP archive |

Example:

```bash
tar -czf backup.tar.gz project/

tar -xzf backup.tar.gz
```

---

# ☁️ DevOps Perspective

Linux commands are used every day for:

* Deploying applications
* Managing servers
* Debugging issues
* Monitoring resources
* Configuring networking
* Automating infrastructure
* Managing Docker & Kubernetes
* CI/CD pipelines

---

# 🏭 Production Example

A website is down.

Investigation:

```bash
systemctl status nginx

ss -tuln

df -h

free -h

journalctl -u nginx

curl localhost
```

These commands quickly help identify whether the issue is related to the service, networking, storage, memory, or application.

---

# 🎯 Common Interview Questions

### Which command shows the current directory?

```bash
pwd
```

---

### Which command lists files?

```bash
ls
```

---

### Which command checks memory usage?

```bash
free -h
```

---

### Which command checks disk usage?

```bash
df -h
```

---

### Which command shows running processes?

```bash
ps -ef
```

or

```bash
top
```

---

### Which command checks service status?

```bash
systemctl status nginx
```

---

### Which command searches text inside files?

```bash
grep
```

---

# 📑 Interview Cheat Sheet

| Task              | Command            |
| ----------------- | ------------------ |
| Current Directory | `pwd`              |
| List Files        | `ls`               |
| Copy File         | `cp`               |
| Move File         | `mv`               |
| Delete File       | `rm`               |
| Process Status    | `ps -ef`           |
| CPU Usage         | `top`              |
| Memory            | `free -h`          |
| Disk Usage        | `df -h`            |
| IP Address        | `ip addr`          |
| Service Status    | `systemctl status` |
| Logs              | `journalctl`       |
| Search Text       | `grep`             |
| Search Files      | `find`             |
| Download File     | `wget`             |

---

# 📚 Summary

Linux commands are the primary interface for managing and administering Linux systems. From navigating directories and monitoring resources to configuring services and troubleshooting applications, these commands form the foundation of Linux administration.

For DevOps Engineers, strong command-line skills are essential for server management, automation, cloud operations, container orchestration, and maintaining production infrastructure efficiently.

---

# 🔗 Related Topics

⬅️ **Previous:** SSH & Remote Access → `../15-SSH-and-Remote-Access/README.md`

➡️ **Next:** Linux Troubleshooting → `../17-Troubleshooting/README.md`

### 📖 Recommended Reading

* Linux Troubleshooting
* Shell Scripting Basics
* Logs & Monitoring
* End-to-End Linux Flow
* Linux Manual Pages (`man`)
