# 🌐 CIDR & Subnetting

> **CIDR (Classless Inter-Domain Routing)** is a method of allocating IP addresses and dividing large networks into smaller, manageable subnetworks called **subnets**.
>
> In cloud platforms like **AWS**, **Azure**, and **Google Cloud**, CIDR and subnetting form the foundation of VPC networking. Every EC2 instance, Kubernetes node, Load Balancer, and database lives inside a subnet created from a CIDR block.

---

# 📖 Table of Contents

* What is CIDR?
* Why Do We Need CIDR?
* Problem It Solves
* Understanding IPv4
* CIDR Notation
* Network Bits vs Host Bits
* What is Subnetting?
* Public vs Private Subnets
* Route Tables and Internet Connectivity
* Real-World Analogy
* DevOps Perspective
* Production Example
* Production Decision
* Senior Engineer Tip
* Common Interview Questions
* Common Mistakes
* Troubleshooting Guide
* Interview Cheat Sheet
* Summary
* Related Topics

---

# ❓ What is CIDR?

**CIDR (Classless Inter-Domain Routing)** is a method of representing IP address ranges.

Instead of assigning individual IP addresses one by one, CIDR allows us to define an entire network using a single notation.

Example:

```text
10.0.0.0/16
```

This means:

* **10.0.0.0** → Network Address
* **/16** → First 16 bits belong to the network
* Remaining **16 bits** are available for hosts.

CIDR allows efficient IP allocation and routing.

---

# 🎯 Why Do We Need CIDR?

Imagine every router on the Internet storing billions of individual IP addresses.

Routing would become impossible.

CIDR allows routers to treat groups of IP addresses as a single network.

Instead of remembering:

```text
10.0.0.1
10.0.0.2
10.0.0.3
...
10.0.255.254
```

A router only remembers:

```text
10.0.0.0/16
```

This dramatically reduces routing complexity.

---

# ⚠️ Problem It Solves

CIDR solves several networking problems:

* Efficient IP address allocation
* Smaller routing tables
* Better scalability
* Easier subnet creation
* Flexible network design

Without CIDR, cloud networking would become difficult to manage.

---

# 🌍 Understanding IPv4

An IPv4 address contains **32 bits**.

Example:

```text
192.168.1.10
```

Each number is called an **octet**.

```
192      168      1      10
│         │       │       │
8 Bits   8 Bits  8 Bits  8 Bits
```

Total:

```
8 + 8 + 8 + 8 = 32 Bits
```

---

# 🏗️ CIDR Notation

CIDR uses the format:

```
IP Address / Prefix Length
```

Example:

```text
10.0.0.0/16
```

Meaning:

```
Network Bits : 16

Host Bits : 16
```

Available Host Addresses

```
2^16 = 65,536
```

Another example:

```text
10.0.1.0/24
```

```
Network Bits : 24

Host Bits : 8
```

Available Host Addresses

```
2^8 = 256
```

---

# 🧠 Network Bits vs Host Bits

Example:

```
10.0.1.0/24
```

```
10.0.1 | Host

Network = First 24 Bits

Host = Last 8 Bits
```

Network Bits identify the network.

Host Bits identify individual devices inside that network.

---

# 🌐 What is Subnetting?

Subnetting means dividing one large network into multiple smaller networks.

Example:

```
VPC

10.0.0.0/16

↓

Public Subnet

10.0.1.0/24

↓

Private Subnet

10.0.2.0/24

↓

Database Subnet

10.0.3.0/24
```

Instead of one giant network,

we create logical network boundaries.

---

# 🌎 Public vs Private Subnets

A common misconception is that a subnet becomes public or private automatically.

**It does not.**

A subnet becomes **public or private based on its Route Table**.

---

## Public Subnet

Route Table

```
0.0.0.0/0

↓

Internet Gateway (IGW)
```

Resources inside can directly access the Internet and can receive incoming Internet traffic if properly configured.

Examples:

* Load Balancer
* Bastion Host
* NAT Gateway

---

## Private Subnet

Route Table

```
0.0.0.0/0

↓

NAT Gateway
```

Resources cannot receive unsolicited inbound traffic from the Internet.

They can still initiate outbound connections.

Examples:

* EC2 Application Servers
* Kubernetes Worker Nodes
* Databases

---

# 🌐 Route Tables and Internet Connectivity

Every subnet is associated with exactly one Route Table.

A Route Table tells AWS where packets should go.

Example:

```
Destination

↓

Target
```

```
10.0.0.0/16

↓

Local
```

```
0.0.0.0/0

↓

Internet Gateway
```

or

```
0.0.0.0/0

↓

NAT Gateway
```

Routers always choose the **Longest Prefix Match**, meaning the most specific matching CIDR route.

---

# 🌍 Real-World Analogy

Imagine a city.

The city represents a VPC.

Each neighborhood represents a subnet.

Each house has its own address.

```
City

↓

Neighborhood

↓

Street

↓

House
```

Similarly,

```
VPC

↓

Subnet

↓

EC2 Instance
```

CIDR defines the city's boundaries,

while subnetting divides it into organized neighborhoods.

---

# ☁️ DevOps Perspective

CIDR and subnetting are fundamental in cloud infrastructure.

Common use cases include:

* AWS VPC
* Kubernetes Networking
* Docker Bridge Networks
* VPN Configuration
* Route Tables
* Security Groups
* NAT Gateway
* Internet Gateway

Without proper subnet planning,

applications become difficult to scale and secure.

---

# 🏭 Production Example

Suppose you're deploying an EKS cluster.

```
VPC

10.0.0.0/16

│
├── Public Subnet A
│      10.0.1.0/24
│
├── Public Subnet B
│      10.0.2.0/24
│
├── Private Subnet A
│      10.0.3.0/24
│
└── Private Subnet B
       10.0.4.0/24
```

* Application Load Balancer lives in the Public Subnets.
* Kubernetes Worker Nodes run inside the Private Subnets.
* Worker Nodes access the Internet through a NAT Gateway to pull container images.
* Internet users never communicate directly with the Worker Nodes.

This is the architecture recommended for production EKS deployments.

---

# 🚀 Production Decision

Use **larger CIDR blocks** for VPCs when future growth is expected.

Example:

```
10.0.0.0/16
```

instead of

```
10.0.0.0/24
```

Use **smaller subnet ranges** for logical separation.

Examples:

* Public Subnets
* Private Subnets
* Database Subnets
* Management Subnets

Never create overlapping CIDR ranges.

Always leave room for future expansion.

---

# 🧠 Senior Engineer Tip

A subnet is **not** public because it contains a public IP.

A subnet is public **only if its Route Table sends Internet traffic to an Internet Gateway**.

Similarly,

a private subnet is not defined by the absence of public IPs,

but by its routing configuration.

This distinction is frequently tested in AWS and DevOps interviews.

---

# 💼 Common Interview Questions

### Q1. What is CIDR?

A notation used to represent IP address ranges.

---

### Q2. Why do we use subnetting?

To divide one large network into smaller, manageable networks.

---

### Q3. What does `/24` mean?

The first 24 bits identify the network.

The remaining 8 bits are used for hosts.

---

### Q4. What makes a subnet public?

A Route Table containing:

```
0.0.0.0/0

↓

Internet Gateway
```

---

### Q5. Why do private subnets need a NAT Gateway?

Private resources often need outbound Internet access for:

* Pulling Docker images
* Downloading updates
* Calling AWS APIs

The NAT Gateway provides outbound connectivity while preventing unsolicited inbound Internet traffic.

---

### Q6. What is the difference between an Internet Gateway and a NAT Gateway?

Internet Gateway allows Internet connectivity for public resources.

NAT Gateway enables outbound Internet access for private resources.

---

# 🔥 Common Mistakes

❌ Every subnet with public IPs is public.

✅ Route Tables determine whether a subnet is public or private.

---

❌ CIDR and subnet are the same thing.

✅ CIDR defines the address range.

Subnetting divides that range into smaller networks.

---

❌ Private instances cannot access the Internet.

✅ They can access the Internet through a NAT Gateway.

---

❌ Overlapping CIDR ranges are acceptable.

✅ AWS does not allow overlapping CIDR ranges within a VPC.

---

# 🔍 Troubleshooting Guide

When networking issues occur:

1. Verify the CIDR ranges.
2. Check for overlapping subnets.
3. Confirm subnet associations.
4. Verify Route Tables.
5. Check Internet Gateway.
6. Check NAT Gateway.
7. Verify Security Groups.
8. Verify NACLs.
9. Test network connectivity.

Useful commands:

```bash
ip addr

ip route

traceroute

ping
```

---

# 💼 Interview Cheat Sheet

Remember:

```
/16

↓

65,536 Addresses
```

```
/24

↓

256 Addresses
```

Production Architecture

```
Internet

↓

Internet Gateway

↓

Public Subnet

↓

Load Balancer

↓

Private Subnet

↓

Application

↓

Database
```

---

# 📚 Summary

CIDR provides a flexible way to allocate IP address ranges, while subnetting divides those ranges into smaller, organized networks.

Together, they form the foundation of cloud networking and are essential for designing scalable, secure, and highly available infrastructures.

Every AWS VPC, Kubernetes cluster, Docker network, and enterprise cloud architecture relies on these concepts.

---

# 🔗 Related Topics

⬅️ Previous: **HTTP vs HTTPS** → `../06-HTTP-vs-HTTPS/README.md`

➡️ Next: **Route Tables** → `../08-Route-Tables/README.md`

### 📖 Recommended Reading

* TCP/IP Model
* Browser to Server Flow
* Internet Gateway
* NAT Gateway
* Security Groups vs NACLs
* AWS VPC Networking
