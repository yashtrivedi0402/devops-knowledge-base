# 👥 Linux Users & Groups

> **Linux is a multi-user operating system, which means multiple users can use the same system securely at the same time.**
>
> Linux uses **Users** and **Groups** to manage authentication, ownership, permissions, and access control. Every file, process, and service runs under a specific user and group.

---

# 📖 Table of Contents

* What are Users & Groups?
* Why Do We Need Them?
* User Types
* User Architecture
* Important Files
* UID & GID
* Root User
* sudo vs su
* User Management
* Group Management
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a User?

A **User** is an identity created in Linux to access and use the system.

Each user has:

* Username
* Password
* Home Directory
* User ID (UID)
* Default Shell
* Permissions

Example:

```text
yash
ubuntu
root
jenkins
mysql
nginx
```

---

# ❓ What is a Group?

A **Group** is a collection of users.

Instead of giving permissions individually, Linux allows permissions to be assigned to groups.

Example:

```text
developers
admins
docker
sudo
```

---

# 🎯 Why Do We Need Users & Groups?

They help Linux:

* Authenticate users
* Secure files
* Control access
* Manage permissions
* Isolate applications
* Improve system security

Without users and groups, every user would have unrestricted access to the system.

---

# 👤 Types of Users

### 1. Root User

* Superuser
* UID = 0
* Full access to the system

---

### 2. Regular User

Created for daily work.

Example:

```text
yash
ubuntu
john
```

---

### 3. System Users

Created for services.

Examples:

```text
mysql

nginx

docker

www-data
```

These users usually cannot log in.

---

# 🏗️ Linux User Architecture

```text
                Linux System
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
     Users                    Groups
        │                         │
        └────────────┬────────────┘
                     ▼
             Files & Processes
                     │
                     ▼
               Permissions
```

---

# 🆔 UID & GID

Every user has a **User ID (UID)**.

Every group has a **Group ID (GID)**.

Example:

```text
User : yash
UID  : 1000

Group : developers
GID   : 1001
```

Linux internally uses UID and GID instead of usernames.

---

# 📂 Important Files

### `/etc/passwd`

Stores user account information.

```bash
cat /etc/passwd
```

---

### `/etc/shadow`

Stores encrypted passwords.

Accessible only by root.

```bash
sudo cat /etc/shadow
```

---

### `/etc/group`

Stores group information.

```bash
cat /etc/group
```

---

# 👑 Root User

The **root** user is the system administrator.

Capabilities:

* Install software
* Create users
* Delete users
* Modify system files
* Manage services

UID of root:

```text
0
```

---

# 🔑 sudo vs su

| sudo                                 | su                             |
| ------------------------------------ | ------------------------------ |
| Executes one command as another user | Switches to another user       |
| Safer                                | Full login shell               |
| Preferred in production              | Mostly used for administration |

Example:

```bash
sudo apt update
```

```bash
su -
```

---

# 👤 User Management

### Create User

```bash
sudo useradd yash
```

or

```bash
sudo adduser yash
```

---

### Set Password

```bash
sudo passwd yash
```

---

### Delete User

```bash
sudo userdel yash
```

Delete with home directory:

```bash
sudo userdel -r yash
```

---

### Change User

```bash
su - yash
```

---

# 👥 Group Management

### Create Group

```bash
sudo groupadd developers
```

---

### Delete Group

```bash
sudo groupdel developers
```

---

### Add User to Group

```bash
sudo usermod -aG docker yash
```

---

### View Groups

```bash
groups yash
```

or

```bash
id yash
```

---

# 🌍 Real-World Analogy

Imagine a company.

```text
Company
   │
   ├── Employees (Users)
   │
   ├── Departments (Groups)
   │
   └── Office Resources (Files)
```

Instead of giving access to every employee individually, access is granted to an entire department.

Linux works the same way.

---

# ☁️ DevOps Perspective

Users and groups are used everywhere in DevOps.

Examples:

* Docker daemon → docker group
* Jenkins → jenkins user
* MySQL → mysql user
* NGINX → www-data user

Applications run using dedicated users to improve security.

---

# 🏭 Production Example

A developer cannot run Docker:

```text
permission denied while trying to connect to Docker daemon
```

Solution:

```bash
sudo usermod -aG docker yash
```

Logout and login again.

Problem solved.

---

# 🎯 Common Interview Questions

### What is UID?

A unique numerical identifier for a user.

---

### What is GID?

A unique numerical identifier for a group.

---

### Difference between adduser and useradd?

* **useradd** is a low-level command.
* **adduser** is an interactive, user-friendly wrapper.

---

### Difference between sudo and su?

* **sudo** runs a specific command with elevated privileges.
* **su** switches to another user account.

---

### Which file stores user information?

```text
/etc/passwd
```

---

### Which file stores encrypted passwords?

```text
/etc/shadow
```

---

### Which file stores groups?

```text
/etc/group
```

---

# 🔍 Useful Commands

```bash
whoami

id

groups

who

users

adduser

userdel

groupadd

groupdel

passwd

su

sudo
```

---

# 📑 Interview Cheat Sheet

```text
User
 │
 ▼
UID
 │
 ▼
Primary Group
 │
 ▼
GID
 │
 ▼
Files & Processes
 │
 ▼
Permissions
```

Remember:

* Root UID = 0
* Every user has a UID
* Every group has a GID
* `/etc/passwd` → User details
* `/etc/shadow` → Passwords
* `/etc/group` → Groups
* Use **sudo** instead of logging in as root whenever possible.

---

# 📚 Summary

Linux uses **Users** and **Groups** to provide secure, multi-user access to the system. Every file, process, and service belongs to a user and a group, allowing Linux to enforce permissions and isolate workloads.

For DevOps Engineers, understanding users and groups is essential for managing servers, configuring services, securing applications, troubleshooting permission issues, and administering Linux systems in production.

---

# 🔗 Related Topics

⬅️ **Previous:** Files & Directories → `../04-Files-and-Directories/README.md`

➡️ **Next:** File Permissions → `../06-File-Permissions/README.md`

### 📖 Recommended Reading

* File Permissions
* Processes & Services
* Systemd & Systemctl
* SSH & Remote Access
* Linux Troubleshooting
