# 🌐 Linux Networking

> **Linux Networking is the set of tools, protocols, and configurations that allow a Linux system to communicate with other systems over a network.**
>
> Networking is essential for accessing the internet, connecting servers, hosting applications, and enabling communication between services.

---

# 📖 Table of Contents

* What is Linux Networking?
* Why Do We Need Networking?
* Networking Architecture
* Network Components
* IP Address
* Ports & Protocols
* DNS
* Routing
* Network Interfaces
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Linux Networking?

Linux Networking enables a system to:

* Connect to the internet
* Communicate with other servers
* Host web applications
* Transfer files
* Access cloud resources

Every server in production relies on networking.

---

# 🎯 Why Do We Need Networking?

Networking helps Linux to:

* Exchange data
* Access remote systems
* Host websites
* Connect databases
* Enable cloud communication
* Support distributed applications

---

# 🏗️ Networking Architecture

```text
User
 │
 ▼
Application
 │
 ▼
TCP / UDP
 │
 ▼
IP Layer
 │
 ▼
Network Interface (eth0)
 │
 ▼
Router / Switch
 │
 ▼
Internet / Other Servers
```

---

# 🌍 Network Components

| Component   | Purpose                     |
| ----------- | --------------------------- |
| IP Address  | Identifies a device         |
| MAC Address | Hardware address            |
| Gateway     | Connects different networks |
| DNS         | Resolves domain names       |
| Router      | Routes network traffic      |
| Switch      | Connects devices in a LAN   |

---

# 📍 IP Address

An **IP Address** uniquely identifies a device on a network.

Types:

* IPv4
* IPv6

Example:

```text
192.168.1.10
```

View IP address:

```bash
ip addr
```

---

# 🚪 Ports & Protocols

A **Port** identifies a specific service running on a system.

Common ports:

| Port | Service    |
| ---- | ---------- |
| 22   | SSH        |
| 80   | HTTP       |
| 443  | HTTPS      |
| 3306 | MySQL      |
| 5432 | PostgreSQL |
| 6379 | Redis      |

---

# 🌍 DNS (Domain Name System)

DNS converts domain names into IP addresses.

Example:

```text
google.com
      │
      ▼
142.x.x.x
```

Check DNS:

```bash
nslookup google.com
```

or

```bash
dig google.com
```

---

# 🛣️ Routing

Routing decides where network packets should travel.

View routing table:

```bash
ip route
```

Default gateway example:

```text
default via 192.168.1.1
```

---

# 🔌 Network Interfaces

A network interface connects Linux to a network.

Examples:

```text
eth0
ens33
wlan0
lo
```

View interfaces:

```bash
ip link
```

---

# ☁️ DevOps Perspective

Linux networking is required for:

* SSH access
* Docker networking
* Kubernetes communication
* Load Balancers
* API communication
* Monitoring tools
* Cloud infrastructure

---

# 🏭 Production Example

A website is unreachable.

Troubleshooting steps:

```bash
ping google.com
```

Check IP:

```bash
ip addr
```

Check routes:

```bash
ip route
```

Check listening ports:

```bash
ss -tuln
```

Verify DNS:

```bash
nslookup example.com
```

These steps help identify whether the issue is related to connectivity, routing, DNS, or the application itself.

---

# 🎯 Common Interview Questions

### What is an IP Address?

A unique address used to identify a device on a network.

---

### Difference between IPv4 and IPv6?

* IPv4 → 32-bit addressing.
* IPv6 → 128-bit addressing with a much larger address space.

---

### What is DNS?

A service that converts domain names into IP addresses.

---

### What is a Port?

A logical endpoint used by applications to communicate over a network.

---

### Which command displays IP addresses?

```bash
ip addr
```

---

### Which command shows the routing table?

```bash
ip route
```

---

# 🔍 Useful Commands

```bash
ip addr

ip link

ip route

ping

ss -tuln

netstat -tuln

nslookup

dig

traceroute

hostname
```

---

# 📑 Interview Cheat Sheet

```text
Application
      │
      ▼
TCP / UDP
      │
      ▼
IP Address
      │
      ▼
Network Interface
      │
      ▼
Router
      │
      ▼
Internet
```

Remember:

* `ip addr` → Show IP addresses
* `ip route` → Show routing table
* `ss -tuln` → Show listening ports
* `ping` → Test connectivity
* `nslookup` / `dig` → Check DNS
* Port **22** → SSH
* Port **80** → HTTP
* Port **443** → HTTPS

---

# 📚 Summary

Linux Networking enables communication between systems using network interfaces, IP addresses, ports, routing, and DNS. It forms the foundation of server communication, cloud infrastructure, and distributed applications.

For DevOps Engineers, networking is a core skill required for deploying applications, troubleshooting connectivity issues, managing cloud resources, configuring load balancers, and maintaining reliable production environments.

---

# 🔗 Related Topics

⬅️ **Previous:** Memory & CPU → `../11-Memory-and-CPU/README.md`

➡️ **Next:** Logs & Monitoring → `../13-Logs-and-Monitoring/README.md`

### 📖 Recommended Reading

* Logs & Monitoring
* SSH & Remote Access
* Linux Troubleshooting
* End-to-End Linux Flow
* Networking Knowledge Base
