# 📤 Terraform Outputs

> **Outputs in Terraform are used to display important information about the infrastructure after it has been created or updated.**
>
> Outputs make it easy to retrieve resource details such as IP addresses, DNS names, IDs, ARNs, and URLs, which can be used by users, other Terraform configurations, or CI/CD pipelines.

---

# 📖 Table of Contents

* What are Outputs?
* Why Do We Need Outputs?
* Output Architecture
* Declaring Outputs
* Using Outputs
* Sensitive Outputs
* Outputs in Modules
* DevOps Perspective
* Production Example
* Interview Questions
* Useful Commands
* Summary
* Related Topics

---

# ❓ What are Outputs?

**Outputs** are values that Terraform displays after executing `terraform apply`.

They provide information about the infrastructure Terraform has created.

Common output values include:

* EC2 Public IP
* Private IP
* Instance ID
* VPC ID
* Load Balancer DNS
* S3 Bucket Name
* IAM Role ARN

Outputs make it easier to access these values without manually searching the cloud console.

---

# 🎯 Why Do We Need Outputs?

Imagine you create an EC2 instance.

Without Outputs:

```text id="r5m2y8"
terraform apply

↓

Login to AWS Console

↓

Find EC2

↓

Copy Public IP
```

With Outputs:

```text id="x8p4c1"
terraform apply

↓

Public IP Displayed Automatically
```

Outputs save time and simplify automation.

---

# 🏗️ Output Architecture

```text id="v3t9q7"
Terraform Resources
        │
        ▼
Output Block
        │
        ▼
terraform apply
        │
        ▼
Terminal Output
```

Outputs retrieve values from Resources and display them after deployment.

---

# 🚀 Declaring Outputs

Basic syntax:

```hcl id="q7k4e9"
output "<OUTPUT_NAME>" {

  value = <EXPRESSION>

}
```

Example:

```hcl id="b2m8r5"
output "public_ip" {

  value = aws_instance.web.public_ip
}
```

After deployment:

```text id="d6y3w1"
Outputs:

public_ip = "13.234.120.45"
```

---

# 🔗 Referencing Resource Attributes

Outputs commonly reference Resource attributes.

Example:

```hcl id="h5n7u2"
output "instance_id" {

  value = aws_instance.web.id
}
```

Other examples:

```hcl id="w9x4j8"
aws_instance.web.public_ip

aws_instance.web.private_ip

aws_instance.web.id

aws_vpc.main.id

aws_s3_bucket.logs.bucket
```

Terraform reads these values from the state file after creating the resources.

---

# 🔒 Sensitive Outputs

Some values should not be displayed.

Example:

```hcl id="f4z8n6"
output "database_password" {

  value     = var.db_password

  sensitive = true
}
```

Terraform hides sensitive values from normal output.

Use this for:

* Passwords
* API Keys
* Tokens
* Secrets

---

# 📦 Outputs in Modules

Outputs are commonly used to share values between Modules.

Example:

```text id="n2q7m4"
Network Module

↓

Outputs VPC ID

↓

Application Module

↓

Uses VPC ID
```

This allows Modules to communicate while remaining independent.

---

# ☁️ DevOps Perspective

Typical workflow:

```text id="g8r3v1"
terraform apply

↓

Infrastructure Created

↓

Outputs Generated

↓

CI/CD Pipeline

↓

Application Deployment
```

Examples:

* Pass Load Balancer DNS to deployment scripts.
* Provide VPC ID to another Terraform module.
* Share database endpoint with application teams.

---

# 🏭 Production Example

A company provisions infrastructure on AWS.

Terraform creates:

* VPC
* EC2
* Application Load Balancer
* RDS Database

Outputs:

```text id="t4m6w9"
VPC ID

↓

EC2 Public IP

↓

ALB DNS Name

↓

Database Endpoint
```

The application deployment pipeline uses these values automatically.

---

# 🎯 Common Interview Questions

### What are Terraform Outputs?

Outputs display useful information about Terraform-managed infrastructure after deployment.

---

### Where are Outputs declared?

In the `outputs.tf` file.

---

### How do Outputs retrieve values?

They reference Resource attributes such as IDs, IP addresses, DNS names, or ARNs.

---

### What are Sensitive Outputs?

Outputs marked with `sensitive = true` hide confidential information such as passwords and API keys.

---

### Why are Outputs important?

Outputs make infrastructure information easily available to users, modules, and automation pipelines.

---

# 🔍 Useful Commands

Display all outputs:

```bash id="k3f8n5"
terraform output
```

Display a specific output:

```bash id="a6r2w7"
terraform output public_ip
```

Display output in JSON format:

```bash id="m9v4c1"
terraform output -json
```

Apply infrastructure:

```bash id="p5t8x2"
terraform apply
```

---

# 📑 Interview Cheat Sheet

```text id="c8y1n6"
Terraform Resources
        │
        ▼
Output Block
        │
        ▼
terraform apply
        │
        ▼
Display Values
```

Remember:

* **Outputs display infrastructure information**
* **Declared in `outputs.tf`**
* **Reference Resource attributes**
* **Use `terraform output` to view values**
* **Sensitive Outputs hide confidential data**
* **Outputs enable communication between Modules and automation pipelines**

---

# 📚 Summary

Outputs are an important Terraform feature that expose useful information about deployed infrastructure. They eliminate the need to manually retrieve resource details and make Terraform configurations easier to integrate with CI/CD pipelines, other Modules, and operational workflows.

For DevOps Engineers, Outputs are essential because they simplify automation, improve infrastructure visibility, and enable seamless integration between different stages of the deployment process.

---

# 🔗 Related Topics

⬅️ **Previous:** Variables → `../06-Variables/README.md`

➡️ **Next:** State → `../08-State/README.md`

### 📖 Recommended Reading

* Terraform State
* Terraform Modules
* Terraform Variables
* HashiCorp Configuration Language (HCL)
* Terraform Official Documentation
