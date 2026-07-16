# 📂 Linux File System

> **A Linux File System is the way Linux organizes, stores, and manages data on storage devices.**
>
> It provides a structured hierarchy that allows users and applications to efficiently access files, directories, and hardware resources.

---

# 📖 Table of Contents

* What is a Linux File System?
* Why Do We Need It?
* Linux File System Architecture
* Filesystem Hierarchy Standard (FHS)
* Important Directories
* Filesystem Types
* Mounting in Linux
* Virtual File Systems
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is a Linux File System?

A **File System** defines **how data is stored, organized, retrieved, and managed** on a storage device.

It acts as a bridge between:

* Applications
* Linux Kernel
* Storage Devices

Without a filesystem, Linux would not know:

* Where a file is stored
* How to retrieve it
* Who owns it
* What permissions it has

---

# 🎯 Why Do We Need a File System?

A File System helps Linux:

* Organize data efficiently
* Retrieve files quickly
* Manage storage devices
* Protect files using permissions
* Store metadata
* Support multiple users

Without it, all data would be an unorganized collection of bytes on the disk.

---

# 🏗️ Linux File System Architecture

```text
                User
                  │
                  ▼
           Application
                  │
                  ▼
             System Calls
                  │
                  ▼
             Linux Kernel
                  │
                  ▼
            File System (ext4)
                  │
      ┌───────────┴───────────┐
      ▼                       ▼
 Metadata (Inode)        Data Blocks
                  │
                  ▼
          SSD / HDD / NVMe
```

Linux applications never access the disk directly.

They communicate with the Kernel, which interacts with the filesystem to read and write data.

---

# 💽 Storage Flow

```text
Physical Disk
      │
      ▼
 Partition
      │
      ▼
 File System
      │
      ▼
 Mount Point
      │
      ▼
 User Access
```

Example:

```text
SSD

↓

Partition (/dev/sda1)

↓

ext4 File System

↓

Mounted at /

↓

Accessible to Users
```

---

# 🌳 Filesystem Hierarchy Standard (FHS)

Linux follows the **Filesystem Hierarchy Standard (FHS)**.

It defines where different types of files should be stored so that every Linux distribution follows a consistent structure.

Everything starts from the root directory:

```text
/
```

---

# 📂 Important Directories

| Directory | Purpose                         |
| --------- | ------------------------------- |
| `/`       | Root of the filesystem          |
| `/boot`   | Bootloader and Kernel files     |
| `/etc`    | Configuration files             |
| `/home`   | User home directories           |
| `/root`   | Root user's home directory      |
| `/usr`    | User applications and libraries |
| `/var`    | Logs, cache, databases          |
| `/tmp`    | Temporary files                 |
| `/dev`    | Device files                    |
| `/proc`   | Process and Kernel information  |
| `/sys`    | Hardware and Kernel information |
| `/opt`    | Third-party software            |
| `/mnt`    | Temporary mount point           |
| `/media`  | Removable devices               |

---

# 📦 Common Linux File Systems

| File System | Description                         |
| ----------- | ----------------------------------- |
| ext4        | Default Linux filesystem            |
| XFS         | High-performance filesystem         |
| Btrfs       | Modern filesystem with snapshots    |
| FAT32       | USB drives, compatible with many OS |
| NTFS        | Windows filesystem                  |
| exFAT       | Large USB drives and SD cards       |

---

# 💾 Mounting in Linux

Unlike Windows, Linux does **not** use drive letters.

Instead, every storage device is **mounted** inside the directory tree.

Example:

```text
/dev/sdb1

↓

Mounted at

/data
```

Now users can access the disk through:

```text
/data
```

Useful command:

```bash
mount
```

---

# 🖥️ Virtual File Systems

Some Linux directories don't store actual files.

Instead, they expose live system information.

### `/proc`

Contains information about:

* Running processes
* CPU
* Memory
* Kernel

Example:

```bash
cat /proc/cpuinfo
```

---

### `/sys`

Provides hardware and kernel information.

---

### `/dev`

Represents hardware devices as files.

Examples:

```text
/dev/sda

/dev/null

/dev/tty
```

---

# 🌍 Real-World Analogy

Think of a **library**.

* Hard Disk → Building
* File System → Library Management System
* Directories → Bookshelves
* Files → Books
* Kernel → Librarian
* User → Reader

Without the library management system, finding a book would be extremely difficult.

---

# ☁️ DevOps Perspective

Every DevOps tool relies on the Linux File System.

Examples:

* NGINX configuration → `/etc/nginx`
* Docker data → `/var/lib/docker`
* Kubernetes data → `/var/lib/kubelet`
* Logs → `/var/log`
* Boot files → `/boot`

Understanding the filesystem helps when:

* Debugging applications
* Finding configuration files
* Managing storage
* Troubleshooting servers

---

# 🏭 Production Example

Suppose an NGINX server isn't starting.

A DevOps Engineer checks:

Configuration:

```text
/etc/nginx/nginx.conf
```

Logs:

```text
/var/log/nginx/
```

Disk usage:

```bash
df -h
```

Filesystem health:

```bash
mount

lsblk
```

---

# 🎯 Common Interview Questions

### What is a Linux File System?

A method used by Linux to organize and manage data on storage devices.

---

### What is FHS?

Filesystem Hierarchy Standard that defines the Linux directory structure.

---

### Which is the default Linux File System?

**ext4**

---

### Difference between `/` and `/root`?

* `/` → Root of the filesystem
* `/root` → Home directory of the root user

---

### What is mounting?

The process of attaching a filesystem to a directory so users can access it.

---

### What is `/proc`?

A virtual filesystem containing information about processes and the Linux Kernel.

---

# 🔍 Useful Commands

```bash
pwd                 # Current directory

df -h               # Disk usage

du -sh *            # Directory size

mount               # Mounted filesystems

lsblk               # Block devices

blkid               # Filesystem information

findmnt             # Mounted filesystems

cat /proc/filesystems

cat /etc/fstab
```

---

# 📑 Interview Cheat Sheet

```text
User
 │
 ▼
Application
 │
 ▼
System Call
 │
 ▼
Linux Kernel
 │
 ▼
File System
 │
 ▼
Disk Partition
 │
 ▼
Storage Device
```

Remember:

* Linux starts from `/`
* ext4 is the default filesystem
* Everything is mounted into one directory tree
* `/etc` → Configurations
* `/var` → Logs
* `/proc` → Process information
* `/dev` → Devices
* `/boot` → Boot files

---

# 📚 Summary

The Linux File System is responsible for organizing and managing data on storage devices. It provides a hierarchical directory structure, supports different filesystem types, and allows Linux to efficiently store, retrieve, and protect data.

For DevOps Engineers, understanding the Linux File System is essential because almost every production task—from configuring applications and analyzing logs to managing storage and troubleshooting servers—depends on navigating and understanding this structure.

---

# 🔗 Related Topics

⬅️ **Previous:** Boot Process → `../02-Boot-Process/README.md`

➡️ **Next:** Files & Directories → `../04-Files-and-Directories/README.md`

### 📖 Recommended Reading

* Files & Directories
* Users & Groups
* File Permissions
* Storage & Disks
* Linux Troubleshooting
