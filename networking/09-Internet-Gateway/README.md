# 🌐 Internet Gateway (IGW)

> **An Internet Gateway (IGW) is a highly available AWS-managed networking component that enables communication between resources inside a VPC and the public Internet.**
>
> An Internet Gateway does **not** automatically make a subnet public. A subnet becomes public only when its **Route Table** contains a route directing Internet traffic (`0.0.0.0/0`) to the Internet Gateway.

---

# 📖 Table of Contents

* What is an Internet Gateway?
* Why Do We Need It?
* Problem It Solves
* Internet Gateway Architecture
* How Internet Gateway Works
* Public Subnet vs Private Subnet
* Internet Gateway vs NAT Gateway
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

# ❓ What is an Internet Gateway?

An **Internet Gateway (IGW)** is an AWS-managed networking component that connects a **Virtual Private Cloud (VPC)** to the public Internet.

Think of it as the **main entrance and exit** of your AWS VPC.

Without an Internet Gateway, resources inside the VPC cannot communicate with the Internet.

However,

simply creating an Internet Gateway **does not provide Internet access**.

It must be:

* Attached to a VPC.
* Referenced in the Route Table.

---

# 🎯 Why Do We Need an Internet Gateway?

Imagine your office building has no entrance door.

Employees cannot go outside.

Visitors cannot enter.

Similarly,

without an Internet Gateway,

resources inside a VPC cannot communicate with external networks.

The Internet Gateway provides this connectivity.

---

# ⚠️ Problem It Solves

Without an Internet Gateway:

* Public websites cannot be accessed.
* Users cannot connect to public EC2 instances.
* Load Balancers cannot receive requests.
* Bastion Hosts cannot be accessed via SSH.
* Public APIs cannot be exposed.

The Internet Gateway solves these connectivity problems.

---

# 🏗️ Internet Gateway Architecture

```text
                    Internet
                        │
                        │
               Internet Gateway
                        │
        ┌───────────────┴───────────────┐
        │                               │
      Route Table                 Route Table
        │                               │
 Public Subnet                  Private Subnet
        │                               │
    EC2 / ALB                    EC2 / EKS Node
```

Notice:

Only the subnet whose Route Table points to the Internet Gateway becomes public.

---

# ⚙️ How Internet Gateway Works

Suppose an EC2 instance in a public subnet wants to access:

```text
https://google.com
```

The networking flow is:

```text
EC2 Instance

↓

Subnet

↓

Route Table

↓

0.0.0.0/0 → Internet Gateway

↓

Internet Gateway

↓

Internet

↓

Google Server

↓

Response

↓

Internet Gateway

↓

EC2 Instance
```

The Internet Gateway allows communication in **both directions**.

---

# 🌐 Public Subnet vs Private Subnet

## Public Subnet

A subnet is public when:

```text
Route Table

↓

0.0.0.0/0

↓

Internet Gateway
```

Resources can:

* Access the Internet.
* Receive Internet traffic (if Security Groups permit).

Examples:

* Bastion Host
* Application Load Balancer
* NAT Gateway
* Public EC2

---

## Private Subnet

A subnet is private when:

```text
Route Table

↓

0.0.0.0/0

↓

NAT Gateway
```

Resources:

* Cannot receive unsolicited Internet traffic.
* Can still initiate outbound Internet connections through the NAT Gateway.

Examples:

* Kubernetes Worker Nodes
* Databases
* Backend APIs

---

# 🔄 Internet Gateway vs NAT Gateway

| Feature                   | Internet Gateway  | NAT Gateway                |
| ------------------------- | ----------------- | -------------------------- |
| Used With                 | Public Subnet     | Private Subnet             |
| Public IP Required        | Yes               | Yes (NAT itself has one)   |
| Incoming Internet Traffic | Yes               | No                         |
| Outgoing Internet Traffic | Yes               | Yes                        |
| Translation               | No                | Performs Source NAT (SNAT) |
| Typical Resources         | ALB, Bastion Host | Private EC2, EKS Nodes     |

---

# 🌍 Real-World Analogy

Imagine an apartment building.

The **main gate** is the Internet Gateway.

Residents can:

* Leave the building.
* Visitors can enter (if security allows).

Private apartments inside the building are still protected by security guards (Security Groups).

The gate only provides access—it doesn't decide who is allowed inside.

---

# ☁️ DevOps Perspective

Internet Gateways are used in almost every production AWS architecture.

Examples:

* Public Web Servers
* Application Load Balancers
* Bastion Hosts
* Reverse Proxies
* Public APIs
* Kubernetes Ingress Controllers

Whenever an application must be accessible from the Internet,

an Internet Gateway is involved.

---

# 🏭 Production Example

Typical AWS Architecture

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

Users communicate only with the Load Balancer.

Application servers remain protected inside private subnets.

---

# 🎯 Real Interview Scenario

### Scenario

Your company deploys an Application Load Balancer in a public subnet.

Users cannot access the application from the Internet.

What would you check?

### Solution

Check in this order:

1. Is an Internet Gateway attached to the VPC?
2. Does the public subnet's Route Table contain:

```text
0.0.0.0/0 → Internet Gateway
```

3. Does the Load Balancer have a public IP/DNS?
4. Are the Security Groups allowing inbound traffic?
5. Are the NACL rules correct?
6. Are the Target Groups healthy?
7. Is the application running?

Never assume the problem is the application.

Always verify networking first.

---

# 🚀 Production Decision

Use an Internet Gateway when:

* Hosting public websites.
* Deploying Internet-facing Load Balancers.
* Creating Bastion Hosts.
* Exposing REST APIs.
* Serving static websites.

Do **not** place:

* Databases
* Kubernetes Worker Nodes
* Backend Servers

directly in public subnets unless absolutely necessary.

---

# 🧠 Senior Engineer Tip

A common misconception is:

> "An Internet Gateway gives Internet access."

Not exactly.

An Internet Gateway **only provides the capability**.

Internet connectivity depends on:

* Route Table
* Security Group
* Network ACL
* Public IP
* Internet Gateway Attachment

All of these must be configured correctly.

---

# 💼 Common Interview Questions

### Q1. What is an Internet Gateway?

An AWS-managed component that connects a VPC to the Internet.

---

### Q2. Does creating an Internet Gateway automatically make a subnet public?

No.

The Route Table must contain:

```text
0.0.0.0/0 → Internet Gateway
```

---

### Q3. Can a private subnet communicate through an Internet Gateway?

No.

Private subnets use a NAT Gateway for outbound Internet access.

---

### Q4. Does an Internet Gateway perform NAT?

No.

The Internet Gateway simply enables communication.

NAT is performed by a NAT Gateway.

---

### Q5. Can multiple subnets use one Internet Gateway?

Yes.

One Internet Gateway can serve multiple public subnets within the same VPC.

---

### Q6. Is an Internet Gateway highly available?

Yes.

It is an AWS-managed, highly available service.

No additional scaling or maintenance is required.

---

# 🔥 Common Mistakes

❌ Creating an Internet Gateway is enough.

✅ You must also update the Route Table.

---

❌ Every public IP automatically works.

✅ A Route Table pointing to the Internet Gateway is also required.

---

❌ Internet Gateway provides security.

✅ Security is handled by:

* Security Groups
* Network ACLs

---

❌ Internet Gateway performs NAT.

✅ NAT Gateway performs Source NAT (SNAT).

---

# 🔍 Troubleshooting Guide

If Internet access isn't working:

1. Verify the Internet Gateway is attached to the VPC.
2. Check the Route Table.
3. Confirm the subnet association.
4. Verify the instance has a public IP (if required).
5. Check Security Groups.
6. Check NACLs.
7. Verify the default route:

```text
0.0.0.0/0 → Internet Gateway
```

---

# 💻 Commands to Verify

AWS CLI

```bash
aws ec2 describe-internet-gateways
```

```bash
aws ec2 describe-route-tables
```

Linux

```bash
ip route
```

```bash
curl ifconfig.me
```

```bash
ping 8.8.8.8
```

---

# 💼 Interview Cheat Sheet

Remember:

```text
Internet

↓

Internet Gateway

↓

Route Table

↓

Public Subnet

↓

EC2 / ALB
```

Key Facts

* IGW connects a VPC to the Internet.
* It is highly available and managed by AWS.
* It does not perform NAT.
* Route Tables determine whether a subnet is public.
* Public-facing AWS resources rely on an Internet Gateway.

---

# 📚 Summary

The Internet Gateway is the entry and exit point between an AWS VPC and the public Internet.

It works together with Route Tables, Security Groups, and Public IP addresses to enable Internet connectivity for public resources.

Understanding how the Internet Gateway interacts with other networking components is essential for designing secure and scalable cloud architectures.

---

# 🔗 Related Topics

⬅️ Previous: **Route Tables** → `../08-Route-Tables/README.md`

➡️ Next: **NAT Gateway** → `../10-NAT-Gateway/README.md`

### 📖 Recommended Reading

* Route Tables
* NAT Gateway
* CIDR & Subnetting
* Security Groups vs NACLs
* AWS VPC
* Browser to Server Flow
