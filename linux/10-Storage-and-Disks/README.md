# 💽 Linux Storage & Disks

> **Storage is where Linux stores data permanently, while disks are the physical or virtual devices that provide this storage.**
>
> Linux uses partitions, file systems, and mount points to organize storage and make it accessible to users and applications.

---

# 📖 Table of Contents

* What is Storage?
* Why Do We Need Storage?
* Storage Architecture
* Types of Storage
* Partitions
* Block Devices
* Mount Points
* Disk Usage
* Disk Management Commands
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Storage?

Storage is used to permanently store:

* Operating System
* Applications
* User Files
* Logs
* Databases

Common storage devices:

* HDD
* SSD
* NVMe
* Cloud Volumes (AWS EBS, Azure Managed Disk)

---

# 🎯 Why Do We Need Storage?

Storage allows Linux to:

* Save files permanently
* Store application data
* Keep logs
* Maintain databases
* Preserve data after reboot

---

# 🏗️ Storage Architecture

```text
Application
     │
     ▼
File System
     │
     ▼
Partition
     │
     ▼
Disk
     │
     ▼
Physical Storage
```

---

# 💾 Types of Storage

| Storage         | Description                              |
| --------------- | ---------------------------------------- |
| HDD             | Mechanical disk, low cost                |
| SSD             | Faster than HDD                          |
| NVMe            | High-speed SSD using PCIe                |
| USB             | Portable storage                         |
| Network Storage | NFS, SAN, NAS                            |
| Cloud Storage   | AWS EBS, Azure Disk, GCP Persistent Disk |

---

# 🧩 Partitions

A **partition** divides a disk into separate logical sections.

Example:

```text
Disk (/dev/sda)
│
├── /dev/sda1
├── /dev/sda2
└── /dev/sda3
```

Each partition can have its own filesystem.

---

# 📦 Block Devices

Linux treats storage devices as **block devices**.

Examples:

```text
/dev/sda
/dev/sdb
/dev/nvme0n1
```

View block devices:

```bash
lsblk
```

---

# 📂 Mount Points

A filesystem must be **mounted** before it can be accessed.

Example:

```text
/dev/sdb1
      │
      ▼
Mounted at
      │
      ▼
/data
```

Mount manually:

```bash
sudo mount /dev/sdb1 /data
```

Unmount:

```bash
sudo umount /data
```

---

# 📊 Disk Usage

Check filesystem usage:

```bash
df -h
```

Check directory size:

```bash
du -sh /var/log
```

Display available block devices:

```bash
lsblk
```

---

# 🛠️ Disk Management Commands

Create filesystem:

```bash
sudo mkfs.ext4 /dev/sdb1
```

View disk partitions:

```bash
sudo fdisk -l
```

Display filesystem UUID:

```bash
blkid
```

Persistent mounts:

```text
/etc/fstab
```

---

# ☁️ DevOps Perspective

Storage management is important for:

* Managing cloud volumes
* Monitoring disk space
* Mounting new storage
* Database storage
* Docker & Kubernetes volumes
* Preventing disk-full outages

---

# 🏭 Production Example

A production server reports:

```text
No space left on device
```

Troubleshooting:

```bash
df -h
du -sh /var/*
```

Find unnecessary logs or files, clean them up, or attach and mount a new disk to restore normal operation.

---

# 🎯 Common Interview Questions

### What is a partition?

A logical division of a physical disk.

---

### Difference between HDD and SSD?

* HDD → Mechanical, slower.
* SSD → Flash storage, faster.

---

### What is a mount point?

A directory where a filesystem is attached and becomes accessible.

---

### Which file stores permanent mount information?

```text
/etc/fstab
```

---

### Which command shows disk usage?

```bash
df -h
```

---

### Which command shows directory size?

```bash
du -sh
```

---

# 🔍 Useful Commands

```bash
lsblk

df -h

du -sh

fdisk -l

blkid

mount

umount

mkfs.ext4

findmnt

cat /etc/fstab
```

---

# 📑 Interview Cheat Sheet

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

Remember:

* `lsblk` → Block devices
* `df -h` → Disk usage
* `du -sh` → Directory size
* `mount` → Attach filesystem
* `umount` → Detach filesystem
* `/etc/fstab` → Permanent mounts

---

# 📚 Summary

Linux organizes storage using **disks**, **partitions**, **file systems**, and **mount points**. Tools like `lsblk`, `df`, `du`, `mount`, and `fdisk` help administrators monitor and manage storage efficiently.

For DevOps Engineers, understanding storage is essential for provisioning servers, attaching cloud volumes, troubleshooting disk issues, managing application data, and ensuring production systems have sufficient capacity and reliable storage.

---

# 🔗 Related Topics

⬅️ **Previous:** Package Management → `../09-Package-Management/README.md`

➡️ **Next:** Memory & CPU → `../11-Memory-and-CPU/README.md`

### 📖 Recommended Reading

* Memory & CPU
* Linux File System
* Logs & Monitoring
* Linux Troubleshooting
* End-to-End Linux Flow
