# 🔄 Terraform Lifecycle

> **Terraform Lifecycle is a set of meta-arguments that control how Terraform creates, updates, and destroys infrastructure resources.**
>
> By default, Terraform follows a standard lifecycle for every resource. However, in production environments, you often need finer control—for example, preventing accidental deletion of critical resources or creating replacement resources before destroying the old ones. Lifecycle rules make this possible.

---

# 📖 Table of Contents

* What is Lifecycle?
* Why Do We Need Lifecycle?
* Default Resource Lifecycle
* Lifecycle Meta-Arguments
* create_before_destroy
* prevent_destroy
* ignore_changes
* replace_triggered_by
* Lifecycle Architecture
* DevOps Perspective
* Production Example
* Interview Questions
* Best Practices
* Summary
* Related Topics

---

# ❓ What is Lifecycle?

A **Lifecycle** is a special configuration block inside a Terraform Resource that controls how Terraform handles the creation, update, replacement, and deletion of that resource.

It allows you to customize Terraform's default behavior.

General syntax:

```hcl id="b2l7v4"
resource "resource_type" "resource_name" {

  ...

  lifecycle {

    ...

  }

}
```

---

# 🎯 Why Do We Need Lifecycle?

Suppose you have a Production EC2 instance.

Normally:

```text id="d8k4r1"
Old EC2

↓

Destroy

↓

Create New EC2
```

This causes downtime.

Using Lifecycle:

```text id="q6m9w2"
Old EC2

↓

Create New EC2

↓

Traffic Shift

↓

Destroy Old EC2
```

No downtime.

---

# 🔄 Default Resource Lifecycle

Without any Lifecycle configuration:

```text id="g3t8x5"
Create Resource

↓

Modify Resource

↓

Destroy Resource
```

Terraform automatically decides whether to update or replace resources based on configuration changes.

---

# ⚙️ Lifecycle Meta-Arguments

Terraform provides several Lifecycle rules.

| Meta Argument         | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| create_before_destroy | Create replacement before deleting the old resource |
| prevent_destroy       | Prevent accidental deletion                         |
| ignore_changes        | Ignore selected attribute changes                   |
| replace_triggered_by  | Force replacement when another resource changes     |

---

# 🚀 create_before_destroy

By default:

```text id="k5n2p8"
Destroy

↓

Create
```

Using:

```hcl id="w7r4m1"
resource "aws_instance" "web" {

  ami           = "ami-xxxxxxxx"

  instance_type = "t3.micro"

  lifecycle {

    create_before_destroy = true

  }

}
```

Terraform changes the workflow to:

```text id="f9x3v7"
Create New Resource

↓

Move Traffic

↓

Destroy Old Resource
```

Use Cases:

* EC2
* Load Balancers
* Auto Scaling
* High Availability Deployments

---

# 🛑 prevent_destroy

Some resources should never be deleted accidentally.

Example:

```hcl id="p4k8t2"
resource "aws_s3_bucket" "logs" {

  bucket = "company-prod-logs"

  lifecycle {

    prevent_destroy = true

  }

}
```

Now if someone runs:

```bash id="z2q6n9"
terraform destroy
```

Terraform returns an error instead of deleting the bucket.

Use Cases:

* Production Databases
* S3 Backup Buckets
* Critical Storage
* Logging Infrastructure

---

# 👀 ignore_changes

Sometimes external systems modify resources.

Example:

```hcl id="n7v5r4"
resource "aws_instance" "web" {

  tags = {

    Environment = "Production"

  }

  lifecycle {

    ignore_changes = [

      tags

    ]

  }

}
```

If someone changes the tags manually:

Terraform ignores those changes instead of attempting to revert them.

Common Use Cases:

* Tags
* Auto Scaling
* External Automation
* Cloud Policies

---

# 🔁 replace_triggered_by

Force a resource replacement when another resource changes.

Example:

```hcl id="c8w2p6"
resource "aws_instance" "web" {

  lifecycle {

    replace_triggered_by = [

      aws_launch_template.app

    ]

  }

}
```

If the Launch Template changes, Terraform automatically replaces the EC2 instance.

---

# 🏗️ Lifecycle Architecture

```text id="v5m1q8"
Terraform Configuration
          │
          ▼
Resource Block
          │
          ▼
Lifecycle Rules
          │
          ▼
Terraform Plan
          │
          ▼
Cloud Infrastructure
```

Lifecycle rules modify Terraform's default execution plan.

---

# ☁️ DevOps Perspective

Production deployment workflow:

```text id="r3x7k4"
Git Push

↓

CI/CD Pipeline

↓

terraform plan

↓

Lifecycle Evaluation

↓

terraform apply

↓

Infrastructure Updated
```

Lifecycle settings help reduce downtime, protect critical resources, and improve deployment safety.

---

# 🏭 Production Example

A company deploys a web application.

Infrastructure:

* Application Load Balancer
* EC2 Instances
* Auto Scaling Group
* RDS Database

Configuration:

```text id="m6t9v2"
EC2

↓

create_before_destroy

──────────────

Database

↓

prevent_destroy

──────────────

Tags

↓

ignore_changes
```

Benefits:

* Zero-downtime deployments
* Protection against accidental deletion
* Stable infrastructure management

---

# 🎯 Common Interview Questions

### What is Terraform Lifecycle?

Lifecycle is a special configuration block that controls how Terraform creates, updates, and destroys resources.

---

### What does `create_before_destroy` do?

Terraform creates the replacement resource before deleting the existing one, minimizing downtime.

---

### What does `prevent_destroy` do?

It prevents Terraform from accidentally deleting a resource.

---

### What does `ignore_changes` do?

It tells Terraform to ignore changes to specified resource attributes.

---

### What does `replace_triggered_by` do?

It forces a resource to be replaced when another specified resource changes.

---

# 🔍 Useful Commands

Preview changes:

```bash id="x4p8m7"
terraform plan
```

Apply changes:

```bash id="n2v6q5"
terraform apply
```

Destroy infrastructure:

```bash id="f7r3w9"
terraform destroy
```

Validate configuration:

```bash id="k5m1x8"
terraform validate
```

---

# 📑 Interview Cheat Sheet

```text id="q9t4r6"
Resource
     │
     ▼
Lifecycle
     │
 ┌────┼──────────────┐
 ▼    ▼              ▼
Create Before    Prevent    Ignore
Destroy          Destroy    Changes
```

Remember:

* **Lifecycle customizes Terraform's default behavior**
* **`create_before_destroy` reduces downtime**
* **`prevent_destroy` protects critical resources**
* **`ignore_changes` ignores external modifications**
* **`replace_triggered_by` forces resource replacement**
* **Lifecycle is configured inside the Resource block**
* **Widely used in production environments**

---

# 📚 Summary

Terraform Lifecycle provides advanced control over how resources are managed throughout their lifecycle. By using Lifecycle meta-arguments, engineers can implement safer deployments, prevent accidental data loss, reduce downtime, and handle external changes more effectively.

For DevOps Engineers, understanding Lifecycle is essential because production infrastructure often requires behavior beyond Terraform's default resource management.

---

# 🔗 Related Topics

⬅️ **Previous:** Workspaces → `../11-Workspaces/README.md`

➡️ **Next:** Provisioners → `../13-Provisioners/README.md`

### 📖 Recommended Reading

* Terraform Provisioners
* Terraform Modules
* Terraform State
* Terraform Official Documentation
* HashiCorp Lifecycle Meta-Arguments
