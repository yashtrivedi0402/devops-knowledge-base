# 🔐 Security Groups vs Network ACLs (NACLs)

> **Security Groups (SGs) and Network Access Control Lists (NACLs) are two layers of security used in AWS VPC networking.**
>
> Both are responsible for controlling network traffic, but they operate at different levels and behave differently.
>
> Understanding the difference between them is one of the **most frequently asked AWS and DevOps interview topics**.

---

# 📖 Table of Contents

* What are Security Groups?
* What are NACLs?
* Why Do We Need Both?
* Problem They Solve
* Security Groups vs NACLs
* How Security Groups Work
* How NACLs Work
* Stateful vs Stateless
* Traffic Flow
* Real-World Analogy
* DevOps Perspective
* Production Example
* Real Interview Scenario
* Production Decision
* Senior Engineer Tip
* Common Interview Questions
* Common Mistakes
* Troubleshooting Guide
* Commands to Verify
* Interview Cheat Sheet
* Summary
* Related Topics

---

# ❓ What are Security Groups?

A **Security Group (SG)** is a **virtual firewall** that protects AWS resources such as:

* EC2 Instances
* Application Load Balancers
* RDS
* ECS Tasks
* EKS Worker Nodes

A Security Group controls **which traffic is allowed** to reach a resource.

> **Security Groups only contain ALLOW rules.**
>
> There are **no DENY rules**.

---

# ❓ What is a Network ACL (NACL)?

A **Network Access Control List (NACL)** is a firewall that operates at the **Subnet Level**.

Instead of protecting individual instances,

it protects the **entire subnet**.

Unlike Security Groups,

NACLs support both:

* ✅ ALLOW Rules
* ❌ DENY Rules

---

# 🎯 Why Do We Need Both?

Imagine a company building.

The building has:

* A main entrance gate
* Security guards outside each office

The entrance gate protects the **entire building**.

The office guard protects **individual offices**.

AWS follows the same layered approach.

---

# ⚠️ Problem They Solve

Without network security:

* Anyone could access your servers.
* Databases could be exposed.
* SSH ports could remain open to the Internet.
* Malware could spread between resources.

Security Groups and NACLs work together to reduce this risk.

---

# 🏗️ Architecture

```text
                   Internet
                       │
                Internet Gateway
                       │
                 Public Route Table
                       │
                Public Subnet
                       │
             Network ACL (Subnet)
                       │
             Security Group (EC2)
                       │
                  EC2 Instance
```

Traffic reaches the **NACL first**, then the **Security Group**.

---

# 📊 Security Groups vs NACLs

| Feature          | Security Group               | Network ACL              |
| ---------------- | ---------------------------- | ------------------------ |
| Level            | Instance / ENI               | Subnet                   |
| Type             | Virtual Firewall             | Subnet Firewall          |
| Rules            | Allow Only                   | Allow + Deny             |
| Stateful         | ✅ Yes                        | ❌ No                     |
| Stateless        | ❌ No                         | ✅ Yes                    |
| Rule Order       | Doesn't Matter               | Lowest Rule Number First |
| Applies To       | EC2, ALB, RDS, ENI           | Entire Subnet            |
| Default Behavior | Deny Inbound, Allow Outbound | Depends on Rules         |

---

# ⚙️ How Security Groups Work

Suppose:

```text
SSH

Port 22

Allowed From

203.0.113.10/32
```

Only that IP can establish an SSH connection.

If SSH is allowed inbound,

the response traffic is automatically allowed outbound.

This happens because Security Groups are **Stateful**.

---

# ⚙️ How NACLs Work

Example

Inbound Rules

```text
100 → Allow Port 80

110 → Allow Port 443

120 → Deny All
```

Outbound Rules

```text
100 → Allow All
```

NACLs evaluate rules from the **lowest rule number**.

The first matching rule wins.

---

# 🔄 Stateful vs Stateless

This is one of the most important interview concepts.

## Security Group (Stateful)

Suppose:

Client

↓

HTTPS

↓

EC2

If:

```text
Inbound

443

Allowed
```

AWS automatically allows the response back.

You do **not** need another outbound rule for the response.

---

## NACL (Stateless)

NACLs remember nothing.

If:

```text
Inbound

443

Allowed
```

You must also allow:

```text
Outbound

Ephemeral Ports
```

Otherwise,

the response packet will be dropped.

---

# 🌍 Traffic Flow

```text
Internet

↓

Internet Gateway

↓

Route Table

↓

Network ACL

↓

Security Group

↓

EC2 Instance
```

Response follows the same path in reverse.

---

# 🌍 Real-World Analogy

Imagine an airport.

### Network ACL

Airport security at the entrance.

Everyone entering or leaving the airport must pass through it.

---

### Security Group

Security at the boarding gate.

Only passengers for that specific flight are allowed through.

This layered security protects both the airport and individual flights.

---

# ☁️ DevOps Perspective

You'll configure Security Groups almost daily.

Examples:

* EC2
* RDS
* ALB
* EKS Worker Nodes
* ECS Services
* Bastion Hosts

NACLs are typically configured when:

* Security teams require subnet-level protection.
* Explicit deny rules are needed.
* Compliance standards demand additional security layers.

---

# 🏭 Production Example

A production web application:

```text
Internet

↓

Internet Gateway

↓

Application Load Balancer

↓

Security Group

↓

Private Subnet

↓

NACL

↓

Application Server

↓

Database
```

Typical rules:

ALB Security Group

* Allow 443 from Internet

Application Security Group

* Allow 8080 only from ALB Security Group

Database Security Group

* Allow 3306 only from Application Security Group

This ensures that only trusted components communicate with each other.

---

# 🎯 Real Interview Scenario

### Scenario

Users cannot access your web application.

The Application Load Balancer is healthy,

but requests are timing out.

How would you troubleshoot?

### Solution

Check in this order:

1. Route Table
2. Internet Gateway
3. Security Group
4. Network ACL
5. Target Group
6. Application Logs

Suppose:

Security Group allows:

```text
443
```

But the NACL denies:

```text
443
```

The packet is dropped before reaching the EC2 instance.

Similarly,

if inbound traffic is allowed but outbound ephemeral ports are blocked in the NACL,

responses will never reach the client.

---

# 🚀 Production Decision

Use **Security Groups** for most application-level access control.

Examples:

* Allow ALB → EC2
* Allow EC2 → Database
* Allow Bastion → EC2
* Allow Jenkins → Kubernetes

Use **NACLs** when:

* Explicit DENY rules are required.
* Protecting an entire subnet.
* Implementing additional defense-in-depth.
* Meeting compliance requirements.

AWS best practice:

> Keep Security Groups as the primary access control mechanism.
>
> Use NACLs as an additional security layer.

---

# 🧠 Senior Engineer Tip

Many beginners think:

> "Security Groups and NACLs do the same thing."

They don't.

Remember:

* **Security Groups protect resources.**
* **NACLs protect subnets.**

Also remember:

> Security Groups are **Stateful**.

> NACLs are **Stateless**.

This distinction appears in almost every AWS interview.

---

# 💼 Common Interview Questions

### Q1. What is the difference between Security Groups and NACLs?

Security Groups operate at the instance level.

NACLs operate at the subnet level.

---

### Q2. Which one is Stateful?

Security Groups.

---

### Q3. Which one is Stateless?

Network ACLs.

---

### Q4. Which one supports DENY rules?

Only NACLs.

---

### Q5. Which one evaluates rules in order?

NACLs.

The first matching rule wins.

---

### Q6. Can multiple Security Groups be attached to one EC2?

Yes.

An EC2 instance can have multiple Security Groups.

---

### Q7. Why do NACLs require outbound rules?

Because they are stateless.

Every request and response must be explicitly allowed.

---

# 🔥 Common Mistakes

❌ Security Groups support DENY rules.

✅ They support only ALLOW rules.

---

❌ NACLs remember previous connections.

✅ NACLs are stateless.

---

❌ Rule order matters in Security Groups.

✅ Rule order does **not** matter.

---

❌ NACLs replace Security Groups.

✅ Both should be used together.

---

# 🔍 Troubleshooting Guide

If traffic is blocked:

1. Check Route Table.
2. Verify Internet Gateway or NAT Gateway.
3. Check Security Group rules.
4. Check NACL rules.
5. Verify outbound ephemeral ports.
6. Confirm subnet association.
7. Verify application is listening on the correct port.
8. Check OS firewall (iptables, firewalld, ufw).
9. Review application logs.

---

# 💻 Commands to Verify

AWS CLI

```bash
aws ec2 describe-security-groups

aws ec2 describe-network-acls

aws ec2 describe-network-interfaces
```

Linux

```bash
ss -tulnp

iptables -L

sudo ufw status

sudo firewall-cmd --list-all
```

---

# 💼 Interview Cheat Sheet

Remember:

```text
Internet

↓

Route Table

↓

Network ACL

↓

Security Group

↓

EC2
```

Key Facts

| Security Group            | NACL               |
| ------------------------- | ------------------ |
| Instance Level            | Subnet Level       |
| Stateful                  | Stateless          |
| Allow Only                | Allow + Deny       |
| Rule Order Doesn't Matter | Rule Order Matters |

---

# 📚 Summary

Security Groups and Network ACLs work together to secure AWS networking.

Security Groups provide **instance-level, stateful protection**, making them the primary access control mechanism for AWS resources.

Network ACLs provide **subnet-level, stateless protection**, offering an additional layer of security with both allow and deny rules.

Understanding when and how to use each one is essential for building secure, production-ready cloud infrastructure.

---

# 🔗 Related Topics

⬅️ Previous: **NAT Gateway** → `../10-NAT-Gateway/README.md`

➡️ Next: **Load Balancers** → `../12-Load-Balancers/README.md`

### 📖 Recommended Reading

* Route Tables
* Internet Gateway
* NAT Gateway
* AWS VPC
* Load Balancers
* Browser to Server Flow
