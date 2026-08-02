# 🏗️ Terraform Architecture

> **Terraform follows a client-based architecture where the Terraform CLI interacts with cloud providers through Providers and APIs to provision and manage infrastructure.**
>
> Understanding Terraform's architecture helps explain **how Infrastructure as Code works behind the scenes**, making it easier to troubleshoot, optimize deployments, and work with production environments.

---

# 📖 Table of Contents

* What is Terraform Architecture?
* Why Do We Need It?
* Terraform Components
* Terraform Workflow
* Architecture Diagram
* Terraform Providers
* Terraform State
* Terraform Plugins
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What is Terraform Architecture?

Terraform Architecture describes how Terraform communicates with cloud platforms to create, update, and destroy infrastructure.

Terraform itself **does not create resources directly**.

Instead, it:

* Reads Terraform configuration files
* Communicates with Providers
* Calls Cloud Provider APIs
* Stores infrastructure state
* Tracks changes over time

---

# 🎯 Why Do We Need Terraform Architecture?

When you run:

```bash
terraform apply
```

Terraform performs several internal operations before creating infrastructure.

It needs to:

* Read configuration files
* Identify the cloud provider
* Download required plugins
* Compare desired infrastructure with the current state
* Generate an execution plan
* Execute API requests

Understanding this workflow helps diagnose deployment failures and optimize infrastructure management.

---

# 🏗️ Terraform Architecture

```text
                 Developer
                      │
                      ▼
              Terraform CLI
                      │
          Reads *.tf Configuration
                      │
                      ▼
             Terraform Core
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
     AWS Provider  Azure Provider  GCP Provider
        │             │             │
        ▼             ▼             ▼
     AWS API      Azure API      GCP API
        │             │             │
        ▼             ▼             ▼
 Cloud Infrastructure Resources
```

Terraform Core coordinates the workflow while Providers communicate with cloud APIs.

---

# 🧩 Terraform Components

Terraform consists of several important components.

---

## 1️⃣ Terraform CLI

The command-line interface used to execute Terraform commands.

Examples:

```bash
terraform init

terraform plan

terraform apply

terraform destroy
```

---

## 2️⃣ Terraform Core

Terraform Core is the brain of Terraform.

Responsibilities:

* Reads configuration files
* Builds dependency graph
* Compares current and desired state
* Generates execution plan
* Coordinates Providers

---

## 3️⃣ Providers

Providers allow Terraform to communicate with different platforms.

Examples:

* AWS
* Azure
* Google Cloud
* Kubernetes
* Docker
* GitHub
* Cloudflare

Terraform downloads the required Provider during initialization.

---

## 4️⃣ Plugins

Each Provider is installed as a plugin.

Example:

```text
Terraform

↓

AWS Provider Plugin

↓

AWS API
```

Plugins make Terraform extensible without changing Terraform Core.

---

## 5️⃣ Cloud APIs

Terraform never creates infrastructure directly.

Instead:

```text
Terraform

↓

Provider

↓

Cloud API

↓

Infrastructure
```

Every cloud resource is created through the provider's API.

---

## 6️⃣ State File

Terraform maintains a **State File** to track infrastructure.

The state contains:

* Resource IDs
* Current configuration
* Dependencies
* Metadata

Without the state file, Terraform cannot determine what already exists.

---

# 🔄 Terraform Workflow

The internal workflow is:

```text
Write Configuration

↓

terraform init

↓

Download Providers

↓

terraform plan

↓

Compare State

↓

Execution Plan

↓

terraform apply

↓

Provider API Calls

↓

Infrastructure Created

↓

State Updated
```

---

# ☁️ Provider Workflow

Example using AWS:

```text
main.tf

↓

AWS Provider

↓

AWS SDK

↓

AWS API

↓

EC2

VPC

S3

IAM

Load Balancer
```

Terraform uses the AWS Provider to translate HCL into AWS API requests.

---

# 💾 Role of the State File

Terraform compares two things:

```text
Desired State

(main.tf)

↓

Current State

(terraform.tfstate)

↓

Difference

↓

Apply Changes
```

This ensures Terraform only creates, updates, or deletes resources when necessary.

---

# ☁️ DevOps Perspective

Typical production workflow:

```text
Developer

↓

GitHub Repository

↓

CI/CD Pipeline

↓

terraform init

↓

terraform plan

↓

Approval

↓

terraform apply

↓

AWS Infrastructure

↓

terraform.tfstate
```

The state file is usually stored remotely (e.g., S3 with DynamoDB locking) to support team collaboration.

---

# 🏭 Production Example

A company wants to deploy a web application infrastructure.

Resources:

* VPC
* Public Subnets
* EC2 Instances
* Application Load Balancer
* Security Groups
* IAM Roles

Deployment flow:

```text
Terraform Code

↓

Terraform Core

↓

AWS Provider

↓

AWS APIs

↓

Infrastructure Created

↓

State Saved
```

Later, if an additional EC2 instance is required:

```text
Update Code

↓

terraform plan

↓

terraform apply

↓

Only New Resource Created
```

Terraform avoids recreating unchanged resources.

---

# 🎯 Common Interview Questions

### What are the main components of Terraform Architecture?

* Terraform CLI
* Terraform Core
* Providers
* Plugins
* Cloud APIs
* State File

---

### What is Terraform Core?

Terraform Core reads configuration files, manages dependencies, compares state, and coordinates Providers.

---

### What is a Provider?

A Provider is a plugin that enables Terraform to interact with a specific platform such as AWS, Azure, or Kubernetes.

---

### Does Terraform communicate directly with AWS?

No.

Terraform communicates with the **AWS Provider**, which then interacts with the AWS APIs.

---

### Why is the State File important?

The state file tracks existing infrastructure and helps Terraform determine what changes need to be applied.

---

# 🔍 Useful Commands

```bash
terraform init

terraform providers

terraform plan

terraform apply

terraform show

terraform state list

terraform state show <resource>

terraform destroy
```

---

# 📑 Interview Cheat Sheet

```text
Terraform CLI
      │
      ▼
Terraform Core
      │
      ▼
Provider Plugin
      │
      ▼
Cloud API
      │
      ▼
Infrastructure
      │
      ▼
State File
```

Remember:

* **Terraform Core is the brain of Terraform**
* **Providers communicate with cloud platforms**
* **Plugins extend Terraform functionality**
* **Terraform uses cloud APIs to manage resources**
* **State File tracks existing infrastructure**
* **Terraform compares desired state with current state before making changes**

---

# 📚 Summary

Terraform Architecture is built around Terraform Core, Providers, Plugins, and Cloud APIs working together to automate infrastructure provisioning. By maintaining a state file and comparing the desired infrastructure with the current environment, Terraform ensures consistent, predictable, and repeatable deployments.

For DevOps Engineers, understanding Terraform Architecture is essential because it forms the foundation for Infrastructure as Code, enabling scalable cloud automation, collaboration, and efficient infrastructure management.

---

# 🔗 Related Topics

⬅️ **Previous:** Installation → `../02-Installation/README.md`

➡️ **Next:** Providers → `../04-Providers/README.md`

### 📖 Recommended Reading

* Terraform Providers
* Terraform Resources
* Terraform State
* HashiCorp Configuration Language (HCL)
* Terraform Official Documentation
