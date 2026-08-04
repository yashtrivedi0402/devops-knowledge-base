# 📦 Terraform Modules

> **Modules are reusable containers of Terraform configuration that group together multiple resources into a single logical unit.**
>
> Instead of writing the same Terraform code repeatedly, Modules allow you to write it once and reuse it across multiple projects and environments, making Infrastructure as Code more maintainable, scalable, and consistent.

---

# 📖 Table of Contents

* What are Modules?
* Why Do We Need Modules?
* Problems Without Modules
* Module Architecture
* Module Structure
* Root Module vs Child Module
* Creating a Module
* Using a Module
* Module Registry
* Module Versioning
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Modules?

A **Module** is a collection of Terraform configuration files that work together to create a specific infrastructure component.

Examples:

* VPC Module
* EC2 Module
* Security Group Module
* RDS Module
* EKS Module

A module can contain:

* Resources
* Variables
* Outputs
* Local values

Instead of copying code, Terraform allows you to reuse modules.

---

# 🎯 Why Do We Need Modules?

Imagine deploying infrastructure for:

* Development
* Testing
* Staging
* Production

Without Modules:

```text id="a8k2x7"
VPC Code

↓

Copy

↓

Paste

↓

Modify

↓

Repeat
```

Problems:

* Duplicate code
* Difficult maintenance
* Higher chance of errors
* Hard to scale

With Modules:

```text id="m5v4r8"
VPC Module

↓

Reuse

↓

Development

Testing

Staging

Production
```

Write once, use many times.

---

# ❌ Problems Without Modules

Suppose your infrastructure contains:

* VPC
* Public Subnets
* Private Subnets
* Route Tables
* Internet Gateway
* NAT Gateway

Without Modules:

```text id="y7d3n6"
Project A

500 Lines

──────────────

Project B

Copy Same 500 Lines

──────────────

Project C

Copy Again
```

Updating one configuration requires updating every project manually.

---

# 🏗️ Module Architecture

```text id="r4m7p1"
             Root Module
                  │
     ┌────────────┼────────────┐
     ▼            ▼            ▼
 VPC Module   EC2 Module   RDS Module
     │            │            │
     ▼            ▼            ▼
AWS Resources AWS Resources AWS Resources
```

The Root Module calls Child Modules, which create infrastructure.

---

# 📂 Module Structure

Typical structure:

```text id="k8q2t5"
terraform-project/

├── main.tf
├── variables.tf
├── outputs.tf

└── modules/
      │
      ├── vpc/
      │     ├── main.tf
      │     ├── variables.tf
      │     └── outputs.tf
      │
      ├── ec2/
      │     ├── main.tf
      │     ├── variables.tf
      │     └── outputs.tf
      │
      └── security-group/
            ├── main.tf
            ├── variables.tf
            └── outputs.tf
```

Each module is self-contained and reusable.

---

# 🌱 Root Module vs Child Module

### Root Module

The directory where Terraform commands are executed.

Example:

```bash id="v2m6r9"
terraform init

terraform plan

terraform apply
```

This is the Root Module.

---

### Child Module

Modules called from the Root Module.

Example:

```text id="p4x8k3"
modules/

↓

vpc

↓

ec2

↓

rds
```

The Root Module orchestrates Child Modules.

---

# 🚀 Creating a Module

Example:

```hcl id="j5t8n1"
module "vpc" {

  source = "./modules/vpc"

  cidr_block = "10.0.0.0/16"

}
```

Explanation:

* **module** → Declares a module.
* **source** → Path to the module.
* **cidr_block** → Input variable passed to the module.

---

# 📥 Using Module Outputs

Modules can return values.

Example:

```hcl id="z9k4w7"
output "vpc_id" {

  value = aws_vpc.main.id

}
```

Use it in the Root Module:

```hcl id="x7r3p6"
module.vpc.vpc_id
```

This allows one module to share information with another.

---

# 🌍 Terraform Module Registry

Terraform provides an official Module Registry.

Popular modules include:

* AWS VPC
* EKS
* RDS
* Security Groups
* IAM

Registry:

```text id="q6y8m2"
https://registry.terraform.io
```

Instead of building everything from scratch, teams often use community-maintained modules.

---

# 📌 Module Versioning

Specify module versions to ensure stable deployments.

Example:

```hcl id="n3v7r4"
module "vpc" {

  source  = "terraform-aws-modules/vpc/aws"

  version = "5.0.0"

}
```

Benefits:

* Predictable deployments
* Easy upgrades
* Rollback support
* Consistent environments

---

# ☁️ DevOps Perspective

Production workflow:

```text id="g4t9x8"
GitHub Repository

↓

Reusable Modules

↓

terraform plan

↓

terraform apply

↓

AWS Infrastructure
```

Large organizations maintain internal module libraries for:

* Networking
* Compute
* Databases
* Kubernetes
* Monitoring

This standardizes infrastructure across teams.

---

# 🏭 Production Example

An enterprise deploys infrastructure for multiple applications.

Instead of rewriting code:

```text id="u5r2n9"
Application A

↓

VPC Module

↓

EC2 Module

↓

RDS Module

──────────────

Application B

↓

Same Modules

──────────────

Application C

↓

Same Modules
```

Only input variables change.

The infrastructure remains standardized.

---

# 🎯 Common Interview Questions

### What is a Terraform Module?

A Module is a reusable collection of Terraform configuration files used to create and manage infrastructure.

---

### What is the difference between a Root Module and a Child Module?

* **Root Module** → The main Terraform configuration where commands are executed.
* **Child Module** → A reusable module called by the Root Module.

---

### Why are Modules important?

Modules reduce code duplication, improve maintainability, and promote reusability.

---

### Can Modules return values?

Yes.

Modules expose values through Outputs, which can be accessed by other modules or the Root Module.

---

### Where can you find reusable Modules?

The Terraform Module Registry:

```text id="c8m1p5"
https://registry.terraform.io
```

---

# 🔍 Useful Commands

Initialize project:

```bash id="t6w4y9"
terraform init
```

Plan deployment:

```bash id="h2k8v1"
terraform plan
```

Apply infrastructure:

```bash id="p9x5r7"
terraform apply
```

View outputs:

```bash id="b4n2q6"
terraform output
```

Validate configuration:

```bash id="r8m7k3"
terraform validate
```

---

# 📑 Interview Cheat Sheet

```text id="m7y4q2"
Root Module
      │
      ▼
Child Modules
      │
      ▼
Resources
      │
      ▼
Infrastructure
```

Remember:

* **Modules make Terraform reusable**
* **Root Module calls Child Modules**
* **Modules contain Resources, Variables, and Outputs**
* **Use Outputs to share values**
* **Use the Terraform Registry for reusable Modules**
* **Always version production Modules**
* **Modules reduce duplication and simplify maintenance**

---

# 📚 Summary

Modules are one of Terraform's most powerful features, enabling reusable, modular, and maintainable Infrastructure as Code. By encapsulating infrastructure into reusable building blocks, Modules reduce duplication, improve consistency, and simplify large-scale deployments.

For DevOps Engineers, Modules are essential because production Terraform projects are almost always organized around reusable Modules rather than large monolithic configuration files.

---

# 🔗 Related Topics

⬅️ **Previous:** Remote State → `../09-Remote-State/README.md`

➡️ **Next:** Workspaces → `../11-Workspaces/README.md`

### 📖 Recommended Reading

* Terraform Workspaces
* Terraform Variables
* Terraform Outputs
* Terraform Registry
* Terraform Official Documentation
