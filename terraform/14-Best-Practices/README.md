# ✅ Terraform Best Practices

> **Terraform Best Practices are a set of guidelines that help build secure, maintainable, scalable, and production-ready Infrastructure as Code (IaC).**
>
> Following these practices reduces configuration errors, improves collaboration, simplifies maintenance, and enables reliable infrastructure deployments across multiple environments.

---

# 📖 Table of Contents

* What are Terraform Best Practices?
* Why Do We Need Best Practices?
* Project Structure
* Use Remote State
* Use Modules
* Version Control
* Variable Management
* Secrets Management
* Provider Versioning
* State Management
* Code Formatting & Validation
* Naming Conventions
* CI/CD Integration
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Terraform Best Practices?

Terraform Best Practices are recommended techniques for writing clean, reusable, secure, and production-ready Terraform code.

They help teams:

* Improve code quality
* Reduce duplication
* Increase security
* Simplify collaboration
* Prevent deployment failures

---

# 🎯 Why Do We Need Best Practices?

Without standards:

```text id="h4t9k2"
Developer A

↓

Writes Terraform

↓

Developer B

↓

Cannot Understand Code

↓

Configuration Errors
```

With Best Practices:

```text id="n7v3m5"
Standard Structure

↓

Reusable Code

↓

Easy Maintenance

↓

Reliable Deployments
```

---

# 📂 Use a Standard Project Structure

Organize Terraform files clearly.

Recommended structure:

```text id="k2x8p7"
terraform-project/

├── main.tf
├── providers.tf
├── variables.tf
├── outputs.tf
├── versions.tf
├── terraform.tfvars
├── backend.tf
├── modules/
└── environments/
```

Benefits:

* Easy navigation
* Better maintainability
* Team consistency

---

# 🌐 Use Remote State

Never use Local State for production.

Recommended:

```text id="b9m4r6"
Terraform

↓

Amazon S3

↓

terraform.tfstate

↓

DynamoDB

↓

State Lock
```

Benefits:

* Centralized State
* Team collaboration
* Backup
* State Locking
* Security

---

# 📦 Use Modules

Avoid duplicate code.

Instead of:

```text id="t6k2w1"
Project A

↓

Same Code

──────────────

Project B

↓

Copy Again
```

Use:

```text id="r5x8n3"
Reusable Module

↓

Project A

Project B

Project C
```

Benefits:

* Reusability
* Maintainability
* Standardization

---

# 🔀 Use Version Control

Always store Terraform code in Git.

Example workflow:

```text id="v8p3q4"
Developer

↓

Git Commit

↓

Pull Request

↓

Code Review

↓

Merge

↓

CI/CD
```

Never edit production code directly.

---

# 📝 Manage Variables Properly

Avoid hardcoding values.

Instead of:

```hcl id="g4n9t8"
instance_type = "t3.large"
```

Use:

```hcl id="c2r7m5"
instance_type = var.instance_type
```

Store values in:

* `terraform.tfvars`
* Environment variables
* CI/CD secrets

---

# 🔐 Never Store Secrets in Code

Avoid:

```hcl id="x8k4p2"
access_key = "AKIA..."

secret_key = "abcd..."
```

Use:

* IAM Roles
* AWS CLI credentials
* Environment variables
* Secret Managers (AWS Secrets Manager, HashiCorp Vault)

Benefits:

* Better security
* Easier credential rotation
* Reduced risk of credential leaks

---

# 📌 Pin Provider Versions

Always specify Provider versions.

Example:

```hcl id="q7v2n6"
terraform {

  required_providers {

    aws = {

      source  = "hashicorp/aws"

      version = "~> 5.0"

    }

  }

}
```

Benefits:

* Predictable deployments
* Stable builds
* Easier upgrades

---

# 💾 Manage State Carefully

Recommendations:

* Never edit `terraform.tfstate` manually.
* Store State remotely.
* Enable State Locking.
* Enable bucket versioning.
* Encrypt the State file.
* Restrict State file access.

The State file contains sensitive infrastructure information.

---

# 🧹 Format and Validate Code

Before deployment:

Format code:

```bash id="t1q5m8"
terraform fmt
```

Validate configuration:

```bash id="m6r3v7"
terraform validate
```

Preview changes:

```bash id="y4k8p1"
terraform plan
```

These commands help catch issues before deployment.

---

# 📛 Follow Naming Conventions

Use meaningful names.

Good examples:

```text id="d9w2n4"
aws_vpc.main

aws_instance.web

aws_security_group.app

aws_s3_bucket.logs
```

Avoid:

```text id="z5m7k3"
aws_instance.test

aws_instance.demo

aws_vpc.xyz
```

Consistent naming improves readability and maintenance.

---

# 🚀 Integrate with CI/CD

Typical workflow:

```text id="f8v1r6"
GitHub

↓

Pull Request

↓

terraform fmt

↓

terraform validate

↓

terraform plan

↓

Approval

↓

terraform apply
```

Benefits:

* Automated validation
* Code review
* Safe deployments
* Reduced human error

---

# ☁️ DevOps Perspective

Enterprise workflow:

```text id="p3k9w5"
Developer

↓

GitHub

↓

CI/CD Pipeline

↓

Remote State

↓

Terraform Plan

↓

Approval

↓

Terraform Apply

↓

AWS Infrastructure
```

Production deployments rely on automation, version control, and peer reviews.

---

# 🏭 Production Example

A company manages AWS infrastructure.

Project includes:

* VPC
* EC2
* RDS
* EKS
* ALB

Best Practices followed:

```text id="u6n4x2"
Git Repository

↓

Reusable Modules

↓

Remote State

↓

Versioned Providers

↓

CI/CD Pipeline

↓

Production Deployment
```

This ensures secure, repeatable, and scalable infrastructure management.

---

# 🎯 Common Interview Questions

### Why should Terraform code be modular?

Modules reduce duplication, improve reusability, and simplify maintenance.

---

### Why should Remote State be used?

Remote State enables centralized storage, team collaboration, backups, and State Locking.

---

### Why should Provider versions be pinned?

To ensure stable and predictable deployments by avoiding unexpected breaking changes.

---

### Why should secrets never be stored in Terraform code?

Hardcoded secrets can be exposed through version control and increase security risks.

---

### Which commands should be executed before `terraform apply`?

```bash id="a2m8v9"
terraform fmt

terraform validate

terraform plan
```

---

# 🔍 Useful Commands

Format configuration:

```bash id="k5r7n1"
terraform fmt
```

Validate configuration:

```bash id="e8p3w6"
terraform validate
```

Preview execution plan:

```bash id="r4x9m2"
terraform plan
```

Apply infrastructure:

```bash id="v7n5k8"
terraform apply
```

Destroy infrastructure:

```bash id="j1q6p4"
terraform destroy
```

---

# 📑 Interview Cheat Sheet

```text id="m9t2v7"
Git

↓

Modules

↓

Remote State

↓

Versioned Providers

↓

Variables

↓

terraform fmt

↓

terraform validate

↓

terraform plan

↓

terraform apply
```

Remember:

* **Use Modules for reusable code**
* **Store State remotely**
* **Enable State Locking**
* **Never hardcode secrets**
* **Pin Provider versions**
* **Use Git for version control**
* **Run `fmt`, `validate`, and `plan` before `apply`**
* **Follow a consistent project structure**

---

# 📚 Summary

Terraform Best Practices help teams write Infrastructure as Code that is secure, maintainable, and scalable. By following standardized project structures, using Modules, managing State correctly, protecting secrets, integrating with CI/CD pipelines, and validating configurations before deployment, organizations can build reliable infrastructure automation workflows.

For DevOps Engineers, these practices are essential because production environments require consistency, collaboration, security, and predictable deployments—not just working Terraform code.

---

# 🔗 Related Topics

⬅️ **Previous:** Provisioners → `../13-Provisioners/README.md`

➡️ **Next:** Troubleshooting → `../15-Troubleshooting/README.md`

### 📖 Recommended Reading

* Terraform Troubleshooting
* Terraform Modules
* Terraform Remote State
* Terraform Style Guide
* Terraform Official Documentation
