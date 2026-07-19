# 🔐 Linux File Permissions

> **Linux File Permissions determine who can access a file or directory and what actions they are allowed to perform.**
>
> Every file and directory in Linux is protected using a permission system based on **Users**, **Groups**, and **Others**. Understanding permissions is one of the most important Linux concepts because most production issues involve permission-related errors.

---

# 📖 Table of Contents

* What are File Permissions?
* Why Do We Need Them?
* Permission Architecture
* Permission Categories
* Permission Types (r, w, x)
* Understanding Permission Notation
* Numeric (Octal) Permissions
* Symbolic Permissions
* chmod Command
* chown Command
* chgrp Command
* Directory Permissions
* Special Permissions (SUID, SGID, Sticky Bit)
* umask
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are File Permissions?

File permissions define **who can access a file or directory and what operations they can perform.**

Linux assigns permissions to:

* 👤 Owner (User)
* 👥 Group
* 🌍 Others

Each category can have different permissions.

---

# 🎯 Why Do We Need File Permissions?

Permissions help Linux:

* Protect sensitive files
* Prevent unauthorized access
* Secure applications
* Isolate users
* Maintain system integrity

Without permissions, any user could modify or delete critical system files.

---

# 🏗️ Permission Architecture

```text id="m7h9a2"
              Linux File
                   │
        ┌──────────┴──────────┐
        ▼          ▼          ▼
      Owner      Group      Others
        │          │          │
        ▼          ▼          ▼
      r w x      r w x      r w x
```

---

# 👥 Permission Categories

## 👤 Owner (User)

The user who owns the file.

---

## 👥 Group

Users belonging to the file's group.

---

## 🌍 Others

Everyone else on the system.

---

# 🔑 Permission Types

Linux has three basic permissions.

## 📖 Read (r)

For Files:

* View file contents.

For Directories:

* List files inside the directory.

Value:

```text id="rval"
4
```

---

## ✍️ Write (w)

For Files:

* Modify file contents.

For Directories:

* Create, rename, or delete files inside the directory.

Value:

```text id="wval"
2
```

---

## ⚙️ Execute (x)

For Files:

* Run the file as a program or script.

For Directories:

* Enter (traverse) the directory using commands like `cd`.

> **Important Interview Point:**
> On a **directory**, `x` does **not** mean "execute." It means **traverse/access** the directory.

Value:

```text id="xval"
1
```

---

# 📄 Understanding Permission Notation

Example:

```bash id="permcmd"
-rwxr-xr--
```

Breakdown:

```text id="permarch"
-  rwx  r-x  r--
│   │     │    │
│   │     │    └── Others
│   │     └────── Group
│   └──────────── Owner
└──────────────── File Type
```

File Type Symbols:

| Symbol | Meaning       |
| ------ | ------------- |
| `-`    | Regular File  |
| `d`    | Directory     |
| `l`    | Symbolic Link |

---

# 🔢 Numeric (Octal) Permissions

Each permission has a numeric value.

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

Examples:

| Permission | Value |
| ---------- | ----- |
| rwx        | 7     |
| rw-        | 6     |
| r-x        | 5     |
| r--        | 4     |
| ---        | 0     |

Common combinations:

| Numeric | Meaning                           |
| ------- | --------------------------------- |
| 777     | Everyone has full access          |
| 755     | Owner full, others read & execute |
| 744     | Owner full, others read only      |
| 700     | Owner only                        |
| 644     | Common for configuration files    |
| 600     | Private files                     |

---

# ✍️ Symbolic Permissions

Instead of numbers, Linux also supports symbolic notation.

Examples:

```bash id="sym1"
chmod u+x script.sh
```

```bash id="sym2"
chmod g+w file.txt
```

```bash id="sym3"
chmod o-r secret.txt
```

Symbols:

| Symbol | Meaning |
| ------ | ------- |
| u      | User    |
| g      | Group   |
| o      | Others  |
| a      | All     |

---

# 🔧 chmod Command

Used to change permissions.

Numeric:

```bash id="chmod1"
chmod 755 script.sh
```

Symbolic:

```bash id="chmod2"
chmod u+x script.sh
```

---

# 👤 chown Command

Changes file ownership.

```bash id="chown1"
sudo chown yash file.txt
```

User and Group:

```bash id="chown2"
sudo chown yash:developers file.txt
```

---

# 👥 chgrp Command

Changes only the group.

```bash id="chgrp1"
sudo chgrp developers file.txt
```

---

# 📂 Directory Permissions

Directories behave differently from files.

| Permission | Meaning                      |
| ---------- | ---------------------------- |
| r          | List directory contents      |
| w          | Create, rename, delete files |
| x          | Enter/traverse directory     |

Example:

Without execute permission:

```bash id="cdfail"
cd project/
```

will fail even if read permission exists.

---

# ⭐ Special Permissions

## 1️⃣ SUID (Set User ID)

Runs a program with the file owner's privileges.

Example:

```text id="suid"
-rwsr-xr-x
```

Numeric:

```text id="suidnum"
4755
```

---

## 2️⃣ SGID (Set Group ID)

Runs with the file group's privileges.

On directories, new files inherit the directory's group.

Numeric:

```text id="sgidnum"
2755
```

---

## 3️⃣ Sticky Bit

Used on shared directories like `/tmp`.

Only the file owner can delete their own files.

Example:

```text id="sticky"
drwxrwxrwt
```

Numeric:

```text id="stickynum"
1777
```

---

# 🛡️ umask

`umask` defines the **default permissions** assigned to newly created files and directories.

Check current umask:

```bash id="umask1"
umask
```

Example:

```text id="umaskex"
Default File Permission : 666

Umask : 022

Final Permission : 644
```

---

# 🌍 Real-World Analogy

Imagine an office.

* **Owner** → Cabin Owner
* **Group** → Department Team
* **Others** → Visitors

Permissions:

* Read → Can view documents.
* Write → Can edit documents.
* Execute → Can enter the office or run the program.

This is exactly how Linux controls access.

---

# ☁️ DevOps Perspective

Permission management is critical in DevOps.

Examples:

* SSH private keys must be `600`.
* Shell scripts require execute permission.
* Configuration files are usually `644`.
* Service users (nginx, mysql, jenkins) own their application files.
* Incorrect permissions can prevent services from starting.

---

# 🏭 Production Example

An application deployment fails:

```text id="err"
Permission denied
```

Investigation:

```bash id="lsperm"
ls -l deploy.sh
```

Output:

```text id="noperm"
-rw-r--r--
```

The script is missing execute permission.

Fix:

```bash id="fixperm"
chmod +x deploy.sh
```

Deployment succeeds.

---

# 🎯 Common Interview Questions

### What does `755` mean?

Owner: `rwx`

Group: `r-x`

Others: `r-x`

---

### What does `644` mean?

Owner:

```text id="644o"
rw-
```

Group:

```text id="644g"
r--
```

Others:

```text id="644ot"
r--
```

---

### Difference between `chmod`, `chown`, and `chgrp`?

* `chmod` → Change permissions.
* `chown` → Change owner.
* `chgrp` → Change group.

---

### Why does a directory need execute permission?

To enter (traverse) the directory.

---

### What is Sticky Bit?

Allows only the owner of a file to delete it in a shared directory.

---

### What is SUID?

Runs a program using the file owner's privileges.

---

### What is SGID?

Runs with the file group's privileges and can enforce group inheritance on directories.

---

# 🔍 Useful Commands

```bash id="cmds"
ls -l

chmod

chown

chgrp

stat

umask

getfacl

setfacl
```

---

# 📑 Interview Cheat Sheet

```text id="cheat"
Owner   Group   Others
  │        │        │
 rwx      r-x      r--

r = 4
w = 2
x = 1

755 = rwx r-x r-x
644 = rw- r-- r--
700 = rwx --- ---
600 = rw- --- ---
```

Remember:

* `chmod` → Permissions
* `chown` → Owner
* `chgrp` → Group
* Directory `x` = Traverse
* `umask` = Default permissions
* Sticky Bit protects shared directories
* SUID and SGID provide elevated execution behavior

---

# 📚 Summary

Linux File Permissions provide a robust security model by controlling access through **Owner**, **Group**, and **Others**, combined with **Read**, **Write**, and **Execute** permissions. Special permissions such as **SUID**, **SGID**, and **Sticky Bit** extend this model for advanced use cases.

For DevOps Engineers, mastering file permissions is essential for securing servers, troubleshooting "Permission Denied" errors, deploying applications, managing service accounts, and maintaining production systems.

---

# 🔗 Related Topics

⬅️ **Previous:** Users & Groups → `../05-Users-and-Groups/README.md`

➡️ **Next:** Processes & Services → `../07-Processes-and-Services/README.md`

### 📖 Recommended Reading

* Processes & Services
* Systemd & Systemctl
* Linux File System
* SSH & Remote Access
* Linux Troubleshooting
