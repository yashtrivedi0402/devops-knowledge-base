# 🐚 Linux Shell Scripting Basics

> **Shell Scripting is the process of writing a series of Linux commands in a file to automate repetitive tasks.**
>
> Instead of executing commands one by one, a shell script runs them automatically, making system administration and DevOps workflows faster, consistent, and less error-prone.

---

# 📖 Table of Contents

* What is Shell Scripting?
* Why Do We Need It?
* Shell Script Architecture
* Creating Your First Script
* Variables
* User Input
* Conditional Statements
* Loops
* Functions
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Shell Scripting?

A **Shell Script** is a text file containing Linux commands that are executed by the shell.

Common shell:

```text
Bash (Bourne Again Shell)
```

File extension:

```text
.sh
```

Example:

```bash
#!/bin/bash

echo "Hello, Linux!"
```

---

# 🎯 Why Do We Need Shell Scripting?

Shell scripts help to:

* Automate repetitive tasks
* Reduce manual effort
* Save time
* Improve consistency
* Automate deployments
* Manage servers efficiently

---

# 🏗️ Shell Script Architecture

```text
User
 │
 ▼
Shell Script (.sh)
 │
 ▼
Bash Shell
 │
 ▼
Linux Kernel
 │
 ▼
System Resources
```

---

# 🚀 Creating Your First Script

Create a file:

```bash
touch hello.sh
```

Edit it:

```bash
nano hello.sh
```

Script:

```bash
#!/bin/bash

echo "Hello World"
```

Give execute permission:

```bash
chmod +x hello.sh
```

Run:

```bash
./hello.sh
```

---

# 📦 Variables

Variables store values.

Example:

```bash
#!/bin/bash

name="Yash"

echo "Welcome $name"
```

---

# ⌨️ User Input

Read input from the user.

```bash
#!/bin/bash

read -p "Enter your name: " name

echo "Hello $name"
```

---

# 🔀 Conditional Statements

Execute code based on a condition.

Example:

```bash
#!/bin/bash

age=20

if [ $age -ge 18 ]
then
    echo "Adult"
else
    echo "Minor"
fi
```

---

# 🔁 Loops

### For Loop

```bash
for i in {1..5}
do
    echo $i
done
```

### While Loop

```bash
count=1

while [ $count -le 5 ]
do
    echo $count
    count=$((count+1))
done
```

---

# ⚙️ Functions

Functions help reuse code.

```bash
#!/bin/bash

greet(){
    echo "Welcome to Linux"
}

greet
```

---

# ☁️ DevOps Perspective

Shell scripting is widely used for:

* Server automation
* User management
* Backup scripts
* Log cleanup
* Health checks
* CI/CD pipelines
* Cron jobs
* Docker automation

Almost every DevOps Engineer writes shell scripts.

---

# 🏭 Production Example

A server's disk usage is checked every day.

Script:

```bash
#!/bin/bash

df -h

free -h

uptime
```

Schedule using **cron** to run automatically every morning and notify the administrator if disk usage exceeds a threshold.

---

# 🎯 Common Interview Questions

### What is Shell Scripting?

Writing Linux commands in a file to automate tasks.

---

### What is Bash?

The default shell in most Linux distributions.

---

### Why is `#!/bin/bash` used?

It tells Linux to execute the script using the Bash interpreter.

---

### How do you make a script executable?

```bash
chmod +x script.sh
```

---

### How do you run a script?

```bash
./script.sh
```

or

```bash
bash script.sh
```

---

# 🔍 Useful Commands

```bash
bash

chmod +x

echo

read

if

for

while

function

exit
```

---

# 📑 Interview Cheat Sheet

```text
Write Script
      │
      ▼
Save (.sh)
      │
      ▼
chmod +x
      │
      ▼
Run Script
      │
      ▼
Automation
```

Remember:

* `.sh` → Shell Script
* `#!/bin/bash` → Bash Interpreter
* `chmod +x` → Make executable
* `./script.sh` → Execute script
* Variables → Store data
* Loops → Repeat tasks
* Functions → Reuse code

---

# 📚 Summary

Shell Scripting is one of the most powerful Linux skills for automating repetitive tasks and managing systems efficiently. By combining commands, variables, conditions, loops, and functions, administrators can create reusable automation for everyday operations.

For DevOps Engineers, shell scripting is a fundamental skill used in server provisioning, CI/CD pipelines, monitoring, backups, deployments, and infrastructure automation.

---

# 🔗 Related Topics

⬅️ **Previous:** Logs & Monitoring → `../13-Logs-and-Monitoring/README.md`

➡️ **Next:** SSH & Remote Access → `../15-SSH-and-Remote-Access/README.md`

### 📖 Recommended Reading

* SSH & Remote Access
* Linux Commands
* Linux Troubleshooting
* End-to-End Linux Flow
* Bash Documentation
