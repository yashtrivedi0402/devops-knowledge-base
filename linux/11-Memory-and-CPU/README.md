# 🧠 Linux Memory & CPU

> **CPU executes instructions, while Memory (RAM) temporarily stores the data and programs required by the CPU.**
>
> Together, CPU and Memory determine the performance of a Linux system. Monitoring their usage is one of the most important tasks for Linux administrators and DevOps engineers.

---

# 📖 Table of Contents

* What is CPU?
* What is Memory?
* Why Do We Need CPU & Memory?
* CPU & Memory Architecture
* CPU Scheduling
* Types of Memory
* Swap Memory
* Monitoring CPU & Memory
* Performance Metrics
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is CPU?

The **CPU (Central Processing Unit)** is the brain of the computer.

It is responsible for:

* Executing programs
* Processing instructions
* Performing calculations
* Managing system operations

Every application uses CPU cycles to perform tasks.

---

# ❓ What is Memory (RAM)?

**RAM (Random Access Memory)** is temporary storage used by the CPU to quickly access running programs and data.

Characteristics:

* Fast access
* Volatile (data is lost after shutdown)
* Stores running processes

---

# 🎯 Why Do We Need CPU & Memory?

CPU and Memory help Linux to:

* Run applications
* Execute multiple processes
* Improve system performance
* Handle multitasking
* Reduce execution time

Without RAM, the CPU cannot efficiently process programs.

---

# 🏗️ CPU & Memory Architecture

```text
           User
             │
             ▼
      Running Process
             │
             ▼
         CPU Executes
             │
             ▼
       Reads/Writes RAM
             │
             ▼
      Disk (Swap if Needed)
```

---

# ⚙️ CPU Scheduling

Linux uses the scheduler to decide **which process gets CPU time**.

Goals:

* Fair CPU allocation
* Efficient multitasking
* High performance
* Low response time

---

# 💾 Types of Memory

| Memory | Purpose                       |
| ------ | ----------------------------- |
| Cache  | Fastest memory inside CPU     |
| RAM    | Stores running applications   |
| Swap   | Backup space when RAM is full |
| Disk   | Permanent storage             |

---

# 🔄 Swap Memory

**Swap** is disk space used as virtual memory when RAM becomes full.

Advantages:

* Prevents system crashes
* Allows more applications to run

Disadvantage:

* Much slower than RAM

Check swap:

```bash
swapon --show
```

---

# 📊 Monitoring CPU & Memory

Check CPU and memory usage:

```bash
top
```

Interactive monitoring:

```bash
htop
```

Memory usage:

```bash
free -h
```

CPU information:

```bash
lscpu
```

Real-time statistics:

```bash
vmstat
```

---

# 📈 Performance Metrics

Important metrics:

* CPU Usage (%)
* Load Average
* Free Memory
* Used Memory
* Swap Usage
* Number of Running Processes

---

# ☁️ DevOps Perspective

CPU and Memory monitoring is essential for:

* Performance tuning
* Capacity planning
* Kubernetes resource limits
* Docker container monitoring
* Auto Scaling decisions
* Troubleshooting slow applications

Monitoring tools:

* Prometheus
* Grafana
* CloudWatch
* top / htop

---

# 🏭 Production Example

A web application becomes slow.

Investigation:

```bash
top
```

Find high CPU usage.

Check memory:

```bash
free -h
```

A process is consuming excessive CPU and RAM. Restart the application or optimize it to restore performance.

---

# 🎯 Common Interview Questions

### What is RAM?

Temporary memory used to store running programs and data.

---

### What is Swap?

Disk space used as virtual memory when RAM is exhausted.

---

### Difference between RAM and Swap?

* RAM → Fast, temporary memory.
* Swap → Disk-based virtual memory, slower than RAM.

---

### Which command checks memory usage?

```bash
free -h
```

---

### Which command displays CPU information?

```bash
lscpu
```

---

### Which command monitors CPU usage in real time?

```bash
top
```

or

```bash
htop
```

---

# 🔍 Useful Commands

```bash
top

htop

free -h

lscpu

vmstat

uptime

cat /proc/cpuinfo

cat /proc/meminfo

swapon --show
```

---

# 📑 Interview Cheat Sheet

```text
Application
      │
      ▼
     CPU
      │
      ▼
     RAM
      │
      ▼
   Swap (if RAM Full)
      │
      ▼
     Disk
```

Remember:

* CPU executes instructions.
* RAM stores running programs.
* Swap is slower than RAM.
* `top` → CPU & Memory usage.
* `free -h` → Memory information.
* `lscpu` → CPU details.
* High CPU = Busy processor.
* High Swap = Low available RAM.

---

# 📚 Summary

The **CPU** processes instructions, while **Memory (RAM)** stores the data needed by running applications. Linux uses **Swap** as additional virtual memory when RAM is insufficient. Monitoring CPU, memory, and swap usage helps maintain system performance and stability.

For DevOps Engineers, understanding CPU and memory utilization is crucial for troubleshooting performance issues, monitoring infrastructure, optimizing applications, and scaling production workloads.

---

# 🔗 Related Topics

⬅️ **Previous:** Storage & Disks → `../10-Storage-and-Disks/README.md`

➡️ **Next:** Networking in Linux → `../12-Networking-in-Linux/README.md`

### 📖 Recommended Reading

* Networking in Linux
* Processes & Services
* Logs & Monitoring
* Linux Troubleshooting
* End-to-End Linux Flow
