# 📂 Linux File System

> **Everything in Linux is treated as a file.**
>
> Whether it's a regular file, directory, hard disk, USB device, keyboard, network socket, or even a running process—Linux represents almost everything as a file.
>
> Understanding the Linux File System is essential for every DevOps Engineer because applications, Docker containers, Kubernetes, logs, configurations, and services all depend on it.

---

# 📖 Table of Contents

* What is the Linux File System?
* Why Do We Need It?
* Problem It Solves
* Linux File System Architecture
* Filesystem Hierarchy Standard (FHS)
* Important Linux Directories
* Mounting in Linux
* Everything is a File
* Absolute vs Relative Path
* File Types
* Real-World Analogy
* DevOps Perspective
* Production Example
* Real Interview Scenario
* Production Decision
* Senior Engineer Tips
* Common Interview Questions
* Common Mistakes
* Troubleshooting
* Useful Commands
* Interview Cheat Sheet
* Summary
* Related Topics

---

# ❓ What is the Linux File System?

A **Linux File System** is the method Linux uses to organize, store, and retrieve data on storage devices.

Unlike Windows, Linux does **not** organize files using drive letters like:

```text
C:
D:
E:
```

Instead, Linux starts everything from a **single root directory**:

```text
/
```

Every file and every storage device becomes part of this one directory tree.

---

# 🎯 Why Do We Need a File System?

Imagine storing millions of files without any organization.

Finding data would become impossible.

The Linux File System provides:

* Organized storage
* Fast file access
* Security
* Permissions
* Data integrity
* Efficient disk management

Without a filesystem, Linux would have no structured way to locate or manage data.

---

# ⚠️ Problem It Solves

The Linux File System solves several challenges:

* Organizes files logically
* Separates system files from user files
* Supports multiple storage devices
* Provides permissions and ownership
* Enables efficient data retrieval
* Allows applications to locate configuration files consistently

---

# 🏗️ Linux File System Architecture

```text
                         /
                    (Root Directory)
                          │
 ┌────────┬────────┬────────┬────────┬────────┬────────┐
 │        │        │        │        │        │
 ▼        ▼        ▼        ▼        ▼        ▼
/bin    /etc    /home    /var    /usr    /tmp
 │        │        │        │        │        │
Commands Config  Users   Logs   Apps   Temp Files
```

Everything starts from the **Root Directory (`/`)**.

---

# 🌳 Filesystem Hierarchy Standard (FHS)

Linux follows the **Filesystem Hierarchy Standard (FHS)**.

This standard defines where different types of files should be stored.

As a result,

every Linux distribution follows a similar directory structure.

---

# 📂 Important Linux Directories

## 📍 /

The root of the entire Linux filesystem.

Everything starts here.

---

## 📍 /bin

Contains essential user commands.

Examples:

```bash
ls

cp

mv

cat

pwd
```

These commands are required even in single-user mode.

---

## 📍 /sbin

Contains system administration commands.

Examples:

```bash
fsck

reboot

shutdown

mount
```

Typically used by the root user.

---

## 📍 /etc

Contains system configuration files.

Examples:

```text
/etc/passwd

/etc/hosts

/etc/fstab

/etc/ssh/
```

As a DevOps Engineer, you'll frequently edit files inside `/etc`.

---

## 📍 /home

Stores personal directories for normal users.

Example:

```text
/home/yash
```

Each user has their own home directory.

---

## 📍 /root

Home directory of the root (administrator) user.

Do not confuse:

```text
/
```

with

```text
/root
```

The first is the filesystem root.

The second is the root user's home directory.

---

## 📍 /var

Stores variable data.

Examples:

* Logs
* Mail
* Cache
* Databases

Examples:

```text
/var/log/

/var/cache/

/var/lib/
```

Most production logs are stored under `/var/log`.

---

## 📍 /usr

Contains installed software and shared libraries.

Examples:

```text
/usr/bin

/usr/lib

/usr/share
```

Think of this as the location for user applications and utilities.

---

## 📍 /tmp

Stores temporary files.

Files here may be deleted automatically after reboot.

Applications use this directory for temporary data.

---

## 📍 /dev

Contains device files.

Examples:

```text
/dev/sda

/dev/null

/dev/random

/dev/tty
```

In Linux,

hardware devices are represented as files.

---

## 📍 /proc

A virtual filesystem containing information about running processes and the kernel.

Examples:

```text
/proc/cpuinfo

/proc/meminfo

/proc/version
```

Useful for monitoring system information.

---

## 📍 /sys

Another virtual filesystem exposing hardware and kernel information.

System administrators use it for device configuration and inspection.

---

## 📍 /boot

Contains files required to boot Linux.

Examples:

* Kernel
* initramfs
* GRUB configuration

---

## 📍 /opt

Used for optional third-party software.

Examples:

* Google Chrome
* Oracle Software
* Custom enterprise applications

---

## 📍 /mnt

Temporary mount point for storage devices.

---

## 📍 /media

Automatically mounts removable media.

Examples:

* USB Drives
* DVDs
* External Hard Disks

---

# 💾 Mounting in Linux

Linux does not assign drive letters.

Instead,

every storage device is **mounted** somewhere within the filesystem.

Example:

```text
SSD

↓

Mounted at

/data
```

or

```text
USB

↓

Mounted at

/media/yash/USB
```

Once mounted,

the device becomes part of the same filesystem tree.

---

# 🌍 Everything is a File

One of Linux's most important philosophies is:

> **Everything is a File**

Examples:

| Object         | Location      |
| -------------- | ------------- |
| Hard Disk      | /dev/sda      |
| Terminal       | /dev/tty      |
| CPU Info       | /proc/cpuinfo |
| Memory Info    | /proc/meminfo |
| Random Numbers | /dev/random   |

Applications interact with these resources just like ordinary files.

---

# 📁 Absolute vs Relative Path

## Absolute Path

Starts from the root directory.

Example:

```text
/home/yash/project/readme.md
```

Always begins with:

```text
/
```

---

## Relative Path

Starts from the current working directory.

Example:

```text
Documents/project.txt
```

Relative paths do not begin with `/`.

---

# 📄 File Types in Linux

Linux supports several file types.

| Symbol | File Type        |
| ------ | ---------------- |
| -      | Regular File     |
| d      | Directory        |
| l      | Symbolic Link    |
| c      | Character Device |
| b      | Block Device     |
| p      | Named Pipe       |
| s      | Socket           |

Use:

```bash
ls -l
```

to view file types.

---

# 🌍 Real-World Analogy

Imagine a large company.

```text
Company Headquarters (/)

├── HR (/home)

├── Finance (/var)

├── Administration (/etc)

├── Equipment (/dev)

├── Temporary Storage (/tmp)

└── Software Department (/usr)
```

Each department has a dedicated purpose.

Similarly,

every Linux directory has a specific responsibility.

---

# ☁️ DevOps Perspective

Understanding the Linux File System is essential because you'll constantly work with:

* `/etc/nginx/`
* `/etc/systemd/`
* `/var/log/`
* `/var/lib/docker/`
* `/var/lib/kubelet/`
* `/boot/`
* `/home/`
* `/proc/`

Most production debugging begins by checking configuration files or logs within these directories.

---

# 🏭 Production Example

Suppose NGINX isn't starting.

Where should you look?

Configuration:

```text
/etc/nginx/
```

Logs:

```text
/var/log/nginx/
```

Systemd Service:

```text
/etc/systemd/system/
```

Understanding the filesystem quickly narrows down where to investigate.

---

# 🎯 Real Interview Scenario

### Question

A server is running out of disk space.

How would you troubleshoot?

### Expected Answer

1. Check disk usage:

```bash
df -h
```

2. Identify large directories:

```bash
du -sh /*
```

3. Inspect logs:

```text
/var/log
```

4. Remove unnecessary temporary files:

```text
/tmp
```

5. Verify mounted filesystems:

```bash
mount
```

---

# 🚀 Production Decision

Follow the FHS standard.

Store files where they belong.

Examples:

* Logs → `/var/log`
* Configuration → `/etc`
* User data → `/home`
* Temporary files → `/tmp`
* Third-party software → `/opt`

This consistency simplifies administration and troubleshooting.

---

# 🧠 Senior Engineer Tips

Many beginners memorize directory names.

A senior engineer understands **why** each directory exists.

For example:

* `/etc` contains configuration because applications need a standard location.
* `/var` stores variable data because logs and databases constantly change.
* `/proc` is virtual because it exposes live kernel information rather than files stored on disk.

Understanding the purpose behind the hierarchy makes troubleshooting much easier.

---

# 💼 Common Interview Questions

### Q1. What is the Linux File System?

The structure Linux uses to organize and manage files and directories.

---

### Q2. What is the root directory?

`/`

The starting point of the entire filesystem hierarchy.

---

### Q3. Where are configuration files stored?

```text
/etc
```

---

### Q4. Where are log files stored?

```text
/var/log
```

---

### Q5. What is the difference between `/` and `/root`?

`/` is the root of the filesystem.

`/root` is the home directory of the root user.

---

### Q6. What is `/proc`?

A virtual filesystem providing information about running processes and the kernel.

---

### Q7. Why does Linux use mounting instead of drive letters?

Linux integrates all storage devices into one unified directory tree, simplifying navigation and management.

---

# 🔥 Common Mistakes

❌ `/root` is the root filesystem.

✅ `/` is the root filesystem.

`/root` is the root user's home directory.

---

❌ `/proc` stores real files.

✅ `/proc` is a virtual filesystem generated by the kernel.

---

❌ `/tmp` stores permanent data.

✅ Files in `/tmp` are temporary and may be deleted automatically.

---

❌ Every storage device has its own drive letter.

✅ Linux mounts storage devices within the filesystem hierarchy.

---

# 🔍 Troubleshooting

Useful commands:

```bash
pwd
```

```bash
ls -l
```

```bash
tree
```

```bash
df -h
```

```bash
du -sh
```

```bash
mount
```

```bash
find
```

```bash
locate
```

```bash
lsblk
```

---

# 💻 Useful Commands

```bash
pwd                # Print current directory

ls -la             # List files with details

tree               # Show directory structure

cd                 # Change directory

df -h              # Filesystem usage

du -sh *           # Directory size

mount              # Mounted filesystems

find               # Search files

locate             # Fast file search

lsblk              # Block devices
```

---

# 💼 Interview Cheat Sheet

```text
                      /
                 (Root Directory)
                      │
 ┌────────┬────────┬────────┬────────┬────────┐
 │        │        │        │        │
 ▼        ▼        ▼        ▼        ▼
/etc    /home    /var    /usr    /dev
Config  Users    Logs    Apps   Devices
```

Remember:

* `/` → Root of the filesystem
* `/etc` → Configuration
* `/home` → User data
* `/var` → Logs & variable data
* `/usr` → Applications
* `/boot` → Boot files
* `/proc` → Process information
* `/dev` → Devices

---

# 📚 Summary

The Linux File System organizes all files, directories, devices, and system resources into a single hierarchical structure rooted at `/`.

By following the Filesystem Hierarchy Standard (FHS), Linux provides consistency across distributions, making system administration, troubleshooting, and application deployment predictable and efficient.

For DevOps Engineers, mastering the Linux File System is essential because nearly every operational task—from editing configurations and inspecting logs to managing containers and diagnosing production issues—depends on navigating this hierarchy effectively.

---

# 🔗 Related Topics

⬅️ Previous: **Processes & Threads** → `../03-Processes-and-Threads/README.md`

➡️ Next: **Inodes & Links** → `../05-Inodes-and-Links/README.md`

### 📖 Recommended Reading

* Inodes & Links
* Files & Directories
* Users & Groups
* File Permissions
* Storage & Disks
* Linux Troubleshooting
