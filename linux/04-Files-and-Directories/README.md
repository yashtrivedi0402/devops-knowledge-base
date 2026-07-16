# 📁 Files & Directories in Linux

> **Everything in Linux is represented as a file.** Whether it's a document, directory, hard disk, USB drive, network socket, printer, or even a running process, Linux treats almost everything as a file.
>
> Understanding files and directories is one of the most fundamental Linux skills because every DevOps task—deploying applications, managing configurations, troubleshooting servers, or automating infrastructure—involves working with them.

---

# 📖 Table of Contents

* What is a File?
* What is a Directory?
* Why Do We Need Them?
* Linux Directory Tree
* File Types
* Absolute vs Relative Path
* Hidden Files
* File Naming Rules
* Common File Operations
* Inodes Explained
* Hard Links
* Symbolic (Soft) Links
* Searching Files
* Compression & Archiving
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

# ❓ What is a File?

A **file** is a collection of data stored on a storage device.

Examples include:

* Text Files
* Configuration Files
* Images
* Videos
* Log Files
* Executable Programs
* Shell Scripts

Examples:

```text
nginx.conf

notes.txt

deploy.sh

app.log

docker-compose.yml
```

Everything you create or use in Linux is stored as a file.

---

# ❓ What is a Directory?

A **directory** is a special type of file that stores references to other files and directories.

Think of it as a folder that organizes data.

Example:

```text
/home

/home/yash

/home/yash/projects

/home/yash/projects/devops
```

Directories make file management efficient and organized.

---

# 🎯 Why Do We Need Files & Directories?

Imagine storing millions of files in one place.

Finding anything would be nearly impossible.

Directories help by:

* Organizing data
* Separating applications
* Managing user files
* Storing configurations
* Improving navigation
* Simplifying administration

---

# 🏗️ Linux Directory Tree

```text
/
│
├── home
│   └── yash
│       ├── Documents
│       ├── Downloads
│       └── Projects
│
├── etc
│
├── var
│
├── usr
│
├── tmp
│
└── boot
```

Every file starts from the **Root Directory (`/`)**.

---

# 📄 Linux File Types

Linux supports multiple file types.

| Symbol | Type             | Description                   |
| ------ | ---------------- | ----------------------------- |
| `-`    | Regular File     | Text files, scripts, binaries |
| `d`    | Directory        | Folder containing files       |
| `l`    | Symbolic Link    | Shortcut to another file      |
| `c`    | Character Device | Keyboard, Terminal            |
| `b`    | Block Device     | Hard Disk, SSD                |
| `s`    | Socket           | Process communication         |
| `p`    | Named Pipe       | IPC communication             |

View file types:

```bash
ls -l
```

---

# 📍 Absolute vs Relative Path

## Absolute Path

Starts from `/`

Example:

```text
/home/yash/Documents/readme.md
```

Always starts with:

```text
/
```

---

## Relative Path

Starts from your current directory.

Example:

```text
Documents/readme.md
```

Useful for navigation inside the current directory.

---

# 👻 Hidden Files

Hidden files begin with a dot (`.`).

Examples:

```text
.git

.bashrc

.profile

.env
```

View hidden files:

```bash
ls -la
```

These files usually store configuration settings.

---

# 📝 File Naming Rules

Linux filenames:

✅ Can contain:

* Letters
* Numbers
* Underscores
* Hyphens
* Dots

Examples:

```text
docker-compose.yml

deploy.sh

notes.txt

project_backup.tar.gz
```

Avoid:

* Spaces
* Special characters
* Long filenames

---

# ⚙️ Common File Operations

## Create File

```bash
touch file.txt
```

---

## Create Directory

```bash
mkdir project
```

---

## Copy

```bash
cp source.txt destination.txt
```

---

## Move / Rename

```bash
mv old.txt new.txt
```

---

## Delete File

```bash
rm file.txt
```

---

## Delete Directory

```bash
rm -r folder
```

---

## Display File

```bash
cat file.txt
```

---

## View Beginning

```bash
head file.txt
```

---

## View End

```bash
tail file.txt
```

---

# 🔑 Inodes

An **inode (Index Node)** stores metadata about a file.

It contains:

* Owner
* Permissions
* File Size
* Timestamps
* Disk Block Locations
* Link Count

It **does NOT** store the filename.

The filename is stored separately in the directory.

View inode numbers:

```bash
ls -i
```

Architecture:

```text
Filename
   │
   ▼
 Inode
   │
   ▼
Data Blocks
```

---

# 🔗 Hard Links

A Hard Link creates another filename pointing to the **same inode**.

Create one:

```bash
ln file.txt hardlink.txt
```

Architecture:

```text
file.txt
     │
     ▼
   Inode
     ▲
     │
hardlink.txt
```

Characteristics:

* Same inode
* Same data
* No original/copy relationship
* Works even if one filename is deleted
* Cannot cross filesystems

---

# 🔗 Symbolic (Soft) Links

A Symbolic Link stores the **path** to another file.

Create one:

```bash
ln -s file.txt shortcut.txt
```

Architecture:

```text
shortcut.txt
      │
      ▼
File Path
      │
      ▼
file.txt
      │
      ▼
Inode
```

Characteristics:

* Own inode
* Stores file path
* Can cross filesystems
* Breaks if the original file is deleted

---

# 📊 Hard Link vs Symbolic Link

| Feature                   | Hard Link | Symbolic Link |
| ------------------------- | --------- | ------------- |
| Points To                 | Inode     | File Path     |
| Same Inode                | ✅ Yes     | ❌ No          |
| Cross Filesystem          | ❌ No      | ✅ Yes         |
| Works if Original Deleted | ✅ Yes     | ❌ No          |
| Own Inode                 | ❌ No      | ✅ Yes         |

---

# 🔍 Searching Files

Search by name:

```bash
find /home -name "*.txt"
```

Fast search:

```bash
locate nginx.conf
```

Search inside files:

```bash
grep "ERROR" app.log
```

---

# 📦 Compression & Archiving

Create a tar archive:

```bash
tar -cvf backup.tar project/
```

Extract:

```bash
tar -xvf backup.tar
```

Compress:

```bash
gzip file.txt
```

Extract:

```bash
gunzip file.txt.gz
```

---

# 🌍 Real-World Analogy

Imagine a library.

* **Directory** = Bookshelf
* **File** = Book
* **Filename** = Book Title
* **Inode** = Library Record
* **Hard Link** = Two catalogue entries for the same book
* **Symbolic Link** = A note saying "This book is on Shelf B"

The book (data) exists independently of how many catalogue entries point to it.

---

# ☁️ DevOps Perspective

As a DevOps Engineer, you'll constantly work with files such as:

```text
/etc/nginx/nginx.conf

/etc/fstab

/etc/hosts

/var/log/syslog

/var/log/nginx/

Dockerfile

docker-compose.yml

Jenkinsfile
```

You'll frequently:

* Create files
* Edit configuration files
* Search logs
* Copy backups
* Archive releases
* Create symbolic links during deployments

---

# 🏭 Production Example

Suppose you're deploying version **v2** of an application.

Instead of replacing files directly, you maintain:

```text
/opt/app/releases/v1

/opt/app/releases/v2

/opt/app/current
```

`current` is a symbolic link.

During deployment:

```text
current

↓

v2
```

Rollback simply changes the symlink back to `v1`.

This is a common deployment strategy in production.

---

# 🎯 Real Interview Scenario

### Question

Your application suddenly starts reading the wrong configuration file after deployment.

How would you troubleshoot?

### Expected Answer

1. Check if configuration files exist.
2. Verify symbolic links using:

```bash
ls -l
```

3. Confirm the symlink points to the correct target.
4. Check permissions.
5. Verify file ownership.
6. Restart the service if necessary.

---

# 🚀 Production Decision

Use:

* **Hard Links** when you need multiple directory entries for the same file within one filesystem.
* **Symbolic Links** for application releases, shared configurations, version management, and cross-filesystem references.

---

# 🧠 Senior Engineer Tips

Many beginners think:

> Filename = File

Not true.

Internally:

```text
Filename

↓

Inode

↓

Data Blocks
```

Linux uses the inode to locate data.

The filename is simply a human-friendly reference.

Understanding this concept explains:

* Hard Links
* Symbolic Links
* Link Counts
* File Deletion
* Storage Management

---

# 💼 Common Interview Questions

### Q1. What is the difference between a file and a directory?

A file stores data.

A directory stores references to files and other directories.

---

### Q2. What is an inode?

A metadata structure describing a file.

---

### Q3. Does an inode store the filename?

No.

The filename is stored in the directory.

---

### Q4. Difference between Hard Link and Symbolic Link?

Hard Link → Same inode.

Symbolic Link → File path.

---

### Q5. Can Hard Links cross filesystems?

No.

---

### Q6. Can Symbolic Links cross filesystems?

Yes.

---

### Q7. What happens if the original file is deleted?

Hard Link still works.

Symbolic Link becomes broken.

---

# 🔥 Common Mistakes

❌ Thinking a filename is the actual file.

✅ Linux identifies files using inodes.

---

❌ Assuming all links behave the same.

✅ Hard Links and Symbolic Links work differently.

---

❌ Using spaces in filenames.

✅ Prefer:

```text
project_backup.tar.gz
```

Instead of:

```text
My Project Backup.tar.gz
```

---

# 🔍 Troubleshooting

Useful commands:

```bash
pwd
```

```bash
ls -la
```

```bash
ls -i
```

```bash
stat file.txt
```

```bash
find
```

```bash
locate
```

```bash
readlink symlink
```

```bash
tree
```

---

# 💻 Useful Commands

```bash
pwd

ls -la

touch

mkdir

cp

mv

rm

cat

head

tail

find

locate

grep

ls -i

stat

ln

ln -s

tree
```

---

# 💼 Interview Cheat Sheet

```text
Directory
      │
      ▼
 Filename
      │
      ▼
    Inode
      │
      ▼
 Data Blocks
```

Remember:

* Everything is a file.
* Directories organize files.
* Inodes store metadata.
* Hard Links → Same inode.
* Symbolic Links → File path.
* Hard Links survive filename deletion.
* Symbolic Links do not.

---

# 📚 Summary

Files and directories form the backbone of the Linux operating system. Every application, configuration, log, and executable is organized through the filesystem hierarchy.

Understanding how Linux manages files, directories, inodes, and links enables DevOps Engineers to deploy applications, troubleshoot systems, manage storage, and confidently handle real-world production environments.

---

# 🔗 Related Topics

⬅️ Previous: **Linux File System** → `../03-Linux-File-System/README.md`

➡️ Next: **Users & Groups** → `../05-Users-and-Groups/README.md`

### 📖 Recommended Reading

* Users & Groups
* File Permissions
* Processes & Services
* Storage & Disks
* Linux Troubleshooting
