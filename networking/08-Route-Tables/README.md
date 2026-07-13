# 🛣️ AWS Route Tables

> **A Route Table is a set of rules that tells AWS where network traffic should go.**
>
> Every subnet inside a VPC is associated with a Route Table. Whenever a packet leaves an EC2 instance, Kubernetes node, or any AWS resource, the Route Table decides its next destination.
>
> **Without Route Tables, resources inside a VPC would have no idea where to send network traffic.**

---

# 📖 Table of Contents

* What is a Route Table?
* Why Do We Need Route Tables?
* Problem It Solves
* Route Table Architecture
* How Route Tables Work
* Longest Prefix Match
* Route Table Components
* Public vs Private Route Tables
* Real-World Analogy
* DevOps Perspective
* Production Example
* Real Interview Scenario
* Production Decision
* Senior Engineer Tip
* Common Interview Questions
* Common Mistakes
* Troubleshooting Guide
* Interview Cheat Sheet
* Summary
* Related Topics

---

# ❓ What is a Route Table?

A **Route Table** is a collection of routing rules.

Each rule answers one question:

> **"If a packet is going to this destination, where should I send it?"**

Every packet leaving a subnet is matched against the Route Table.

AWS then forwards the packet to the correct destination.

---

# 🎯 Why Do We Need Route Tables?

Imagine sending a parcel without knowing which road to take.

Even if you know the destination,

you still need directions.

Similarly,

an EC2 instance knows the destination IP,

but it still needs instructions on **where to send the packet next**.

Route Tables provide those directions.

---

# ⚠️ Problem It Solves

Without Route Tables:

* Packets would never leave a subnet.
* Public resources couldn't access the Internet.
* Private resources couldn't reach NAT Gateways.
* Communication between subnets would fail.
* Applications inside a VPC couldn't communicate correctly.

---

# 🏗️ Route Table Architecture

```text
                VPC (10.0.0.0/16)

        ┌────────────────────────────┐
        │                            │
        │     Route Table            │
        │                            │
        │ Destination    Target      │
        │ 10.0.0.0/16 → Local        │
        │ 0.0.0.0/0   → IGW          │
        │                            │
        └─────────────┬──────────────┘
                      │
                Public Subnet
                      │
                   EC2 Instance
```

Every subnet is associated with one Route Table.

---

# ⚙️ How Route Tables Work

Suppose an EC2 instance wants to access:

```text
https://google.com
```

The packet leaves the EC2 instance.

↓

AWS checks the Route Table.

↓

Destination:

```text
0.0.0.0/0
```

↓

Target:

```text
Internet Gateway
```

↓

The packet is forwarded to the Internet Gateway.

↓

The Internet Gateway sends it to the Internet.

---

# 📌 Route Table Components

Every Route Table consists of:

| Destination | Target   |
| ----------- | -------- |
| CIDR Block  | Next Hop |

Example:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

---

# 🌐 Default Local Route

Every VPC automatically creates this route:

| Destination | Target |
| ----------- | ------ |
| 10.0.0.0/16 | Local  |

This allows all subnets inside the VPC to communicate with each other.

Without this route,

resources inside the same VPC couldn't communicate.

---

# 🌍 Longest Prefix Match

AWS always chooses the **most specific matching route**.

Example:

```text
Destination          Target

10.0.1.0/24    → NAT Gateway

10.0.0.0/16    → Local

0.0.0.0/0      → Internet Gateway
```

Suppose the packet is going to:

```text
10.0.1.45
```

AWS chooses:

```text
10.0.1.0/24
```

instead of

```text
10.0.0.0/16
```

because `/24` is more specific.

This rule is called **Longest Prefix Match**.

---

# 🌐 Public Route Table

A Route Table becomes **Public** when it contains:

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

Resources inside the subnet can directly communicate with the Internet.

Typical resources:

* Bastion Host
* Load Balancer
* NAT Gateway

---

# 🔒 Private Route Table

A Route Table becomes **Private** when Internet-bound traffic is forwarded to:

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

Resources inside the subnet cannot receive direct inbound Internet traffic.

Examples:

* Kubernetes Worker Nodes
* EC2 Application Servers
* Databases

---

# 🌍 Real-World Analogy

Imagine Google Maps.

You enter a destination.

Google Maps decides:

* Which road to take.
* Which highway to use.
* Which turn to make.

A Route Table performs exactly the same task.

It decides the next path for every packet.

---

# ☁️ DevOps Perspective

Every cloud architecture depends on Route Tables.

Examples:

* AWS VPC
* EKS Networking
* ECS
* Public Subnets
* Private Subnets
* Internet Gateway
* NAT Gateway
* Transit Gateway
* VPN

Understanding Route Tables is essential for troubleshooting production networking.

---

# 🏭 Production Example

A production web application:

```text
Internet

↓

Internet Gateway

↓

Public Route Table

↓

Application Load Balancer

↓

Private Route Table

↓

Kubernetes Worker Nodes

↓

Database
```

The Public Route Table allows Internet traffic.

The Private Route Table sends outbound traffic through a NAT Gateway.

---

# 🎯 Real Interview Scenario

**Scenario**

Your Kubernetes Worker Node is deployed inside a Private Subnet.

It needs to pull a Docker image from Docker Hub.

Walk through the networking flow.

### Solution

1. Worker Node sends an HTTPS request.
2. Private Route Table checks the destination.
3. The rule:

```text
0.0.0.0/0 → NAT Gateway
```

matches.

4. Packet reaches the NAT Gateway.
5. NAT Gateway performs Source NAT (SNAT).
6. Public Route Table forwards traffic to the Internet Gateway.
7. Internet Gateway sends the packet to Docker Hub.
8. Docker Hub responds to the NAT Gateway's public IP.
9. NAT Gateway translates the packet back to the Worker Node.
10. The image is downloaded successfully.

---

# 🚀 Production Decision

Use separate Route Tables for different subnet types.

Example:

* Public Route Table
* Private Route Table
* Database Route Table
* Management Route Table

This improves:

* Security
* Isolation
* Scalability
* Troubleshooting

Never use one Route Table for every subnet in a production environment.

---

# 🧠 Senior Engineer Tip

Many beginners think:

> "A subnet becomes public because resources have public IPs."

This is incorrect.

A subnet becomes public **only if its Route Table contains a route to an Internet Gateway**.

Similarly,

a private subnet is determined by its routing configuration, not simply by the absence of public IP addresses.

---

# 💼 Common Interview Questions

### Q1. What is a Route Table?

A Route Table is a collection of routing rules that determine where packets should be forwarded.

---

### Q2. What is the default route in every VPC?

```text
Destination

10.0.0.0/16

↓

Target

Local
```

---

### Q3. What makes a Route Table public?

A route like:

```text
0.0.0.0/0 → Internet Gateway
```

---

### Q4. What makes a Route Table private?

A route like:

```text
0.0.0.0/0 → NAT Gateway
```

---

### Q5. What is Longest Prefix Match?

When multiple routes match a destination,

AWS chooses the **most specific route**.

---

### Q6. Can multiple subnets use one Route Table?

Yes.

Multiple subnets can share the same Route Table.

However, production environments often use different Route Tables for different subnet types.

---

# 🔥 Common Mistakes

❌ Thinking every subnet automatically has Internet access.

✅ Internet access depends on the Route Table.

---

❌ Thinking Route Tables perform firewall functions.

✅ Route Tables decide **where** traffic goes.

Security Groups and NACLs decide **whether** traffic is allowed.

---

❌ Forgetting the Local Route.

✅ Every VPC automatically includes a Local Route.

---

❌ Believing Route Tables inspect packets.

✅ Route Tables only determine the next hop.

They do not inspect or filter traffic.

---

# 🔍 Troubleshooting Guide

When connectivity fails:

1. Verify the subnet association.
2. Check the Route Table.
3. Verify the Local Route.
4. Check Internet Gateway attachment.
5. Check NAT Gateway availability.
6. Verify Security Groups.
7. Verify NACL rules.
8. Confirm destination CIDR.
9. Test connectivity.

Useful commands:

```bash
ip route

traceroute

curl

ping
```

---

# 💼 Interview Cheat Sheet

Remember these routes:

```text
10.0.0.0/16

↓

Local
```

```text
0.0.0.0/0

↓

Internet Gateway
```

```text
0.0.0.0/0

↓

NAT Gateway
```

Remember:

* Route Tables decide **where** traffic goes.
* Security Groups decide **whether** traffic is allowed.
* NACLs decide **whether** subnet-level traffic is allowed.

---

# 📚 Summary

Route Tables are the decision-makers of AWS networking.

Every packet leaving a subnet is evaluated against a Route Table, which determines the next hop based on destination CIDR and the **Longest Prefix Match** rule.

A solid understanding of Route Tables is essential for designing, troubleshooting, and securing cloud infrastructure.

---

# 🔗 Related Topics

⬅️ Previous: **CIDR & Subnetting** → `../07-CIDR-Subnetting/README.md`

➡️ Next: **Internet Gateway** → `../09-Internet-Gateway/README.md`

### 📖 Recommended Reading

* CIDR & Subnetting
* Internet Gateway
* NAT Gateway
* Security Groups vs NACLs
* AWS VPC
* Kubernetes Networking
