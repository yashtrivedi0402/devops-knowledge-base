# 🔐 Linux SSH & Remote Access

> **SSH (Secure Shell) is a secure network protocol used to remotely access and manage Linux systems over a network.**
>
> SSH encrypts communication between a client and a server, making it the standard method for remote administration of Linux servers in production environments.

---

# 📖 Table of Contents

* What is SSH?
* Why Do We Need SSH?
* SSH Architecture
* How SSH Works
* Authentication Methods
* SSH Keys
* SSH Configuration
* File Transfer
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is SSH?

**SSH (Secure Shell)** is a protocol that allows users to securely connect to remote Linux systems.

It is used to:

* Access remote servers
* Execute commands remotely
* Transfer files securely
* Manage cloud instances
* Deploy applications

Default SSH Port:

```text
22
```

---

# 🎯 Why Do We Need SSH?

SSH provides:

* Secure remote login
* Encrypted communication
* Secure file transfer
* Remote administration
* Password and key-based authentication

Without SSH, administrators would need physical access to every server.

---

# 🏗️ SSH Architecture

```text
SSH Client
     │
Encrypted Connection (Port 22)
     │
     ▼
SSH Server (sshd)
     │
     ▼
Linux Server
```

---

# 🔄 How SSH Works

1. Client requests a connection.
2. Server verifies its identity.
3. User authenticates using a password or SSH key.
4. A secure encrypted session is established.
5. Commands are executed remotely.

---

# 🔑 Authentication Methods

### Password Authentication

Login using username and password.

Example:

```bash
ssh ubuntu@192.168.1.10
```

---

### SSH Key Authentication

Uses a public/private key pair instead of passwords.

Advantages:

* More secure
* Faster login
* Ideal for automation

---

# 🔐 SSH Keys

Generate a key pair:

```bash
ssh-keygen
```

Default location:

```text
~/.ssh/
├── id_rsa
├── id_rsa.pub
```

Copy the public key to a remote server:

```bash
ssh-copy-id user@server-ip
```

---

# ⚙️ SSH Configuration

SSH client configuration:

```text
~/.ssh/config
```

SSH server configuration:

```text
/etc/ssh/sshd_config
```

Restart the SSH service after configuration changes:

```bash
sudo systemctl restart ssh
```

---

# 📂 Secure File Transfer

Copy a file to a remote server:

```bash
scp file.txt user@server:/home/user/
```

Copy a file from a remote server:

```bash
scp user@server:/home/user/file.txt .
```

---

# ☁️ DevOps Perspective

SSH is essential for:

* Managing cloud servers
* Accessing AWS EC2 instances
* Deploying applications
* Running automation scripts
* Configuring servers
* Troubleshooting production issues

Many automation tools such as **Ansible** use SSH to communicate with remote servers.

---

# 🏭 Production Example

A new EC2 instance is launched.

Connect using:

```bash
ssh -i mykey.pem ubuntu@<public-ip>
```

After logging in:

* Update packages
* Install Docker
* Configure NGINX
* Deploy the application

SSH provides secure remote administration without physical access.

---

# 🎯 Common Interview Questions

### What is SSH?

A secure protocol used for remote login and remote command execution.

---

### Which port does SSH use?

```text
22
```

---

### Difference between SSH and Telnet?

* SSH → Encrypted and secure.
* Telnet → Unencrypted and insecure.

---

### Difference between Password Authentication and SSH Key Authentication?

* Password → Uses username and password.
* SSH Key → Uses a public/private key pair.

---

### Which service runs SSH?

```text
sshd
```

---

### Where is the SSH server configuration stored?

```text
/etc/ssh/sshd_config
```

---

# 🔍 Useful Commands

```bash
ssh

ssh-keygen

ssh-copy-id

scp

sftp

systemctl status ssh

systemctl restart ssh

cat ~/.ssh/authorized_keys
```

---

# 📑 Interview Cheat Sheet

```text
SSH Client
      │
      ▼
Port 22
      │
Encrypted Connection
      │
      ▼
SSH Server (sshd)
      │
      ▼
Linux Server
```

Remember:

* SSH = Secure Shell
* Default Port = 22
* `ssh` → Remote login
* `scp` → Secure file transfer
* `ssh-keygen` → Generate SSH keys
* `ssh-copy-id` → Copy public key
* `sshd` → SSH server service
* `~/.ssh/` → SSH key directory

---

# 📚 Summary

SSH is the standard protocol for securely accessing and managing Linux systems over a network. It provides encrypted communication, supports password and key-based authentication, and enables secure file transfers.

For DevOps Engineers, SSH is a core skill used to manage cloud servers, automate deployments, troubleshoot production systems, and securely administer Linux infrastructure.

---

# 🔗 Related Topics

⬅️ **Previous:** Shell Scripting Basics → `../14-Shell-Scripting-Basics/README.md`

➡️ **Next:** Important Commands → `../16-Important-Commands/README.md`

### 📖 Recommended Reading

* Important Commands
* Linux Networking
* Systemd & Systemctl
* Linux Troubleshooting
* End-to-End Linux Flow
